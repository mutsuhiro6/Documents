---
lang: jp-ja
title: ベイジアンネットワーク
tags: AI, fai9, ベイジアンネットワーク
---
ベイジアンネットワーク
===

## 条件付独立

* $\boldsymbol{Z}$の値が与えられると$\boldsymbol{X},\boldsymbol{Y}$が独立となること。
* $\boldsymbol{Z}$を与えた時、$\boldsymbol{X}$を推論するのに$\boldsymbol{Y}$は役に立たない。
* $I(\boldsymbol{X},\boldsymbol{Y},\boldsymbol{Z})$とかき、$P(x,y|z)=P(x|z)P(y|z)$が成り立つこと。

## 条件付き確率、ベイズの定理
### 確率の表記
* 「事象aが起きる確率」を$P(a)$と表す。
    * 「命題aが真になる確率」
* 「aとbが同時に起きる、**同時結合確率**」を$P(a,b)$(または$P(a\cap b)$)と表す。
* 「aが起き、bが起きる**条件付き確率**」を$P(b|a)$と表す。
    * 「aが真の時のa→bの確率」

### ベイズの定理
1. aとbが互いに独立である時、$P(a,b)=P(a)P(b)$とかける。
2. $P(a,b)=P(b,a)=P(b|a)P(a)=P(a|b)P(b)$は自明。
3. $P(c|b,a)=\frac{P(c,b,a)}{P(b,a)}$も成り立つ。
4. 2.3.から以下のような**ベイズの定理**が導かれる。
$$
P(b|a)=\frac{P(a|b)P(b)}{P(a)}
$$

## CPT (Conditional Probability Table)
ベイジアンネットワークの計算において、事前にCPTが与えられる。
* 独立して起きる事象についての発生確率を定義
    * 独立 : アークが入ってこない事象
* 例) Burglar-Alarm


### チェインルール
$P(a,b)=P(a|b)P(b)$
$P(a,b,c)=P(a|b,c)P(b,c)=P(a|b,c)P(b|c)P(c)$
$P(a,b,c,d)=\dots =P(a|b,c,d)P(b|c,d)P(c|d)P(d)$

## 計算手順
[参考ページ](http://www.sist.ac.jp/~kanakubo/research/reasoning_kr/bayesiannetwork.html)

## 因果的推論

![ベイジアンネットワーク例](https://lpvz3a.ch.files.1drv.com/y4ml_XtMAMzxQzYZuJwf3pmdKO0p7S00iAu1wQ2Nfyz_HM3SVd7Wzi8n2HteHJZsaFcEN2gQUFgpigkASzmohh4BCxw25roGFJfrrxC3OXKEqJM0ByeA0fxrz2znprSdspWsgmHa-6ql0peb16W3ZwjyKyUXSc3mPHlpLYkzd7msTzPk2Bt0oKaiOwW5fTYWS_7z3fNv8Cn-WO5HQAEG58yGw?width=482&height=184&cropmode=none)

上のベイジアンネットワークにおいて、$p(E|H)$を計算することを考える。

$L$ : evidence
$E$ : Query node

$$
\begin{eqnarray}
p(E|H)&=&p(E,B|H)+p(E,\lnot B|H) \\
&=&p(E|B,H)p(B|H)+p(E|\lnot B,H)p(\lnot B|H)
\end{eqnarray}
$$
(2行目は、$H$がおきて、$E$と$B$が同時に起きる確率を表す。$B$,$H$の真偽を明確にするのでこのような書き方になる。)
ここで、$p(B|L)=p(B),p(\lnot B|L)=p(\lnot B)$だから、...と変形していく。

### アルゴリズム

1. Query node Vの条件付き確率をevidenceが与えられた時のV自身とその全ての親ノードの同時確率として書き直す。
2. これらの**同時確率**を計算し、Vの条件付き確率を求める。

## 診断的推論

先ほどと同じベイジアンネットワークにおいて、$p(\lnot E|\lnot H)$を計算する。

ベイズの定理から、
$p(\lnot H|\lnot E)=\frac{p(\lnot E|\lnot H)p(\lnot H)}{p(\lnot E)}$となり、
因果的推論から$p(\lnot E|\lnot H)=\alpha$であり、$p(\lnot H|\lnot E)=\frac{\alpha\beta}{p(\lnot E)}$となる。
一方、同様に$p(E|\lnot H)$を求め、$p(\lnot H|\lnot E)+p(H|\lnot E)=1$から$p(\lnot H|\lnot E)$を求める。

## D分離