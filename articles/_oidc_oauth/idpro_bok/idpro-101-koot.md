---
layout: columns
title: Introduction to Privileged Access Management
permalink: /docs/oidc_oauth/idpro_bok/101
date: 2024-09-09
modify_date: 2025-01-13
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "PAM", "特権アクセス管理", "非人間アカウント"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/101/](https://bok.idpro.org/article/id/101/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

Privileged Access Management (PAM) plays a crucial role in modern cybersecurity. Organizations can significantly enhance their security posture and protect valuable assets by addressing the issues and risks associated with privileged accounts. Implementing a combination of robust policies, technologies, and best practices will help organizations manage the risks effectively while ensuring the availability, integrity, and confidentiality of their systems and data.

This article introduces the concepts of managing privileged access and will touch on non-human accounts, including those that are both interactive and non-interactive. It will show that not all privileged access accounts should be treated in the same way. It will explore the scenarios in which PAM solutions can help organizations gain control of privileged access. Different use cases for PAM solutions are explained and illustrated with architecture diagrams.

Critically, even when implementing PAM systems, practitioners cannot neglect the human factor (which requires policy, training, and controls). This article concludes with best practices for implementation, adoption considerations, and core guiding principles.

Keywords: PAM, Privileged Access Managament, Non-human accounts

@column
## 概要

特権アクセス管理（PAM）は現代のサイバーセキュリティにおいて中心的な役割を果たします。特権アカウントに関連する問題やリスクに対処することで、組織はセキュリティ体制を非常に強化し、価値ある資産を守ります。強力なポリシー、テクノロジーとベストプラクティスの組み合わせを実装することで、組織が、システムやデータの可用性、完全性と機密性を確保しながらリスクを効果的に管理する助けとなります。

この記事では、特権アクセス管理の概念について紹介し、対話型と非対話型の両方の非人間アカウントについても触れます。すべての特権アクセスアカウントが同じように亜塚wれるべきでなはないことを示します。PAMソリューションが、組織の特権アカウントの制御に役立つシナリオについて探ります。PAMソリューションの異なるユースケースについて説明し、アーキテクチャ図を描きます。

重要なこととして、PAMシステムを実装したときでさえ、専門家は人的要因（ポリシー、トレーニング、管理を必須とする）を無視することはできません。本稿は、導入のためのベストプラクティス、採用に関する考慮事項および核となる指針で締めくくります。

**Keywords:** PAM, 特権アクセス管理, 非人間アカウント

@row
© 2024 IDPro, André Koot (SonicBee)

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction to Privileged Access

Privileged Access Management (PAM) plays a crucial role in modern cybersecurity. All organizations (at least those with technical infrastructure) maintain accounts with some form of super-user permissions, e.g., the Administrator account on a laptop. Organizations enhance their security posture and protect valuable assets from inside and outside threats by addressing the issues and risks associated with privileged accounts. This requires a combination of robust policies, technologies, and best practices that help organizations manage the risks while ensuring the confidentiality, integrity, and availability (the “CIA Triad”) of systems and data.

@column
## 特権アクセスへの導入

特権アクセス管理（PAM）は現代のサイバーセキュリティにおいて重要な役割を果たします。全ての組織（少なくとも技術インフラストラクチャを有している）は、ノートパソコンの管理者権限のように何らかのスーパーユーザー権限を持つアカウントを管理しています。特権アカウントに関連する問題やリスクに対処することで、組織はセキュリティ体制を非常に強化し、価値ある資産を守ります。これには強力なポリシー、テクノロジーとベストプラクティスの組み合わせを実装することが必須であり、これらは、組織がシステムやデータの可用性、完全性と機密性（「CIAトライアド」）を確保しながらリスクを効果的に管理する助けとなります。

@row
## Terminology

|     |     |
| --- | --- |
| Access | The permissions, privileges, and abilities granted to users, account types, system processes, applications, or any other entities within a computing environment. |
| Privileged Access | Users or accounts with high-risk permissions, such as those that grant them access to (critical) systems, sensitive data, and configuration settings |
| Privileged Access Management | A mechanism for managing temporary access for accounts with high-risk permissions. PAM often involves check-out and check-in of a credential generated for a single use. [^1] |
| Privileged Account Management | Focuses on special control for risky high-level access. Privileged Account Management (PAM) is a mechanism for getting those special accounts under control. [^2] |
| Role Based Access Control (RBAC) | The use of roles at runtime: a way to govern who gets access to what through the use of business roles and application roles |
| Joiner/Mover/Leaver | The joiner/mover/leaver lifecycle of an employee identity considers three stages in the life cycle: joining the organization, moving within the organization, and leaving the organization. |
| Least Privilege | The principle that a security architecture should be designed so that each entity is granted the minimum system resources and authorizations that the entity needs to perform its function. [^3] |
| Identity Governance and Administration | A discipline that focuses on identity life cycle management and access control from an administrative perspective. [^4] |

@column
## 用語解説

|     |     |
| --- | --- |
| アクセス | ユーザー、アカウント種別、システムプロセス、アプリケーションまたはコンピューティング環境のその他エンティティに与えられた許可、特権および能力。 |
| 特権アクセス | （重要な）システム、機密データと構成設定にアクセスを許可するような、高リスク権限を持つユーザーまたはアカウント |
| 特権アクセス管理 | 高リスク権限を持つアカウントに対する一時的なアクセス管理するメカニズム。しばしば、PAMは、1回の利用のために作成したクレデンシャルのチェックアウトおよびチェックインを伴います。 [^1] |
| 特権アカウント管理 | リスクの高い強いアクセス権への特別な制御に焦点を当てています。特権アクセス管理（PAM）は、このような特別なアカウントを管理下に置くためのメカニズムです。 [^2] |
| ロールベースアクセス制御（RBAC） | ランタイムでのロールの利用：誰が何へのアクセス権を取得しているのかを、業務のロールおよびアプリケーションロールの利用によって管理する方法 |
| Joiner/Mover/Leaver | 従業員アイデンティティのjoiner/mover/leaverライフサイクルはライフサイクルにおいて3つのステージを考慮します：組織への加入、組織内での異動、組織からの離脱。 |
| 最小特権 | セキュリティアーキテクチャは、各エンティティは、そのエンティティが機能の実行に必要な最小のシステムリソースへのアクセスと認可を付与されるように設計されるべきという原則。 [^3] |
| アイデンティティガバナンスと管理 | アイデンティティライフサイクル管理および管理観点からのアクセス制御に焦点をおいた分野。 [^4] |

@row
### Acronyms in Use

|     |     |
| --- | --- |
| CIA: Confidentiality, Integrity, and Availability | The “triad” that forms the basis of information security. |
| RPA: Robotic Process Automation | Autonomous IT solution to automate manual tasks. This autonomy is in contrast to a user-initiated macro. |
| ICS: Industrial Control Systems | Implemented to separate IT environments from Operational Technology environments (e.g., in industrial process industries) |
| SCADA: Supervisory Control and Data Acquisition | An architecture framework to secure ICS environments |

@column
### 使われている略称

|     |     |
| --- | --- |
| CIA: Confidentiality, Integrity, and Availability（機密性、完全性および可用性） | 情報セキュリティの基礎を構成する「トライアド」。 |
| RPA: Robotic Process Automation（ロボティック・プロセス・オートメーション） | 手作業を自動化するための自律的なITソリューション。この自律性はユーザー主導のマクロとは対照的です。 |
| ICS: Industrial Control Systems（産業用制御システム） | IT環境と運用技術環境を分離するために導入されます（例 工業プロセス産業） |
| SCADA: Supervisory Control and Data Acquisition（監視制御とデータ取得） | ICS環境をほぼするためのアーキテクチャフレームワーク |

@row
### Privileged Accounts

Privileged accounts, often called ‘super-user’ or ‘administrator’ accounts, possess elevated permissions granting access to (critical) systems, sensitive data, and configuration settings. With this level of access, these accounts define the behavior of the component they belong to. ‘Administrator’ is the built-in account needed to configure a Windows component, such as the directory, the filesystem, and the networking capabilities. Similarly, ‘root’ is the super-user account on UNIX and Linux systems and many infrastructure components. In database management systems, there are ‘SA’ (system admin), ‘DBO/DBA’ (database owner/admin), ‘root,’ or ‘postgres.’ These accounts function on behalf of a component itself (rather than a user). Anyone who knows the password can log in and effectively _**be**_ the component: they can change the component's behavior and thus make or break the system. These super accounts are almighty.

Managing access to privileged accounts should be one of the most common early initiatives in an organization’s identity & access management (IAM) journey. Why? The simple answer is that the organization should manage access where risk is highest. For more detail, look no further than the #1 item in the 2021 OWASP top 10 list of Web Application Security Risks: Broken Access Control ( [OWASP link](https://owasp.org/Top10/A01_2021-Broken_Access_Control/) ). [^5] Without effective privileged access management (PAM), all three legs of the information security CIA triad can be compromised, sometimes with catastrophic results. This is why, although they vary by country, emerging regulatory frameworks specifically call for controls on privileged access. For example, here is one clause in which the European NIS2 Directive specifically refers to PAM as an essential part of ‘cyber hygiene:’

> _…Cyber hygiene policies comprising a common baseline set of practices, including software and hardware updates, password changes, the management of new installs, the limitation of administrator-level access accounts, and the backing-up of data, enable a proactive framework of preparedness and overall safety and security in the event of incidents or cyber threats_ [^6]

Regulation is not the only reason to start a PAM program. Even if an organization isn’t subject to these compliance controls, managing access to privileged accounts is in its best interests. Figure 1 demonstrates what can happen when unauthorized users gain access to admin accounts.

@column
### 特権アカウント

特権アカウント、しばしば「スーパーユーザー」や「管理者」と呼ばれるアカウント、は（重要な）システムや機密データ、構成設定へのアクセス権を付与できるより強い権限を有しています。このアクセスレベルによって、これらのアカウントは所属するコンポーネントの振る舞いを定義します。「管理者」はディレクトリやファイルシステム、ネットワーク機能などのWindowsコンポーネントを設定するために必要なビルドインのアカウントです。同様に、「root」はUNIXおよびLinuxシステムそして多くのインフラストラクチャにおけるスーパーユーザーアカウントです。データベース管理システムでは、「SA」（システム管理者）、「DBO/DBA」（データベース所有者/管理者）、「root」や「postgres」などが存在します。これらのアカウントはコンポーネント自体（ユーザーというよりも）に代わって機能します。パスワードを知っていれば誰でもログインすることができ、事実上コンポーネントに _**なる**_ ことができます：コンポーネントの振る舞いを変更することができ、システムを作成したり、破壊したりできます。これらのスーパーアカウントは全能です。

特権アカウントへのアクセスを管理することは、組織のアイデンティティとアクセス管理（IAM）ジャーニーにおける最も一般的な早期段階での取り組みの1つです。なぜでしょうか？シンプルな答えは、組織はリスクが最も高い場所へのアクセスを管理すべきだからです。より詳細にいえば、2021年のOWASPのWebuアプリケーションセキュリティリスクのトップ10のナンバー1の項目を参照してください：アクセス制御の不備（[OWASPのリンク](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)）。 [^5] 効果的な特権アクセス管理（PAM）がなければ、情報セキュリティCIAトライアドの3本柱全てが侵害され、時には壊滅的な結果になります。このため、国によって差異はありますが、新たな規制の枠組みでは特権アクセスの制御が特に求められています。例えば、欧州のNIS2指令の一節では、PAMを「サイバーハイジーン」の不可欠な部分として特に言及しています：

> _…ソフトウェアおよびハードウェアの更新、パスワード変更、新規インストールの管理、管理者レベルのアカウントアクセスの制限およびデータのバックアップを含む基本的な慣習から構成されるサイバーハイジーンポリシーは、インシデントやサイバー脅威が発生したときの備えと全般的な安全性とセキュリティのプロアクティブな枠組みを可能にします_ [^6]

規制だけがPAM計画を開始する理由ではありません。組織がこれらのコンプライアンス規制の対象ではない場合でも、特権アカウントへのアクセスを管理することは最善の利益です。Figure 1では、認可されていないユーザーが管理者アカウントへのアクセス権を得たときに何が起きうるのかを示してます。

@row
![Screen shots of two twitter posts, nominally from Joe Biden and Barack Obama but posted as a result of hacked Twitter admin accounts.](/assets/images/idpro_bok/PAM-image1.png)

Figure 1: In 2020, the admin accounts of Twitter Operations Management software were leaked to a Slack channel and accessed by an unauthorized person, leading to fraudulent activity. [^7]

@row
### Threats of Privileged Access

As demonstrated by the example in Figure 1, organizations that do not constrain the proliferation of – and access to - privileged accounts face several issues. Those issues include:

*   **Over-Privilege** : Employees with privileged access might be granted excessive permissions beyond their role requirements, thus increasing the risk of unauthorized actions and data breaches. For example, a support technician who gains full root access when they have a limited or occasional need to restart a single service.
    
*   **Credential Sharing** : When multiple individuals share privileged credentials, organizations may struggle to track who accessed what resources, increasing the chance of a security breach. This creates a lack of accountability. For example, a support team may all know root credentials – a situation exacerbated by employee turnover if those credentials are not changed.
    
*   **Credential Theft** : Cybercriminals often target privileged accounts due to the extensive access they provide. Malicious actors can gain unauthorized access to critical systems and data if these credentials are compromised.
    
*   **Insider Threats** : Trusted employees can become insider threats if their privileged access is misused intentionally or unintentionally.
    

@column
### 特権アクセスの脅威

Figure 1の例で示したように、特権アカウントの増加とアクセスを制限しなかった組織はいくつかの問題に直面します。以下のような問題です：

*   **過剰な特権**：特権アクセス権を持つ従業員は自身のロールの必要性を超えた権限を与えられる可能性があり、認可されていないアクションやデータ漏洩のリスクが高まります。例としては、サポート技術者が1つのサービスを再起動する必要が限定的または時折発生するようなときに、すべてのルートアクセス権を付与するケースです。
    
*   **クレデンシャル共有**：複数の個人が特権クレデンシャルを共有するとき、組織はどのリソースに誰がアクセスしているかを追跡するのに苦労するかもしれず、セキュリティ侵害の機会が高くなります。これは説明責任の欠落になります。例えば、サポートチームは全員がルートクレデンシャルを知っている可能性がありますが、これらのクレデンシャルが変更されない場合、従業員の入れ替わりによって状況が悪化します。
    
*   **クレデンシャル窃取**：サイバー犯罪者は、特権アカウントが提供する幅広いアクセス権を理由に、特権アカウントをターゲットにすることが多いです。これらのクレデンシャルが侵害された場合、悪意のあるアクターは重要なシステムやデータにへの認可されていないアクセスを取得することができます。
    
*   **内部脅威**：信頼されている従業員の特権アクセスが意図的であれ、偶発的であれ正しく利用されなかった場合、彼らは内部脅威になり得ます。
    

@row
## A Typology of Privileged Access Accounts

Understanding the different types and characteristics of privileged accounts is essential to management and risk mitigation.

@column
## 特権アクセスアカウントの類型

特権アカウントの異なる酒類と特徴を理解することは、管理とリスク軽減に不可欠です。

@row
### Human Privileged Accounts

Generally, human-privileged accounts are governed by the human resource practices in an organization. The CEO, for example, often has more privileges in systems than interns. Because the CEO’s user accounts have more power – and because the CEO is often easily identifiable – their privileged accounts are at a greater risk of attack. Fortunately, executives seldom have root access to Linux servers and are rarely assigned as admins to Windows Server management. However, their access and associated risks should be managed thoughtfully. Role-Based and Policy-Based Access Control can help control the amount of access that such users have.

Another type of access would be individual/nominative accounts – those with root access, global admin rights, or other highly privileged group membership. Managers should consider these accounts high-risk. The usage of these authorizations may not be anonymous, but they should never be assigned for an indefinite amount of time. Just-in-Time (JIT) provisioning or dynamic access controls offer further controls to prevent long-standing high-risk authorizations.

Privileged access may also refer to operations involving sensitive data, e.g., the amount or type of personally identifiable information (PII) or company financial data that an individual user has access to. In some scenarios, privileged access may extend to _which_ customers’ data. For instance, a healthcare organization treating a ‘VIP’ may consider their data more sensitive. While policy and regulation treat them as equal, the collateral damage in the event of a data breach may be more significant, and, therefore, an organization may put more access controls in place.

The key risks applicable to human accounts are two-fold:

1.  Legitimate users (employees, contractors, etc.) gain more access than they should and, thus, put the organization at greater risk of insider threat or data loss.
    
2.  Bad actors gain access to legitimate users’ accounts through one of many attack vectors, like password spray attacks, phishing campaigns, or consent hacking.
    

Of course, these risks often work hand-in-hand since bad actors that gain access to the highly-privileged accounts of legitimate users can inflict greater damage.

Best practices for managing this type of account include:

*   **Role-Based and Policy-Based Access Control (RBAC)** : Authorizations are granted to personnel via business roles.
    
*   **Multi-factor authentication (MFA)** : Mandatory MFA dramatically de-risks account take-over.
    
*   **Least Privilege:** Accounts are provisioned with the minimum number of authorizations required to do the job.
    
*   **Just-in-Time Provisioning** : Accounts are authorized only as and when a task needs to be performed. Once a task is finished, the authorizations should be deprovisioned.
    
*   **Strong Governance** : Robust IGA procedures, like access request management and approval workflows, ensure that interventions like RBAC, Least Privilege, and MFA continue functioning.
    

These controls depend on solid governance and access management processes. For more information on Workforce Identity and Access Management (also called Identity Governance and Administration, or IGA) solutions that support Joiner-Mover-Leaver workflows and Role Based Access Control, _see An Overview of the Digital Identity Lifecycle._ [^8] These solutions can, however, not ideal for the management of non-human privileged accounts since the managing process is not a joiner-mover-leaver process.

@column
### 人間の特権アカウント

一般的に、人間の特権アカウントは組織の人的リソースの活動によって管理されます。例えば、多くの場合でCEOはインターン生よりもシステムにおける特権を有しています。CEOのユーザーアカウントはより強い権限を持っており、多くの場合CEOの特定は容易であることから、その特権アカウントは攻撃されるリスクがより高いです。幸運にも、経営陣はLinuxサーバーのルートアクセス権を持つことは滅多になく、Windowsサーバーの管理者権限の割り当てもほとんどありません。しかし、経営陣のアクセスと関連するリスクは思慮深く管理されるべきです。ロールベースおよびポリシーベースのアクセス制御はユーザーが有しているアクセス権の量を管理するために役立ちます。

別のアクセス権のタイプは、ルートアクセス、グローバル管理者権限またはほかの高い特権グループメンバーシップを持つ個人／名前が付けられたアカウントです。マネージャーはこのようなアカウントは高リスクと考えるべきです。これらの認可の使い方は匿名でなくてもよいですが、決して無期限に割り当てられるべきではありません。ジャストインタイム（JIT）プロビジョニングまたはダイナミックアクセス制御は多くの場合、長期の高いリスクの認可を防止するためのさらなる制御を提供します。

また、特権アクセスは機密データ、例えば個人識別情報（PII）や個人ユーザーがアクセスできる会社の財務データの量や種類にかかわる操作を指すことがあります。一部のシナリオにおいて、特権アクセスは _どの_ 顧客データにも広がる可能性があります。例えば、「VIP」を治療する医療機関はこれらのデータをより機密性の高いもの考えるかもしれません。ポリシーや規制は彼らを同等に扱いますが、データ漏洩が起きたときの巻き添え被害はさらに重大になるかもしれないため、組織はより多くのアクセス制御を導入するかもしれません。

人間のアカウントに適用される重要なリスクは2つあります：

1.  正規ユーザー（従業員、委託契約者など）が持つべきよりも大きいアクセス権を取得すると、組織において内部脅威またはデータ漏洩のリスクが大きくなります。
    
2.  悪意のあるアクターは、パスワードスプレー攻撃、フィッシングキャンペーンや動機ハッキングなど多くの攻撃ベクトルの一つとして、正規ユーザーのアカウントにアクセスします。
    

もちろん、正規ユーザーの強い特権アカウントへのアクセスした悪意のあるアクターはより大きなダメージを与えることができるため、これらのリスクは多くの場合に連動します。

この種のアカウントを管理するベストプラクティスには以下が含まれます：

*   **ロールベースおよびポリシーベースアクセス制御（RBAC）**：認可は業務上の役割を通じて社員に与えられます。
    
*   **多要素認証（MFA）**：MFAを必須とすることで、アカウント乗っ取りのリスクを劇的に軽減します。
    
*   **最小特権**：アカウントは、仕事に必要な最小の認可を有した状態でプロビジョニングされます。
    
*   **ジャストインタイム・プロビジョニング**：アカウントは、タスクが実行される必要があるときのみ、認可されます。タスクが完了すると認可はデプロビジョニングされるべきです。
    
*   **強力なガバナンス**：アクセス要求管理や承認ワークフローのような堅固なIGA手順は、RBAC、最小特権やMFAのような干渉が機能し続けることを保証します。
    

これらの制御は、強固なガバナンスとアクセス管理プロセスに依存しています。Joiner-Mover-Leaverワークフローおよびロールベースアクセス制御をサポートする従業員アイデンティティとアクセス管理（アイデンティティガバナンスと管理、IGAとも呼ばれる）ソリューションについての詳細は、 _An Overview of the Digital Identity Lifecycle_ [^8] を参照してください。しかし、これらのソリューションは非人間特権アカウントの管理には理想的ではありません。なぜならば、管理するプロセスがjoiner-mover-leaverプロセスではないためです。

@row
### Non-Human Privileged Accounts

Non-Human Accounts require different management processes and risk mitigation strategies because they are not human (as suggested by the name). These non-human accounts are not managed via a joiner-mover-leaver processes. Instead, events in their lifecycle - which resemble those of human accounts - are triggered by a change management process.

@column
### 非人間の特権アカウント

非人間アカウントは、（その名称からわかるとおり）人間ではないため、異なる管理プロセスとリスク軽減戦略を必要とします。これらの非人間アカウントはjoiner-mover-leaverプロセスを介した管理はされません。代わりに、管理プロセスの変化によって、人間アカウントと似たライフサイクルのイベントがトリガーされます。

@row
![A diagram of a digital identity lifecycle for non-human accounts. The boxes include Create then Provision then Authenticate then Manage / Maintain then Deprovision Access.](/assets/images/idpro_bok/PAM-image2.png)

Figure 2: Lifecycle of Non-Human Accounts

@row
Figure 2 articulates the following lifecycle for non-human accounts:

1.  **Create:** A non-human account is created as the result of a change request, either in a development process or brought in through a procurement process (rather than an HR process that triggers a human account). The account can belong to a server, a network component, or an RPA.
    
2.  **Provision:** The component is activated, gets an identity and an account, and is given the least privileged authorizations required to perform the configured tasks. A secret is configured to make it possible to identify and authenticate the component at runtime.
    
3.  **Authenticate:** Once activated, the component needs to be identified by a governing body (like the network) and authenticated, whether by a configured password, a certificate, or a token.
    
4.  **Manage/Maintain:** During the lifecycle, the component's functionality can change, and any changes to required authorizations will be managed through the change management process.
    
5.  **Deprovision Access:** When the component is decommissioned, access is removed to prevent abuse (practitioners often forget this step).
    

There are two forms of non-human privileged accounts: those that humans interact with and those they do not. While the main focus of this article is _interactive_ non-human accounts, it is crucial to consider the PAM implications of those that do not interact.

@column
Figure 2は次のような非人間アカウントのライフサイクルを示しています：

1.  **新規作成**：非人間アカウントは開発プロセスにおける変更要求の結果として作成されたり、調達プロセス（人間アカウントをトリガーするHRプロセスではなく）を通じて持ち込まれたりします。このアカウントは、サーバー、ネットワークコンポーネントまたはRPAに属することができます。
    
2.  **プロビジョニング**：コンポーネントがアクティブ化され、アイデンティティとアカウントを取得し、設定されたタスクの実行に必要な最小の特権認可が与えられること。ランタイムでコンポーネントの識別および認証を可能にするシークレットが設定されます。
    
3.  **認証**：アクティブ化されると、コンポーネントは管理組織（ネットワークのような）によって識別される必要があり、設定されたパスワード、証明書またはトークンのいずれかによって認証される必要があります。
    
4.  **管理／メンテナンス**：ライフサイクルを通じてコンポーネントの機能は変化する可能性があり、必要な認可が変化数rことは変更管理プロセスによって管理されるでしょう。
    
5.  **アクセスのデプロビジョニング**：コンポーネントが廃止されるとき、アクセス権は悪用を防ぐために削除されます（専門家はしばしばこのステップを忘れます）。
    

非人間特権アカウントには2酒類あります：人間と対話するものと対話しないものです。この記事の主な焦点は _対話型_ 非人間アカウントですが、非対話型でもPAMの意味を考えることは非常に重要です。

@row
#### Non-Human, Non-Interactive Privileged Accounts

Some privileged accounts are non-interactive, meaning that humans generally do not log into them to perform business activities. These are the accounts of components like middleware services, such as databases or web servers. These services access resources after a login with a secret kept in a config file using tokens or secrets. These accounts act as placeholders in the system log that register resource usage.

For example, in accounting software, an application may need to register transactions in a relational database. To do this registration, the application looks up the password of the configured service account and logs in to the database. This results in each transaction being logged against and owned by that application. The application must, of course, ensure that the account of every actor is registered as the initiator of their transactions.

Other examples include accounts used for automation, such as batch accounts, macros, or RPAs. The organization’s Technology team documents a change request with the process requirements for each automated task and then creates the appropriate script or configuration to execute the steps. The process itself needs to have the requisite authorization to run. Or, in other words, achieve the minimal required authorizations according to the ‘least privilege’ principle.

In these scenarios, the change requester or requirements owner should be considered the accountable party for the script, macro, or RPA.

Best practices for managing this type of account include:

*   **Change Management Governance:** These accounts don’t follow regular IGA processes like JML, and authorizations are not role-based but specific. Ensure an accountable party oversees the requirements and a robust process managing any change to the functionality and authorizations of the component.
    
*   **Least Privilege:** Accounts are provisioned with the minimum number of authorizations required to do the task.
    
*   **No Login:** Make sure that these accounts cannot be logged into in the underlying infrastructure, like the operating system.
    

To learn more about managing these types of privileged accounts, see _Non-human Account Management_ in the BoK. [^9]

@column
#### 非人間、非対話型特権アカウント

一部の特権アカウントは非対話型であり、これは一般的に業務活動をおこなうために人間がログインするわけではないということを意味します。これらの特権アカウントは、データベースやWebサーバーのようなミドルウェアなどのコンポーネントのためのアカウントです。これらのサービスは設定ファイルに保管されているシークレットを使ってログインした後、トークンやシークレットを使ってリソースにアクセスします。これらのアカウントは、リソースの利用状況を登録するシステムログのプレースホルダーとして機能します。

例えば、会計ソフトウェアにおいて、アプリケーションはリレーショナルデータベースに取引を登録する必要がある可能性があります。この登録をおこなうため、アプリケーションは設定されたサービスアカウントのパスワードを見つけ、データベースにログインします。この結果、各トランザクションはアプリケーションにログで記録され、そのアプリケーションが所有します。もちろん、アプリケーションは全てのアクターのアカウントがトランザクションを開始できるものとして登録されていることを保証しなければなりません。

他の例では、バッチアカウントやマクロ、RPAのような自動化に使用されるアカウントがあります。組織の技術チームはそれぞれの自動化タスクのプロセス要件を変更要求として文書化し、実行するために適切なスクリプトと設定を作成します。プロセス自体は実行するために必要な認可を取得する必要があります。言い換えれば、そうしないと「最小特権」の原則に従って、最低限必要な認可を達成できません。

これらのシナリオでは、変更要求者や要件オーナーはスクリプト、マクロまたはRPAの説明責任者と考えられるべきです。

この種のアカウントを管理するためのベストプラクティスは以下のようになります：

*   **変更管理ガバナンス**：これらのアカウントは、JMLのような一般的なIGAプロセスには従わず、認可はロールベースではなく、固有です。説明責任者が要件と機能およびコンポーネントの認可の変更を管理する強固なプロセスを監視することを確実にしてください。
    
*   **最小特権**：アカウントは、タスク実行に必要な最小限の認可を有した状態でプロビジョニングされます。
    
*   **ログイン禁止**：これらのアカウントがオペレーティングシステムのような基盤インフラストラクチャにログインできないようにします。
    

このタイプの特権アカウントの管理ついての詳細は、BoKの _Non-human Account Management_ を参照してください。 [^9]

@row
#### Interactive Non-Human Privileged Accounts

Interactive non-human accounts - the main focus for the remainder of this article - are also called system accounts: these are the built-in component accounts, such as ‘admin’ or ‘root.’ These can also be accounts that are built-in into applications, such as the super-user of an application. A person who needs to use the power of this account will log in to the component with this account name and the password provided by the developer or the vendor. In the session that results, the person _is_ the component.

The existence of these almighty accounts creates severe risks of unauthorized access by individuals capable of breaking or exploiting the component: they can be tremendously damaging to an organization’s security posture if practitioners do not contain and strictly control their usage. As stated, someone who logs in with the component account _**is**_ the component. And that means that the component itself is the actor, performing all the tasks. Without additional measures, the actual human being may not be known or identifiable.

This type of account should only be used in specific circumstances and for a particular purpose, like during an incident or to deliver a change. This practice is a fundamental security principle. A common control is to raise a ticket in a service management solution when access to this type of account is required. A PAM solution can then check that the ticket is valid. Connecting a PAM solution to the service management solution is best practice.

Best practices for managing this type of account include:

*   **No Default Passwords:** Immediately change the default password to prevent unauthorized persons from becoming the component and taking action.
    
*   **Password Vault:** Use a vault to retrieve a password.
    
*   **Restricted Use** : If possible, these accounts should only be used once during setup and then deactivated (if possible) or heavily restricted (e.g., for disaster recovery scenarios).
    
*   **Named Super-Users:** Ensure that usage of the super-user account can be traced to a person. For example, on Linux systems, a system operator logs in normally under their own credential and then uses sudo to promote to root.
    
*   **Service Ticket Validation** : Verify legitimate use at access request time by checking a service management system.
    
*   **Use logging and monitoring** by connecting the PAM to an SIEM or SOC.
    

@column
#### 対話型非人間特権アカウント

対話型非人間アカウント、本記事の残りの部分の主な焦点、もシステムアカウントと呼ばれます：これらは「admin」や「root」のようなビルトインのコンポーネントアカウントです。また、アプリケーションのスーパーユーザーのようなアプリケーションにビルトインのアカウントもありあｍす。このアカウントの権限を利用する必要がある人間は、このアカウントの名前と開発者またはベンダーから提供されたパスワードを使ってコンポーネントにログインするでしょう。その結果としてセッション中では、その人間 _こそが_ コンポーネントです。

この万能なアカウントの存在は、コンポーネントを破壊したり、悪用したりすることができるという個人による認可されていないアクセスという深刻なリスクを生みます：実務者はその使用方法を含めない場合や厳密に管理しない場合、組織のセキュリティ体制に対して甚大な損害を与える可能性があります。前述のように、コンポーネントアカウントによってログインした人 _**こそが**_ 。コンポーネントです。そして、コンポーネント自体がアクターであり、すべてのタスクを実行することを意味します。追加の対応がなければ、実際の人間を知ることも識別することもできないかもしれません。

このタイプのアカウントは、例えばインシデントの発生時や変更を提供するためなど、特定の環境および特定の目的だけに利用すべきです。この慣習は、基本的なセキュリティ原則です。この種のアカウントにアクセスする必要がある場合、一般的な管理はサービス管理ソリューションにチケットを起票することです。PAMソリューションは、そのチケットが有効であることを検証できます。PAMソリューションをサービス管理ソリューションに結合することはベストプラクティスです。

このタイプのアカウントの管理のためのベストプラクティスには以下のものが含まれます：

*   **デフォルトのパスワード利用禁止**：認可されていない人間がコンポーネントになり、アクションをおこなうことを防ぐため、デフォルトのパスワードはすぐに変更します。
    
*   **パスワード保管庫**：パスワードを収集する保管庫を利用する。
    
*   **利用制限**：可能であれば、これらのアカウントはセットアップ時に１回だけ利用し、その後は（可能であれば）非アクティブ化するか大幅に制限する（例えば、災害復旧シナリオのため）べきです。
    
*   **名前付きスーパーユーザー**：スーパーユーザーアカウントの利用は、人間まで追跡できるようにしましょう。例えば、Linuxシステムでは、システムオペレーターは一般的に自身のクレデンシャルでログインし、それからrootに昇格するためにsudoを使います。
    
*   **サービスチケット検証**：サービス管理システムをチェックすることで、アクセス要求において正当な利用であることを検証します。
    
*   **ロギングとモニタリングの実施**：PAMとSIEMまたはSOCを結合することで実施します。
    

@row
## Addressing the Challenges of Privileged Accounts

As established, there is a strong business driver to implement PAM. However, not every organization needs a costly solution. As long as an organization can cope with manual procedures for managing internal privileged accounts, that may be the best fit. A manual process might be something akin to the “envelope procedure,” in which the password to shared admin accounts is stored in a sealed envelope (yes, a physical envelope) that is kept inside a vault (yes, a physical vault). When an emergency arises, this envelope can be opened. This opening should be treated as a security incident resulting in password rotation and a new physical envelope.

This type of process is appropriate when only a handful of people manage the system. Even where it may be effective, beware of risks: if one of these admins is absent or leaves the organization, there will be a lot of work to mitigate the risk of any shared accounts.

@column
## 特権アカウントの課題に対応する

認められているように、PAMの導入には強力なビジネス上の動機が存在します。しかし、全ての組織に高価なソリューションが必要なわけではありません。内部特権アカウントの管理のための手動手続きに組織が協力できる場合、それが最も合うかもしれません。手動プロセスはは「封筒手続き」のようなものであり、共用管理者アカウント向けのパスワードを封印された封筒（そう、物理的な封筒）に保管し、金庫内（そう、物理的な金庫）に保管しておきます。緊急時には、この封筒を開けることができます。この開封ではセキュリティインシデントとして扱うべきであり、パスワードローテーションをおこない、新しい物理的な封筒を作成します。

このタイプのプロセスは、システムを管理する人間が一握りしかいない場合に適切です。効果的であっても、リスクには注意しましょう：これらの管理者の一人が不在であったり、組織を離れたりした場合、共用アカウントのリスクを軽減するために多くの作業が必要になります。

@row
### Privileged Access Management Solutions

Several conditions drive a need for automation and more formal solutions:

*   **Task Volume or Team Size:** When the volume of admin tasks rises or the team size grows beyond five people requiring access, automated PAM should be considered a best practice.
    
*   **Internal Policy** : When an organization's information security policy explicitly addresses the risks of privileged accounts, the business may need to invest in a specific solution.
    
*   **Laws and Regulation:** For many companies, PAM solutions are essential for complying with regulations like the European Union’s GDPR and NIS2 directives or the United States’ HIPAA and PCI DSS regulations explicitly defining the need for privileged access control.
    
*   **Complex Architecture** : In complex architectures, multiple administrators and sysops manage the IT infrastructure landscape. When additional architecture landscapes exist, think of IT + OT environments, as well as hybrid on-prem + cloud and multi-national / multiple jurisdiction environments. Control is becoming a predominant theme.
    
*   **Outsourced Operations** : In the case of outsourced IT operations, either outsourcing the data center or having external parties manage the internal data center, insight into operations and limiting risks needs to be done, and PAM will play an important role.
    

Readers may also be interested in reading the Body of Knowledge article “ _The Business Case for IAM_ .” [^10]

With a need for automated PAM processes, organizations can implement a PAM solution. These solutions provide several means for managing Privileged Accounts. These can include different approaches to privilege management and secrets management, and they support a variety of operational use cases.

@column
### 特権アクセス管理ソリューション

いくつかの状況では自動化およびさらに正式なソリューションの必要性を促します：

*   **タスク量またはチーム規模**：管理者タスクの量が増えたり、アクセス権を要求するチーム規模が5人よりも多くなったりしたとき、自動PAMはベストプラクティスと考えるべきです。
    
*   **内部ポリシー**：組織の情報セキュリティポリシーで明確に特権アカウントのリスクに対応するとき、企業は特定のソリューションに投資する必要があるかもしれません。
    
*   **法律と規制**：多くの企業では、PAMソリューションは欧州連合のGDPRやNIS2指令、あるいは特権アクセス制御の必要性を明確に定義した米国のHIPAAやPCI DSS規制のような規制への準拠が不可欠です。
    
*   **複雑なアーキテクチャ**：複雑なアーキテクチャでは、複数の管理者やシステム運用者はITインフラストラクチャ・ランドスケープを管理します。追加のアーキテクチャ・ランドスケープが存在する場合、IT + OT環境、オンプレミス * クラウドのハイブリッド環境、多国籍／複数法域環境と考えられます。制御は主要なテーマになりつつあります。
    
*   **運用アウトソーシング**：データセンターのアウトソーシングや内部データセンターを外部で管理するようなIT運用をアウトソーシングするとき、運用状況を把握し、リスクを抑える必要があり、PAMは重要な役割を果たします。
    

また、読者はBody of Knowledgeの記事「 _The Business Case for IAM_ 」 [^10] を読むことに興味があるかもしれません。

自動化されたPAMプロセスの必要性によって、組織はPAMソリューションを導入することができます。これらのソリューションは、特権アカウントを管理するいくつかの方法を提供します。これらには、特権管理およびシークレット管理に対する異なるアプローチが含まれており、様々な運用上のユースケースをサポートします。

@row
### Privilege Management

*   **Approval Workflows:** When a privileged account is configured with an approval workflow, a user must go through several approval phases to obtain privileged access. Depending on the type and sensitivity of the access request, this may entail approvals from managers at higher levels, security teams, or technical specialists. The PAM system maintains the record of all the requests and approvals. These steps ensure that access to privileged accounts or resources is granted only when required and only under secure conditions. In turn, this minimizes the risk of unauthorized use of privileged access.
    
*   **Just-In-Time** **(JIT) Privilege Escalation** : When privileges are assigned on a JIT basis, it means only time-bound privileged access that is automatically revoked when a predetermined time expires. This control ensures that privileged access is provided only when required and prevents users from abusing permanent standing privileges. It also minimizes the organization’s overall attack surface. Combined with MFA, Request/Approval workflows, email notifications, and ITSM Ticket validation, JIT Provisioning is a powerful control.
    
*   **Privileged Identity Management** : Some solutions offer a combination of on-demand access and role-based access control (RBAC) provided via an Identity Governance and Administration (IGA) solution.
    

@column
### 特権管理

*   **承認ワークフロー**：特権アカウントが承認ワークフローによって設定される場合、ユーザーは特権アクセスを取得するために複数の承認フェーズを通過しなればなりません。アクセス要求の種類や機密性に応じて、より高いレベルの管理者、セキュリティチームまたはテクニカルスペシャリストによる承認が必要かもしれません。PAMシステムは、すべての要求と承認の記録を維持します。これらの段階は、必要なときにだけ、安全な環境だけで、特権アカウントへのアクセスまたはリソースへのアクセス権が与えらえることを保証します。結果、これは特権アクセスの認可されていない利用のリスクを最小にします。
    
*   **ジャストインタイム** **（JIT）特権昇格**：特権がJITベースで割り当てられている場合、予め決定した有効期限となると自動的に取り消される時間制限のある特権アクセスのみを指します。この制御は、必要なときにだけ特権アクセスが提供され、ユーザーが永続的な特権を乱用することを防ぐことを保証します。また、組織全体の攻撃対象を最小にします。MFA。要求／承認ワークフロー、Eメール通知およびITSMちっっと検証と組み合わせることで、JITプロビジョニングは強力な制御になります。
    
*   **特権アイデンティティ管理**：一部のソリューションは、オンデマンドアクセスとアイデンティティガバナンスと管理（IGA）ソリューションを介して提供されるロールベースアクセス制御（RBAC）の組み合わせを提供します。
    

@row
### Secret Management

Secrets management aims to securely store, distribute, and control access to sensitive information, such as passwords, encryption keys, API tokens, and certificates. PAM solutions often offer:

*   **Password Vaulting** : A digital password vault contains the privileged account's password. Anyone who knows how to open the vault can use the password. Whenever the password is used, the password vault will rotate the password so that the used password can no longer be used or shared.
    
*   **Password Rotation** : PAM systems can automatically rotate the passwords for privileged accounts “on access” (i.e., when the session ends) or based on a defined frequency like every 7, 14, 90, or _n_ days. In some cases, it even offers disposal passwords that are valid for only a few minutes or hours.
    
*   **Secrets** : Secrets management ensures the secure handling of sensitive information involved in Continuous Integration (CI), Continuous Deployment (CD), and API management. PAM solutions increasingly cater to API keys, session tokens, access tokens, etc. Non-human services, such as API gateways and microservices, use these tokens.
    

| **Secret Management for CI and CD** | **Secret Management for APIs** |
| --- | --- |
| **Environment Variables:** CI/CD systems like Jenkins, Travis CI, or CircleCI allow developers to store sensitive information as environment variables. These secrets are encrypted and can be accessed during the pipeline execution, ensuring that they are never exposed directly in code or logs. | **API Keys and Tokens:** When accessing external APIs, developers often require API keys or tokens. Secrets management ensures that these keys are stored securely and are only accessible by authorized services or applications. It also enables the rotation of keys to mitigate security risks. |
| **Secrets Vault:** Many organizations use dedicated secrets management tools like HashiCorp Vault or AWS Secrets Manager. These tools centralize the storage of secrets, enforce access controls, and often provide features like secret rotation and auditing. CI/CD pipelines can authenticate and retrieve secrets from these vaults as needed. | **OAuth and JWT:** For more robust API access control, OAuth tokens and JSON Web Tokens (JWTs) are used. Secrets management ensures that the keys used to sign and verify these tokens are kept secure and rotated as necessary. |
| **Temporary Credentials:** For cloud-based services, CI/CD pipelines can request temporary access credentials from the cloud provider’s IAM (Identity and Access Management) services. This limits exposure and ensures that access credentials are short-lived. | **Role-Based Access Control (RBAC):** Secrets management can enforce RBAC for APIs, ensuring that only authorized users or applications have access to specific endpoints or resources. |
|     | **Logging and Monitoring:** API access should be closely monitored, and logs should be audited to detect any suspicious or unauthorized access attempts. |

@column
### シークレット管理

シークレット管理は、パスワード、暗号化キー、APIトークンおよび証明書のような機密情報を安全に保管、配信およびアクセスの制御をおこなうことを目的にしています。多くの場合、PAMソリューションは以下を提供します：

*   **パスワードの保管** : デジタルパスワードの保管庫には特権アカウントのパスワードが含まれます。保管庫の開け方を知っているすべての人はパスワードを使うことができます。パスワードを使用する場合は、毎回パスワード保管庫はパスワードをローテートし、使用済のパスワードは使用や共有ができなくなります。
    
*   **パスワードのローテーション** : PAMシステムは、特権アカウントの「アクセス時」（つまり、セッション終了時）または7、14、90やn日毎のように定義済の頻度で自動的にパスワードをローテートします。場合によっては、数分か数時間だけ有効な使い捨てのパスワードを提供することもあります。
    
*   **シークレット** : シークレット管理は、継続的インテグレーション（CI）、継続的デプロイ（CD）およびAPI管理における機密情報の安全な管理を保証します。PAMソリューションは、APIキー、セッショントークン、アクセストークンなどへ対応が増えてきています。APIゲートウェイやマイクロサービスのような、非人間サービスはこれらのトークンを利用します。
    

| **CIおよびCD向けのシークレット管理** | **API向けのシークレット管理** |
| --- | --- |
| **環境変数**：Jenkins、Travis CIやCircleCIのようなCI/CDシステムは、開発者が機密情報を環境変数として保管することを可能にします。これらのシークレットは暗号化され、パイプライン実行時にアクセスされることで、コードやログに直接さらされることがなくなります。 | **APIキーおよびトークン**：外部APIにアクセスする場合、多くの場合で開発者にはAPIキーまたはトークンが必要です。シークレット管理は、これらのキーが安全に保管され、認可されたサービスやアプリケーションだけがアクセスできることを保証します。また、セキュリティリスクを軽減するため、キーのローテーションをおこないます。 |
| **シークレットの保管**：多くの組織はHashiCorp ValutやAWS Secrets Managerのような専用のシークレット管理ツールを利用します。これらのツールはシークレットの管理を一元化し、アクセス性制御を実施し、しばしばシークレットローテーションおよび監査のような機能を提供します。CI/CDパイプラインは、認証をおこない、必要なときにこれらの保管庫からシークレットを取得します。 | **OAuthおよびJWT**：さらに堅固なAPIアクセス制御のために、OAuthトークンおよびJSON Web Token（JWT）が利用されます。シークレット管理は、これらのトークンを署名および検証するためのキーが安全に管理され、必要なときにローテートされることを保証します。 |
| **一時的なクレデンシャル**：クラウドベースサービスのため、CI/CDパイプラインは、クラウドプロバイダーのIAM（アイデンティティとアクセス管理）サービスから一時的なアクセスクレデンシャルを要求します。これは漏洩を抑制し、アクセスクレデンシャルが短命であることを保証します。 | **ロールベースアクセス制御（RBAC）**：シークレット管理はAPIに対するRBACを実施させ、認可されたユーザーやアプリケーションだけが特定のエンドポイントまたはリソースへのアクセス権を取得することを保証します。 |
|     | **ロギングと監視**：APIアクセスは監視に近いものであるべきであり、ログは何らかの疑念がある、もしくは認可されていないアクセス試行を検知するための監査であるべきです。 |

@row
### PAM Use Cases and Architectural Choices

*   **PAM as Single Sign-On** : Accessing a privileged account requires a user login. When using a PAM system, the PAM system will log in on behalf of the user. For the user, this means logging into the PAM system and then single sign-on from the PAM portal. It’s not ‘true’ single sign-on since the PAM solution logs in every time, but the user no longer has to use the admin login functions.
    
*   **PAM as a Stepping Stone:** The stepping stone mechanism, also called Jump Server, enables a user to log in to the PAM system, and when the session is started, the PAM system gives access to secured components, like servers. Usually, this is done by creating an SSH or an RDP session that the PAM system can control (and end). It should not be possible to bypass the PAM system. Note that this approach has the added benefit of enabling remote access for target user groups.
    

The following section explores a variety of architectures incorporating PAM.

@column
### PAMユースケースとアーキテクチャの選択

*   **SSOとしてのPAM**：特権アカウントへのアクセスにはユーザーのログインが必要です。PAMシステムを利用する場合、PAMシステムがユーザーに代わってログインします。ユーザーにとっては、これはPAMシステムにログインし、PAMポータルからシングルサインオンすることを意味します。これはPAMソリューションが毎回ログインをおこなうために「真の」シングルサインオンではありませんが、ユーザーは管理者ログイン機能を使う必要がなくなります。
    
*   **飛び石としてのPAM**：飛び石メカニズム、ジャンプサーバーとも呼ばれる、はユーザーがPAMシステムにログインできるようにし、セッション開始時にPAMシステムはサーバーのような保護されたコンポーネントに対するアクセスを許可します。一般的に、これはPAMシステムが管理する（および終了させる）SSHまたはRDPセッションを作成することで実現されます。PAMシステムをバイパスできるようにすべきではありません。このアプローチは、対象のユーザーグループにリモートアクセスを可能にするという利益があることに注意してください。
    

以下のセクションでは、PAMに組み込まれる様々なアーキテクチャについて探ります。

@row
#### PAM as a Stepping Stone

@column
#### 飛び石としてのPAM

@row
![A diagram showing a PAM system at the center of an architecture that includes ITSM, Directory, SOC/SIEM, Recording, and Target System. ](/assets/images/idpro_bok/PAM-image3.png)

Figure 3: PAM as a Stepping Stone Architecture

@row
Traditionally, PAM systems are installed in a data center, close to the components they manage. PAM systems can also be implemented as a SaaS solution (see the cloud discussion section at the end of this section).

@column
伝統的に、PAMシステムはデータセンター、つまり管理するコンポーネントの近くにインストールされていました。また、PAMシステムがSaaSソリューションとして実装されることもあります（このセクションの最後にクラウドについての議論があります）。

@row
#### PAM in IT / OT environments

In organizations employing Operational Technology (OT) components, the IT and OT domains are separated by default. This separation may be via airgap firewalls, Industrial Control Systems (ICS), or SCADA implementations. Some organizations add IT capabilities to OT to share control center capabilities and to provide remote access and monitoring. Traditionally, the separation is done through SCADA or ICS systems. A modern and more affordable solution is to use a ‘PAM-PAM’ connection that secures access. Only through an IT-PAM system does an operator get access to an OT-PAM system, where OT tasks can be performed:

@column
#### IT/OT環境のPAM

オペレーショナルテクノロジー（OT）コンポーネントを導入している組織では、デフォルトではITとOTの領域が分離されています。この分離は、エアギャップ・ファイアウォール、産業制御システム（ICS）やSCADAなどの実装を介していることがあります。一部の組織は、コントロールセンター機能を共有し、リモートアクセスとモニタリングを提供するため、IT機能をOTに追加します。伝統的に、分離はSCADAやICSシステムを通じておこないます。モダンでより安価なソリューションでは、アクセスを安全にするための「PAM-PAM」接続を使います。IT-PAMシステムを介してのみ、オペレーターはOT-PAMシステムにアクセスでき、OTタスクは実行できます：

@row
![A diagram showing a PAM-to-PAM architecture in an IT/OT environment. It starts with a Directory and LDAP account, then goes through the IT PAM system to the Admin account, to the OT PAM system and finally the target system.](/assets/images/idpro_bok/PAM-image4.png)

Figure 4: PAM-PAM Architecture in an IT/OT Environment

@row
#### External Service Provider

Many companies outsource parts of their operations management. The component owner is accountable for granting access if a third-party manages company resources. In this case, privileged access must also be assigned to third-party operators. In addition, when using external services, the company must ensure that the service provider uses a PAM solution.

@column
#### 外部サービスプロバイダー

多くの企業では、運用管理の一部をアウトソーシングしています。サードパーティーが企業リソースを管理する場合、コンポーネントの所有者はアクセス権の付与に説明責任があります。この場合、特権アカウントもサードパーティーの運用者に割り当てなくてはなりません。加えて、外部サービスを利用する場合、企業はサービスプロバイダーがPAMソリューションを利用することを保証しなくてはなりません。

@row
![A PAM system in a third-party access model with the internal pam system being fed by the third party PAM system. ](/assets/images/idpro_bok/PAM-image5.png)

Figure 5: PAM in 3rd-Party Access

@row
#### Remote access

As described above, PAM solutions can offer business users and (external) developers remote access capability. This way, legacy remote access services and VPNs can be decommissioned, resulting in lower costs and reduced technical debt.

@column
#### リモートアクセス

上述のように、PAMソリューションはビジネスユーザーと（外部）開発者にリモートアクセス能力を提供することができます。こうすることで、従来のリモートアクセスさビスやVPNを廃止することができ、コスト削減と技術的負債の削減となります。

@row
![A diagram for PAM in a remote access scenario where the PAM account touches a PAM web portal, which is the front half to the PAM System, then goes on to the target system. ](/assets/images/idpro_bok/PAM-image6.png)

Figure 6: PAM for Remote Access

@row
## Implementing PAM

@column
## PAM実装

@row
### Good Implementation Practices

@column
### 良い実装プラクティス

@row
#### Automated Discovery and Component Onboarding

Components that need to be managed through a PAM system must be onboarded first, meaning that the privileged accounts and passwords must be brought into the PAM system. Onboarding components can be done manually, but PAM systems can automate the discovery of components in the network to start the actual onboarding.

@column
#### 自動ディスカバリーとコンポーネントオンボーディング

PAMシステムを介して管理される必要があるコンポーネントはまずオンボーディングしなくてはならず、これは特権アカウントおよびパスワードをPAMシステムに持ち込まなくてはならないということを意味します。コンポーネントのオンボーディングを手動で実行することもできますが、PAMシステムはネットワーク内のコンポーネントの自動的なディスカバリーによって実際のオンボーディングを開始することもできます。

@row
#### Session Control

Authentication and logging controls happen by default when a session starts from a PAM system. Implementors can also add risk-based session controls, such as:

*   **Session recording** : the whole session is recorded as a video-stream.
    
*   **Keystroke logging** : all keystrokes can be recorded to make audit or forensics possible.
    
*   **Keystroke deny-list** : when working in a console, specific commands can be blocked; for instance, the “rm -rf” control can be blocked, limiting the risk of destructive actions by a highly privileged user.
    

Beware that recording and playing back sessions should be considered a privacy and security issue. Ensure workers (counsels/unions) agree and that playback calls for 4-eyes control. [^11]

@column
#### セッション制御

PAMシステムからセッションが開始されるとき、認証およびロギングの制御がデフォルトで実施されます。また、実装者は以下のようにリスクベースのセッション制御を追加することができます：

*   **セッション記録**：セッション全体がビデオストリームとして記録されます。
    
*   **キーストロークロギング**：監査またはフォレンジックスを実施できるように、全てのキーストロークを記録することができます。
    
*   **キーストロークの拒否リスト**：コンソールで作業している場合、特定のコマンドをブロックすることができます；例えば、「rm -rf」制御をブロックすることができ、高い特権ユーザーによる破壊アクションのリスクを抑制することができます。
    

セッションの記録と再生はプライバシーやセキュリティの問題があると考えるべきであることに注意してください。労働者（カウンセラー/組合）が同意しておりその再生が2者による制御が必要であることを確認してください。 [^11]

@row
#### Break-the-Glass Procedures

PAM systems act as authentication services. If the service is not available, the operator cannot get access to the component that needs to be managed. While redundancy is an essential control, break-the-glass procedures enable access to the password vault under emergency conditions.

@column
#### ブレーク・ザ・ガラス手順

PAMシステムは認証サービスとして振る舞います。サービスが利用できない場合、運用者は管理する必要があるコンポーネントにアクセスすることができません。冗長性は必要な制御である一方、ブレーク・ザ・ガラス手順は緊急時にパスワード保管庫にアクセスすることを可能にします。

@row
#### PAM in the Cloud

Developments in PAM mirror the developments in most IT domains: where PAM systems used to be self-hosted, on-prem systems, nowadays, both SaaS and MSP options are becoming available, as well as hybrid solutions.

@column
#### クラウドでのPAM

PAMの発展は、ほとんどのIT領域の発展を反映しています：PAMシステムは以前はセルフホスト、オンプレミスシステムでしたが、現代ではSaaSとMSPの両方の選択肢が利用できるようになり、ハイブリッドソリューションも登場しています。

@row
#### Third-Party Contracts

When outsourcing operations or using services provided by third parties, an organization must ensure that PAM requirements and rules apply to the third party. To protect the supply chain in this way, organizations should build this requirement into third-party contracts as well as procurement and vendor management processes.

@column
#### サードパーティとの契約

アウトソーシング運用またはサードパーティが提供するサービスを利用する場合、組織はサードパーティにPAM要件とルールを適用することを保証しなくてはなりません。この方法でサプライチェーンを保護するため、組織は、調達およびベンダー管理プロセスと同様に、サードパーティとの契約にこの要件を入れるべきです。

@row
### Addressing Barriers

@column
### 障壁の克服

@row
#### Adoption & Friction

PAM System adoption depends heavily on user experience. PAM systems often add extra steps to log into the target systems, introducing a new pattern. Like the reason for access, ticket number, MFA, or lack of native integration with remote tools, these changes to established methods may lead to frustration among users. This friction also might lead users to seek backdoors that help them bypass PAM systems.

Current admin account users may regret their loss of almighty powers – and may feel less empowered to manage their components. They may fear being mistrusted by management. It should be noted that these concerns are real: communication is essential in change management, and emphasis on the added functionality of PAM solutions, such as single sign-on and auditability of actions, can help.

@column
#### 採用と摩擦

PAMシステムの採用は、ユーザー体験に大きく依存しています。多くの場合、PAMシステムは対象システムへのログインに追加ステップを加え、新たなパターンとなります。アクセスの理由、チケット番号、MFAや遠隔ツールとのネイティブな結合の欠如など、確立されている方法へのこれらの変更はユーザーにとってフラストレーションとなるかもしれません。この摩擦もP、ユーザーがAMシステムをバイパスするためのバックドアを探すことになるかもしれません。

現在の管理者アカウントユーザーは、万能な力を失うことに公開するかもしれませんし、コンポーネントを関するために権限が不足していると感じるかもしれません。マネジメント層から不審に思われていると恐れるかもしれません。これらの懸念が現実にあることに注意すべきです：変更管理においてコミュニケーションは必要不可欠であり、シングルサインオンやアクションの監査可能性のようなPAMソリューションの追加機能を強調することが役立つかもしれません。

@row
#### PAM System Availability

PAM system availability is one of the biggest concerns for organizations. If the PAM system is unavailable, it prevents recovery since all the privileged accounts required to access IT assets are stored and managed by the PAM system. This risk can be countered by a flawless and tested break-glass procedure, which enables swift access recovery. Unfortunately, these break-glass accounts are often forgotten and can cause more harm than good, so it’s necessary to monitor, test, and securely store the break-glass credentials.

@column
#### PAMシステムの可用性

PAMシステムの可用性は、組織にとって最大の懸念の1つです。PAMシステムが利用できない場合、IT資産にアクセスするために必須のすべての特権アカウントは保管され、PAMシステムによって管理されていることから回復を妨げます。このリスクは、完璧でテスト済のブレークガラス手順によって対抗することができ、迅速なアクセスリカバリーを可能にします。残念ながら、多くの場合でこれらのブレークガラスアカウントは忘れられ、利益よりも多くの害をもたらす可能性があるため、監視、テストそして安全にブレークガラス・クレデンシャルを管理する必要があります。

@row
#### Password Rotation of Hard-Coded Credentials

Almost every service or application requires credentials to communicate with databases or other applications. These credentials are used to prove the application’s identity. Typically, they are privileged and embedded in various locations, such as configuration files, source code, INI files, OS services, and scheduled tasks, which are referred to as dependencies of the credentials. Therefore, when the password is rotated, the new password must also be updated in all dependencies. Many mature Privileged Access Management (PAM) systems can automatically update the new passwords in the dependencies after rotation.

@column
#### ハードコーディングされたクレデンシャルのパスワードローテーション

ほとんど全てのサービスやアプリケーションは、データベースやその他のアプリケーションと通信するためにクレデンシャルを必要とします。これらのクレデンシャルは、アプリケーションのアイデンティティを証明するために利用されます。通常、クレデンシャルは特権を持ち、設定ファイル、ソースコード、INIファイル、OSサービスやスケジュールされたタスクなどクレデンシャルの依存関係と呼ばれるような様々な場所に埋めこまれています。つまり、パスワードをローテートするとき、新しいパスワードも全ての依存関係で更新しなければなりません。多くの成熟した特権アクセス管理（PAM）システムは、ローテーション後に依存関係において自動的に新しいパスワードに更新することができます。

@row
## Conclusion

Remember, PAM solutions do not address all risks relating to sensitive data access: practitioners must understand different privileged access scenarios and map them to the appropriate controls. First and foremost, they must consider the differences between human and non-human accounts. PAM solutions are not a panacea and do not address the thorny challenges of managing people or the non-interactive accounts that do not require humans once coded (these are demonstrably not people). Effective policy, governance, change management, and other controls are still very much required.

PAM solutions are best used for interactively used non-human accounts, although their secret management tools often cater to the needs of non-interactively used non-human accounts. Make sure that these use cases are identified correctly before introducing any technology.

Once an organization introduces PAM tools, do not underestimate the impact of culture: it can be a significant change for people. It is essential to bring people along, highlight the benefits of additional functionality, and communicate the necessity of an improved security posture for the organization.

@column
## 結論

PAMソリューションは機密データアクセスに関連するすべてのリスクに対応することはできないということを覚えておいてください：実務者は異なる特権アクセスシナリオを理解し、それらに適切な制御を適用しなければなりません。何よりもまず、実務者は人間と非人間アカウントの違いを考慮しなければなりません。PAMソリューションは万能ではなく、人間やいったんコーディングしたら人間を必要としない非対話型アカウント（明らかに人間ではない）を管理するような難しい課題に対応できないです。効果的なポリシー、ガバナンス、変更管理やそのほかの制御は依然として非常に必要です。

PAMソリューションは、対話敵に利用される非人間アカウントに対して利用されるのが最適ですが、これらのシークレット管理ツールは非対話的に利用される非人間アカウントのニーズに対応することが多いです。テクノロジーを導入する前に、これらのユースケースが正しく特定されていることを確認しましょう。

組織がPAMツールを導入すると、文化の影響を過小評価しないでください：これは人々にとって重要な変更です。人々を巻き込み、追加機能の利点を強調し、組織のセキュリティ体制の改善の必要性を伝えることが不可欠です。

@row
### Remember these Core Principles

*   **Least Privilege:** maximum authorization should be equal to the bare minimum required to perform a task (or simply said: “just enough” access).
    
*   **Ownership:** the accountable owner of a component is the owner of the non-human (built-in/admin) account. This is also true of service accounts (non-interactive). The owner of the component is accountable for providing access.
    
*   **Security Controls** : should be layered on top, including MFA. These must be applied with a risk-based strategy (e.g., what is the suitable retention period for session recording/keystroke logging, given the organization’s server capacity?).
    
*   **Third-Party Access:** with third parties, the component's owner must ensure that contracted third-party personnel _only_ have access via PAM.
    
*   **Outsourcing:** The contract owner must ensure that the service provider employs a fitting PAM facility for managing the outsourced service.
    

@column
### 以下の中核となる原則を覚えましょう

*   **最小特権**：最大の認可は、タスクの実行に必要な最低限の認可と同じであるべきです（単純にいうと：「必要十分な」アクセス権）。
    
*   **所有権**：コンポーネントの説明責任のある所有者は、非人間（ビルトイン/管理者）アカウントの所有者です。これはサービスアカウント（非対話型）でも当てはまります。コンポーネントの所有者は、アクセス権の提供に説明責任があります。
    
*   **セキュリティ制御**：MFAを含めて、セキュリティ制御は重ねるべきです。セキュリティ制御はリスクベースの戦略として適用しなければなりません（例えば、組織のサーバー容量を考慮し、セッション記録/キーストロークロギングの適切な保存期間はどの程度か）。
    
*   **サードパーティアクセス**：サードパーティが存在する場合、コンポーネントの所有者は契約したサードパーティの要員がPAMを介したとき _だけ_ アクセスできることを保証しなければなりません。
    
*   **アウトソーシング**：契約の所有者は、サービスプロバイダーが外部委託されたサービスを管理するために適したPAM機能を採用することを保証しなければなりません。

@row
## Appendix: A Note on Entra ID

The IDPro Body of Knowledge is an independent source of information and the authors do not endorse any specific product or vendor. With that said, we do acknowledge that guidance related to widely adopted products can be useful to practitioners.

One of these products is Microsoft’s Entra ID, formerly Azure AD. This is an Identity and Access Management solution that runs on the Azure cloud platform. It is used to manage digital identities and authorization in cloud environments using modern federation protocols like OAuth2.0, SAML, and OpenID Connect. Given its role in access control, Microsoft added extensive authorization profiles to secure access to Entra ID and Azure administrative functions. This is called “Privileged Identity Management” (PIM).

With features like just-in-time access and role-based approval workflows, one could argue that PIM is a PAM solution. This article will not weigh the benefits of PIM versus a dedicated PAM solution in general. However, when an organization works on primarily on Azure and has a compatible license,[^12] PIM offers a core element of its security strategy. When other platforms and on-premises systems are present, a supplementary or alternative PAM solution may make sense.

@column
## Appendix: Entra IDに関する注意書き

IDPro Body of Knowledgeは独立した情報ソースであり、著者は特定の製品やベンダーを推奨してはいません。そうはいうものの、広く採用されている製品に関連したガイダンスが実務者にとって有用であることは認識しています。

そのような製品の1つがMicrosoftのEntra ID、以前の名称はAzure ADです。これはアイデンティティとアクセス管理ソリューションであり、Azureクラウドプラットフォーム上で動作します。これは、デジタルアイデンティティの管理およびOAuth2.0、SAMLやOpenID Connectのようなモダンなフェデレーションプロトコルを使ったクラウド環境での認可に利用されます。アクセス制御での役割を考慮し、MicrosoftはEntra IDおよびAzure管理機能に対するアクセスを安全にするために高度な認可プロファイルを追加しました。これは「特権アイデンティティ管理」（PIM）と呼ばれます。

ジャストインタイムアクセスやロールベース承認ワークフローのような機能によって、PIMはPAMソリューションであると主張する人もいます。この記事では、PIMと一般的な専用のPAMソリューションの利点を比較することはしません。しかし、組織がAzure上で主に作業し、互換性のあるライセンスを保有している場合、[^12] PIMはこのセキュリティ戦略の中核となる要素を提供します。他のプラットフォームおよびオンプレミスシステムが存在する場合、補完的または代替的なPAMソリューションが合理的かもしれません。

@row
## Author Bio

André Koot has over 25 years of experience in the field of IAM, and he is a principal consultant and co-founder of SonicBee, a Dutch IAM consultancy company (IDPro partner). André is focused on business consultancy and gives IAM training courses aligned with the BoK. He is also a member of the IDPro BoK committee and (co-) authored several articles in the BoK.

@row
## Acknowledgments

The author wishes to thank BoK editor Elizabeth Garber for reviewing and helping with this article. He also wishes to thank other contributors and reviewers:

Contributors

*   Pranav Chugh
    
*   Sebastian Rohr
    
*   Eric Woodruff, thanks for the diagrams
    
*   Lance Peterman
    

Reviewers

*   Bertrand Carlier (IDPro)
    
*   Mike Kiser (IDPro)
    
*   Abhi Bandopadhyay
    

- - -

[^1]:  Carter, M. K., (2022) “Techniques To Approach Least Privilege”, _IDPro Body of Knowledge_ 1(9). doi: https://doi.org/10.55621/idpro.88 
    
[^2]:  Bago (Editor), E. & Glazer, I., (2021) “Introduction to Identity - Part 1: Admin-time (v2)”, _IDPro Body of Knowledge_ 1(5). doi: [https://doi.org/10.55621/idpro.27](https://doi.org/10.55621/idpro.27) 
    
[^3]:  Carter, M. K., (2022) “Techniques To Approach Least Privilege”, _IDPro Body of Knowledge_ 1(9). doi: https://doi.org/10.55621/idpro.88 
    
[^4]:  Bago (Editor), E. & Glazer, I., (2021) “Introduction to Identity - Part 1: Admin-time (v2)”, _IDPro Body of Knowledge_ 1(5). doi: [https://doi.org/10.55621/idpro.27](https://doi.org/10.55621/idpro.27) 
    
[^5]:  OWASP (2021) “OWASP Top 10: 2021,” https://owasp.org/Top10/A01\_2021-Broken\_Access\_Control/ 
    
[^6]:  European Parliament and the Council of the European (2022) “DIRECTIVE (EU) 2022/2555 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL of 14 December 2022on measures for a high common level of cybersecurity across the Union, amending Regulation (EU) No 910/2014 and Directive (EU) 2018/1972,” clause 49, https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32022L2555 
    
[^7]:  BBC (2020), “Major US Twitter accounts hacked in Bitcoin scam “ https://www.bbc.com/news/technology-53425822 
    
[^8]:  Cameron, A. & Grewe, O., (2022) “An Overview of the Digital Identity Lifecycle (v2)”, _IDPro Body of Knowledge_ 1(7). doi: [https://doi.org/10.55621/idpro.31](https://doi.org/10.55621/idpro.31) 
    
[^9]:  Williamson, G., Koot, A. & Lee, G., (2022) “Non-human Account Management (v4)”, _IDPro Body of Knowledge_ 1(11). doi: [https://doi.org/10.55621/idpro.52](https://doi.org/10.55621/idpro.52) 
    
[^10]:  Koot, A., (2023) “The Business Case for IAM”, _IDPro Body of Knowledge_ 1(12). doi: [https://doi.org/10.55621/idpro.97](https://doi.org/10.55621/idpro.97) 
    
[^11]:  And as a side note: storage of recordings could lead to capacity issues. 

[^12]:  At the time of writing this includes Premium P2, 365 E5, or EMS (E5)
