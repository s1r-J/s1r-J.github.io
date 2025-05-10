---
layout: columns
title: An Overview of the Digital Identity Lifecycle (v2)
permalink: /docs/oidc_oauth/idpro_bok/31
date: 2024-09-09
modify_date: 2024-09-27
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "アイデンティティライフサイクル", "ユーザー・ジャーニー"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/31/](https://bok.idpro.org/article/id/31/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

A digital identity goes through several stages during its existence, from creation, through various modifications in response to different events, to inactivation or deletion. This article walks through the types of digital identities that must be managed, along with the various stages of a digital identity, describing the typical beginning-to-end lifecycle within or across multiple systems. The lifecycles outlined in this document are not meant to be comprehensive but should be applicable over most B2B, B2C, and B2E use cases.

Keywords: Lifecycle, Digital Identity, User Journey


@column
## 概要

デジタル・アイデンティティは、作成されてから、複数の異なるイベントに対する様々な変更があり、不活化もしくは削除するまで、存在している間にいくつかのステージを通過します。この記事では、管理する必要がある複数の種類のデジタル・アイデンティティについて説明し、デジタル・アイデンティティのさまざまなステージについて説明し、複数のシステム内または複数のシステムにわたる典型的な最初から最後までのライフサイクルを説明します。この文書で概説しているライフサイクルは包括的なものではありませんが、ほとんどのB2B、B2CおよびB2Eのユースケースに適用できるはずです。

キーワード：ライフサイクル。デジタル・アイデンティティ、ユーザー・ジャーニー


@row
By Andrew Cameron and Olaf Grewe

© 2022 IDPro, Andrew Cameron, Olaf Grewe

@row
## Introduction to Digital Identity

A digital identity, for the purpose of this document, is defined as the combination of a unique identifier together with relevant attributes that uniquely identifies an entity. Depending on the complexity of the environment in which a digital identity is used, its lifecycle—from its inception to its closure—can be significantly more complicated than a simple create, read, update, and delete (CRUD) lifecycle.[^1]

Depending on the type of identity (human such as Workforce or Customer, and non-human types such as System or Device), the lifecycle phases will differ. Enterprise IAM has typically been a well-established set of processes that provide the processes and governance capabilities to ensure only the correct people (via their accounts) have access to only the required applications (resources). Customer IAM has an entirely different set of requirements that represent value to a business due to the nature of its defining interactions with a customer. Poor or inefficient interactions with customers can have severe negative effects on a business. For these reasons, the different identity types will require separate systems and processes supporting them:

|     |     |
| --- | --- |
| **Identity Type** | **Description** |
| Workforce | A workforce identity is one created to function in an enterprise context, which may include a Business-to-Business (B2B) and/or Business-to-Employee (B2E). Examples of these identity types will be Employees, Suppliers, Contractors, or other human identities that support the corporate workforce. |
| Customer | A customer identity type will usually function outside the enterprise context, enabling digital business between the owner of the customer identity and the enterprise. Typically, there will be multiple channels (Web, Mobile, IoT Device) of access to manage with a larger set of profile (identity attribute) data necessary to facilitate the interaction. |
| Device or System | Device identities typically are used to provide identification and representation on a digital network. System identities are used to authenticate services (e.g., applications or server-based processes) to a network. |

@column
## デジタル・アイデンティティへの導入

この記事の目的のため、デジタル・アイデンティティとは一意の識別子とエンティティを一意に識別する関連属性との組み合わせとして定義しています。デジタル・アイデンティティが利用される環境の複雑さによっては、そのライフサイクル (開始から終了まで) は、単純な作成、読み取り、更新および削除 (CRUD) のライフサイクルよりもはるかに複雑になる可能性があります。 [^1]

アイデンティティの種類（従業員や顧客などの人間およびシステムやデバイスなどの人間以外）に応じて、ライフサイクルフェーズは異なります。企業向けIAMは一般的にプロセスとガバナンス機能を提供する確立された一連のプロセスであり、（アカウントを介して）適切なユーザーのみが必要なアプリケーション（リソース）のみにアクセスできるようにします。顧客向けIAMには顧客とのやり取りを定義する性質があるため、ビジネスにとっての価値を表すまったく異なる一連の要件が存在しています。顧客とのやり取りが貧弱または非効率的であると、ビジネスに深刻な悪影響を及ぼす可能性があります。これらの理由から、様々な種類のアイデンティティが個別のシステムとそれらをサポートするプロセスを必要とします：

|     |     |
| --- | --- |
| **アイデンティティの種類** | **詳細** |
| 従業員 | 従業員アイデンティティは、企業対企業（B2B）およびまたは企業対従業員（B2E）を含むエンタープライズコンテキストで機能するように作成されたアイデンティティです。これらの種類のアイデンティティの例は、従業員、サプライヤー、請負業者または企業の従業員をサポートするその他の人間のアイデンティティです。 |
| 顧客 | 顧客アイデンティティは一般的にエンタープライズコンテキストの外で機能し、顧客アイデンティティの所有者と企業の間でデジタル・ビジネスを可能にします。通常、複数のアクセスチャネル（Web、モバイル、IoTデバイス）のが存在し、相互作用 を促進するために必要なプロファイル（アイデンティティ属性）データの大きなセットとともに管理されます。 |
| デバイスまたはシステム | デバイス・アイデンティティは通常、デジタルネットワーク上で識別および表現を提供するために利用されます。システム・アイデンティティは、ネットワークに対するサービス（例えば、アプリケーションやサーバーベースのプロセス）を認証するために利用されます。 |

@row
### Terminology

*   Digital Identity – the combination of a unique identifier together with relevant attributes that uniquely identifies an entity.
    
*   Journey-based Creation – The process that guides a customer through a series of interactions prior to establishing a digital identity. For example, capturing the minimum basic information needed from a customer to enable creation of an identity.
    
*   Attributes - Key/value pairs relevant for the digital identity (username, first name, last name, etc.).
    
*   Inter-organizational (Federation): An organization relies on another organization’s digital identity and lifecycle management processes.
    
*   Intra-organizational (Single Sign-On): A central digital identity, such as an account in a directory, is linked by downstream systems as authoritative for authentication.
    

@column
### 用語解説

*   デジタル・アイデンティティ – エンティティを一意に識別するための、一意の識別子と関連する属性の組み合わせ。
    
*   ジャーニーに基づく作成 – デジタル・アイデンティティを確立する前に、一連のやり取りを通じて顧客を誘導するプロセス。例えば、アイデンティティの作成を可能にするために顧客から必要な最低限の基本情報を取得すること。
    
*   属性 - デジタル・アイデンティティ（ユーザー名、名、姓など）に関するキーバリューペア。
    
*   組織間（フェデレーション）：ある組織が、他の組織のデジタル・アイデンティティおよびライフサイクル管理プロセスに依存すること。
    
*   組織内（シングルサインオン）：ディレクトリ内のアカウントのような中央デジタル・アイデンティティが、認証のための権威のあるものとして下流のシステムによって連携されること。
    

@row
## Identity Lifecycles

For any lifecycle ‘create’ phase, a digital identity is created as a unique identifier in a system of record. It can be created either as part of a business process (workforce or device identity) or transparently as part of a user journey (customer identity).

Throughout its lifecycle, a digital identity enables digital transactions through all of its assigned accounts and the entitlements assigned to those accounts. Although a lifecycle is outlined as a continuum in this document, the reader should expect that:

*   The digital identity lifecycle could be distributed across multiple technical solutions in most organizations.
    
*   Some steps in the lifecycle (e.g., authenticate, use) will occur more frequently than others (e.g., merge, delete).
    

@column
## アイデンティティライフサイクル

ライフサイクル「作成」フェーズでは、デジタル・アイデンティティは記録システム内で一意の識別子として作成されます。これは、ビジネスプロセスの一部として作成されるか（従業員またはデバイス・アイデンティティ）またはユーザー・ジャーニーの一部として透過的に作成されます（顧客アイデンティティ）。

そのライフサイクル全体を通じて、デジタル・アイデンティティは全ての割り当てられたアカウントとアカウントに割り当てられた資格を通じてデジタル取引を可能にします。本記事ではライフサイクルが連続体としてまとめられていますが、読者は次のことを想定する必要があります：

*   デジタル・アイデンティティライフサイクルはほとんどの組織で複数のテクニカルソリューションに分散されています。
    
*   ライフサイクルの一部のステップ（例えば、認証や利用）は他のステップ（例えば、マージや削除）よりも頻繁に発生するでしょう。
    

@row
### Workforce Identity

The workforce identity lifecycle is addressed through three principal business processes: Joiner, Mover, or Leaver. The **Joiner** processes cover all lifecycle phases that facilitate the creation of assets (identities, accounts, group memberships, etc.) to enable identification and access in an enterprise environment. The **Mover** process allows for changes or updates to identity status while still engaged in the enterprise environment and considers the necessary attestation processes to verify access permissions and entitlements. The **Leaver** process covers the series of steps that must occur when an identity is removed from access to the enterprise environment.

Figure 1 depicts the workforce IAM phases in the process:

@column
### 従業員アイデンティティ

従業員アイデンティティライフサイクルはJoiner、Mover、Leaverという3つの主要なビジネスプロセスによって対処されます。 **Joiner** プロセスは、エンタープライズ環境での識別とアクセスを可能にする資産 (アイデンティティ、アカウント、グループメンバーシップなど) の作成を容易にするすべてのライフサイクルのフェーズをカバーします。 **Mover** プロセスは、エンタープライズ環境に従事しているあいだ、アイデンティティのステータスを変更または更新でき、そしてアクセス許可と資格を検証するために必要な認証プロセスを考慮しています。 **Leaver** プロセスは、アイデンティティがエンタープライズ環境へのアクセス権を削除されたときに必ず発生する一連の手順をカバーしています。

図1は各プロセスにおける従業員IAMフェーズを示しています：

@row
![Diagram Description automatically generated](/assets/images/idpro_bok/lifecycle-fig1.jpg)

_Figure 1 –_ _Core IAM Processes_

@row
The following table describes the phases that support the workforce identity lifecycle:

|     |     |
| --- | --- |
| **Lifecycle Phase** | **Description** |
| Create Identity | The creation of a workforce identity as part of a business process (employees, suppliers, etc.) is frequently combined with the collection of proof to establish a minimum set of attributes to be associated with the identifier. The creation of a digital identity may be automated (e.g., synchronized with an HR system event), especially when digital identities are generated at scale for various purposes, such as a merger or acquisition.<br><br>Enrollment processes for workforce entities frequently involve other human entities (such as a line manager or delegated admin agent) validating the proof provided. In countries without an established national identity system (US, UK, AU, etc.), it can be required to provide multiple documents as proof (driver’s license, passport, utility bill, bank card/statement) in lieu of a national identity document. |
| Provision Account | Create accounts in enterprise systems based on business rules and required access to resources. |
| Provision Access | Create entitlements by associating user accounts to objects that enable access to corporate resources in the required systems. Entitlements are generally represented by attribute values, group memberships, or organizational alignment. Business rules will define access to a resource based on enterprise entitlements. |
| Authenticate | Require a user account to validate a credential before allowing access to a network or resource. |
| Manage Access | Validate that the access that has been assigned an account and approving continued access to corporate resources. Access certification is a process that validates all current access and can be used to remove no longer needed access. The attestation process for verifying and access is a critical and often underestimated component of a mature IAM system.<br><br>Digital identities are frequently subject to updates, primarily of their attributes. Less frequently, the identifier itself may change. An example is a digital identity for which the username is also used as the identifier (e.g., email address). A user may wish to change their username for various purposes, such as a name change due to a life event or a change of preferences. For an in-depth discussion, please refer to Ian Glazer’s article, “Identifiers and Usernames.”[^2]<br><br>Frequently update the use cases describing workflow capabilities that address approval, step-up, or notification requirements. These are important controls to address identity take-over risks. Depending on the value of the digital identity for the organization, updates to digital identities may be subject to enrolment-type proofing. |
| Deprovision Access | Remove access to any or all corporate resources. The need to remove access could occur as a result of a Leaver process or a validation from an Access Certification. When a digital identity is not required anymore, it should be disabled in the system of record. This action implies not only disablement or deletion from a central directory but also downstream systems that maintain records associated with this digital identity as well as logging and auditing repositories. Only once the identifier used for this digital identity has been removed from all systems can a digital identity be considered genuinely deleted.<br><br>A detailed discussion on the importance of account disable or removal given current best practices can be found in Andrew Hindle’s article, “Impact of GDPR on Identity and Access Management.”[^3] |

@column
以下の表はフェーズとそれがサポートする従業員アイデンティティライフサイクルを記載しています：

|     |     |
| --- | --- |
| **ライフサイクル・フェーズ** | **詳細** |
| アイデンティティの作成 | ビジネスプロセスの一部として従業員アイデンティティ（従業員、サプライヤーなど）を作成することは証拠の収集と組み合わせて、識別子に関連付ける最低限の属性セットを確立することがよくあります。デジタル・アイデンティティの作成は自動化される場合（たとえば、HRシステムのイベントと同期）があります。特に合併や買収などのさまざまな目的でデジタル・アイデンティティが大規模に生成される場合です。<br><br>従業員のエンティティの登録プロセスには、提供された証拠を検証する他の人間のエンティティ（ラインマネージャーや委任された管理エージェントなど）が関与することがよくあります。国民アイデンティティシステムが確立されていない国（米国、英国、オーストラリアなど）では、国民身分証の代わりに、証拠として複数の証明書（運転免許証、パスポート、公共料金の請求書、銀行カード/明細書）の提出が必要な場合があります。 |
| アカウントのプロビジョニング | ビジネスルールと必要なリソースへのアクセスに基づいて、エンタープライズシステムにアカウントを作成します。 |
| アクセスのプロビジョニング | 必要なシステム内の企業リソースへのアクセスを可能にするオブジェクトにユーザーアカウントを関連付けて、資格を作成します。 一般的に、資格は属性値、グループメンバーシップまたは組織の連携によって表されます。ビジネスルールは、企業の資格に基づいてリソースへのアクセスを定義します。 |
| 認証 | ネットワークやリソースへのアクセスを許可する前に、ユーザーアカウントにクレデンシャルの検証を要求すること。 |
| アクセス管理 | アカウントを割り当てられたアクセス権を検証し、企業リソースへの継続的なアクセスを承認します。アクセス認定は現在のすべてのアクセスを検証するプロセスであり、不要になったアクセスを削除するために使用することができます。検証とアクセスのための認証プロセスは、成熟したIAMシステムの重要な構成要素であり、過小評価されがちなものです。<br><br>デジタル・アイデンティティは頻繁に更新され、主にその属性が更新されます。それほど頻繁ではありませんが、識別子自体も変更されることがあります。例えば、ユーザー名が識別子としても使用されるデジタル・アイデンティティ（例えば、Eメールアドレス）があります。ユーザーは、ライフイベントによる名前の変更や好みの変化など、さまざまな目的でユーザー名を変更する可能性があります。詳細な議論についてはIan Glazerの記事「Identifiers and Usernames」を参照してください。 [^2] <br><br>承認、ステップアップまたは通知要件に対応するワークフロー機能を説明するユースケースを頻繁に更新します。これらは、アイデンティティの乗っ取りリスクに対処するための重要な管理です。組織にとってのデジタル・アイデンティティの価値に応じて、デジタル・アイデンティティの更新は、登録タイプの証明の対象となる場合があります。 |
| アクセスのデプロビジョニング | 一部または全部の企業リソースへのアクセス権を削除します。アクセス権削除の必要性は、Leaverプロセスの結果またはアクセス認定からの検証結果として発生する可能性があります。デジタル・アイデンティティが不要になったとき、記録システムで無効にする必要があります。この措置は、中央ディレクトリからの無効化または削除だけでなく、このデジタル・アイデンティティに関連する記録を維持する下流システムおよびログ記録と監査リポジトリからの無効化または削除を意味します。このデジタル・アイデンティティに使用された識別子がすべてのシステムから削除されて初めて、デジタル・アイデンティティは正真正銘に削除されたと見なすことができます。<br><br>現在のベストプラクティスを考慮したアカウントの無効化または削除の重要性に関する詳細な議論は、Andrew Hindleの記事「Impact of GDPR on Identity and Access Management.」 [^3] に記載されています。 |

@row
### Customer Identity

Customer IAM has evolved more recently to support the processes that govern consumers’ User Experience as they interact with digital business. CIAM solutions have developed to provide companies with added value from the data they collect from customers as a result of the customers’ experiences with corporate websites and services. Most customer experiences are described as part of a “User Journey,” which represents the interactions (Authentication, Registration, Profile Update) that a customer has when engaging with digital resources such as websites, mobile apps, or IoT interfaces.

The following diagram depicts the phases of the CIAM Lifecycle.

@column
### 顧客アイデンティティ

近年、顧客IAMは消費者がデジタルビジネスと接する際のユーザーエクスペリエンスを管理するプロセスをサポートするために進化してきました。CIAMソリューションは、企業のWebサイトやサービスを利用した顧客体験の結果として顧客から収集したデータから、付加価値を企業に提供するために開発されてきました。多くの顧客体験は、Webサイト、モバイルアプリやIoTインターフェースなどのデジタルリソースに関わる際に顧客がおこなうやり取り（認証、登録、プロファイル更新）を表す「ユーザー・ジャーニー」の一部として記述されます。

以下の図は、CIAMライフサイクルの各フェーズを表しています。

@row
![Diagram Description automatically generated](/assets/images/idpro_bok/lifecycle-fig2.jpg)

_Figure 2 – The Customer Identity Lifecycle_

@row
The following table describes the phases that support the customer identity lifecycle:

|     |     |
| --- | --- |
| **Lifecycle Phase** | **Description** |
| Register | The first part of the user journey is the creation of a customer identity through a registration process. This registration typically happens where a digital identity is required to enable an experience. Information is captured from a user as part of a user journey, and the user is allowed to consent to usage of the data provided. Registration interactions are typically a one-time interaction with the customer that concludes with a confirmation of the purpose of the flow (i.e. “Your account has been created”). Registration interactions can also be transparent to the user if enabled thru a federated identity such as a social account sign-in (i.e., “Sign in with your Facebook account to get registered”).<br><br>Registration does not require mandatory attributes other than the linking steps in the user journey to the identifier. Depending on the nature of the digital transaction, customer identities may require assurance over several attributes. A key consideration here is the attributes used to establish ownership (or recovery) for a digital identity, either via human or non-human means. |
| Manage Profile Data | Each customer has a profile and managing the profile data involves a user experience that allows a customer to update their data across corporate resources (e.g., websites or mobile apps).<br><br>This phase primarily applies to user journey-based digital identities. In order to enable digital services to resume user journeys, it is necessary to enhance the digital identities with attributes that are specific to the way the user accesses the service. Two common techniques are cookies or device fingerprinting. For an illustration of the latter, see the EFFs Panopticlick site.[^4] |
| Manage Privacy and Consent | The customer lifecycle must include a process that informs and enables the customer to invoke their rights around knowledge and consent of what can happen with their customer information. |
| Authenticate | As part of the workflow, the customer is required to validate their credential prior to accessing any customer services |
| Manage Access | The customer lifecycle will require managing access to business services based on customer interactions.<br><br>The user may also choose to provide additional attributes. The service would typically allow the user to create a username and password to login after their current session has expired. At this stage, a service may be able to combine multiple identifiers created by different devices (mobile, desktop, laptop, etc.). At this stage, the digital identity is considered pseudonymous as there is no assurance over the attributes provided by the user. |
| Monitor | After the initial phases are complete, the customer lifecycle will move into monitoring, where the process of mining/collecting data about the customer and their experiences support a variety of business and consumer requirements occur. From a security perspective, monitoring data can be used to notify the customer of leaked credentials or other breaches of information. The business can also benefit by leveraging historical usage information of customer activity thru an analytics service. |
| Remove Access | Removal of customer access is typically done as a result of a customer request or based on some amount of inactivity measure. |

@column
以下の表では顧客アイデンティティのライフサイクルを支えるフェーズについて記述しています：

|     |     |
| --- | --- |
| **ライフサイクル・フェーズ** | **詳細** |
| 登録 | ユーザー・ジャーニーの最初の部分は、登録プロセスによる顧客アイデンティティの作成です。通常、この登録は、ある体験を実現するためにデジタル・アイデンティティが必要とされる場合におこなわれます。ユーザー・ジャーニーの一部として、ユーザから情報が収集され、ユーザーは提供したデータの使用に同意することができます。通常、登録操作はフローの目的の確認（「アカウントが作成されました」など）で終了する、顧客との1回限りの操作です。登録操作は、ソーシャルアカウント・サインインのようにフェデレーション・アイデンティティによって実施される場合（例えば、「Facebookのアカウントでサインインして登録してください。」）、ユーザーに対して透過的になることもあります。<br><br>登録には、ユーザー・ジャーニーにおける識別子への関連付けステップ以外の必須属性は必要ありません。デジタル取引の性質によっては、顧客アイデンティティは複数の属性に対する保証を必要とする場合があります。ここで考慮すべき重要な点は、デジタル・アイデンティティの所有権（または回復）を、人間または非人間の手段によって確立するために用いられる属性です。 |
| プロファイルデータの管理 | 各顧客はプロファイルを持っており、プロファイルデータの管理には、顧客が企業のリソース（例、Webサイトやモバイルアプリ）をまたいでデータを更新できるようなユーザーエクスペリエンスが必要です。<br><br>このフェーズは、主にユーザー・ジャーニーに基づくデジタル・アイデンティティに適用されます。デジタル・サービスでユーザー・ジャーニーを再開できるようにするには、ユーザーがサービスにアクセスする方法に特有の属性でデジタル・アイデンティティを強化する必要があります。一般的な手法としては、Cookieやデバイスフィンガープリントの2つがあります。後者については、EFFs Panopticlickのサイトを参照してください。 [^4] |
| プライバシーと同意の管理 | 顧客ライフサイクルには、顧客情報の扱いについて知識と同意に関する権利を顧客に通知し、権利を行使できるようにするプロセスが含まれていなければなりません。 |
| 認証 | ワークフローの一部として、顧客は顧客サービスにアクセスする前にクレデンシャルを検証する必要があります。 |
| アクセス管理 | 顧客ライフサイクルでは、顧客とのやり取りに基づくビジネスサービスへのアクセスを管理することが必要です。<br><br>また、ユーザーは追加属性の提供を選択することができます。一般的に、サービスは現在のセッションが有効期限切れになった後、ログインするためのユーザー名とパスワードを作成させます。この段階で、サービスは異なるデバイス（携帯電話、デスクトップ、ラップトップなど）で作成された複数の識別子を組み合わすことができることがあります。この段階では、ユーザーによって提供された属性の保証がされていないため、デジタル・アイデンティティは偽物とみなされます。 |
| 監視 | 初期フェーズが完了すると、顧客ライフサイクルは監視に移行します。監視とは顧客とその体験に関するデータをマイニング／収集するプロセスで、ビジネスと消費者のさまざまな要件をサポートすることが可能になります。セキュリティの観点からは、監視データを使って、クレデンシャル侵害や情報漏洩を顧客に通知することができます。また、分析サービスを通じて、顧客の活動の履歴情報を活用することで、ビジネスで利益を得ることができます。 |
| アクセス権の削除 | 顧客のアクセス権削除は一般的に顧客の要望の結果または一部の非アクティブ指標に基づいておこなわれます。 |

@row
### Device or System Identity

A device or system identity is an evolving area in that devices are being enabled with increasing levels of technological capability, which increases the need to identify and manage them through a lifecycle. For example, cars have dozens of internal systems that require sophisticated management capabilities over the life of the vehicle identity. On the other end of the scale, some simple monitors can connect to a network and only provide a temperature value or some other basic information. All devices will need specific lifecycle phases to manage them based on their capabilities.

@column
### デバイスやシステム・アイデンティティ

デバイスやシステムのアイデンティティは、デバイスの技術的能力が向上していることから、いま進化している分野です。そして、ライフサイクルを通じてデバイスを識別・管理する必要性が高まっています。例えば、自動車には何十もの内部システムが存在し、車両アイデンティティのライフサイクル全体を通じて高度な管理機能を必要とします。一方、ネットワークに接続し、温度などの基本情報を提供するだけのシンプルなモニターもあります。すべてのデバイスは、その能力に応じたデバイスを管理するために固有のライフサイクル・フェーズを必要とします。

@row
![Diagram Description automatically generated](/assets/images/idpro_bok/lifecycle-fig3.jpg)

_Figure 3 – The Device Identity Lifecycle_

@row
The following table describes the phases in a simple model that support the device identity lifecycle:

|     |     |
| --- | --- |
| **Lifecycle Phase** | **Description** |
| Create | The first stage in the device or system lifecycle is to kick off the process of creating the identifier that will be assigned to the device or system. |
| Provision | When the identifier is assigned, the process of enabling the device or system to be recognized, monitored, and managed. Device provisioning is typically done using some sort of certificate or PKI infrastructure to ensure that only known devices can interact with corporate resources. |
| Authenticate | Device or system authentication typically is done using a PKI infrastructure that ensures that the connected device is known and allowed to interact with the network. |
| Manage / Maintain | Once the initial phases are complete, the device or system must be monitored to determine if any actions are needed to maintain the device. As an IT security best practice, credentials (passwords) associated with non-human identities should be rotated on a periodic basis to enable protection against brute force password-based attacks. |
| Deprovision Access | When the device or system is no longer in use (which may require different processes than workforce or customer digital identities to determine), remove access of the device or system from the system of record, disabling any access to the corporate network. |

@column
次の表では、デバイス・アイデンティティのライフサイクルをサポートするシンプルなモデルにおけるフェーズを説明しています：

|     |     |
| --- | --- |
| **ライフサイクル・フェーズ** | **詳細** |
| 作成 | デバイスやシステムのライフサイクルの第一段階は、デバイスやシステムに割り当てられる識別子を作成するプロセスを開始することです。 |
| プロビジョン | 識別子が割り当てられたときにデバイスまたはシステムを認識、監視および管理できるようにするプロセスです。通常、デバイスのプロビジョニングは、ある種の証明書またはPKIインフラストラクチャを使用しておこなわれ、既知のデバイスのみが企業リソースとやり取りできるようにします。 |
| 認証 | デバイスまたはシステムの認証は、通常、接続されたデバイスが既知でネットワークとのやり取りが許可されていることを保証するPKIインフラストラクチャを使用して実行されます。 |
| 管理 / メンテナンス | 初期フェーズが完了したら、デバイスまたはシステムを監視し、デバイスをメンテナンスするために必要なアクションを決定する必要があります。ITセキュリティのベストプラクティスとして、人間ではないアイデンティティに紐づいたクレデンシャル（パスワード）は定期的にローテーションし、パスワードベースのブルートフォース攻撃から防御できるようにすべきです。 |
| アクセス権のデプロビジョン | デバイスまたはシステムを使わなくなった場合（従業員または顧客のデジタル・アイデンティティとは異なるプロセスで決定することが必要かもしれません）、システム記録からデバイスまたはシステムのアクセス権を削除し、企業のネットワークへの接続を無効にします。 |

@row
## Other Digital Identity Relationships

Some digital transactions require an organization to establish relationships between digital identity issuers, also known as identity providers. These relationships may be with external partners (e.g., a B2B relationship) or across various enterprise applications (e.g., a single sign-on environment). In addition, digital identities may be related to other identities within an organization to establish delegation authority or to manage dual-control requirements. In all cases, relationships are typically managed either as attributes of the digital identity (e.g., identifiers for the allowed services) or as separate data points in a central directory (e.g., membership in an LDAP group).

Common types of relationships are:

|     |     |
| --- | --- |
| Inter-organizational (Federation) | ![](/assets/images/idpro_bok/lifecycle-federation.png)<br><br>An organization relies on the digital identity and lifecycle management processes of another organization. |
| Intra-organizational (Single Sign-On) | ![](/assets/images/idpro_bok/lifecycle-sso.png)<br><br>A central digital identity, such as an account in a directory, is linked by downstream systems as authoritative for the purpose of authentication. |
| Inter-entity (Delegation) | ![](/assets/images/idpro_bok/lifecycle-delegation.png)<br><br>Delegation involves assigning a subset of authority from an identity in one business domain to an identity that resides in another business domain. In this example, business domain refers to defined boundaries that exist within or across an entity, which enables policy enforcement to occur. Examples of business domain include company, organization (within a company) or even work teams (within an organization). Authority is granted across domain boundaries for the purpose of enabling the transactions within the scope of a policy. Authority can be granted either explicitly or based on business rules (policies) defined at the domain level. |
| Intra-entity | ![](/assets/images/idpro_bok/lifecycle-intraentity.png)<br><br>Either user-driven or out of organizational requirements, a relationship is established between multiple digital identities to identify a single human or non-human entity as the owner (see Enhance above). |

@column
## 他のデジタル・アイデンティティとの関係性

一部のデジタル・トランザクションは、アイデンティティ・プロバイダーとしても知られるデジタル・アイデンティティ・イシュア間の関係を確立することを組織に要求します。これらの関係性は、外部のパートナーとの関係（例えば、B2B関係）、複数のエンタープライズ・アプリケーションとの関係（例えばシングルサインオン環境）かもしれません。加えて、デジタル・アイデンティティは組織内の他のアイデンティティと関係を持つことで、委譲権限を確立したり、二重の制御要件を管理したりすることがあります。いずれのケースでも、一般的に関係性はデジタル・アイデンティティの属性（例えば、許可されたサービスの識別子）または中央ディレクトリ内の個別のデータポイント（例えば、LDAPグループのメンバーシップ）として管理されます。

よくわる関係性の種類は以下の通りです：

|     |     |
| --- | --- |
| 組織間（フェデレーション） | ![](/assets/images/idpro_bok/lifecycle-federation.png)<br><br>ある組織は、他の組織のデジタル・アイデンティティおよびライフサイクル管理プロセスに依存しています。 |
| 組織内（シングルサインオン） | ![](/assets/images/idpro_bok/lifecycle-sso.png)<br><br>ディレクトリ内のアカウントのような中心となるデジタル・アイデンティティは、認証のために下流のシステムによって権威あるものとして紐づけられています。 |
| エンティティ間（委譲） | ![](/assets/images/idpro_bok/lifecycle-delegation.png)<br><br>委譲は、あるビジネス・ドメインのアイデンティティから別のビジネス・ドメインに存在するアイデンティティへと権限のサブセットを割り当てることを含みます。この例では、ビジネス・ドメインは、エンティティ内またはエンティティ間に存在する定義済みの境界を指し、ポリシーの適用を可能にします。ビジネス・ドメインの例には、会社、組織（会社内）、さらには作業チーム（組織内）が含まれます。ポリシーの範囲内でトランザクションを有効にする目的で、ドメインの境界を越えて権限が付与されます。権限は、明示的、またはドメイン・レベルで定義されたビジネス・ルール（ポリシー）に基づいて付与できます。 |
| エンティティ内 | ![](/assets/images/idpro_bok/lifecycle-intraentity.png)<br><br>ユーザー主導または組織の要件のいずれであっても、単一の人間または非人間エンティティを所有者として識別するために、複数のデジタル・アイデンティティ間に関連性が確立されます（上図参照）。 |

@row
## Conclusion

The complexity of the digital identity lifecycle frequently becomes apparent only after a number of years and as more functionality gets added to systems. Therefore, it is advisable to approach life cycle requirements with a longer-term horizon and ensure user management capabilities are extensible.

@column
## 結論

デジタル・アイデンティティライフサイクルの複雑さは、何年も経過してシステムに機能が追加されてから初めて明らかになることが頻繁にあります。したがって、より長期的な視野でライフサイクル要件に取り組み、ユーザー管理機能が拡張可能であることを保証することを推奨します。

@row
## Acknowledgements

The author would like to acknowledge Ian Glazer for articulating the progression of an identity from anonymous to pseudonymous and known. Dean Saxe contributed the classification of relationships. Jon Lehtinen, and Heather Flanagan contributed encouragement and suffered through early drafts of the article.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2022-02-28 | Updated definition of digital identity; clarified the use of the term ‘lifecycle’; updated diagrams; updated Delegation description |
| 2020-10-30 | V1 published |

- - -

[^1]:  “Create Read Update Delete” ldapwiki.com, paged last modified 19 March 2020, [https://ldapwiki.com/wiki/Create%20Read%20Update%20Delete](https://ldapwiki.com/wiki/Create%20Read%20Update%20Delete).
    
[^2]:  Glazer, Ian, “Identifiers and Usernames,” IDPro Body of Knowledge, 31 March 2020, [https://bok.idpro.org/article/id/16/](https://bok.idpro.org/article/id/16/).
    
[^3]:  Hindle, Andrew, “Impact of GDPR on Identity and Access Management,” IDPro Body of Knowledge, 31 March 2020, [https://bok.idpro.org/article/id/24/](https://bok.idpro.org/article/id/24/).
    
[^4]:  “Panopticlic 3.0,” Electronic Frontier Foundation, viewed 13 April 2020, [https://panopticlick.eff.org/](https://panopticlick.eff.org/).
