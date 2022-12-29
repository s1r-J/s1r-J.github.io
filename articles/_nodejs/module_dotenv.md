---
layout: article
title: dotenvでの環境変数
permalink: /docs/nodejs/dotenv
date: 2022-12-29
aside:
  toc: true
tags: ["Node.js", "dotenv", "JavaScript"]
---

[ブログに書いた記事](https://s1r-j.hatenablog.com/entry/2022/12/29/180654)を少しまとめた記事。

[dotenv](https://www.npmjs.com/package/dotenv)はNode.jsで利用される環境変数を読み込むためによく使われているライブラリ。
`.env`ファイルに書き込んだ環境変数を読み込んで、JSファイルで`process.env`から取得できるようになる。

簡単な例としては以下。

`.env`ファイル

```.env
MY_ENV=myvalue
```

`index.js`ファイル

```javascript
require('dotenv').config();

console.log(process.env.MY_ENV); // myvalue
```

## 環境変数がどのようにJSファイルで扱われるか

色々試したコードは[GitHub](https://github.com/s1r-J/nodejs-module-labo/tree/main/dotenv)においた。

### JSファイルでは全て文字列型になる

`.env`ファイルで文字列ではなく、数値やbooleanのつもりで渡したときにもJSファイルでは文字列型になることに注意。

```.env
STRING_ENV="string value"
NUMBER_ENV=123
BOOLEAN_ENV=true
```

`index.js`ファイルでconsole.logを使って確認してみると、`NUMBER_ENV`および`BOOLEAN_ENV`の両方とも文字列型（`string`）と表示される。

```javascript
require('dotenv').config();

const stringEnv = process.env.STRING_ENV;
console.log('STRING_ENV type:', typeof stringEnv); // string
console.log('STRING_ENV:', stringEnv); // string value

const numberEnv = process.env.NUMBER_ENV;
console.log('NUMBER_ENV type:', typeof numberEnv); // string
console.log('NUMBER_ENV:', numberEnv); // 123

const booleanEnv = process.env.BOOLEAN_ENV;
console.log('BOOLEAN_ENV type:', typeof booleanEnv); // string
console.log('BOOLEAN_ENV:', booleanEnv); // true
```

文字列型から数値型への変換はNumberオブジェクトを利用したり、boolean型には`===`を使って比較したりすることで変換する。

### 複数行

v15以降では複数行の環境変数が利用できる。
必ずクォーテーションで囲むこと。囲まなかった場合は後述。

```.env
MULTI_ENV="THIS IS MULTILINE
ENV VALUE
END"
```

```javascript
require('dotenv').config();

const multiEnv = process.env.MULTI_ENV;
console.log('MULTI_ENV:', multiEnv); // THIS IS MULTILINE
                                     // ENV VALUE
                                     // END
```

`\n`を使っても複数行の環境変数が利用できる。

```.env
ALT_MULTI_ENV="THIS IS ALT MULTILINE\nENV VALUE\nEND"
```

```javascript
require('dotenv').config();

const altMultiEnv = process.env.ALT_MULTI_ENV;
console.log('ALT_MULTI_ENV:', altMultiEnv); // THIS IS ALT MULTILINE
                                            // ENV VALUE
                                            // END
```

ダブルクォーテーションで囲わなかったため、複数行にならないパターンを記述しておく。

```.env
FAIL_MULTI_ENV=THIS IS FAIL MULTILINE
ENV VALUE
END
FAIL_ALT_MULTI_ENV=THIS IS ALT MULTILINE\nENV VALUE\nEND
```

```javascript
require('dotenv').config();

const failMultiEnv = process.env.FAIL_MULTI_ENV;
console.log('FAIL_MULTI_ENV:', failMultiEnv); // THIS IS FAIL MULTILINE

const failAltMultiEnv = process.env.FAIL_ALT_MULTI_ENV;
console.log('FAIL_ALT_MULTI_ENV:', failAltMultiEnv); // THIS IS ALT MULTILINE\nENV VALUE\nEND
```


### クォーテーションとエスケープ

文字列は、`.env`ファイル内でダブルクォーテーション（`"`）で囲ってもシングルクォーテーション（`'`）で囲っても、囲わなくても同じ。

また、クォーテーションを使いたい場合には`\`を使ってエスケープすること。

```.env
STRING_ENV="string value"
NO_QUOTATION_ENV=no quotation env
SINGLEQUOTATION_ENV='singleenv'
ESCAPE_ENV=\"escapeenv\"
```

```javascript
require('dotenv').config();

const stringEnv = process.env.STRING_ENV;
console.log('STRING_ENV:', stringEnv); // string value

const noQuotationEnv = process.env.NO_QUOTATION_ENV;
console.log('NO_QUOTATION_ENV:', noQuotationEnv); // no quotation env

const singleQuotationEnv = process.env.SINGLEQUOTATION_ENV;
console.log('SINGLEQUOTATION_ENV:', singleQuotationEnv); // singleenv

const escapeEnv = process.env.ESCAPE_ENV;
console.log('ESCAPE_ENV:', escapeEnv); // \"escapeenv\"
```

### コメント

`.env`ファイルでは`#`を使うことでそれ以降はコメントになり、変数としては渡されない。
`#`を使いたい場合にはダブルクォーテーションで囲うこと。

```.env
COMMENT_ENV=VALUEISHERE # comment is here
COMMENT_IN_ENV="VALUE#IS#HERE" # comment is here
```

```javascript
require('dotenv').config();

const commentEnv = process.env.COMMENT_ENV;
console.log('COMMENT_ENV:', commentEnv); // VALUEISHERE

const commentInEnv = process.env.COMMENT_IN_ENV;
console.log('COMMENT_IN_ENV:', commentInEnv); // VALUE#IS#HERE
```
