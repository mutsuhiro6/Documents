---
lang: ja-jp
title: 反復改良法
tags: AI, fai4, ミニマックス法
---
反復改良法
===
状態の評価(コスト)関数を定義し、コストがより小さい方へ探索し、準最適な解を求める。
* 総当たり手法
* 発見的手法
* **反復改良法**
    * 勾配降下法(Gradient Descent)
    * 焼きなまし法(Simulated Annealing)
    * min-max法
        * αβカット
## 勾配降下法(Gradient Descent)
fai4.pdf(page 2)の図を参考。
### アルゴリズム
$Cost(N)$をノード$N$におけるコストとする。
1. ルートノードを*N*とする。
2. *N*がゴールノードであれば成功、実行終了。
3. *N*が子ノードを持たなければ失敗、実行終了。
4. *N*の子ノード*Nc*のうち$Cost(Nc)$が最小のものを*N*'とする。
5. $Cost(N')<Cost(N)$のとき、*N* = *N*'として、2へ。そうでなければ失敗、実行終了。

**局所解しか得られない**ので初期値を変更して何度か実行する。
```clike
Gradient_Descent(node Root){
    node N = Root;
    node Nd;
    while(true){
        if(N is goal) exit(Success);
        else if(N has No child) exit(Failure);
        Nd = child of N with minimum cost;
        if(Cost(Nd) < Cost(N)) N = Nd;
        else exit(Failure);
    }
}

main(){
    Gradient_Descent(Root1);
    Gradient_Descent(Root2);
    ...
    use the best result of Gradient_Descent(RootN).
}
```
## 焼きなまし法(Simulated Annealing)
Gradient Descentでは局所解に陥りやすいので、局所解に陥っても抜け出せるうよう、非最小のコストのノードも探索範囲とする。
* $T(t):$時刻$t$に関する**単調減少関数**(温度)
* $Cost(N)$:ノード$N$のコスト
### アルゴリズム
1. ルートノードを*N*とする。
2. $T=T(t)$として、$T=0$なら*N*を答えとして探索成功、実行終了。
3. *N*の子ノードからランダムにノード*M*を選ぶ。
4. *N*と*M*のコストの差$\Delta E=Cost(M)-Cost(N)$を求める。
5. $\Delta E<0$なら*N*=*M*とし、そうでなければ$exp(-\Delta E/T)$の確率で*N*=*M*とする。(コストが大きい方への探索)
6. $t=t+1$として2.へ戻る。
```clike
Simulated_Annealing(){
    node N = Root;
    temperature T;
    while(true){
        T = T(t);
        if(T == 0) exit(Success with ans = N);
        M = choose RANDAMLY from children of N;
        if((ΔE = Cost(M) - Cost(N)) < 0) N = M;
        else N = M with the probability of exp(-ΔE/T);
        t++;
}
```
* ある確率(ここでは$exp(-\Delta E/T)$)でよりコストの大きいノードを探索。
* $t$が小さいとき、$T(t)$は大きいので、その確率も大きいが、$t$が大きくなるにつれて確率は小さくなる。

## min-max法
自分と相手のノードを区別して、相手が最善手を打つと仮定して探索。相手の最善手、つまり自分にとってスコアが最小である。何手先を読むかによって評価が変わる。
### アルゴリズム
`function MinMax(node, turn);`
1.ノード*N*がリーフノードである場合、そのスコアを返す。
2.そうでなければ(ターンチェンジの上)それぞれの子ノードについて、再帰的に`MinMax()`を呼ぶ。
3.自分のターンの場合、子ノードのスコアのうち最大のものを返す。
4.相手のターンの場合、子ノードのスコアのうち最小のものを返す。
```clike
int MinMax(node N, turn T){
    if(N is leaf) return score(N);
    else{
        T = !T; //change turn
        for(M:children of N) scores.add(MinMax(M, T));
        if(MyTurn) return max(scores);
        if(OppTurn) return min(scores);
    }
}
```

### αβカット
min-max法は深さ優先探索。深さ$d$、分岐数$b$で計算量が$b^d$と先読みを深くすると指数的に増大する。
αβカットはmin-max法において、計算量を削減する。**αカット**と**βカット**(fai4.pdf page 5,6参照)
* αカット:自分の評価値計算に反映されないノードの計算をしない。
* βカット:相手の評価値計算に反映されないノードの計算をしない。
    * 誰のターンかに注意する。
### 計算量
最良の場合$b^{d/2}$に削減可能。平均的には$b^{3d/4}$
### 偶然性のあるゲーム
スコアは期待値を用いる。