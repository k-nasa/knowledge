# gRPC の話

ここらへんを重点的に説明していく

- gRPC の説明（特に HTTP JSON との違い）
- そもそも gRPC 化と k8s の組み合わせの何が難しい
- 一般に k8s でやるならどうするか

## まず、gRPC というのは何か？

gRPC は google が開発した RPC フレームワークです。client-server 間の通信に利用され、client が特定の method を呼び出すと、それが server への Request となり、server で処理された結果が Response として返され RPC の返り値になります。
gRPC では、IDL（インターフェース定義言語）を使ってあらかじめ API 仕様を定義し、そこから server-client に必要なソースコードを生成する。IDL はデフォルトでは protocol buffers を使用しますが、json を使用することも出来るようです。

## http と何が違うのか

では http を使用して、json を返す方法とは何が違うのでしょうか?

gRPC は HTTP2 の上に構築されているので、意識せずに HTTP2 の恩恵を受けることができます。具体的な恩恵としては次のようなものがあるかと思います。

- 1 つの TCP connection での multiplexing
- header comporession
- etc(調べてみて下さい)

4 つの通信方式を取り扱うことが出来る

- Unary RPCs 1:1
- Server Streaming RPCs 1:多
- Client Streaming RPCs 多:1
- Duplex Streaming RPCs 多:多

## k8s と gRPC の組み合わせの難しさ

次のブログが参考になりました。(ここでの詳細な説明は放棄します)
https://deeeet.com/writing/2018/03/30/kubernetes-grpc/

> Kubernetes Service は L4 の Load balancer（LB）であること
> gRPC はコネクションを使いまわすこと

この 2 文にすべてが詰まっていますね。

k8s の pods は生成、破棄を繰り返します。そのたびに違う IP アドレスが割り当てられます。
しかし、pod へのアクセスに使われるのはこの IP アドレスではありません、service が管理している VIP を返すことになります。この VIP は pod への仮想 IP アドレスと実際の pod の IP アドレスを紐付けた、アドレステーブルになっています。

例えば、次のような VIP テーブルがあったとします。http 通信を普通に行っている場合は pod へのリクエストのたびにコネクションを張ることになるので、返ってくる pod のアドレスは`192.168.0.1`か`192.168.0.2`どちらになるかはその時の状況によります。(service によってロードバランシングされているので)

| VIP         | pod 名 | pods の実アドレス |
| ----------- | ------ | ----------------- |
| 192.168.0.1 | A      | xxx.yyy.0.0       |
| 192.168.0.2 | B      | xxx.zzz.0.0       |

しかし、gRPC では一度貼ったコネクションを使い回すので、最初に pod A にアクセスしたとしたら常に pod A にリクエストを投げ続けることになります。

なので、何も考えずに k8s 上で gRPC を使うと問題が出てしまう場合があります。

## gRPC を k8s でやるならばどうするか？

- 1 つは gRPC の clientLoadbalancing を使う方法 https://github.com/grpc/grpc/blob/master/doc/load-balancing.md
- L7 load blancer があれば解決するのでは?

envoy というやつで L7 load blancing 出来るらしい
