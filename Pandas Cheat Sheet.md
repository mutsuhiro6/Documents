# Pandas Cheat Sheet

## 基本モジュールの読み込み

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
```



## Pandasの表示に関わる基本設定

| コマンド | 説明 |
|:--|:--|
| `pd.options.display.max_columns = None` | 常に全ての列（カラム）を表示 |
| `pd.set_option('display.max_columns', None)` | 常に全ての列（カラム）を表示 |
| `pd.options.display.max_rows = 10` | 常に10行だけ表示 |
| `pd.options.display.precision = 2` | 表示用の有効桁数を2にする |
| `pd.options.display.notebook_repr_html = True` | データフレームをHTMLで綺麗に表示 |

## Pandasのデータオブジェクト

| コマンド | 説明 |
|:--|:--|
| `pd.Series` | インデックス付きの1次元データ（シリーズ） |
| `pd.DataFrame` | インデックス付きの2次元データ（データフレーム） |
| `pd.Panel` | インデックス付きの3次元データ（パネル） |


## データI/O

| コマンド | 説明 |
|:--|:--|
| `pd.read_csv('foo.csv', header=0)` | CSVファイルからの読み込み |
| `df.to_csv('bar.csv', index=False)` | CSVファイルへの書き出し |
| `pd.read_excel('foo.xlsx', sheetname='Sheet1')` | エクセルファイルからの読み込み |
| `df.to_excel('bar.xlsx', sheet_name='Sheet1')` | エクセルファイルへの書き出し |
| `pd.read_hdf('foo.h5','df')` | HDF5ファイルからの読み込み |
| `df.to_hdf('bar.h5','df')` | HDF5ファイルへの書き出し |


## データを眺める

### チラ見

| コマンド | 説明 |
|:--|:--|
| `df.head()` | 最初の5行を表示 |
| `df.tail()` | 最後の5行を表示 |

### インデックス、カラム、値

| コマンド | 説明 |
|:--|:--|
| `df.index` | インデックスを取得 |
| `df.columns` | カラム名を取得 |
| `df.values` | 値をnumpy.ndarrayで取得 |

### 基本情報

| コマンド | 説明 |
|:--|:--|
| `df.info()` | 「有効データ数」「データ型」「メモリ使用量」などの総合的な情報を表示 |
| `df.shape` | 縦横の形を調べる |
| `df.count()` | 各カラムの有効データ数を表示 |
| `df.dtypes` | 各カラムのデータ型を表示 |
| `len(df) - df.count()` | すべてのカラムに対して、欠損値の数を計算 |

### 各種統計量

| コマンド | 説明 |
|:--|:--|
| `df.describe()` | 数値データに対して各種統計量を計算 |
| `df.describe(include='all')` | 全てのデータに対して各種統計量を計算 |

## データの選択

### カラムの選択

| コマンド | 説明 |
|:--|:--|
| `df['Age']` | Ageをシリーズとして取得（キーワードアクセス） |
| `df.Age` | Ageをシリーズとして取得（ドットアクセス）|

### インデックスとカラムの同時選択

| コマンド | 説明 |
|:--|:--|
| `df[['Age', 'Name']][1:3]` |  位置番号 `[1, 2]`のAgeとNameカラムを取得  |
| `df.iloc[1:3, [0, 4]]` | 位置番号 `[1, 2]` or 真偽値リスト |
| `df.loc[1:3, ['Age', 'Height']]` |インデックス名 `[1, 2, 3]` or 真偽値リスト|
| `df.ix[1:3, ['Age', 'Height']]` | インデックス名 or 位置番号 or 真偽値リスト |
| `df.iat[0, 1]` | 位置番号による高速な要素アクセス |
| `df.at[1, 'Age']` | インデックス名による高速な要素アクセス |

### 真偽値インデックスによる選択

| コマンド | 説明 |
|:--|:--|
| `df[df.Age >= 70]` | Ageが70以上の人を選択 |
| `df[df > 0]` | 0より上の要素はそのまま返し、それ以外はNaN |
| `df.where(df > 0)` | 0より上の要素はそのまま返し、それ以外はNaN |
| `df.mask(df > 0)` | 0より上の要素をNaNでマスクし、それ以外はそのまま返す |
| `df.ix[:, df.columns.map(lambda x: x.startswith('A'))]` | Aという文字から始まる列を取得 |
| `df[df['Grade'].isin(['A', 'B'])]` | Gradeの値がAかBの行だけを返す |
| `df.ix[:, ~df.columns.isin(['Age', 'Height'])]` | AgeとHeight以外の列を全て返す |

## データの操作

### 基本操作

| コマンド | 説明 |
|:--|:--|
| `df.T` | データフレームの転置 |
| `s.any()` | ひとつでも真であればTrue |
| `s.all()` | すべて真であればTrue |
| `s.astype('float64')` | データ型の変換 |
| `s.map({'Female':0, 'Male':1, })` | 辞書を用いた値の変換 |
| `s.value_counts()` | 値の頻度を計算 |
| `pd.get_dummies(df['Club'])` | カテゴリ変数をone-hotベクトルに変換|

```python
# カテゴリ変数をone-hot codingで離散化
colname = 'Category'
df_dummies = pd.get_dummies(df[colname], prefix=colname)
df.drop([colname], axis=1, inplace=True)
df = df.join(df_dummies)
```




### インデックス関連

| コマンド | 説明 |
|:--|:--|
| `df.index = df.pop('UserId')` |'UserId'というカラムをインデックスとして使用|
|`df.reset_index(drop=True)`|インデックスの振り直し|


### 並び替え

| コマンド | 説明 |
|:--|:--|
| `df.sort_index(axis=1, ascending=True)` | インデックスによる並び替え |
| `df.sort_values(by='Age', ascending=False)` | 値による並び替え |

### コピー

以下の２つのコードの結果はまったく同じ。

 ```python

# 変更したデータフレームを代入

`df2 = df.sort_values(by='Age')

 ```
```python
# コピーしたデータフレーム自体を変更
df2 = df.copy()
df2.sort_values(by='Age', inplace=True)
```

### カラムの追加

```python
# 方法1
df['AB'] = df['A'] + df['B']

# 方法2
df.loc[:, 'AB'] = df['A'] + df['B']
```

### 欠損値の処理

- pandasは通常np.nanで欠損値を表現。これらの欠損値は計算時には基本的に無視される。

| コマンド | 説明 |
|:--|:--|
| `df.dropna()` |欠損値がひとつでも含まれていたら、行を落とす |
| `df.dropna(how='all')` | すべての値が欠損していたら、行を落とす |
| `df.fillna(0)` | 欠損値を0で埋める |
| `df.fillna(method='ffill')` | 前の値で欠損値を埋める |

### 削除

| コマンド | 説明 |
|:--|:--|
| `df.drop("Tmp", axis=1)` | カラムの削除 |
| `df.drop_duplicated()` | 重複した行の削除 |

### 文字列メソッド

| コマンド | 説明 |
|:--|:--|
| `s.str.lower()` | 小文字に変換 |
| `s.str.startswith('A')` | Aから始まるか検証 |
| `s.str.contains('^[Aa]')` | 正規表現を満たすかどうか検証 |
| `s.str.strip()` | 両端の空白文字を取り除く |

### カテゴリー関連

| コマンド | 説明 |
|:--|:--|
| `df['dcodes'] = df['d'].astype('category').cat.codes` | カテゴリーごとに新規IDを振る |

### データの結合

| コマンド | 説明 |
|:--|:--|
| `pd.concat([df1, df2], axis=0)` | 行方向に結合 |
| `df1.append(df2, ignore_index=True)` | 行方向に結合。インデックスは振り直し。|
| `df1.join(df2)` | 列方向に結合 |
| `pd.merge(df_left, df_right, how='inner', on='key')` | SQLスタイルのマージ |

### グルーピング

Group byという操作は1つ以上の以下のステップを含む

- Split: ある指標に基づき、データをグループに分割
- Apply: グループごとにある関数を適用
- Combine: 結果をまとめてデータ構造体に入れる

| コマンド | 説明 |
|:--|:--|
| `df.groupby(['A', 'B']).sum()` | グルーピングした結果を足し合わせる |
| `df.groupby(['A', 'B']).apply(lambda x: (x - x.mean()) / x.std())` | グルーピングした結果をホワイトニング |
| `df.groupby(['A', 'B']).agg(['mean', 'std'])` | グルーピングした結果の平均と標準偏差を求める |
| `df.pivot_table(values='D', index=['A', 'B'], columns=['C'], aggfunc=np.mean)` | ピボットテーブルを作成 |

### 階層インデックス

| コマンド | 説明 |
|:--|:--|
| `df.stack()` | カラムからインデックスへ |
| `df.unstack()` | インデックスからカラムへ |

```python
tuples = list(zip(*[['bar', 'bar', 'baz', 'baz'],
                    ['one', 'two', 'one', 'two']]))
index = pd.MultiIndex.from_tuples(tuples, names=['first', 'second'])
df = pd.DataFrame(np.random.randn(4, 2), index=index, columns=['A', 'B'])
df_stacked = df.stack()
df_stacked.index.names = ['first', 'second', 'third']
```

## 時系列データ	

### 時系列データの基本処理

| コマンド | 説明 |
|:--|:--|
| `pd.date_range('20170101', periods=7)` | 2017年の元旦から7日間のタイムスタンプをインデックスとして取得 |
| `pd.to_datetime(s)` | sをdatetimeに変換 |
| `ts.asfreq('5Min')` | 一定周期でスポットサンプリング（周期から値を1つだけ選択） |
| `df[['A', 'B']]['2017-01-01':'2017-01-07']` | 2017年1月1日から2017年1月7日までのAとBに関するデータを取得 |
| `ts.asfreq('1T').ffill(limit=3)` | 1分ごとにスポットサンプリングし、欠損値は3ステップまで埋める |
| `ts.resample('5Min').mean()` | 一定周期でリサンプリング（周期間の値をすべて使って演算） |
| `df['A'].resample('3T', how=['mean', 'std', 'count'])` | 3分毎にリサンプリングしたデータに対し、各種統計量を求める |
| `ts.at_time(datetime.time(18, 30))` | 18時30分のデータのみを取得。`import datetime`を仮定 |
| `ts.pct_change()` | 変化量検出 |
| `ts.rolling(50).mean()` | 移動平均 |

### タイムゾーン

| コマンド | 説明 |
|:--|:--|
| `ts_utc = ts.tz_localize('UTC')` | 時刻をUTC（協定世界時）に合わせる |
| `ts_utc.tz_convert('US/Eastern')` | US/Eastern（アメリカ東部標準時間）にタイムゾーンを変更 |
| `ts_utc.tz_convert('Japan')` | 日本標準時間にタイムゾーンを変更 |

## 参考資料

- [10 Minutes to pandas](http://pandas.pydata.org/pandas-docs/stable/10min.html)
- [CheatSheet: Data Exploration using Pandas in Python](https://www.analyticsvidhya.com/blog/2015/07/11-steps-perform-data-analysis-pandas-python/)
- [Pandas DataFrame Notes](http://www.webpages.uidaho.edu/~stevel/504/Pandas%20DataFrame%20Notes.pdf)
- [PyData.Okinawa Meetup #18 - Pandasでデータ前処理](https://github.com/PyDataOkinawa/meetup018)
- [sinhrksさんのブログ(StatsFragments)のpandas記事](http://sinhrks.hatenablog.com/archive/category/pandas)
- [Python For Data Science Cheat Sheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/PandasPythonForDataScience.pdf) from DataCamp
- [Data Wrangling with Pandas Cheat Sheet](https://github.com/pandas-dev/pandas/blob/master/doc/cheatsheet/Pandas_Cheat_Sheet.pdf)