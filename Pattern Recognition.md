# パターン認識まとめ

## 0. 行列代数

### 0.1. スカラーをベクトルで微分

$f\in\mathbb{R},\ \boldsymbol{y}\in\mathbb{R}^n$のとき
$$
\frac{\partial f}{\partial\boldsymbol{y}}\in\mathbb{R}^n
$$

### 0.2. ベクトルをベクトルで微分

$\boldsymbol{x}\in\mathbb{R}^m,\ \boldsymbol{y}\in\mathbb{R}^n $のとき、
$$
\frac{\partial\boldsymbol{y}}{\partial\boldsymbol{x}}\in\mathbb{R}^{n\times m}
$$

### 0.3. スカラーを行列で微分

$f \in\mathbb{R},\ \boldsymbol{A}\in\mathbb{R}^{m\times n}$のとき、
$$
\frac{\partial f}{\partial\boldsymbol{A}}\in\mathbb{R}^{m\times n}
$$

### 0.4. 表記

行列$\boldsymbol{X}$に対して
$$
\frac{\partial\boldsymbol{X}_{kl}}{\partial\boldsymbol{X}_{ij}}=\delta_{ik}\delta_{lj}
$$
また、ベクトルについて
$$
\left[\frac{\partial\boldsymbol{x}}{\partial y}\right]_i=\frac{\partial x_i}{\partial y}\qquad\left[\frac{\partial x}{\partial \boldsymbol{y}}\right]_i=\frac{\partial x}{\partial y_i}\qquad\left[\frac{\partial\boldsymbol{x}}{\partial\boldsymbol{ y}}\right]_{ij}=\frac{\partial x_i}{\partial y_j}
$$

### 0.5. 正定値行列

ある行列$\boldsymbol{\Sigma}$について、$\boldsymbol{\Sigma}\succ 0$と書いて、**正定値行列**といい、対照行列である。また以下が成り立つ。
$$
\boldsymbol{x}^T\boldsymbol{\Sigma}\boldsymbol{x}\gt 0,\ \forall\boldsymbol{x}\in\mathbb{R}^d,\ \boldsymbol{\Sigma}^T=\boldsymbol{\Sigma}
$$

### 0.6. 2次形式

$\boldsymbol{x}^T\boldsymbol{A}\boldsymbol{x}$であるような形を2次形式と呼ぶ。また、
$$
\boldsymbol{x}^T\boldsymbol{A}\boldsymbol{x}=\mathrm{trace}(\boldsymbol{A}\boldsymbol{x}\boldsymbol{x}^T)
$$
という性質を持つ。

## 1. ガウス分布(正規分布)

$$
\mathcal{N}(\boldsymbol{x};\boldsymbol{\mu},\boldsymbol{\Sigma})=\frac{1}{(2\pi)^{d/2}|{\boldsymbol\Sigma}|^{1/2}}\exp\left(-\frac{1}{2}{(\boldsymbol{x}-\boldsymbol{\mu})}^T\boldsymbol{\Sigma}^{-1}(\boldsymbol{x}-\boldsymbol{\mu})\right)
$$

## 2. 確率・統計におけるモデル推定

$x$の情報源推定のための$p(x)$を、モデル$q(x;\boldsymbol{\theta})$として表現する。学習データ$\{x^{(i)}\}_{i=1}^{n}$からパラメータを最適化する。

**最尤推定**
$$
\boldsymbol{\theta}_{ML}=\mathrm{argmax}_{\boldsymbol{\theta}}\ln\left(\prod_{i=1}^nq(x_i;\boldsymbol{\theta})\right)
$$

## 3. 生成的なパターン認識によるパラメトリック法

推定したいカテゴリの数を2として、$y=k\in\{1,2\}$に対する条件付分布$p(\boldsymbol{x}|y=k)$を適当なモデル$q(\boldsymbol{x};\boldsymbol{\theta}_y)$により表現することを考える。

$$
\begin{align}
\hat{y}&=\mathrm{argmax}_yp(y|\boldsymbol{x}) \\
&=\mathrm{argmax}_{y}\ln\left(\frac{q(\boldsymbol{x};\boldsymbol{\theta_y})p(y)}{p(\boldsymbol{x})}\right) \\
&=\mathrm{argmax}_y\ln q(\boldsymbol{x};\boldsymbol{\theta}_y)+\ln\frac{n_y}{n}+C
\end{align}
$$
またカテゴリ数が2であるとき、カテゴリの識別境界は、
$$
\ln p(y=1|\boldsymbol{x})-\ln p(y=2|\boldsymbol{x})=0
$$
となるような$$\boldsymbol{x}$$の集合。

## 4. ベイズ推定

### 4.1. パラメータの確率的取り扱い 

事前確率$p(\boldsymbol{\theta})$、事後確率$p(\boldsymbol{\theta}|\boldsymbol{X})$、尤度$p(\boldsymbol{X}|\boldsymbol{\theta})$から、ベイズの定理から、
$$
p(\boldsymbol{\theta}|\boldsymbol{X})\propto p(\boldsymbol{X}|\boldsymbol{\theta})p(\boldsymbol{\theta})
$$
とかける。

### 4.2. 共役事前分布

 モデル$q(\boldsymbol{x}|\boldsymbol{\theta})$、パラメータ事前分布$q(\boldsymbol{\theta};\boldsymbol{\alpha})$を用いて、事後分布$p(\boldsymbol{\theta}|\boldsymbol{X})$を表す。尤度$L(\boldsymbol{\theta})=\displaystyle\prod_{i}q(x_i|\boldsymbol{\theta})$を用いて、

$$
\begin{align}
p(\boldsymbol{\theta}|\boldsymbol{X})&\propto q(\boldsymbol{\theta};\boldsymbol{\alpha})L(\boldsymbol{\theta}) \\
&\propto q(\boldsymbol{\theta};\boldsymbol{\alpha})\prod_i q(x_i|\boldsymbol{\theta})
\end{align}
$$

と表してみると、パラメータ事前分布$q(\boldsymbol{\theta};\boldsymbol{\alpha})$と事後分布$p(\boldsymbol{\theta}|\boldsymbol{X})$の形が一致するときの、事前分布を共役事前分布と呼ぶ。

## 5. MAP推定

$$
\begin{align}
\hat{\theta}_{MAP}&=\mathrm{argmax}_\boldsymbol{\theta}p(\boldsymbol{\theta})\prod_iq(x_i|\boldsymbol{\theta}) \\
&=\mathrm{argmax}_\boldsymbol{\theta}\left[\ln{p(\boldsymbol{\theta})}+\sum_i\ln{q(x_i|\boldsymbol{\theta})}\right]
\end{align}
$$

$\ln{p(\boldsymbol{\theta})}$を罰則項と呼ぶこともある。(罰則付き最尤推定)

## 6. モデル選択

### 6.1. 情報量基準

真の確率密度をよく近似するためにはパラメータ数の多い複雑なモデルが良いとともに、最尤推定によると、パラメータに対する訓練データを十分多く用意する必要があルため、パラメータ数が程よく、より真の確率密度の推定が求められる。その程よさを情報量基準によってはかる。

### 6.2. 交差検証法 

訓練データとテストデータに分けて、訓練データによりモデル推定を行い、それをテストデータに適応させ、対数尤度を計算し、最尤推定を行う。その結果から一番良いモデルを選ぶ。

## 7. 混合モデル 

### 7.1. カーネル密度推定

$$
\hat{p}_{KDE}(\boldsymbol{x})=\frac{1}{nb^d}\sum_i^nK(\frac{\boldsymbol{x}-\boldsymbol{x}_i}{b})
$$

$b$はバンド幅で、大きくすると推定グラフが滑らかになる。カーネル密度関数$K$は、
$$
K(\boldsymbol{x})\geq0,\quad \forall \boldsymbol{x}\in D,\quad\int_DK(\boldsymbol{x})d\boldsymbol{x}=1
$$
を満たす。カーネル密度関数の例としてガウスカーネル
$$
K(\boldsymbol{x})=\frac{1}{(2\pi)^{d/2}}\exp\left(-\frac{\boldsymbol{x}^T\boldsymbol{x}}{2}\right)
$$
がよく用いられる。

