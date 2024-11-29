---
layout: columns
title: Introduction to IAM Architecture (v2)
permalink: /docs/oidc_oauth/idpro_bok/38
date: 2024-09-09
modify_date: 2024-11-19
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "アクセス管理", "アーキテクチャ", "アイデンティティライフサイクル"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/38/](https://bok.idpro.org/article/id/38/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

In this section of the BoK, you will explore several conceptual architectures and how they enable IAM solutions across your enterprise. IAM touches all aspects of an organization’s IT environment whether it’s the HR system, email system, phone system or corporate applications, they all need to interface to the IAM environment. Whether it is by supporting the enforcement of user provisioning rules or validating the access of non-corporate users, IAM will always play a role in making IT operations efficient and secure. An architectural approach will heighten the probability that a consistent and comprehensive IAM solution will be achieved.

Keywords: Identity, Access Management, Architecture, Identity Lifecycle

@column
## 概要

BoKのこのセクションでは、いくつかの概念アーキテクチャと、それらがどのように企業でIAMソリューションを実現するのかについて探求します。人事システム、Eメールシステム、電話システムまたは企業アプリケーションであれ、それらすべてがIAM環境とのインタフェースを必要とすることから、IAMは組織のIT環境のすべての側面に関与します。ユーザープロビジョニングルールの実施をサポートすることであれ、企業外のユーザーのアクセスを検証することであれ、IAMは常にITオペレーションの効率化とセキュリティ向上の役割を果たします。アーキテクチャアプローチは、一貫性のある包括的なIAMソリューションが達成される可能性を高くします。

Keywords: アイデンティティ, アクセス管理, アーキテクチャ, アイデンティティライフサイクル

@row
By Andrew Cameron and Graham Williamson

© 2021 Andrew Cameron, Graham Williamson, IDPro

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code)._

_Note: IDPro® does not endorse a particular architecture framework. IAM practitioners will face many different approaches and must adopt the model that best suits their organizations._

@row
## Introduction

Identity and Access Management (IAM) touches all aspects of an organization’s IT environment. Whether it is the human resources (HR) system, email system, phone system, or corporate applications, each system needs to interface to the IAM environment. IAM will always play a role in making IT operations efficient and secure, by supporting the enforcement of user provisioning rules, as an example, or validating the access of non-corporate users. An architectural approach to developing IAM systems will heighten the organization’s probability of achieving a consistent and comprehensive IAM solution.

If the organization maintains an enterprise architecture (EA), any IAM solution they deploy must adhere to the enterprise models and be reflected in the organization’s EA artifacts. This article provides a basic approach for IAM professionals to consider whether or not there is an EA in place.

@column
## 導入

アイデンティティとアクセス管理（IAM）は、組織のIT環境のあらゆる側面に関与します。人事（HR）システムであれ、Eメールシステムであれ、電話システムであれ、企業アプリケーションであれ、各システムはIAM環境にインターフェースを持つ必要があります。IAMはIT運用を効率的かつ安全にする役割を常に担っており、例としてユーザーのプロビジョニングルールの施行をサポートしたり、企業以外のユーザーのアクセスを検証したりします。IAMシステムを開発するためのアーキテクチャアプローチは、組織が一貫性のある包括的なIAMソリューションを実現する確率を高めます。

組織がエンタープライズアーキテクチャ（EA）をメンテナンスしている場合、デプロイするIAMソリューションはエンタープライズモデルを遵守し、組織のEAアーティファクトに反映させる必要があります。この記事では、IAMの専門家がEAが導入されているかどうかを検討するための基本的なアプローチを提供します。

@row
### Terminology

*   **Access Management**: the use of identity information to provide access control to protected resources such as computer systems, databases, or physical spaces.
    
*   **Architecture**: a framework for the design, deployment, and operation of an information technology infrastructure. It provides a structure whereby an organization can standardize its technology and align its IT infrastructure with digital transformation policy, IT development plans, and business goals.
    
*   **Architecture Overview**: describes the architecture components required for supporting IAM across the enterprise.
    
*   **Architecture Patterns**: identifies the essential patterns that categorize the IT infrastructure architecture in an organization and will guide the deployment choices for IAM solutions.
    
*   **Enterprise Architecture:** an architecture covering all components of the information technology (IT) environment
    
*   **Identity Governance and Administration (IGA):** includes the collection and use of identity information as well as the governance processes that ensure the right person has the right access to the right systems at the right time.
    

@column
### 用語解説

*   **アクセス管理**：コンピュータシステム、データベースまたは物理的空間などの保護されたリソースへのアクセス制御を提供するためのアイデンティティ情報の利用。
    
*   **アーキテクチャ**：情報テクノロジーインフラストラクチャの設計、デプロイ、運用のためのフレームワーク。組織が技術を標準化し、ITインフラをデジタル変革の方針、IT開発計画およびビジネス目標に整合させるための構造を提供します。
    
*   **アーキテクチャ概要**：企業全体でIAMをサポートするために必須のアーキテクチャコンポーネントを説明すること。
    
*   **アーキテクチャパターン**：組織内のITインフラストラクチャアーキテクチャを分類する重要なパターンを特定し、IAMソリューションのデプロイの選択肢をガイドすること。
    
*   **エンタープライズアーキテクチャ**：情報テクノロジー（IT）環境のすべてのコンポーネントをカバーするアーキテクチャ。
    
*   **アイデンティティガバナンスと管理（IGA）**：アイデンティティ情報の収集と使用、および適切な人物が適切なシステムに適切なタイミングで適切にアクセスできるようにするガバナンスプロセスのこと。
    

@row
### Acronyms

*   AP – Application Portfolio
    
*   BPMn – Business Process Mapping notation
    
*   BSA – Business System Architecture
    
*   EA – Enterprise Architecture
    
*   HTTP – HyperText Transfer Protocol
    
*   IA – Information Architecture
    
*   IAM – Identity and Access Management
    
*   IDaaS – Identity-as-a-Service
    
*   IGA – Identity Governance and Administration
    
*   JSON – file structure for the communication of data attributes
    
*   MFA – Multi-factor Authentication
    
*   PABX – Private Automatic Branch Exchange
    
*   PAP – Policy Administration Point
    
*   PDP – Policy Decision Point
    
*   PEP – Policy Enforcement Point
    
*   PIP – Policy Information Point
    
*   RBAC – Role-based Access Control
    
*   RESTful API - architecture for a programming interface defining how HTTP methods are to be used
    
*   SAML – Security Assertion Markup Language
    
*   SCIM – System for Cross-domain Identity Management
    
*   SSO – Single Sign-On
    
*   TA – Technical Architecure
    
*   XML – eXtensible Markup Language - a file structure for the communication of data attributes
    

@column
### 略語

*   AP – アプリケーションポートフォリオ
    
*   BPMn – ビジネスプロセス・モデルと表記法
    
*   BSA – ビジネスシステムアーキテクチャ
    
*   EA – エンタープライズアーキテクチャ
    
*   HTTP – HyperText Transfer Protocol
    
*   IA – インフォメーションアーキテクチャ
    
*   IAM – アイデンティティとアクセス管理
    
*   IDaaS – Identity-as-a-Service
    
*   IGA – アイデンティティガバナンスと管理
    
*   JSON – データ属性のやり取りのためのファイル構造
    
*   MFA – 多要素認証
    
*   PABX – 構内自動交換機
    
*   PAP – ポリシー管理ポイント
    
*   PDP – ポリシー決定ポイント
    
*   PEP – ポリシー実行ポイント
    
*   PIP – ポリシー情報ポイント
    
*   RBAC – ロールベースアクセス制御
    
*   RESTful API - HTTPメソッドの使用方法を定義するプログラミングインターフェイスのアーキテクチャ
    
*   SAML – Security Assertion Markup Language
    
*   SCIM – System for Cross-domain Identity Management
    
*   SSO – シングルサインオン
    
*   TA – テクニカルアーキテクチャ
    
*   XML – eXtensible Markup Language - データ属性のやり取りのためのファイル構造
    

@row
## IAM Architecture Overview

IAM professionals must have a vision for the IAM environment that satisfies corporate requirements. Each IAM project must build towards the desired target state. An architectural approach will enable the IAM professional to plan, design, and deploy IAM solutions that are both coordinated and integrated; and combine to form a comprehensive IAM environment that meets corporate stakeholders' current and projected needs.

Identity management within an enterprise touches virtually all systems in use within the organization. Systems, in this context, comprise computer systems that staff and business partners use in the performance of their job responsibilities and physical access systems, such as a requirement to show an identity pass to gain access to a restricted area. Staff includes contractors; they are typically managed through a different system (many HR systems only accommodate employees) but need access to many of the same corporate systems as employees. Including non-human accounts should also be considered; most organizations have service accounts for machine access to systems. As more automation is incorporated into company operations, access control for sensors or bots should be incorporated in the IAM environment. Including non-human entities in the architecture allows the enterprise to manage their access control in a manner consistent with all other accounts; IAM professionals should consider these entities during the system development planning process.

It is the task of an IAM practitioner to ensure that, wherever and whenever identity information is used within an enterprise, the information is collected and used in a properly designed environment that ensures efficiency, protects privacy, and safeguards integrity. Applying an architectural approach, i.e., developing project requirements within a structured framework, will significantly raise the likelihood that an IAM project will be completed consistently and comprehensively with a controlled impact on stakeholders.

There are four levels that the IAM practitioner should consider when developing a solution architecture:

@column
## IAMアーキテクチャ概要

IAMの専門家は、企業の要件を満たすIAM環境のビジョンを持っている必要があります。各IAMプロジェクトは、望ましい目標状態に向けて構築する必要があります。アーキテクチャアプローチにより、IAM専門家は、調整および統合されたIAMソリューションを計画、設計、デプロイし、企業のステークホルダーの現在および将来のニーズを満たす包括的なIAM環境を形成するために組み合わせることになります。

企業内のアイデンティティ管理は、組織内で使用される事実上すべてのシステムに関係します。ここでいうシステムとは、スタッフおよびビジネスパートナーが職責を果たすために使用するコンピュータシステムと、制限区域にアクセスするためにアイデンティティパスの提示を要求するような物理的なアクセスシステムです。スタッフには業務委託者も含まれます；彼らは通常、別のシステムで管理されますが（多くの人事システムは従業員のみを対象としている）、従業員と同じ企業システムの多くにアクセスする必要があります。また、人間以外のアカウントも考慮する必要があります；ほとんどの組織では、機械からシステムにアクセスするためのサービスアカウントを持っています。企業運営に自動化が進むにつれて、センサーやボットに対するアクセス制御をIAM環境に取り入れる必要があります。人間以外のエンティティをアーキテクチャに含めることで、企業は他のすべてのアカウントと一律の方法でそのアクセス制御を管理できます；IAMの専門家は、システム開発の計画プロセスでこれらのエンティティを考慮する必要があります。

アイデンティティ情報が企業内で使用されるときはいつでもどこでも、効率性を確保し、プライバシーを保護し、完全性を保証する適切に設計された環境で情報が収集および使用されるようにすることは、IAM実践者の仕事です。アーキテクチャアプローチ、すなわち構造化されたフレームワーク内でプロジェクト要件を作成することを適用すると、IAMプロジェクトがステークホルダーへの影響を制御し、一貫して包括的に完了する可能性が大幅に高まります。

IAM実践者がソリューションアーキテクチャを開発する際に考慮すべき4つのレベルがあります：

@row
![Simple configuration with a Mainframe application accessed from a monitor ](/assets/images/idpro_bok/image1.png)

Figure 1: Generic Enterprise Architecture Framework

@row
### Business System Architecture (BSA)

Mapping business processes for the collection, usage, and eventual deletion of identity data will greatly assist in understanding the breadth of the IAM task. While BPMn is typically used for business process mapping, the IAM practitioner should adopt whatever tool is typically used in their company.

Considering IT architecture at the business level will facilitate a more holistic approach that considers the identity requirements of all connected systems and ensures consistency in naming conventions. It will also reduce the probability of an IAM project running over budget or over time (a common occurrence when a system owner who has not previously been consulted hears about an IAM project and adds unanticipated requirements).

@column
### ビジネスシステムアーキテクチャ（BSA）

アイデンティティデータの収集、使用、最終的な削除のビジネスプロセスをマッピングすると、IAMのタスクの幅を理解するのに大いに役立ちます。BPMnは通常、ビジネスプロセスのマッピングに使用されますが、IAM実践者は、会社で一般的に利用されているツールを採用するべきです。

ITアーキテクチャをビジネスレベルで考えることは、接続されたすべてのシステムのアイデンティティ要件を考慮し、命名規則の一貫性を保証し、より包括的なアプローチを容易にすることでしょう。また、IAMプロジェクトが予算や時間を超過して実行される可能性を低下させます（IAMプロジェクトについて事前に相談を受けていないシステムオーナーが、予期せぬ要件を追加するときによく起きる出来事です）。

@row
### Information Architecture

It is important to map the identity data elements required by the various applications to the IAM collection, management, and governance systems. This mapping will ensure no application is ‘left behind’ when the IAM systems are re-developed. A useful tool is an ‘entity-relationship diagram’ that maps each attribute collected to each system that requires it. The Information Architecture (IA) should drive consistency between connected systems (e.g., should Firstname, Middle Initial, and Lastname be used, or should Common name, Lastname be used). It should also help define roles (e.g., is this role for a Payroll Clerk or a Financial Officer). The IA should nominate attribute authority (e.g., which system is the authority for phone numbers). Best practice is for the IAM system to be the ‘source of truth’ for identity information in the company (sometimes called the ‘book of record’) because it is typically bad practice for source systems (HR, PABX, etc.) to be queried for data attribute lookups.

The IA becomes the vehicle for ‘identity data orchestration.’ It is the master plan for the collection and use of identity data within an enterprise.

@column
### インフォメーションアーキテクチャ

さまざまなアプリケーションで必要とされるアイデンティティデータ要素を、IAMの収集、管理およびガバナンスのシステムにマッピングすることは重要です。このマッピングにより、IAM システムの再開発時にアプリケーションが「取り残される」ことがなくなります。収集された各属性を、その属性を必要とする各システムにマッピングする「エンティティ関係図」は、便利なツールです。インフォメーションアーキテクチャ（IA）は、接続されたシステム間の一貫性を推進すべきです（例えばファーストネーム、ミドルネーム、ラストネームを使用するか、通称名、ラストネームを使用するか）。 また、ロールを定義するのにも役立ちます（例えば、このロールは給与事務担当者または財務担当者のどちらのためか）。IAは属性の権限を指定する必要があります（例 どのシステムが電話番号の権限を持っているか）。ベストプラクティスは、IAMシステムを企業内のアイデンティティ情報の「信頼できる情報源」にすることです（「記録簿」と呼ばれることもあります）。これは、情報源となるシステム（HR、PABXなど）に対してデータ属性検索を問い合わせることは、一般的に不適切な方法であるためです。

IAは、「アイデンティティ情報オーケストレーション」の手段となります。これは、企業内でアイデンティティデータを収集および使用するためのマスタープランとなります。

@row
### Application Portfolio

An inventory of applications to be included in the IAM project should be conducted.[^1] How current are they? Are any of the included applications under development? Will the IAM project materially change how each application interacts with the IAM environment? For instance, if an API gateway is being deployed for access to IAM attributes, any application redevelopment should migrate from existing authentication mechanisms to the gateway operation.

A company’s Application Portfolio (AP) becomes an inventory of corporate applications. The record for each application should identify the system owner, type of application (web app, client-server, mainframe, etc.), and its reliance on the IAM environment. Some applications will expect the IAM system to pass authenticated sessions to it. In contrast, others will require user attributes so that it can determine the authorization that a user has to application functionality. The AP should identify the level of integration between each relying application and the IAM system. Web applications will likely pass user requests and responses via HTTP headers. In other scenarios, client-server applications may use an API, while cloud applications may use a SAML request or, if it maintains its own data repository, the SCIM protocol.[^2]

The AP becomes an important record for an organization because it facilitates the planning required as applications are updated.

@column
### アプリケーションポートフォリオ

IAMプロジェクトに含まれるアプリケーションの一覧を作成する必要があります。 [^1] それらはどれくらい最新ですか？含まれるアプリケーションの中に開発中のものが含まれていますか？IAMプロジェクトは、各アプリケーションがIAM環境と連携する方法を大幅に変えますか？例えば、IAM属性へのアクセスのためにAPIゲートウェイを導入する場合、アプリケーションの再開発は、既存の認証メカニズムからゲートウェイ運用に移行する必要があります。

企業のアプリケーションポートフォリオ（AP）は、企業のアプリケーションの一覧となります。各アプリケーションのレコードは、システム所有者、アプリケーションの種類（Webアプリ、クライアントサーバー、メインフレームなど）、IAM環境への依存度を特定する必要があります。一部のアプリケーションは、IAMシステムが認証されたセッションを渡すことを期待します。対照的に、他のアプリケーションは、アプリケーションの機能に対してユーザーが保持する認可を決定できるように、ユーザー属性を必要とします。APは、各依存アプリケーションとIAMシステムとの間の結合の度合いを特定する必要があります。Webアプリケーションは、HTTPヘッダを介してユーザーのリクエストとレスポンスを渡すでしょう。他のシナリオでは、クライアントサーバアプリケーションはAPIを使用し、クラウドアプリケーションはSAMLリクエストまたは、独自のデータリポジトリを保持している場合はSCIMプロトコルを使用することがあります。 [^2]

APは、アプリケーションのアップデート時に必要な計画を容易にするため、組織にとって重要な記録となります。

@row
### Technical Architecture

The Technical Architecture (TA) describes, among other things, the technical environment to be supported by the IAM environment. This description will involve understanding the patterns used within the company. Most organizations will have “n-tier” web services and hybrid cloud patterns, but there might still be client-server patterns and potentially mainframe hub-and-spoke patterns. Each additional pattern to be supported will increase the complexity and cost of the project. Often IAM environments with older infrastructure leave out support for legacy technology due to cost considerations, but this fragments the IAM task. Properly constituted, a cost/benefit analysis for deploying legacy connectors will typically be successful.

The TA impacts the IAM environment because different solutions are required for different patterns. For example, a web services pattern will mandate a single sign-on (SSO) environment capable of supporting RESTful APIs and SAML assertions and passing identity attributes in JSON arrays or XML files. An on-premise Windows environment, as another example, will typically use the Kerberos authentication protocol from an AD infrastructure or an LDAP directory. A cloud environment will often require a SAML operation or an Identity-as-a-Service (IDaaS) offering, whereas an older directory should be supported via a connector from the IAM infrastructure.

Additionally, corporate security policy may create requirements that require certain technical decisions. For instance, a requirement to maintain full control and authority over the data and infrastructure may require hosting the entire identity management stack on premises.

@column
### テクニカルアーキテクチャ

テクニカルアーキテクチャ（TA）は、特にIAM環境でサポートされる技術環境を記述します。この記述には、企業内で使用されているパターンを理解することが含まれます。ほとんどの組織では、「nティア」Webサービスとハイブリッドクラウドのパターンがありますが、クライアントサーバーのパターンや、メインフレームのハブ・アンド・スポークのパターンが残っている可能性があります。対応するパターンが増えるたびに、プロジェクトの複雑さとコストは増加します。古いインフラストラクチャを持つIAM環境では、コストを考慮してレガシーテクノロジーのサポートを省くことがよくありますが、これはIAMのタスクを断片化します。適切に構成すれば、レガシーコネクタを導入するためのコスト/利益分析は、通常成功します。

TAはIAM環境に影響を与えますが、これはパターンによって異なるソリューションが必要とされるためです。たとえば、Webサービスのパターンでは、RESTful APIとSAMLアサーションをサポートし、アイデンティティ属性をJSON配列またはXMLファイルで渡すことができるシングルサインオン（SSO）環境が必須となります。他にも、オンプレミスのWindows環境では、通常、ADインフラストラクチャまたはLDAPディレクトリからKerberos認証プロトコルが使用されます。クラウド環境では、SAML運用またはIdentity-as-a-Service（IDaaS）提供が必要になることが多いですが、古いディレクトリはIAMインフラからコネクタを介してサポートされる必要があります。

さらに、企業のセキュリティポリシーによって、特定の技術的な決定を必要とする要件が生じることがあります。例えば、データとインフラストラクチャに対しての完全なコントロールと権限を維持するという要件がある場合、アイデンティティ管理スタック全体をオンプレミスでホスティングする必要があるかもしれません。

@row
## Architectural Approach

It is an unfortunate fact that many IAM (identity and access management) projects exceed their scheduled time and budget. The usual reason for this is a misunderstanding of the extent of the project and the systems impacted. The project team tends to focus just on the task at hand, e.g., installing the IAM software package, without realizing that IAM systems within an enterprise touch virtually all other systems in use within the organization. These other systems might include a birthright system such as email, an administrative system such as the Financial Management system, or an operational system such as an Enterprise Resource Management system.

In some circumstances, the change caused by an IAM project will be minimal, with a limited impact on resources. In other cases, the change will be significant, impacting both infrastructure and personnel across the organization. An architectural approach will ensure that a solution architecture is developed for each IAM project to understand the extent of the work required and effectively plan for the change it will generate.

An IAM practitioner's task is to ensure that, wherever and whenever identity information is used within an enterprise, the information is collected and used in a properly designed environment that ensures efficiency, protects privacy, and safeguards integrity.

For organizations with an EA, understanding how information is collected and used should be quite easy, as it is fundamentally a part of how the systems are deployed. For other organizations, the environment will be a “greenfield,” allowing the IAM practitioner to develop their own architectural approach.

@column
## アーキテクチャアプローチ

多くのIAM（アイデンティティとアクセス管理）プロジェクトが、予定した期間と予算を超過しているのは残念な事実です。その原因は、プロジェクトの範囲や影響を受けるシステムに対する誤解にあることがほとんどです。プロジェクトチームは、IAMソフトウェアパッケージのインストールなど、目の前のタスクだけに集中しがちですが、企業内のIAMシステムが組織内で使用されているほぼすべての他のシステムに関与していることに気づいていないのです。これらの他のシステムには、電子メールなどの基本的なシステム、財務管理システムなどの経営に必要なシステム、または企業資源管理システムなどの運用システムが含まれる場合があります。

状況によっては、IAMプロジェクトによる変更は最小限にとどまり、リソースへの影響も限定的なものになります。一方、変化が大きく、組織全体のインフラストラクチャと人員の両方に影響する場合もある。アーキテクチャアプローチにより、IAMプロジェクトごとにソリューションアーキテクチャが開発され、必要な作業の範囲を理解し、それによって生じる変更を効果的に計画できるようになります。

IAM実践者のタスクは、企業内でアイデンティティ情報を使用する場合、いつでもどこでも、情報が効率性を確保し、プライバシーを保護し、完全性を保護するように適切に設計された環境で収集および使用されることを保証することです。

EAを導入している組織では、情報がどのように収集され使用されるかを理解することは、基本的にシステムのデプロイ方法の一部であるため、非常に簡単です。他の組織では、環境は「グリーンフィールド」となり、IAM実践者は独自のアーキテクチャアプローチを開発することができます。

@row
### Architecture Patterns

At the Technical Architecture level, a “pattern” approach is useful to understand the supported technology within an organization. For instance: what is the predominant server infrastructure – is it Linux or Windows or both? What server operating system versions are supported? Are VMs used? What is the support for cloud infrastructure – public, private, hybrid? Is AWS, Azure, or Google Cloud supported? Can the scale required for customer IAM be accommodated? For IoT devices – how does the IoT platform integrate with the corporate environment?

The TA will define the computer system “patterns” to be supported by the IAM environment within an organization. For young companies, this will be web-based patterns, either “2-tier” or “n-tier.” Increasingly managed cloud environments are being engaged, potentially with a micro-services approach. But for mature organizations, there will typically be legacy applications with a client-server pattern, or even a mainframe ‘hub and spoke’ pattern, with PCs running terminal emulator software.

The IAM environment must support the selected patterns and ensure a managed approach that adheres to the organization’s governance and cybersecurity policy.

@column
### アーキテクチャパターン

テクニカルアーキテクチャのレベルでは、組織内でサポートされている技術を理解するために「パターン」アプローチが有用です。例：主要なサーバーインフラストラクチャは何か、LinuxかWindowsか、あるいは両方か？どのようなサーバーオペレーティングシステムのバージョンがサポートされているか？VMは使用されているか？クラウドインフラストラクチャのサポートはどうなっているか - パブリック、プライベート、ハイブリッド？AWS、Azure、Google Cloudはサポートされているか？カスタマーIAMに必要な規模に対応できますか？IoTデバイスの場合には、IoTプラットフォームはどのように企業環境と統合されるか？

TAでは、組織内のIAM環境がサポートするコンピュータシステムの「パターン」を定義します。若い企業では、これはWebベースのパターンであり、「2層」または「N層」のいずれかになります。管理されるクラウド環境はますます増えており、マイクロサービスアプローチを採用する可能性もあります。しかし、成熟した企業では、クライアントサーバー型のレガシーアプリケーションや、メインフレームの「ハブ・アンド・スポーク」型、ターミナルエミュレーターソフトウェアを実行するPCが一般的でしょう。

IAM環境は、選択したパターンをサポートし、組織のガバナンスとサイバーセキュリティポリシーに準拠した管理されたアプローチを確保する必要があります。

@row
#### Host

There are few mainframe systems left in service, with notable exceptions in the banking industry and some government installations. The IAM environment will often be required to synchronize to an older data store to support a mainframe system.

@column
#### ホスト

銀行業界や一部の政府施設での例外を除き、現役で残っているメインフレームシステムはほとんどありません。IAM環境は、メインフレームシステムをサポートするために、古いデータストアに同期することが必要になることがよくあります。

@row
![Simple configuration with a Mainframe application accessed from a monitor ](/assets/images/idpro_bok/image2.png)

Figure 2: Mainframe application accessed from a monitor

@row
### Client-Server

Client-server environments can present a complex support requirement since many such systems maintain their own identity database to provide fine-grained access control to system functionality. Redevelopment of a client-server application to externalize access control decisions to an authentic authorization server can be a way to harmonize access policies across an organization.

@column
### クライアントサーバー

クライアントサーバー環境では、システム機能へのきめ細かなアクセス制御をおこなうために、多くのシステムが独自のアイデンティティデータベースを保持しているため、複雑なサポート要件が存在する可能性があります。クライアントサーバーアプリケーションを再開発し、アクセス制御の決定を認可サーバーに外部化することは、組織全体のアクセスポリシーを調和させる方法となり得ます。

@row
![Simple client-server network diagram](/assets/images/idpro_bok/image3.png)

Figure 3: Client application access a backend server

@row
#### N-tier

The most common on-premise application environment these days is an “n-tier” web services infrastructure. While there are many variants, a user accessing the front-end web server will be redirected to an authentication service, usually supporting SSO, with an authentication token passed back to the application in an HTTP header. If the application requires user authentication, the IAM system should set user entitlements as part of the initial provisioning activity when a user joins the organization.

@column
#### Nティア

近年、最も一般的なオンプレミスアプリケーション環境は、「nティア」のWebサービスインフラストラクチャです。多くのバリエーションがありますが、フロントエンドのWebサーバーにアクセスするユーザーは、通常SSOをサポートする認証サービスにリダイレクトされ、HTTPヘッダーで認証トークンがアプリケーションに引き渡されます。アプリケーションがユーザー認証を必要とする場合、IAMシステムは、ユーザーが組織に参加するときの最初のプロビジョニング活動の一部として、ユーザーエンタイトルメントを設定する必要があります。

@row
![Diagram of client machine connecting through the network to the presentation and application servers as well as the database system.](/assets/images/idpro_bok/image4.png)

Figure 4: Common web-services model

@row
#### Hub & Spoke

Hub and spoke systems are typically only in large transaction processing systems. Often the only IAM touchpoint is access control for DevOps staff via a privileged access management system.

@column
#### ハブ・アンド・スポーク

ハブ・アンド・スポークシステムは一般的に大規模なトランザクションシステムでのみ利用されます。 しばしば、唯一のIAMタッチポイントは特権アクセス権管理システムを経由したDevOpsスタッフに対するアクセス制御です。

@row
![Two client systems connecting through the network to the "ETL" host, which in turn connects to an Internal and an external database](/assets/images/idpro_bok/image5.png)

Figure 5: Common data service configuration

@row
#### Remote Access

Increasingly remote access to corporate systems must be supported. The authentication server must accommodate the required access control mechanisms, from basic LDAP lookups for password accounts to sophisticated MFA environments capable of elevating authentication levels to suit application security requirements. The provisioning task in such environments requires maintaining one or more identity provider services within the enterprise.

@column
#### リモートアクセス

企業内システムへのリモートアクセスをサポートする必要性が高くなっています。認証サーバーは、パスワードを利用しているアカウント向けの基本的なLDAPルックアップからアプリケーションのセキュリティ要求事項に対応するために認証レベルを上げられる高度なMFA環境まで、必要なアクセス制御メカニズムに対応しなければなりません。そのような環境でのプロビジョニングは、企業内で1つ以上のアイデンティティプロバイダーサービスをメンテンナンスする必要があります。

@row
![Typical enterprise model providing external, remote devices access to corporate applications via a web application firewall or VPN](/assets/images/idpro_bok/image6.png)

Figure 6: Typical enterprise network access model

@row
#### Hybrid Cloud Identity

A key indicator of effectiveness in an IAM Architecture is how complexity is managed across the IAM components in the environment. Today, most organizations are leveraging cloud infrastructure platforms in some capacity, either private clouds provided by their technology partners or public clouds such as AWS, Azure, or Google. This raises the issue of how to establish identity as a common control plane between the on-premises environment and the cloud infrastructure. IAM is a critical component of a hybrid IT architecture. Hybrid IAM allows organizations to establish a common credential that can be enabled for access to resources in either on-premises or cloud environments.

The hybrid cloud example assumes an existing ‘source of truth’ to which all enterprise users authenticate; this is typically Active Directory. With the Hybrid IAM pattern, authenticated on-premise users will have access to on-premise, public cloud, or other external services that support common identity standards such as OpenID Connect or OAuth.

@column
#### ハイブリッドクラウドアイデンティティ

IAMアーキテクチャの有効性の重要な指標は、環境内のIAMコンポーネントの複雑性がどのように管理されるかです。今日、ほとんどの組織がテクノロジーパートナが提供するプライベートクラウドかAWS、AzureまたはGoogleのようなパブリッククラウドなど、ある程度はクラウドインフラストラクチャプラットフォームを利用しています。この状況は、オンプレミス環境とクラウドインフラストラクチャとの間で一般的な制御プレーンとしてアイデンティティを確立する方法が課題となります。IAMは、ハイブリッドITアーキテクチャの重要なコンポーネントです。ハイブリッドIAMは、組織がオンプレミスまたはクラウド環境のリソースにアクセスすることを許可する一般的なクレデンシャルを生成することを可能にします。

ハイブリッドクラウドの例では、全ての企業内ユーザが認証をおこなう既存の「信頼できる情報源」、一般的にはActive Directoryを想定しています。ハイブリッドIAMパターンでは、認証されたオンプレミスユーザはオンプレミス、パブリッククラウドそしてOpenID ConnectやOAuthのような一般的なアイデンティティ標準仕様をサポートするその他外部サービスへのアクセス権を有しています。

@row
![Hybrid Cloud diagram](/assets/images/idpro_bok/image7.png)

Figure 7: Hybrid Cloud Identity Architecture model

@row
Table 1: Hybrid IAM Architecture components

| Component | Description |
| --- | --- |
| On-Premise (Corporate) Directory | Directory service that enables authentication to access enterprise resources (e.g., Active Directory). Typically contains directory objects (accounts) that represent a human (user account) or non-human identity (service account). |
| On-Premise Federation Service | Identity service that implements common access management capabilities (authentication and authorization) for enterprise applications. Typically supports identity standards like SAML or OpenID Connect to enable access to internal or external resources. |
| Identity Sync Service | Infrastructure service that monitors directory objects in the enterprise directory for changes and synchronizes changes to a mapped cloud directory object. Sync direction can be one-way or two-way but is typically implemented in an Enterprise to Cloud direction to minimize risk and complexity. Standards such as SCIM can be used for this data transfer. |
| Cloud IAM Service | Platform service in a public cloud that implements core IAM capabilities (Authentication, Federation, Access Management) and can be leveraged to access on-premise resources as well. |

Important considerations for Hybrid IAM:

*   User Provisioning: User objects can be configured to synchronize when added to either the cloud or the on-premises environment. The best practice is to restrict user provisioning to one environment and sync account and profile data to the other environment (typically from enterprise to the cloud).
    
*   Profile Data: Manually maintaining identities in more than one environment can add unnecessary complexity and risk to your security posture. Cloud identity objects may not need the entire set of user profile data available for an on-premises user; the IAM practitioner should take care (e.g., understand the business requirements for authentication) when deciding how much user profile data should be stored on a cloud user object. A principle of “least privilege” should be applied to avoid data spillage.
    
*   Single Sign-On: Cloud IAM environments can enable SSO to on-premises applications or services. For SSO to be successful, the user object must have been provisioned and enabled for sign-in. It is critical to understand the authentication scenarios available from the cloud IAM platform (e.g., pass-through authentication or federation) and ensure that there is a fit with the enterprise requirements.
    

As enterprises place increasing importance on “time to value”, a hybrid IAM architecture will be critical to support infrastructure expansion beyond the enterprise perimeter and leverage cloud-enabled benefits (e.g., agility, scalability, reliability). The IAM professional will find use-cases where IDaaS solutions offer rapid deployment and appealing software update methods, when compared as an alternative to on-premises solutions. However, hybrid scenarios may require both types of deployments, cloud and on-premise, to working together. In some cases, the cloud identity service will be the ‘source of truth’ for identity data within the organization. Such an IDaaS approach can reduce the overhead of managing on-premise infrastructure for an enterprise, an activity that can be costly and inflexible.

@column
Table 1: ハイブリッドIAMアーキテクチャコンポーネント

| コンポーネント | 説明 |
| --- | --- |
| オンプレミス（企業内）ディレクトリ | エンタープライズリソースにアクセスするための認証を可能にするディレクトリサービス（例、Active Directory）。通常、人間（ユーザーアカウント）または非人間のアイデンティティ（サービスアカウント）を表すディレクトリオブジェクト（アカウント）が含まれます。 |
| オンプレミスフェデレーションサービス | エンタープライズアプリケーションに対する共通のアクセス管理機能（認証と認可）を実装するアイデンティティサービス。通常、SAMLやOpenID Connectなどのアイデンティティ標準仕様をサポートして、内部または外部のリソースへのアクセスを可能にします。 |
| アイデンティティ同期サービス | エンタープライズディレクトリ内のディレクトリオブジェクトの変更を監視し、マッピングされたクラウドのディレクトリオブジェクトに変更を同期するインフラストラクチャサービス。同期の方向は一方向も双方向もありますが、リスクと複雑さを最小限に抑えるために、通常はエンタープライズからクラウドへの方向で実装されます。このデータ転送には、SCIMなどの標準仕様が利用されます。 |
| クラウドIAMサービス | コアIAM機能（認証、フェデレーション、アクセス管理）を実装し、オンプレミスリソースへのアクセスにも利用できるパブリッククラウドのプラットフォームサービス。 |

ハイブリッドIAMにとっての重要な考慮事項は以下の通りです：


*   ユーザープロビジョニング：ユーザーオブジェクトは、クラウドまたはオンプレミス環境のいずれかに追加されたときに同期するように構成することができます。ベストプラクティスは、ユーザープロビジョニングを一方の環境に限定し、アカウントとプロファイルのデータをもう一方の環境（通常はエンタープライズからクラウドへ）に同期させることです。
    
*   プロファイルデータ：複数の環境でアイデンティティを手動で管理すると、セキュリティ態勢に不必要な複雑さとリスクが追加されます。クラウドアイデンティティオブジェクトは、オンプレミスユーザーにとって一連のすべてのユーザープロファイルデータを入手する必要はないかもしれません：IAM実務者は、クラウドのユーザーオブジェクトに保存すべきユーザープロファイルデータの量を決定する際に（例えば、認証のビジネス要件を理解するなど）注意を払う必要があります。データ流出を避けるために、「最小特権」の原則を適用する必要があります。
    
*   シングルサインオン：クラウドIAM環境では、オンプレミスのアプリケーションやサービスに対してSSOを有効にすることができます。SSOが成功するためには、ユーザーオブジェクトがプロビジョニングされ、サインインが有効になっていなければなりません。クラウドIAMプラットフォームから利用できる認証シナリオ（例、パススルー認証やフェデレーションなど）を理解し、企業要件に適合していることを確認することが重要です。
    

企業が「価値実現までの時間」を重視するようになるにつれ、ハイブリッドIAMアーキテクチャは、企業の境界を超えたインフラストラクチャの拡大をサポートし、クラウド対応のメリット（例、敏捷性、拡張性、信頼性など）を活用するために不可欠となるでしょう。IAM実務者は、オンプレミスのソリューションと比較して、IDaaSソリューションが迅速なデプロイと魅力的なソフトウェア更新方法を提供するユースケースを見出すことができます。しかし、ハイブリッドシナリオでは、クラウドとオンプレミスの両方のタイプのデプロイメントを一緒に使用する必要があります。場合によっては、クラウドアイデンティティサービスが組織内のアイデンティティデータの「信頼できる情報源」となることもあります。このようなIDaaSアプローチは、企業のオンプレミスインフラストラクチャの管理という、コストと柔軟性に欠けるオーバーヘッドを削減することができます。

@row
## Applying an Architectural Approach

An architectural approach can be taken to an IAM project regardless of whether it is in the collection and management of identity information or access management, using identity information for access control to protected resources.

@column
## アーキテクチャアプローチの適用

保護されたリソースに対するアクセス制御にアイデンティティ情報を利用することで、IAMプロジェクトがアイデンティティ情報の収集および管理またはアクセス管理であるかに関係なく、アーキテクチャアプローチを適用することができます。

@row
### Identity Governance and Administration

Identity Governance and Administration (IGA) covers the identity management side of IAM, e.g., the ‘admin-time’ events that establish user entitlements, as opposed to ‘real-time’ events that occur when users request access to protected resources. IGA combines administration and governance over the collection, use, and disposal of identity information. It requires a governance facility that enables managers to certify the entitlements that their staff have been granted. In addition, IGA typically includes monitoring and reporting functions for identity services that, in turn, support corporate requirements.

IGA systems support:

*   Administering accounts and credentials
    
*   Identity and account provisioning
    
*   Managing entitlements
    
*   Segregation of duties
    
*   Role management
    
*   Analytics and reporting
    

IGA systems provide additional functionality beyond standard IAM systems. In particular, they help organizations meet compliance requirements and enable them to audit access for compliance reporting. They also automate workflows for tasks such as access approvals and provisioning/deprovisioning.

@column
### アイデンティティガバナンスと管理

アイデンティティガバナンスと管理（IGA）は、IAMのアイデンティティ管理の側面を対象としており、保護されたリソースへのアクセスをユーザーがリクエストしたときに発生する「リアルタイム」イベントとは対照的に、ユーザーエンタイトルメントを確立する「管理時間」イベントがその例です。IGAは、アイデンティティ情報の収集、使用、および廃棄に関する管理とガバナンスを組み合わせたものです。それには、マネージャーが自分のスタッフに与えられたエンタイトルメントを認定できるガバナンス機能が必要です。さらに、IGAには通常、企業の要件をサポートするアイデンティティサービスの監視およびレポート機能が含まれています。

IGAシステムは以下をサポートします：

*   アカウントおよびクレデンシャルの管理
    
*   アイデンティティとアカウントのプロビジョニング
    
*   エンタイトルメントの管理
    
*   職務分掌
    
*   ロール管理
    
*   分析とレポート
    

IGAシステムは標準IAMシステムを超える追加の機能を提供します。特に、組織がコンプライアンス要件を満たすことと、コンプライアンスレポートのためのアクセス監査を可能にすることに役立ちます。また、アクセス承認やプロビジョニング／デプロビジョニングのようなタスクのワークフローを自動化します。

@row
#### Identity Lifecycle

The business rules that tie these elements together are generally referred to as the identity lifecycle.[^3] In the identity lifecycle, an identity is created that defines who or what (human or non-human) needs access to a protected resource. Every stage of the identity lifecycle sees the activities of the identity managed to ensure business rules are enforced according to the identity and security rules of the enterprise.

@column
#### アイデンティティライフサイクル

これらの要素を結びつけるビジネスルールは、一般にアイデンティティライフサイクルと呼ばれます。 [^3] アイデンティティライフサイクルでは、保護されたリソースにアクセスする必要がある誰かまたは何か（人間または被人間）を定義するアイデンティティが作成されまさう。アイデンティティライフサイクルの各段階では、企業のアイデンティティおよびセキュリティ規則に従ってビジネスルールが実施されるように、アイデンティティの活動が管理されます。

@row
![A graphic of the Identity Lifecycle, starting with Identity Onboarding, then Identity Management, Account Management, Entitlement Management, and Access Management.](/assets/images/idpro_bok/image8.png)

Figure 8: Identity Lifecycle Categories

@row
#### IGA System Components

Identity governance and administration tools help facilitate identity lifecycle management.

IGA systems generally include the following components for identity administration:

*   **Password management**: using tools like password vaults or, more often, SSO, IGAs ensure users don’t have to remember many different passwords to access applications.
    
*   **Integration connectors**: used to integrate with directories and other systems that contain information about users and the applications and systems they have access to, as well as their authorization in those systems.
    
*   **Access request approval workflows**: support the automation of a user’s request for access to applications and systems and ensures all access is properly authorized.
    
*   **Automated de-provisioning**: supports the removal of a user’s entitlement to access an application when the user is no longer authorized to access a system.
    
*   **Attestation reporting**: used to periodically verify user entitlements in various applications (such as add, edit, view, or delete data) and is usually sent to a user’s manager.
    
*   **Recertification of user entitlements**: often a response to an attestation report, recertification of user entitlements involves recording a manager’s approval of their staff’s system access. If access is no longer required, this shifts to automatic de-provisioning.
    
*   **Segregation of duties**: rules that prevent risky sets of access from being granted to a person. For example, if a person has the ability to both view a corporate bank account and transfer funds to outside accounts, this might enable a user to transfer money to a personal account.
    
*   **Access reviews**: reviews include tools that streamline the review and verification (or revocation) of a user’s access to different apps and resources. Some IGA tools also provide discovery features that help identify entitlements that have been granted.
    
*   **Role-based management**: also known as Role-based Access Control (RBAC), this includes defining and managing access through user roles.
    
*   **Analytics and reporting**: include tools that log activities, generate reports (including for compliance), and provide analytics to identify issues and optimizations.
    

@column
#### IGAシステムコンポーネント

アイデンティティガバナンスと管理のツールは、アイデンティティライフサイクル管理を促進する助けになります。

一般的に、IGAシステムはアイデンティティ管理のために以下のコンポーネントを有しています：

*   **パスワード管理**：パスワード保管庫またはSSOなどのツールを使用し、IGAはユーザーがアプリケーションにアクセスするためにたくさんの異なるパスワードを覚えておく必要がないようにします。

*   **インテグレーションコネクター**：ユーザーに関する情報やそのユーザーがアクセスするアプリケーションやシステムに関する情報、およびそれらのシステムでの認可をおこなうディレクトリやその他のシステムと統合するために使用されます。
    
*   **アクセスリクエスト承認ワークフロー**：ユーザーによるアプリケーションおよびシステムへのアクセスのリクエストを自動化することを助け、すべてのアクセスが適切に認可されるようにします。
    
*   **自動デプロビジョニング**：ユーザーがシステムへのアクセスを認可されなくなったとき、アプリケーションへアクセスするためのユーザーのエンタイトルメントを削除することを助けます。
    
*   **アテステーションレポート**：各種アプリケーションにおけるユーザーのエンタイトルメント（データの追加、編集、閲覧、削除など）を定期的に検証するために使用され、通常、ユーザーの管理者に送信されます。
    
*   **ユーザーエンタイトルメントの再認定**：アテステーションレポートに対する対応として、ユーザーエンタイトルメントの再認定は、しばしば管理者が自身のスタッフのシステムへのアクセス権を承認することが含まれます。アクセス権が既に不要であれば、自動デプロビジョニングに移行します。
    
*   **職務分掌**：危険な一連のアクセス権が個人に付与されないようにするルール。例えば、ある個人が企業の銀行口座の閲覧と外部口座への送金の両方を実行できる場合、ユーザーは個人口座に送金できる可能性があります。
    
*   **アクセス権レビュー**：レビューには、さまざまなアプリやリソースへのユーザーアクセス権のレビューと検証（または取り消し）を効率化するツールが含まれます。一部のIGAツールは、付与されたエンタイトルメントを特定するのに役立つ検知機能も提供します。
    
*   **ロールベース管理**：ロールベースアクセス制御（RBAC）としても知られ、ユーザーの役割によるアクセス権の定義と管理が含まれます。
    
*   **分析とレポート**：アクティビティをログに記録し、レポートを生成し（コンプライアンス遵守の目的も含む）、問題と最適化を特定するための分析を提供するツールが含まれます。
    

@row
#### IGA Solution Architecture

An example of how an IGA solution could support an authentication service is shown in Figure 9 (access management shown for context):

@column
#### IGAソリューションアーキテクチャ

IGAソリューションがどのように認証サービスを助けるのかという例をFigure 9で示してします（背景としてアクセス管理を示しています）：

@row
![A diagram of IAM architecture components, including the end user who goes through an Access Gateway to the Authentication Services. There is also the administrative user who handles end-user on and off-boarding and administration through the IA service, Account Management Services Entitlement Management Service, and the Enterprise Applications](/assets/images/idpro_bok/image9.png)

Figure 9: IAM Architecture Components

@row
This architecture supports the following IAM Processes:

Table 2: IAM Processes

| Process | Description |
| --- | --- |
| Identity Provisioning | Creates identity records based on initiation from trusted identity sources (e.g., the HR System) |
| Account Provisioning | Creates accounts in Enterprise Directories based on birthright provisioning rules. Also supports the creation of application accounts based on request / approval workflows. |
| Entitlement Management | Supports the workflow and administration requirements of enabling user-to-group/role mappings that enable access management rule creation. |

@column
このアーキテクチャは以下のIAMプロセスをサポートしています：

Table 2: IAMプロセス

| プロセス | 説明 |
| --- | --- |
| アイデンティティプロビジョニング | 信頼できるアイデンティティソース（例、HRシステム）を初期データとしてアイデンティティレコードの作成します |
| アカウントプロビジョニング | 生得権プロビジョニングルールに基づいてエンタープライズディレクトリにアカウントを作成します。また、リクエスト／承認ワークフローに基づいてアプリケーションアカウントを作成します。 |
| エンタイトルメント管理 | ワークフローと、ユーザーとグループ／ロールのマッピングをおこない、アクセス管理ルール作成を有効にする管理要件をサポートします。 |

@row
### Access Management

Access Management is the ‘real-time’ component of IAM. It encompasses the processes that are critical in protecting corporate resources and securing the digital business. Whether it is giving access to customers to enable e-commerce or securing resources for partners to conduct business securely, the Access Management architecture will control the planning, design, and development of the enabling technology.

@column
### アクセス管理

アクセス管理は、IAMの「リアルタイム」なコンポーネントです。企業のリソースを保護し、デジタルビジネスを安全にするために重要なプロセスを包括しています。eコマースを可能にするために顧客にアクセスを提供する場合でも、安全にビジネスをおこなうためにパートナーのリソースを保護する場合でも、アクセス管理アーキテクチャは、実現するためのテクノロジーの計画、設計、開発をコントロールします。

@row
#### Access Management Overview

An access management architecture will have components that enable only those accounts that are authorized to perform an action on a protected enterprise resource.

The key functions supported in an Access Management Architecture are:

*   User Authentication (staff, contractors, business partners)
    
*   Access Policy Management
    
*   Access Policy Decision making and enforcement
    
*   Authorization Control (Coarse / Fine-Grained)
    
*   Adaptive Access controls
    
*   Single Sign-On (SSO)
    
*   Authenticated Session Management
    
*   Security Token Services
    
*   Access Event Logging
    
*   User Behavior Analytics
    
*   Access Management Solution Architecture
    

The two most common Access Management services supported in most scenarios are:

*   Authentication – logging into a computer system - typically role-based
    
*   Authorization – accessing computer system functionality – typically attribute-based
    
*   Policy-based authorization is increasingly being deployed. It provides access control to corporate resources in accordance with centrally managed corporate policy rather than entitlements established on a system-by-system basis.
    

An example of a fine-grained authorization environment is shown in Figure 10. The components of the solution combine to control access to corporate resources based on the policies in the Decision Point.

@column
#### アクセス管理概観

アクセス管理アーキテクチャは、保護された企業リソースに対してアクションを実行することを認可されたアカウントのみを有効にするコンポーネントを備えています。

アクセス管理アーキテクチャでサポートされる主な機能は以下です：

*   ユーザー認証（従業員、業務委託者、ビジネスパートナー）
    
*   アクセスポリシー管理
    
*  アクセスポリシーの決定と実行
    
*   認可制御（粗い／きめ細かい）
    
*   アダプティブアクセス制御
    
*   シングルサインオン（SSO）
    
*   認証セッション管理
    
*   セキュリティトークンサービス
    
*   アクセスイベントロギング
    
*   ユーザー行動分析
    
*   アクセス管理ソリューションアーキテクチャ
    

ほとんどのシナリオでサポートされる最も一般的な2つのアクセス管理サービスは以下です：

*   認証 – コンピュータシステムへのログイン - 通常はロールベース
    
*   認可 – コンピュータシステム機能へのアクセス – 通常は属性ベース
    
*   ポリシーベース認可は、ますます導入が進んでいます。システムごとに設定されるエンタイトルメントではなく、中央で管理される企業ポリシーに従って、企業リソースへのアクセス制御を提供します。
    

きめ細かい認可環境の例をFigure 10に示します。ソリューションのコンポーネントを組み合わせて、ポリシー決定ポイントにおいてポリシーに基づいて企業リソースへのアクセスを制御します。

@row
![A diagram of the relationship between various Access Management Comonents, including the Policy Enforcement point (PEP), the POlicy Decision Point (PDP), the Policy Access Point (PAP), and the Policy Information Point (PIP). ](/assets/images/idpro_bok/image10.png)

Figure 10: Typical Components of an Authorization Service

@row
The architecture of an authorization service will typically contain the key elements that are involved in the flow from an actor (person or system) on a device (mobile or desktop) that accesses an application or service (typically over the internet) that resides within an enterprise boundary (behind network firewalls).

Table 3: Policy Control Points

| Policy Control Point | Definition |
| --- | --- |
| Policy Administration Point (PAP) | responsible for creating policy statements that tie the user to a role or group and defines the type of access to a resource |
| Policy Enforcement Point (PEP) | responsible for protecting the resource; intercepts traffic to the resource, and validates access with the PDP |
| Policy Decision Point (PDP) | determines access to a resource, uses policy to determine if a subject (user) has access to a resource, usually via an attribute value or role or group membership. |
| Policy Information Point (PIP) | typically a user or attribute store that provide information about managed users (e.g., Active Directory or LDAP directory) |

@column
認可サービスのアーキテクチャには、通常、企業の境界の内側（ネットワークファイアウォールの背後）に存在するアプリケーションまたはサービスに（通常はインターネット経由で）アクセスする（モバイルまたはデスクトップ）デバイスの（人間またはシステムといった）アクターからのフローに関わる主な要素が含まれます。

Table 3: ポリシー制御ポイント

| ポリシー制御ポイント | 定義 |
| --- | --- |
| ポリシー管理ポイント（PAP） | ユーザーをロールまたはグループに関連付けてリソースへのアクセスの種類を定義するポリシーステートメントを作成する責任を負います |
| ポリシー実行ポイント（PEP） | リソースを保護する責任を負います；リソースへのトラフィックをインターセプトしてPDPでアクセスの正当性を検証します |
| ポリシー決定ポイント（PDP） | リソースへのアクセスを決定し、通常、属性値またはロールやグループメンバーシップによって主体（ユーザー）がリソースへのアクセスできるかを決定するためにポリシーを利用します。 |
| ポリシー情報ポイント（PIP） | 通常、管理されたユーザーに関する情報を提供するユーザーまたは属性ストア（例：Active DirectoryまたはLDAPディレクトリ） |

@row
#### Access Management Patterns

A well-crafted IAM architecture is able to both improve user experience and increase security by combining the flow between architecture components in a connected, orchestrated framework. Historically, organizations have seen security and ease of use as tradeoffs, but with the new identity technologies available today, it is possible to have both.

When combining these key components in a deployment blueprint (solution configuration), an architecture pattern evolves to support most, if not all, access management needs across the organization.

@column
#### アクセス管理パターン

よく練られたIAMアーキテクチャは、接続されオーケストレーションされたフレームワーク内のアーキテクチャコンポーネント間のフローと組み合わせることにより、ユーザーエクスペリエンスを向上させ、セキュリティを強化することが実現できます。歴史的に、組織はセキュリティと使いやすさをトレードオフの関係ととらえてきましたが、今日利用できる新しいアイデンティティ技術によって、その両方を手に入れることが可能になります。

これらの主要なコンポーネントをデプロイメントの青写真（ソリューション構成）として組み合わせると、アーキテクチャパターンが進化し、組織全体のアクセス管理のニーズ、すべてではないにしても、ほとんどをサポートできるようになります。

@row
![A diagram of possible access management patterns, taking a user from a client such as a browser or mobile app through a DMZ and into a corporate network.](/assets/images/idpro_bok/image11.png)

Figure 11: Access Management Patterns

@row
Table 4: Access Management Pattern descriptions

| Pattern | Description |
| --- | --- |
| Browser to Web Application | A user needs to sign in to a web application that is secured by an Authentication Service |
| Native App (also Single Page App) to Web API | A native application needs to authenticate a user to access resources from a web API that is secured by an Authentication Service |
| Server App to Web API | A server application with no web user interface needs to get resources from a web API secured by an Authentication Service |

@column
Table 4: アクセス管理パターンの説明

| パターン | 説明 |
| --- | --- |
| ブラウザからWebアプリケーション | ユーザーが、認証サービスによって保護されているWebアプリケーションにサインインする必要があります |
| ネイティブアプリ（シングルページアプリを含む）からWeb API | ネイティブアプリケーションが、認証サービスによって保護されているWeb APIからリソースにアクセスするために、ユーザーを認証する必要があります |
| サーバーアプリからWeb API | ウェブユーザーインターフェースを持たないサーバーアプリケーションは、認証サービスによって保護されたWeb APIからリソースを取得する必要があります |

@row
### Identity Standards

No IAM solution architecture is complete without addressing the applicable standards. Because IAM touches virtually all corporate systems, interfaces need to adhere to standards in order to minimize the amount of customization that would otherwise be required. An IAM Architecture should support a “pluggable” approach that facilitates interconnection and ties together key security enablers that are built on industry standards. There are several industry organizations (standards bodies) like IETF, OASIS, Kantara Initiative, and the OpenID Foundation.

The key standards that support modern identity and access management today are OIDC, OAuth2, and SAML.[^4]

@column
### アイデンティティ標準仕様

IAMソリューションアーキテクチャは、適用される標準仕様に対処しなければ完全とは言えません。IAMは事実上すべての企業システムに関与するため、必要となるカスタマイズの量を最小にするため、インタフェースは標準仕様に準拠する必要があります。IAMアーキテクチャは、相互接続を容易にし、業界標準に基づいて作られた重要なセキュリティアドオンを結びつける「プラグイン可能な」アプローチをサポートする必要があります。IETF、OASIS、Kantara Initiative、OpenID Foundationなど、いくつかの業界団体（標準化団体）が存在します。

今日のモダンなアイデンティティおよびアクセス管理を支える主要な標準仕様は、OIDC、OAuth2およびSAMLです。 [^4]

@row
![Logos for OIDC, OAuth, SAML](/assets/images/idpro_bok/image12.png)

Figure 12: Logos for OIDC, OAuth2 , SAML

@row
## Conclusion

IAM practitioners should adopt the enterprise architecture approach used within the organization in which they are working. In the absence of a corporate approach to architecture, IAM practitioners should develop an architectural approach that ensures their IAM projects consider all the business systems that might be affected, the types of applications to be supported, and the infrastructure on which IAM solutions are to be deployed.

An IAM project that takes such an approach will have a significantly better chance of being completed within schedule and budget constraints. It will also be much more likely to satisfy users.

@column
## 結論

IAM実務者は、彼らが働いている組織内で使用されているエンタープライズアーキテクチャアプローチを採用する必要があります。アーキテクチャに対する企業のアプローチがない場合、IAM実務者は、IAMプロジェクトが影響を受ける可能性のあるすべてのビジネスシステム、サポートされるアプリケーションの種類、IAMソリューションがデプロイされるインフラストラクチャを確実に考慮するアーキテクチャアプローチを開発する必要があります。

このようなアプローチをとるIAMプロジェクトは、スケジュールと予算の制約の中で完遂できる可能性が大幅に高くなります。また、ユーザーを満足させることができる可能性も高くなります。

@row
### Authors

Andrew Cameron

<!-- ![Photo of author](/assets/images/idpro_bok/image13.jpeg) -->Andrew Cameron is the Enterprise Architect for Identity and Access Management at General Motors. His responsibilities include Defining the Strategy and Implementation Roadmaps of their IAM technology platform and ensuring the architectural quality of the many initiatives driving the GM digital business.

Graham Williamson

<!-- ![Photo of author](/assets/images/idpro_bok/image14.jpeg) -->Graham Williamson is an IAM consultant working with commercial and government organizations for over 20 years with expertise in identity management and access control, enterprise architecture and service-oriented architecture, electronic commerce, and public key infrastructure, as well as ICT strategy development and project management. Graham has undertaken major projects for commercial organizations such as Cathay Pacific in Hong Kong and Sensis in Melbourne, academic institutions in Australia such as Monash University and Griffith University, and government agencies such as Queensland Government CIO’s office and the Northern Territory Government in Australia and the Ministry of Home Affairs in Singapore.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2020-06-17 | V1 published |
| 2021-09-30 | Additional information added regarding hybrid cloud infrastructures; removed specific mention of RACF; minor editorial updates |

- - -

[^1]:  Readers may find the IDPro BoK article “Introduction to Project Management for IAM Projects” of interest. See Williamson, Graham, and Corey Scholefield, “Introduction to Project Management for IAM Projects,” IDPro Body of Knowledge, vol 1, issue 1, March 2020, [https://bok.idpro.org/article/id/25/](https://bok.idpro.org/article/id/25/).
    
[^2]:  “SCIM: System for Cross-domain Identity Management” [http://www.simplecloud.info/](http://www.simplecloud.info/)
    
[^3]:  Cameron, Andrew and Olaf Grew, “An Overview of the Digital Identity Lifecycle,” IDPro Body of Knowledge, 30 October 2021, [https://bok.idpro.org/article/id/31/](https://bok.idpro.org/article/id/31/).
    
[^4]:  OpenID Connect, website, OpenID Foundation, [https://openid.net/connect/](https://openid.net/connect/); OAuth2, website, [https://oauth.net/2/](https://oauth.net/2/) ; “Security Assertion Markup Language (SAML) V2.0 Technical Overview,” OASIS, [http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html)
