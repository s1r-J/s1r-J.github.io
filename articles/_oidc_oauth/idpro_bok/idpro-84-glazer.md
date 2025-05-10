---
layout: columns
title: User Provisioning in the Enterprise
permalink: /docs/oidc_oauth/idpro_bok/84
date: 2024-09-09
modify_date: 2024-10-20
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "ユーザープロビジョニング", "エンタープライズ"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/84/](https://bok.idpro.org/article/id/84/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

User provisioning is the means by which user accounts are created and maintained in a system (e.g., database, SaaS app, operating system, etc.). When we say that a user-provisioning system maintains a user account, we mean everything from changes to attributes in the user account, changes of entitlements or privileges associated with the user account, locking and unlocking the user account, and even deletion of the user account. User provisioning is primarily an admin-time affair: a user account is created (or changed) based on an administrative action as opposed to a user’s action at the time of resource use. This article explores the uses and components of a user-provisioning system and focuses mainly on situations where user accounts are maintained in central repositories, typically enterprise and workforce settings.

Keywords: user provisioning, enterprise, digital identity

@column
## 概要

ユーザー・プロビジョニングとは、システム（例えば、データベース、SaaSアプリ、オペレーティング・システムなど）においてユーザーアカウントを作成し、メンテナンスする手段です。ユーザー・プロビジョニング・システムがユーザー・アカウントをメンテナンスしていると表現するとき、ユーザーアカウントの属性の変更、ユーザーアカウントに関連するエンタイトルメントまたは特権の変更、ユーザーアカウントのロックとロック解除、さらにはユーザーアカウントの削除まで、あらゆることを意味します。 ユーザー・プロビジョニングは、主に管理時間の問題です：つまり、ユーザーアカウントはリソース使用時のユーザのアクションとは対照的に、管理者のアクションに基づいて作成（または変更）されます。この記事では、ユーザー・プロビジョニング・システムの用途とコンポーネントを検討し、主にユーザーアカウントが中央リポジトリで管理される状況、一般に企業や従業員の状況に焦点を当てます。

Keywords: ユーザー・プロビジョニング, エンタープライズ, デジタル・アイデンティティ

@row
By Ian Glazer, Lori Robinson, and Mat Hamlin

© 2022 IDPro, Ian Glazer, Lori Robinson, Mat Hamlin

@row
## Introduction

Creating and managing user accounts is the bedrock of any IAM system. The process is generally referred to as user provisioning and is used to establish the entitlements a user is given to access restricted resources (applications, documents or databases) maintained by the organization. User provisioning processes not only create user accounts and assign entitlements but also maintains those user account entitlement through the detection of meaningful lifecycle events such as changes to job responsibility and the application of policies to ensure. User provisioning is often used to ensure the right people have access to the right systems in a timely fashion and with entitlement appropriate for their responsibilities.

@column
## 導入

ユーザーアカウントの作成と管理は、IAMシステムの根幹をなすものです。このプロセスは一般にユーザー・プロビジョニングと呼ばれ、組織がメンテナンスする制限付きリソース（アプリケーション、ドキュメントやデータベース）にアクセスするためにユーザに与えられるエンタイトルメントを確立するために使用されます。ユーザー・プロビジョニング・プロセスは、ユーザーアカウントを作成してエンタイトルメントを割り当てるだけでなく、職務の変更など意味のあるライフサイクルイベントの検出やポリシーの適用を通じて、それらのユーザーアカウントのエンタイトルメントをメンテナンスします。ユーザー・プロビジョニングは、多くの場合、適切な人が適切なシステムにタイムリーにアクセスし、その責任に適したエンタイトルメントを持つことを保証するために使用されます。

@row
### Terminology

*   **Authoritative source(s):** The system of record (SOR) for identity data; an organization may have more than one authoritative source of data in their environment.
    
*   **Entitlement catalog:** A database of entitlements and their related metadata. The catalog includes an index of entitlement data pulled from business systems, applications, and platforms, as well as technical and business descriptions of the entitlements or their use
    
*   **Identity lifecycle management:** A process that detects changes in authoritative systems of record and updates identity records based on policies.
    
*   **Identity repository:** The identity repository is a directory or a database that can be referenced by external systems and services (such as authentication or authorization services).
    
*   **Reconciliation:** The process of identifying and processing changes to users and user access made directly on target systems.
    
*   **User provisioning** : the means by which user accounts are created, maintained, and deactivated/deleted in a system according to defined policies.
    

@column
### 用語解説

*   **権威あるソース** ：アイデンティティ・データのための記録システム（SOR）；組織は、その環境に複数の権威あるデータソースを持つことができます。
    
*   **エンタイトルメント・カタログ** ：エンタイトルメントとそれに関連したメタデータのデータベース。カタログにはビジネスシステム、アプリケーション、およびプラットフォームから取得したエンタイトルメント・データのインデックスと、エンタイトルメントまたはその使用に関する技術的およびビジネス的な説明が含まれています。
    
*   **アイデンティティライフサイクル管理** ：権限のある記録システムでの変更を検出し、ポリシーに基づいてアイデンティティ・レコードを更新するプロセス。
    
*   **アイデンティティ・リポジトリ** ：アイデンティティ・リポジトリは、外部システムおよびサービス（認証サービスや認可サービスなど）から参照できるディレクトリまたはデータベースです。
    
*   **調整** ：ターゲットシステムで直接おこなわれたユーザーおよびユーザーアクセスへの変更を特定して処理するプロセス。
    
*   **ユーザー・プロビジョニング** ：定義されたポリシーに従ってシステム内でユーザーアカウントを作成、メンテナンス、非アクティブ化/削除する手段。
    

@row
### What is User Provisioning?

User provisioning is setting up the entitlements for users to the resources to which they need access. User-provisioning technologies are deployed across multiple industries, including healthcare, education, financial services, government, retail, manufacturing, technology, etc.

Functionality supported by user-provisioning technologies include:

**Identity lifecycle management:** An identity and its associated attributes are the basis for authentication and authorization decisions made in an environment. It is, therefore, essential that the identity record is maintained. Provisioning systems detect changes in authoritative systems of record (such as a Human Resources database/repository) and update the identity record accordingly.

**User account provisioning:** As the name suggests, a user-provisioning system’s primary function is user account provisioning (and de-provisioning). User-provisioning technologies automate the creation, maintenance, and deactivation/deletion of user accounts on target systems according to defined policies.

**Self-service and delegated administration:** User-provisioning systems provide interfaces that allow users to request access to systems, manage passwords and update their data. Delegated administrators can perform similar tasks such as onboarding and off-boarding users, password changes, profile updates, and entitlement assignments on behalf of others.

**Workflow:** Provisioning systems employ workflow tools that allow for the automation of provisioning processes and approval workflows. Using automated approval workflows, business stakeholders can validate and approve proposed changes before they are applied to target systems. While many decisions to grant access are automated through policy, others may require human intervention.

**Audit and Reporting:** Provisioning systems log all identity lifecycle management, access policies, and user provisioning transactions and provide reporting mechanisms to extract the logged data.

A note about governance: User-provisioning systems are often packaged with identity governance capabilities such as access review and certification, risk analysis, and identity analytics. The combined user provisioning and identity governance solutions may be referred to as Identity Governance and Administration (IGA). This document focuses exclusively on user-provisioning functionality and does not include identity governance information. Similarly, password management, which may be packaged with provisioning solutions, is not covered in this document.

@column
### ユーザー・プロビジョニングとは何か？

ユーザー・プロビジョニングとは、ユーザがアクセスする必要のあるリソースに対してユーザのエンタイトルメントを設定することです。ユーザー・プロビジョニング技術は、ヘルスケア、教育、金融サービス、政府、小売、製造、テクノロジーなどさまざまな業界で展開されています。

ユーザー・プロビジョニング技術でサポートされる機能は以下の通りです：

**アイデンティティライフサイクル管理**： アイデンティティとその関連属性は、環境内で実施される認証と認可の決定の基礎です。したがって、アイデンティティの記録をメンテナンスすることが不可欠です。プロビジョニングシステムは、（人事データベース/リポジトリのような）権威ある記録システムの変更を検出し、それによって記録を更新します。

**ユーザーアカウント・プロビジョニング**： その名が示すように、ユーザー・プロビジョニングシステムの主な機能は、ユーザーアカウントのプロビジョニング（およびデプロビジョニング）です。ユーザー・プロビジョニング技術は、定義されたポリシーに従って、ターゲットシステム上のユーザーアカウントの作成、メンテナンス、非活性化/削除を自動化しています。

**セルフサービスと委譲された権限**： ユーザー・プロビジョニングシステムは、ユーザーがシステムへのアクセス権を要求し、パスワードを管理し、データを更新することができるインターフェースを提供します。権限委譲された管理者は、ユーザーのオンボーディングとオフボーディング、パスワードの変更、プロファイルの更新、エンタイトルメントの割り当てなど、同様のタスクを他の人に代わって実行することができます。

**ワークフロー**： プロビジョニングシステムは、プロビジョニングプロセスと承認ワークフローの自動化を可能にするワークフローツールを採用しています。自動化された承認ワークフローを使用することで、ビジネス・ステークホルダーは、提案された変更をターゲットシステムに適用する前に検証し、承認することができます。アクセス権の付与に関する多くの決定はポリシーによって自動化されていますが、その他の決定には人間の介入が必要な場合があります。

**監査と報告**： プロビジョニングシステムは、すべてのアイデンティティライフサイクル管理、アクセスポリシーおよびユーザー・プロビジョニング処理を記録し、記録されたデータを抽出するためのレポート機能を提供します。

ガバナンスに関する注意点： 多くの場合、ユーザー・プロビジョニングシステムはアクセスレビューや認定、リスク分析、アイデンティティ分析などのアイデンティティ・ガバナンス機能とともにパッケージ化されています。ユーザー・プロビジョニングとアイデンティティ・ガバナンスを組み合わせたソリューションは、アイデンティティ・ガバナンスと管理（IGA）と呼ばれることがあります。本稿では、ユーザー・プロビジョニング機能のみに焦点を当て、アイデンティティ・ガバナンスに関する情報は含んでいません。同様に、プロビジョニング・ソリューションとパッケージ化される可能性のあるパスワード管理も扱いません。

@row
### Business Drivers for Automated User Provisioning

Three primary business drivers justify the deployment of automated user-provisioning systems:

*   **Operational efficiency** : The amount of administrative overhead associated with the manual creation and maintenance of user accounts is significant for medium- to large-size organizations. Without an automated process, it may be weeks before a user has access to the resources they need to perform their job duties or other tasks. User-provisioning systems automate the user account management process, reducing administrative overhead and improving time to productivity, resulting in operational efficiency.
    
*   **Security:** Manual provisioning of user accounts may lead to security gaps such as overprivileged user accounts or orphaned accounts (active accounts assigned to inactive employees). Automated user account provisioning systems improve security by ensuring that user accounts and entitlements are provisioned according to policy and deprovisioned in a timely manner.
    
*   **Compliance** : Various laws and regulations require organizations to demonstrate control over access to critical systems, resources, and data. User-provisioning systems enforce policy-based access controls and allow organizations to demonstrate the efficacy of these controls with reporting and attestation capabilities.
    

@column
### 自動化されたユーザー・プロビジョニングに向けたビジネス推進要因

自動化されたユーザー・プロビジョニングシステムの展開を正当化する3つの主たるビジネス推進要因は以下のとおりです：

*   **運用効率**： 中規模から大規模の組織では、ユーザーアカウントの手動作成とメンテナンスに関する管理オーバーヘッドが非常に大きくなります。自動化されたプロセスがなければ、ユーザーが職務やその他のタスクを実行するために必要なリソースにアクセスできるようになるまでに数週間かかることもあります。 ユーザー・プロビジョニングシステムはユーザーアカウント管理プロセスを自動化することで、管理者のオーバーヘッドを削減し、生産性向上までの時間を短縮し、結果として業務効率を向上させます。
    
*   **セキュリティ**： ユーザーアカウントの手動プロビジョニングは、過剰権限のユーザーアカウントや孤児アカウント（アクティブでない従業員に割り当てられたアクティブなアカウント）などのセキュリティギャップにつながる可能性があります。自動化されたユーザーアカウント・プロビジョニングシステムは、ユーザーアカウントとエンタイトルメントがポリシーに従ってプロビジョニングされ、タイムリーにデプロビジョニングされることを保証することにより、セキュリティを向上させます。
    
*   **コンプライアンス**： 様々な法律や規制により、組織は重要なシステム、リソース、データへのアクセス制御を実証することが求められています。ユーザー・プロビジョニングシステムは、ポリシーベースのアクセス制御を実施し、レポートと認証機能により、これらの制御の有効性を証明することができます。
    

@row
## User Provisioning Logical Architecture

User-provisioning systems employ policies, workflows, and connectors to synchronize identity data from an authoritative system to an identity store and to provision user accounts to target applications.

@column
## ユーザー・プロビジョニングの論理アーキテクチャ

ユーザー・プロビジョニングシステムはポリシー、ワーウフローとコネクタを使用して、アイデンティティデータを権威あるシステムからアイデンティティ・ストアに動悸させ、ユーザーアカウントをターゲットアプリケーションにプロビジョニングします。

@row
![](/assets/images/idpro_bok/UP-figure1.png)

Figure 1 illustrates the standard architectural components of a user-provisioning ecosystem.

@row
**Authoritative source(s):** The system of record (SOR) for identity data. The authoritative system publishes changes to the provisioning system. There may be more than one authoritative system in the environment. For example, in workforce use cases, the Human Capital Management (HCM) / Human Resources (HR) system may be the SOR for employee data, but contractor data may be stored in a procurement system.

**Target system(s):** Target systems subscribe to changes to identity records and are on the receiving end of the provisioning process. The provisioning system creates and manages user accounts and associated entitlements within the target system environment.

**Connectors:** The integration layer between the provisioning system and authoritative and target systems. There are various types of connectors: proprietary (application-specific connectors that communicate with app-specific APIs), generic (e.g., LDAP, JDBC, delimited text), or standards-based. See the standards section for more information on standards-based connectivity.

**Provisioning server:** The middleware layer responsible for data synchronization, mapping, and transformation; the application of business logic and access policies; and the orchestration of provisioning process flows. The provisioning server is comprised of the following functional components:

*   **Account correlation rules:** correlates or matches disparate user accounts (in target or authoritative systems) with a single identity record and ensure that duplicate identities for a single person/entity are not created.
    
*   **Data mapping rules:** maps and transforms data from the source context to the target context.
    
*   **Account creation rules:** establishes standards for creating an identity record such as naming conventions, required attributes, password policy, location policy, etc.
    
*   **Access policies** : determines access rights and entitlements that should be assigned to a user. See the Policies section for information on different types of access policies.
    
*   **Workflow engine:** orchestrates the provisioning based on business processing logic and enables access request, approval, and review workflows.
    
*   **Reconciliation engine:** discovers user accounts created directly in target systems (circumventing standard provisioning processes), ensures that the user account is in compliance with access policies, and correlates the user account with the individual’s identity record.
    

**Identity repository:** Identity records are stored in an identity repository. The identity repository is a directory or a database that can be referenced by external systems and services (such as authentication or authorization services). The identity record includes attributes associated with the identity and a record of all user accounts associated with the identity.

**Entitlement catalog:** A database of entitlements and their related metadata. The catalog includes an index of entitlement data pulled from business systems, applications, and platforms. The entitlement data can be enriched with metadata such as risk scores and business-friendly descriptions of entitlements that can be displayed to users during access requests, access reviews, and certifications.

**System configuration and audit store:** A dedicated repository to hold information such as system configuration, identity mapping, policy, role definition, and workflow data. This repository may also serve as the store for audit logs.

**User interfaces:** User-provisioning systems include administrative, end-user, and delegated administration interfaces. Administrative interfaces are used for the set-up and configuration of the system. End-user and delegated administration interfaces are used for access requests, approval workflows, reporting, profile updates, etc. Provisioning systems typically include web-based interfaces that can be accessed from a pc or mobile device. While not standard, some provisioning vendors offer a mobile app for self-service and approval workflows.

Given their highly connected and interactive nature, user-provisioning systems must be open and extensible. The provisioning provider should provide open APIs, no or low code workflows, and generic connectors that allow for flexibility in the system.

@column
**権威あるソース**： アイデンティティ・データ用の記録システム（SOR）。権威あるシステムは、プロビジョニング・システムに変更を発行します。環境には1 つ以上の権威システムが存在するかもしれません。たとえば、従業員のユースケースでは、人的資本管理（HCM）/人事（HR）システムが従業員データのSORになる場合がありますが、契約者データは調達システムに格納される場合があります。

**ターゲットシステム**： ターゲットシステムはアイデンティティ・レコードへの変更をサブスクライブし、プロビジョニングプロセスの受信側に存在します。プロビジョニングシステムは、ターゲットシステム環境内でユーザーアカウントと関連するエンタイトルメントを作成および管理します。

**コネクター**： プロビジョニングシステムと権威があるターゲットシステムの間の統合レイヤー。コネクターにはさまざまな種類があります：独自仕様（アプリ固有のAPIと通信するアプリケーション固有のコネクター）、汎用（例えばLDAP、JDBC、区切りテキスト）、または標準ベース。標準ベースの接続の詳細については、標準のセクションを参照してください。

**プロビジョニングサーバー**： データの同期、マッピングおよび変換を担当するミドルウェアレイヤー；ビジネスロジックとアクセスポリシーのアプリケーション；そして、プロビジョニングプロセスフローのオーケストレーション。プロビジョニングサーバーは、次の機能コンポーネントで構成されています：

*   **アカウント相関ルール**： （ターゲットまたは権威あるシステム内の）異なるユーザーアカウントを単一のアイデンティティ・レコードと関連付けまたは照合し、単一の個人/エンティティの重複アイデンティティが作成されないようにします。
    
*   **データマッピングルール**： ソースコンテキストからターゲットコンテキストにデータをマッピングおよび変換します。
    
*   **アカウント作成ルール**： 命名規則、必須属性、パスワードポリシー、ロケーションポリシーなどのようにアイデンティティ・レコードの作成するための標準を確立します。
    
*   **アクセスポリシー**： ユーザーに割り当てる必要のあるアクセス権と資格を決定します。様々な種類のアクセスポリシーについては、ポリシーセクションを参照してください。
    
*   **ワークフローエンジン**： ビジネス処理ロジックに基づくプロビジョニングをオーケストレーションし、アクセス要求、承認およびレビューワークフローを有効にします。
    
*   **調整エンジン**： ターゲットシステムで直接作成された（標準のプロビジョニングプロセスを回避した）ユーザーアカウントを発見し、ユーザーアカウントがアクセスポリシーに準拠していることを確認し、ユーザーアカウントを個人のアイデンティティ・レコードと関連付けます。
    

**アイデンティティ・リポジトリ**： アイデンティティ・レコードはアイデンティティ・リポジトリに格納されます。アイデンティティ・リポジトリは、外部システムおよびサービス（認証または認可サービスのような）から参照できるディレクトリまたはデータベースです。アイデンティティ・レコードには、アイデンティティに紐づく属性およびアイデンティティに紐づく全てのユーザーアカウントのレコードを含みます。

**エンタイトルメントカタログ**： エンタイトルメントとその関連メタデータのデータベース。カタログは、ビジネスシステム、アプリケーションおよびプラットフォームから取得したエンタイトルメントデータのインデックスを含みます。エンタイトルメントデータは、リスクスコアやアクセス要求、アクセスレビューおよび認定の際にユーザーに表示するエンタイトルメントのビジネスフレンドリーな説明のようなメタデータで強化することができます。

**システム構成および監査ストア**： システム構成、アイデンティティ・マッピング、ポリシー、ロール定義、ワークフローデータなどの情報を保持するための専用リポジトリ。このリポジトリは、監査ログのストアとしても機能することがあります。

**ユーザーインターフェース**： ユーザー・プロビジョニングシステムには、管理者用インタフェース、エンドユーザ用インタフェースおよび委譲管理者用インタフェースがあります。管理者用インターフェイスは、システムのセットアップと構成に利用されます。エンドユーザーおよび委譲管理者用インターフェイスは、アクセス要求、承認ワークフロー、レポート、プロファイルの更新などに利用されます。通常、プロビジョニングシステムにはPCやモバイル機器からアクセスできるウェブベースのインターフェイスが含まれています。標準ではありませんが、一部のプロビジョニングベンダーはセルフサービスと承認ワークフロー用のモバイルアプリを提供しています。

強い関連性と相互作用的な性質を考えると、ユーザー・プロビジョニングシステムはオープンで拡張可能でなければなりません。プロビジョニングプロバイダーは、システムの柔軟性を持たせることを可能にするオープンAPI、ノーコードまたはローコードのワークフローおよび汎用コネクタを提供すべきです。

@row
## User Provisioning Process Flow

User-provisioning technologies allow organizations to efficiently manage thousands of identities by capturing lifecycle events and ensuring that user accounts and their associated privileges are kept up-to-date and accurate. These processes reduce administrative overhead and improve security. That said, automated user account provisioning is a complex, multifaceted process that includes three distinct phases:

*   **Event trigger** : A business event or a change to an identity that triggers a provisioning action
    
*   **Policy administration** : Application of access policies that bind the identity to specific user accounts and entitlements
    
*   **User account provisioning** : Creation, maintenance, deactivation, or deletion of user accounts in target applications
    

@column
## ユーザー・プロビジョニングプロセスフロー

User-provisioning technologies allow organizations to efficiently manage thousands of identities by capturing lifecycle events and ensuring that user accounts and their associated privileges are kept up-to-date and accurate. These processes reduce administrative overhead and improve security. That said, automated user account provisioning is a complex, multifaceted process that includes three distinct phases:

*   **Event trigger** : A business event or a change to an identity that triggers a provisioning action
    
*   **Policy administration** : Application of access policies that bind the identity to specific user accounts and entitlements
    
*   **User account provisioning** : Creation, maintenance, deactivation, or deletion of user accounts in target applications
    

@row
### Event Trigger

The act of provisioning begins with an event. Such an event could be:

*   The creation of a new employee in an HR system.
    
*   A modification to an entry in Active Directory moving a person from one business unit to another.
    
*   A ticket being created in an IT Service Management (ITSM) or Help Desk ticketing system.
    
*   A person directly interacting with the provisioning system to request a change to a user account.
    

There are three primary types of events:

*   Join
    
*   Move
    
*   Leave
    

Joiners, Movers, and Leavers (JML) are grist for the user provisioning mill. Managing JML processes becomes the work of an identity system. This work includes connecting the user-provisioning system to trigger sources and then constructing policies to be evaluated for each event type for each target system.

@column
### イベントトリガー

プロビジョニングのアクションはイベントから始まります。プロビジョニングを始めるようなイベントには次のようなものがあります：

*   HRシステムでの新しい従業員を作成する
    
*   あるビジネスユニットから別のビジネスユニットに人員を移動させるようなActive Directoryエントリの変更をおこなう
    
*   ITサービス管理（ITSM）またはヘルプデスクチケットシステムでチケットを作成する
    
*   人間がプロビジョニングシステムと直接操作して、ユーザーアカウントの変更を要求する
    

イベントには主に3つのタイプがあります：

*   Join
    
*   Move
    
*   Leave
    

Joiner、Movers、Leaver（JML）は、ユーザー・プロビジョニングの要です。JMLプロセスの管理は、アイデンティティシステムの作業になります。この作業には、ユーザー・プロビジョニングシステムをトリガーソースに接続し、各ターゲットシステムのイベントタイプごとに評価されるポリシーを構築することが含まれます。

@row
#### Join

The easiest way to think about the Join event is when a new employee joins a company. She needs her benefits and payroll set up along with user accounts in IT systems. In its purest sense, Join events are meant to create a net new identity and net new user accounts in IT systems. [^1]

@column
#### Join

Joinイベントを考える最も簡単な方法は、新入社員が会社に入社するときです。彼女は、ITシステムのユーザーアカウントとともに、福利厚生や給与計算を設定する必要があります。最も純粋な意味において、JoinイベントはITシステムに新しいアイデンティティと新しいユーザーアカウントを作成することを意味します。 [^1]

@row
#### Move

When a person changes roles with an enterprise, she likely needs access to new business systems and to have access to her older ones removed. This is the purpose of the Move event. You can think of Move as a change in the relationship between the organization and person. They might change which business unit they report to, get promoted, or change their last name. [^2]

@column
#### Move

ある人が企業で役割を変えるとき、おそらく新しいビジネスシステムへのアクセスが必要になり、古いものへのアクセスを削除する必要があります。これがMoveイベントの目的です。Moveイベントは、組織と個人との関係の変化と考えることができます。例えば、所属するビジネスユニットが変わったり、昇進したり、姓が変わったりすることがあります。 [^2]

@row
#### Leave

A person retiring is the simplest example of a Leave event. In such a case, the person’s user accounts need to be deleted or at least locked to prevent further use in all target systems. Another example is when a contractor’s project concludes and the contract ends. The story is the same; a Leave event triggers the user-provisioning system to remove their access.

User-provisioning technologies provide various mechanisms to capture JML events, including:

*   **Automated provisioning:** The user-provisioning system “listens” for events from systems of record such as Human Resources, ITSM, or a directory.
    
*   **Batch processing:** The provisioning system executes a regularly scheduled process that polls an authoritative source for changes and generates an output file.
    
*   **Self-service request:** Today’s user provisioning solutions include an end-user access request portal where end-users or managers can request access to specific systems and rights needed to perform their business responsibilities. The user or a delegated administrator updates the user profile or makes an access change request via the self-service interface.
    
*   **Manual/Ticket:** In some instances, an organization may use a ticketing system or other manual process to notify the identity team of a change needed on the identity record. In this case, the identity administrator would update the identity record directly to trigger downstream policy and provisioning activities.
    
*   **Reconciliation event:** Reconciliation is the process of identifying and processing changes to users and user access made directly on target systems. When an organization configures a user provisioning solution for centralized management of user access, that does not prevent changes from occurring directly on a target system. So, to ensure the consistency of user access and user attributes across the organization, the user-provisioning system will periodically _**reconcile**_ what it knows about users and their access to a specific target system. This reconciliation is accomplished by gathering and comparing all user data on the target system (full reconciliation) or by processing known changes to user access based on a changelog or other time-based query. When changes or variances are identified in a reconciliation process, events are triggered and processed based on defined policies. The result of reconciliation could be to synchronize changes from the target system to other systems, or it could be to roll back any locally applied changes that occurred outside of the user provisioning solution.
    

@column
#### Leave

退職は、Leaveイベントの最もシンプルな例です。このような場合、その人のユーザーアカウントは削除するか、少なくとも対象システムすべてで今後使用できないようにロックする必要があります。もう一つの例は、請負業者のプロジェクトが終了し、契約が終了した場合です。同じように；Leaveイベントが発生すると、ユーザープロビジョニングシステムはその人のアクセスを削除することになります。

ユーザープロビジョニング技術はJMLイベントを捕捉するために、以下のような様々なメカニズムを提供します：

*   **自動化されたプロビジョニング**：ユーザープロビジョニングシステムは、人事部、ITSMやディレクトリのような記録システムからのイベントを「リッスン」します。
    
*   **バッチ処理**：プロビジョニングシステムは定期的にスケジュールされたプロセスを実行し、権威あるソースに変更を問い合わせ、出力ファイルを生成します。
    
*   **セルフサービスのリクエスト**：今日のユーザープロビジョニングソリューションには、エンドユーザーのアクセス要求ポータルが含まれており、エンドユーザーやマネージャーは、ビジネス上の責任を果たすために必要な特定のシステムや権利へのアクセスを要求することができます。ユーザーまたは委譲された管理者は、セルフサービスインターフェースを介してユーザープロファイルを更新したり、アクセス権変更のリクエストをおこなったりします。
    
*   **手動/チケット**：場合によっては、組織はアイデンティティ・レコードに必要な変更をアイデンティティチームに通知するために、チケットシステムまたは他の手動プロセスを使用することがあります。この場合、アイデンティティ管理者はアイデンティティ・レコードを直接更新し、下流のポリシーおよびプロビジョニング活動を開始します。
    
*   **リコンシリエーションイベント**：リコンシリエーションは、ターゲットシステム上で直接おこなわれたユーザーおよびユーザーアクセスへの変更を特定し、処理するプロセスです。組織がユーザーアクセスの集中管理のためにユーザープロビジョニングソリューションを構成する場合、ターゲットシステム上で直接発生する変更を防ぐことはできません。そこで、組織全体のユーザーアクセスとユーザー属性の一貫性を確保するために、ユーザープロビジョニングシステムは特定のターゲットシステムに対するユーザーとそのアクセスについて知っていることを定期的に _**照合（reconcile）**_ ことになります。この照合は、ターゲットシステム上のすべてのユーザーデータを収集して比較すること（完全な照合）、または変更ログやその他の時間ベースのクエリに基づいてユーザーアクセスに対する既知の変更を処理することによって実施されます。照合プロセスで変更または差異が特定されると、定義されたポリシーに基づいてイベントがトリガーされ、処理されます。照合の結果、ターゲットシステムから他のシステムに変更が同期されることもあれば、ユーザープロビジョニングソリューションの外部で発生したローカルに適用された変更がロールバックされることもあり得ます。
    

@row
### Policy Administration

In the past, organizations have managed users’ access to target systems in an ad hoc manner; given the complexities of the enterprise environment, this is no longer viable. They need documented rules to determine who should have access to which target systems; furthermore, they need to control what kind of entitlements and privileges people have in those target systems. This is the role of policies in a user-provisioning system. Instead of leaving the details to an administrator to determine which groups a user account ought to be a member of, a policy can describe which groups are required, optional, and even forbidden for people to be a member of.

A policy can be thought of as a way to bind groups of people to groups of target systems with groups of related access (entitlements, privileges, etc.) In this way, there are always two components of user provisioning: Who and What. The Who portion of the policy describes the inclusion criteria for which people the policy will apply. For example, all full-time employees, contractors, and finance people are all examples of the Who portion of a policy. The What portion of the policy describes the user accounts and associated entitlements and privileges a person gets. The What can be very coarse-grained, for example, the creation of a user account in all target systems, to very fine-grained, as when this specific entitlement and these two specific privileges are created in the target system.

Different kinds of policies use different combinations of Who and What to help identity practitioners govern access. While the overall topic of policies can be extremely broad, for the purposes of this article, let’s focus on four kinds of policies:

*   Birthright
    
*   Role-based
    
*   Segregation of duties
    
*   Workflow approvals
    

It is important to note that a user provisioning process won’t have just a single policy for a target system or event. Policies can be combined and applied to multiple target systems and triggering events.

@column
### ポリシー管理

これまで、組織はターゲットシステムへのユーザのアクセスを場当たり的に管理してきました；複雑な企業環境を考慮すると、これはもはや実行不可能です。誰がどのターゲットシステムにアクセスすべきかを決定するための文書化されたルールが必要です；さらにターゲットシステムにおいて人々がどのようなエンタイトルメントと特権を持つかを管理する必要があります。これが、ユーザープロビジョニングシステムにおけるポリシーの役割です。ユーザーアカウントがどのグループのメンバーであるべきか、その詳細を管理者に任せるのではなく、ポリシーによってどのグループが必須かオプションか、さらにはメンバーであることを禁じているのかを記述することができるのです。

ポリシーは、人々のグループを、関連するアクセス（エンタイトルメント、特権など）のグループとターゲットシステムのグループに結びつける方法と考えることができます。このように、ユーザー・プロビジョニングには、常に2つの要素があります：誰と何です。ポリシー誰の部分には、そのポリシーがどのような人々に適用されるかという包含基準が記述されます。例えば、すべての従業員、業務委託者、財務担当者などはすべて、ポリシーの「誰」の部分の例です。ポリシーの「何」の部分は、その人が取得するユーザーアカウントと関連するエンタイトルメントや特権を記述します。例えば、すべてのターゲットシステムでユーザーアカウントを作成するという非常に粗い粒度のものから、ターゲットシステムでこの特定のエンタイトルメントとこの2つの特定の特権を作成するという非常に細かい粒度のものまで、「何」の部分にはさまざまなものがあります。

異なる種類のポリシーは、アイデンティティ実務者がアクセスを管理するために「誰」と「何」の異なる組み合わせを利用します。ポリシーの全てのトピックとなると非常に広範になりますが、この記事では4種類のポリシーに焦点を当てます：

*   生得権（Birthright）
    
*   ロールベース
    
*   職務分掌
    
*   ワークフロー承認
    

ユーザープロビジョニングプロセスは、ターゲットシステムやイベントに対して単一のポリシーだけを持つわけではないことに注意することが重要です。複数のターゲットシステムやトリガーとなるイベントに対して、ポリシーを組み合わせて適用することができます。

@row
#### Birthright

There are specific systems and entitlements that often broad swaths of the organization need; this kind of access is considered a birthright. Examples of such policies include:

*   All full-time employees need email, calendar, collaboration, and file sharing.
    
*   Everyone in the Finance department needs at least minimal access to the financial reporting system.
    
*   Interns need access to the ‘Intern Team Excellence’ collaboration channel.
    

Birthright policies can be thought of as defining access that is fundamental to certain kinds of people who have a relationship with the organization. Such access does not need additional scrutiny, review, or approval; simply by being a person who matches the criteria of the policy (such as being a member of the Finance department) that person is allowed to have and will get user accounts in certain systems with specified levels of access (as managed by their user account’s associated entitlements and privileges.) More often than not, birthright policies grant coarse-grained access to target systems; that is to say, they might only give someone a user account in an email system but not necessarily access to specific distribution groups. Birthright policies are most commonly applied as part of a Join event and typically occur by assigning one or more business roles. Birthright events can also happen as a part of a Move event, specifically when a person moves from one business function to another. For example, when a person is hired into the Accounting division within an organization, they’d receive birthright access to things like email and the productivity suite and basic access to critical accounting systems. When that person then transfers to Corporate Strategy, they lose access to the account systems, gain access to budget forecasting systems, and continue to retain access to email and productivity tools.

@column
#### 生得権

しばしば組織全体が必要とする特定のシステムやエンタイトルメントがあり、この種のアクセス権は生得権とみなされます。このようなポリシーには、次のような例があります：

*  すべてのフルタイム従業員は、電子メール、カレンダー、コラボレーション、およびファイル共有が必要です。
    
*   財務部門の社員は、財務報告システムへ最低限アクセスする必要がある。
    
*   インターンは、「Intern Team Excellence」コラボレーションチャンネルにアクセスする必要がある。
    

生得権ポリシーは、組織と関係のある特定の種類の人々にとって基本的なアクセス権を定義するものと考えることができます。このようなアクセス権には、追加の精査、レビューまたは承認は必要ありません；単にポリシーの基準に一致する人（財務部門のメンバーなど）であることによって、その人は特定のアクセスレベル（そのユーザーアカウントの関連エンタイトルメントと特権によって管理される）で特定のシステムのユーザーアカウントを持つことが許され、それを取得することができます。多くの場合、生得権ポリシーはターゲットシステムに対して荒い粒度のアクセス権を付与します；つまり、ある人に電子メールシステムのユーザーアカウントを与えるだけかもしれませんが、特定の部門グループへのアクセス権は与える必要はありません。生得権ポリシーは、最も一般的にはJoinイベントの一部として適用され、通常1つまたは複数のビジネスロールを割り当てることによって発生します。生得権イベントは、Moveイベントの一部として発生することもあり、具体的にはある人があるビジネス部門から別の部門に異動するときに発生します。たとえば、ある組織の経理部門に採用された場合、その人は電子メールやオフィススイート、重要な会計システムへの基本的なアクセス権などの権利を得ます。しかし、その人が経営企画部に異動すると、会計システムへのアクセス権は失われ、予算予測システムへのアクセスが可能になり、電子メールとオフィスツールへのアクセス権は継続されます。

@row
#### Role-based

Because an organization can have many business functions and thus lots of different business responsibilities as well as tens of thousands of individual entitlements in their systems, there is no way to manage who gets access at an individual level. Trying to do so would quickly lead to the management of tens of millions of combinations of people and privileges. User-provisioning systems attempt to bring order to this chaos by using roles to aggregate people and entitlements into more manageable policy components.

Much is made of roles in identity management. [^3] Roles can come in a variety of flavors; this article focuses on business roles and technical roles. A business role is a way to aggregate people who share the same business responsibilities. For example, a retail banking organization might have a business role called “Teller” and use it to describe the access appropriate for people who work as tellers. The second kind of role we’ll need to understand for this article is a “Technical” role. A technical role is a way to aggregate the entitlements and privileges required within one or more target systems to perform a task. For example, the same retail bank could have a technical role called “Check and Update Balances,” which gives user accounts in their systems the ability to check and update savings account balances.

A role-based policy in a user-provisioning system uses business and technical roles to govern access for more specific sets of people, entitlements, and privileges in target systems than birthright policies do. For example, a user-provisioning system might have a birthright policy that gives all full-time employees access to email. An additional role-based policy might grant Tellers access to a specific mailing list and shared drive.

@column
#### ロールベース

組織には多くのビジネス機能があり、そのため多くの異なるビジネス責任と何万もの個人のエンタイトルメントがシステムに存在するため、誰がアクセス権を持つかを個人レベルで管理する方法はありません。これを実現しようとすると、何千万という人と権限の組み合わせを管理することになります。ユーザープロビジョニングシステムは、このカオスに秩序をもたらすために、ロールを使って人とエンタイトルメントを集約し、より管理しやすいポリシーコンポーネントにすることを試みています。

アイデンティティ管理において、多くの場合ロールが利用されます。 [^3] ロールにはさまざまな種類があります；この記事ではビジネスロールとテクニカルロールに焦点を当てます。ビジネスロールは、同じビジネス責任を共有する人々を集約する方法です。例えば、リテールバンキング組織は「テラー」というビジネスロールを持ち、テラーとして働く人に適したアクセス権を記述するために使用することができます。この記事で理解する必要がある2つ目のロールは、「テクニカル」ロールです。テクニカルロールは、あるタスクを実行するために1つまたは複数の対象システムで必要とされるエンタイトルメントおよび特権を集約する方法です。例えば、同じリテールバンクが「Check and Update Balances」というテクニカルロールを持ち、そのシステム内のユーザーアカウントに普通預金口座の残高を確認および更新する能力を与えることができます。

ユーザープロビジョニングシステムのロールベースのポリシーは、ビジネスロールおよびテクニカルロールを使用し、対象システムにおける特定の人々、エンタイトルメントおよび特権のセットに対するアクセス権を生得権ポリシーよりも管理するものです。たとえば、ユーザープロビジョニングシステムには、すべてのフルタイム従業員に電子メールへのアクセス権を与える生得権ポリシーがあるとします。さらにロールベースのポリシーによって、テラーに特定のメーリングリストと共有ドライブへのアクセスを許可することができます。

@row
#### Segregation of Duties

Stemming from the fallout of the WorldCom and Enron accounting scandals, the Sarbanes-Oxley Act had a profound impact on business practices. [^4] These impacts made their way to user provisioning. As part of compliance activities, organizations looked to their user provisioning policies to not only grant access to people but also prevent “toxic combinations” of access. A toxic combination of access is one in which a person has privileges that could enable some form of fraud, such as the ability to create a new vendor and issue a payment to that vendor. This combination of access would allow a bad actor to create a fictitious company in the financial system and then divert monies to that company. Another application of a toxic combination policy is to prevent anyone who isn’t a system administrator from having system admin or highly privileged entitlements.

If roles are a way of describing what someone should have, then segregation of duty (SoD) policies are a way of describing what they must not have. Such policies are typically evaluated when a provisioning event is triggered so new toxic combinations are not introduced into target systems and existing ones are detected and remediated.

@column
#### 職務分掌

WorldCom社とEnron社の会計スキャンダルに端を発し、Sarbanes-Oxley法はビジネス慣習に大きな影響を与えました。 [^4] この影響は、ユーザープロビジョニングにも及んでいます。コンプライアンス活動の一環として、組織はユーザーへのアクセス権を付与するだけでなく、アクセス権の「有害な組み合わせ」を防止するためのユーザープロビジョニングポリシーに注目しました。アクセス権の有害な組み合わせとは、例えば、新しいベンダーを作成し、そのベンダーに支払いをおこなうことができるなど、ある種の不正行為を可能にするような権限を持つユーザーのことです。このようなアクセス権の組み合わせでは、悪質な行為者が金融システム内に架空の会社を設立し、その会社に金銭を流用することが可能になります。有害な組み合わせのポリシーのもう一つの応用例は、システム管理者でない人がシステム管理者または高度な特権を持つことを防ぐことです。

ロールがある人が持つべきものを記述する方法であるなら、職務文章（SoD）ポリシーは、持ってはならないものを記述する方法です。このようなポリシーは一般的にプロビジョニングイベントがトリガーされたときに評価され、新しい有害な組み合わせがターゲットシステムに導入されないようにし、既存の組み合わせは検出され、是正されます。

@row
#### Workflow Approvals

Workflow approvals are an essential component of the policy management toolbox. Organizations with a mature provisioning deployment may only auto-provision 70-80% of access using birthright rules, roles, or SoD. So how does the remaining 20-30% of access get provisioned? The answer is self-service access request and approval workflows.

Workflow approvals are used when a human needs to make a policy decision. If a rule or role is not available, the provisioning system invokes a workflow process that routes an access request to a designee for approval. For example, an employee may make a self-service access request that is routed to a line manager for approval. The workflow approval process applies a layer of control and documents the access policy decision.

@column
#### ワークフロー承認

ワークフロー承認は、ポリシー管理ツールボックスの重要な要素です。成熟したプロビジョニングデプロイメントを持つ組織は、生得権ポリシールール、ロールまたはSoDを用いて、アクセス権の70-80%のみ自動プロビジョニングするでしょう。では、残りの20-30%のアクセス権はどのようにプロビジョニングされるのでしょうか？答えは、セルフサービスのアクセス権リクエストと承認ワークフローです。

ワークフロー承認は、人間がポリシー決定をおこなう必要がある時に利用されます。ルールまたはロールが利用できない場合、プロビジョニングシステムはワークフロープロセスを呼び出し、承認のためにアクセス権要求を被指名人にルーティングします。例えば、従業員がセルフサービスアクセス権要求を作成し、承認のためにラインマネージャにルーティングされる場合があります。ワークフロー承認プロセスは制御レイヤーに適用され、アクセスポリシー決定を文書化します。

@row
### User Account Provisioning

Once a provisioning event has been triggered and policy evaluated to determine what user account attributes, entitlements, and privileges need to be set or changed, then that information needs to make its way into the target system to affect the change to the user account stored locally there. How the necessary changes are made in the target system is the act of provisioning. Provisioning can be accomplished in two primary ways:

*   Automated
    
*   Manual
    

@column
### ユーザーアカウントプロビジョニング

プロビジョニングイベントが呼び出され、設定または変更する必要があるユーザアカウント属性、エンタイトルメントおよび特権を決定するためにポリシーが評価されたら、その情報をターゲットシステムに送信してそのシステムでローカルに保存されているユーザアカウントの変更に影響を与える必要があります。ターゲットシステム内で必要な変更をおこなう方法は、プロビジョニングのアクションです。プロビジョニングは主に2つの方法で実行できます：

*   自動
    
*   手動
    

@row
#### Automated

Automated user account provisioning is the process of creating and maintaining a user account in the target system using automated processing. To automate the user account provisioning process, the target system must provide a user management API or other means for the user-provisioning solution to systematically create, manage, and deactivate/delete user accounts.

Automated user account provisioning in target systems is the ultimate goal of user-provisioning technologies, but it is not without challenges. Each target system is an island. The user-provisioning system must maintain connections to the various target systems, which can be a heavy lift.

@column
#### 自動

自動ユーザアカウントプロビジョニングは、自動化されたプロセスを利用してターゲットシステムのユーザアカウントの作成とメンテナンスをおこなうプロセスです。ユーザアカウントプロビジョニングプロセスを自動化するために、ターゲットシステムはユーザー管理APIまたはシステム的にユーザーアカウントを作成、管理および無効化/削除するユーザープロビジョニングソリューションのための手段を提供しなくてはなりません。

ターゲットシステムでの自動ユーザーアカウントプロビジョニングは、ユーザープロビジョニング技術の究極的な目標ですが、課題がないわけではありません。各ターゲットシステムは島のようなものです。ユーザープロビジョニングシステムは、さまざまなターゲットシステムへの接続を維持する必要があり、これは大変な作業になる可能性があります。

@row
#### Manual

Manual provisioning requires human intervention to affect the change to the user account in the target system. This intervention often takes the form of the details of a user-provisioning event being sent to a team or a person who takes that information and manually keys it into the target system, using the target system’s unique user management interfaces. The information required could be sent via email or work ticket.

Manual provisioning introduces humans into a critical step of user provisioning, creating two specific risks. First, the person who manually works with the target system to create and change user accounts, by definition of the work she does, is a highly privileged user. It is a good practice to minimize the distribution of such privileges, but sometimes it is necessary. The second risk, manual provisioning, introduces is the possibility of human error. The person might misread or mistype an attribute, entitlement, or privilege, thus incorrectly setting the user account in the target system. While that might result in a minor annoyance, such as misspelling a user’s name, it might also lead to the assignment of incorrect privileges or even a toxic combination of entitlements.

It is fair to ask why manual provisioning is needed or wanted, given such risks. Manual provisioning is needed because not all target systems have APIs to which automatic provisioning connectors can connect. That homegrown general ledger system running on an extremely old operating system is an example of such. Another example is situations in which the target system is actually managed by a managed service provider and the identity team does not have direct access to that service provider. In that case, the change to a user account needs to be sent to the managed service provider via an email or ticket to trigger them to make the necessary change.

Manual provisioning is wanted because automation isn’t worth the effort. Consider an application with very few users, entitlements, or changes required, or all three. An identity team may decide that it is not worth deploying (or possibly building) an automatic provisioning connector but instead choose to accept the human cost and risk of manual provisioning. It is a best practice to apply automated provisioning to high volume (lots of users), high velocity (frequent changes to user accounts), and high value (mission-critical, financial material, etc.) systems. Conversely, it is not a best practice to automate every single system in the enterprise because, eventually, the costs to maintain connectors are simply not worth it.

@column
#### 手動

手動プロビジョニングでは、ターゲットシステムのユーザーアカウントを変更するためには人間の介在が必要です。しばしば、この介在はターゲットシステムの独自のユーザー管理インターフェイスを使用して、情報を取得し、手動でターゲットシステムに入力するチームまたは個人に送信されるユーザープロビジョニングイベントの詳細という形を取ります。必要な情報は、電子メールまたは作業チケットで送信できます。

手動プロビジョニングでは、ユーザープロビジョニングの重要なステップに人間が入り込み、2つの特定のリスクが生じます。１つ目に、ターゲットシステムを手動で操作してユーザーアカウントを作成および変更する人は、その作業の定義上、高度な特権を持つユーザーです。このような特権の付与を最小限に抑えることは良い方法ですが、必要な場合もあります。手動プロビジョニングによってもたらされる2つ目のリスクは、人的エラーの可能性です。属性、エンタイトルメントまたは特権を読み間違えたり、タイプミスしたりして、ターゲットシステムでユーザーアカウントを誤って設定する可能性があります。これにより、ユーザー名のスペルミスなどの小さな問題が発生する可能性がありますが、誤った権限が割り当てられたり、エンタイトルメントの有毒な組み合わせが発生したりする可能性もあります。

このようなリスクを考えると、なぜ手動プロビジョニングが必要なのか、もしくは求められるのかを尋ねるのは当然です。すべてのターゲットシステムに、自動プロビジョニングコネクタが接続できるAPIがあるわけではないため、手動プロビジョニングが必要です。非常に古いオペレーティングシステムで実行されている自社開発の総勘定元帳システムは、その一例です。もう1つの例は、ターゲットシステムがマネージドサービスプロバイダーによって実際に管理されており、アイデンティティチームがそのサービスプロバイダーに直接アクセスできない状況です。その場合、ユーザーアカウントの変更をマネージドサービスプロバイダーにメールまたはチケットで送信して、必要な変更を行うようにトリガーする必要があります。

自動化は労力に見合わないため、手動プロビジョニングが望まれます。非常に少数のユーザ、エンタイトルメントまたは変更が必須、あるいはその3つすべてを持つアプリケーションを考えてみてください。アイデンティティチームは、自動プロビジョニングコネクタをデプロイ（または構築）する価値がないと判断し、代わりに手動プロビジョニングの人的コストとリスクを受け入れることを選択する場合があります。自動プロビジョニングは、大規模（多数のユーザー）、高速（ユーザーアカウントの頻繁な変更）、高価（ミッションクリティカル、財務資料など）なシステムに適用するのがベストプラクティスです。逆に、企業内のすべてのシステムを自動化することはベストプラクティスではありません。なぜなら、最終的にはコネクタを維持するためのコストが単に割に合わなくなるだけだからです。

@row
## The Role of Standards

The identity industry recognized that the proliferation of proprietary user management APIs would lead to a lack of automated provisioning and make it difficult for organizations to mitigate the risks inherent in manual user provisioning. Starting with [Directory Service Markup Language](https://en.wikipedia.org/wiki/Directory_Services_Markup_Language) in 1999, followed by [Service Provisioning Markup Language](https://en.wikipedia.org/wiki/Service_Provisioning_Markup_Language) [^5] (SPML) in 2003, and finally followed by [System for Cross-domain Identity Management](https://en.wikipedia.org/wiki/System_for_Cross-domain_Identity_Management) [^6] (SCIM) in 2011, the industry has produced standards. The latest version of SCIM, version 2, has had significant uptake and, as of the second half of 2021, signs that the standards community is interested in making further enhancements. The fact that there have been at least three different standards with multiple versions is a testament to both the challenge of building a viable standard and the changes in the application development world.

For a user provisioning standard to be considered successful, it requires adoption from both user-provisioning system providers and application vendors. This “it takes two” challenge had thwarted mass adoption, especially in the era of on-premise software. The era of cloud computing and SaaS has seen a marked increase in the number of service providers willing to use SCIM v2 as well as user-provisioning technology providers. If the reader’s IT organization is building custom applications, it is worth investigating the implementation of SCIM v2 in those apps to facilitate automated user provisioning, especially in high-volume, high-velocity, and high-value applications.

@column
## 標準仕様の役割

アイデンティティ業界は、独自のユーザー管理APIの普及が自動プロビジョニングの欠如につながり、組織が手動ユーザープロビジョニングに固有のリスクを軽減することが困難になることを認識していました。1999年の[Directory Service Markup Language](https://en.wikipedia.org/wiki/Directory_Services_Markup_Language)に始まり、2003年の[Service Provisioning Markup Language](https://en.wikipedia.org/wiki/Service_Provisioning_Markup_Language) [^5] （SPML）、そして2011年の[System for Cross-domain Identity Management](https://en.wikipedia.org/wiki/System_for_Cross-domain_Identity_Management) [^6] （SCIM）と業界は標準規格を策定してきました。SCIMの最新版であるバージョン2には大きな反響があり、2021年後半の時点では、標準化コミュニティがさらなる機能強化に関心を持つ兆しがあります。少なくとも3種類の規格があり、複数のバージョンが存在するという事実は、実行可能な規格を構築することの難しさとアプリケーション開発の世界の変化の両方を証明しています。

ユーザープロビジョニング標準仕様が成功したと見なされるには、ユーザープロビジョニングシステムプロバイダとアプリケーションベンダの両方から採用される必要があります。この「二人がかり」という課題が、特にオンプレミス型ソフトウェアの時代には、大量採用を阻んでいました。クラウドコンピューティングとSaaSの時代には、ユーザープロビジョニング技術プロバイダと同様に、SCIM v2の利用に前向きなサービスプロバイダの数が著しく増加しました。読者のIT組織がカスタムアプリケーションを構築している場合、特に大規模、高速、高価値のアプリケーションにおいて、自動ユーザープロビジョニングを促進するために、それらのアプリケーションへのSCIM v2の実装を調査する価値があります。

@row
## Why is User Provisioning Challenging?

User-provisioning systems have been on the market for 20+ years. In that time, they have garnered a reputation for being difficult and expensive to deploy, and many organizations have found it challenging to realize a return on investment. Why?

User provisioning is similar to data integration technologies in many ways. Like data integration technologies, user-provisioning systems aggregate and synchronize data to many different systems and services in the environment. Each new connection adds a new level of complexity. The process of onboarding a single application to a provisioning environment requires an understanding of the application’s user management APIs and authorization construct, deployment of a connector, configuration of access policies, and implementation of policies and procedures for managing users (e.g., rules against creating or managing users directly within the application). Adding one application can be complex; consider the complexity when you have hundreds or even thousands of applications in your environment.

Another aspect that can be difficult is data quality issues in the SOR. Ideally, there is one authoritative SOR, but this is not always the case. Data collisions may happen when information is coming from multiple authoritative sources. Also, the administrators and users of the SOR may not understand the downstream effects of insufficient and poor-quality data. For example, they may not populate certain fields, enter inaccurate data, or delay event triggers. This all has implications for the provisioning system’s ability to accurately update identity records and access entitlements. Managing the data quality process can be taxing on identity practitioners.

Another common challenge is policy definition. Identity practitioners are responsible for configuring access policies (rules/roles), but they don’t own access decisions. The line of business in partnership with audit, legal, governance, risk management and compliance (GRC), etc., own access decisions. The effort to collect this data for provisioning policy and role definition is a significant undertaking.

Last but not least, maintaining the entitlement catalog can be a difficult task. A single organization may have hundreds of thousands, if not millions, of entitlements. The effort to collect entitlements and metadata should not be underestimated.

While the advantages of automated user account provisioning are well understood, deployments can be challenging. Identity practitioners should obtain executive support and set proper expectations, build a structured process for onboarding applications (e.g., dedicated resources, intake forms/surveys, automation, etc.), and set clear key performance indicators that show continued progress.

@column
## なぜユーザープロビジョニングは困難なのか？

ユーザープロビジョニングシステムが市場に出てから20年以上が経ちました。この間、ユーザープロビジョニングシステムは導入が難しく高価であるという評判を集め、多くの組織が投資に対するリターンを実現することが困難であると感じてきました。なぜでしょうか？

ユーザープロビジョニングは、多くの点でデータ統合テクノロジに似ています。データ統合テクノロジと同様に、ユーザープロビジョニングシステムは環境内のさまざまなシステムやサービスにデータを集約して同期します。新しい接続ごとに、新しいレベルの複雑さが追加されます。単一のアプリケーションをプロビジョニング環境にオンボーディングするプロセスでは、アプリケーションのユーザー管理APIと認可構成、コネクタのデプロイメント、アクセスポリシーの構成およびユーザーを管理するためのポリシーと手順の実装（例えば、アプリケーション内で直接ユーザーを作成または管理することを禁止するルール）を理解する必要があります。1つのアプリケーションの追加が複雑になる場合があります；環境内に数百または数千のアプリケーションがある場合は、その複雑さを考慮してください。

困難なもう1つの側面は、SORのデータ品質の問題です。理想的には、1つの権威のあるSORが存在して欲しいですが、常にそうであるとは限りません。情報が複数の権威あるソースから送られてきた場合、データの衝突が発生することがあります。また、SORの管理者とユーザーは、不十分で質の低いデータが下流に与える影響を理解していない可能性があります。たとえば、特定のフィールドに値を入力しなかったり、不正確なデータを入力したり、イベントトリガーを遅延させたりすることがあります。これはすべて、アイデンティティ・レコードとアクセス権を正確に更新するプロビジョニングシステムの機能に影響します。データ品質プロセスの管理は、アイデンティティ担当者に負担をかける可能性があります。

もう1つの共通の課題は、ポリシー定義です。アイデンティティ担当者は、アクセスポリシー（ルール/ロール）を構成する責任がありますが、アクセス権決定権を所有していません。監査、法務、ガバナンス、リスク管理、コンプライアンス（GRC）などと連携した基幹業務は、独自のアクセス権決定をおこないます。プロビジョニングポリシーとロールの定義のため、この情報を収集する作業は、重要な作業です。

最後になりますが、エンタイトルメントカタログの保守は困難な作業です。1つの組織に、数百万ではないにしても数十万のエンタイトルメントがある場合があります。資格とメタデータを収集する作業を過小評価しないでください。

自動化されたユーザアカウントプロビジョニングの利点はよく理解されていますが、そのデプロイは困難な場合があります。アイデンティティ担当者は、経営陣の支持を得て適切な期待値を設定し、アプリケーションのオンボーディングのための構造化されたプロセス（専用のリソース、インテークフォーム/調査、自動化など）を構築し、継続的な進歩を示す明確な主要業績評価指標を設定する必要があります。

@row
## The Next Generation, Hybrid-Approach to Provisioning

While user-provisioning technologies have been around for quite some time, user-provisioning technologies were developed at a time when the IT environment was much more contained. Target systems and systems of record were located on-premises, and users were primarily employees accessing resources onsite.

Cloud, mobile, work from home, and various other initiatives have changed the dynamics of user provisioning. Now authoritative and target systems are hosted in the cloud (and on-premises), and external users are accessing internal resources.

In traditional security models, provisioning is an admin-time function (users are pre-provisioned into systems by an administrator). Contrast this with authentication and authorization technologies that are run-time functions that occur at the point the user is logging into the system. Security technologies like SIEM, DLP, and threat detection kick in once the user is in session.

Modern security models that include remote access, cloud computing, and zero-trust security principles require a new approach to user provisioning: a just-in-time (JIT), least privilege approach. This modern approach to provisioning means that rather than pre-provisioning users at admin-time, users are provisioned at run-time and they are given the minimal privileges necessary to complete a task. Consequently, organizations are deploying a hybrid approach to provisioning that includes a mix of traditional API-based, SAML/OIDC-based, and SCIM-based connectors.

A hybrid provisioning architecture allows organizations to pre-provision to a set of applications (typically on-premises) but use OIDC, SAML, and SCIM-based connectors to enable JIT provisioning (primarily used in cloud and SaaS product use cases).

@column
## プロビジョニングへの次世代ハイブリッドアプローチ

ユーザープロビジョニング技術はかなり以前から存在していたが、ユーザープロビジョニング技術が開発されたのはIT環境がより抑制されていた時代でした。対象システムや記録システムはオンプレミスにあり、ユーザーは主に従業員がオンサイトでリソースにアクセスするものでした。

クラウド、モバイル、在宅勤務、その他さまざまな取り組みにより、ユーザープロビジョニングの状況は変化しています。現在、権威あるシステムやターゲットシステムはクラウド（およびオンプレミス）にホストされており、外部ユーザーが社内のリソースにアクセスしています。

従来のセキュリティモデルでは、プロビジョニングは管理者側の機能でした（ユーザーは管理者によりシステムに事前にプロビジョニングされます）。これに対して、認証と認可の技術は、ユーザーがシステムにログインする時点で発生するランタイム機能です。SIEM、DLP、脅威検知などのセキュリティ技術はユーザーがセッションに参加した時点で起動します。

リモートアクセス、クラウドコンピューティング、ゼロトラストのセキュリティ原則を含む最新のセキュリティモデルは、ユーザープロビジョニングに対する新しいアプローチ、すなわちジャストインタイム（JIT）、最小権限アプローチを必要とします。この最新のプロビジョニングアプローチは、管理者時にユーザーを事前にプロビジョニングするのではなく、実行時にユーザーをプロビジョニングし、タスクを完了するために必要な最小限の特権を与えることを意味します。その結果、組織は従来のAPIベース、SAML/OIDCベース、およびSCIMベースのコネクタを組み合わせたハイブリッドなプロビジョニングアプローチを導入しています。

ハイブリッドプロビジョニングアーキテクチャでは、企業は一連のアプリケーション（通常はオンプレミス）に事前プロビジョニングをおこないますが、OIDC、SAMLおよびSCIMベースのコネクタを使用してJITプロビジョニングを可能にします（主にクラウドおよびSaaS製品の使用例で使用されます）。

@row
## Author Bios

Ian Glazer

<!-- ![](/assets/images/idpro_bok/iglazer.jpg) -->

Ian Glazer is the founder and president of Weave Identity – an advisory services firm. Prior to founding Weave, Ian was the Senior Vice President for Identity Product Management at Salesforce. His responsibilities include leading the product management team, product strategy, and identity standards work. Earlier in his career, Ian was a research vice president and agenda manager on the Identity and Privacy Strategies team at Gartner, where he oversaw the entire team’s research. He is a Board Emeritus and the co-founder of IDPro and works to deliver more services and value to the IDPro membership, raise funds for the organization, and help identity management professionals learn from one another. During his career in the identity industry, he has co-authored a patent on federated user provisioning, co-authored and contributed to user provisioning specifications, and is a noted blogger, speaker, and photographer of his socks.

Lori Robinson

<!-- ![](/assets/images/idpro_bok/lrobinson.jpg) -->

Lori Robinson is the Vice President of Enterprise Identity Product Management at Salesforce where leads a team responsible for Salesforce’s enterprise identity management program. Before joining Salesforce she was the VP Product and Market Strategy at SailPoint. She also served as the Managing Vice President and Analyst at Gartner where she covered the identity governance and administration, privileged access management, and consumer IAM markets. Lori is a recognized industry thought leader, speaker, and publisher. She is passionate about advancing opportunities for women in IT and has led various user groups, round tables, and events for women in identity.

Mat Hamlin  
  
<!-- ![](/assets/images/idpro_bok/mhamlin.png) -->

Mat Hamlin is the Vice President of Product Management for Platform Identity at Salesforce. His responsibilities include leading the product management team, product strategy, and innovation for the Identity Services on the Salesforce core platform. Prior to Salesforce, he served in multiple product management roles at SailPoint, Oracle, and Sun Microsystems, focusing on User Provisioning, Access Governance, and Enterprise Role Management.

@row
## Endnotes

- - -

[^1]:  More on Joiner, Mover, and Leaver is available in Cameron, A. & Grewe, O. (2022) “An Overview of the Digital Identity Lifecycle (v2)”, _IDPro Body of Knowledge_ 1(7). doi: [https://doi.org/10.55621/idpro.31](https://doi.org/10.55621/idpro.31) 
    
[^2]:  Changes to name or place of residence can be just as impactful as a change in job role or reporting structure. 
    
[^3]:  More on roles is available in McKee, M. K., (2021) “Policy-Based Access Controls”, _IDPro Body of Knowledge_ 1(4). doi: [https://doi.org/10.55621/idpro.61](https://doi.org/10.55621/idpro.61) and Koot, A., (2020) “Introduction to Access Control (v3)”, _IDPro Body of Knowledge_ 1(6). doi: [https://doi.org/10.55621/idpro.42](https://doi.org/10.55621/idpro.42) . 
    
[^4]:  Corporate Finance Institute, “Top Accounting Scandals: A recap of the top scandals in the past,” n.d., [https://corporatefinanceinstitute.com/resources/knowledge/other/top-accounting-scandals/](https://corporatefinanceinstitute.com/resources/knowledge/other/top-accounting-scandals/) (accessed 17 May 2022). 
    
[^5]:  For the sake of transparency, one of the authors of this article contributed to the SPML v2 standard and apologizes for the mistakes he didn’t know he was making at the time. 
    
[^6]:  For the sake of transparency, one of the authors of this article contributed to the SCIM v2 standard and is proud of that work. 
