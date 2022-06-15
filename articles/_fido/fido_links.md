---
layout: article
title: FIDOについて理解するためのリンク集
permalink: /docs/fido/fido_links
date: 2021-08-30
aside:
  toc: true
tags: FIDO FIDO2 WebAuthn
---

## 公式情報

W3CやFIDO Allianceの情報

- [Web Authentication: An API for accessing Public Key Credentials - Level 3](https://www.w3.org/TR/webauthn-3/)
    - WebAuthnAPIの仕様
- [Server Requirements and Transport Binding Profile](https://fidoalliance.org/specs/fido-v2.0-rd-20180702/fido-server-v2.0-rd-20180702.html)
    - FIDO Allianceの提供している実装ガイド
- [FIDO Security Reference](https://fidoalliance.org/specs/fido-v2.0-id-20180227/fido-security-ref-v2.0-id-20180227.html)
- [FIDO Alliance - Open Authentication Standards More Secure than Passwords](https://fidoalliance.org/?lang=ja)
	- [仕様概要 - FIDO Alliance](https://fidoalliance.org/%E4%BB%95%E6%A7%98%E6%A6%82%E8%A6%81/?lang=ja)
- [FIDO Alliance Metadata Service - FIDO Alliance](https://fidoalliance.org/metadata/)
	- MDSの公式サイト
	- 仕様へのリンク以外に、実際の認証器データおよびルート証明書が取得できる

## 解説

- [パスワードのいらない世界へ　　FIDO認証の最新状況](https://www.slideshare.net/FIDOAlliance/fido-178936595)
- [2020 0218 - パスワードのいらない世界へ：FIDOアライアンスとFIDO認証の最新状況](https://www.slideshare.net/FIDOAlliance/2020-0218-fidofido)
	- 基本的な用語と概念がわかる
- [FIDO at LINE: パスワードのいらない世界に向けて - LINE ENGINEERING](https://engineering.linecorp.com/ja/blog/fido-at-line/)
    - LINEの事例
- [Web Authentication API - Web API \| MDN](https://developer.mozilla.org/ja/docs/Web/API/Web_Authentication_API)
    - W3Cの仕様を読む前に読んでおき、用語に振り回されないようにするのによい
- [Yahoo! JAPANでの生体認証の取り組み（FIDO2サーバーの仕組みについて） - Yahoo! JAPAN Tech Blog](https://techblog.yahoo.co.jp/advent-calendar-2018/webauthn/)
- [Yahoo! JAPANでの生体認証の取り組み（FIDO2サーバーの仕組みについて） - Yahoo! JAPAN Tech Blog](https://techblog.yahoo.co.jp/advent-calendar-2018/webauthn/)
	- 具体的な処理や実装例がわかる。RPサーバとFIDOサーバに分かれており、若干こんがらがる
- [FIDO2 attestation formatの紹介 - Yahoo! JAPAN Tech Blog](https://techblog.yahoo.co.jp/advent-calendar-2018/webauthn-attestation-packed/)
- [WebAuthnことはじめ \| メルカリエンジニアリング](https://engineering.mercari.com/blog/entry/2019-06-04-120000/)
- [WebAuthn/FIDO2: What’s new in MDS3? Migrating from MDS2 to MDS3. \| by Ackermann Yuriy \| WebAuthn Works \| Medium](https://medium.com/webauthnworks/webauthn-fido2-whats-new-in-mds3-migrating-from-mds2-to-mds3-a271d82cb774)
	- FIDO Alliance Metadata Service(MDS) v3についての記事（英語）
	- v3の特徴、v3で配布されるデータのサンプル、v2からの違いなど
- [WebAuthn/FIDO —Series Content Page - WebAuthn Works - Medium](https://medium.com/webauthnworks/webauthn-fido-series-content-page-4f9a187aa588)
	- WebAuthnとFIDOについての記事がいくつかある（英語）
	- Attestationの検証方法について記事にしてくれているようなので、読みたい
    - [Ackermann Yuriy – Medium](https://herrjemand.medium.com/)
- [Web Authentication API の裏側と、なぜそうなっているのかを図解した - Qiita](https://qiita.com/kyrieleison/items/3dbb8ece94572dc3e962)
    - なんとなくわかるけれど、いきなり読んでもわからないと思う

## 実装例

- [line/line-fido2-server: FIDO2(WebAuthn) server officially certified by FIDO Alliance and Relying Party examples.](https://github.com/line/line-fido2-server)
- [WebAuthnを使ったFIDOサーバを立ててみた - Qiita](https://qiita.com/poruruba/items/243d39c8b77b98a99bab)
- [OpenAM で FIDO2(WebAuthn) ユースケースを考える - Qiita](https://qiita.com/tonoki/items/16a99d770fa496bdaafc)
- [OpenAM 14 パスワードレス認証モジュールでResidentKeyを実装した話 - Qiita](https://qiita.com/tonoki/items/25bc2bc98917c59da433)
	- ResidentKeyについて理解するための記事
