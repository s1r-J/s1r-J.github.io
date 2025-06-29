---
layout: article
title: querystringモジュール
permalink: /docs/nodejs/querystring
date: 2021-03-10
aside:
  toc: true
tags: Node.js
---

使ってみたソースコードは[GitHub](https://github.com/s1r-J/nodejs-module-labo/tree/main/querystring)にあります。

## Query string

[Query string | Node.js v14.16.0 Documentation](https://nodejs.org/docs/latest-v14.x/api/querystring.html)

Nodejs標準モジュールのひとつ。URLのクエリストリングをオブジェクトから作成したり、反対に文字列からオブジェクトに変換したりする。Webアプリでは必須なモジュール。

似ているモジュールとしては`qs`が存在する。

クエリストリング：`http://example.com?foo=bar&w=%E3%81%82`のようなURLの`?`以降の部分`

メソッド一覧

| 関数名 | 説明 |
| --- | --- |
| decode | `parse`と同じ |
| encode | `stringfy`と同じ |
| [escape](#escape(str)) | 文字列をURLパーセントエンコーディングする。stringfyメソッドから呼び出される。unescapeの逆。 |
| [parse](#parse) | 文字列をデコーディングしてオブジェクトにする。デフォルトではunescapeメソッドを使ってURLパーセントデコーディングする。 |
| [stringfy](#stringfy) | オブジェクトをエンコーディングする。デフォルトではescapeメソッドを使ってURLパーセントエンコーディングする。 |
| [unescape](#unescape) | URLパーセントエンコーディングされた文字列をデコードする。parseメソッドから呼び出される。escapeの逆。 |

escapeはURLエンコーディングする、unescapeはURLデコーディングするという反対の関係。
stringfyはデフォルトのエンコーディング方式としてescapeを使い、オブジェクトを文字列に変換する。
parseはデフォルトのデコーディング方式としてunescpeを使い、文字列をオブジェクトに変換する。


### escape(str)

- str string URLパーセントエンコーディングをおこなう文字列

URLクエリストリングの要件に適したURLパーセントエンコーディングを引数の文字列に対しておこなう。

escapeメソッドは基本的には直接呼び出さない。stringfyメソッドから呼び出されることが本来の使われ方である。  
エクスポートされているのは、このメソッドを別のエンコーディング方式に差し替えて、stringfyメソッドの処理方法を変更するため。
stringfyメソッドのデフォルトのエンコーディング方式はこのescapeメソッド（=URLパーセントエンコーディング）である。

サンプルでは「い」を「1」に置換するというエンコーディング方式に変更してみた。

### parse(str[, sep[, eq[, options]]])

- str string デコーディングをおこなう文字列
- sep string キーバリューのペアを区切る文字。デフォルトは`&`。
- eq string キーとバリューを区切る文字。デフォルトは`=`。
- options Object
	- decodeURIComponent Function デコーディング方式。デフォルトはunescapeメソッド（=URLパーセントデコーディング）。
	- maxKeys number パース（エンコーディング）するキーの最大数。デフォルトは1000。0を指定したときには無制限となる。

引数の文字列を、URLパーセントデコーディングしたうえでキーとバリューのペアのオブジェクトに変換（パース）する。

引数sepはキーバリューのペアを区切る文字に利用される。引数を指定しない場合は`&`となる。
引数eqはキーとバリューを区切る文字に利用される。引数を指定しない場合は`=`となる。

引数option 

```
{
	decodeURIComponent: querystring.unescape
	maxKeys: 1000
}
```

### stringify(obj[, sep[, eq[, options]]])

- obj Object エンコーディングをおこなうオブジェクト
- sep string キーバリューのペアを区切る文字。デフォルトは`&`。
- eq string キーとバリューを区切る文字。デフォルトは`=`。
- options Object
	- encodeURIComponent Function エンコーディング方式。デフォルトはescapeメソッド（=URLパーセントエンコーディング）。

引数のオブジェクトを、URLパーセントエンコーディングしたうえでキーとバリューのペアの集合にエンコードする。

配列は各要素が同じキーで並ぶ。`{ foo: ['bar', 'hoge']}`は`foo=bar&foo=hoge`となる。

注意：ネストされたオブジェクトはバリューがエンコーディングできず、キーだけ出力される。

`{ foo: { bar: 2}, hoge: 'piyo'}`というオブジェクトは`foo=&hoge=piyo`のように`foo=`だけ出力される。

引数sepはキーバリューのペアを区切る文字に利用される。引数を指定しない場合は`&`となる。
引数eqはキーとバリューを区切る文字に利用される。引数を指定しない場合は`=`となる。

引数option 

```
{
	encodeURIComponent: querystring.escape
}
```

### unescape(str)

- str string デコードするURLパーセントエンコーディングされた文字列

URLパーセントエンコーディングされた文字列をデコードする。つまり、escapeの逆をおこなう。

escapeメソッドと同じく、このunescapeも基本的には直接呼び出さず、parseメソッドから呼び出される。
parseメソッドでのデコーディング方式を差し替えるためにエクスポートされている。

