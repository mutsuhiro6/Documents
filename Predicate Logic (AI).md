---
lang: ja-jp
title: 述語論理(AI)
tags: AI, fai5
---

述語論理(AI)
===

## 用語

### 論理の種類

* 命題論理 : 命題記号、論理記号
    * 実用が困難
* 一階述語論理 : 個体定数、個体変数、関数記号、述語記号、限量記号、論理記号
* 二階述語論理 : 関数変数、述語変数
    * 高階述語論理は非効率的

### 論理式

* 束縛変数 : 限量子がついた変数
* 自由変数 : 限量子がつかない変数
* 開論理式 : 自由変数を含む分
* 閉論理式 : 自由変数を含まない分(**wff**)

## 解釈

解釈$I$とは論理式の要素と対象領域の要素との対応づけ

### 個体変数

* $a,b,c,d,e$ : 論理式における個体定数
* $A,B,C,D,E$ : 対象領域における個体

$$
I(a)=A,\ I(b)=B,...
$$

### 関数

* $f$ : 論理式における関数記号
* $F$ : 対象領域における関数

$$
I(f)=F
$$

例 : $above$
$I(above)$ : 「ある箱の上にあるもの」

## 述語

* $p$ : 論理式における述語記号、
* $P$ : 対象領域における要素間の関係

$$
I(p)=P
$$

例 : $bigger$
$I(bigger)$ : 「ある箱はある箱より大きい」

## 変数割り当て

変数割り当て$V$とは、個体変数から対象領域における要素への写像
$x$を個体変数、$o$を対象領域における要素とすると、以下のように表せる。

$$
V(x)=o
$$

## 充足可能性

論理式$\varphi$が解釈$I$と変数割り当て$V$の元で真であるとき、「$\varphi$は$I$と$V＄のもとで充足される」と表現し、

$$
\vDash_{IV}\varphi
$$

とかく。

### 充足可能性による論理式の分類

* 恒真 : $I,V$によらず常に真
* 恒偽 : $I,V$によらず常に偽
* それ以外 : $I,V$を適当に選ぶことで真にすることが可能

## 論理的公理

1. $\varphi\rightarrow (\psi\rightarrow\varphi)$
2. $(\varphi\rightarrow(\psi\rightarrow X))\rightarrow((\varphi\rightarrow\psi)\rightarrow(\varphi\rightarrow X))$
3. $(\lnot\varphi\to\lnot\psi)\to(\psi\to\varphi)$ : 対偶
4. $(\forall x\varphi)\to\varphi_{x/t}$
5. $\forall x(\varphi\to\psi)\to((\forall x \varphi)\to(\forall x\psi))$
6. $\varphi\to(\forall x)\varphi$

## 論理的帰結

$\varphi_1,\dots,\varphi_n$の全てを真とする解釈と変数割り当て$I,V$に対して別の論理式$\psi$が真のとき

$$
\{\varphi_1,...,\varphi_n\}\vDash_{IV}\psi
$$

$\varphi_1,\dots,\varphi_n$の全てを真とする任意の解釈と変数割り当てに対して別の論理式$\psi$が真の時

$$
\{\varphi_1,...,\varphi_n\}\vDash\psi
$$

この時$\psi$は$\{\varphi_1,...,\varphi_n\}$の**論理的帰結である**という。

## モデル

論理式$\varphi$がある解釈$I$について、任意の変数割り当て$V$に対して真である時、$I$を$\varphi$のモデルという。

## 述語論理の推論

真である論理式の集合(**前提**)から推論規則を用いて新しい論理式(**結論**)を導出

### 6つの推論規則

* Modus Pones
* Modus Torens
* AND導入規則(AND Introduction)
* AND除去規則(AND Elimination)
* 全称例化(Universal Instantiation)
* 存在例化(Existential Instantiation)

$$
\begin{array}{c}
\boxed{
\scriptsize \text{Modus Pones} \\
\begin{array}{l}
\varphi\to\psi \\
\varphi \\
\hline
\psi
\end{array}}
\boxed{
\scriptsize \text{Modus Torens} \\
\begin{array}{l}
\varphi\to\psi \\
\lnot\psi \\
\hline
\lnot\varphi
\end{array}}
\boxed{
\scriptsize \text{AND Introduction} \\
\begin{array}{l}
\varphi \\
\psi \\
\hline
\varphi\land\psi
\end{array}}
\boxed{
\scriptsize \text{AND Elimination} \\
\begin{array}{l}
\varphi\land\psi \\
\hline
\varphi \\
\psi
\end{array}} \\
\boxed{
\scriptsize \text{Universal Instatiaiton} \\
\begin{array}{l}
\forall x\varphi \\
\hline
\varphi_{x/t}
\end{array}}
\boxed{
\scriptsize \text{Existential Instatiaiton} \\
\begin{array}{l}
\exists x\varphi \\
\hline
\varphi_{x/f(x_1,...,x_n)}
\end{array}}
\end{array}
$$

### 論理式の証明

* $\{\varphi_1,...,\varphi_n\}$が真の場合$\psi$が成立するかは、$\{\varphi_1,...,\varphi_n\}\vDash\psi$を示す。
* 前提(論理式の集合$\{\varphi_1,...\varphi_n\}$,論理的公理)から推論規則を用いて結論$\psi$を導く。

#### 証明プロセス

1. 前提と結論の整理
2. 記号化
3. 論理式集合の記述
4. 推論規則を順に適用して行くことによる証明

fai5.pdf(page 41,42)の証明をきちんとやるべし