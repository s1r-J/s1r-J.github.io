---
layout: article
title: Lodash
permalink: /docs/nodejs/lodash
date: 2021-04-11
aside:
  toc: true
tags:Node.js
---

## Lodash

- [lodash - npm](https://www.npmjs.com/package/lodash)
- [Lodash](https://lodash.com/)

Lodashとは、JavaScriptの便利なメソッドを集めたユーティリティモジュールである。JavaのApache StringUtilsのような感じだと思う。

> Lodash makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, strings, etc.

さて、似ているモジュールに[Underscore.js](https://underscorejs.org/)が存在している。この2つには関係はないようだ。一般的にはLodashのほうがメソッドが多いなどの理由から上位互換と認識されている。npmでは現時点ではLodash.jsのほうがダウンロード数が多く、人気のようだ。

また、以下の記事のようにJavaScript(ECMA Script)の進歩によって、Lodash自体が不要ではないかとも言われているらしい。

- [you-dont-need/You-Dont-Need-Lodash-Underscore: List of JavaScript methods which you can use natively + ESLint Plugin](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore)
    - 日本語訳：[Lodash/Underscoreは必要ない（かも） - Qiita](https://qiita.com/ossan-engineer/items/ad5313d84da82c6ac421)

Lodashは様々な環境で利用できるように、いくつかのビルドおよびモジュールで提供されている。

### 使い方

一般的に`_`（アンダースコア）としてロードする。

```js
var _ = require('lodash');
```

実装に手間がかかると感じたら、[Lodashのサイト](https://lodash.com/)のドキュメントを探して使えそうなメソッドを探すとよさそう。  
特徴的なメソッドは徐々にメモしていきたい。

Lodashを使わずともJS単体で対応できることもあるので、要勉強。  
以下のようなモダンなJSの構文の記事も参考にする。

- [Modern JavaScript Cheatsheet | Modern JS Cheatsheet](https://mbeaudru.github.io/modern-js-cheatsheet/)
