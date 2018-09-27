---
lang: ja-jp
title: Python memo
tags: python, sort, lambda
---

# Python memo

## ソート

- `sorted(iterable, key = none, reverse = False)`
    - 任意の*iterable*をソートできる
- `list.sort(key = none, reverse = False)`
    - リストにのみ実装できる。

`sort()`はインプレースにリストをソートする。

```python
>>> a = [3, 5, 4, 1, 2]
>>> sorted(a)
>>> [1, 2, 3, 4, 5]
>>> a
>>> [3, 5, 4, 1, 2]
>>> a.sort()
>>> a
>>> [1, 2, 3, 4, 5]
```

## 多次元リストのソート

**lambda式**を使う

```python
>>> list = [[5, 3], [2, 5], [4, 4], [1, 2], [3, 1]]
>>> sorted(list, key = lambda x: x[0])
[[1, 2], [2, 5], [3, 1], [4, 4], [5, 3]]
>>> sorted(list, key = lambda x: x[1])
[[3, 1], [1, 2], [5, 3], [4, 4], [2, 5]]
```

## whileやifのboolean

`None`や、`0`は`False`扱いされる。

```python
>>>i = 3
>>>while i:
...    i-=1
...    print(i)
2
1
0
```

## pythonの三項演算子

```python
(変数) = (条件がTrueのときの値) if (条件) else (条件がFalseのときの値)
```
