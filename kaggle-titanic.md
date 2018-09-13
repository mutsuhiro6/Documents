# kaggle-titanic

## Preprocess

### MostFrequentImputer

これを使って，categoricalな要素の欠損値の補完．numericalな場合と同様の発想で，もっとも多く出現する属性を欠損値の補完に使う．

### MultiColumnLabelEncoder

LabelEncoderは，MultiColumnには非対応であるので，自作．

scikit-learn 0.20.0以降でCategory Encoderが使えるようになるらしい．

今も`conda install -c conda-forge category_encoders`でanaconda環境に追加できる．