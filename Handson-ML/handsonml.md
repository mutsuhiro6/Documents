# Hands on ML

## 交差検証 Cross Varidation

### Stratified K-Fold

#### K-Fold

k-foldで"k個の部分(のある)"という意味で，K-Fold法による**交差検証**(Cross Varidation)は，k個の部分集合に分けて交差検証を行うということ．

#### Stratified

stratify 階層化する

から，Stratified K-Fold は階層化K分割法（による交差検証）と訳す．

*階層化ってなんだ？？*

## 混同行列 Confusion Matrix

クラスAのインスタンスがクラスBに(誤って)分類された回数を数える．

### 適合率 precision

### 再現率 recall

### F値 F~1~ Score

## 多クラス分類

SVMなどは実際は2クラス分類器であるが，多クラス分類を行える．10クラス分類をしたければ，10個の分類器を使えば良い．

scikit-learnではSVMでも自動で多クラス分類をしてくれる．

ここの分類器の決定スコアを比較して，一番良いスコアを出力する分類器のクラスを選択する．**OVA法**と呼ぶ．

*Random Forestってなんだ？*

### 誤分類分析

matplotlibの`matshow()`による，confusion matrixのイメージ表現．



## データのクリーニング

### 欠損値の処理，補完

1. 対応区域を取り除く
2. 属性全体を取り除く
3. なんらかの値を補完

`Imputer`クラス