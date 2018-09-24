# TensorFlowによるCNNの実装

## 事前知識

- 個々の入力画像は$shape[height, width, channel]$の3Dテンソル
- ミニバッチは$shape[mini\ batch\ size, height, channel]​$の4Dテンソル
- 畳み込み層の重みは$shape[f_h, f_w, f_{n'}, f_n]$
- バイアス項は$shape[f_n]​$の1Dテンソル

で表される．

## 畳み込み層の実装

scikit-learnの`load_sample_images()`で画像をロードし，7×7の2つのフィルタを用いて`tf.nn.conv2d()`で作った畳み込み層から画像にフィルタを適用したのち，得られた特徴量マップをプロットする．

## プーリング層の実装

