---
layout: article
title: Consolidate.js
permalink: /docs/nodejs/consolidate
date: 2021-04-05
aside:
  toc: true
tags: Node.js
---

## Consolidate.js

- [consolidate - npm](https://www.npmjs.com/package/consolidate)
- [tj/consolidate.js: Template engine consolidation library for node.js](https://github.com/tj/consolidate.js)

express.jsと一緒に使うモジュール。express.jsで使うことができる様々なテンプレートエンジンを、統一（consolidate）された呼び出し方（ファンクション）で利用できるようにしたモジュール。

イメージとしては、デザインパターンのAdapterパターンのようなものだと認識している。ejsやpug等の異なるテンプレートエンジンに対して、共通的なメソッド名で呼び出せるようにアダプタ（Consolidate.js）を利用するというようなイメージである。

「consolidate」には、「統合する、まとめる、合併する」という意味があるらしい。

使ってみたソースコードは[GitHub](https://github.com/s1r-J/nodejs-module-labo/tree/main/consolidate)にあります。

## API

### 基本

`cons.*(path[, locals], callback)`という形式でテンプレートエンジンを使った結果を取得できる（`*`はテンプレートエンジンの名称）。  
引数`path`はテンプレートファイル, 引数`locals`はテンプレートファイルに渡すオブジェクト、引数`callback`は`function (err, html)`のような形式にする。`err`はテンプレートエンジンの実行時にエラーが発生したときのエラー、`html`はテンプレートエンジンでの変換結果となる。

上記のGitHubにあるソースコードの`index.js`から抜粋する。  
テンプレートエンジンの変換結果を確認するにはexpress.jsは不要。

テンプレートエンジン`ejs`を利用するには`npm install ejs`でインストールしておく必要がある。  
`consolidate`があれば全部インストールされると思ったので少し戸惑った。考えてみれば当然で、全てのテンプレートエンジンが`consolidate`と一緒にインストールされたら非常に大きいモジュールとなってしまう。

```js
const cons = require('consolidate');

cons.ejs('views/ejs.html', { user: 'Chris Paul' }, function(err, html) {
  if (err) {
    throw err;
  }

  console.log('ejs');
  console.log(html);
});
```

`views/ejs.html`はejsの記法に従って以下のようにした。変数`user`に最初の関数で渡した値（つまり、「Chris Paul」）がセットされて、出力される。

```html
<div>
  <h1>template engine: ejs</h1>
</div>
<div>
  <p>
    User: <%= user %>
  </p>
</div>
```

異なるテンプレートエンジン（今回は`jazz`）も同じ構文で利用できた。  
基本的にejsと違うのは`cons.*`の部分だけである。

```js
cons.jazz('views/jazz.html', { user: 'Joe Ingles' }, function(err, html) {
  if (err) {
    throw err;
  }

  console.log('jazz');
  console.log(html);
});
```

`views/jazz.html`はjazzの記法に従って以下のようにした。

```html
<div>
    <h1>template engine: jazz</h1>
  </div>
  <div>
    <p>
    {if user}
      Hello, {user}
    {end}   
    </p>
</div>
```

### 動的にテンプレートエンジンを変更する

ちょっと応用したパターンとして、変数を利用してテンプレートエンジンを動的に変更することができる。

```js
let engine = 'ejs';
cons[engine]('views/ejs.html', { user: 'Devin Booker' }, function(err, html) {
  if (err) {
    throw err;
  }

  console.log('ejs');
  console.log(html);
});
```

### Promiseを使う

callback関数はPromiseを使って、同期的に利用することができる。  
テンプレートエンジンによる変換は時間がかかるはずなので、利用する機会もあるだろう。

```js
cons.jazz('views/jazz.html', { user: 'Donovan Mitchell' })
  .then(function (html) {
    console.log('jazz');
    console.log(html);
  })
  .catch(function (err) {
    throw err;
  });
```

### express.jsと合わせて使う

[GitHub](https://github.com/s1r-J/nodejs-module-labo/tree/main/consolidate)にサンプルコードを用意した。

`server.js`を`node server`で実行することで試すことができる。

### キャッシュを使う

一部のテンプレートエンジンはキャッシュを利用することができる。Consolidate.jsでも、キャッシュの機能を持つテンプレートエンジンにキャッシュを利用させられる。

キャッシュを使うには、`{cache: true}`というオブジェクトを渡す。
`cons.*(path[, locals], callback)`の引数`locals`に`{cache: true}`を含めることでキャッシュ機能を有効化できる。

```js
cons.ejs('views/ejs.html', { user: 'Chris Paul', cache: true }, function(err, html) {
  if (err) {
    throw err;
  }

  console.log('ejs');
  console.log(html);
});
```

express.jsを使っている場合には`app.locals.cache = true`または環境変数`NODE_ENV`に`production`を指定することでキャッシュを有効化できる。

### 注意点

いくつかのテンプレートエンジンでは注意が必要らしい。  
詳しくは[READMEのNotes](https://github.com/tj/consolidate.js#notes)に記載されている。

## 利用できるテンプレートエンジン

Consolidate.jsで利用できるテンプレートエンジンは、[README](https://github.com/tj/consolidate.js#supported-template-engines)に書いてある。

`cons.*`で呼び出すときの`*`と実際のパッケージ名が異なることがあるため、呼び出し時やインストール時には注意する。  
例： `cons.liquid`で呼び出すが、 実際のパッケージ名は`tinyliquid`である。
