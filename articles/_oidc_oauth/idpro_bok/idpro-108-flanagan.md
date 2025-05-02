---
layout: columns
title: "Token Lifetimes and Security in OAuth 2.0: Best Practices and Emerging Trends"
permalink: /docs/oidc_oauth/idpro_bok/108
date: 2024-12-11
modify_date: 2025-05-01
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "OAuth", "トークン", "クレデンシャル"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/108/](https://bok.idpro.org/article/id/108/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

In networked and federated systems using OAuth 2.0 and OpenID Connect, tokens are essential for securely communicating between human and non-human entities without requiring the constant revalidation in every request.  The improper management of these tokens, however, can expose systems to serious threats, such as token replay attacks.

While the most secure practices involve real-time risk-based token revocation and sender-constrained tokens, organizations may not be ready for that, given the maturity of their security infrastructure. Developers and architects should consider the security benefits of using short-lived, narrowly scoped client-bound tokens designed to minimize the risk of misuse. By limiting the lifespan of tokens or binding them to specific clients (as in sender-constrained tokens), organizations can significantly reduce the attack surface and thwart token replay attempts. Identity practitioners must be aware of the limitations of long-lived tokens as well as the best practices for securing token-based systems.

Keywords: OAuth, tokens, credentials

@column
## 概要

OAuth 2.0およびOpenID Connectを利用してネットワーク化され、フェデレーションされたシステムでは、リクエストごとに常に再検証を必要することなく、人間と非人間エンティティとの安全な通信のためにトークンが不可欠です。しかし、これらのトークンの不適切な管理は、システムをトークンリプレイ攻撃のような深刻な脅威にさらすことになります。

ほとんどのセキュアなプラクティスは、リアルタイムにリスクベースのトークン失効およびsender-constrainedなトークンを利用することですが、セキュリティインフラストラクチャの成熟を考慮すると、組織はその準備が整っていないかもしれません。開発者とアーキテクトは、悪用のリスクを最小にするために設計された、短命でスコープの狭く、クライアントにバインドされたトークンを利用するというセキュリティにおける利益を考慮すべきです。トークンの寿命を制限したり、特定のクライアントにトークンをバインド（sender-constrainedなトークンのように）したりすることによって、組織は攻撃対象領域を大きく減らし、トークンリプレイの試みを阻止することができます。アイデンティティ実務者は、トークンベースシステムを保護するためのベストプラクティスだけでなく、長寿命のトークンを制限することについても認識しなければなりません。

**Keywords:** OAuth, トークン, クレデンシャル

@row
By Heather Flanagan (Spherical Cow Consulting)

© 2024 IDPro, Heather Flanagan

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code)._

@row
## Introduction

Identity systems and the use of tokens go hand in hand; their existence is ubiquitous, and the need to manage them carefully is at the core of identity security practice today. But what is a token?

A token is a digital object that can represent a set of claims or attributes about an entity, such as a user, device, or process, typically used in authentication and authorization protocols.[^1] Tokens are often cryptographically signed and/or encrypted to ensure their integrity and confidentiality, preventing tampering and unauthorized access. Tokens are commonly employed in various identity and access management systems, enabling a secure mechanism for proving identity, delegating access, or asserting permissions across networked systems.

Tokens may be differentiated based on whether they require the server to maintain session information. A token may be stateless and only carry encoded information (e.g., claims, user roles, and expiration times) within the token itself, such as JSON Web Tokens (JWTs). This enables a more scalable architecture by reducing demand on the server. Alternatively, a token may be stateful, at which point the contents are always opaque to the client and do not inherently “contain” information. (A stateless token can be opaque as well, if encrypted.) Instead, their meaning is tracked by the issuing server, which maintains the state (e.g., session data, user permissions) associated with the token.

Tokens are also described by how they are used. Tokens can be classified as bearer tokens, which are usable by anyone in possession of them, or client-bound tokens (sometimes called sender-constrained tokens (e.g., Demonstrating Proof of Possession (DPoP)),[^2]), which are bearer tokens cryptographically tied to a specific client. In the OAuth 2.0 Framework, both client-bound tokens and bearer tokens can be used for authorization. Tokens may also be short-lived (expiring within a few minutes or hours) to minimize the risk of misuse or long-lived (remaining valid for extended periods), with the former offering stronger protection against token replay attacks. However, while the OAuth 2.0 framework allows these options, implementation decisions have a meaningful impact on security – which is why various Working Groups have emerged to develop profiles of OAuth 2.0 that are appropriate for use cases requiring heightened security.[^3]

One of the most effective strategies when issuing tokens is to narrowly scope their permissions. A narrowly scoped token is designed to grant access to only a specific resource or a limited set of actions rather than offering broad, unrestricted access. Narrowly scoped tokens limit access to specific resources or actions, reducing the risk of unauthorized access if a token is compromised. This limitation contrasts with broader scopes, which can provide access to multiple services or actions with a single token. Using narrowly scoped tokens, combined with short expiration times, ensures that even if a token is compromised, the damage is limited to a small portion of the system, reducing the risk of unauthorized access to critical resources.

The term ‘credential’ is often used interchangeably with ‘token’; unfortunately, that’s technically incorrect. While tokens and credentials are often related, they serve distinct roles. Credentials are used to authenticate the identity of a user or system, while tokens in OAuth 2.0 are issued after authentication to authorize specific actions. Before the broad adoption of token-based protocols, you may recall that websites would simply ask for (and store) your credentials: they would log in on your behalf and access any data they deemed necessary. This is called ‘screen-scraping.’ By limiting the scope, context, and duration of the tokens they grant, authorization servers protect users (and their credentials) from unscrupulous actors on the internet.

While tokens provide a convenient and flexible way to authorize users, they can also introduce significant security risks if not properly managed. Ideally, organizations are implementing real-time risk-based token revocation.[^4] However, considering the correct lifetime for a given token is necessary for organizations that do not have integrated security management tools.

This brings us to this article and the complicated family of tokens in the OAuth 2.0 framework. OAuth 2.0 is a set of specifications, defined in the Internet Engineering Task Force (IETF) that allow a client to request a set of scoped tokens to enable access to resources such as APIs. Understanding the different types and uses of tokens will help developers and identity and access management professionals understand the implementation considerations they need to consider in their environments.

@column
## イントロダクション

アイデンティティシステムとトークン利用について密接な関係にあります；トークンの存在はユビキタスであり、トークンを注意深く管理する必要性は、今日のアイデンティティセキュリティプラクティスの中核です。しかしトークンとは何でしょう？

トークンとは、通常は認証および認可プロトコルにおいて利用される、ユーザー、デバイスまたはプロセスのようなエンティティについてのクレームまたは属性のセットを表現できるデジタルオブジェクトです。[^1] 多くの場合、トークンは改善および認可されていないアクセスを防ぎ、完全性および機密性を確保するために、暗号学的な署名および/または暗号化されています。一般的にトークンは、様々なアイデンティティとアクセス管理のシステムにおいて利用され、ネットワーク化されたシステム間でアイデンティティを証明し、アクセス権を委譲し、権限を検証するためのセキュリティ機構を有効にします。

トークンは、セッション情報をメンテナンスするためにサーバーを必要とするかしないかによって区別されるかもしれません。あるトークンは、JSON Web Token（JWT）のように、ステートレスで、トークン内にエンコードされた情報（例えば、クレーム、ユーザーロールおよび有効期限）を運ぶだけです。これは、サーバーへの要求を減らすことでよりスケーラブルなアーキテクチャを実現します。また、あるトークンはステートフルで、このときトークンのコンテンツはクライアントにとって常に不透明であり、本質的には情報を「含みません」。（ステートレストークンも暗号化されている場合、同様に不透明です。）代わりに、発行したサーバーによってトークンの意味が追跡されており、トークンに関連付けられたステート（例、セッションデータ、ユーザー権限）を管理します。

トークンはどのように利用されるのかによっても説明できます。トークンは、トークンを所持する誰もが利用できるベアラートークンと、特定のクライアントに暗号的に紐づけられたベアラートークンであるクライアントバウンドトークン（時折、sender-constrainedトークンと呼称されます（例えば、Demonstrating Proof of Possession（DPoP）[^2]））に分類できます。OAuth 2.0フレームワークにおいて、クライアントバウンドトークンとベアラートークンの両方が認可に利用できます。また、トークンは、悪用のリスクを最小化するために短命（数分か数時間以内に有効期限を迎えます）の可能性もあれば、トークンリプライ攻撃に対してより強い保護を提供するために長命（長時間有効）であることもあります。しかし、OAuth 2.0フレームワークはこれらの選択肢を可能にする一方で、実装の決定がセキュリティに対する重大な影響を与えます - そのため、様々なワーキンググループが高度なセキュリティを必要とするユースケースに適したOAuth 2.0のプロファイルを開発するために発足しました。[^3]

トークンを発行するときの最も効果的な戦略の1つは、トークンの権限を狭い範囲に設定することです。スコープの狭いトークンは、幅広く制限のないアクセス権ではなく、特定のリソースだけ、またはアクションの制限されたセットへのアクセス権の付与をおこなうように設計されています。スコープの狭いトークンは特定のリソースやアクションへのアクセスに制限しており、トークンが侵害された場合に認可していないアクセスのリスクを低減できます。この制限は、たった一つのトークンで複数のサービスやアクションにアクセス権を提供できる幅広いスコープと対称的です。有効期限が短く、スコープの狭いトークンを利用することは、たとえトークンが侵害されたとしても、損害をシステムの小さい範囲に制限し、きわめて重要なリソースへの認可されていないアクセスのリスクを低減します。

しばしば、「クレデンシャル」という単語は「トークン」と言い換えられるような形で使われます；残念ながら、これは技術的には不正確です。トークンとクレデンシャルは多くの場合に関係がある一方で、それぞれ異なる役割を果たします。クレデンシャルはユーザーまたはシステムのアイデンティティの認証に利用される一方で、OAuth 2.0におけるトークンは認証後に発行され、特定のアクションを認可します。トークンベースのプロトコルが幅広く採用される前、Webサイトが単にクレデンシャルを要求（および保管）していたことを思い出すかもしれません。これは、「スクリーンスクレイピング」と呼ばれます。トークンのスコープ、コンテキストそして期間を制限することによって、認可サーバーはインターネット上の悪意のあるアクターから、ユーザー（と彼らのクレデンシャル）を保護します。

トークンはユーザーを認可するために便利で柔軟な方法を提供する一方で、適切に管理されていない場合に重大なセキュリティリスクをもたらすこともあります。理想的には、組織はリアルタイムなリスクに基づいたトークン失効を実装しようとします。[^4] しかし、提供したトークンの正しい生存期間を考慮することは、セキュリティ管理ツールを結合していない組織にとって不可欠です。

これが、この記事とOAuth 2.0フレームワークの複雑なトークンファミリーにつながります。OAuth 2.0はInternet Engineering Task Force（IETF）で定義された仕様のセットであり、APIのようなリソースにアクセスすることを可能にするため、スコープ付きのトークンのセットをクライアントに要求できるようにします。異なる種類のトークンと使い方を理解することは、開発者およびアイデンティティとアクセス管理の専門家がそれぞれの環境において考慮する必要がある実装の注意点を把握することに役立ちます。

@row
![A high level swimlane diagram of the OAuth process, used with permission.](/assets/images/idpro_bok/108-image1.png)

Figure : "The OAuth process, at a high level" – reproduced with permission from OAuth 2 in Action[^5] by Justin Richer and Antonio Sanso.

@row
### Terminology

*   Token: A digital object that can represent a set of claims or attributes about an entity, such as a user, device, or process, typically used in authorization protocols
    
*   Credential: Credentials are used to authenticate the identity of a user or system, while OAuth 2.0 tokens are issued after authentication to authorize specific actions.
    
*   Bearer Token: According to RFC 6750, “The OAuth 2.0 Authorization Framework: Bearer Token Usage,” a bearer token is a security token with the property that any party in possession of the token (a "bearer") can use the token in any way that any other party in possession of it can.[^6]
    
*   Client-bound Token: Tokens that are tied to a specific client or device, ensuring that only the client to which the token was issued can use it. This is not a formally defined term in the specifications, but you can learn more in RFC 8705, “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens”,[^7] and RFC 9449, “OAuth 2.0 Demonstrating Proof of Possession (DPoP)”.
    
*   Refresh Token: According to RFC 6749, “The OAuth 2.0 Authorization Framework,” a refresh token is a credential used to obtain access tokens without requiring the resource owner to reauthenticate.[^8]
    
*   Sender-constrained Token: Tokens that require the sender to prove that they are the authorized holder of the token when making a request.
    
*   Token replay attack: A cybersecurity attack that occurs when an attacker intercepts valid tokens—such as tokens or session IDs—during transmission and reuses them to impersonate the legitimate user or system.
    

@column
## 用語解説

*   トークン：通常は認可プロトコルにおいて利用される、ユーザー、デバイスまたはプロセスのようなエンティティについてのクレームまたは属性のセットを表現できるデジタルオブジェクト
    
*   クレデンシャル：クレデンシャルはユーザーまたはシステムのアイデンティティを認証するために利用されますが、OAuth 2.0のトークンは特定のアクションを認可ｓるうための認証後に発行されます。
    
*   ベアラートークン：RFC 6750 「The OAuth 2.0 Authorization Framework: Bearer Token Usage」によれば、ベアラートークンはセキュリティトークンであり、トークンを所有している全ての当事者（「ベアラー」）がトークンを所有している他の当事者と同じようにトークンを利用できるという性質を有しています。 [^6]
    
*   クライアントバウンドトークン：特定のクライアントかデバイスに紐づけられ、トークンを発行されたクライアントだけが利用できるトークン。これは仕様に正式に定義されている用語ではありませんが、RFC 8705「OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens」[^7]およびRFC 9449￥OAuth 2.0 Demonstrating Proof of Possession (DPoP)」でさらに学ぶことができます。
    
*   リフレッシュトークン：RFC 6749「The OAuth 2.0 Authorization Framework」によれば、リフレッシュトークンはリソースオーナーに再認証を要求することなく、アクセストークンを取得するために領されるクレデンシャルです。[^8]
    
*   sender-constrainedトークン：リクエストを作成するとき、送信者がトークンの認可された所持者であることを証明する必要があるトークン。
    
*   トークンリプレイ攻撃：攻撃者がトークンやセッションアイデンティティのような正当なトークンを通信の途中で傍受し、正当なユーザーやシステムになりすまして再利用するときに発生しするサイバーセキュリティ攻撃。
    

@row
## Defining “Short” versus “Long”

In OAuth 2.0, two types of tokens are issued during the authorization process. The access token tends to be short-lived and is scoped for the resources where it will be used. The refresh token tends to be longer-lived and is only used with the authorization server to obtain new short-lived access tokens. Access tokens are typically created during the authorization process after the user successfully authenticates. In contrast, refresh tokens are issued alongside access tokens and allow new short-lived access tokens to be generated without requiring the user to reauthenticate. Access tokens are meant for authorizing specific API calls, while refresh tokens are used only with the authorization server to obtain new access tokens. This mechanism ensures that users don’t need to log in again for subsequent access, but periodic reauthentication might still be necessary, depending on the security requirements.

How you define “short” versus “long” token lifespans will vary depending on the sensitivity of your use case. For example, NIST SP 800-63B specifies that for Authenticator Assurance Level (AAL) 1, “reauthentication of the subscriber SHOULD be repeated at least once per 30 days during an extended usage session, regardless of user activity.” This guideline suggests that even with mechanisms like refresh tokens, reauthentication should occur periodically to maintain the security of the session.”[^9]

@column
## 「短命」と「長命」の定義

OAuth 2.0において、認可プロセス中に2酒類のトークンが発行されます。アクセストークンは短命な傾向にあり、利用されるであろうリソースに限定されます。リフレッシュトークンは長命な傾向にあり、新しい短命なアクセストークンを取得するために認可サーバーに対してだけ使えます。通常、アクセストークンはユーザーが認証に成功した後、認可プロセスで作成されます。対照的に、リフレッシュトークンはアクセストークンと一緒に発行され、新しい短命なアクセストークンをユーザーの再認証なしに生成することを可能にします。アクセストークンは特定のAPI呼び出しを認可するという意味があり、リフレッシュトークンは新しいアクセストークンを獲得するために認可サーバーに対してだけ利用されます。このメカニズムは、ユーザーがアクセスのために再度ログインする必要がないことを保証しますが、セキュリティ要件に依りますが定期的な再認証は依然として必要です。

「短命」と「長命」トークンの生存期間の定義は、ユースケースの機密性に依存して変化します。例えば、NIST SP 800-63Bは当人認証保証レベル（AAL）1について、「サブスクライバーの再認証は、ユーザーアクティビティに関係なく、長期間使用中のセッションを少なくとも30日に1回は繰り返すべきである（SHOULD）」と規定しています。このガイドラインは、リフレッシュトークンのようなメカニズムを利用しても、セッションの安全性を維持するために再認証は定期的におこなうべきであることを示唆しています。 [^9]

@row
## The Role of Short-Lived Tokens in Security

Short-lived tokens are a fundamental tool in enhancing the security of modern authentication and authorization systems. These tokens are designed to expire after a brief period—usually minutes or hours—thereby minimizing the window of opportunity for attackers to exploit them if they are intercepted or compromised. By limiting their lifespan, short-lived tokens reduce the risk of token misuse and improve the overall security posture of a system. Short-lived tokens significantly mitigate risks associated with token replay attacks and unauthorized use, but they must be part of a broader security strategy, including token binding and revocation mechanisms.

Although this article focuses on short-lived tokens as a security best practice, emerging standards like Continuous Access Evaluation Profile (CAEP) aim to extend token lifetimes in controlled ways, reflecting a shift toward risk-based token management. [^10]

The use of short-lived tokens is recommended in numerous security standards and guidelines. For instance, NIST SP 800-63C emphasizes the importance of using short-lived, narrowly-scoped tokens for federated identity systems to minimize risks.[^11] Similarly, BCP 225 outlines best practices for JSON Web Tokens (JWTs), including the recommendation to limit the lifetime of tokens to reduce their exposure to attacks.

The standards also encourage the combination of short-lived tokens with other security mechanisms, such as client-bound tokens or token binding, which ensures that tokens can only be used by specific clients, further enhancing their security, or sender-constrained tokens, which require the sender to prove that they are the authorized holder of the token when making a request.

@column
## セキュリティにおける短命のトークンの役割

短命トークンは、現代の認証および認可システムの安全性を強化するための基本的なツールです。これらのトークンは一般的に数分から数時間という短時間で有効期限を迎えるように設計されており、トークンが傍受されたり侵害されたりした場合に攻撃者がトークンを悪用する機会を最小化しています。トークンの生存期間を制限することによって、短命なトークンはその悪用のリスクを低減し、システムのセキュリティ体制全体を向上します。短命なトークンはトークンリプレイ攻撃および認可されていない利用に関連したリスクを大きく軽減しますが、トークンバインディングおよび失効メカニズムを含むより広いセキュリティ戦略の一部でなければなりません。

この記事ではセキュリティベストプラクティスとして短命なトークンに焦点を当てますが、Continuous Access Evaluation Profile（CAEP）のような新しい標準仕様は、リスクベースのトークン管理への移行を反映した管理された方法でトークンの生存時間を延長することを目的としています。 [^10]

短命なトークンの利用は、数多くのセキュリティ標準およびガイドラインで推奨されています。例えば、NIST SP 800-63Cはフェデレーションアイデンティティシステムにおいてリスクを最小限にするため、短命でスコープの狭いと０君の利用の重要性を強調しています。[^11] 同様にBCP 225はJSON Web Token（JWT）のベストプラクティスの概要を記述しており、攻撃に晒されることを減らすためにトークンの生存期間を制限することを推奨しています。

また、標準仕様では短命なトークンと、トークンが特定のクライアントだけに利用されることを保証するクライアントバウンドトークンやトークンバインディング、さらにセキュリティを強化するためにリクエストを作成する際に送信者がトークンの認可された所持者であることを証明する必要がある送信者制約付きトークンなどその他セキュリティメカニズムを組み合わせることを推奨しています。

@row
### Reduced Attack Surface

One of the big benefits of short-lived tokens is the reduction of the attack window (i.e., the length of time that an attacker could exploit endpoints). In traditional token-based systems, tokens with long expiration times are particularly vulnerable to token replay attacks, where an attacker captures a token and reuses it to impersonate the legitimate user. Short-lived tokens mitigate this threat by limiting the time in which a token can be used. Even if an attacker manages to steal a token, its utility is severely restricted because it will soon expire, rendering it invalid.

For example, in the context of OAuth 2.0, access tokens should be issued with a short lifespan, after which the client must request a new token using a refresh token.[^12] This approach ensures that even if an attacker intercepts an access token, they cannot use it for long.

@column
### 攻撃領域範囲の縮小

短命なトークンの大きな利益の一つは、攻撃ウィンドウ（つまり、攻撃者がエンドポイントを悪用する期間）の低減です。伝統的なトークンベースシステムでは、有効期間の長いトークンは特にトークンリプレイ攻撃、攻撃者がトークンを取得し、再利用して正当なユーザーを侵害しようとする攻撃、の脆弱性があります。短命なトークンは、トークンが利用可能な時間を制限することで、この脅威を軽減します。攻撃者がトークンを盗むことに成功したとしてトーkンはすぐに有効期限が切れて無効となるため、その利用は非常に制限されます。

例えば、OAuht 2.0のコンテキストでは、アクセストークンは短い生存期間を持って発行されるべきであり、クライアントはリフレッシュトークンを利用して新しいトークンを要求しなければなりません。[^12] このアプローチは、攻撃者がアクセストークンを傍受したとしても長期間利用できないことを保証します。

@row
#### Enhanced Security Through Short-Lived Token Rotation

Short-lived tokens play a crucial role in reducing the impact of token compromise by enforcing frequent token rotation. With short expiration times—typically ranging from minutes to hours—these tokens minimize the window of opportunity for attackers. If a short-lived access token is intercepted, its limited lifespan means that it will soon become invalid, rendering it useless to the attacker. This frequent renewal of access tokens forces attackers to be more persistent and repeatedly intercept new tokens, which increases the likelihood of detecting suspicious activity.

In contrast, long-lived tokens remain valid for extended periods, such as days or even months. If compromised, they provide attackers with prolonged access to protected resources, increasing the risk of unauthorized activity. By reducing token lifespan, organizations can significantly limit the potential damage of compromised tokens, ensuring that access is tied to a shorter, more controlled time frame.

However, it is important to consider the role of refresh tokens, which are used to obtain new access tokens without requiring the user to reauthenticate. While refresh tokens often have longer lifespans, they must be protected with robust security measures. If an attacker gains access to a refresh token, they can continue to generate new short-lived access tokens, potentially maintaining unauthorized access over time. There must be additional protections to prevent or mitigate refresh token replay, such as refresh token rotation upon every use, client binding, real-time risk-based token revocation, and secure storage of refresh tokens. Together, these protections prevent misuse and ensure that short-lived token strategies remain effective.

@column
#### 短命なトークンのローテーションによるセキュリティ強化

短命なトークンは、頻繁なトークンローテーションを強制することで、トークン侵害の影響を低減するという重要な役割を果たします。短い有効期限、通常数分からス時間の間、を持つトークンは攻撃者の機会の範囲を最小化します。短命なアクセストークンが傍受された場合、その制限された生存期間はトークンがすぐに無効になることを意味し、攻撃者にとって有用ではありません。このアクセストークンの頻繁な更新によって、攻撃者は新しいトークンをより執拗に繰り返し傍受することを余儀なくされ、疑わしいアクティビティの検知の可能性が高くなります。

対照的に、長命なトークンは数日や数カ月の期間で有効です。侵害された場合、攻撃者は保護されたリソースへ長期間アクセスできることになり、認可されていないアクティビティのリスクが増加します。トークンの生存期間を短くすることで、組織は侵害されたトークンの潜在的な被害を非常に大きく制限することができ、アクセスがより短く、より制御された時間枠に結び付けることを保証します。

しかし、ユーザーに再認証を要求することなく、アクセストークンを取得するために利用されるリフレッシュトークンの役割について考慮することが重要です。リフレッシュトークンはしばしば長い生存期間を有していますが、強固なセキュリティ対策によって保護されなければなりません。攻撃者がリフレッシュトークンへのアクセス権を取得した場合、新しい短命のアクセストークンを生成し続けることができ、認可されていないアクセスを長期間維持することができる可能性があります。利用するたびにリフレッシュトークンをローテーションする、クライアントバインディングする、リアルタイムなリスクベーストークン失効およびリフレッシュトークンの安全な保管をのような、リフレッシュトークンリプレイ攻撃を阻止または軽減するための追加の防御がなければなりません。これらの保護を同時におこなうことで悪用を防止し、短命なトークン戦略の有効性を維持することを保証します。

@row
#### Security of Refresh Tokens

While access tokens are short-lived and may be in API requests or during authentication flows, refresh tokens are stored securely on the client. This safe storage is critical because refresh tokens are valuable; if they are compromised, the attacker can maintain access far beyond the expiration of the original access token.

Systems that use refresh tokens should implement several security measures to mitigate the risk:

1.  Refresh Token Rotation: Upon each use, the refresh token should be reissued to limit the threat of any one token being captured.
    
2.  Client Binding: Refresh tokens should be cryptographically bound to a specific client or device. This secure binding means that even if an attacker steals both the access token and the refresh token, they cannot use the refresh token from a different device or application. The refresh token will only work on the client it was originally issued to.
    
3.  Reauthentication: Some systems require users to periodically reauthenticate before issuing new refresh tokens. This action adds a layer of security by forcing legitimate users to prove their identity again, limiting the window during which a stolen refresh token can be used.
    
4.  Token Revocation: If suspicious activity is detected—such as refresh tokens being used from an unfamiliar device or location—the system can revoke both the refresh and access tokens. This revocation forces a reauthentication and cuts off any further unauthorized access.
    

@column
#### リフレッシュトークンのセキュリティ

アクセストークンが短命で、APIリクエスト内もしくは認証フロー内に存在する可能性がある一方で、リフレッシュトークンはクライアントに安全に保管されています。リフレッシュトークンは価値が高いために、この安全な倉庫は重要です；リフレッシュトークンが侵害されると、攻撃者はオリジナルのアクセストークンの有効期間を大きく超える期間、アクセスを維持できます。

リフレッシュトークンを利用するシステムは、このリスクを軽減するためにいくつかのセキュリティ対策を実装すべきです：

1.  リフレッシュトークンローテーション：利用するたびに、リフレッシュトークンはキャプチャーされたときの脅威を制限するために再発行されるべきです。
    
2.  クライアントバインディング：リフレッシュトークンは、特定のクライアントまたはデバイスに暗号的にバインドされるべきです。このセキュアなバインドは、攻撃者はアクセストークンとリフレッシュトークンの両方を窃取したときでさえ、別のデバイスやアプリケーションからリフレッシュトークンを利用することはできないことを意味します。リフレッシュトークンは本来発行されたクライアント上だけで動作します。
    
3.  再認証：一部のシステムは、新しいリフレッシュトークンを発行するために、ユーザーに定期的な再認証を要求します。この動作は、正当なユーザーに自身のアイデンティティを再度証明させることを強制することで、セキュリティレイヤーを追加し、盗難されたリフレッシュトークンが利用できる期間を限定します。
    
4.  トークン失効：デバイスや場所がいつもと異なるリフレッシュトークンの利用のような疑わしいアクティビティを検知した場合、システムはリフレッシュトークンとアクセストークンの両方を失効させることができます。この失効は再認証を強制し、更なる認可されていないアクセスを排除します。
    

@row
#### Summarizing the Security Implications

*   If only the access token is compromised and not client-bound, the impact is limited to the token’s short lifespan. The attacker can use the token for a limited time, after which it becomes useless.
    
*   If both the access token and the refresh token are compromised, the attacker can maintain long-term access by continuously refreshing the access token. In this case, additional security measures such as client binding, reauthentication, or token revocation become crucial for mitigating the damage.
    

@column
#### セキュリティ実装のまとめ

*   アクセストークンだけが侵害され、クライアントバウンドではない場合、その影響はトークンの短い生存期間に限定されます。攻撃者は限られた時間だけトークンを利用することができ、その後利用できなくなります。
    
*   アクセストークンおよびリフレッシュトークンの両方が侵害された場合、攻撃者はアクセストークンを継続的に更新することで長期間のアクセスを維持できます。この場合、クライアントバインディング、再認証やトークン失効のような追加のセキュリティ対策がダメージの軽減に重要になります。
    

@row
### Support for Scalable and Stateless Architectures

Short-lived tokens are particularly well-suited for stateless architectures, such as RESTful APIs, because they reduce the need to maintain the server’s session state. When a token is short-lived, the server may not need to track session data over an extended period, which simplifies the architecture and reduces the potential attack vectors related to session management.

In microservices architectures, where services communicate frequently over APIs, short-lived tokens play a critical role in authenticating and authorizing requests between services. Their limited lifespan ensures that, even if an attacker manages to access a token from one microservice, the time available for them to use it is minimal. The scope of the token is also critical to its security impact. A token representing only the client’s identity can expose a broader range of resources. However, if the token carries user-specific information with a narrowly defined scope, the potential attack surface is significantly reduced.

Another option for microservices, currently under discussion within the IETF, is the use of transaction tokens.[^13] These tokens allow workloads in a trusted domain to maintain the user identity and authorization details of an external request, such as an API call, across all workloads involved in processing that request.

@column
### スケーラブルでステートレスなアーキテクチャのサポート

短命なトークンは、サーバーのセッション状態を関する必要が少ないことから、RESTful APIのようなステートレスなアーキテクチャに特に適しています。トークンが短命な場合、サーバーは長期間セッションデータを維持する必要がないかもしれず、アーキテクチャをシンプルにし、セッション管理に関連する潜在的な攻撃ベクトルを低減します。

マイクロサービスアーキテクチャにおいて、APIを介してサービスは頻繁に通信し、短命なトークンはサービス間の認証および認可リクエストにおいて非常に重要な役割を果たします。トークンの制限された生存時間は、攻撃者が一つのマイクロサービスからアクセストークンを取得した場合でも、トークンが使用可能な時間は最小となることを保証します。トークンのスコープもセキュリティへの影響を与える重要なものです。クライアントのアイデンティティを表現するだけのトークンは、幅広くリソースを公開します。しかし、トークンは定義された狭い範囲のスコープによってユーザー固有の情報を有している場合、潜在的な攻撃対象領域は大きく減少します。

現在IETFで議論されている、マイクロサービスのための他の選択肢は、トランザクショントークンの利用です。[^13] このトークンは、信頼されたドメインでのワークロードにおいて、ユーザーのアイデンティティとAPI呼び出しのような外部リクエストの認可の詳細情報を、そのリクエスト処理に関与するワークロードすべてにわたって保持できるようにします。

@row
## Security Risks of Long-Lived Tokens

While short-lived tokens are not inherently more secure in stateless architectures, their design aligns with the scalability and efficiency needs of modern systems, reducing the attack surface by limiting token lifespans. The persistence and vulnerability of tokens can open doors for various attack vectors, particularly token compromise and replay. Let’s look at a few critical security drawbacks associated with tokens whose lifetimes are long enough to be more easily used by an attacker.

@column
## 長命なトークンのセキュリティリスク

短命なトークンは、ステートレスなアーキテクチャにおいて本質的にはよりセキュアではない一方で、その設計はモダンなシステムのスケーラビリティと効率性のニーズに沿っており、トークンの生存期間を制限することで攻撃対象領域を減らすことができます。トークンの永続性と脆弱性は、様々な攻撃ベクトル、特にトークン侵害とリプレイ、を許すことになります。いくつかの、生存期間が攻撃者が簡単に利用できるほど充分に長いトークンに関連した致命的なセキュリティ上の欠点を確認しましょう。

@row
### Long-Lived Tokens

Common types of long-lived tokens, such as API keys and session tokens used in mobile apps, often remain valid for extended periods—sometimes days, weeks, or even indefinitely. API keys are often used for backend services that need to authenticate to external services, while session tokens maintain user sessions across mobile app interactions. More to the point, API keys are used to authenticate programmatic requests, while session tokens help maintain user sessions across multiple interactions. These tokens reduce the burden on users or applications to re-authenticate or refresh their credentials frequently, offering convenience and stability.

However, this also creates a significant security risk. If these long-lived tokens are compromised, attackers can use them to gain persistent unauthorized access to systems or resources without being detected for an extended period.

In environments where tokens are not frequently reissued or refreshed, the chances of interception or theft increase. This possibility makes long-lived tokens particularly attractive targets for attackers, as they allow for sustained access once compromised. Without mechanisms like token revocation or detection of replayed tokens, such breaches can go unnoticed, giving attackers ample time to explore and exploit vulnerabilities within the system.

@column
### 長命なトークン

一般的な長命なトークン、APIキーやモバイルアプリで利用されるセッショントークンなど、はしばしば長期間、場合によっては数日、数週間もしくは無期限の間、有効です。APIキーは多くの場合、外部サービスへの認証が必要なバックエンドサービスで利用され、セッショントークンはモバイルアプリのインタラクション全体でユーザーセッションを維持するために利用されます。さらに言えば、APIキーはプログラマティックなリクエストの認証に利用され、セッショントークンは複数のインタラクション全体でのユーザーセッションの維持を助けます。これらのトークンは、ユーザーやアプリケーションが頻繁に再認証やクレデンシャル更新をおこなう負担を減らし、利便性と安定性を提供します。

しかし、これは重大なセキュリティリスクを生み出すことにもなります。これらの長命なトークンが侵害された場合、攻撃者はトークンを使うことで、長期間検知されることなく、システムやリソースに対して永続的な認可されていないアクセス権を取得することができます。

トークンが頻繁に再発行されたり、更新されたりしない環境では、傍受や窃取の機会が増加します。この可能性は、一度侵害されると持続的なアクセスが可能になるため、特に長命なトークンを攻撃者にとって魅力的なものにします。トークン失効やリプレイされたトークンの検出のような仕組みがなければ、このような侵害は気付かれず、攻撃者にシステム内の脆弱性を探索し、悪用する充分な時間を与えてしまいます。

@row
### Token Replay Vulnerabilities

One of the most concerning security drawbacks of some tokens is their susceptibility to token replay attacks. In a token replay attack, an attacker intercepts a token (through manipulator-in-the-middle attacks, session hijacking, or other methods) and reuses it to impersonate a legitimate user.[^14] Tokens that are not tied to a specific client or have long expiration times are easy targets for replay attacks.

For example, in a system using long-lived tokens, an attacker who successfully intercepts an access token could reuse it repeatedly until it expires, giving them ongoing access to sensitive resources. Without mechanisms like token binding or short expiration times, little can prevent these replay attacks from succeeding. According to NIST SP 800-63C, tokens not bound to a specific client or have inadequate expiration times are a critical weakness in federated identity systems.

@column
### トークンリプレイ脆弱性

一部のトークンで最も懸念されるセキュリティ上の欠点の１つは、トークンリプレイ攻撃に対する感受性です。トークンリプレイ攻撃では、攻撃者はトークンを傍受（中間者攻撃、セッションハイジャックやその他の手法によって）し、正当なユーザーになりすましてトークンを利用します。[^14] 特定のクライアントに紐づけられていない、または有効期間が長いトークンはリプレイ攻撃のターゲットになりやすいです。

例えば、長命なトークンを利用するシステムにおいて、アクセストークンの傍受に成功した攻撃者は、有効期限を迎えるまで繰り返し再利用することができ、機密リソースへの継続的なアクセスが可能になります。トークンバインディングや短い有効期間のような仕組みがなければ、このようなリプレイ攻撃の成立を防ぐことはほとんどできまん。NIST SP 800-63Cによれば、トークンを特定のクライアントに紐づけない、または不適切な有効期間にすることはフェデレーションアイデンティティシステムにおいて致命的な弱点になります。

@row
### Challenges with Revocation

Revocation is another significant weakness of traditional long-lived tokens. Once issued, long-lived tokens, session cookies, or API keys are often difficult to revoke in real time. If a token is compromised, administrators must manually revoke it or wait for it to expire, creating a time window in which an attacker can continue to exploit the token.

Many systems that rely on older OAuth token specifications do not have effective mechanisms for real-time token revocation or monitoring of credential usage, which can lead to prolonged security incidents. While traditional long-lived tokens pose revocation challenges, frameworks like CAEP are redefining how tokens can be managed dynamically, enabling longer lifespans under strict monitoring and policy enforcement. Organizations that are taking advantage of CAEP may extend token lifetimes, requiring a refresh only after an event that triggers policy enforcement.

@column
### 失効に関する課題

失効は、伝統的な長命なトークンの別の重大な弱点です。長命なトークン、セッションCookieやAPIキーはいったん発行されると、多くの場合でリアルタイムに失効することは難しいです。トークンが侵害されると、管理者は手動でトークンを失効させるか、有効期限となるまで待つかしなければならず、これは攻撃者がトークンを悪用し続けるための時間を作ることになります。

古いOAuthトークンの仕様に依存している多くのシステムでは、リアルタイムなトークンん失効やクレデンシャル利用の監視のための効果的な仕組みを持っておらず、セキュリティインシデントが長期化する可能性があります。伝統的な長命トークンは失効に関する課題を抱えていましたが、CAEPのようなフレームワークはトークンを動的に管理する方法を再定義し、厳格な監視とポリシー実行の下でより長い生存期間を可能にしています。CAEPを活用している組織では、トークンの生存期間を延長し、ポリシー実行のトリガーとなるイベントの後にだけ更新を要求するようになるかもしれません。

@row
### Increased Attack Surface

Long-lived tokens can increase the attack window for an organization, especially when they are not tightly scoped or frequently refreshed. Because these tokens remain valid for extended periods and may be used across multiple devices or services, a compromised long-lived token can give attackers more time to explore and exploit vulnerabilities within a network. This is particularly true when the token allows access to multiple services or resources without requiring frequent revalidation.

However, refresh tokens are typically not issued in most server-to-server interactions, and short-lived access tokens are preferred to minimize the time a token remains valid. This restriction limits the window of opportunity for attackers to misuse a compromised token. In contrast, long-lived tokens, like those used in user sessions or in environments where periodic reauthentication is not enforced, could be reused by an attacker until they are revoked or expire naturally.

For instance, if an attacker gains access to a compromised long-lived token, they can use it to maintain access to specific services or potentially move laterally within a network to escalate privileges. While the token itself does not directly extend its own lifespan (unlike a refresh token), the extended time during which it remains valid provides the attacker with more opportunities to exploit the network before detection.

In microservices environments, where APIs are constantly communicating, short-lived tokens are crucial for securing service-to-service interactions. These tokens ensure that access is limited in time and scope, making it harder for attackers to leverage a compromised token to pivot to other services. However, each location where tokens are stored or transmitted in such environments represents a potential attack vector, emphasizing the need for secure storage and transmission practices.

@column
### 攻撃領域の増大

長命なトークンは組織にとって、特にトークンのスコープが狭くなかったり、更新が頻繁でなかったりする場合、攻撃対象を増やすことになります。これらのトークンは、長期間有効なままで、複数のデバイスまたはサービスで利用できる可能性があるため、侵害された長命なトークンは攻撃者にネットワーク内で脆弱性を探索して悪用するためのより多くの時間を提供することになります。特に、再検証を頻繁に実施する必要がなく、トークンが複数のサービスやリソースに対するアクセスを可能にする場合には注意が必要です。

しかし、通常リフレッシュトークンはサーバー間通信では発行されず、トークンが有効な時間を最小化した短命なトークンが好まれます。この制約は、攻撃者が侵害されたトークンを悪用する期間を制限します。対照的に、ユーザーセッションとして利用される場合や定期的な再認証が実行されない場合のような長命なトークンでは、攻撃者はトークンが失効させられたり、自然に有効期限を迎えたりするまで再利用するかもしれません。

例えば、攻撃者が侵害された長命なトークンへのアクセス権を取得した場合、攻撃者は特定のサービスへのアクセスを維持するため、または潜在的にネットワーク内で水平方向に移動して特権に昇格するためにトークンを使うことができます。トークン自体は直接自身の生存期間を延長することはありません（リフレッシュトークンとは異なります）が、トークンが有効な間に延長された時間は検出される前にネットワークを悪用する機会を攻撃者に提供します。

マイクロサービス環境では、APIが常に通信している場合、短命なトークンは安全なサービス間通信にとって致命的です。これらトークンは、アクセスが時間とスコープにおいて制限されていることを保証することで、攻撃者が侵害されたトークンを他のサービスに向けて利用することを難しくします。ただし、そのような環境でトークンが保管または送信される場所はそれぞれ潜在的な攻撃ベクトルとなるため、安全な保管と送信のプラクティスの必要性が強調されます。

@row
### Difficulty in Enforcing Least Privilege

While long-lived tokens can be scoped to enforce least privilege, their existence represents standing privilege;[^15] they still pose a higher risk if not carefully managed, as compromised tokens can grant attackers prolonged access to specific resources.[^16] If the scope is too broad at the time of issuance, long-lived tokens might unintentionally provide access to resources beyond what is necessary.

In contrast, short-lived, narrowly scoped tokens allow administrators to enforce fine-grained access control, ensuring that tokens are only valid for specific operations or resources for a limited time. By applying narrow scopes, organizations can reduce the potential damage from a compromised token, as an attacker would only gain access to a limited subset of resources. This approach restricts unauthorized access to a small part of the infrastructure, making it an essential control for protecting sensitive systems.

@column
### 最小特権を実行する難しさ

長命なトークンは最小特権を強制するようにスコープを設定できますが、トークンの存在は永続的な特権を表します；[^15] トークンが侵害されると、攻撃者に特定のリソースへの長期間のアクセスを許可する可能性があるため、慎重に管理しないと依然として高いリスクが生じます。[^16] 発行時のスコープが広すぎる場合、長命なトークンによって必要以上のリソースへのアクセス権が意図せず提供される可能性があります。

対照的に、短命でスコープの狭いトークンは管理者がきめ細かなアクセス制御を強制できるようにすることで、トークンは限られた時間に特定の操作やリソースにだけ有効であることｗ保証します。狭いスコープを適用することで、攻撃者がリソースの制限されたサブセットに対してのアクセス権だけを取得するため、組織は侵害されたトークンから潜在的な被害を減らすことができます。このアプローチでは、認可されていないアクセスを少数のインフラストラクチャに制限することで、機密システムを保護するための必要不可欠な制御をおこなうことになります。

@row
## When Long-Lived Tokens May Make Sense

There are scenarios where long-lived tokens do offer certain benefits, particularly in specific use cases where organizations have good reason to prioritize convenience and reduced token management overhead. For example:

@column
## 長命なトークンが意味を持つかもしれない場合

長命なトークンが特定の利益を提供するシナリオ、特に組織が利便性とトークン管理オーバーヘッドの削減を優先する正当な理由がある特定のユースケース、が存在します。例えば：

@row
### Reduced Overhead in Token Renewal

Long-lived tokens minimize the need for frequent token refreshes, reducing the number of calls to the authentication server. This limitation is particularly useful in applications where users or services need continuous access over extended periods without interruptions.

*   **Use case**: In systems where uptime and uninterrupted access are critical (such as in background services, batch processing, or long-running data analytics jobs), long-lived tokens can prevent delays or failures caused by expired tokens.
    
*   _Note: In cases where the application involves [workload identities](https://learn.microsoft.com/en-us/entra/workload-id/workload-identities-overview), then protocols like [SPIFFE](https://spiffe.io/docs/latest/spiffe-about/overview/) enable dynamic, instance-based tokens._[^17] _Long-lived tokens are not necessary._
    

@column
### トークン更新のオーバーヘッドを減らす

長命なトークンは頻繁にトークンを更新する必要性を最小化し、認証サーバーへの呼び出し回数を減らします。この制限は、ユーザーやサービスが長期間中断されることなく継続的にアクセスする必要があるアプリケーションで特に有用です。

*   **ユースケース**：稼働時間と中断のないアクセスが重要なシステム（バックグラウンドサービス、バッチ処理や長時間実行のデータ分析ジョブなど）では、長命なトークンにより期限切れのトークンによって引き起こされる遅延や障害を防ぐことができます。
    
*   _注意：アプリケーションが[ワークロードID](https://learn.microsoft.com/en-us/entra/workload-id/workload-identities-overview)を含むようなケースでは、[SPIFFE](https://spiffe.io/docs/latest/spiffe-about/overview/)のようなプロトコルは、動的な、インスタンスベースのトークンを有効にします。_[^17] _長命なトークンは必須ではありません。_
    

@row
### Improved Performance in Stateless Systems

In stateless architectures, such as RESTful APIs, where the session state is not maintained on the server side, long-lived tokens eliminate the need to constantly issue new tokens. This option can enhance the system’s overall performance by reducing the load on authentication and authorization servers.

*   **Use case**: For applications requiring minimal server-side interaction for performance reasons, such as APIs serving high requests, long-lived tokens can reduce the number of database or server interactions needed to reissue tokens.
    

@column
### ステートレスなシステムで性能を改善する

RESTful APIのようなステートレスなアーキテクチャにおいて、サーバーサイドでセッション状態を維持しない場合、長命なトークンは常時新しいトークンを発行する必要性を排除します。この選択は、認証および認可サーバーへの負荷を減らし、システム全体の性能を向上させることができます。

*   **ユースケース**：大量のリクエストを処理するAPIのように、パフォーマンスを理由に最小のサーバーサイドの通信を要求するアプリケーションにとって、長命なトークンはトークンを再発行するために必要なデータベースまたはサーバーの通信の量を減らすことができます。
    

@row
### Service-to-Service Communication

In certain system-to-system communications where services need to interact with each other in a highly trusted environment (e.g., within the same enterprise or data center), long-lived tokens can reduce the need for frequent authentication and authorization exchanges. This makes service communication more efficient.

*   **Use case**: Within microservice architectures in secure internal networks, long-lived tokens can facilitate inter-service communication without requiring frequent re-authentication.
    
*   _Note: This use can also be solved by using short-lived tokens that leverage client\_secret\_jwt or private\_key\_jwt as defined in the OpenID Connect Core specification_.[^18]
    

@column
### サーバー間通信

信頼度の高い環境（例、同じ企業内やデータセンター内）においてサービス同士が互いに作用しあう必要がある特定のシステム間通信において、長命なトークンは頻繁に認証および認可のやり取りをする必要性を減らすことができます。これはサービスの通信をより効率化します。

*   **ユースケース**：安全な内部ネットワークにおけるマイクロサービスアーキテクチャでは、長命なトークンはサービス間通信が頻繁に再認証を必要とすることがなくなるように推進します。
    
*   _注意：この使い方は、OpenID Connect Core specificationに定義されているclient\_secret\_jwtやprivate\_key\_jwtを活用する短命なトークンの利用によっても解決することができます_ 。[^18]
    

@row
## Emerging Trends and Future Directions

The field of token management is evolving rapidly as organizations seek to balance security, scalability, and usability. While this article focuses on the current best practices for short-lived tokens, ongoing advancements in standards and frameworks are introducing new approaches to token lifetimes and security.

@column
## 新しいトレンドと将来の方向性

トークン管理の分野は、組織がセキュリティ、スケーラビリティおよびユーザビリティのバランスを探し求めることで急速に進化しています。この記事では短命なトークンについての現在のベストプラクティスについて焦点を当てましたが、標準仕様とフレームワークの継続的な進歩により、トークンの有効期間とセキュリティに対する新しいアプローチが導入されています。

@row
### Continuous Access Evaluation Profile (CAEP)

One of the most significant emerging developments is the Continuous Access Evaluation Profile (CAEP), a framework designed to dynamically assess and adjust access permissions in real time. CAEP enables access tokens to have longer lifespans without compromising security. This is achieved by combining periodic risk assessments with real-time revocation capabilities. For example, if a security event, such as a user’s location change or device compromise, is detected, access can be revoked immediately, even if the token has not yet expired. While still in draft form, CAEP is gaining traction among vendors as a promising solution for risk-based token management.

@column
### Continuous Access Evaluation Profile（CAEP）

最も新しい発明の１つはContinuous Access Evaluation Profile（CAEP）という、動的に評価をおこない、リアルタイムにアクセス権限を調整するように設計されたフレームワークです。CAEPは、アクセストークンがセキュリティの侵害を受けずにより長い生存期間を持つことを可能にします。定期的なリスク評価とリアルタイムに失効をおこなう機能を組み合わせることで実現されています。例えば、ユーザーの場所の変化やデバイス侵害のようなセキュリティイベントが検知されたとき、トークンが有効期限を迎えていなくともアクセスは即座に失効されます。現在はまだドラフト段階ですが、CAEPはリスクベースのトークン管理の有望なソリューションとしてベンダーの間で注目を集めています。

@row
### Risk-Based Token Lifetimes

Traditional token lifetimes often rely on static durations, but future implementations are likely to adopt adaptive token lifetimes based on real-time risk analysis. By evaluating factors such as user behavior, device trust levels, and contextual signals, organizations could dynamically adjust token expiration times. This approach seeks to reduce unnecessary reauthentication while maintaining a high level of security.

@column
### リスクベーストークン生存時間

従来のトークンの生存時間は多くの場合に静的な期間に依存していましたが、将来の実装はリアルタイムなリスク分析に基づいたアダプティブなトークン生存時間を採用するようになりそうです。ユーザーの振る舞い、デバイスの信頼レベルおよびコンテキストシグナルのような要素を評価することで、組織はトークンの有効期間を動的に調整します。このアプローチは、セキュリティを高いレベルでメンテナンスする一方で、再認証の必要性を減らすことを追求しています。

@row
### Proof of Possession and Sender-Constrained Tokens

The shift from bearer tokens to proof-of-possession (PoP) or sender-constrained tokens, mentioned earlier in the Introduction, represents another critical trend. These tokens require the client to demonstrate cryptographic proof that they are the legitimate holder of the token. Standards such as OAuth 2.0 DPoP (Demonstration of Proof-of-Possession) and Mutual TLS (mTLS) are advancing this concept, reducing the risk of token replay attacks and unauthorized use.

@column
### 所持証明および送信者制約付きのトークン

前述のイントロダクションで述べた、ベアラートークンから所持証明（Proof-of-Possession、PoP）または送信者制約付きトークンへの移行は、別の重大なトレンドを示しています。これらのトークンは、クライアントにトークンの正当な所持者であることを示す暗号的な証明を提示することを要求します。OAuth 2.0 DPoP（Demonstration of Proof-of-Possession）およびMutual TLS８mTLS）のような標準仕様ははこの概念を進めており、トークンリプレイ攻撃および認可されていない使用のリスクを低減します。

@row
### Enhanced Revocation Mechanisms

Real-time token revocation remains a challenge, especially in distributed systems. One draft under discussion is draft-parecki-oauth-global-token-revocation,

“Global Token Revocation”.[^19] At the time of publication of this article, the draft has not been accepted by an IETF working group, but it remains an interesting example of ongoing work in the revocation space.

@column
### 強化された失効メカニズム

リアルタイムなトークン失効は、特に分散システムにおいて課題のままです。議論中のドラフトの１つが、 draft-parecki-oauth-global-token-revocation、
Real-time token revocation remains a challenge, especially in distributed systems. One draft under discussion is draft-parecki-oauth-global-token-revocation,

「Global Token Revocation」です。[^19] この記事の公開時点では、IETFワーキンググループでは承認されていませんが、失効の領域では進捗中の興味深い事例であることは変わりありません。

@row
## Conclusion

While long-lived tokens can offer convenience, particularly in trusted environments, the risks they present—such as token replay, session hijacking, and unauthorized access—must be carefully managed. (Of course, if you are following zero-trust principles, there is no such thing as a trusted environment.) Short-lived, narrowly-scoped tokens, client-bound tokens, and strong cryptographic standards provide an effective framework for mitigating these risks. Several guides are available on best practices in different environments, including BCP 225, “JSON Web Token Best Current Practices”; review them and consider how they can apply to your environment.

Frameworks like OAuth 2.0 and emerging standards like WIMSE (Workload Identity in Multi-System Environments) are beginning to provide the necessary infrastructure for managing short-lived tokens, particularly in cloud-native and microservices architectures.[^20] WIMSE is an interesting standardization effort for applications and multi-cloud identities. And while short-lived tokens remain a cornerstone of secure token management today, the evolving landscape of token management frameworks, such as CAEP, suggests that risk tolerance for longer token lifetimes may shift as standards and implementations mature.

Your organization’s risk posture will guide your definition of “short” and “long.” Regardless of whether you consider seconds, minutes, or months “short,” you need to implement strict scoping, use token binding, and ensure robust revocation and monitoring processes. You are aiming for a balance between security, usability, and performance, ensuring that both user and service interactions are protected against emerging threats.

@column
## 結論

長命なトークンは特に信頼された環境では利便性を提供できますが、トークンリプレイ攻撃、セッションハイジャックおよび認可されていないアクセスなど、トークンがもたらすリスクは慎重に管理されなければなりません。（もちろん、ゼロトラストの原則に従うのであれば、信頼された環境など存在しません。）短命でスコープの狭いトークン、クライアントバウンドトークンおよび強力な暗号標準仕様は、これらのリスクを軽減するための効果的なフレームワークを提供します。BCP 225「JSON Web Token Best Current Practices」など、さまざまな環境におけるベストプラクティスに関するガイドが入手可能です；ガイドを確認し、どのように自身の環境に適用できるかを考慮しましょう。

OAuth 2.0のようなフレームワークや、WIMSE（Workload Identity in Multi-System Environments）のような新たな標準仕様は、特にクラウドネイティブやマイクロサービスアーキテクチャにおいて、短命なトークンを管理するために必要なインフラを提供し始めています。[^20] WIMSEは、アプリケーションとマルチクラウドアイデンティティのための興味深い標準化の取り組みです。また、短命なトークンは今日でも安全なトークン管理の要石であることは変わらない一方で、CAEPのようなトークン管理フレームワークが進化している状況では、標準仕様と実装が成熟するにつれて、トークンの寿命が長くなることに対するリスク許容度が変化する可能性を示唆しています。

組織のリスク態勢が、「短い」と「長い」の定義の指針となります。数秒、数分または数ヶ月のどれを「短い」と考えるかにかかわらず、厳格なスコープを実装し、トークンバインディングを利用し、強固な失効と監視プロセスを確保する必要があります。セキュリティ、ユーザビリティおよびパフォーマンスのバランスを取り、ユーザーとサービスの通信が新たな脅威から保護されることを目指します。

@row
## Author Bio

<!-- ![](image2.jpeg) -->Heather Flanagan, Principal at Spherical Cow Consulting, comes from a position that the Internet is led by people, powered by words, and inspired by technology. She has been involved in leadership roles with some of the most technical, volunteer-driven organizations on the Internet, including IDPro as Executive Director and Principal Editor; the OpenID Foundation as Lead Editor; the IETF,  IAB, and the IRTF as RFC Series Editor; ICANN as Technical Writer and Editor; and REFEDS as Coordinator, just to name a few. If there is work going on to develop new Internet standards, or discussions around the future of digital identity, she is interested in engaging in that work. You can learn more about her at <[https://www.linkedin.com/in/hlflanagan/](https://www.linkedin.com/in/hlflanagan/)\>

- - -

[^1]:  Y., Hardt, D., and M. Jones, "JSON Web Token Best Current Practices", BCP 225, RFC 8725, DOI 10.17487/RFC8725, February 2020, <[https://www.rfc-editor.org/info/rfc8725](https://www.rfc-editor.org/info/rfc8725)\>. _Note that some readers may find reference to RFC 8471, “The Token Binding Protocol” in their search for more information on token binding. That specification has been largely abandoned. See_ _[https://groups.google.com/a/chromium.org/g/blink-dev/c/OkdLUyYmY1E/m/w2ESAeshBgAJ](https://groups.google.com/a/chromium.org/g/blink-dev/c/OkdLUyYmY1E/m/w2ESAeshBgAJ) for the thread that ultimately ended widescale adoption of the Token Binding Protocol._
    
[^2]:  Fett, D., Campbell, B., Bradley, J., Lodderstedt, T., Jones, M., and D. Waite, "OAuth 2.0 Demonstrating Proof of Possession (DPoP)", RFC 9449, DOI 10.17487/RFC9449, September 2023, <[https://www.rfc-editor.org/info/rfc9449](https://www.rfc-editor.org/info/rfc9449)\>.
    
[^3]:  For examples of how specific use cases are handled, see the profile of OAuth 2.0 and OpenID Connect recommended by the OpenID Foundation’s FAPI Working Group that focuses on use cases requiring high security, like Open Banking: Fett, D. “FAPI 2.0 Security Profile” Implementers Draft, December, 2022, https://openid.net/specs/fapi-2\_0-security-profile-ID2.html
    
[^4]:  There is work underway in the IETF to standardized real-time token revocation, but the work is still in draft form. See Parecki, A., “Global Token Revocation,” draft-parecki-oauth-global-token-revocation, [https://datatracker.ietf.org/doc/draft-parecki-oauth-global-token-revocation/](https://datatracker.ietf.org/doc/draft-parecki-oauth-global-token-revocation/).
    
[^5]:  Richer, Justin, and Antonio Sanso. 2017. _OAuth 2 in Action_. Manning.
    
[^6]:  Jones, M. and D. Hardt, "The OAuth 2.0 Authorization Framework: Bearer Token Usage", RFC 6750, DOI 10.17487/RFC6750, October 2012, <https://www.rfc-editor.org/info/rfc6750>.
    
[^7]:  Campbell, B., Bradley, J., Sakimura, N., and T. Lodderstedt, "OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens", RFC 8705, DOI 10.17487/RFC8705, February 2020, <https://www.rfc-editor.org/info/rfc8705>.
    
[^8]:  Hardt, D., Ed., "The OAuth 2.0 Authorization Framework", RFC 6749, DOI 10.17487/RFC6749, October 2012, <[https://www.rfc-editor.org/info/rfc6749](https://www.rfc-editor.org/info/rfc6749)\>.
    
[^9]:  Grassi, Paul A, James L Fenton, Elaine M Newton, Ray A Perlner, Andrew R Regenscheid, William E Burr, Justin P Richer, et al. 2017. “Digital Identity Guidelines: Authentication and Lifecycle Management.” [https://doi.org/10.6028/nist.sp.800-63b](https://doi.org/10.6028/nist.sp.800-63b).
    
[^10]:  Cappalli, T. and Tulshibagwale, A. “OpenID Continuous Access Evaluation Profile 1.0 – Draft 03” 2024-06-19, https://openid.net/specs/openid-caep-1\_0-ID2.html
    
[^11]:  Grassi, Paul A, Justin P Richer, Sarah K Squire, James L Fenton, Ellen M Nadeau, Naomi B Lefkovitz, Jamie M Danker, Yee-Yin Choong, Kristen K Greene, and Mary F Theofanos. 2017. “Digital Identity Guidelines: Federation and Assertions.” [https://doi.org/10.6028/nist.sp.800-63c](https://doi.org/10.6028/nist.sp.800-63c).
    
[^12]:  RFC 6749, "The OAuth 2.0 Authorization Framework”.
    
[^13]:  Fletcher, George, Pieter Kasselman, Atul Tulshibagwale, “Transaction Tokens,” last updated 2024-07-03, [https://datatracker.ietf.org/doc/draft-ietf-oauth-transaction-tokens/](https://datatracker.ietf.org/doc/draft-ietf-oauth-transaction-tokens/).
    
[^14]:  “Manipulator-in-the-middle Attack \| OWASP Foundation,” n.d. https://owasp.org/www-community/attacks/Manipulator-in-the-middle\_attack.
    
[^15]:  Trevino, Aranza, and Aranza Trevino. 2024. “What Are Zero Standing Privileges?” Keeper Security Blog - Cybersecurity News & Product Updates. April 29, 2024. [https://www.keepersecurity.com/blog/2024/04/29/what-are-zero-standing-privileges/](https://www.keepersecurity.com/blog/2024/04/29/what-are-zero-standing-privileges/).
    
[^16]:  Carter, M. K., (2022) “Techniques To Approach Least Privilege”, _IDPro Body of Knowledge_ 1(9). doi: [https://doi.org/10.55621/idpro.88](https://doi.org/10.55621/idpro.88)
    
[^17]:  “SPIFFE – Secure Production Identity Framework for Everyone,” n.d. https://spiffe.io/.
    
[^18]:  Sakimura, Nat, John Bradley, Michael Jones, Breno De Medeiros, and Chuck Mortimore. 2023. “OpenID Connect Core 1.0 incorporating errata set 2.” OpenID Foundation. [https://openid.net/specs/openid-connect-core-1\_0.html](https://openid.net/specs/openid-connect-core-1_0.html).
    
[^19]:  Parecki, A. “Global Token Revocation,” draft-parecki-oauth-global-token-revocation, https://datatracker.ietf.org/doc/draft-parecki-oauth-global-token-revocation/.
    
[^20]:  “Workload Identity in Multi System Environments (Wimse).” n.d. [https://datatracker.ietf.org/group/wimse/about/](https://datatracker.ietf.org/group/wimse/about/).
