---
layout: columns
title: IAM Reference Architecture (v2)
permalink: /docs/oidc_oauth/idpro_bok/76
date: 2024-09-09
modify_date: 2024-11-16
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "アーキテクチャ", "参照モデル"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/76/](https://bok.idpro.org/article/id/76/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article provides a reference model to organize the presentation of technical details associated with various implementations of identity and access management (IAM) architectural concepts. The model is conceptual, as are the set of abstract components which it provides.

Additional articles will be made available in the IDPro Body of Knowledge that offer more specific technical use-cases based on the abstract concepts in this document.

Keywords: Architecture, Reference Model

@column
## 概要

本稿では、アイデンティティとアクセス管理（IAM）アーキテクチャコンセプトの様々な実装に関する技術的な詳細を整理するための参照モデルを提供します。このモデルは概念的なものであり、これが提供する抽象的なコンポーネントも概念的なものです・

この文書の抽象的な概念に基づいたさらに具体的な技術的ユースケースを提供する、追加の記事はIDPro Body of Knowledgeで入手可能になるでしょう。

Keywords: アーキテクチャ, 参照モデル

@row
### By George B. Dobbs

© 2022 IDPro, George B. Dobbs

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction

It has been said that all models are wrong, but some are useful. [^1] This model attempts to find a level of generality that is broadly useful. Too general, and the model becomes untethered to reality and definitely not useful. Too specific, and the model will only work in some cases.

This Identity and Access Management (IAM) Reference Architecture leans more towards technical implementation and touches on some of the process, legal, and capability dimensions. This breadth of coverage is intended to give the reader a set of concepts that can be applied when thinking about IAM.

The principle behind this model assumes that the management of identities and access can (mostly) be separated from their use. This concept can apply to distributed systems as well as self-contained systems. So, when you see IAM working together with, say, an application, it may mean that these are separate physical systems. Alternatively, it could mean these parts are separate pieces of software running on a single system.

The main goal of this article is to allow consistent discussion of more specific use-cases by offering a common set of terms and concepts to be used across all IAM architectures.

While the model incorporates guidance from various standards and best practice documents, the primary structure for the model started with the ISO/IEC framing. [^2] The Unified Modeling Language (UML) detail was removed for simplicity, and the IAM model has been extended so that authorization, governance, and risk-control can be included.

Some of the ISO/IEC names have been changed to reflect more common usage. In some cases, the ISO names have been used in a more expansive way than their original definition.

In an attempt to adopt the most useful terminology, the model has been reviewed in conjunction with the FICAM, [^3] Internet2, [^4] NIST SP-800-63 definitions, [^5] NIST Zero Trust frameworks, [^6] and with the Identity Stack as presented at Identiverse 2019. [^7]

The model can be used to support varying levels of system complexity. For example:

*   in a Distributed System environment, where the architecture may have a web-hosted application the Relying Party (RP) that depends on a cloud identity service, the Identity Provider (IDP). The RP, in this case, could be a customer-facing application or a workforce-facing application;
    
*   in a Single System model, where a computer’s file system (the RP) provides access control based on the user information acquired at login (the IDP). In this case, both the file system and IAM function are encapsulated in an operating system.
    

@column
## 導入

すべてのモデルが間違っているが、有用なものもあると言われてきました。 [^1] このモデルは、広く役立つ一般性のレベルを見つけようとしています。あまりにも一般的すぎると、モデルが現実にそぐわなくなり、まったく役に立たなくなります。具体的すぎると、モデルが一部のケースにしか機能しないことになります。

このアイデンティティとアクセス管理（IAM）参照アーキテクチャは技術的な実装に重きが置かれていますが、プロセス、法律および機能の側面の一部にも触れています。このように幅広い範囲をカバーすることで、IAMについて考える際に適用できる一連の概念を読者に提供することを目的としています。

このモデルの背後にある原則は、アイデンティティとアクセスの管理が（ほとんど）それらの使用から分離できることを前提としています。この概念は、自己完結型システムだけでなく、分散システムにも適用できます。したがって、IAMがアプリケーションなどと連携して動作している場合、これらは別々の物理システムであることを意味している可能性があります。または、これらの部分が単一のシステムで実行される個別のソフトウェアを意味する場合もあります。

この章の主な目的は、すべてのIAMアーキテクチャで使用される共通の用語と概念を提供することによって、より具体的なユースケースについて一貫した議論をおこなえるようにすることです。

モデルにはさまざまな標準やベストプラクティスドキュメントからのガイダンスが組み込まれていますが、モデルの主要な構造はISO/IECの枠組みから始まりました。 [^2] 簡単にするために統一モデリング言語（UML）の詳細を削除し、IAMモデルを拡張して、認可、ガバナンスおよびリスク管理を含められるようにしました。

一部のISO/IEC名は、より一般的な使用法を反映するように変更されています。場合によっては、ISO名が元の定義よりも広範な方法で使用されています。

最も有用な用語を採用する試みとして、モデルはFICAM、 [^3] Internet2、 [^4] NIST SP-800-63定義、 [^5]  NISTゼロトラストフレームワーク、 [^6] およびIdentiverse 2019 で発表されたアイデンティティスタックと併せてレビューされました。 [^7] 

このモデルは、さまざまなレベルのシステムの複雑さをサポートするために使用できます。例えば：

*   分散システム環境では、クラウドアイデンティティサービス、アイデンティティプロバイダー（IDP）に依存するWebホスト型アプリケーションであるリライングパーティ（RP）がアーキテクチャに含まれます。この場合、RPは顧客向けアプリケーションまたは従業員向けアプリケーションである可能性があります。
    
*   Single Systemモデルでは、コンピュータのファイルシステム（RP）が、ログイン時に取得したユーザー情報（IDP）に基づいてアクセス制御を提供します。この場合、ファイルシステムとIAM機能の両方がオペレーティングシステムにカプセル化されます。
    

@row
## Terminology

The terms are defined below. Those with a mark are the abstract components that comprise the model.

Two of the terms, IDM and Access Management, are used for a conceptual grouping of components. This is to aid understanding.

|     |     |
| --- | --- |
| Item | Definition |
| Access Control | Various methods to limit access to data, systems, services, resources, locations by a user, a device or thing, or a service. |
| Access Governance (also known as Identity Governance and Administration (IGA)) | Access Governance provides oversight and control over access rights implemented in multiple local or shared authorization systems. These rights may be controlled in a variety of ways, starting with the existence and validity of the digital identity. Other controls include various mechanisms such as policies, the mapping of roles, permissions, and identities. The abbreviation used is for Identity Governance and Administration and is commonly used in the commercial sector. This roughly corresponds to the Access Certification section of the first-class component Governance Systems in the FICAM model. IGA is not specifically addressed in the ISO/IEC model. |
| Access Management | The process and techniques used to control access to resources. This capability works together with identity management and the Relying Party to achieve this goal. The model shows access management as a conceptual grouping consisting of the Access Governance function and the shared authorization component. However, access management impacts local authorization as well (through the governance function). |
| Assertion | A formal message or token that conveys information about a principal, typically including a level of assurance about an authentication event and sometimes additional attribute information. Sometimes this is called a Security Token. |
| Assurance Level | A category describing the strength of the identity proofing process and/or the authentication process. See NIST SP.800-63-3 for further information. |
| Attribute Provider | Sometimes the authority for attributes is distinguished from the authority for identities. In this case, the term Attribute Provider is sometimes used. It is a subset or type of an Identity Information Authority. |
| Audit Repository | A component that stores records about all sorts of events that may be useful later to determine if operations are according to policy, support forensic investigations, and allow for pattern analysis. Typically, this is highly controlled to prevent tampering. Audit Repository is the ISO name for this concept and is localized to the IDM. In this model, the term is generalized to indicate a service that supports event records from any part of the ecosystem. |
| AuthN) | The act of determining that to a level of assurance, the principal/subject is authentic. |
| AuthN Assertion | A security token whereby the IDP provides identity and authentication information securely to the RP. |
| Authorization (AuthZ) | Authorization is how a decision is made at run-time to allow access to a resource. We break this down into two types: shared and local. The FICAM framework includes this as a subcomponent of the Access Management System. AuthZ is not included in the ISO or Internet2 models. |
| > Shared AuthZ | Shared authorization is provided by a facility outside of the RP. It is shown here as part of the access management grouping. |
| > Local AuthZ | Local authorization is handled by the RP. |
| Credential | A credential allows for authentication of an entity by binding an identity to an authenticator. |
| Credential Service Provider (CSP) | Following the guidance included in NIST 800-63-3, we include both the enrollment function and credential services together under the name Credential Services Provider. |
| Credential Services | Credential Services issue or register the subscriber authenticators, deliver the credential for use, and subsequently manage the credentials. We include PKI information for IAM architectures that must include system components that need certificates and private keys. This roughly corresponds to the FICAM component called Credential Management Systems. |
| Enforcement | The mechanism that ensures an individual cannot perform an action or access a system when prohibited by policy. |
| Enrollment | Also known as Registration. Enrollment is concerned with the proofing and lifecycle aspects of the principal (or subject). The entity that performs enrollment has sometimes been known as a Registration Authority, but we (following NIST SP.800-63-3) will use the term Credential Service Provider. |
| Entitlement | The artifact that allows access to a resource by a principal. This artifact is also known as a privilege, access right, permission, or an authorization. An entitlement can be implemented in a variety of ways. |
| Identity Information Authority (IIA) | This represents one or more data sources used by the IDM as the basis for the master set of principal/subject identity records. Each IIA may supply a subset of records and a subset of attributes. Sometimes the IIA is distinguished from the Identity Information Provider or IIP. We use IIA to include the service that actually provides the information as well as the root authority. This corresponds to Identity Information Source in ISO/IEC 24760-2 and Identity Sources in Internet2. |
| Identity Management (IDM) | A set of policies, procedures, technology, and other resources for maintaining identity information. The IDM contains information about principals/subjects, including credentials. It also includes other data such as metadata to enable interoperability with other components. The IDM is shown with a dotted line to indicate that it is a conceptual grouping of components, not a full-fledged system in itself. |
| Identity Provider (IDP) | Identity Provider or IDP is a common term. We treat this as a subset of Identity Management. It consists of the service interfaces: AuthN/Assertion, Service Provisioning Agent, Session Management, Discovery Services, and Metadata Management. |
| Identity Register | This is the datastore that contains the enrolled entities and their attributes, including credentials. See the IDM section for elaboration. The terms Directory, Identity Repository, and Attribute Store are sometimes used as synonyms. |
| Metadata Management | The processes and techniques that allow the collection, use, and eventual deletion of control data used by the IDM to recognize and trust the Relying Party. This corresponds to Relying Party data in the Internet2 model. |
| Relying Party (RP) | A component, system, or application that uses the IDP to identify its users. The RP has its own resources and logic. Note that the term ‘relying service’ is used in the ISO/IEC standards to encompass all types of components that use identity services, including systems, sub-systems, and applications, independent of the domain or operator. We will use the more common Relying Party (or RP). An RP roughly corresponds to the Agency Endpoint in the FICAM model or to Identity Consumers in the Internet2 model. |
| Risk Context (RCTX) | Risk Context consists of additional facts that can be brought to bear to improve the overall security of the ecosystem. Internal or external events and facts can be applied to enable, limit, or terminate access. This is similar to the section Monitors and Sensors under FICAM’s Governance Systems and to many of the inputs of the Policy Decision Point in the NIST Special Publication 800-207, a paper on Zero Trust. |
| Session | A period of time after an authentication event when an RP grants access to resources for the principal/subject. The duration of the session and the mechanism for enforcement vary by implementation. |
| Session Management | A coordinating function provided by an IDP to control sessions of subscribing RPs. |
| Trust Framework | This component represents the legal, organizational, and technical apparatus that enables trust between the IDM and the RPs. |
| Trust Root | A technical structure that provides the IDP and RP the ability to recognize each other with a high degree of certainty. This is similar to the concept of Trust Anchor (NIST SP.800-63-3), but we allow for a structure that relies on a mutually agreed-upon third party. A trust root derives from the operation of a Trust Framework. |

@column
## 用語解説

用語の定義は以下の通りです。✓印は、モデルを構成する抽象的な構成要素です。

IDMとAccess Managementの2つの用語は、構成要素の概念的なグループ分けに使用されています。これは理解を助けるためです。

|     |     |
| --- | --- |
| 用語 | 定義 |
| アクセス制御 | ユーザー、デバイスやモノ、サービスによるデータ、システム、サービス、リソース、場所へのアクセスを制限するための様々な方法。 |
| ✓アクセスガバナンス（アイデンティティガバナンスと管理（IGA）としても知られます） | アクセスガバナンスは、複数のローカルまたは共有の認可システムに実装されたアクセス権の監視と制御を提供します。これらの権利は、デジタルアイデンティティの存在と有効性から始まる様々な方法で制御される場合があります。その他の制御には、ポリシー、ロールのマッピング、パーミッションおよびアイデンティティなどのさまざまなメカニズムが含まれます。Identity Governance and Administrationの略称で、商業分野では一般的に使用されています。FICAMモデルの第一級コンポーネントGovernance SystemsのAccess Certificationの部分にほぼ相当します。IGAはISO/IECモデルでは扱われていません。 |
| ✓アクセス管理 | リソースへのアクセスを管理するプロセスおよび技術です。この機能はアイデンティティ管理およびリライングパーティと強力してこの目標を達成します。このモデルでは、アクセス管理はアクセスガバナンス機能と共有認可コンポーネントで構成される概念的なグループとして示されています。ただし、アクセス管理はローカル認可にも（ガバナンス機能を通じて）影響を与えます。 |
| アサーション | 主要な情報を伝える正式なメッセージまたはトークンで、通常、認証イベントに関する保証レベル、場合によっては追加の属性情報を含みます。これをセキュリティトークンと呼ぶこともあります。 |
| 保証レベル | 身元確認プロセスおよび／または認証プロセスの強度を記述するカテゴリ。詳細については、NIST SP.800-63-3を参照してください。 |
| ✓属性プロバイダー | 属性のための権威機関とアイデンティティのための権威機関を区別することがあります。この場合、属性プロバイダーという用語が使われることがあります。これは、アイデンティティ情報権威機関のサブセットもしくは一種です。 |
| ✓監査リポジトリ |	あらゆる種類のイベントに関する記録を保存するコンポーネントで、後で操作がポリシーに従っているかどうかを判断したり、フォレンジックス調査をサポートしたり、パターン分析を可能にしたりするのに役立つ可能性があります。一般に、改竄を防ぐために高度に管理されます。監査リポジトリは、この概念のISOでの名称であり、IDMにローカライズされています。このモデルでは、この用語はエコシステムのあらゆる部分からのイベント記録をサポートするサービスを示すために一般化されています。 |
| ✓認証（AuthN） | 一定の保証レベルを得るために、主体／対象が本物であると判断する行為。 |
| AuthNアサーション | IDPがRPにアイデンティティおよび認証情報を安全に提供するためのセキュリティトークン。 |
| 認可（AuthZ） | 認可は、リソースへのアクセスを許可するかどうかを実行時に決定する方法です。これは2種類に分けることができます：共有とローカルです。FICAMフレームワークは、アクセス管理システムのサブコンポーネントとしてこれを含んでいます。AuthZは、ISOやInternet2モデルには含まれていません。 |
| > ✓共有AuthZ | 共有認可はRP外の機関によって提供されます。ここでは、アクセス管理のグループ化の一部として紹介します。 |
| > ✓ローカルAuthZ | ローカル認可はRPによって扱われます。 |
| クレデンシャル | 	クレデンシャルはアイデンティティを認証子にバインドすることでエンティティの認証を可能にします。 |
| ✓クレデンシャルサービスプロバイダー（CSP） | NIST 800-63-3のガイダンスに従い、登録機能とクレデンシャルサービスをクレデンシャルサービスプロバイダーという名称でまとめています。 |
| クレデンシャルサービス | クレデンシャルサービスは、サブスクライバー認証子を発行または登録し、使用するためにクレデンシャルを提供し、その後クレデンシャルを管理します。証明書および秘密鍵を必要とするシステムコンポーネントを含める必要があるIAMアーキテクチャのために、PKI情報を含みます。これは、クレデンシャル管理システムというFICAMコンポーネントに概ね対応します。 |
| 強制 | ポリシーによって禁止されている場合に、個人がアクションを実行したりシステムにアクセスしたりできないようにするメカニズム。 |
| エンロールメント | 登録とも呼ばれます。エンロールメントは、主体（または対象）の証明とライフサイクルの側面に関連しています。エンロールを実行するエンティティは、登録機関と呼ばれることもありますが、（以下のNIST SP.800-63-3）クレデンシャルサービスプロバイダーという用語を使用します。 |
| エンタイトルメント | 本人によるリソースへのアクセスを許可する成果物。この成果物は、特権、アクセス権、パーミッションまたは認可とも呼ばれます。エンタイトルメントは、さまざまな方法で実装できます。 |
| ✓アイデンティティ情報機関（IIA） | これは、本人/対象のアイデンティティレコードのマスターセットの基礎としてIDMによって使用される1つ以上のデータソースを表します。各IIAは、レコードのサブセットと属性のサブセットを提供できます。IIAは、アイデンティティ情報プロバイダー、つまりIIPと区別される場合があります。IIAはルート機関だけでなく、実際に情報を提供するサービスも含めて使用します。これは、ISO/IEC 24760-2のアイデンティティ情報ソースおよびInternet 2のアイデンティティソースに対応します。 |
| ✓アイデンティティ管理（IDM） | アイデンティティ情報を維持するためのポリシー、手順、技術およびその他のリソースのセット。IDMには、クレデンシャルズなど、本人/対象に関する情報が含まれます。また、他のコンポーネントとの相互運用性を可能にするメタデータなどの他のデータも含まれます。IDMは、それ自体が完全なシステムではなく、コンポーネントの概念上のグループであることを示すために、点線で示されています。 |
| アイデンティティプロバイダー（IDP） | アイデンティティプロバイダーつまりIDPは一般的な用語です。これはアイデンティティ管理のサブセットとして扱います。以下のサービスインターフェイスで構成されます：AuthN／アサーション、サービスプロビジョニングエージェント、セッション管理、ディスカバリサービスおよびメタデータ管理。 |
| アイデンティティレジスター | これは、登録されたエンティティとクレデンシャルを含む属性を保持しているデータストアです。詳細は、IDMの項目を参照してください。ディレクトリ、アイデンティティリポジトリおよび属性ストアという用語は、シノニムとして使用される場合もあります。 |
| ✓メタデータ管理 | IDMがリライングパーティを認識して信頼するために使用する制御データの収集、利用および最終的な削除を可能にするプロセスと技術。これは、Internet2モデルのリライングパーティデータに対応します。 |
| ✓リライングパーティ（RP） | ユーザーを識別するために、IDPを使用するコンポーネント、システムまたはアプリケーション。RPには独自のリソースとロジックがあります。「リライングサービス」という用語は、ISO/IEC規格では、ドメインや事業者とは無関係に、システム、サブシステム、アプリケーションを含むアイデンティティサービスを使用するあらゆる種類のコンポーネントを包含するために使用されていることに注意してください。より一般的なリライングパーティ（つまりRP）を使用します。RPは、FICAMモデルの代理エンドポイントまたはInternet2モデルのアイデンティティコンシューマに大まかに対応します。 |
| ✓リスクコンテキスト（RCTX） | リスクコンテキストは、エコシステムの全体的なセキュリティを向上させるために持ちこたえることができる追加的なファクトで構成されています。内部または外部のイベントとファクトを適用して、アクセスを有効化、制限または終了できます。これは、FICAMのガバナンスシステムのモニターとセンサーの項目や、ゼロトラストに関する論文であるNIST Special Publication 800-207のポリシー決定ポイントのインプットの多くに似ています。 |
| セッション | 認証イベント後、RPが本人/対象のリソースへのアクセスを許可する期間。セッションの期間と強制のメカニズムは、実装によって異なります。 |
| ✓セッション管理 | サブスクライブするRPのセッションを制御するためにIDPによって提供される調整機能。 |
| トラストフレームワーク | このコンポーネントは、IDMとRP間の信頼を可能にする法的、組織的および技術的な装置を表します。 |
| ✓トラストルート | IDPとRPが互いを高い確実性で認識する能力を提供する技術的構造。これは、トラストアンカー（NIST SP.800-63-3）の概念に似ていますが、相互に合意した第三者に依存する構造を考慮しています。トラストルートは、トラストフレームワークの運用から派生します。 |

@row
## Basic Structure of the Model

The most basic function of the identity system is to provide secure storage of the information about identities and a way for Relying Parties (RPs) to use that data to control access to resources. The following diagram shows the core components of an identity management system (IDM) that supports multiple RPs.

@column
## モデルの基本的な構造

アイデンティティシステムの最も基本的な機能は、アイデンティティに関する情報を安全に保管し、リライングパーティ（RP）がそのデータを使用してリソースへのアクセスを制御する方法を提供することです。次の図は、複数のRPをサポートするアイデンティティ管理システム（IDM）の中核となるコンポーネントを示しています。

@row
![](/assets/images/idpro_bok/76-image1.png)

_Figure 1: Basic Component Dependencies the IDM supports multiple relying parties. The core components of the IDM are shown. The dotted arrowed lines show dependencies_

@row
### Identity Management

Identity Management (IDM) is a set of policies, procedures, technology, and other resources for maintaining identity information. In this model, it contains information about principals/subjects, including credentials. It also includes other data such as metadata to enable interoperability with other components. The IDM is shown with a dotted line to indicate that it is a conceptual grouping of components, not a full-fledged system in itself.

@column
### アイデンティティ管理

アイデンティティ管理（IDM）は、アイデンティティ情報を維持するためのポリシー、手順、技術およびその他のリソースのセットです。このモデルでは、IDMにはクレデンシャルを含む主体／対象の情報が含まれます。また、他のコンポーネントとの相互運用性を可能にするメタデータなど、他のデータも含まれます。IDMは、それ自体が本格的なシステムではなく、構成要素の概念的なグループであることを示すために、点線で示されています。

@row
### Relying Party

The Relying Party (RP) is a component, system, or application that uses the IDM to identify its users. The RP has its own resources and logic. It comes in many forms, all of which use identity services, including systems, sub-systems, and applications, independent of the domain or operator.

@column
### リライングパーティ

リライングパーティ（RP）は、ユーザーを識別するためにIDMを使用するコンポーネント、システム、またはアプリケーションです。RPは独自のリソースとロジックを持ちます。さまざまな形態があり、ドメインや運用者とは無関係に、システム、サブシステム、アプリケーションなどを含めてすべてアイデンティティサービスを使用します。

@row
### Trust Framework

This component represents the legal, organizational, and technical apparatus that enables trust between the IDM and the RPs.

When the IDM and the RP are not in the same organization, the Trust Framework takes on a salient aspect, resulting in multilateral or bilateral agreements. In simple cases, this may be a contract between two parties. In other cases, there may be a multilateral agreement. We will use the term federation loosely to cover both cases. These frameworks are described further in Laws Governing Identity Systems (v2). [^8]

These agreements, rules, and policies govern how the federation members operate and interact. [^9] The parties of a federation establish mutual agreement upon an acceptable identity to be used between the parties in a federated relationship (for instance, the level of assurance used) in order to operate well. In addition, the definition and values of attributes of federated identities should be agreed upon. The parties should agree on the security/access policies of federated users between the parties in a federated relationship. For instance, whether there are duties to notify others in the event of security failures.

When IDM and the RP are in the same organization, the agreements may be more tacit.

When the IDM and RP are both built into a single system framework that allows for mutual trust may be completely opaque to the system operator, although the system developer may be aware of the framework or at least its implications since he or she will need to implement mechanisms that support the trust.

@column
### トラストフレームワーク

このコンポーネントは、IDMとRPの間の信頼を可能にする法的、組織的、技術的な仕組みを表します。

IDMとRPが同じ組織内に存在しない場合、トラストフレームワークは重要な側面を持ち、その結果、複数者間または二者間での合意が結ばれます。単純なケースでは、これは二者間の契約かもしれません。他のケースでは、複数者間の合意が存在することもあります。ここでは、どちらの場合もカバーするために、フェデレーションという言葉を拡大して使用します。これらのフレームワークは、「Laws Governing Identity Systems (v2)」 [^8] でさらに説明されています。

これらの合意、ルールおよびポリシーはどのようにフェデレーションメンバーが運用し、相互作用するのかを管理します。 [^9] フェデレーションの当事者は、良好な運用をおこなうために、フェデレーション関係にある当事者間で利用される受け入れ可能なアイデンティティ（たとえば、使用する保証レベル）について相互の合意を確立します。さらに、フェデレーションされたアイデンティティの属性の定義と値についても合意しておくべきです。フェデレーション関係にある当事者間で、フェデレーションユーザーのセキュリティ／アクセスポリシーについて合意しておくべきです。例えば、セキュリティ障害が発生した場合に他者に通知する義務があるかどうかなどです。

IDMとRPが同じ組織内にある場合、合意はより暗黙的である可能性があります。

IDMとRPの療法が単一のシステムに組み込まれている場合、相互信頼を可能にするフレームワークは、システム開発者はかなり意識していると思われる、つまり少なくとも信頼をサポートするための仕組みを実装する必要があることを意味しているが、システム運用者には全く不透明な場合がある。

@row
### Trust Root

A trust root is a technical structure that provides the IDP and RP the ability to recognize each other with a high degree of certainty. This is similar to the concept of Trust Anchor (NIST SP.800-63-3), but we allow for a structure that relies on a mutually agreed-upon third party. A trust root derives from the operation of a Trust Framework. There is a need for a trust root so that the systems can operate without human involvement in every transaction. This may be done through a Public Key Infrastructure (PKI), where the parties agree to trust a common certificate authority that signs the certificates of all parties in the federation. This may be done through a set of several independent certificates that the parties agree to trust.

@column
### トラストルート

トラストルートとは、IDPとRPが高い確実性で互いを認識する能力を提供する技術的な構造です。これはトラストアンカー（NIST SP.800-63-3）の概念に似ていますが、相互に合意した第三者に依存する構造を使っています。トラストルートは、トラストフレームワークの運用に由来するものです。システムがすべての取引に人間が関与することなく運用できるように、トラストルートが必要です。これは公開鍵基盤（PKI）を通じておこなわれるかもしれず、PKIではフェデレーション内のすべての当事者の証明書に署名している共通の認証局を信頼することに当事者たちは合意しています。これは、当事者たちが信頼することに同意した、一連のいくつかの独立した証明書を通しておこなわれるかもしれません。

@row
## Provisioning

Provisioning is a term that encompasses the processes and methods that create, modify, and, eventually, delete the identity and profile information used by IT infrastructure and business applications. By these methods, records are created or updated in the identity register and removed from it. Often, provisioning needs to extend to applications to support authorization decisions. This is sometimes known as “downstream provisioning”. The term “Onboarding” is sometimes used to refer to the sum of the initial provisioning activities in both the identity and access aspects.

@column
## プロビジョニング

プロビジョニングは、ITインフラストラクチャおよびビジネスアプリケーションで使用されるアイデンティティおよびプロファイル情報を作成、変更、そして最終的には削除するプロセスおよび方法を含む用語です。これらの方法によって、アイデンティティレジスターでレコードが作成または更新され、そこから削除されます。多くの場合、プロビジョニングは認可の決定をサポートするためにアプリケーションに対して拡張される必要があります。これは「ダウンストリームプロビジョニング」としても知られます。「オンボーディング」という用語は、アイデンティティとアクセスの両方の側面における初期プロビジョニングアクティビティの総和を指すために使われることがあります。

@row
![Provisioning: The Identity register receives updates from one or more external sources and administrative actions, passing the information on as needed.](/assets/images/idpro_bok/76-image2.png)

_Figure 2: Provisioning: The Identity register receives updates from one or more external sources and administrative actions, passing the information on as needed._

@row
### Identity Information Authorities

While it is possible to have an IDM populated without attaching to an external data service, this is typically not the case. Usually, employee or customer data needs to be imported. This can be referred to as upstream provisioning.

Note that the authoritative sources for identity attributes transcend the HR system and may include email, phone, training certification system, etc. In some cases, a company may have more than one HR system.

@column
### アイデンティティ情報の権威あるソース

外部のデータサービスに接続せずにIDMを構築することも可能ですが、一般的にはそのようなことはありません。通常、従業員や顧客のデータをインポートする必要があります。これはアップストリームプロビジョニングと呼ばれます。

アイデンティティ属性の権威あるソースは、人事システムを超えて、電子メール、電話、トレーニング認定システムなどを含む場合があることに注意してください。場合によっては、1つの企業が複数の人事システムを持つこともあります。

@row
### Governance

The act of provisioning may include certain logic, best modeled as governance. In some cases, the IGA system takes on all the provisioning duties (see also the section on Access Governance below).

@column
### ガバナンス

プロビジョニングのアクティビティには、ガバナンスとして最適にモデル化された、ある種のロジックが含まれる場合があります。場合によっては、IGAシステムがすべてのプロビジョニング業務を引き受けることもあります（以下のアクセスガバナンスのセクションも参照してください）。

@row
### Credential Services & Enrollment

This function includes steps needed to originate and activate an identity. It is also concerned with ongoing maintenance such as password reset and key rotation. This function includes administrative activities and self-serve activities.

@column
### クレデンシャルサービスと登録

この機能には、アイデンティティの生成と活性化に必要な手順が含まれます。また、パスワードのリセットやキーのローテーションなど、継続的な保守にも関連します。この機能には、管理アクティビティおよびセルフサービスアクティビティが含まれます。

@row
### Enrollment

Also sometimes known as Registration. It involves such activities as proofing, verification or vetting, and recording sponsorship if needed. It also is responsible for the secure delivery of credentials. Enrollment ends when a user formally receives ownership of their digital identity and assumes control and ownership of their account’s credentials.

@column
### 登録（Enrollment）

登録（Registration）と呼ばれることもあります。必要に応じて、証明、検証または審査およびスポンサーの記録などの活動を含みます。また、クレデンシャルの安全な配信も担当します。登録は、ユーザーが正式にデジタルアイデンティティの所有権を受け取り、自分のアカウントのクレデンシャルの制御および所有権を引き受けたときに終了します。

@row
### Credential Services

Credential services include the creation of passwords, cryptographic keys, and other authenticators. It associates or "binds" these to an identity record. It is also concerned with ongoing maintenance such as password reset and key rotation and revocation of credentials as needed.

@column
### クレデンシャルサービス

クレデンシャルサービスには、パスワード、暗号鍵、その他の認証器の作成が含まれます。これらはアイデンティティレコードに関連付けたり、「バインド」したりします。また、パスワードのリセットやキーのローテーションなどの継続的なメンテナンス、必要に応じてクレデンシャルを失効させることにも関係します。

@row
### Identity Register

This is the datastore that contains the enrolled entities and their attributes, including credentials. In this model, we use the singular, as if it were one singular database. In practice, designs may store some attributes separately from identities. We also use this term to include the storage related to credentials, although all or some of the credentials may be stored in their own physical repository.

Identity Registers, by their nature, have high availability requirements. Often at the physical level, they contain multiple instances which are synchronized. The Identity Register could be implemented in several ways. Common methods include the use of general-purpose databases, optimized stores such as directories, either physical or virtual.

Importing data does not necessarily mean making a physical copy of data, although it often does. The notion also supports the idea of virtualization - where the import of identity information is done at run-time.

@column
### アイデンティティレジスター

アイデンティティレジスターは、登録されたエンティティとクレデンシャルを含む属性を格納するデータストアです。このモデルでは、単一のデータベースであるかのように、単数形を使用しています。実際には、設計上、一部の属性はアイデンティティとは別に保存される場合があります。また、この用語を使用して、クレデンシャルに関連するストレージを含めますが、クレデンシャルのすべてまたは一部は、独自の物理リポジトリに格納される場合があります。

アイデンティティレジスターは、その性質上、高い可用性が要求されます。多くの場合、物理レベルでは、同期される複数のインスタンスが含まれます。アイデンティティレジスターはいくつかの方法で実装することができます。一般的な方法としては、汎用データベース、ディレクトリなどの最適化されたストア、物理または仮想のいずれかを使用する方法があります。

データのインポートは、しばしば実行されますが、必ずしもデータの物理的なコピーを作成することを意味しません。この概念は、アイデンティティ情報のインポートがランタイムで実行されるという仮想的なコピーもサポートしています。

@row
### Service Provisioning Agent

Also noted is the function of propagating selected information further into the ecosystem. This typically occurs when an RP needs additional information about the users, e.g., for access control or personalization. The RP makes a copy of the identity data for future use in the application processes. A complete solution will support the full data lifecycle, including creation, update, and eventual deletion of the identity data stored locally.

@column
### サービスプロビジョニングエージェント

選択した情報をさらにエコシステムに伝播させる機能も注目に値します。これは通常、アクセス制御やパーソナライゼーションのためなど、RPがユーザーに関する追加情報を必要とする場合に発生します。RPは、将来アプリケーション処理で使用するためにアイデンティティデータのコピーを作成します。完全なソリューションとしては、ローカルに保存されたアイデンティティデータの作成、更新、および最終的な削除を含む、完全なデータライフサイクルをサポートすることです。

@row
### Just in Time Provisioning

So far, the discussion of the provisioning function has been focused on “admin-time”. However, there are some cases where provisioning occurs at run time.

Not shown here, but sometimes implemented, are provisioning actions that occur on a just-in-time basis. This can happen when additional identity information is passed to an RP in real-time to support a specific application requirement, possibly including identity attributes (See Authentication and Sessions). A similar case involves the RP querying the IDM to acquire attributes (see Authorization later in this document)

@column
### ジャストインタイム・プロビジョニング

これまで、プロビジョニング機能については、「管理時間」を中心に議論してきました。しかし、ランタイムにプロビジョニングが発生するケースもあります。

ここには示していませんが、ときおり実装されるのは、ジャストインタイムベースで発生するプロビジョニング動作です。これは、特定のアプリケーション要件をサポートするために、アイデンティティ属性を含む追加のアイデンティティ情報がリアルタイムでRPに渡される場合に発生する可能性があります（「認証とセッション」のセクションを参照）。同様のケースとして、RPがIDMに照会をおこなって属性を取得する場合があります（本文書で後述する「認可」セクションを参照）。

@row
### Audit Repository

The audit repository is shown to indicate the accumulation of historical event data. To avoid clutter, we assume audit information is written but call that out with arrows in the diagram.

@column
### 監査リポジトリ

監査リポジトリは、過去のイベントデータの集積を示すものです。ごちゃごちゃしないように、監査情報が書き込まれていることを想定しているが、図中では矢印でそれを表しています。

@row
## Authentication and Sessions

@column
## 認証とセッション

@row
### Authentication

Authentication is the process by which a subject’s credentials are used to verify their identity. The IDP checks and verifies credentials that are presented to it. There are multiple scenarios. Typically, the RP asks the Identity provider to gather the credentials from the user and receives an assessment from the IDP regarding the level of certainty that the user is authentic. Often the assessment (and more information about the user) is delivered to the RP via a security token, which is protected by cryptography. There are several varieties of security tokens. The diagram uses bidirectional arrows to show that use cases exist that require ongoing exchange of information as describe in the section in this document called “Sessions.”

@column
### 認証

認証は、主体のクレデンシャルを使用して身元を確認するプロセスです。IDPは、提示されたクレデンシャルを確認して検証します。ここからは複数のシナリオがあります。通常、RPはアイデンティティプロバイダーにユーザーからクレデンシャルを収集するように依頼し、IDPからユーザーが本物であるという確実性のレベルに関する評価を受け取ります。多くの場合、評価（およびユーザーに関する詳細情報）は、暗号化によって保護されているセキュリティトークンを介してRPに配信されます。 セキュリティトークンにはいくつかの種類があります。図では双方向矢印を使って、本ドキュメントのセクションで「セッション」と呼称する情報のやり取りを必要とするユースケースの存在を示しています。

@row
![Authentication and Sessions: The Identity Register supports authentication scenarios. The IDP may monitor or participate if the full session lifecycle with the Relying services.](/assets/images/idpro_bok/76-image3.png)

_Figure 3: Authentication and Sessions: The Identity Register supports authentication scenarios. The IDP may monitor or participate in the full session lifecycle with the relying parties._

@row
### Sessions

A common pattern is to associate the authentication event with the start of a session. The session is mostly the concern of the RP. However, it is sometimes desirable to keep the sessions of several relying parties in synch. For instance, logging out of one session will terminate concurrent sessions. To do this, often the IDP will act to orchestrate sessions termination. In high-security environments, session management must support termination based on real-time identity data, such as when a user’s entitlements have been modified.

The existence of a centralized point of view about sessions can be leveraged to support good security practices. For example, if the identity attributes of a user with an active session change and these new values then contravene an access control policy, the session should terminate. If session management becomes aware of a terminated account, it should end any active session that the user has. This could also occur in advanced scenarios that include facts presented by external risk monitors. See Risk Context below.

Sessions also support another important concept: step-up authentication. A session can keep track of the level of assurance of a particular authentication, so when a user requests access to a transaction or application requiring a higher level of identity assurance, the IDP can be prepared to determine the course of action, such as improving the certainty that the user is the right person by asking the user provide additional evidence. For example, maybe the password is good enough to review some information, but to withdraw money, the additional factor of a one-time password from a phone app is required. The detection of the assurance gap and subsequent action will logically be done at the RP, but to avoid a poor user experience in multiple RP scenarios, the step-up needs to be recorded in the session.

@column
### セッション

一般的なパターンは、認証イベントをセッションの開始に関連付けることです。セッションは主にRPの関心事です。ただし、複数のリライングパーティのセッションを同期させておくことが望ましい場合もあります。たとえば、1つのセッションからログアウトすると、同時にセッションが終了します。これをおこなうには、多くの場合、IDPはセッションの終了を調整するように機能します。高度なセキュリティ環境では、セッション管理は、ユーザーのエンタイトルメントが変更された場合など、リアルタイムのアイデンティティデータに基づいた終了をサポートする必要があります。

セッションに関する一元化された視点の存在は、適切なセキュリティプラクティスをサポートするために活用できます。たとえば、アクティブなセッションを持つユーザーのアイデンティティ属性が変更され、これらの新しい値がアクセス制御ポリシーに違反する場合、セッションは終了する必要があります。セッション管理が終了したアカウントを認識した場合、ユーザーが持っているアクティブなセッションを終了する必要があります。これは、外部のリスク監視によって提示された事実を含む高度なシナリオでも発生する可能性があります。以下のリスクコンテキストのセクションを参照してください。

セッションは、ステップアップ認証という別の重要な概念もサポートしています。セッションは特定の認証の保証レベルを追跡できるため、ユーザーがより高いレベルのアイデンティティ保証を必要とするトランザクションまたはアプリケーションへのアクセスを要求した場合、IDPは、ユーザーに追加の証拠を提供するよう求めることで、ユーザーが正しい人物であることを確実にします。たとえば、一部の情報を確認するにはパスワードで十分ですが、お金を引き出すには、電話アプリのワンタイムパスワードという追加要素が必要になる場合があります。保証ギャップの検出とその後のアクションは、論理的にはRPでおこなわれますが、複数のRPシナリオでユーザーエクスペリエンスの低下を避けるために、ステップアップをセッションに記録する必要があります。

@row
## Authorization

Authorization models are many and diverse. The diagram illustrates two approaches for authorization: local and shared. As noted below, both approaches are subject to Access Governance.

Both approaches typically use subject attributes to help determine access, although some systems rely on direct enumerations mapping users to resources known as access control lists.

@column
## 認可

認可モデルは多種多様です。図では、ローカルと共有の2つの認可方法を示しています。以下に示すように、どちらのアプローチもアクセスガバナンスの対象となります。

どちらのアプローチも通常、主体の属性を使用してアクセスを決定しますが、一部のシステムは、ユーザーをアクセス制御リストと呼ばれるリソースにマッピングする直接列挙に依存しています。

@row
![Authorization models: Some RPs perform authorization tasks internally. Sometimes authorization is a shared resource for many RPs.](/assets/images/idpro_bok/76-image4.png)

_Figure 4: Authorization models: Some RPs perform authorization tasks internally. Sometimes authorization is a shared resource for many RPs._

@row
### Local Authorization

Many Relying parties perform authorization tasks internally. Often the fine-grained access control required by a protected resource makes this appealing. For instance, a financial management system may maintain a user’s entitlements to specific functionality within the application. In this scenario, the application makes the authorization decision and implements (enforces) the result.

The controlling values may have been provisioned into the local access data store by the Provisioning process described above. Or the values can be acquired at run-time from the IDM as shown by the attribute query, which may provide the user’s role or other attributes during the sign-on, perhaps as a value in the security token.

@column
### ローカル認可

多くのリライングパーティは、認可タスクを内部で実行します。保護されたリソースに要求されるきめ細かいアクセス制御は、しばしばこれを魅力的なものにします。例えば、財務管理システムは、アプリケーション内の特定の機能に対するユーザのエンタイトルメントを維持することができます。このシナリオでは、アプリケーションが認可の決定をおこない、その結果を実行（強制）します。

制御する値は、上述のプロビジョニングプロセスによってローカルアクセスデータストアにプロビジョニングされたものでかもしれません。あるいは、属性クエリによって示されるように、IDMからランタイムで値を取得することができ、IDMは、サインオン中にユーザーのロールまたは他の属性を、おそらくセキュリティトークンの値として提供します。

@row
### Shared Authorization

Sometimes authorization is a shared resource for many Relying parties. This design can improve the consistency of authorization decisions and supports organizations wishing to include advanced access decisions strategies such as those required by a “Zero Trust” access control approach. Shared authorization systems typically have a consistent approach to policy, such as a standardized policy language. In this scenario, the RP asks the shared authorization function to make the decision but implements (enforces) that itself.

@column
### 共有認可

認可は、多くのリライングパーティにとって共有リソースである場合があります。この設計により認可決定の一貫性が向上し、「ゼロトラスト」アクセス制御アプローチで必要とされるような、高度なアクセス決定戦略を組み込みたい組織をサポートできます。通常、共有認可システムには、標準化されたポリシー言語など、ポリシーに対する一貫したアプローチがあります。 このシナリオでは、RPは共有認可機能に決定を依頼しますが、自分自身でその決定を実行（強制）します。

@row
### Authorization Mechanisms

In either approach, the access rights may be established, maintained, and revoked in a variety of ways, starting with the existence and validity of the digital identity. Other controls include various mechanisms such as policies, roles, permissions, and identities. Some controls rely on user attributes, including group memberships or roles stored in an Identity Register. Some controls may depend on the properties of the accessed resource or the context of the request, such as time, device, or location.

Each mechanism relies on a particular logical data structure to implement the access control; that data structure becomes the focus of implementers. For instance, in role-based access control, there is some art involved in “Role Management” (defining and managing a useful set of roles) since too many roles become difficult to manage, whereas too few leads to users with access to things they don’t need. Similarly, in the case of policy-based access control, the set of policies (the Policy Rules) needs to be designed, stored, and managed.

@column
### 認可メカニズム

どちらのアプローチでも、アクセス権は、デジタルアイデンティティの存在と有効性から始まり、さまざまな方法で確立、維持、および取り消すことができます。その他の制御には、ポリシー、ロール、アクセス許可、アイデンティティなどのさまざまなメカニズムが含まれます。一部の制御は、アイデンティティレジスタに格納されているグループメンバーシップやロールなど、ユーザー属性に依存しています。一部の制御は、アクセスされたリソースのプロパティまたはリクエストのコンテキスト（時間、デバイスまたは場所など）に依存する場合があります。

それぞれの仕組みは、アクセス制御を実現するために特定の論理的なデータ構造に依存しており、そのデータ構造が実装者の焦点となります。例えば、ロールベースアクセス制御では、ロールが多すぎると管理が難しくなり、逆に少なすぎるとユーザーが必要のないものにアクセスすることになるので、「ロールの管理」（有用なロールのセットを定義し管理すること）に多少の技術が必要となります。同様に、ポリシーベースアクセス制御の場合、ポリシーのセット（ポリシールール）を設計し、保存し、管理する必要があります。

@row
## Access Governance

Access Governance, also known as Identity Governance and Administration (IGA), provides control over access rights implemented in multiple local or shared authorization systems. This function is often broken into the administration of these rights and the oversight needed to ensure that these rights are in good order over time.

In enterprise systems, Access Governance focuses on managing staff (employee/contractor) entitlements. The concept can also apply to other scenarios, such as when business-to-business delegated administrative rights are required or to in business-to-customer scenarios where authorized third parties such as attorneys are required.

@column
## アクセスガバナンス

アクセスガバナンスは、アイデンティティガバナンスと管理（IGA）とも呼ばれ、複数のローカルまたは共有権限システムに実装されているアクセス権の制御を提供します。この機能は、多くの場合、これらの権利の管理と、これらの権利が長期にわたって適切な状態にあることを保証するために必要な監視に分けられます。

企業システムにおいて、アクセスガバナンスはスタッフ（従業員/受託業者）の権限を管理することに重点を置いています。この概念は、企業間の管理権限の委譲が必要な場合や、弁護士のような権限を持つ第三者が必要な企業対顧客のシナリオなど、他のシナリオにも適用することができます。

@row
![Access Governance provides oversight and control over access rights implemented in many Local authorization systems and, sometimes, in Shared authorization systems.](/assets/images/idpro_bok/76-image5.png)

_Figure 5: Access Governance provides oversight and control over access rights implemented in many Local authorization systems and, sometimes, in Shared authorization systems._

@row
### Control

The controls may also include methods such as procedures and workflows to ensure proper review. Typically, a request for access to resources is passed to one or more approvers and an audit trail is created.

Often deployed to prevent internal fraud is the “segregation of duties” control. The control defines groups of access rights that cannot be held by the same person. This control is best implemented in a location that has visibility to all the implicated access rights, i.e., the IGA system.

@column
### 制御

また、制御には、適切なレビューを確実に実行するための手順やワークフローなどの方法が含まれることもあります。通常、リソースへのアクセス要求は、1人または複数の承認者に渡され、監査証跡が作成されます。

内部不正を防止するためにしばしば導入されるのが、「職務分掌」制御です。この制御は、同一人物が保持できないアクセス権のグループを定義します。この制御は、関係するすべてのアクセス権を可視化できる場所、すなわちIGAシステムで実施するのが最適です。

@row
### Oversight

Typically, governance activities review and potentially modify the data in one or more of the authorization components in order to effect a change in entitlements. Often organizations will have a formal process to review existing entitlements and may require a responsible party to certify or attest that the entitlements are in good order. Additional tools to ensure that IAM policies are effective at enforcing their stated controls include internal and external audits as well as analytic reports.

@column
### 見落とし

一般的に、ガバナンス活動は、エンタイトルメントの変更を実現するために、1つ以上の認可コンポーネントのデータをレビューし、潜在的に修正します。多くの場合、組織は既存のエンタイトルメントをレビューするための正式なプロセスを持っており、責任者がエンタイトルメントが正常であることを証明または認証することを要求する場合があります。IAMポリシーが有効であることを確認するための追加ツールでは内部監査や外部監査、分析レポートなど、定められた統制を実施するために有効な手段も用意されています。

@row
### Risk Context

Risk Context (often abbreviated as RCTX) information can be valuable to improve the security of the relying service. Risk can be judged based on information in the request, information about the history of the user, or assertions/evidence from third parties.

The linkage from the Audit Repository illustrates that the Risk Context may consume the local historical data about events.

@column
### リスクコンテキスト

リスクコンテキスト（多くの場合、RCTXと略される）情報は、リライングサービスのセキュリティを向上させるのに役立ちます。リスクは、リクエスト情報、ユーザーの履歴情報、または第三者のアサーション／エビデンスに基づいて判定できます。

監査リポジトリからのリンクは、リスクコンテキストがイベントに関するローカル履歴データを消費する可能性があることを示しています。

@row
![Risk Context: It is possible to use risk information in authentication decisions. For instance, if a stolen password is found on the dark web, don’t allow login.](/assets/images/idpro_bok/76-image6.png)

_Figure 6: Risk Context: It is possible to use risk information in authentication decisions. For instance, if a stolen password is found on the dark web, don’t allow login._

@row
External events may be visible to the IDM operator through consortia or vendor packages. In some mutual-support scenarios, it may be possible for the IDM operator to also publish events for the benefit of others, supporting other operators’ risk management requirements.

Events need to be delivered into the IDM so that they can selectively be used to modify the behavior of the authentication function. For example, armed with additional event data, the authentication function may request a step-up authentication or even plainly deny access.

In some severe scenarios, attaching the events to the session management function may be desirable so that current sessions can be reviewed and terminated if needed. The OpenID Shared Signals and Events working group is developing standard ways to deliver these signals. [^10]

As shown in the diagram, shared authorization systems may consume risk data as well. For example, an authorization might be denied if the subject’s recent activity history is outside of normal bounds, possibly indicating a compromised credential. Logically this could happen with local authorization as well, but this is not shown.

@column
外部イベントは、コンソーシアムやベンダーパッケージを通じてIDM運用者に表示される場合があります。一部の相互サポートシナリオでは、IDM運用者が他の運用者のリスク管理要件をサポートするため、他の運用者の利益のためにイベントを公開することも可能です。

認証機能の動作を変更するためにイベントを選択的に使用できるように、イベントをIDMに配達する必要があります。たとえば、追加のイベントデータを備えた認証機能は、ステップアップ認証を要求したり、単純にアクセスを拒否したりすることさえあります。

一部の深刻なシナリオでは、必要に応じて現在のセッションを確認して終了できるように、イベントをセッション管理機能に付属させることが望ましい場合があります。OpenID Shared Signals and Eventsワーキンググループは、これらのシグナルを配信する標準的な方法を開発しています。 [^10]

図に示されているように、共有認可システムはリスクデータも使用する可能性があります。たとえば、主体の最近のアクティビティ履歴が通常の範囲外である場合、認証が拒否される可能性があります。これは、認証情報の侵害を示している可能性があります。論理的には、これは（RPの）ローカル認可でも発生する可能性がありますが、これは図示されていません。

@row
### Example: Information in the request

@column
### 例：リクエストの情報

@row
#### Boundary control

An authentication or authorization decision may be influenced by specific criteria, such as whether a request is coming from a known or unknown network. A more sophisticated version of this attempts to prohibit access from, say, certain countries.

@column
#### 境界制御

認証や認可の判断は、リクエストが既知のネットワークからか未知のネットワークからか、といった特定の基準によって影響されることがあります。より高度なバージョンでは、例えば、特定の国からのアクセスを禁止することができます。

@row
### Examples: Historical usage

@column
### 例：履歴の利用

@row
#### Usage pattern match

Determine if this request is outside the normal usage patterns for a given individual. The reference to historical usage patterns allows for pattern detection and can help establish a metric for risk for a user, a specific transaction, or in general. Such activity can be called risk profiling.

@column
#### 使用パターンマッチ

リクエストが、ある個人の通常の使用パターンから外れているかどうかを判断します。過去の使用パターンを参照することで、パターン検出が可能になり、ユーザー、特定のトランザクションまたは一般的なリスクに対する評価基準を確立するのに役立つことがあります。このような活動は、リスクプロファイリングと呼ぶことができます。

@row
#### Land speed violation

Amending the user’s request and history with location information makes it possible to identify a likely compromised account because the user can’t be in two places at once.

Such examples depend on signals from the local environment, but it is also possible to obtain signals from further afield.

@column
#### 地上速度違反

ユーザーのリクエストと履歴に位置情報を付加することで、ユーザーが同時に2つの場所に存在することができないため、侵害された可能性が高いアカウントを特定することができます。

このような例は、ローカル環境からのシグナルに依存しますが、より遠くからのシグナルを得ることも可能ですs from further afield.

@row
### Example: Third party

it is possible to determine commonly used passwords based on postings on the “dark web.” Bad actors acquire these in the hope that users will use the same password at other sites. A countermeasure is for the IDM operator to require additional certainty if one of those passwords were presented.

@column
### 例：サードパーティ

「ダークウェブ」上の投稿から、よく使われるパスワードを特定することができます。悪意のあるアクター、ユーザーが他のサイトで同じパスワードを使用することを期待して、これらを入手します。そのため、IDM運用者は、これらのパスワードが提示された場合、さらなる確実性を要求することが対策となります。

@row
## Metadata and Discovery

Metadata refers to control data that allows the IDM and the Relying Parties to interoperate.

@column
## メタデータとディスカバリー

メタデータとは、IDMとリライングパーティが相互運用できるようにする制御データを指します。

@row
![](/assets/images/idpro_bok/76-image7.png)

_Figure 7: Metadata and discovery these two functions are involved with mutual recognition of the IDM and Relying Service._

@row
One example is the registration of public-key certificates to enable mutual authentication. In some scenarios, this information is shared between the parties manually. At run-time for distributed systems, the technical root of trust is needed to validate the security channel (PKI)

Another example points out that configuration information is another form of metadata. OpenID Connect has a list of required, recommended, and optional values that describe a particular implementation aimed at providing a degree of automation during setup.

The metadata may include information that limits the types of interactions and scope of the data that is exchanged. It can also contain security information to allow the counterparties to authenticate each other. For instance, public key components such as certificates with a common certificate authority may be used.

Discovery refers to protocols that facilitate automation. For instance, OpenID Connect defines a method for RPs to locate an end-point where a user’s identity can be verified. [^11] The concept is more supported by other methods such as SAML. [^12] A Discovery service can advise where specific data can be accessed and which end-points are maintained to allow an RP to use the identity service.

@column
1つの例は、相互認証を有効にするための公開鍵証明書の登録です。一部のシナリオでは、この情報は当事者間で手動で共有されます。分散システムのランタイムでは、セキュリティチャネル（PKI）を検証するために技術的な信頼の基点が必要です。

別の例では、構成情報がメタデータの別の形式であることを指摘しています。OpenID Connectには、セットアップ中にある程度の自動化を提供することを目的とした特定の実装を記述する必須、推奨およびオプションの値のリストがあります。

メタデータには、交換されるデータの相互作用の種類と範囲を制限する情報が含まれる場合があります。また、取引先が互いを認証できるようにするためのセキュリティ情報を含めることもできます。例えば、共通の認証局で発行された証明書のような公開鍵コンポーネントが使われます。

ディスカバリーとは、自動化を容易にするプロトコルのことです。たとえば、OpenID Connectは、RPがユーザーのアイデンティティを検証できるエンドポイントを見つけるためのメソッドを定義します。 [^11] この概念は、SAMLなどの他の手法もサポートされています。 [^12] ディスカバリーサービスは、特定のデータにアクセスできる場所や、RPがアイデンティティサービスを使用できるようにするために、どのエンドポイントが維持されるかを通知できます。

@row
## Author Bio

George Dobbs manages architects at a major insurance company. He is also the chairman of the IDPro Body of Knowledge Committee. One of his interests is modernizing the use of Identity and Access Management techniques used by the firm. He is particularly interested in the area of customer-facing applications, including approaches to fraud prevention in call center and digital contexts. Related to this, he is interested in the evolution of distributed session management – notably distributed session termination. He is a founding member of IDPro and represented his firm in the Identity Ecosystem Steering Group (IDESG). Prior to his current position, he led the development of customer-facing identity for websites at three other insurers. He has led a local identity and access management user group since 2004. Prior to that, he was the chairman of the Network Applications Consortium.

@row
## Acknowledgments

The author would like to express gratitude to Ian Glazer, Graham Williamson, and Corey Scholefield for the detailed reviews of early drafts; Jon Lehtinen and Steve Hutchinson for some of the definitions from their unpublished Introduction to Identity Part 3 document; and Bertrand Carlier for his thorough and thoughtful review.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2021-09-30 | V1 published |
| 2022-12-15 | V2 published; minor editorial changes; some clarification in the text re: Credential Services and in Authentication |

@row
## References

- - -

[^1]:  Wikipedia contributors, "All models are wrong," _Wikipedia, The Free Encyclopedia,_ [https://en.wikipedia.org/w/index.php?title=All\_models\_are\_wrong&oldid=1111346950](https://en.wikipedia.org/w/index.php?title=All_models_are_wrong&oldid=1111346950) (accessed November 28, 2022). 
    
[^2]:  ISO/IEC 24760-1 Second edition “IT Security and Privacy — A framework for identity management — Part 1: Terminology and concepts,” [https://www.iso.org/standard/77582.html](https://www.iso.org/standard/77582.html) and ISO/IEC 24760-2, 2015 “Information technology — Security techniques — A framework for identity management — Part 2: Reference architecture and requirements,” [https://www.iso.org/standard/57915.html](https://www.iso.org/standard/57915.html) (accessed 28 November 2022). 
    
[^3]:  “FICAM Playbooks – FICAM Architecture – System Component Examples,” Identity Assurance and Trusted Access Division in the GSA Office of Government-wide Policy, [https://playbooks.idmanagement.gov/arch/components/](https://playbooks.idmanagement.gov/arch/components/) (accessed 28 November 2022). 
    
[^4]:  Hazelton, Keith “The TAP Reference Architecture (RA)” [https://spaces.at.internet2.edu/pages/viewpage.action?pageId=98306902](https://spaces.at.internet2.edu/pages/viewpage.action?pageId=98306902) (accessed 28 November 2022). 
    
[^5]:  Grassi, Paul A., Michael E. Garcia, James L. Fenton, “NIST Special Publication 800-63-3 – Digital Identity Guidelines,” National Institute of Standards and Technology, U.S. Department of Commerce, June 2017, [https://doi.org/10.6028/NIST.SP.800-63-3](https://doi.org/10.6028/NIST.SP.800-63-3) . 
    
[^6]:  Rose, Scott, Oliver Borchert, Stu Mitchell, Sean Connelly, “NIST Special Publication 800-207 – Zero Trust Architecture,” National Institute of Standards and Technology, U.S. Department of Commerce, August 2020, [https://doi.org/10.6028/NIST.SP.800-207](https://doi.org/10.6028/NIST.SP.800-207) . 
    
[^7]:  Hutchinson, Steve, “Introduction to Identity Part 2 - June 25,” Identiverse 2019, recording starting minute 27:39, [https://www.youtube.com/watch?v=zxKRUXmTLJs&list=PLpKq7xRiIHaTDwAqpIU1UYpKZY03tfTMf&index=8](https://www.youtube.com/watch?v=zxKRUXmTLJs&list=PLpKq7xRiIHaTDwAqpIU1UYpKZY03tfTMf&index=8) . 
    
[^8]:  Smedinghoff T. J., (2021) “Laws Governing Identity Systems (v2),” _IDPro Body of Knowledge_ 1(5). [https://bok.idpro.org/article/id/8/](https://bok.idpro.org/article/id/8/) . 
    
[^9]:  Temoshak, David, Christine Abruzzi, “NISTIR 8149 - Developing Trust Frameworks to Support Identity Federations,” National Institute of Standards and Technology, U.S. Department of Commerce, January 2018, [https://doi.org/10.6028/NIST.IR.8149](https://doi.org/10.6028/NIST.IR.8149) . 
    
[^10]:  “Shared Signals and Events WG” [https://openid.net/wg/sse/](https://openid.net/wg/sse/) (Accessed 28 November 2022). 
    
[^11]:  Sakimura, N., J. Bradley, M. Jones, E., Jay, “OpenID Connect Discovery 1.0 incorporating errata set 1,” OpenID Foundation, 8 November 2014, [https://openid.net/specs/openid-connect-discovery-1\_0.html](https://openid.net/specs/openid-connect-discovery-1_0.html) (accessed 28 November 2022). 
    
[^12]:  Widdowson, Rod, Scott Cantor, “Identity Provider Discovery Service Protocol and Profile,” OASIS Committee Specification 01, 27 March 2008, [https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-idp-discovery.pdf](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-idp-discovery.pdf) (accessed 28 November 2022). 
