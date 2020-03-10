# データ構造についてのメモ

## Array (静的配列)

![static array](https://www.interviewcake.com/images/svgs/array__preview.svg?bust=204)

### 強み

インデックスアクセスの速度が早い。 O(1)
１要素のサイズが決まっているため、指定されたインデックスの要素の取得は高速である。

配列の最後に新しい要素を追加するには O(1)で行ける

### 弱み

事前に格納する要素の数を指定する必要がある。 -> 固定長のため

挿入と削除では最大 O(n)となる。
理由としては、例えば先頭に挿入する場合、すべての要素を 1 つずらす必要があるため

## Dynamic Array (動的配列)

![dynamic array](https://www.interviewcake.com/images/svgs/dynamic_array__preview.svg?bust=204)

配列はサイズが固定されてしまっていたが、ダイナミックアレイは要素を追加すると、サイズが拡張される。

### 強み

- インデックスアクセスが高速。配列と一緒。
- サイズが可変である

### 弱み

- 最後に新しい要素を追加するのは O(1)。だが、空きスペースがない場合は拡張する必要があるため O(n)になる。
- 配列と同様、挿入と削除は最大で O(n)。

## Linked List (リンクリスト)

![linked list](https://www.interviewcake.com/images/svgs/linked_list__nodes_and_pointers_labeled_head_and_tail.svg?bust=204)

### 強み

- リンクリストの両端に要素を追加するのは O(1)で行ける。
- 最初の要素を削除することも O(1)
- サイズが可変である。

### 弱み

- インデックスアクセスが高コストである。 先頭からたどっていく必要があるため

### 用途

キューやスタックは両端へのアクセス(操作)を高速に行いたいのでリンクリストが内部的には使用されている

## Queue (キュー)

![queue](https://www.interviewcake.com/images/svgs/queue__preview.svg?bust=204)

FIFO のやつ

### 強み

- すべてのキュー操作は O(1)

## Stack (スタック)

LIFO のやつ (もしくは FILO)

![stack](https://www.interviewcake.com/images/svgs/stack__preview.svg?bust=204)

### 強み

- すべてのスタック操作は O(1)

## Hash Table (ハッシュマップ)

### 強み

- 高速検索。key でアクセスする場合は O(1)である場合が多い
- ハッシュ可能なら様々なデータ型をキーに出来る。

### 弱み

- key でのアクセス時に最悪の場合に O(n)かかってしまう
- 順不同
- ある値を検索する場合は O(n)

## Tree (ツリー)

![tree](https://www.interviewcake.com/images/svgs/trees__animal_classes.svg?bust=204)

### ツリートラバーサル

#### 幅優先探索 (BFS)

この順序で探索していく

![BFS](https://www.interviewcake.com/images/svgs/trees__bfs.svg?bust=204)

#### 深さ優先探索 (DFS)

この順序で探索していく

![DFS](https://www.interviewcake.com/images/svgs/trees__dfs.svg?bust=204)
