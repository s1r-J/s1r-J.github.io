---
layout: columns
title: Delegated Authentication Using a SAML Web Browser SSO Profile (v2)
permalink: /docs/oidc_oauth/idpro_bok/79
date: 2024-09-09
modify_date: 2024-11-11
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "SAML"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/79/](https://bok.idpro.org/article/id/79/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article builds on a generic IAM reference architecture to describe a common use case of an authentication service using the Security Assertion Markup Language (SAML). We show how a service (the relying party) uses the authentication capability of an identity provider during a web-based single sign-on action.

Keywords: SAML, Audit, Authentication, Assertion, Identity Register, Relying Party, Trust Anchor

@column
## 概要

本記事では汎用的なIAM参照アーキテクチャに基づいて、Security Assertion Markup Language（SAML）を使った認証サービスの一般的なユースケースについて説明します。どのようにサービス（リライングパーティ）がWebベースのシングルサインオンアクションを通じてアイデンティティプロバイダーの認証機能を利用するのかを示します。

Keywords: SAML, 監査, 認証, 検証, アイデンティティレジスタ, リライングパーティ, トラストアンカー

@row
By George B. Dobbs

© 2022 IDPro, George B. Dobbs

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction

This article is one of a set that illustrates several abstract components defined in the IDPro Body of Knowledge article, “IAM Reference Architecture.” [^1] This particular article focuses on a specific method of web-based single sign-on via the common use case of a service (the relying party) that uses the authentication capability of an identity provider (IDP) via the Security Assertion Markup Language (SAML) standard. This method allows the RP to delegate the authentication function to the IDP.

This widespread use case relies on trust between the IDP and the relying party (RP). There are various ways of doing this; this article assumes that the trust is based on the use of public-key cryptography, which involves exchanging certificates.

The SAML specification defines three different kinds of assertion statements; this article is only about the authentication assertion.

The SAML specification supports the mapping of identities between different names, known as federated identity. This article is restricted to a single domain, such as an organization providing access for its employees to web-based services provided by third-party vendors. In other words, a single domain of administration allows for the user identifiers to be shared.

Even a cursory review of the OASIS SAML standards documents will reveal an extremely rich and flexible structure. [^2] This article represents a very thin slice of its possibilities focusing on the run-time aspect of authentication using the web (HTTPS) messaging protocol. Technically, we are discussing what OASIS calls the Web Browser SSO profile, using the POST binding. [^3]

This synopsis stresses the importance of the Trust Root. The messaging between the IDP and RP passes through the User Agent. The User Agent must be considered untrusted, as a corrupted agent could potentially modify the messages. To protect against this modification, the messages are protected by a digital signature, which must be validated. It is the common certificate authority that acts as the Trust Root to support these signatures.

The topic of signatures becomes quite deep quickly and is not covered in detail here. The SAML specification relies on the W3C Recommendation XML Signature Syntax and Processing, which may be of interest. [^4]

@column
## 導入

本記事は、IDPro Body of Knowledgeの記事「IAM Reference Architecture」 [^1] で定義されている、いくつかの抽象的なコンポーネントを説明するセットの1つです。この記事では、Security Assertion Markup Language（SAML）標準仕様によってアイデンティティプロバイダー（IDP）の認証機能を使用するサービス（リライングパーティ）の一般的なユースケースを通じて、Webベースのシングルサインオンの特定の方法に焦点を当てています。この方法は、RPにIDPへの認証機能を委譲することを可能にしています。

この広く使われているユースケースは、IDPとリライングパーティ（RP）間の信頼に依存しています。信頼の確立にはさまざまな方法があります；この記事では証明書の交換を伴う公開鍵暗号の利用に基づいて信頼することを想定しています。

SAML仕様は3種類のアサーションステートメントを定義しています；本稿では、認証アサーションのみを取り上げます。

SAML仕様は、フェデレーションアイデンティティと呼ばれる、異なる名前間のアイデンティティのマッピングをサポートしています。本記事は、サードパーティベンダーが提供するWebベースのサービスに従業員がアクセスできるようにする組織など、単一ドメインに限定しています。つまり、単一の管理ドメインでは、ユーザー識別子を共有することができます。

OASIS SAML標準文書をざっと読んだだけでも、非常に豊富で柔軟な構造を持つことがわかります。 [^2] この記事は、Web（HTTPS）メッセージングプロトコルを使用した認証の実行の側面に焦点を当てた、その可能性のごく一部を紹介します。技術的には、OASISがPOSTバインディングを使用してWeb Browser SSOプロファイルと呼んでいるものについて議論しています。 [^3]

この概要は、トラストルートの重要性を強調しています。IDPとRP間のメッセージングは、ユーザーエージェントを介しておこなわれます。ユーザーエージェントは、破損したエージェントがメッセージを変更する可能性があるため、信頼されていないと考える必要があります。この変更から保護するために、メッセージはデジタル署名で保護されており、この署名は検証されなければなりません。これらの署名をサポートするトラストルートとして機能するのは、共通の認証局です。

署名の話題はすぐに奥が深くなるので、ここでは詳しく説明しません。SAML仕様はW3C勧告XML Signature Syntax and Processingに依存しており、これは興味深いものでしょう。 [^4]

@row
## Terminology

Please see also the terminology in the IDPro Body of Knowledge article, “IAM Reference Architecture.”

|     |     |
| --- | --- |
| **Item** | **Definition** |
| User Agent | A user agent is any software that retrieves, renders, and facilitates end-user interaction with Web content. [^5] |

@column
## 用語解説

IDPro Body of Knowledgeの記事「IAM Reference Architecture」もご参照ください。

|     |     |
| --- | --- |
| **用語** | **定義** |
| ユーザーエージェント | ユーザーエージェントは、Webコンテンツを取得し、レンダリングし、エンドユーザーとインタラクションすることを用意にするソフトウェアです。 [^5] |

@row
## Use Case

@column
## ユースケース

@row
### Summary

The web user works through a user agent to access resources at an RP. The access request results in a redirection of the user to an IDP as part of an authentication action. This result of the authentication is an authentication assertion that is consumed by the RP and used to establish a security context for the web user. In effect, the RP has delegated the authentication to the IDP.

@column
### サマリ

ウェブユーザーは、ユーザーエージェントを介してRPのリソースにアクセスします。アクセス要求は、認証アクションの一部として、ユーザーをIDPにリダイレクトさせます。この認証の結果は、RPによって利用される認証アサーションであり、Webユーザのセキュリティコンテキストを確立するために使用されます。

@row
### Architecture Types

Different architecture types are defined in the “Introduction to IAM Architecture” article in the IDPro Body of Knowledge. The SAML-based authentication use case applies specifically to the architecture of Cloud Environments. [^6]

@row
### アーキテクチャタイプ

IDPro Body of Knowledgeの「Introduction to IAM Architecture」では様々なアーキテクチャタイプが定義されています。SAMLベース認証のユースケースは特にクラウド環境のアーキテクチャに適用されます。 [^6]

@row
### Actors

The user is the only actor. The user acts through the User Agent (the browser). The other participants in the use-case are systems “actors”, which we show as components.

@column
### アクター

ユーザーは唯一のアクターです。ユーザーはユーザエージェント（ブラウザ）を通じてアクションをおこします。ユースケースの他の参加者は、システムの「アクター」であり、ここではコンポーネントとして示しています。

@row
### Components

The following components are defined in the article, “IAM Reference Architecture.” [^7]

*   Audit Repository
    
*   AuthN / Assertion (part of IDP)
    
*   Identity Register
    
*   Relying Party (RP)
    
*   Trust Root
    

Please note that the SAML documents refer to the relying party as the service provider.

@column
### コンポーネント

以下のコンポーネントは「IAM Reference Architecture」の記事で定義されています。 [^7]

*   監査リポジトリ
    
*   AuthN／アサーション（IDPの一部）
    
*   アイデンティティレジスタ
    
*   リライングパーティ（RP）
    
*   トラストルート
    

SAML仕様ではリライングパーティをサービスプロバイダーと呼称することに注意してください。

@row
### Assumptions

The user wishes to access a protected resource and has requested access via a web browser, the User Agent.

The RP has a single IDP. The RP may support several IDPs, so a method to determine which one to use would be needed in that case.

@column
### 想定

ユーザーは保護されたリソースへのアクセスを希望し、ユーザーエージェントであるWebブラウザを介してアクセスを要求しています。

RPはただ1つのIDPを持ちます。RPは複数のIDPをサポートする可能性があり、その場合、どのIDPを使用するかを決定する方法が必要です。

@row
### Preconditions

There must be an established trust between the RP and the IDP before SAML can be used for authentication. “The primary mechanism is for the relying party and asserting party to have a pre-existing trust relationship which typically relies on a Public Key Infrastructure (PKI). While SAML does not mandate using a PKI, it is recommended.” [^8]

The IDP and the RP use the same user identifiers. The SAML specification establishes ways to map these, but we don’t discuss this subject here.

@column
### 事前条件

SAMLを認証に利用する前に、RPとIDPの間に信頼関係が確立されている必要があります。「主なメカニズムは、リライングパーティとアサーションパーティが既存の信頼関係を持つことであり、通常は公開鍵基盤（PKI）に依存します。PKIの使用はSAMLによって義務付けられてはいないが、推奨されています。」 [^8]

IDPとRPは、同じユーザー識別子を使用しています。SAML仕様では、これらをマッピングする方法を確立しているが、これについては説明しません。

@row
### Postconditions

The user is logged into the RP’s site.

@column
### 事後条件

ユーザーがRPのサイトにログインします。

@row
### Basic Course of Events

The following shows the “happy path”, without errors. See also the sequence diagram below. See Alternative Paths for some variations.

1.  The user selects the login function on the RP’s site. This selection may be automatic when the user attempts to access the protected resource.
    
2.  RP determines that the user is not logged in.
    
3.  The RP prepares an Authentication Request message, which the RP may sign. It is delivered to the user agent as a form targeted at the IDP, which is known since there is a single configured IDP. The user agent (automatically via a client-side script) sends the request to the IDP.
    
4.  The IDP ensures the signing certificate from the RP is still valid by checking for revocation.
    
5.  The IDP validates the request and interprets its contents. The signature and some field values (such as Issuer, AuthnContextClassRef, etc.) are checked.
    
6.  The IDP interacts with the user agent to gather the user’s identifier and credentials. For example, this could ask for a username and password, but it could be something else.
    
7.  The IDP uses its Identity Register to validate the credentials.
    
8.  The IDP prepares a Response message, which the IDP signs.
    
9.  The response is then sent back to the user agent with instructions to use an HTTP POST to forward it to the RP. (The target RP URL is typically known to the IDP through initial configuration).
    
10.  The RP ensures the signing certificate from the IDP is still valid by checking for revocation.
    
11.  The RP validates the response and interprets its contents. The signature **must** be checked. The RP checks it against the already active assertions to prevent replay and makes other checks. The RP then determines whether the authentication was successful.
    
12.  Not shown in the chart are the audit records being written. The various components should write these.
    

@column
### イベントの基本的な流れ

以下では、エラーの発生しない「ハッピーケース」を示します。また、下記のシーケンス図も合わせて参照してください。一部のバリエーションには[その他の流れ](#その他の流れ)を参照してください。

1.  ユーザーはRPのサイトでログイン機能を選択します。この選択は、ユーザーが保護されたリソースにアクセスしようとするときに自動的に発生する可能性があります。
    
2.  RPがユーザーがログインしていないと判断します。
    
3.  RPは、おそらくRPが署名した認証リクエストメッセージを用意します。これはIDPを対象とする形式でユーザーエージェントに送信されます。IDPは1つしか設定されていないため、既知です。ユーザーエージェントは（クライアントサイドのスクリプトを経由して自動的に）IDPにリクエストを送信します。
    
4.  IDPは、RPから送られてきた署名付き証明書が失効しているかを検証することで、まだ有効であることを確認します。
    
5.  IDPはリクエストを検証し、内容を解釈します。署名といくつかのフィールド（発行者、AuthnContextClassRef等）の値をチェックします。
    
6.  IDPはユーザーエージェントと連携してユーザーの識別子とクレデンシャルを収集します。例えばユーザー名とパスワードを要求する、もしくは他のものであるかもしれません。
    
7.  IDPはアイデンティティレジスターを利用し、クレデンシャルを検証します。
    
8.  IDPはレスポンスメッセージを用意し、署名します。
    
9.  そして、このレスポンスは、HTTP POSTを使ってRPにフォワードされるように指定してユーザーエージェントに送り返されます（通常、初期設定によってIDPは対象RPのURLを知っています）。
    
10.  RPは、IDPから送られてきた署名付き証明書が失効しているかを検証することで、まだ有効であることを確認します。
    
11.  RPはレスポンスを検証し、その内容を解釈します。この署名はチェック **しなければなりません** 。RPは、再利用を防ぐために既にアクティブなアサーションに対してチェックをおこない、そのほかのチェックをおこないます。そして、RPは認証が成功したがどうかを判断します。
    
12.  図には示していませんが、監査記録は出力されています。様々なコンポーネントが監査記録を書き込む必要があります。
    

@row
### Alternative Paths

Step 3 may be replaced with an HTTP redirect. This formulation is an allowed composition of the POST binding and the Redirect binding. [^9]

There are also alternatives to the POST method in step 3. [^10]

In SAML terms, this is the service provider-initiated variant. There is also an IDP-initiated alternative.

The messages may be encrypted. For instance, in step 8, the IDP may encrypt, and in step 10, the RP would need to decrypt the response.

Not recommended: some implementations have ignored request signing and signature verification, possibly due to historical performance issues.

@column
### その他の流れ

ステップ3はHTTPリダイレクトに置換することができます。これはPOSTバインディングとリダイレクトバインディングの許可された構成です。 [^9]

また、ステップ3のPOSTメソッドに対して代替手段があります。 [^10]

SAML用語では、これはサービスプロバイダによって開始されたバリアントです。また、IDPによって開始される別の方法もあります。

メッセージは暗号化されている場合があります。例えば、ステップ8においてIDPは暗号化をおこなう可能性があり、ステップ10でRPはレスポンスを復号する必要があります。

非推奨：一部の実装では、過去のパフォーマンス上の問題を原因とするであろう、リクエストの署名と署名検証を無視することがあります。

@row
### Exception Paths

Failure to authenticate at the IDP does not return an assertion.

Failure to validate the signature indicates that the assertion should not be honored.

Various error conditions, such as the validity period expiring, are described in the standard.

@column
### 例外の流れ

IDPでの認証失敗はアサーションを返却しません。

署名検証に失敗すると、アサーションが受け入れられないことを示します。

有効期限切れなど、様々なエラー条件が標準仕様に記載されています。

@row
### Sequence Diagram

![The “happy path” of the Web Browser SSO Profile](/assets/images/idpro_bok/79-image1.png)

_Figure 1: The “happy path” of the Web Browser SSO Profile_

@row
## Author Bio

George Dobbs manages architects at a major insurance company. He is also the chairman of the IDPro Body of Knowledge Committee. One of his interests is modernizing the use of Identity and Access Management techniques used by the firm. He is particularly interested in the area of customer-facing applications, including approaches to fraud prevention in call center and digital contexts. Related to this, he is interested in the evolution of distributed session management – notably distributed session termination. He is a founding member of IDPro and represented his firm in the Identity Ecosystem Steering Group (IDESG). Prior to his current position, he led the development of customer-facing identity for websites at three other insurers. He has led a local identity and access management user group since 2004. Prior to that, he was the chairman of the Network Applications Consortium.

@row
## Acknowledgments

The author would like to express gratitude to Chris Olsen and Bernard Carlier for their review and suggestions for improving this text.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2021-09-30 | V1 published |
| 2022-12-15 | V2 published; title changed, intro and use case summary clarified; Alternate Path includes a “not recommended” |

@row
## References

- - -

[^1]:  Dobbs, George, “IAM Reference Architecture,” IDPro Body of Knowledge, 30 September 2021, [https://bok.idpro.org/article/id/76/](https://bok.idpro.org/article/id/76/) . 
    
[^2]:  “OASIS SAML Wiki – Front Page,” wiki page, OASIS, [https://wiki.oasis-open.org/security/FrontPage#SAML\_V2.0\_Standard](https://wiki.oasis-open.org/security/FrontPage#SAML_V2.0_Standard) (accessed 28 November 2022). 
    
[^3]:  Hughes, John, and Scott Cantor, Jeff Hodges, Frederick Hirsch, Prateek Mishra, Rob Philpott, Eve Maler, eds. “Profiles for the OASIS Security Assertion Markup Language (SAML) V2.0,” OASIS, 15 March 2005, [https://docs.oasis-open.org/security/saml/v2.0/saml-profiles-2.0-os.pdf](https://docs.oasis-open.org/security/saml/v2.0/saml-profiles-2.0-os.pdf) (accessed 28 November 2022). 
    
[^4]:  Bartel, Mark, and John Boyer, Barb Fox, Brian LaMacchia, Ed Simon, “XML Signature Syntax and Processing Version 1.1,” Section: Core Validation, World Wide Web Consortium, 11 April 2013, [https://www.w3.org/TR/xmldsig-core/#sec-CoreValidation](https://www.w3.org/TR/xmldsig-core/#sec-CoreValidation) , (accessed 28 November 2022). 
    
[^5]:  “User Agent Accessibility Guidelines (UAAG) 2.0,” W3C Working Group Note, https://www.w3.org/TR/UAAG20/#glossary (accessed 28 November 2022). 
    
[^6]:  Cameron, Andrew, and Graham Williamson, “Introduction to IAM Architecture,” IDPro Body of Knowledge, 17 June 2020, [https://bok.idpro.org/article/id/38/](https://bok.idpro.org/article/id/38/) (accessed 28 November 2022). 
    
[^7]:  “IAM Reference Architecture,” [https://bok.idpro.org/article/id/76/](https://bok.idpro.org/article/id/76/) . 
    
[^8]:  Ragouzis, Nick, and John Hughes, Rob Philpott, Eve Maler, Paul Madsen, Tom Scavo, “Security Assertion Markup Language (SAML) V2.0 Technical Overview - Committee Draft 02,” OASIS, 25 March 2008, [https://www.oasis-open.org/committees/download.php/27819/sstc-saml-tech-overview-2.0-cd-02.pdf](https://www.oasis-open.org/committees/download.php/27819/sstc-saml-tech-overview-2.0-cd-02.pdf) (accessed 28 November 2022) 
    
[^9]:  Cantor, Scott, and Frederick Hirsch, John Kemp, Rob Philpott, Eve Maler, eds. “Bindings for the OASIS Security Assertion Markup Language (SAML) V2.0,” OASIS, 15 March 2005, [https://docs.oasis-open.org/security/saml/v2.0/saml-bindings-2.0-os.pdf](https://docs.oasis-open.org/security/saml/v2.0/saml-bindings-2.0-os.pdf) (accessed 28 November 2022). 
    
[^10]:  Ibid. 
