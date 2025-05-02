---
layout: columns
title: An Introduction to OpenID Connect
permalink: /docs/oidc_oauth/idpro_bok/109
date: 2024-12-11
modify_date: 2025-05-01
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "OpenID Connect", "OAuth 2.0"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/109/](https://bok.idpro.org/article/id/109/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

The OpenID Connect (OIDC) specification builds on the OAuth 2.0 framework as a widely adopted identity layer. It provides a standardized and interoperable method for authenticating users and retrieving basic profile information via an ID Token. By leveraging REST-like protocols, OIDC ensures seamless integration across systems and platforms.

This article delves into the process of OpenID Providers (OP) connecting with federated Identity Providers (IdPs) to authenticate users, which facilitates the retrieval of user claims that can be returned to Relying Parties (RPs), enabling them to make informed decisions.

Keywords: OpenID Connect, OAuth 2.0, Authorization Server, Identity Providers, OpenID Provider

@column
## 概要

OpenID Connect（OIDC）仕様は、OAuth 2.0フレームワーク上に成り立ち、広く受け入れられているアイデンティティレイヤーです。OIDC仕様は、IDトークンを使ったユーザーの認証および基本的なプロファイル情報の収集のための標準化された、相互運用可能な方法を提供します。RESTに似たプロトコルを利用することで、OIDCはシステムおよびプラットフォームを横断してシームレスな統合を保証します。

OpenIDプロバイダー（OP）は、ユーザーの認証のためにフェデレーションされたアイデンティティプロバイダー（IdP）と接続し、これにより、リライングパーティ（RP）に返却されるユーザーのクレームを取得できるようになり、RPが情報に基づいた決定を下せるようになります。本記事では、このOpenIDプロバイダー（OP）のプロセスについて掘り下げます。

**Keywords:** OpenID Connect, OAuth 2.0, 認可サーバー, アイデンティティプロバイダー, OpenIDプロバイダー

@row
By Anoop Gupta (Capital One)

© 2024 IDPro, Anoop Gupta (Capital One)

To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code).

@row
## About OpenID Connect

OpenID Connect (OIDC) is a framework that facilitates the creation of a secure Internet identity ecosystem.[^1] It provides seamless integration and robust support while prioritizing security and privacy configurations. Additionally, it promotes interoperability and boasts widespread client and device support.

Authorization Servers implementing the OpenID Connect (OIDC) protocol are called OpenID Providers (OP). A Relying Party (RP) connects to the OP to obtain an ID token as an assertion that the user has successfully authenticated and to receive a unique identifier representing the user. Additional purposes are ensuring the user is authorized for requested access and obtaining user attributes. The OP may authenticate users directly or delegate authentication to federated or non-federated Identity Providers (IDPs) to facilitate sign-in flows on web or mobile applications and share user profile information upon successful authentication. OpenID Connect does not define how OPs integrate with federated IDPs. Such integrations are left to the implementation details of the OP. The OP may act as a bridge in these cases, using proprietary or other non-standard protocols to authenticate users via the federated IDPs.

RPs use the authenticated user claims found in the issued tokens to comprehend the user's authentication process and the level of assurance, allowing RPs to make well-informed decisions.

For this article, the federated IDP flow is referenced. Note that OIDC does not mandate or standardize how federated IDPs are integrated. These integrations depend on the implementation details of the OP and may involve non-standard protocols or proprietary methods.

@column
## OpenID Connectについて

OpenID Connect（OIDC）はセキュアなインターネットアイデンティティエコシステムの構築を推進するフレームワークです。[^1] OIDCはセキュリティとプライバシー設定を優先しながら、シームレスな結合と強固なサポートを提供します。加えて、OIDCは相互運用性を促進し、クライアントとデバイスのサポートの拡大を加速させています。

OpenID Connect（OIDC）プロトコルを実装している認可サーバーは、OpenIDプロバイダー（OP）と呼ばれます。リライングパーティ（RP）はOPに接続し、ユーザーが認証に成功したことを証明するIDトークンを取得し、ユーザーを表現するユニークな識別子を受け取ります。更なる目的は、要求しているアクセス権についてユーザーが認可されていることを保証することと、ユーザー属性を取得することです。OPは直接ユーザーを認証するかもしれませんし、認証をフェデレーションされた、またはフェデレーションされていないアイデンティティプロバイダー（IDP）に委譲し、Webまたはモバイルアプリケーションでのサインインフローを促進し、認証成功時にユーザープロファイル情報の共有するかもしれません。OpenID Connectは、OPがフェデレーションされたIDPとどのように統合するかは定義しません。そのような統合は、OPの詳細実装に残されています。OPはこれらのケースでの橋渡しとして機能し、フェデレーションされたIDPを使ってユーザーを認証するためにプロプライエタリまたは標準ではないプロトコルを利用する可能性があります。

RPはユーザーの認証プロセスと保証レベルを理解するために、発行されたトークン内で確認した認証されたユーザーのクレームを利用し、RPは充分な情報に基づく決定が可能になります。

本稿では、フェデレーションされたIDPフローを参照します。OIDCはフェデレーションされたIDPとどのように統合されるかを義務付けたり、標準化したりはしていません。これらの統合は、OPの実装詳細に依存し、非標準のプロトコルまたはプロプライエタリな手法を含むかもしれません。

@row
### Background

The OAuth 2.0 specification defines a framework where clients or Relying Parties (RPs) connect with Resource Servers to access API resources on behalf of resource owners.[^2] The OP is pivotal in allowing this integration between the parties involved.

Bertrand Carlier's article "[An Introduction to OAuth 2.0](https://bok.idpro.org/article/id/99/)" in the IDPro Body of Knowledge provides a comprehensive overview of OAuth 2.0 and touches on OIDC. It is a valuable starting point for understanding these widely used protocols and covers fundamental terminology and references to IETF RFC details that describe the protocols.

OIDC emphasizes user authentication and introduces the concept of the ID Token. This token is exchanged between the OP and RP. It takes the form of a JSON Web Token (JWT) and communicates details about the authenticated user's identity through predefined [standard claims](https://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) and information related to the authentication process.[^3], [^4], [^5]

The OIDC specification allows RPs to access more detailed user information through the UserInfo endpoint, a protected resource in the OAuth 2.0 framework. During the authentication process, RPs can request user claims from this endpoint using the Access Token obtained from the OP. The user claims are returned as a JSON object containing name-value pairs, providing comprehensive user information to the RP.

@column
### 背景

OAuth 2.0仕様は、クライアントまたはリライングパーティ（RP）がリソースサーバーに接続し、リソースオーナーに代わってAPIリソースにアクセスするフレームワークを定義します。[^2] OPは、関係する当事者同士の結合を可能にするさいに極めて重要です。

IDPro Body of KnowledgeのBertrand Carlierの記事「[An Introduction to OAuth 2.0](https://bok.idpro.org/article/id/99/)」は、OAuth 2.0の包括的な解説を提供しており、OIDCにも触れています。この記事は、幅広く利用されているプロトコルの理解のために価値のある出発点であり、基本的な用語解説とプロトコルを記述しているIETF RFCの詳細への参照をカバーしています。

OIDCはユーザーの認証を強調し、IDトークンの概念を導入します。このトークンはOPとRPの間でやり取りされます。IDトークンはJSON Web Token（JWT）の形式をとり、事前に定義された[標準クレーム](https://openid.net/specs/openid-connect-core-1_0.html#StandardClaims)を介して認証されたユーザーのアイデンティティに関する詳細および認証プロセスに関係した情報について通信します。[^3], [^4], [^5]

OIDC仕様は、RPがUserInfoエンドポイントを介してより詳細なユーザー情報やOAuth 2.0フレームワークによって保護されたリソースにアクセスできるようにします。認証プロセス中に、RPはOPから取得したアクセストークンを使ってこのエンドポイントにユーザークレームを要求できます。ユーザークレームは、JSONオブジェクトとして返却され、名前-値のペアが含まれており、RPに対して包括的なユーザー情報を提供します。

@row
### Terminology

Terminology is primarily derived from the [Terminology in the IDPro Body of Knowledge](https://bok.idpro.org/article/id/41/).

|     |     |     |
| --- | --- | --- |
| Term | Definition | Source |
| Identity Provider (IdP) | An IdP is a service that stores and manages digital identities. Companies use these services to allow their employees or users to connect with the resources they need. They provide a way to manage access, adding or removing privileges while security remains tight. | [Identity Providers (IdPs): The key to secure digital access.](https://www.okta.com/identity-101/why-your-company-needs-an-identity-provider/) |
| OAuth 2.0 | The OAuth 2.0 authorization framework enables a third-party application to obtain limited access to an HTTP service, either on behalf of a resource owner by orchestrating an approval interaction between the resource owner and the HTTP service or by allowing the third-party application to obtain access on its own behalf. | [The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749#section-1.1) |
| Authorization Server (AS) | The Authorization Server is able to authorize a client, issue tokens, and potentially validate tokens. It is also responsible for authenticating users, either directly or through federation. | [An Introduction to OAuth2.0](https://bok.idpro.org/article/id/99/) |
| OpenID Connect | OpenID Connect is a simple identity layer on top of the OAuth 2.0 protocol. It enables Clients to verify the identity of the End-User based on the authentication performed by an Authorization Server, as well as to obtain basic profile information about the End-User in an interoperable and REST-like manner. | [Federation Simplified (v2)](https://bok.idpro.org/article/id/62/) |
| OpenID Provider (OP) | An OpenID Provider (OP) is an entity that has implemented the OpenID Connect and OAuth 2.0 protocols, OP's can sometimes be referred to by the role it plays, such as: an identity provider (IDP), or an authorization server, or a security token service. | [What is OpenID Connect](https://openid.net/developers/how-connect-works/) |
| Resource Server | The server hosting the protected resources, capable of accepting and responding to protected resource requests using access tokens. Typically, exposed as an API. | [The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749#section-1.1) |
| Relying Party (RP) | A component, system, or application that uses the IDP to identify its users. The RP has its own resources and logic. Note that the term 'relying service' is used in the ISO/IEC standards to encompass all types of components that use identity services, including systems, sub-systems, and applications, independent of the domain or operator. We will use the more common Relying Party (or RP). An RP roughly corresponds to the Agency Endpoint in the FICAM model or to Identity Consumers in the Internet2 model. | [IAM Reference Architecture](https://bok.idpro.org/article/id/76/) |
| Client | An application making protected resource requests on behalf of the resource owner and with its authorization. The term "client" does not imply any particular implementation characteristics (e.g., whether the application executes on a server, a desktop, or other devices). | [The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749#section-1.1) |

@column
### 用語解説

用語解説は主として[Terminology in the IDPro Body of Knowledge](https://bok.idpro.org/article/id/41/)に由来します。

|     |     |     |
| --- | --- | --- |
| 用語 | 定義 | ソース |
| アイデンティティプロバイダー（IdP） | IdPとは、デジタルアイデンティティを保管、管理するサービスです。企業はこれらのサービスを利用し、従業員やユーザーに対して、彼らが必要とするリソースに接続できるようにします。これらのサービスはアクセスを管理する方法を提供し、セキュリティは厳しいままに特権の追加または削除を実施します。 | [Identity Providers (IdPs): The key to secure digital access.](https://www.okta.com/identity-101/why-your-company-needs-an-identity-provider/) |
| OAuth 2.0 | OAuth 2.0とは、リソースオーナーとHTTPサービス間での調整された承認手続き、またはサードパーティアプリケーションが自身に代わってアクセス権を取得することによって、サードパーティアプリケーションがリソースオーナーに代わってHTTPサービスに対して制限されたアクセス権を取得することを可能にする認可フレームワークです。 | [The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749#section-1.1) |
| 認可サーバー（AS） | 認可サーバーとは、クライアントを保護し、トークンを発行し、潜在的にはトークンの検証をおこなうことができます。また、直接もしくはフェデレーションを通じて、ユーザーの認証にも責任を負います。 | [An Introduction to OAuth2.0](https://bok.idpro.org/article/id/99/) |
| OpenID Connect | OpenID Connectとは、OAuth 2.0プロトコル上の単なるアイデンティティレイヤーです。OpenID Connectは、相互運用が可能でRESTのような方法によってクライアントが、認可サーバーで実行された認証に基づいてエンドユーザーのアイデンティティを検証できるようにし、同時にエンドユーザーに関する基本プロファイル情報を取得できるようにします。 | [Federation Simplified (v2)](https://bok.idpro.org/article/id/62/) |
| OpenIDプロバイダー（OP） | OpenIDプロバイダー（OP）は、OpenID ConnectおよびOAuth 2.0プロトコルを実装したエンティティです。OPはアイデンティティプロバイダー（IDP）、認可サーバー、セキュリティトークンサービスなどが果たす役割から参照される場合があります。 | [What is OpenID Connect](https://openid.net/developers/how-connect-works/) |
| リソースサーバー | 保護されたリソースがホストされているサーバーであり、アクセストークンを使って保護されたリソースに対するリクエストを受領し、レスポンスをおこなうことができます。通常は、APIとして公開されます。 | [The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749#section-1.1) |
| リライングパーティ（RP） | ユーザーを特定するためにIDPを利用するコンポーネント、システムまたはアプリケーション。RPは、独自のリソースとロジックを有しています。「リライングサービス」という用語は、領域や運用者にかかわらず、アイデンティティサービスを利用するシステム、サブシステムやアプリケーションを含んだ全ての種類のコンポーネントを包含するISO/IEC標準仕様において使われることに注意してください。私たちはより一般的なリライングパーティ（またはRP）を使用します。RPは大まかにいうと、FICAMモデルにおけるエージェンシーエンドポイント、Internet2モデルでのアイデンティティコンシューマーに対応します。 | [IAM Reference Architecture](https://bok.idpro.org/article/id/76/) |
| クライアント | リソースオーナーに代わって、その認可によって、保護されたリソースへリクエストをおこなうアプリケーション。「クライアント」という用語は、特定の実装特性（例、アプリケーションがサーバー、デスクトップまたはその他デバイスで実行されているかどうか）を意味するものではありません。 | [The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749#section-1.1) |

@row
## Tokens

The Authorization Code flow is the most commonly used method for RPs to obtain tokens in OIDC. This flow ensures secure communication between the RP and the Authorization Server through the following steps:

1.  User Authentication: The RP redirects the user to the Authorization Server, where the user logs in.
    
2.  Authorization Code Issuance: After successful authentication, the Authorization Server issues an Authorization Code to the RP.
    
3.  Token Exchange: The RP exchanges the Authorization Code for tokens via a secure back-channel server-to-server call. These tokens typically include:
    
    *   ID Token: Provides authenticated user identity claims.
        
    *   Access Token: Grants access to protected resources.
        
    *   Refresh Token (optional): Allows the RP to obtain new Access Tokens without requiring the user to log in again.
        

To enhance security, particularly for public clients, the Proof Key for Code Exchange (PKCE) extension is mandatory.[^6] While PKCE is mandatory for public clients, its use is also encouraged for confidential clients to provide additional protection against interception attacks. PKCE mitigates interception attacks by binding the authorization request to the token exchange process.[^7]

@column
## トークン

認可コードフローとは、OIDCにおいてRPがトークンを取得するために最も一般的に用いられるメソッドです。このフローは、以下のステップを通じてRPと認可サーバー間での安全なコミュニケーションを保証します：

1.  ユーザー認証：RPはユーザーを認可サーバーにリダイレクトし、ユーザーはそこでログインします。
    
2.  認可コード発行：認証成功後、認可サーバーは認可コードをRPに発行します。
    
3.  トークン引き換え：RPは、安全なバックチャネルでのサーバー間の呼び出しによって、認可コードをトークンに引き換えます。これらのトークンには通常、以下のものを含みます：
    
    *   IDトークン：認証されたユーザーのアイデンティティクレームを提供します
        
    *   アクセストークン：保護されたリソースへのアクセス権の付与
        
    *   リフレッシュトークン（オプション）：ユーザーに再度ログインを要求することなく、RPがアクセストークンを取得することを許可します・
        

セキュリティを強化するため、特にパブリッククライアントで、Proof Key for Code Exchange（PKCE）拡張機能が義務になっています。[^6] パブリッククライアントにとってPKCEは義務になっている一方で、その利用はコンフィデンシャルクライアントでも横取り攻撃に対して追加の保護を提供します。PKCEは、認可リクエストをトークン引き換えプロセスにバインドすることで横取り攻撃を軽減します。[^7]

@row
### ID Token

The ID Token is a critical element of OpenID Connect, designed to securely communicate user authentication details. It is structured as a JWT and includes claims such as:

*   sub: A unique identifier for the authenticated user.
    
*   Optional Claims: Additional claims like name, profile, or email, which must be explicitly requested using scopes (e.g., openid, profile, email).
    

To ensure integrity, the Authorization Server digitally signs the ID Token using JSON Web Signature (JWS).[^8] For enhanced confidentiality, the ID Token can also be encrypted with JSON Web Encryption (JWE) using symmetric or asymmetric algorithms.[^9]

Both Access Tokens and ID Tokens have expiration times to ensure security. RPs should validate the expiration (exp) claim in tokens before processing them.

@column
### IDトークン

IDトークンはOpenID Connectの重大な要素であり、ユーザー認証の詳細を安全に通信するために設計されています。IDトークンはJWTとして構成され、以下のクレームを含んでいます：

*   sub：認証されたユーザーのユニークな識別子
    
*   追加のクレーム：スコープム（例えば、openid、profile、email）を使って明示的に要求されるべき、name、profileやemailのような追加のクレー。
    

真正性を確保するため、認可サーバーはJSON Web Signature（JWS）を使ってIDトークンにデジタルに署名します。[^8] 機密性を強化するため、IDトークンも共有鍵または非対称鍵暗号方式を使ったJSON Web Encryption（JWE）によって暗号化をおこないます。[^9]

アクセストークンとIDトークンの両方とも、セキュリティを保証するために有効期限を有しています。RPは、トークンを利用する前にトークン内の有効期限（exp）クレームを検証すべきです。

@row
## UserInfo Endpoint

The UserInfo endpoint is a key feature of OIDC, enabling RPs to retrieve additional user claims beyond those provided in the ID Token. Common claims retrieved via the UserInfo endpoint include name, email, birthdate, and address, depending on the scopes requested by the RP. These claims, formatted as a JSON object, offer more detailed information about the user’s profile or authentication process.

RPs should follow the principle of data minimization by requesting only the claims necessary for their application to function.

@column
## UserInfoエンドポイント

UserInfoエンドポイントはOIDCの重要な機能であり、RPがIDトークンで提供されるユーザークレーム以上の追加のクレームを取得することができます。UserInfoエンドポイントを介して収集できる一般的なクレームは、RPによって要求されたスコープに依存しますが、name、email、birthdateおよびaddressがあります。これらのクレームは、JSONオブジェクト形式であり、ユーザーのプロファイルまたは認証プロセスについてのより詳細な情報を提供します。

RPは、自身のアプリケーションが機能するために必要なクレームだけを要求し、データ最小化の原則に従うべきです。

@row
### Access and Authorization

The UserInfo endpoint requires an Access Token, issued by the Authorization Server during the authorization process, to authenticate and authorize requests. The claims available from the UserInfo endpoint depend on:

*   The scopes requested during the authorization process (e.g., profile, email).
    
*   The OpenID Provider's (OP) configuration and policies.
    

RPs may also explicitly request specific claims using the claims parameter in the authorization request. This allows for fine-grained control over the user information retrieved from the OP.

@column
### アクセス権と認可

UserInfoエンドポイントは、リクエストを認証および認可するために、認可プロセスで認可サーバーから発行されたアクセストークンを要求します。UserInfoエンドポイントから取得できるクレームは以下に依存します：

*   認可プロセスで要求されたスコープ（例えばprofile、email）。
    
*   OpenIDプロバイダー（OP）の設定およびポリシー。
    

RPは、認可リクエストのクレームパラメータを利用して明示的に特定のクレームを要求するかもしれません。これはOPから取得するユーザー情報に対するきめ細かな制御を可能にします。

@row
### Optional Claims and Provider Discretion

The OP determines which claims are included in the ID Token and which are provided through the UserInfo endpoint. Not all claims in the ID Token are guaranteed to be available via the UserInfo endpoint. This separation ensures flexibility while adhering to privacy and security considerations.

@column
### 追加のクレームとプロバイダーの裁量

OPは、どのクレームはIDトークンに含まれ、どのクレームはUserInfoエンドポイントで提供されるべきかを決定します。IDトークンに含まれるクレーム全てがUserInfoエンドポイントから入手できることが保証されるわけではありません。このような分離は、プライバシーとセキュリティを考慮しつつ、柔軟性を保証します。

@row
### Data Security

To ensure confidentiality, the response from the UserInfo endpoint can be encrypted using JWE. This encryption can be implemented using symmetric or asymmetric algorithms, depending on the RP’s requirements, to safeguard sensitive user information during transmission.

@column
### データセキュリティ

機密性を保証するため、UserInfoエンドポイントからのレスポンスはJWEを使って暗号化できます。この暗号化は、RPの要件に依存して、共有鍵または非対称鍵暗号方式で実装でき、通信中の機密ユーザー情報を保護します。

@row
### Enhanced Decision-Making

The detailed claims retrieved from the UserInfo endpoint empower RPs to make informed decisions about user access, authentication levels, and personalized experiences within their applications.

By offering this additional layer of user information, the UserInfo endpoint complements the ID Token, allowing RPs to access a richer set of data while maintaining robust security and privacy standards.

@column
### 意思決定の強化

UserInfoエンドポイントから取得できる詳細なクレームにより、RPはアプリケーション内のユーザーのアクセス権、認証レベルおよびパーソナライズされた体験についての情報に基づく決定ができるようになります。

ユーザー情報の追加レイヤーを提供することで、UserInfoエンドポイントはIDトークンを補完し、RPが堅固なセキュリティとプライバシーの標準仕様を維持しながら、より多くのデータセットへアクセスできるようにします。

@row
## OIDC Flow

OIDC provides a secure framework for authenticating users and exchanging identity information between RPs and OPs In some cases, the OP may delegate authentication to an external IDP. The typical sequence of the OIDC flow includes the following steps:

1.  The Relying Party (RP) initiates the OpenID Connect (OIDC) flow with the Authorization Server to obtain user claims.
    
2.  The Authorization Server initiates a new OIDC flow with the federated IDP, providing user authentication, and claims. The login screen is not rendered on the federated IdP if the user has already been authenticated.
    
3.  After the user is successfully authenticated, the Identity Provider (IDP) issues an authorization code to the Authorization Server.
    
4.  The Authorization Server exchanges the authorization code to retrieve the tokens.
    
5.  The Authorization Server can optionally call the UserInfo endpoint of the federated IdP to retrieve extra user claims.
    
6.  The Authorization Server returns an authorization code to the Relying Party.
    
7.  The Relying Party (RP) exchanges the authorization code to retrieve the tokens from the Authorization Server.
    
8.  The RP can optionally call the UserInfo endpoint on the Authorization Server to retrieve additional user claims.
    
9.  The RP presents the access token to the Authorization Server.
    
10.  The Authorization Server authenticates the RP using an access token to retrieve the protected resource.
    
11.  The Authorization Server provides the protected resource to the RP.
    

Additional Notes

*   Flexibility in Claims Sharing: The OP and, if applicable, the IDP may provide claims through their respective UserInfo endpoints. This flexibility allows RPs to access detailed user profiles tailored to their needs.
    
*   Simplified Representation: This explanation omits intermediate browser redirects and technical details for brevity.
    
*   Error Handling: If an error occurs at any step, such as invalid credentials or an expired authorization code, the OP should return an error response detailing the reason. RPs must handle these errors gracefully to provide feedback to the user.
    

By following this structured flow, OIDC ensures secure and reliable authentication while providing a flexible mechanism for retrieving identity and profile information. This enables RPs to create personalized and secure user experiences.

@column
## OIDCフロー

OIDCは、ユーザーの認証とRPとOPの間のアイデンティティ情報を交換するための安全なフレームワークを提供します。一部のケースでは、OPは外部IDPに認証を委譲するかもしれません。OIDCフローの通常のシーケンスは以下のステップを踏みます：

1.  リライングパーティ（RP）は、ユーザークレームを取得するために、認可サーバーとともにOpenID Connect（OIDC）フローを開始します。
    
2.  認可サーバーは、ユーザー認証とクレームを提供するフェデレーションされたIDPとともに新しいOIDCフローを開始します。ユーザーが既に認証している場合、ログイン画面はフェデレーションされたIdPではレンダリングされません。
    
3.  ユーザーが認証に成功した後、アイデンティティプロバイダー（IDP）は認可サーバーに認可コードを発行します。
    
4.  認可サーバーは、トークンを所得するために認可コードを交換します。
    
5.  オプションとして、認可サーバーはフェデレーションされたIdPのUserInfoエンドポイントを呼び出して、追加のユーザークレームを取得します。
    
6.  認可サーバーはリライングパーティに認可コードを返却します。
    
7.  リライングパーティ（RP）は認可コードを交換し、認可サーバーからトークンを取得します。
    
8.  オプションとして、RPは認可サーバーのUserInfoエンドポイントを呼び出して追加のユーザークレームを取得します。
    
9.  RPは認可サーバーにアクセストークンを提示します。
    
10.  認可サーバーは、保護されたリソースを利用するために、アクセストークンを使ってRPを認証します。
    
11.  認可サーバーはRPに保護されたリソースを提供します。
    

追加の注意事項

*   クレーム共有の柔軟性：OPおよび、該当する場合にはIDPは、それぞれのUserInfoエンドポイントを通じてクレームを提供できます。この柔軟性はRPはニーズに合わせて詳細なユーザープロファイルにアクセスを可能にします。
    
*   単純化された表現：この説明では、簡潔に表現するために、中間のブラウザリダイレクトや技術的な詳細について省略しています。
    
*   エラーハンドリング：無効なクレデンシャルや有効期限切れとなった認可コードのように、特定のステップでエラーが発生した場合、OPは理由を詳細に表したエラーレスポンスを返却すべきです。RPはこれらのエラーを上品にハンドリングし、ユーザーにフィードバックを提供しなければなりません。
    

この構造化されたフローに従うことで、OIDCは安全で新r内できる認証を保証し、アイデンティティとプロファイル情報を取得するための柔軟なメカニズムを提供します。これにより、RPはパーソナライズされた安全なユーザー体験を生み出すことが可能になります。

@row
![1. User Agent/Browser sends Authorize request 2. Auth Server redirects to IDP to render login screen 3. User authenticates and provides claims 4. Auth Server returns authorization code 5. Fetch tokens using authorization code 6. (optionally) call UserInfo endpoint using Access Token 7. Present Access Token to access resource 8. Auth Server fetches protected resource from resource server 9. Auth Server returns protected resource](/assets/images/idpro_bok/oidc-image1.png)

Figure 1: OAuth 2.0 and OpenID Connect flow

@row
## Logout

OIDC supports RP-initiated and back-channel logout mechanisms. However, the implementation of these protocols varies among OPs. RPs should consult the OP's metadata to determine the supported logout methods. The OP and IDP can provide logout endpoints for the RP to call during the user logout flow. Logout endpoints ensure no further calls can be made to the Resource Server using invalidated access tokens. In addition to invalidating tokens, RPs should ensure session cookies are cleared to fully terminate the user's session.

RP-initiated and back-channel logout are two mechanisms for ending a user session on the Identity Provider and invalidating the associated tokens.

*   RP-Initiated Logout ( [https://openid.net/specs/openid-connect-rpinitiated-1\_0.html](https://openid.net/specs/openid-connect-rpinitiated-1_0.html) )
    
*   Back Channel Logout ( [https://openid.net/specs/openid-connect-backchannel-1\_0.html](https://openid.net/specs/openid-connect-backchannel-1_0.html) )
    

Some OPs also support Single Logout (SLO), enabling simultaneous session termination across multiple RPs. RPs should review the OP's metadata to determine the supported logout methods and endpoints.

In general, implementations of logout mechanisms may vary significantly across OPs. RPs should test these flows thoroughly to ensure compatibility.

@column
## ログアウト

OIDCはRP-initiatedおよびバックチャネルのログアウトメカニズムをサポートしています。しかし、これらのプロトコルの実装はOPによって異なります。RPは、サポートされているログアウトメソッドを決定すrためにOPのメタデータを確認すべきです。OPとIDPは、ユーザーのログアウトフロー中にRPが呼び出しをおこなうログアウトエンドポイントを提供します。ログアウトエンドポイントは、無効化されたアクセストークンを使ってこれ以上呼び出しを実行しないことを保証します。トークン尾無効化に加えて、ユーザーのセッションを完全に終了させるため、RPはセッションCookieの抹消を保証すべきです。

RP-initiatedおよびバックチャネルのログアウトは、アイデンティティプロバイダー上のユーザーセッションの終了と関連するトークン尾無効化のための2酒類の仕組みです。

*   RP-Initiatedログアウト（[https://openid.net/specs/openid-connect-rpinitiated-1\_0.html](https://openid.net/specs/openid-connect-rpinitiated-1_0.html)）
    
*   バックチャネルログアウト（[https://openid.net/specs/openid-connect-backchannel-1\_0.html](https://openid.net/specs/openid-connect-backchannel-1_0.html)）
    

一部のOPは、複数のRPに同時にセッションを終了させられるシングルログアウト（SLO）もサポートしています。RPは、サポートされているログアウト手法とエンドポイントを決定するためにOPのメタデータを確認すべきです。

一般的に、ログアウトの仕組みの実装は、OPによって大きく異なります。RPはこれらのフローを充分にテストし、互換性を確認すべきです。

@row
## Discovery

The OpenID Connect (OIDC) discovery mechanism simplifies the integration of Relying Parties (RPs) with OpenID Providers (OPs) by providing a standardized method for retrieving configuration metadata. This metadata is accessible at a well-known URL: /.well-known/openid-configuration.

@column
## ディスカバリー

OpenID Connect（OIDC）ディスカバリーメカニズムは、設定メタデータを収集する標準化されたメソッドを提供することで、OpenIDプロバイダー（OP）とリライングパーティ（RP）との結合を簡単にします。このメタデータはwell-known URL: /.well-known/openid-configuration でアクセスできます。

@row
### Metadata Overview

The discovery document includes essential details about the OP's capabilities, such as:

*   **Endpoints:** URLs for token issuance, user authentication, and the UserInfo API.
    
*   **Supported Grant Types:** Information on flows like authorization code and implicit.
    
*   **Cryptographic Algorithms:** Supported methods for signing and encrypting tokens.
    
*   **Scopes and Claims:** Available scopes and the claims that can be requested by RPs.
    

@column
### メタデータ概要

ディスカバリードキュメントは、OPの能力について以下のような重要な詳細情報を含みます：

*   **エンドポイント**：トークン発行、ユーザー認証およびUserInfo APIのURL。
    
*   **サポートされているグラントタイプ**：認可コードやインプリシットのようなフローについての情報。
    
*   **暗号アルゴリズム**：サポートされているトークンの署名および暗号化のメソッド。
    
*   **スコープおよびクレーム**：RPによってリクエストされたときに利用可能なスコープおよびクレーム。
    

@row
### Dynamic Client Registration

The metadata also supports dynamic client registration, allowing RPs to programmatically register with the OP. This feature automates integration, reducing manual setup and ensuring consistency across different implementations. Dynamic client registration should be protected with appropriate measures, such as client authentication or pre-authorization by the OP, to prevent misuse.

@column
### 動的クライアント登録

メタデータは動的クライアント登録もサポートしており、これはRPがOPにプログラマティックに登録することが可能にします。この機能は結合を自動化し、手動セットアップを減らし、異なる実装での一貫性を確保します。動的クライアント登録は、悪用を防ぐためにクライアント認証やOPによる事前認可のような適切な方法によって保護されるべきです。

@row
### Interoperability and Security

By centralizing these configuration details, the discovery mechanism:

*   Streamlines the setup process for RPs.
    
*   Enhances interoperability between systems.
    
*   Improves security by ensuring that the RP operates with accurate, up-to-date information.
    

@column
### 相互運用性とセキュリティ

これらの設定詳細を一元化することで、ディスカバリーの仕組みは以下を実現します：

*   RPにとって設定プロセスを合理化します。
    
*   システム間の相互運用性を強化します。
    
*   RPが正確で最新の情報を運用することを保証することで安全性を向上させます。
    

@row
### Best Practices

RPs should periodically validate the information retrieved from the discovery document to account for any updates or changes in the OP's configuration. This ensures seamless operation and adherence to the latest security standards.

The discovery mechanism is a cornerstone of OIDC's flexibility, enabling a wide range of applications to integrate quickly and securely with OpenID Providers.

@column
### ベストプラクティス

RPは、OPの設定の更新や変更を考慮し、定期的にディスカバリードキュメントから収集した情報を検証すべきです。これは、シームレスな運用および最新のセキュリティ標準仕様への準拠を保証します。

ディスカバリーメカニズムは、OIDCの柔軟性の要石であり、幅広いアプリケーションがOpenIDプロバイダーと素早く、安全に統合できるようにします。

@row
## Beyond The Introduction

In addition to what has been mentioned in this introduction, the OIDC specification covers a wide range of measures to ensure the secure transmission of user data. Several other topics are included that can enhance the authentication process.

*   OAuth 2.0 Step Up Authentication Challenge Protocol ( [RFC 9470](https://www.rfc-editor.org/info/rfc9470) )
    
*   Vector of Trust ( [RFC 8485](https://www.rfc-editor.org/info/rfc8485) )
    
*   Client Dynamic Registration ( [_RFC 7591_](https://www.rfc-editor.org/info/rfc7591) )
    
*   Authorization Server Metadata ( [_RFC 8414_](https://www.rfc-editor.org/info/rfc8414) )
    

@column
## イントロダクションを超えて

このイントロダクションにおいて述べたことに加えて、OIDC仕様はユーザーデータの安全な伝送を保証する幅広い手段をカバーしています。認証プロセスを強化するためのいくつかの他のトピックが含まれています。

*   OAuth 2.0ステップアップ認証チャレンジプロトコル（[RFC 9470](https://www.rfc-editor.org/info/rfc9470)）
    
*   信頼のベクトル（[RFC 8485](https://www.rfc-editor.org/info/rfc8485)）
    
*   クライアント動的登録（[_RFC 7591_](https://www.rfc-editor.org/info/rfc7591)）
    
*   認可サーバーメタデータ（[_RFC 8414_](https://www.rfc-editor.org/info/rfc8414)）
    

@row
### Additional Reading

1.  Lodderstedt, T., Ed., McGloin, M., and P. Hunt, "OAuth 2.0 Threat Model and Security Considerations", RFC 6819, DOI 10.17487/RFC6819, January 2013, <https://www.rfc-editor.org/info/rfc6819>.
    
2.  M. Jones, "JSON Web Key", RFC 7517, DOI 10.17487/RFC7517, May 2015, <https://www.rfc-editor.org/info/rfc7517 >
    
3.  Jones, M. and D. Hardt, "The OAuth 2.0 Authorization Framework: Bearer Token Usage", RFC 6750, DOI 10.17487/RFC6750, October 2012, <https://www.rfc-editor.org/info/rfc6750>.
    
4.  Richer, J., Ed., "OAuth 2.0 Token Introspection", RFC 7662, DOI 10.17487/RFC7662, October 2015, <[https://www.rfc-editor.org/info/rfc7662](https://www.rfc-editor.org/info/rfc7662)\>.
    

- - -

[^1]:  Sakimura, N., Bradley, J., Jones, M., de Medeiros, B., Mortimore, C. “OpenID Connect Core 1.0 incorporating errata set 1,” OpenID Foundation, November 2014, [https://openid.net/specs/openid-connect-core-1\_0.html](https://openid.net/specs/openid-connect-core-1_0.html) .
    
[^2]:  Hardt, D., Ed., "The OAuth 2.0 Authorization Framework", RFC 6749, DOI 10.17487/RFC6749, October 2012, <[https://www.rfc-editor.org/info/rfc6749](https://www.rfc-editor.org/info/rfc6749)\>.
    
[^3]:  Y.Sheffer, D.Hardt, M.Jones, "JSON Web Token Best Current Practices", RFC 8725, DOI 10.17487/RFC8725, February 2020, <[https://www.rfc-editor.org/info/rfc8725](https://www.rfc-editor.org/info/rfc8725)\>.
    
[^4]:  Bertocci, V., "JSON Web Token (JWT) Profile for OAuth 2.0 Access Tokens", RFC 9068, DOI 10.17487/RFC9068, October 2021, <https://www.rfc-editor.org/info/rfc9068>.
    
[^5]:  Jones, M., Bradley, J., and N. Sakimura, "JSON Web Token (JWT)", RFC 7519, DOI 10.17487/RFC7519, May 2015, <[https://www.rfc-editor.org/info/rfc7519](https://www.rfc-editor.org/info/rfc7519)\>.
    
[^6]:  Sakimura, N., Ed., Bradley, J., and N. Agarwal, "Proof Key for Code Exchange by OAuth Public Clients", RFC 7636, DOI 10.17487/RFC7636, September 2015, <https://www.rfc-editor.org/info/rfc7636>.
    
[^7]:  Jones, M., Nadalin, A., Campbell, B., Ed., Bradley, J., and C. Mortimore, "OAuth 2.0 Token Exchange", RFC 8693, DOI 10.17487/RFC8693, January 2020, <https://www.rfc-editor.org/info/rfc8693>.
    
[^8]:  M. Jones, J.Bradley, N.Sakimura M, “JSON Web Signature”, RFC 7515, DOI 10.17487/RFC7515, May 2015, < [https://www.rfc-editor.org/info/rfc7515](https://www.rfc-editor.org/info/rfc7515) >.
    
[^9]:  M. Jones, James Hilderbrand, “JSON Web Encryption (JWE)”, RFC 7516, DOI 10.17487/RFC7516, May 2015, <[https://www.rfc-editor.org/info/rfc7516](https://www.rfc-editor.org/info/rfc7516)\>.
