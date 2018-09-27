---
lang: ja-jp
title: 型、型クラス
tags: Haskell, 型クラス, type
---

# 型、型クラス

## 型付け規則(typing rule)

`f :: Char -> String`という関数と`x :: Char`という式があるとき、関数適用した`f x`の型は`String`である、という規則。

## 多相性(polymorphism)

### パラメータ多相(parametoric polymorphism)

1つの式に汎用の型を表す型変数を割り当て、複数の具体的な型で利用できるようにした型システム

```haskell
sample :: (t1 -> t) -> t1 -> t
sample f x = f x
```

### アドホック多相(ad-hoc polymorphism)

**型クラス(type class)** を利用して型によってそれぞれ異なる実装の式を扱える。例えば`1 == 1`と`"hoge" == "hoge"`では`==`において全く違う実装が使われている。

## 型推論(type inference)

型を指定せずとも処理系が自動で型を決定してくれる。

```haskell
> hello name = "hello, " + name
> :t hello
hello :: [Char] -> [Char]
```

## 型コンストラクタ(type constructor)

これまで単純に型と呼んできたもの。型引数をとることもある。(`IO`,`Maybe`,`->`,`,`など)

```haskell
> :t undefined :: Int Double
error: ...(ry
```

> `undefined`はボトムであり、任意の型の式として扱える。

### kind

型を組み合わせる際のルールを規定するために使うもの。

## 型変数(type variables)

```haskell
> :t id
id :: a -> a
> :t head
head :: [a] -> a
```

### 型制約(type constraints)

`expression:: type-constraints type-variables => type` 

```haskell
> :t show
show :: Show a => a -> String
```

`show`関数において型変数`a`に代入できるのは`Show`型のクラスに属する型のみ。ということを表す。