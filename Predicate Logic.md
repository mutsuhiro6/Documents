---
lang: ja-jp
title: 述語論理
tags: Logic & Reasoning, 05, 06
---

述語論理
===

## 用語

### 対象変数、対象定数

* 対象変数 : 議論の対象としているものの集まりを動く変数
    * 実数値の変数など
* 対象定数 : 特定された、ものを表す**記号**
    * 円周率$\pi$など

### 限量子

* $\exists xP(x)$ : 性質$P$を有する$x$が存在する
* $\forall xP(x)$ : 全ての$x$が性質$P$を有する
    * $\forall x\exists y(x=2y)$ : 全ての$x$に対して$x=2y$となる$y$が存在する

### 集合$A$について

#### 直積

$A^n=\{(x_1,x_2,\cdots ,x_n)|x_1\in A,\cdots x_n\in A\}$

#### 関係

$A$の直積の部分集合を$A$上の関係という
$R\subseteq A^n$のとき、$R$は$n$項関係$(n\geq 1)$

#### 関数

$A^n$から$A$への写像$A^n\rightarrow A$を関数という

### 述語

$n$項関係$R$に対して

$$
\begin{eqnarray}
P(x_1,\cdots,x_n)=
\begin{cases}
1 & (x_1,\cdots,x_n)\in R \\
0 & (x_1,\cdots,x_n)\notin R
\end{cases}
\end{eqnarray}
$$

となる述語$P$が決まる。
$n$項関係$R$とそれに対応する述語$P$は同一視する。

#### 例

$N$を自然数の集合とする。このとき$<$は$N$上の2項関係$R$を与える。

$$
R=\{(n,m)|n<m\}
$$

また、対応して、

$$
P(n,m)=
\begin{cases}
1 & n<m \\
0 & n\geq m
\end{cases}
$$

となる述語$P$が決まる。

### 構造

$(A,R_1,\cdots ,R_n,F_1,\cdots ,F_m,\{c_i\})$
集合 : $A$
関係 : $R_i\subseteq A^{r_i}$
写像 : $f_j:A^{a_j}\longrightarrow A$
定数記号 : $c_i$

### Similarity Type

$$(r_1,\cdots,r_n;a_1,\cdots ,a_m;k)$$

ただし、$k=|\{c_i\}|$(定数記号の数)

#### 例

* 構造 : $(\mathbb{N},<,,)$
* Similarity Type : $(2;;0)$


