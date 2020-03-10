## スタックとヒープについて書く

### まとめ

- スタックのほうが高速で、管理が容易です。
- しかし、自由にメモリを確保、解放することができず、サイズの変更もできません。
- ヒープは柔軟に使用できる分、領域管理にコストが掛かってしまいます。
- メモリを確保しないことを第一に考え、次にスタック、最後にヒープを使うのがいいでしょう。

## スタック(Stack)

## ヒープ (heap)

todo!() // そのうち書くぞい

## 参考文献

- https://keens.github.io/blog/2017/04/30/memoritosutakkutohi_puto/

- https://doc.rust-jp.rs/the-rust-programming-language-ja/1.6/book/the-stack-and-the-heap.html
