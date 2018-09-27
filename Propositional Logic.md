---
lang: ja-jp
title: 命題論理
tags: Logic & Reasoning, 02, 03, 04
---

命題論理
===

## 命題(Proposition)

### 命題とは

真偽が確定している文のこと

### 命題変数(Propositional variable)

* 基本的な命題を記号化・形式化したもの
* これ以上分解できない最小の単位

例 :
$p$ : 太郎は日本人である。
$q$ : 花子は日本人である。

### 原子論理式

命題倫理において、原子論理式とは命題変数と$\perp$のこと。

### 結合子

$\land$ : 論理積, and, conjuction
$\lor$ : 論理和, or, disjunction
$\rightarrow$ : 含意(if..., then...), implication
$\lnot$ : 否定, not, negation
$\leftrightarrow$ : 同値, iff, equivalence
$\perp$ : 常に偽, falsity, falsum

### 複合命題

例 :
$(p\land q)$ : 太郎と花子は日本人である。

## 命題の集合$PROP$

**整論理式**(Well-formed formula)ともいう。

### 条件

以下の性質を満たす**最小の集合**$X$
$p_i(i\in N)$ : 原子論理式
1. $p_i\in X(i\in N),\perp\in X$
2. $\varphi,\psi\in X$ *ならば* $(\varphi\land\psi),(\varphi\lor\psi),(\varphi\rightarrow\psi),(\varphi\leftrightarrow\psi)\in X$ 
3. $\varphi\in X$ *ならば* $(\lnot\varphi)\in X$

言い換えると、
1. $p_i$が$X$に含まれていれば、$\perp$も$X$に含まれる。
2. $\varphi,\psi$が$X$に含まれていれば、4つの結合子でできた複合命題も$X$に含まる。
3. $\varphi$が$X$に含まれていれば、その$(\lnot\varphi)$も$X$に含まれる。

### $\lnot\lnot\perp\notin PROP$の証明

#### 方針

$\lnot\lnot\perp\in X$として、$X$は$PROP$の条件を満たすとする。このとき$Y=X-\{\lnot\lnot\perp\}$とすると、$Y$も$PROP$の条件を満たすことを示す。しかし$PROP$は**最小の集合**であるはずなので矛盾し、$\lnot\lnot\perp\notin PROP$が言えることになる。1.2.3.と順に示していく。

## 論理式の構造的帰納法(Induction Principle)

### 定義2.1 [Induction Principle]

$A$を*ある論理式の性質*として、以下の1.2.3.を満たすとき、**全ての論理式が性質**$A$**を持つ**。すなわち、$A(\varphi),\varphi\in PROP$
1. $A(p_i),(i\in N)$かつ$A(\perp)$
2. $\forall\varphi,\forall\psi$について$A(\varphi)$かつ$A(\psi)$ならば$A((\varphi\square\psi))$
3. $A(\varphi)$ならば$A((\lnot\varphi))$

証明は02.pdf(page13)

## 構成系列(Formation Sequence)

### 定義2.2 [Formation Sequence]
$\varphi_n=\varphi$
$\forall i\leq n$に対して : 
$\varphi_i$は原子論理式または、
$\exists j,\exists k<i$に対して$\varphi_i=(\varphi_i\square\varphi_k)$または、
$\exists j<i$に対して$\varphi_i=(\lnot \varphi_j)$
以上の条件を満足する系列$\varphi_1,\varphi_2,\dots ,\varphi_n$を$\varphi$**の構成系列**と呼ぶ。

### 定理2.2 [$PROP$に含まれる全ての論理式は構成系列を持つ]

証明は02.pdf(Page21)

## 論理式の付値

### 真理値表

0がfalse、1がtrue

|       | $p_1$ | $p_2$ | $(p_1\land p_2)$ | $(p_1\lor p_2)$ | $(p_1\rightarrow p_2)$ | $(p_1\leftrightarrow p_2)$ | $(\lnot p_1)$ | $(\lnot p_2)$ |
| :---: | :---: | :---: | :--------------: | :-------------: | :--------------------: | :------------------------: | :-----------: | :-----------: |
| $v_1$ |   0   |   0   |        0         |        0        |           1            |             1              |       1       |       1       |
| $v_2$ |   0   |   1   |        0         |        1        |           1            |             0              |       1       |       0       |
| $v_3$ |   1   |   0   |        0         |        1        |           0            |             0              |       0       |       1       |
| $v_3$ |   1   |   1   |        1         |        1        |           1            |             1              |       0       |       0       |
$v_i$ : 付値(valuation)

### 定義3.1 [valuation]

写像$v:PROP\rightarrow \{0,1\}$が以下を満たすとき$v$を**付値**(valuation)という。

$$
\begin{eqnarray}
v((\varphi\land\psi))&=&min(v(\varphi),v(\psi)) \\
v((\varphi\lor\psi))&=&max(v(\varphi),v(\psi)) \\
v((\varphi\rightarrow\psi))&=&
\begin{cases}
0 & (v(\varphi)=1,v(\psi)=0) \\
1 & otherwise
\end{cases} \\
v((\varphi\leftrightarrow\psi))&=&
\begin{cases}
0 & (v(\varphi)=v(\psi)) \\
1 & otherwise
\end{cases} \\
v((\lnot\varphi))&=&1-v(\varphi) \\
v(\perp)&=&0
\end{eqnarray}
$$

### 定理3.1

論理式$\varphi$の中に現れる原子論理式$\{p_i\}$全てに対して$v(p_i)=v'(p_i)$ならば、$v(\varphi)=v'(\varphi)$である。ただし$v,v'$は付値である。

#### 証明

論理式の構造的帰納法を用いる(03.pdf page 9)。**valuationという性質とも言える。**

## トートロジー(tautology)

1. 全ての付値$v$に対して$v(\varphi)=1$であるならば、論理式$\varphi$は**トートロジーである**といい、$\vDash\varphi$と表す。
2. 論理式の集合$\Gamma$に含まれる論理式$\varphi$に対して任意の付値$v$が $v(\varphi)=1$であるとする。このとき$v(\psi)=1$ならば、$\Gamma\vDash\psi$とかく。

### 論理的同値性

$\vDash(\varphi\leftrightarrow\psi)$のとき、$\varphi\Leftrightarrow\psi$と表す。

1. 反射律 : $\varphi\Leftrightarrow\varphi$
2. 対称律 : $\varphi\Leftrightarrow\psi$ならば$\psi\Leftrightarrow\varphi$
3. 推移律 : $\varphi\Leftrightarrow\psi$かつ$\psi\Leftrightarrow\sigma$ならば$\varphi\Leftrightarrow\sigma$

以上から、$「\Leftrightarrow」$は論理式の同値関係を定義する。
その他の論理式の同値関係は、03.pdf(page 13)を参照

## 論理式の代入

$\varphi[\psi/p_i]$ : $\varphi$に現れる$p_i$を全て$\psi$で置き換えた論理式を表す。

### 代入の再帰的定義

$$
\begin{eqnarray}
&&\varphi[\psi/p_i]=
\begin{cases}
    \varphi & \mathrm{if\ \varphi\ is\ an\ atom\ and\ \varphi\neq p_i} \\
    \psi & \mathrm{if\ \varphi=p_i}
\end{cases} \\
&&(\varphi_1\square\varphi_2)[\psi/p_i]=(\varphi_1[\psi/p_i]\square\varphi_2[\psi/p_i]) \\
&&(\lnot\varphi)[\psi/p_i]=(\lnot\varphi[\psi/p_i])
\end{eqnarray}
$$

### 代入定理

$\vDash (\varphi_1\leftrightarrow\varphi_2)$ならば$\vDash (\psi[\varphi_i/p]\leftrightarrow\psi[\varphi_2/p])$

$(p\ is\ atom)$

## 標準形

任意の論理式$\varphi\in PROP$に対して論理積標準形$\varphi^\land$と論理和標準形$\varphi^\lor$が存在して、

$$
\varphi\Leftrightarrow\varphi^\land
\\ \varphi\Leftrightarrow\varphi^\lor
$$

が成立する。

### 定義4.1

$$
\begin{eqnarray}
\begin{cases}
{\underset{i\leq 0}{\large\mathrm I}}\varphi_i=\varphi_0 \\
{\underset{i\leq n+1}{\large\mathrm I}}\varphi_i=({\underset{i\leq n}{\large\mathrm I}}\varphi_i)\land\varphi_{n+1}
\end{cases}
\hspace{25mm}
\begin{cases}
{\underset{i\leq 0}{\large\mathrm Y}}\varphi_i=\varphi_0 \\
{\underset{i\leq n+1}{\large\mathrm Y}}\varphi_i=({\underset{i\leq n}{\large\mathrm Y}}\varphi_i)\lor\varphi_{n+1}
\end{cases}
\end{eqnarray}
$$

### 定義4.2

#### 論理積標準形(Conjunctive normal form)

$\varphi_{ij}$を原子論理式または原子論理式の否定として、
* $\varphi={\underset{i\leq n}{\large\mathrm I}}\ {\underset{j\leq m}{\large\mathrm Y}}\varphi_{ij}$
    * 例 : $\varphi =(p_i\lor p_2)\land(p_3\lor p_4)$

#### 論理和標準形(Disjunctive normal form)
* $\varphi={\underset{i\leq n}{\large\mathrm Y}}\ {\underset{j\leq m}{\large\mathrm I}}\varphi_{ij}$
    * 例 : $\varphi =(p_i\land p_2)\lor(p_3\land p_4)$

### 定理4.1

#### 任意の論理式$\varphi$は$\{\land,\lnot\}$のみを用いた論理式$\omega$でかける。

* $\varphi\leftrightarrow\omega$がトートロジーであることを示せば良い。
    * $\vDash(\varphi\leftrightarrow\omega)=(\varphi\Leftrightarrow\omega)$

## ブール代数

${\bf A}=\left<A,\cap,\cup,{'},0,1\right>$が*ブール代数である*とは、$\forall a,\forall b,\forall c\in{\bf A}$に対して、04.pdf(page 16)が成り立つことである。論理式の基本的な同値関係と対応する。

### 補元

ブール代数${\bf A}$の要素$a$に対し、$a'$のことを$a$の補元といい、以下が成り立つ。

$$
\begin{eqnarray}
&1)&\hspace{5mm}a''=a \\
&2)&\hspace{5mm}0'=1,\ 1'=0 \\
&3)&\hspace{5mm}(a\cap b)'=a'\cup b',\ (a\cup b)'=a'\cap b'
\end{eqnarray}
$$