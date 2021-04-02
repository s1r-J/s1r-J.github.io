---
layout: article
title: corsモジュール
permalink: /docs/nodejs/cors
date: 2021-03-11
aside:
  toc: true
tags: nodejs
---

## corsモジュール

- [cors - npm](https://www.npmjs.com/package/cors)
- [expressjs/cors: Node.js CORS middleware](https://github.com/expressjs/cors)

サーバーサイドでCORS（オリジン間リソース共有）対応をおこなうために使われる便利なモジュール。express.jsのミドルウェアとして利用する。

CORSとは、あるサイトを表示するときに異なるオリジン（ドメイン）からデータを取得する場合、それを許可する処理を必要とする仕組み。  
あるリクエストに対し、サーバーはリソースにアクセスできるドメインをレスポンスの`Access-Control-Allow-Origin`ヘッダにて応答する必要がある。
また、特定のHTTPメソッドでは本命のリクエストを送る前にプリフライトリクエストを送り、サーバのCORS対応（=`Access-Control-Allow-Origin`ヘッダの値）を確認することがある。

ブラウザのコンソールに`Access-Control-Allow-Origin`と書かれたエラーが発生している場合、その原因はCORS対応ができていないことにある。
CORSについて詳しくは[オリジン間リソース共有 (CORS) - HTTP | MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/CORS)を参照。

ついでにこちらも：[Access-Control-Allow-Origin - HTTP | MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Access-Control-Allow-Origin)

基本的にCORSの仕様について把握していれば、分かる内容だとおもう。このモジュールについて調べながら少し勉強することになった。

### middlewareWrapper([o])

- o Object CORSの設定情報。省略時のデフォルト値は下記参照。

引数`o`のプロパティは以下の表を参照。

| プロパティ名 | 型 | 説明 |
| --- | --- | --- |
| origin | boolean, string, regexp, array, function | レスポンスヘッダ`Access-Control-Allow-Origin`を設定する、つまりどのドメインからのアクセスを許可するかを設定する。デフォルトでは全てのドメインを許可する。<br/>boolean: `true`の場合、リクエストのドメインをそのまま返す。`false`の場合、CORS対応をおこなわない。<br/>string: 特定のドメイン名を記載する（例: `http://example.com`）。<br/>regexp: 正規表現で一致するドメインを許可する（例: `/example\.com$/`）。<br/>array: 許可するドメインを配列で記載する。配列の要素は文字列でも正規表現でも構わない（例: `["http://example1.com", /\.example2\.com$/]`）。<br/>function: 独自の関数で値を決定する。例えばDBに登録されている値を呼び出すなど。実装例を後述した。 |
| methods | string, array | レスポンスヘッダ`Access-Control-Allow-Methods`を設定する、つまりどのメソッドを許可するかを設定する。<br/>string型の場合はカンマ区切りでメソッドを指定する（例：`'GET,PUT,POST'`）。配列での指定も可能（例：`['GET', 'PUT', 'POST']`）。<br/>デフォルトでは全てのメソッドを許可する。 |
| allowedHeaders | string, array | レスポンスヘッダ`Access-Control-Allow-Headers`を設定する、つまり許可するリクエストヘッダを設定する（正確にはプリフライトリクエストに対して許可されているリクエストヘッダとして示す値を設定する）。<br/>デフォルトでは、プリフライトリクエストのヘッダ`Access-Control-Request-Headers`の値をそのまま返す。<br/>string型の場合はカンマ区切りでヘッダ名を指定する（例：`'Content-Type,Authorization'`）。配列での指定も可能（例：`['Content-Type', 'Authorization']`）。 |
| exposedHeaders | string, array | レスポンスヘッダ`Access-Control-Expose-Headers`を設定する、つまりレスポンスで返却するヘッダを設定する。[CORSセーフリストレスポンスヘッダ](https://developer.mozilla.org/en-US/docs/Glossary/CORS-safelisted_response_header)なるものがあるらしく、デフォルトではこれ以外のカスタムヘッダは許可しない。 |
| credentials | `true` | レスポンスヘッダ`Access-Control-Allow-Credentials`の値を設定する、つまり認証情報（Cookie、認証ヘッダ、またはTLSクライアント証明書）を使ったリクエストを許可するかどうかを設定する。<br/>許可する場合は`true`を設定し、許可しない場合はこのプロパティを省略する。 |
| maxAge | number(integer) | レスポンスヘッダ`Access-Control-Max-Age`を設定する、つまりプリフライトリクエストの結果をキャッシュできる時間（単位は秒）を設定する。<br/>デフォルトではキャッシュは無効と思われる。指定しない場合はプロパティを省略する。 |
| preflightContinue | funtion | プリフライトリクエストをこのモジュールで処理した後、引数の関数に渡す。<br/>デフォルトでは`false`。 |
| optionSuccessStatus | number | HTTPメソッド`OPTIONS`によるプリフライトリクエストに対し、成功したときのステータスコードを設定する。<br/>デフォルトでは`204`となっている。 |

よって、デフォルトでは以下のようになる。

```
{
  "origin": "*",
  "methods": "GET,HEAD,PUT,PATCH,POST,DELETE",
  "preflightContinue": false,
  "optionsSuccessStatus": 204
}
```

expressjsのミドルウェアとして利用されるため、エクスポートされているメソッドは`middlewareWrapper(o)`だけである。  
ファイルも非常にシンプルで実装自体は`lib/index.js`だけであった。

今回実際に動かすのは少々手間なので、モジュール作者がサンプルとして用意した環境を触りながら確認するとよさそう。

- [公開されている環境](https://node-cors-client.netlify.app/)
    - [クライアントアプリのソースコード](https://github.com/troygoode/node-cors-client)
    - [サーバーサイドのソースコード](https://github.com/troygoode/node-cors-server)

以下は公式サイトのソースコードを丸コピもしくは一部改変している。

#### 全経路にCORS対応をおこなう

一般的なexpress.jsのミドルウェアらしく、`use`メソッドにcorsモジュールを指定する。これで全てのパスでcorsモジュールが呼び出される。

```js
var express = require('express')
var cors = require('cors')
var app = express()

app.use(cors())

app.get('/products/:id', function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for all origins!'})
})

app.listen(80, function () {
  console.log('CORS-enabled web server listening on port 80')
})
```

### 特定の経路にCORS対応を入れる

特定の経路にだけ設定する場合、その経路のメソッドの第2引数以降に設定する。

下記の場合は、`/product/123`のようなパスではCORS対応があるが、`/animals`というパスではCORS対応がないことになる。

```js
var express = require('express')
var cors = require('cors')
var app = express()

app.get('/products/:id', cors(), function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for a Single Route'})
})

app.get('/animals', function (req, res, next) {
  res.json({msg: 'This path is CORS-disabled'})
})

app.listen(80, function () {
  console.log('CORS-enabled web server listening on port 80')
})
```

### CORS対応の設定をおこなう

corsモジュールmiddlewareWrapperメソッドの引数に値を設定し、CORS対応の設定をおこなう。

下記の場合は、許可するドメインは`http://example.com`で、プリフライトリクエストに対するレスポンスのステータスコードは`200`に設定している。

```js
var express = require('express')
var cors = require('cors')
var app = express()

var corsOptions = {
  origin: 'http://example.com',
  optionsSuccessStatus: 200 // some legacy browsers (IE11, various SmartTVs) choke on 204
}

app.get('/products/:id', cors(corsOptions), function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for only example.com.'})
})

app.listen(80, function () {
  console.log('CORS-enabled web server listening on port 80')
})
```

### 独自関数でドメインを設定する

middlewareWrapperメソッドの引数のoriginプロパティで関数を指定したときの挙動および関数の例を示す。

アクセス許可するオリジンをデータベースに登録している場合などに有用な設定である。

originプロパティに設定する関数は、`function(origin, callback)`のような形式とする。引数`origin`にはリクエストを送ってきたドメインが入る。引数`callback`はこの独自の関数の処理が終わったときに呼び出す関数で、`callback(error, origins)`のように使う。このとき、引数`error`は独自関数でエラーが発生したときに値を設定する。引数`origins`はアクセスを許可するオリジン（ドメイン）を設定する。この値はmiddlewareWrapperメソッドの引数のoriginプロパティで指定できる値である必要がある。

`db.loadOrigins`は、データベースに問い合わせをおこない、アクセスを許可するオリジン（ドメイン）の情報を取得する呼び出しである。  
`db.loadOrigins`はコールバック関数を引数に持ち、エラーが発生した場合には第1引数`error`にその情報を格納する。値を取得した場合、第2引数`origins`にその値を格納する。この呼び出しがエラーとなっても正常終了しても、今度は`callback`という関数が呼び出される。DB問い合わせがあれば、エラーを関数`callback`の第1引数にセットし、値を取得できればそれを第2引数にセットする。

```js
var express = require('express')
var cors = require('cors')
var app = express()

var corsOptions = {
  origin: function (origin, callback) {
    // db.loadOrigins is an example call to load
    // a list of origins from a backing database
    db.loadOrigins(function (error, origins) {
      callback(error, origins)
    })
  }
}

app.get('/products/:id', cors(corsOptions), function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for an allowed domain.'})
})

app.listen(80, function () {
  console.log('CORS-enabled web server listening on port 80')
})
```
