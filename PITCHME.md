---
## RubyistがScalaを学んでみて

- 0x64物語 Reboot 0x08夜
- 静的型付き言語
- by iwtn


---
## 動機

- モノリシックなシステムではなく、スケールアウトしていけるシステムを作っていくためにRubyでは効率悪いのでは、ぐらい
- 静的型付き自体に特に興味はない
- Akka使ってみたい←ワナビ

---
## 一応、私の背景

- 母プログラミング言語はRuby
- プログラムを考える時はRuby
- あとは適当にかじった

---
## ざっとScala紹介

- オブジェクト指向言語＆関数型言語
- 静的型付き
- 処理系はJVM上で動作
- Javaの資産を使える

---
## 使用した教材

- https://dwango.github.io/scala_text/
- 株式会社ドワンゴさんのScalaの教科書
- PDFもWebもあって便利(GitBook)

---
> 本資料を用いた講義を受講することで
> * プログラミング言語Scalaを用いたアプリケーションを開発できるようになること

---
> * 『Scala スケーラブルプログラミング』（第三版）（通称コップ本）を通読して理解できるようになること
> * 『Scala関数型デザイン&プログラミング ―Scalazコントリビューターによる関数型徹底ガイド』（通称FP in Scala）を通読して理解できるようになること

---
> 読者層としては、
> * 大学の情報学部卒である
> * Java言語の基本知識がある←ここが足りなかった
> * 何か意味のあるアプリケーションを作ったことがある
> * 趣味でTwitter APIなどを触ったり、プログラミングを行っている

---
## 教材への全体的な感想

- マジで他の言語でプログラミングをしていた人向け
- 教材のコンセプトにはぴったり

---
## 軽く紹介

- 型推論とかよくある機能は大体ある
- トレイトがモジュール化するのに重要な機能なので1章割いてある
- エラー処理でOption型を使うとNullPointerException無くなるよ

---
## 面白かったところ

- 関数がすべて Function0 〜 Function22 までのトレイトの無名サブクラスのインスタンス

```scala
val add = new Function2[Int, Int, Int]{
  def apply(x: Int, y: Int): Int = x + y
}

add: (Int, Int) => Int = <function2>
```

---
## 辛かったところ

### 練習問題

> foldLeftを用いて、Listの要素を反転させる次のシグニチャを持ったメソッドreverseを実装してみましょう：

---
### foldLeftとは

- Listを左からの畳み込むもの

```scala
def foldLeft[B](z: B)(f: (B, A) ⇒ B): B
```

---
```
List(1, 2, 3).foldLeft(0)((x, y) => x + y)

       +
      / \
     +   3
    / \
   +   2
  / \
 0   1
```

---
```scala
scala> def reverse[T](list: List[T]): List[T] =
     | list.foldLeft(Nil)((a, b) => b :: a)

<console>:12: error: type mismatch;
 found   : List[T]
 required: scala.collection.immutable.Nil.type
       list.foldLeft(Nil)((a, b) => b :: a)

```

---
```scala
scala> def reverse[T](list: List[T]): List[T] =
     | list.foldLeft(Nil: List[T])((a, b) => b :: a)

reverse: [T](list: List[T])List[T]
```

---
## Scalaどうよ？

- この教科書では関数型であることが強調されている
- sbt重い
- 絶対にちょっとしたスクリプトを組むのには向いていない

---
## 結論

- 勉強にはなったな
- Scalaめんどくせえ
