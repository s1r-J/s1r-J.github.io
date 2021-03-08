---
layout: article
title: randomstringモジュール
permalink: /docs/nodejs/randomstring
aside:
  toc: true
tags: nodejs
---

## randomstringモジュールの使い方

[klughammer/node-randomstring: A node.js module for generating random strings](https://github.com/klughammer/node-randomstring)

`generate`というメソッドが1つあるだけ。

### generate([options])

引数`options`の条件に従って、ランダムな文字列を生成して返却する。

引数`options`は数値型またはオブジェクトを指定する。

引数を指定しない場合、半角数字と大文字および小文字の半角英字から構成される32文字のランダムな文字列が返却される。

数値型の場合、半角数字と大文字および小文字の半角英字で構成された生成されるランダム文字列の長さを指定したことになる。
基本的には正の整数を引数にすべきである。小数の場合には、切り上げとなる。
また、ゼロもしくはマイナスの場合は空文字列が返却される。

オブジェクトの場合、

```
{
    length: num,
    charset: str,
    capitalization: str,
    readable: bool
}
```

lengthは生成するランダム文字列の長さを決定する。  
引数に数値型をセットした場合には、このプロパティだけ値を設定したのと同じになる。

charsetは生成するランダム文字列に利用する文字種を指定できる。指定可能な文字列は以下の4種類である。

| charset | 内容 |
| -- | -- |
| alphanumeric | 半角数字と大文字および小文字の半角英字。指定がなかった場合のデフォルト設定。 |
| numeric | 半角数字 |
| alphabetic | 大文字および小文字の半角英字 |
| hex | 16進数で利用される文字種、つまり半角数字と半角英小文字の`abcdef` |

capitalizationは生成される文字列全てを大文字もしくは小文字に変換するときに使用する。指定しなかった場合、変換をおこなわれない。

| charset | 内容 |
| -- | -- |
| uppercase | 全て大文字に変換 |
| lowercase | 全て小文字に変換 |


readableは判別しにくい文字種を除外するかどうかを決定するために使う。trueの場合、ゼロ（`0`）、大文字のオー（`O`）、大文字のアイ（`I`）、小文字のエル`l`がランダム生成の文字種として利用されなくなる。生成される文字列の長さが短くなるわけではない。

ランダム文字列の生成には、利用される文字に偏りが生じないような工夫がされており、特に乱数生成には`crypto`モジュールが利用されている。
`crypto`モジュールを使うことで`Math.random()`よりもセキュアに乱数が生成できる。

javaのRandomに対するSecureRandomみたいなものだと認識している。
