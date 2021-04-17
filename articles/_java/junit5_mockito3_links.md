---
layout: article
title: JUnit5とMockito3に関するリンクまとめ
permalink: /docs/java/junit5_mockito3_links
date: 2021-04-13
aside:
  toc: true
tags: ["Java", "JUnit", "Mockito"]
---

JUnit5とMockito3を使って実装するときに有用なリンク一覧

## JUnit5

まずは公式ドキュメント

- [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/): JUnit5の公式ドキュメント
- [JUnit 5 ユーザガイド](https://udzuki.jp/public/junit5-user-guide-ja/): ありがたい人による邦訳、下記との違いは不明
- [JUnit 5 ユーザーガイド](https://oohira.github.io/junit5-doc-jp/user-guide/): ありがたい人による邦訳、上記との違いは不明

JUnit5ってなんだっけの説明  
JUnit5とは一体どれを指すのか、そしてライブラリの関連とかそれぞれの役割

- [JUnit 5 でどこが変わったのか - 京都行きたい](https://progret.hatenadiary.com/entry/2019/06/18/191822)
- [JUnit5 使い方メモ - Qiita](https://qiita.com/opengl-8080/items/efe54204e25f615e322f)


JUnit5を使った実装例

- [junit-team/junit5-samples: Collection of sample applications using JUnit 5.](https://github.com/junit-team/junit5-samples)

Matcherの使い方

- [JUnit5メモ(Hishidama's JUnit5 Memo)](https://www.ne.jp/asahi/hishidama/home/tech/java/junit/5/index.html)


JUnit5はHamcrestと合わせたほうがMatcherの幅が広がるので使ったほうがよい。良い記事を探す。

## Mockito3

公式ドキュメント

- [Mockito (Mockito 3.8.0 API)](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html)

Mockitoについては正直雰囲気でした使っていないので、基本的な使い方は自分でもう少し公式ドキュメントを読むか噛み砕いてくれた記事を見つけたいところ。

- [Mockito事始め - 俄](https://niwaka.hateblo.jp/entry/2015/09/19/171610)

特定の場面での使い方

- [Mockitoがstaticメソッドのモックに対応したので試してみた - kamoqq.info](https://kamoqq.info/post/mockito-static-method-mock/)
- [Mockitoで複数回のメソッド呼び出しをモックする \| DevelopersIO](https://dev.classmethod.jp/articles/mockito-multiple-mock-call/)
- [ArgumentMatcherとは - Qiita](https://qiita.com/takenakat/items/61d38d89c912de5d29b1)
- [Mock Java Constructors and Their Object Creation With Mockito \| rieckpil](https://rieckpil.de/mock-java-constructors-and-their-object-creation-with-mockito/)
