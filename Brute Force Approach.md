---
lang: ja-jp
title: 総当たり探索手法
tags: AI, fai2, DFS, BFS
---
総当たり探索手法
===
* 総当たり手法
    * 深さ優先探索(DFS)
    * 幅優先探索(BFS)
    * 反復深化探索(IDDFS)
* 発見的手法
* 反復改良法
## 深さ優先探索
左側部分グラフから順に最深部まで探索していく。
### アルゴリズム
*open*はノードの格納領域、**stackで表現**
1.  *open*にルートノードを加える。
2.  *open*が空の場合、探索失敗、実行終了。
3.  *open*から1つのノード*N*を取り出す。
4.  *N*がゴールノードの場合、探索成功。実行終了。
5.  *N*の全ての子ノードを*open*に追加。2.へ。

```clike
DFS(){
    stack open;
    push(open, root);
    while(1){
        if(isNull?(open)) exit(Falure);
        N = pop(open);
        if(isGoal?(N)) exit(Success);
        for(child : N) push(open, child);	
    }
}
```

## 幅優先探索
ある深さにあるノードすべてを探索してまた次の深さへと探索していく。
### アルゴリズム
*open*は**queueで表現**
```clike
BFS(){
    queue open;
    enqueue(open, root);
    while(1){
        if(isNull?(open)) exit(Failure);
        N = dequeue(open);
        if(isGoal?(N)) exit(Success);
        for(child : N) enqueue(open, child);
    }
}
```

### 探索コスト
*コスト*：計算量(ノード展開数)とメモリ使用量
ノード分岐数を$b$、深さを$d$とした時、最悪の場合を想定した計算量は、

$$b+b^2+b^3+\dots +b^d = O(b^{d+1})$$

であり、表にまとめると以下。
|          | ノード展開数 |メモリ使用量|
| :------: | :--------: | :------: |
| **DFS**  |$O(b^{d+1})$| $bd$     |
| **BFS**  |$O(b^{d+1})$| $b^d$    |

## 反復深化探索
### アルゴリズム
*DFS*において深さに制限をつけ、解が見つかるまで制限を徐々に緩めていく。
計算量:$O(b^d)$、メモリ使用量:$O(bd)$で、探索空間が大きく、深さが知られていない時に特に有効。
1. *cutoff=1*
2. ルートノードを*open*に入れる。
3. *open*が空なら*cutoff*に1足して2.へ。
4. *open*から先頭のノード*N*を取り出す。
5. *N*がゴールノードの場合、*探索成功*、実行終了。
6. *N*の子ノードのうち*cutoff*よりも浅いものすべてを*open*に追加。

```clike
IDDFS(){
    stack open;
    cutoff = 1;
p2:
    push(open, root);
    while(1){
        if(isNull?(open)){
            cutoff++;
            goto p2;
        }
        N = pop(open);
        if(isGoal?(N)) exit(Success);
        for(child : N)
            if(child->depth < cutoff) push(open, child);
    }
}
```

### ノード展開数の比較
#### DFSまたはBFS
$1+b+b^2+\dots +b^d=\sum_0^d b^i$

#### 反復深化探索
$(d+1)\times 1+db+(d-1)b^2+\dots +2b^{d-1}+b^d=\sum_0^d(d-i+1)b^i$

