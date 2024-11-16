---
layout: columns
title: Federation Simplified (v2)
permalink: /docs/oidc_oauth/idpro_bok/62
date: 2024-09-09
modify_date: 2024-11-13
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "フェデレーション", "SAML", "OpenID Connect", "企業内IAM", "シングルサインオン", "OAuth", "OAuth2.0"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/62/](https://bok.idpro.org/article/id/62/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article describes the fundamentals of enterprise identity federations, focusing on SAML and OpenID Connect (a protocol built on OAuth2.0). It will also contain common scenarios where federations are used and high-level terminology. Academic identity federations are out of scope but are mentioned briefly for comparison. 

Keywords: Federation, SAML, OpenID Connect, Enterprise IAM, Single Sign On, OAuth, OAuth2.0

@column
## 概要

本記事では、SAMLおよび（OAuth2.0の上に構築されたプロトコル）OpenID Connectに焦点を当てながら、企業のアイデンティティフェデレーションの基礎について説明しています。また、フェデレーションが利用される一般的なシナリオと高レベルの用語についての説明も含みます。学術的なアイデンティティフェデレーションについては範囲外であるものの、比較のために簡単に言及します。 

Keywords: フェデレーション, SAML, OpenID Connect, エンタープライズIAM, シングルサインオン, OAuth, OAuth2.0

@row
Patrick Lunney, Product Owner - Single Sign-On & Multi Factor Authentication

Capital One

© 2022 IDPro, Patrick Lunney

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction

This article describes identity federation in the context of single sign-on in enterprises and outlines some use cases for enterprise federation integrations. Enterprises have various ways to manage federation connections: the connections may be full service within the enterprise, self-service with controls in place for governance, or manual integrations. Each integration model has its strengths and weaknesses, which will be discussed in turn below.

@column
## 導入

この記事では、エンタープライズにおけるシングルサインオンの観点からアイデンティティフェデレーションについて説明し、企業におけるフェデレーション統合のいくつかのユースケースの概略を説明します。企業には、フェデレーション接続を管理するためのさまざまな方法があります：接続には、企業内のフルサービスである場合や、ガバナンス統制を備えたセルフサービスであったり、または手動の統合であったりします。各統合モデルには長所と短所があり、以下で順番に説明します。

@row
### Terminology

|     |     |
| --- | --- |
| Term | Definition |
| Identity Federation | An identity federation is a group of computing or network providers that agree to operate using standard protocols and trust agreements. In a **Single Sign-On (SSO)** scenario, identity federation occurs when an **Identity Provider (IdP)** and **Service Provider (SP)** agree to communicate via a specific, standard protocol. The enterprise user will log into the application using their credentials from the enterprise rather than creating new, specific credentials within the application. By using one set of credentials, users need to manage only one credential, credential issues (such as password resets) can be managed in one location, and applications can rely on the appropriate enterprise systems (such as the HR system) to be the source of truth for a user’s status and affiliation.<br><br>Identity federations can take several forms. In academia, **multilateral federations** , where a trusted third party manages the metadata of multiple IdPs and SPs, are fairly common. [^1] This article focuses, however, on the enterprise use case where **bilateral federation** arrangements, where the agreements are one-to-one between an IdP and an SP, are the most common form of identity federation in use today. |
| Bilateral Federation | A bilateral federation is one that consists of only two entities: one **Identity Provider (IdP)** and one **Service Provider (SP)** . This is the most common model for an enterprise identity federation. |
| Identity Provider (IdP) | An Identity Provider (IdP) performs a service that sends information about a user to an application. This information is typically held in a user store, so an identity provider will often take that information and transform it to be able to be passed to the service providers, AKA apps. The OASIS organization, which is responsible for the SAML specifications, defines an IdP as “A kind of SP that creates, maintains, and manages identity information for principals and provides principal authentication to other SPs within a federation, such as with web browser profiles.” [^2] |
| Multilateral Federation | A federation that consists of multiple entities that have agreed to a specific trust framework. There are several forms of multilateral federations, including hub-and-spoke and mesh. Multilateral federations are the most common model for academic identity federations. |
| OAuth 2.0 | OAuth 2.0 is an open-source protocol that allows Resource Owners such as applications to share data with clients by facilitating communication with an Authorization Server. [^3] That data takes the form of credentials given to applications to obtain information/data from other applications. The Authorization Server is usually the Identity Provider (IdP). The Authorization Server (AS) may provide authorization directly or indirectly. For example, the AS may supply attributes or profile data of the Resource Owner or provide access to data that can later be used for authorization purposes, such as entitlements from an Identity Management or Governance Solution. |
| OpenID Connect | OpenID Connect is a simple identity layer on top of the OAuth 2.0 protocol. It enables Clients to verify the identity of the End-User based on the authentication performed by an Authorization Server, as well as to obtain basic profile information about the End-User in an interoperable and REST-like manner. |
| Security Assertion Markup Language (SAML) | SAML is an XML-based communication protocol between SPs and IdPs. [^4] Usually, the enterprise hosts the IdP, whereas applications (including cloud services) are the SPs. |
| Service Provider (SP) | Defined by the OASIS organization, which is responsible for the SAML specification, as “A role donned by a system entity where the system entity provides services to principals or other system entities.” This usually takes the form of an application that offers services requiring authentication and authorization to a user. |
| Single Sign-On | Single Sign-On is a service that enables SPs to verify the identities of **End Users** by facilitating communication with IdPs. SSO acts as a bridge to decouple SPs and IdPs. This can happen via numerous protocols such as agent-based integrations, direct LDAP integration, SAML, and OpenID Connect, to name a few. |

@column
### 用語解説

|     |     |
| --- | --- |
| 用語 | 定義 |
| アイデンティティフェデレーション |  アイデンティティフェデレーションは、標準プロトコルと信頼合意を使用して運用することに同意しているコンピューティングプロバイダーまたはネットワークプロバイダーのグループです。 **シングルサインオン（SSO）** シナリオでは、 **アイデンティティプロバイダ（IdP）** と **サービスプロバイダ（SP）** が特定の標準プロトコルを介して通信することに同意したときに、アイデンティティフェデレーションが発生します。企業ユーザーは、アプリケーション内で新しい特定のクレデンシャルを作成するのではなく、企業のクレデンシャルを使用してアプリケーションにログインします。1セットのクレデンシャルを使用することにより、ユーザーは1つのクレデンシャルのみを管理する必要があり、クレデンシャルの問題（パスワードのリセットなど）は1箇所で管理でき、アプリケーションはユーザーのステータスや所属に関する信頼できる唯一の情報源として適切な企業システム（人事システムなど）に依存することができます。<br><br>アイデンティティフェデレーションはいくつかの形式をとれます。学術的には、信頼できる第三者が複数のIdPおよびSPのメタデータを管理する **多者間フェデレーション** がかなり一般的です。 [^1] しかし、この記事では、IdPとSPの間で1対1の契約を結ぶ **二者間フェデレーション** が現在最も一般的に使用されているエンタープライズ・ユースケースに焦点を当てます。 |
| 二者間フェデレーション | 二者間フェデレーションは、1つの **アイデンティティプロバイダー（IdP）** と1つの **サービスプロバイダ（SP）** の2つのエンティティのみで構成されるものです。これは、企業のアイデンティティフェデレーションとしては最も一般的なモデルです。 |
| アイデンティティプロバイダー（IdP） | アイデンティティプロバイダー（IdP）は、ユーザーに関する情報をアプリケーションに送信するサービスを運用します。この情報は通常、ユーザーストアに保持されるため、アイデンティティプロバイダーはその情報を取得し、サービスプロバイダー（またはアプリ）に渡すことができるように変換することが多くあります。SAMLの仕様を所管するOASISという組織では、IdPを「主体者のアイデンティティ情報を作成、維持、管理し、Webブラウザプロファイルなど、フェデレーション内の他のSPに主体者認証を提供するSPの一種」と定義しています。 [^2] |
| 多者間フェデレーション | 特定のトラストフレームワークに合意した複数のエンティティで構成されるフェデレーション。複数フェデレーションには、ハブ・アンド・スポークやメッシュなど、いくつかの形態があります。多者間フェデレーションは、学術のアイデンティティフェデレーションで最も一般的なモデルです。 |
| OAuth 2.0 | OAuth 2.0はオープンソースのプロトコルであり、アプリケーションのようなリソースオーナーが認可サーバーとの通信を促進することでクライアントとデータを共有できるようにするものです。 [^3] そのデータは、他のアプリケーションから情報/データを取得するためにアプリケーションに与えられるクレデンシャルの形式をとります。認可サーバーは通常、アイデンティティプロバイダー（IdP）です。認可サーバー（AS）は、直接または間接的に認可を提供することができます。たとえば、ASはリソースオーナーの属性またはプロファイルデータを提供したり、アイデンティティ管理またはガバナンスソリューションからの権限など、後で認可の目的に使用できるデータへのアクセスを提供したりすることができます。 |
| OpenID Connect | OpenID Connectは、OAuth 2.0プロトコル上のシンプルなアイデンティティレイヤーです。これにより、クライアントは認可サーバーによって実行された認証に基づいてエンドユーザーのアイデンティティを検証できるようになり、また相互運用可能でRESTに似た方法でエンドユーザーの基本プロファイル情報を取得することができるようになります。 |
| Security Assertion Markup Language (SAML) | SAMLとはSPとIdP間のXMLベースの通信プロトコルです。 [^4] 通常、企業がIdPをホストし、アプリケーション（クラウドサービスを含む）がSPとなります。 |
| サービスプロバイダー（SP） | SAML仕様を所管するOASISによる定義では、「あるシステムエンティティが、主体または他のシステムエンティティにサービスを提供する際に負う役割」と定義されています。これは通常，ユーザーに認証と認可を必要とするサービスを提供するアプリケーションの形をとります。 |
| シングルサインオン | 	シングルサインオンは、SPがIdPとの通信を円滑にすることで、 **エンドユーザー** のアイデンティティを検証できるようにするサービスです。SSOは、SPとIdPを切り離して利用するための橋渡し役として機能します。これは、エージェントベースの連携、LDAPの直接連携、SAML、OpenID Connectなど、数多くのプロトコルを介して実現することができます。 |

@row
### Exploring Identity Federation in the Enterprise

There are several common scenarios where an identity practitioner is likely to encounter identity federation in an enterprise context. This section explores the most common protocols, OpenID Connect, and SAML.

@column
### Exploring Identity Federation in the Enterprise

アイデンティティ実践者がエンタープライズにおけるアイデンティティフェデレーションに遭遇する可能性が高い一般的なシナリオがいくつかあります。このセクションでは、最も一般的なプロトコルであるOpenID ConnectとSAMLについて説明します。

@row
### Use Case 1: SAML

@column
### ユースケース1：SAML

@row
![Screenshot of a common Single Sign-On interface.](/assets/images/idpro_bok/Figure1.jpg)

_Figure 1 - Example of a Single Sign-On User Interface_

@row
SAML is most often found in SaaS (Software as a Service) applications. An application is purchased or created by an enterprise to do "something" and employees need to log into the application. The application will need to exchange information with the enterprise to form this federation. Usually, an IdP (the enterprise) and an SP (the app) will exchange metadata, allowing them to set up the connections in the SSO system. Metadata exchange can be done manually, but that often takes time and can cause headaches for IdPs and SPs.

See Appendix Item 1 for an example of a metadata file from an IdP. In that example, the IdP operator will give this metadata to the SP operator. The SP can then input this information manually (or import it, depending on their SSO platform) into their SSO system to allow the enterprise's users to sign in to the application using their SSO accounts. The IdP operator will need to do the same, either by importing an SP metadata file or manually updating the configuration of the IdP.

An IdP metadata file contains the enterprise's entityID, the various URLs used in SAML, and the attributes that will be passed in the SAML assertion (the data that is passed to the app). An entity ID is a unique name for a SAML entity, both an IdP and an SP. No two IdPs or SPs can share the same entityID.

Think of a SAML assertion as a voucher or ticket. The IdP gives the user a voucher to the user to get into the SP, and the SP is validating the voucher using certificate validation. After the voucher is validated, the SP will look at the attributes to see what the user can do. For example, in Appendix Item 2, you can see a user's username and email address were passed to this SP.

For more information on the details of SAML assertions and components, see the SAML specification and associated supporting documents. [^5]

One last piece of information regarding enterprise SAML federations: there are two different types of URLs for applications. Sometimes it is the SP’s URL, for example, ‘https://myhrapp.com/enterprise’. This is known as an SP-initiated request. Other times, the IdP will initiate the request. For example, ‘https://authn.enterprise.com/idp/SAML20=myhrapp’. In both cases, the user will be logging into the same app tenant for the enterprise. Some applications only support IdP-initiated login requests. Some applications only support SP-initiated requests.

Here is a diagram flow of a standard SAML authentication:

@column
SAMLは、SaaS（Software as a Service）アプリケーションで最もよく見られます。アプリケーションは、企業が「何か」をおこなうために購入または作成され、従業員はアプリケーションにログインする必要があります。アプリケーションは、このフェデレーションを形成するために企業と情報を交換する必要があります。通常、IdP（エンタープライズ）とSP（アプリ）はメタデータを交換し、SSOシステムで接続をセットアップできるようにします。メタデータの交換は手動でおこなうことができますが、多くの場合、時間がかかり、IdPとSPの頭痛の種になる可能性があります。

IdPからのメタデータファイルの例についてはAppendixのItem1を参照してください。この例では、IdP運用者がこのメタデータをSP運用者に渡します。SPは、この情報を手動で入力（またはSSOプラットフォームに応じてインポート）してSSOシステムに入力し、企業のユーザーがSSOアカウントを使用してアプリケーションにサインインできるようにします。IdP運用者は、SPメタデータファイルをインポートするか、IdPの構成を手動で更新することによって、同じことをおこなう必要があります。

IdPメタデータファイルには、企業のエンティティID、SAMLで使用されるさまざまなURL、およびSAMLアサーションで渡される属性（アプリに渡されるデータ）が含まれています。エンティティIDは、SAMLエンティティ、IdPとSPの両方で、の一意の名前です。2つのIdPまたはSPが同じエンティティIDを共有することはできません。

SAMLアサーションは、バウチャーまたはチケットと考えてください。IdPは、SPに入るためのバウチャーをユーザーに渡し、SPは証明書の検証を使用してバウチャーを検証します。バウチャーが検証されると、SPは属性を調べて、ユーザーが実行できる操作を確認します。たとえば、AppendixのItem2では、ユーザーのユーザー名とメールアドレスがこのSPに渡されたことがわかります。

SAMLアサーションおよびコンポーネントの詳細については、SAML仕様および関連するサポート文書を参照してください。 [^5]

エンタープライズSAMLフェデレーションに関する最後の情報です：アプリケーションには2つの異なるタイプのURLがあります。SPのURLであることもあり、例えば「https://myhrapp.com/enterprise」など。これは、SP-initiatedリクエストと呼ばれます。それ以外の場合は、IdPがリクエストを開始します。たとえば、「https://authn.enterprise.com/idp/SAML20=myhrapp」のように。どちらの場合も、ユーザーは企業の同じアプリテナントにログインします。一部のアプリケーションは、IdP-initiatedログインリクエストのみをサポートします。一部のアプリケーションは、SP-initiatedリクエストのみをサポートします。

標準のSAML認証のフローを次に示します：

@row
![Sequence Diagram for a SAML authentication flow, including the IdP, user Agent, and Service Provider. ](/assets/images/idpro_bok/Figure2.jpg)

_Figure 2 - SAML Authentication Flow_

@row
It should be noted that the _authentication_ of the user is completed at step 5; the IdP has validated the user's credentials and is now passing the SAML assertion back to the browser. Federation is completed at step 7; the browser forwards the assertion to the application so that the application can know the user has been authenticated and create a session for that user. In steps 8 and 9, that is where _authorization_ takes place. Based on the information provided by the IdP, the application will allow or deny the user access to certain parts of the application.

@column
特筆すべきは、ユーザーの __認証__ はステップ5で完了しています；IdPはユーザーのクレデンシャルを検証し、SAMLアサーションをブラウザに返しています。フェデレーションはステップ7で完了します；ブラウザはアサーションをアプリケーションにフォワードすることで、アプリケーションはユーザーが認証されたことを認識し、そのユーザーのセッションを作成します。ステップ8と9では、 __認可__ がおこなわれます。IdPによって提供される情報に基づいて、アプリケーションはアプリケーションの特定の部分へのユーザーのアクセスを許可または拒否します。

@row
### Use Case 2: OpenID Connect

Another common type of identity federation is internal to the enterprise and increasingly found in SaaS offerings. Previously, enterprises would use "agents," which they would install on web servers hosting applications. The agents would communicate with something called a policy server to determine what a user could do, if anything at all. That agent/policy server technology is old and not used as much in enterprises anymore.

Instead, a popular protocol that is increasingly being used is OpenID Connect. OpenID Connect is newer than SAML and based on the OAuth2.0 protocol; most in-house enterprise apps are based on APIs and microservices, which is why OIDC is favored. [^6] It should be noted that some SaaS applications do support OpenID Connect.

OpenID Connect uses the authorization\_code grant type of OAuth2.0. It is important to note that OpenID Connect is meant to share user attributes, so it will be the only part of OAuth2.0 in this document. There are many other grant\_types in OAuth2.0 which authenticate users or clients in different ways but are not part of user _authentication_ and _authorization_ and are outside the scope of this document.

@column
### ユースケース2：OpenID Connect

もう1つの一般的なアイデンティティフェデレーションは企業内部のもので、SaaS製品に見られることが多くなっています。以前は、企業はアプリケーションをホストするWebサーバーにインストールする「エージェント」を利用していました。エージェントは、ポリシーサーバーと呼ばれるものと通信し、もし可能であればユーザーができることを決定します。このエージェント／ポリシーサーバーの技術は古く、企業ではもうあまり使われていません。

その代わり、普及が進んでいるのがOpenID Connectというプロトコルです。OpenID ConnectはSAMLよりも新しく、OAuth2.0プロトコルに基づきます；企業内アプリケーションの多くはAPIやマイクロサービスに基づいており、これがOIDCが支持される理由です。 [^6] 特筆すべきことに、一部のSaaSアプリケーションはOpenID Connectをサポートしています。

OpenID Connectは、OAuth2.0のauthorization\_codeグラントタイプを使用します。OpenID Connectはユーザー属性を共有するためのものなので、このドキュメントではOAuth2.0の部分のみを扱うことにします。OAuth2.0には他にも多くのgrant\_typeがあり、さまざまな方法でユーザーやクライアントを認証しますが、これはユーザー __認証__ や __認可__ の一部ではないため、このドキュメントの範囲外です。

@row
#### Authorization\_Code Flow

The authorization\_code grant type is explained in the OAuth2.0 spec. [^7] OpenID Connect 1.0 is based on this flow. An important consideration to note involves the scopes in OpenID Connect: they must contain openid (and most often include profile). Here is a diagram of that authorization\_code flow: [^8]

@column
#### Authorization\_Codeフロー

authorization\_codeのグラントタイプはOAuth2.0仕様で説明されています。 [^7] OpenID Connect 1.0は、このフローに基づいています。OpenID Connectにおいて重要な考慮事項はスコープを含んでいることです：openidが含まれていなければなりません（そして多くの場合、profileも含まれています）。以下は、そのauthorization\_codeフローの図です： [^8]

@row
![A diagram of the OAuth 2.0 authorization_grant flow](/assets/images/idpro_bok/Figure3.jpg)

_Figure 3 - OAuth 2.0 authorization\_grant Flow_

@row
In this diagram, we can see that the user will first go to a browser (user agent) and initiate a request against the authorization server. The authorization server will then prompt the user to enter their credentials (B). After collecting the credentials, the browser will send that information to the authorization server, which then will respond with a code to the browser (C). The backend of the application (Client, C) will take that code and exchange it for an access token (D, E). In OpenID Connect, there is an optional step F in which the client may request additional information about the user (attributes) by making an API request against a ‘userinfo’ endpoint. With this API request, the AS will return the user's information allowing the client to _authorize_ the user.

To see the API calls, please see Appendix Item 3.

@column
この図では、ユーザーはまずブラウザ（ユーザエージェント）にアクセスし、認可サーバーに対してリクエストを開始することがわかります。認可サーバーは、ユーザーにクレデンシャルを入力するように促します（B）。クレデンシャルを収集した後、ブラウザはその情報を認可サーバーに送信し、認可サーバーはブラウザにコードで応答します（C）。アプリケーションのバックエンド（Client, C）はそのコードを受け取り、アクセストークンに交換します（D, E）。OpenID Connectでは、オプションのステップFがあり、クライアントは「userinfo」エンドポイントに対してAPIリクエストを実行することで、ユーザーに関する追加情報（属性）をリクエストすることができます。このAPIリクエストにより、認可サーバーはユーザーの情報を返し、クライアントはそのユーザを __認可する__ ことができます。

APIコールを見るには、Appendix Item3を参照してください。

@row
## Challenges in Enterprise Federations

@column
## 企業内フェデレーションの課題

@row
### When to Use SAML versus OpenID Connect

@column
### SAML対OpenID Connectでどちらを使うか

この質問に対する短い答えは、「場合による」です。SPができることに制限があり、IdPも同様です。両者に長所と短所があるため、実際にはIdPとSPの間の選択（または制限）の問題に過ぎません。 [^9]

Pamela DingleによるIDPro Body of Knowledgeの記事「[Introduction to Identity - Part 2: Access Management](../45/)」は、認証およびアクセス制御ツールの進化について興味深い見方を示しています。 [^10] 特に、「モバイルとAPIの革新がOAuthと委任型認可フレームワークをもたらした」というセクションでは、SAMLの存在にもかかわらずOAuthの開発につながった進化について、興味深い洞察を示しています。

@row
### Attributes - Data and Formatting

Applications require different names for attributes. Sometimes an attribute must be called firstname, where other applications may need firstName, or perhaps even givenName. This can cause issues, as the application might not be able to pick up the attribute in the SAML Assertion / userinfo endpoint it needs to authorize the user. This is where the IdP and SP need to collaborate to determine how the attributes should be sent. In some enterprises, the attribute names do not change; the enterprise forces the application to adopt its formatting of the attribute. Other times, the application forces the IdP to change the attributes. There is also something called attribute mapping which can take place. Most SAML and OpenID Connect plugins allow this to take place in attribute mapping files, like Shibboleth. [^11] The IdP will send attributes, and upon receiving them, the SP can transform them into the correct format.

@column
### 属性 - データとフォーマット

アプリケーションは、属性について異なる名称を要求します。ある属性がfirstnameという名称でなければならないことがありますが、他のアプリケーションではfirstNameやgivenNameという名称でなければならないこともあります。この場合、アプリケーションは、ユーザーを認可するために必要な SAMLアサーション/userinfoエンドポイントにその属性を取り込むことができないので、問題が発生する可能性があります。そこで、IdPとSPが協力して、属性をどのように送信すべきかを決定する必要があります。企業によっては、属性名は変更されず、企業はアプリケーションにその属性のフォーマットを採用させることがあります。また、アプリケーションがIdPに属性を変更するよう強制する場合もあります。また、属性マッピングと呼ばれるものがおこなわれることもあります。ほとんどのSAMLやOpenID Connectプラグインでは、Shibbolethのような属性マッピングファイルでこれをおこなうことができます。 [^11] IdPが属性を送信し、それを受け取ったSPが正しい形式に変換することができます。

@row
### Assertion Sizing

Quite a bit of information can be passed to SPs, and the assertion can become so large that it will break the SP. This is somewhat common when applications authorize users via Active Directory or LDAP groups (also known as SID bloat, essentially a large data blob of information about the user), and the IdP sends an array of all Active Directory groups. The SAML assertion will contain so much information that the SP will not be able to parse it out, and the user will not be able to get into the application. Resolving this issue often requires custom integrations, where there needs to be a special configuration within the IdP to manage assertions for that single application. Additionally, assertion sizes can be limited based on web servers, browsers, and even proxies. This problem can be alleviated via identity governance processes that limit the number of Active Directory groups and removes memberships no longer required.

@column
### アサーションのサイズ設定

SPにはかなりの量の情報が渡され、アサーションが大きくなりすぎてSPが壊れてしまうこともあります。これは、アプリケーションがActive DirectoryまたはLDAPグループ（SIDの肥大化とも呼ばれ、基本的にユーザーに関する情報の大きなデータの塊）を介してユーザーを認可し、IdPがすべてのActive Directoryグループの配列を送信する場合によくあることです。SAMLアサーションには非常に多くの情報が含まれるため、SPはそれを解析できず、ユーザーはアプリケーションにアクセスできなくなります。この問題を解決するには、多くの場合、カスタム統合が必要であり、IdP内にその単一アプリケーションのアサーションを管理するための特別な構成が必要です。さらに、アサーションのサイズは、Webサーバー、ブラウザおよびプロキシによって制限されることがあります。この問題は、Active Directoryのグループ数を制限し、不要になったメンバーシップを削除するアイデンティティガバナンスプロセスによって軽減することができます。

@row
### Cross-Origin Resource Sharing (CORS)

Cross-Origin Resource Sharing, commonly known as CORS, causes issues in many enterprises. CORS is a standard that allows a server to relax the same-origin policy. [^12] Usually, an API call from one application cannot be returned to a separate application. For example, if I make a request to application1.com/api, I would expect the request to come back to me and not be sent to application2.com/api. These are two different domains and application1.com could potentially be sending malicious data to application2.com.

CORS is used to explicitly allow some cross-origin requests while rejecting others. For example, if a site offers an embeddable service, it may be necessary to relax certain restrictions. If I attempt to load application1.com, and that application requires resources from application2.com, my browser will make that request through application1.com into application2.com, thus making it a cross-domain API call. CORS allows the request to pass through and retrieve information so I can visit the application.

Setting up such a CORS configuration is a challenge. It is also potentially not secure. What most IdPs can do is relax their policies to allow sharing between top-level domains, for example, \*.enterprise.com or \*.partner.com. This way, there will be no restrictions on the origin of requests. [^13]

@column
### Cross-Origin Resource Sharing（CORS）

一般的にCORSとして知られているオリジン間リソース共有は、多くの企業で問題を引き起こします。CORSは、サーバーに同一オリジンポリシーを緩和することを許可する標準仕様です。 [^12] 通常、あるアプリケーションからのAPI呼び出しは別のアプリケーションに戻ることはできません。例えば、私がapplication1.com/apiに対するリクエストを送信した場合、リクエストは私に返ってきて、application2.com/apiには送信されないことを期待するでしょう。これら2つは異なるドメインであり、application1.comは悪意のあるデータをapplication2.comに送信している可能性があります。

CORSは一部のオリジン間リクエストを明示的に許可し、それ以外を拒否するために利用されます。例えば、サイトが埋め込み可能なサービスを提供しているとき、特定の制限を緩和する必要がある場合があります。application1.comを読み込もうとし、そのアプリケーションがapplication2.comからのソースを必要とする場合、ブラウザはapplication1.comからapplication2.comへのリクエストを送るため、オリジン間API呼び出しをおこなうことになります。CORSはリクエストの送信、情報の取得を許可することで、アプリケーションへのアクセスを可能にします。

このようなCORS設定をおこなうことは困難です。また、潜在的にセキュアではありません。ほとんどのIdPでできることは、例えば\*.enterprise.comや\*.partner.comのように、トップレベルドメイン間での共有を許可するポリシーに緩めることです。この場合、リクエストのオリジンに制限がなくなります。 [^13]

@row
## Conclusion

This document is a high-level review of application federations in the enterprise. The most common protocols used are SAML and OpenID Connect. Both are widely used today in the enterprise world as well as the consumer world as well. When you see this screen:

@column
## 結論

このドキュメントでは、企業内でのアプリケーションフェデレーションをおおまかにまとめました。最も一般的に利用されるプロトコルは、SAMLとOpenID Connectです。今日では両方とも企業内だけでなく、コンシューマーでも広く利用されています。このような画面を見たとき：

@row
![Screenshot of a common login screen using social networks](/assets/images/idpro_bok/Figure4.jpg)

_Figure 4 - Sample Social Login Screen_

@row
you are actually selecting the IdP you'd like to sign into the SP with. You also have the ability (in most cases) to sign up in the app directly. One thing to note, when you do sign in to an application using an Identity Provider such as social media sites, you are passing information about yourself, the same way your enterprise passes information about you to SPs in the enterprise. On social networks, it is important to understand the terms and conditions of what can be done with this data. In enterprise applications, this is usually done by legal teams to ensure there will be no data exfiltration.

With more and more applications becoming SaaS applications, enterprises are creating more and more federations. With that, there will continue to be innovations in the single sign-on community to make them safer, such as adding multifactor authentication into the flow.

@column
SPにサインインするときに使いたいIdPを選択しています。また、（ほとんどのケースで）アプリケーションに直接サインアップする機能を使っています。ひとつ覚えておくこととして、ソーシャルメディアサイトのようなアイデンティティプロバイダーを使ってアプリケーションにサインインするとき、企業が自分の情報を企業内のSPに提供しているときと同じ方法で自分の情報を提供していることに注意してください。ソーシャルネットワークでは、そのデータを使って何ができるかという条件を理解することが重要です。エンタープライズアプリケーションでは、一般的に法務チームによって、データ流出が起きないようにします。

ますますアプリケーションがSaaSアプリケーションとなっていくことで、企業はさらにフェデレーションを作成していきます。これにより、フローに多要素認証を追加するなどシングルサインオンコミュニティをさらに安全にするようなイノベーションが継続されるでしょう。

@row
## Author Bio

My name is Patrick Lunney. I have managed/owned identity providers in two fortune 50 companies over the past eight years. In that time, I've worked with 100s of SaaS applications as well as in-house applications to ensure federations are set up securely and properly. Currently, I am the product owner for Capital One's internal workforce Single Sign-On and Multi Factor Authentication products. All applications in our enterprise must use either OpenID Connect or SAML for SSO, with very few exceptions. I have held this role since July of 2019.

@row
## Change Log

|     |     |
| --- | --- |
| Date | Change |
| 2022-06-03 | V2 published; Changed title, updated OIDC definition, added detail re: SP-initiated flows |
| 2021-04-19 | V1 published |

@row
## Appendix:

@row
### Item 1: SAML Request

```
<md:EntityDescriptor xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata" ID="mzWO1kVu-dAmFIdmN.08s9bOaCH" cacheDuration="PT1440M" entityID="IdProvider">

<md:IdPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol" WantAuthnRequestsSigned="false">

<md:KeyDescriptor use="signing">

<ds:KeyInfo xmlns:ds="http://www.w3.org/2000/09/xmldsig#">

<ds:X509Data>

<ds:X509Certificate>

</ds:X509Certificate>

</ds:X509Data>

</ds:KeyInfo>

</md:KeyDescriptor>

<md:NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified</md:NameIDFormat>

<md:SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Location="https://authn.enterprise.com/idp/SSO.saml2"/>

<md:SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://authn.enterprise.com/idp/SSO.saml2"/>

<saml:Attribute xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" Name="firstname" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:unspecified"/>

<saml:Attribute xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" Name="groups" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:unspecified"/>

<saml:Attribute xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" Name="lastname" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:unspecified"/>

<saml:Attribute xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" Name="userid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:unspecified"/>

<saml:Attribute xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" Name="email" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:unspecified"/>

</md:IdPSSODescriptor>

<md:ContactPerson contactType="administrative"/>

</md:EntityDescriptor>
```

@row
### Item 2: SAML Response

```
<samlp:Response Destination="https://serviceprovider.com/acs"

ID="HpiyLr_zVMK.jxdUHXxRvjJ8Fwy" IssueInstant="2020-11-24T01:53:06.809Z" Version="2.0"

xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">

<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">IDprovider</saml:Issuer>

<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">

<ds:SignedInfo>

<ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>

<ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"/>

<ds:Reference URI="#HpiyLr_zVMK.jxdUHXxRvjJ8Fwy">

<ds:Transforms>

<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>

<ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>

</ds:Transforms>

<ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"/>

<ds:DigestValue>PwJICHFA1QIlML2p5MyJaRib5TDY4TWj5J7IEAjn1Yo=</ds:DigestValue>

</ds:Reference>

</ds:SignedInfo>

<ds:SignatureValue> Signature

</ds:SignatureValue>

<ds:KeyInfo>

<ds:X509Data>

<ds:X509Certificate>

</ds:X509Certificate>

</ds:X509Data>

<ds:KeyValue>

<ds:RSAKeyValue>

<ds:Modulus>

</ds:Modulus>

<ds:Exponent>AQAB</ds:Exponent>

</ds:RSAKeyValue>

</ds:KeyValue>

</ds:KeyInfo>

</ds:Signature>

<samlp:Status><samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>

</samlp:Status>

<saml:Assertion ID="bJUFiJZEXV0rDgdTh9HnF2CbrIq" IssueInstant="2020-11-24T01:53:07.104Z"

Version="2.0" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">

<saml:Issuer>IDprovider</saml:Issuer>

<saml:Subject>

<saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:entity">ztl593</saml:NameID>

<saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer"><saml:SubjectConfirmationData NotOnOrAfter="2020-11-24T01:58:07.104Z"

Recipient="https://serviceprovider.com/acs"/></saml:SubjectConfirmation>

</saml:Subject>

<saml:Conditions NotBefore="2020-11-24T01:48:07.104Z" NotOnOrAfter="2020-11-24T01:58:07.104Z">

<saml:AudienceRestriction>

<saml:Audience>http://www.serviceprovider.com/</saml:Audience>

</saml:AudienceRestriction>

</saml:Conditions>

<saml:AuthnStatement AuthnInstant="2020-11-24T01:53:07.103Z"

SessionIndex="bJUFiJZEXV0rDgdTh9HnF2CbrIq">

<saml:AuthnContext>

<saml:AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Telephony</saml:AuthnContextClassRef>

</saml:AuthnContext>

</saml:AuthnStatement>

<saml:AttributeStatement>

<saml:Attribute Name="mail" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">

<saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema"

xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Patrick.Lunney@idprovider.com</saml:AttributeValue>

</saml:Attribute>

</saml:AttributeStatement>

</saml:Assertion>

</samlp:Response>
```

@row
### Item 3: OpenID Connect

To begin the process the user agent will first make a GET request against the authorization server, passing along information about the application the user wishes to go to.

```
curl --request GET \

--header ‘content-type: application/x-www-form-urlencoded' \

--url “${sso_prefix}/authorization?response_type=code&redirect_uri=${redirect_uri}&scope="openid profile”&client_id=${client_id}
```

What will return from this request is the login page (assuming there is no session), and a user will enter their credentials so the authorization server can authenticate the user. Afterward, an authorization\_code is sent to the application in the browser. The application backend must take that authorization\_code and exchange it for an access token.

To exchange the authorization\_code for the access token:

```
curl --request POST \

--url “https://${sso_prefix}/token” \

--header 'content-type: application/x-www-form-urlencoded' \

--header 'Authorization: Basic base64(urlencode("${client_id}:${client_secret}))' \

--data “code=${code}” \

--data “grant_type=authorization_code” \

--data “redirect_uri=${redirect_uri}” \

--data 'scope=openid profile'
```

After this exchange, the application can then make a backend API call to the authorization server to obtain additional information about the user for further authorization.

```
curl --request GET \

--header ‘content-type: application/x-www-form-urlencoded' \

--header 'Authorization: Bearer ${token}

--url “${sso_prefix}/userinfo
```

This will give applications information like this:

```
{

"sub" : "83692",

"name" : "Alice Adams",

"email" : "alice@example.com",

"department" : "Engineering",

"birthdate" : "1975-12-31"

}
```

- - -

[^1]:  “Multilateral federation,” InCommon Federation wiki, last updated 17 February 2020, [https://spaces.at.internet2.edu/display/federation/Multilateral+federation](https://spaces.at.internet2.edu/display/federation/Multilateral+federation) . 
    
[^2]:  Hodges, Jeff, Rob Philpott, Eve Maler, eds. “Glossary for the OASIS Security Assertion Markup Language (SAML) V2.0,” OASIS Standard, 15 March 2005, [https://docs.oasis-open.org/security/saml/v2.0/saml-glossary-2.0-os.pdf](https://docs.oasis-open.org/security/saml/v2.0/saml-glossary-2.0-os.pdf) . 
    
[^3]:  Hardt, D., Ed., "The OAuth 2.0 Authorization Framework", RFC 6749, DOI 10.17487/RFC6749, October 2012, <https://www.rfc-editor.org/info/rfc6749>. 
    
[^4]:  Ragouzis, Nick, John Hughes, Rob Philpott, Eve Maler, Paul Madsen, Tom Scavo, eds. “Security Assertion Markup Language (SAML) V2.0 Technical Overview,” OASIS Committee Draft, 25 March 2008, [https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.pdf](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.pdf) . 
    
[^5]:  OASIS Standards landing page, [https://www.oasis-open.org/standards/](https://www.oasis-open.org/standards/) . 
    
[^6]:  Hardt, D., Ed., "The OAuth 2.0 Authorization Framework", RFC 6749, DOI 10.17487/RFC6749, October 2012, < [https://www.rfc-editor.org/info/rfc6749](https://www.rfc-editor.org/info/rfc6749) \>. 
    
[^7]:  Ibid, see Section 4.1. 
    
[^8]:  Hardt, D., Ed., "The OAuth 2.0 Authorization Framework", RFC 6749, Section 4.1, DOI 10.17487/RFC6749, October 2012, < [https://www.rfc-editor.org/info/rfc6749](https://www.rfc-editor.org/info/rfc6749) \>. 
    
[^9]:  For further discussion on the pros and cons between SAML and OAuth, see [https://www.okta.com/identity-101/whats-the-difference-between-OAuth-openid-connect-and-saml/](https://www.okta.com/identity-101/whats-the-difference-between-OAuth-openid-connect-and-saml/) or [https://auth0.com/intro-to-iam/saml-vs-openid-connect-oidc/](https://auth0.com/intro-to-iam/saml-vs-openid-connect-oidc/) 
    
[^10]:  Dingle, Pamela, “Introduction to Identity – Part 2: Access Management,” IDPro Body of Knowledge, 17 June 2020, [https://bok.idpro.org/article/id/45/](https://bok.idpro.org/article/id/45/) . 
    
[^11]:  Shibboleth Consortium, [https://www.shibboleth.net/](https://www.shibboleth.net/) . 
    
[^12]:  “Same-origin Policy,” MDM Web Docs, [https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin\_policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) . 
    
[^13]:  For additional information, see [https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) and https://web.dev/cross-origin-resource-sharing/ . 