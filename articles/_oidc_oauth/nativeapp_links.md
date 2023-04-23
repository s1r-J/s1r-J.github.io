---
layout: article
title: ネイティブアプリでのOAuth・OIDCに関するリンク集
permalink: /docs/oidc_oauth/nativeapp_links
date: 2023-04-23
aside:
  toc: true
tags: ["ネイティブアプリ", "RFC8252", "リンク集", "Universal links", "App links", "カスタムURLスキーム"]
---

ネイティブアプリでのOAuth・OIDCに関する参考になるリンクを記載しておく。

ネイティブアプリにはバックエンドサーバを持つもの、持たないもの（クライアントシークレットを安全に管理できるかできないか）という複数パターンが存在すること、そもそもWebブラウザベースではないことからOAuth・OIDCの想定になかったケースであること、iPhoneやAndroidといった端末OSによる仕様・実装の違いや変化に対応する必要があることなど課題が多い。

## RFCなど

- [RFC 8252: OAuth 2.0 for Native Apps](https://www.rfc-editor.org/rfc/rfc8252)
  - ネイティブアプリのOAuth 2.0のフローについて規定されている
  - [RFC 8252 - OAuth 2.0 for Native Apps 日本語訳](https://tex2e.github.io/rfc-translater/html/rfc8252.html)
- [OAuth 2.0 for Mobile and Native Apps](https://oauth.net/2/native-apps/)
[Guest Blog: Implementing App-to-App Authorisation in OAuth2/OpenID Connect \| OpenID](https://openid.net/2019/10/21/guest-blog-implementing-app-to-app-authorisation-in-oauth2-openid-connect/)


- [RFC 8252 OAuth 2.0 for Native Apps - Qiita](https://qiita.com/unhurried/items/d2fb100e50c0b596ff41)
- [OAuth 2.0・OpenID ConnectでのEmbedded User-Agentの扱い - Qiita](https://qiita.com/unhurried/items/fbd538b5f4b24a0a5999)
- [Google Developers Japan: ネイティブ アプリの OAuth インタラクションを最新にしてユーザビリティとセキュリティを向上する](https://developers-jp.googleblog.com/2016/09/modernizing-oauth-interactions-in-native-apps.html?m=1)


## Universal Links・App Links

- [Universal Linksを試してみました。関連づけファイル(apple-app-site-association）はS3に置きました。 \| DevelopersIO](https://dev.classmethod.jp/articles/universal-links/)
[App Linksに対応してみた - Qiita](https://qiita.com/noboru_i/items/fd4634ecb326b3749ac0)
- [URLスキーム・独自ディープリンク実装に代わる、Universal Links(iOS 9で導入)でより良いUXを実現 - Qiita](https://qiita.com/mono0926/items/2bf651246714f20df626)
- [Android App Linksの複数ホスト対応と、Android App Links対応Webサイトに対して複数アプリを関連付けるための知見 - クックパッド開発者ブログ](https://techlife.cookpad.com/entry/2022/05/31/100000)
- [apple-app-site-associationのpaths(遷移対象パス)の作り方（UniversalLinks対応） - Qiita](https://qiita.com/keroppi0_0/items/1a7fab4a8cc78412d30c)
- [ユニバーサルリンクを利用する \| LINE Developers](https://developers.line.biz/ja/docs/ios-sdk/objective-c/universal-links-support/#ul-s1)
- [今更だけど試してみようUniversalLink - Takahiro Octopress Blog](https://grandbig.github.io/blog/2017/12/02/universallink/)
- [\[iOS\] Universal Linksの「apple-app-site-association」へのアクセスにIP制限がかかっている場合の動作について \| DevelopersIO](https://dev.classmethod.jp/articles/ios-universal-link-developer-mode/)


## 攻撃

- [カスタムURLスキームの乗っ取りとその対策 - Akaki I/O](https://akaki.io/2021/url_scheme_hijack)
- [OAuthにおける認可コード横取り攻撃とその対策 - Akaki I/O](https://akaki.io/2021/authz_code_interception)

## ネイティブアプリ実装

- [Webサービスを通してユーザーを認証する - 日本語ドキュメント - Apple Developer](https://developer.apple.com/jp/documentation/authenticationservices/authenticating_a_user_through_a_web_service/)
- [ios - How to close ASWebAuthenticationSession with redirect to external website not to app universal link - Stack Overflow](https://stackoverflow.com/questions/75408658/how-to-close-aswebauthenticationsession-with-redirect-to-external-website-not-to)

### AppAuth

- [AppAuth](https://appauth.io/)
- [AndroidでAppAuthを使ってOAuth 2.0認証を行う - asoview! TECH BLOG](https://tech.asoview.co.jp/entry/2022/12/24/104204)
- [iOS Setup and AppAuth Sample – OAuth Developer Experience](https://authguidance.com/ios-setup/)
