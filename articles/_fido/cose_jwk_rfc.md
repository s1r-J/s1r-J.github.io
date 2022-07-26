---
layout: article
title: COSEとJWKのRFCやらレジストリやらライブラリのリンク集
permalink: /docs/fido/cose_jwk_rfc
date: 2022-07-27
aside:
  toc: true
tags: ["COSE", "CBOR", "JWK", "JOSE", "WebAuthn"]
---

いつも探し回っているので、まとめておく。

## COSE関連

COSEのRFC
[RFC8152 - CBOR Object Signing and Encryption (COSE)](https://datatracker.ietf.org/doc/html/rfc8152)

COSEとJOSE（JWK）の対応に関するRFC
[RFC8812 - CBOR Object Signing and Encryption (COSE) and JSON Object Signing and Encryption (JOSE) Registrations for Web Authentication (WebAuthn) Algorithms](https://datatracker.ietf.org/doc/html/rfc8812)
[RFC 8812 - CBOR Object Signing and Encryption (COSE) and JSON Object Signing and Encryption (JOSE) Registrations for Web Authentication (WebAuthn) Algorithms 日本語訳](https://tex2e.github.io/rfc-translater/html/rfc8812.html)


IANAのレジストリ  
COSEのキーバリューとそれぞれの値の割当が定義されている。

[CBOR Object Signing and Encryption (COSE) | IANA](https://www.iana.org/assignments/cose/cose.xhtml)


QiitaのCOSEについての記事  
- COSEとJOSE関連のRFCや対応情報などが書かれていた。
- JOSE関連（JWS, JWE, JWK等の情報）の複数のRFCは、COSEでは１つのRFCにまとまっている
- COSEのキー情報はJWKに記載されている

[\[CWT入門その2\] CBOR Object Signing and Encryption (COSE) - Qiita](https://qiita.com/ritou/items/bd2d429dae63bf0ad325)


COSEワーキンググループによるJava実装
あんまり見ていない。

[cose-wg/COSE-JAVA: JAVA implementation of the COSE specification](https://github.com/cose-wg/COSE-JAVA)


Webブラウザ上でCBORからの変換とCBORからの変換をしてくれるサイト  
便利

[CBOR playground](https://cbor.me/)


## JWK関連

RFC 

- [RFC7517 - JSON Web Key (JWK)](https://datatracker.ietf.org/doc/html/rfc7517)

IANAのレジストリ
キーバリューとそれぞれの値の意味が定義されている。
[JSON Object Signing and Encryption (JOSE)](https://www.iana.org/assignments/jose/jose.xhtml#web-encryption-compression-algorithms)

## WebAuthn

- attestationObjectはCBORでエンコードされている
- attestationObjectのauthDataのcredential public keyにあたる領域はさらにCBORエンコードされている
- デコードするとPublicKeyがCOSEのルールで表現されている

## Node.jsライブラリ

- [panva/jose](https://github.com/panva/jose)
	- joseのライブラリ: jwkをインポート、エクポートできる。PEMに変換も可能か？
- [jwk-to-pem](https://www.npmjs.com/package/jwk-to-pem)
	- jwkからpemに変換できる。対応しているjwkが少し少ないES256と対応してほしい
- [apowers313/cose-to-jwk](https://github.com/apowers313/cose-to-jwk)
    - coseからjwkに変換できる。jwk-to-pemと合わせてPEMをつくる
- [kjur/jsrsasign](https://github.com/kjur/jsrsasign)
    - jwkは扱うことができ、PEMと変換できる
- [parse-cosekey](https://www.npmjs.com/package/parse-cosekey)
    - COSE、JWK、PEMの相互変換ができる
