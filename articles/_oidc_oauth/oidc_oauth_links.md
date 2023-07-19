---
layout: article
title: OIDCとOAuth2.0について理解するためのリンク集
permalink: /docs/oidc_oauth/links
date: 2021-08-30
aside:
  toc: true
tags: OAuth OAuth2.0 OpenIDConnect
---

OAuth2.0とOpenID Connectについて勉強するときに読んだ、読んでいるリンクのまとめ。

読んだら記事の感想とともに残す。今後も増やす。

## OAuth2.0

- [OAuth 2.0の代表的な利用パターンを仕様から理解しよう - Build Insider](https://www.buildinsider.net/enterprise/openid/oauth20)
	- ユースケースに応じたフロー図および利用するパラメータについて具体的に示されている。
	- 概念についてなんとなくわかった、実際の利用シーンやHTTPリクエスト・レスポンスがどうなっているのか気になり始めたら、見ると良い。
- [OAuth2.0 PKCEとは 〜Stateとの違い〜 - Qiita](https://qiita.com/naoya_matsuda/items/992c67b803ff460818ec)
    - PKCEについての説明
    - 今後PKCEは仕様としても標準になる予定、必ず理解しておくこと
- [図解：OAuth 2.0に潜む「5つの脆弱性」と解決法：デジタルID最新動向（2）（1/4 ページ） - ＠IT](https://www.atmarkit.co.jp/ait/articles/1710/24/news011.html)
	- OAuthの脆弱性についての説明
    - 今は上記以外にも増えてきているはず、要確認
- [OAuth IdP Mix-Up Attack とは？ - OAuth.jp](https://oauth.jp/blog/2016/01/12/oauth-idp-mix-up-attack/)
    - 上記の記事の5つ目にも出ているミックスアップ攻撃
- [OAuth 2.0でのHolder-of-Key TokenとKeycloakについて - Qiita](https://qiita.com/tnorimat/items/ee45d2cb08d799a7d4a6)
    - ちょっと別の内容だが、Bearer以外のトークンについて
- [Financial-grade API (FAPI) WG \| OpenID](https://openid.net/wg/fapi/)
    - FAPIの公式情報
- [実装者による Financial-grade API (FAPI) 解説 - Qiita](https://qiita.com/TakahikoKawasaki/items/83c47c9830097dba2744)
    - FAPIについての記事
- [OAuth 2.1](https://oauth.net/2.1/)
    - 次のOAuthの公式情報

## OpenID Connect

- [OAuth および OpenID Connect — Authlete ナレッジベース](https://kb.authlete.com/ja/s/oauth-and-openid-connect)
- [なぜOpenID Connectが必要となったのか、その歴史的背景](https://www.slideshare.net/tkudo/openid-connect-devlove)
	- OpenID ConnectおよびOAuth、その前に活躍していたSAMLなどの概念をざっくり掴むのに良い。
	- ただし、スライド1枚1枚を詳しく見ていくと初学者は戸惑いそう（戸惑った）。
- [OpenID Connect 概要 (2013年9月)](https://www.slideshare.net/oidfj/openid-connect-intro-september-2013)
	- 上記のスライドと似ているが、OpenID Connectにだけフォーカスした短いスライド（本編だけなら10枚ほど）
	- IDトークンと各フローについて各1枚ずつにまとまっていて、ざっくり復習するには良い。
	- 初学者にはいきなり全て説明されてしまうので戸惑うとおもう（戸惑った）。
- [一番分かりやすい OpenID Connect の説明 - Qiita](https://qiita.com/TakahikoKawasaki/items/498ca08bbfcc341691fe)
	- OpenID Connectの登場人物を擬人化して説明しており、初学者にもわかりやすい。
	- 記事下部のYoutube動画で記事の内容を動画で説明しており、こちらのほうが話が入ってくる気がする。
- [OAuth & OIDC 入門編 by #authlete - YouTube](https://www.youtube.com/watch?v=PKPj_MmLq5E)
	- 上記記事の動画での説明および周辺の用語について詳しく説明している。
	- 実際のHTTPリクエスト・レスポンスを示しながら説明しており、SEとしてはこのほうが理解しやすいと思う。
- [OpenID Connect 全フロー解説 - Qiita](https://qiita.com/TakahikoKawasaki/items/4ee9b55db9f7ef352b47)
    - OIDCのフローのまとめ
    - 頭がこんがらがったら、読むと良い
- [『いまどきの OAuth / OpenID Connect (OIDC) 一挙おさらい』の予習・復習用情報 - Qiita](https://qiita.com/TakahikoKawasaki/items/90ef63fc4f267b33d46d)
- [OpenID Connectユースケース、OAuth 2.0の違い・共通点まとめ - Build Insider](https://www.buildinsider.net/enterprise/openid/connect)
    - 基本的な用語からの記事
    - アプリごとの具体的なフローも示されている、このフローが読めて理解できていれば基本的な実装はできるとおもう
- [オージス総研の製品事例](https://www.ogis-ri.co.jp/news/themistruct/docs/20180531_AWS_Summit_OGIS_1.pdf)
    - 興味があれば
- [アイデンティティ管理の新しい教科書 連載インデックス - ＠IT](https://atmarkit.itmedia.co.jp/fsecurity/index/index_kantara.html)
    - 連載記事
    - OIDCがわかってきたら読むべきか
- [JSON Web Tokens - jwt.io](https://jwt.io/)
    - JWTをブラウザ上で解析、復号化してくれる


## その他

- [OAuth.jp](https://oauth.jp/)
	- OAuthの記事が書かれているブログ
	- 検索はしにくいかもしれない、タイムリーな記事の解説としてみるべきか