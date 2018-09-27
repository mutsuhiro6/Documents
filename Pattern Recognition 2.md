---
lang: ja-jp
title: パターン認識
tags: AI, fai10, パターン認識
---
パターン認識
===
* [Symbol grounding problem - Wikipedia](https://en.wikipedia.org/wiki/Symbol_grounding_problem)
## 特徴

### 特徴抽出

パターン認識に有効な特徴をヒューリスティックな方法で選択

### 特徴ベクトル

$d$個の特徴を用いる場合特徴ベクトル$\boldsymbol{x}$は以下のようになる。

$$
\boldsymbol{x}=\left(
\begin{array}{c}
{x_1 \\x_2\\\vdots\\x_d}
\end{array}
\right)
$$

## 線形識別関数

$\boldsymbol{x}$に対する線形識別関数を定義する。

$$
g(x)=w_0+\sum_{j=1}^dw_jx_j
$$

ここで、変数の置き換えをする。

$$
\boldsymbol{x}=(x_0,x_1,...,x_d)^t=\pmatrix{x_0\\x},x_0\equiv1 \\
\boldsymbol{w}=(w_0,w_1,...,w_d)^t=\pmatrix{w_0\\w}
$$

また、$\boldsymbol{x}$は拡張特徴ベクトル、$\boldsymbol{w}$は拡張重みベクトルである。

クラス$i$の識別関数は、

$$
g_i(\boldsymbol{x})=\boldsymbol{w}_i^t\boldsymbol{x}
$$

とかけ、また、$\boldsymbol{w}_i$はクラス$i$の拡張重みベクトルである。

## パーセプトロン(Perceptron)
線形関数を識別関数として用いて、その最大値を選択する識別器をパーセプトロンと呼ぶ。
ここでは**単純パーセプトロン**(Simple-)について記述

### 学習

学習パターン全体の集合 : $\Gamma$
クラス$\omega_i$に属する学習パターンの集合 : $\Gamma_i\ (i=1,2,...,c)$として

$\Gamma_i$に属する全ての$\boldsymbol{x}$について、

$$
g_i(\boldsymbol{x})>g_j(\boldsymbol{x})\ (j\neq i)
$$

が成り立つように重み$\boldsymbol{w}_i$を決定することを学習という。

このような重み$\boldsymbol{w}_i$が存在する時$\Gamma$は**線形分離可能である**という。
$g_i(\boldsymbol{x})=g_j(\boldsymbol{x})$ : クラス$i,j$の決定境界

### 2クラスの識別

\begin{eqnarray}
g(\boldsymbol{x})&=&g_1(\boldsymbol{x})-g_2(\boldsymbol{x}) \\
&=&(\boldsymbol{w_1}-\boldsymbol{w_2})^t\boldsymbol{x} \\
&=&\boldsymbol{w}^t\boldsymbol{x}\ (\boldsymbol{w}\equiv\boldsymbol{w_1}-\boldsymbol{w_2})
\end{eqnarray}

\begin{cases}
g(\boldsymbol{x})=\boldsymbol{w}^t\boldsymbol{x}>0 & (\boldsymbol{x}\in\omega_1) \\
g(\boldsymbol{x})=\boldsymbol{w}^t\boldsymbol{x}<0 & (\boldsymbol{x}\in\omega_2)
\end{cases}

決定境界 : $g(\boldsymbol{w}^t\boldsymbol{x})=0$

### 学習

\begin{cases}
g(\boldsymbol{x})=\boldsymbol{w}^t\boldsymbol{x}>0 & (\forall\boldsymbol{x}\in\Gamma_1) \\
g(\boldsymbol{x})=\boldsymbol{w}^t\boldsymbol{x}<0 & (\forall\boldsymbol{x}\in\Gamma_2)
\end{cases}

を見たす$\boldsymbol{w}$を求めること。

#### アルゴリズム

1. 重みベクトルの初期値を適当に決める。
2. $\Gamma$の中から学習パターンを一つ選ぶ。
3. $g(\boldsymbol{x})$により識別。
    4. 誤った場合、$\boldsymbol{w}$を以下で求めた$\boldsymbol{w}'$で置き換える\begin{cases}\boldsymbol{w}'=\boldsymbol{w}+\rho\boldsymbol{x} & (\mathrm{misrecognize\ \omega_1\ as\ \omega_2})\\\boldsymbol{w}'=\boldsymbol{w}-\rho\boldsymbol{x} & (\mathrm{misrecognize\ \omega_1\ as\ \omega_2}）\end{cases}
5. 2.3.の処理を$\Gamma$の全パターンについて繰り返す。
6. $\Gamma$の全パターンを識別できれば終了。誤りがあれば2.へ戻る。

## 多層パーセプトロン

fai11.pdfを参照