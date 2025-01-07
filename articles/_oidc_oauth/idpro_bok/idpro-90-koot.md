---
layout: columns
title: Strategic Alignment and Access Governance
permalink: /docs/oidc_oauth/idpro_bok/90
date: 2024-09-09
modify_date: 2024-12-29
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "アクセスガバナンス", "戦略的アライメント"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/90/](https://bok.idpro.org/article/id/90/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

In today’s digital age, for an organization to succeed, it must have a strong IT function. That IT function will not be at its best, however, if it is missing a close partnership with the business components of the organization. In many organizations, IAM is seen as an IT responsibility. While some IAM-related tasks and activities can be considered IT-related, others are not. Without a clear understanding of the different tasks and responsibilities in the field of IAM, the success of IAM-related programs will be limited.

This article argues for the need for explicit strategic alignment, also referred to as business-to-IT alignment, between IT efforts around IAM, particularly access management, and the business needs of an organization. Lack of this type of alignment leads to failed IAM projects and blocked business maturity growth.

**Keywords:** Access Governance, Strategic alignment, Governance, IAM, IT, ICT

@column
## 概要

今日のデジタル時代において、組織が成功するためには、強力なIT部門を持っていなければなりません。しかし、組織のビジネス部門との緊密な連携が欠けていると、IT部門は最高の力を発揮できないでしょう。多くの組織では、IAMはITの責任とみなされています。IAM関連のタスクや活動は、一部はIT関連とみなされ、他はみなされないことがあります。IAM分野における多様なタスクと責任を明確に理解しなければ、IAM関連プログラムの成功は限定的なものになるでしょう。 

本稿では、IAM、特にアクセス管理に関するITの取り組みと組織のビジネスニーズとの間に、ビジネスITアライメントとも呼ばれる、明確な戦略的アライメントを必要とすることを主張しています。この種のアライメントが欠如しているとIAMプロジェクトが失敗したり、ビジネス的に成熟した成長が阻害されたりします。

**Keywords:** アクセスガバナンス, 戦略的アライメント, ガバナンス, IAM, IT, ICT

@row
By André Koot

© 2022 IDPro, André Koot

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction

Many Information Technology (IT) departments are responsible for implementing IAM systems to support an organization’s efforts to operate efficiently and effectively. Identity management systems are designed to automate the joiner, mover, and leaver processes (JML processes) for employees. [^1] Access management systems, in turn, are designed to make it possible to request and grant authorizations in information systems and even physical access to facilities such as buildings or data centers. For IT to support the necessary processes and controls, they must understand the business drivers for the organization. IT in general, and IAM in particular, must serve the organization; strategic alignment is critically important and, unfortunately, challenging. Different day-to-day languages, cultures, and priorities obstruct the understanding on both sides regarding what has to happen and why for the business to succeed.

@column
## 導入

多くの情報テクノロジー（IT）部門は、組織の効率的かつ効果的な運営をサポートするためにIAMシステムの実装に責任を負っています。アイデンティティ管理システムは、従業員のJoiner-Mover-Leaverプロセス（JMLプロセス）を自動化するために設計されています。 [^1] 反対に、アクセス管理システムは、情報システムおよび建物やデータセンターのような施設への物理的なアクセスにおいて認可を要求し、付与することを可能にするように設計されています。必要なプロセスと制御をサポートするためにIT部門にとって、組織におけるビジネス的な動機付けを理解しなくてはなりません。一般的にIT部門および特にIAM部門は組織に貢献しなければなりません；戦略的アライメントは非常に重要であり、残念ながら困難です。日々の言語、文化および優先順位が異なると、ビジネスが成功するために何がなぜ必要なのか、双方の理解が妨げられます。

@row
### Terminology

*   Alignment: the synchronization rate of processes and environments
    
*   Governance: making sure that accountable owners are demonstrably in control
    
*   Identity Governance and Administration: a solution for automating user management and authorizations in target systems, building on the organization’s customer and human resource processes.
    
*   Joiner-Mover-Leaver processes: The joiner/mover/leaver lifecycle of an employee identity considers three stages in the life cycle: joining the organization, moving within the organization, and leaving the organization. [^2]
    

@column
### 用語解説

*   アライメント：プロセスと環境の同期率
    
*   ガバナンス：説明責任のある所有者が確実に管理できるようにする
    
*   アイデンティティガバナンスと管理：組織の顧客プロセスと人事プロセスを基盤に、 対象システムのユーザー管理と認可を自動化するソリューション
    
*   Joiner-Mover-Leaverプロセス：従業員アイデンティティのjoiner/mover/leaverライフサイクルは、ライフサイクルを3つのステージと考えています：組織への加入、組織内での異動、組織からの離脱。 [^2]
    

@row
### Acronyms

*   CEO: Chief Executive Officer; CFO Chief Financial Officer; CRO Chief Risk Officer; CTO Chief Technology Officer; COO: Chief Operations Officer
    
*   RBAC: Role-Based Access Control
    
*   IGA: Identity Governance and Administration
    
*   JML processes: joiner, mover, and leaver processes
    

@column
### 略語

*   CEO：最高経営責任；CFO 最高財務責任者；CRO 最高リスク責任者；CTO 最高技術責任者；COO 最高執行責任者
    
*   RBAC：ロールベースアクセス制御
    
*   IGA：アイデンティティガバナンスと管理
    
*   JMLプロセス：Joiner-Mover-Leaverプロセス
    

@row
## Understanding Strategic Alignment

Business-to-IT Alignment, also known as Strategic Alignment, has been studied since the 1980s. Following the Henderson and Venkatraman model, strategic alignment brings together a dynamic integration of IT planning and business development to shape or enable a holistic business strategy.

Ideally, IT enables the business to perform efficiently and effectively. IT can help solve business issues by providing logical, structured ways of working, integrating solutions, and making access and application integrations possible. For example, IT supports automating manual tasks, keeping records, integrating different information processing components and systems, and following security best practices. IT better understands what problems need to be solved when aligned closely with the organization’s business drivers. In general, businesses are more successful when they incorporate the efficiencies IT can bring to the table.

In order to reach the necessary levels of strategic alignment, we first must consider the barriers. Often, the language used by the business to identify what’s important is quite different than the language used in IT.

|     |     |     |
| --- | --- | --- |
| Business talks about |     | IT talks about |
| Customer satisfaction |     | System service level agreements (e.g., 99.999% availability) |
| Return on Investment (ROI) |     | Network architecture (e.g., hybrid, cloud, on-prem) |
| Legal and regulatory requirements (e.g., GDPR, CCPA) |     | Common Vulnerability and Exposure (CVE) Announcements [^3] |
| Market share |     | Latest container management technologies (e.g., Kubernetes) |
| Earnings before interest, taxes, depreciation, and amortization (EBITDA) |     | Access control mechanics (e.g., -rwxr-xr-x) |
| Financial bottom line (i.e., General ledger) |     | Network capabilities (e.g., bits per second, database structures)BPS |
| Interest rates |     | Data Center architecture and computing clusters |
| Consumer trust and business reputation |     | P1 (Priority 1 incidents) |

(There is no implied horizontal correlation between the terms in the left and right columns).

@column
## 戦略的アライメントを理解する

戦略的アライメントとしても知られる、ビジネスITアライメントは1980年代から研究されてきました。HendersonおよびVenkatramanモデルに従うと、戦略的アライメントはIT計画とビジネス的な発展の動的な結合し、全体的なビジネス戦略を形作り、実現します。 [^3]

理想的には、ITがビジネスを効率化し、効果的にします。ITは、論理的で構造化された作業方法を提供し、ソリューションを統合し、アクセスやアプリケーションの統合を可能にすることででのビジネスの課題を解決することを助けます。例えば、ITは手作業を自動化し、記録を残し、異なる情報処理コンポーネントとシステムを統合し、セキュリティベストプラクティスに従うようにすることに役立ちます。IT部門は、組織のビジネス動機と密接に連携することで、解決すべき問題をよりよく理解することができます。一般的に、ITがもたらす効率性を取り入れることで、ビジネスはより成功します。

戦略的アライメントに必要なレベルに到達するため、まず障壁について検討しなければなりません。多くの場合、何が重要かを特定するためにビジネスで使われる言葉は、ITで使われる言葉とはまったく異なります。

|     |     |     |
| --- | --- | --- |
| ビジネスでの表現 |     | ITでの表現 |
| 顧客満足度 |     | システムサービスレベルアグリーメント（例、可用性99.999%） |
| 投資収益率（ROI） |     | ネットワークアーキテクチャ（例、ハイブリッド、クラウド、オンプレ） |
| 法的および規制の要件（例、GDPR、CCPA） |     | Common Vulnerability and Exposure（CVE）通知 [^4] |
| マーケットシェア |     | 最近のコンテナ管理技術（例、Kubernetes） |
| 利払い前税引き前償却前利益（EEBITDA） |     | アクセス制御メカニクス（例、-rwxr-xr-x） |
| 当期純利益（つまり、総勘定元帳） |     | ネットワーク容量（例、bits per second、データベース構造）BPS |
| 金利 |     | データセンターアーキテクチャとコンピューティングクラスタ |
| 消費者の信頼と企業の評判 |     | P1（優先順位1のインシデント） |

（左右の列の単語同士には暗黙的な水平相関はありません）。

@row
### Alignment Models

There are different methodologies that describe the necessary points of communication to support strategic alignment. Hendersen and Venkatraman, two IBM fellows, came up with this model for strategic alignment in 1993: [^4]

@column
### アライメントモデル

戦略的アライメントを支持するためのコミュニケーションの要点について述べている複数の方法論が存在します。HendersenとVenkatraman、両者はIBMのフェロー、は1993年に戦略的アライメントのモデルと出会いました： [^5]

@row
![A figure with four boxes that line up with two columns, Business and IT, and two rows, Strategy and Operation. Double-ended arrows point between each box only in the horizontal and vertical axes. ](/assets/images/idpro_bok/90-image1.png)

_Figure 1: Simple Model for Strategic Alignment_

@row
This model suggests that business and IT stakeholders should communicate on both the strategic and the operational levels. This multidirectional communication ensures that the business processes are supported by fitting IT solutions. By pairing strategic choices with operational ones, the organization can minimize unnecessary changes in process and technology. For this model to work, however, the organization must address the fact that IT and the business often have different ways of working, cultures, languages, and jargon. These differences make strategic alignment difficult.

One critical characteristic of this model (and in the other models presented) is that communication between domains/cells can only occur across the horizontal and vertical lines, not diagonally. That means communication can only happen in formalized relations to prevent disrupting formal, mature procedures.

> _Case CEO:_
> 
> _My old CEO was tempted to get a smartphone. All young marketers used those devices, so why not the CEO? But he also wanted to read his company email on the same smartphone. This expectation would not be a problem except for the fact that in 2008 enterprises were not supporting those devices in a standard way. The CEO directly ordered an IT engineer to make it possible: install the app, connect to the mail server, create a secure channel to the Internet, add certificates, etc. This non-standard change interrupted IT operations for three months._

In the Amsterdam Information Model by Professor Rik Maes, Dr. Maes added additional components to implement information management and structure. [^5] :

@column
このモデルでは、ビジネス部門とIT部門の利害関係者が戦略および運用の両方のレベルでコミュニケーションをすべきであることを提案しています。この双方向コミュニケーションは、ビジネスプロセスが適したITソリューションによってサポートされることを保証します。戦略的な選択を運用上の選択と組み合わせることで、組織はプロセスとテクノロジーでの不必要な選択を最小にできます。しかし、このモデルが機能するためには、組織はIT部門とビジネス部門が多くの場合に異なる仕事のやり方、文化、言語および専門用語を持っているという事実に対処しなければなりません。これらの差異は、戦略的アライメントを難しくします。

このモデル（および提示された他のモデル）の重大な特徴の1つは、ドメイン/セル間のコミュニケーションが水平および垂直のラインでしか発生せず、対角線上ではないということです。これは、正式で成熟した手順を混乱させることを防ぐために、正式化された関係でしか起きないことを意味します。

> _ケース CEO:_
> 
> _私の昔のCEOはスマートフォンを手に入れたがっていました。若いマーケティング担当者はみんなスマートフォンを使っていましたが、なぜCEOはそうでなかったのでしょうか？しかし、CEOは同じスマートフォン上で会社メールを確認することも求めていました。この要望は、2008年時点で企業は通常の方法ではこれらのデバイスをサポートしていなかったという事実を除けば問題ではありません。CEOは直接ITエンジニアに以下のことを可能にするように指示しました：アプリをインストールし、メールサーバーと接続し、インターネットとのセキュアなチャネル用意し、証明書を追加するなど。この標準ではない変更はIT運用を3カ月阻害しました。_

Rik Maes教授によるAmsterdam Information Modelにおいて、Maes博士は情報管理と構造を実装するために追加コンポーネントを加えました。 [^6] ：

@row
![A figure with nine boxes that line up with three columns, Business, Information, and Technology, and three rows, Direction, Structure, and Execution. Double-ended arrows point between each box only in the horizontal and vertical axes. ](/assets/images/idpro_bok/90-image2.png)

_Figure 2: the Amsterdam Information Model for Strategic Alignment_

@row
The middle column, Information management, translates the business requirements into IT solutions (left-to-right translation). It also translates the features and functionality of IT components (platforms, services, applications) into business opportunities (the right-to-left translation). The information management function must overcome the issues indicated above, such as language and cultural differences. The information manager (or CIO) should understand and know how to converse with businesspeople and IT personnel. The information manager should be able to connect to the entire organization and act as the missing link in business-to-IT alignment.

The added horizontal middle layer also has a specific ‘translation’ role:

This layer can be seen as the architecture layer. It translates strategic concepts into day-to-day operations. Looking at the different columns within this layer, from left to right, we can identify the following architectural concepts:

*   Business architecture (organogram/org-chart and business processes models, including Segregation of Duties (SoD), abuse of information prevention controls, etc.).
    
*   Information architecture (data models, -flows, and interfaces).
    
*   The IT architecture (including servers and networking, containerization, cloud, and security architecture).
    

In this model, we can position the CEO, CFO, and COO in the top-left area. These persons are accountable for defining the organization's business strategy, direction, and course. The head of IT, or CTO (Chief Technology Officer), would be positioned in the top-right area, accountable for IT strategy, like sourcing strategy and IT vendor management strategy. This assignment leaves the CIO in control of the middle column, responsible for the business-to-IT alignment.

Governance, ownership of control, would, in this model, be owned by the top-left area players.

@column
情報管理の中段のコラムでは、ビジネス上の要求をITソリューションに変換しています（左から右への変換）。また、ITコンポーネント（プラットフォーム、サービス、アプリケーション）の機能や機能性をビジネス機会にに変換しています（右から左への変換）。情報管理機能は上述のような言語と文化の違いの問題を克服しなければなりません。情報管理者（またはCIO）は、ビジネスパーソンやIT担当者との会話の仕方を理解し、知っておくべきです。この情報管理者は、組織全体とつながり、ビジネスITアライメントのミッシングリンクとして機能するべきです。

追加された水平方向の中央のレイヤーも、特定の「翻訳」の役割があります：

このレイヤーはアーキテクチャレイヤーと見ることができます。このレイヤーは戦略的概念を日ごとの運用に変換しています。このレイヤーの別の列を左から右へ見ると、以下のアーキテクチャ的概念を特定することができます：

*   ビジネスアーキテクチャ（職務分掌（SoD）、情報乱用防止策などを含む、組織図とビジネスプロセスモデル）。
    
*   情報アーキテクチャ（データモデル、フローおよびインタフェース）。
    
*   ITアーキテクチャ（サーバーおよびネットワーク、コンテナ化、クラウドおよびセキュリティアーキテクチャを含む）。
    

このモデルでは、CEO、CFOおよびCOOを上段左のエリアに位置付けることができます。これらの人々は、組織のビジネス戦略、方向性および方針を定義する説明責任があります。IT部門のトップ、またはCTO（最高技術責任者）は上段右のエリアに位置付けられ、調達戦略やITベンダー管理戦略のようなIT戦略について説明責任があります。この配置では、CIOが中央の列をコントロールし、ビジネスITアライメントに責任を負うことになります。

このモデルではガバナンス、制御の所有権は上段左のエリアのプレイヤーが所有することになります。

@row
### IAM and Alignment

So far in this article, we have focused on the IT/business relationship in general. As IAM is traditionally considered part of IT, the challenges of strategic alignment are at the core of most failures of IAM projects. In many cases, IAM is very much an IT function. IAM includes basic “techie” tasks such as password resets, account management, user provisioning, and so on. IAM, however, is arguably more closely tied to business needs than any other aspect of IT. Authorization processes, in particular, regularly bridge the gap between IT operations and business requirements.

@column
### IAMとアライメント

ここまで本記事では、一般的なIT/ビジネスの関係性にフォーカスしてきました。IAMは伝統的にITの一部と考えられているため、戦略的アライメントの課題がほとんどIAMプロジェクトの失敗の核心です。多くのケースで、IAMはIT機能と非常に相性がよいです。IAMはパスワードリセット、アカウント管理、ユーザープロビジョニングなど基本的な「技術的」タスクが含まれます。しかし、ほぼ間違いなくIAMは他のITの側面よりもビジネスニーズにより密接に結びついています。特に、認可プロセスは定期的にIT運用とビジネス要件のギャップを橋渡しします。

@row
![A figure with nine boxes that line up with three columns, Business, Information, and Technology, and three rows, Direction, Structure, and Execution. Double-ended arrows point between each box only in the horizontal and vertical axes. The box on the bottom right has a callout that says "Identity sync password reset scripts and tools"](/assets/images/idpro_bok/90-image3.png)

_Figure 3: Amsterdam Information Model - IAM as an IT Function_

@row
IAM started as an IT responsibility. Creating interfaces and connectors, protocols, and adding certificates all fell in the realm of IAM and IT. The trigger for all identity transactions was often the HR department, but in daily operations, identity management belonged to IT as part of the general task of automating business processes. That has not changed. Most identity management in an organization is still seen as IT: bottom right.

Authorization management, on the other hand, is not as easily plotted. Authorization involves “determining a user’s rights to access functionality with a computer application and the level at which that access should be granted. In most cases, an ‘authority’ defines and grants access, but in some cases, access is granted because of inherent rights (like patient access to their own medical data).” [^6] Authorization is directly tied to business practices, and yet the IAM group generally implements them.

Using the Amsterdam Information Model _,_ we can identify where authorizations are most prominently defined. Authorizations are enablers for performing tasks in an organization and so are critical to the execution phases. Authorizations are derived from the organizational structure and business processes. Implementing authorization management must therefore be plotted on the Business Structure area in the model. For example, SoD rules are defined in a business process: one person may not be allowed to perform multiple successive tasks because that could create a risk of fraud, abuse of permissions, or data breaches. Tasks are defined in a process. That means a process owner, ‘mid-left,’ is accountable for defining these specific access control policies.

@column
IAMはIT部門の責任として始まりました。インタフェースおよびコネクター、プロトコルそして追加の証明書の作成のすべてがIAMおよびITの領域に当たります。全てのアイデンティティトランザクションの引き金は多くの場合HT部門ですが、日常の運用ではアイデンティティ管理はビジネスプロセスの自動化という一般的なタスクの一部であることからIT部門となります。これは変わりません。組織におけるほとんどのアイデンティティ管理は依然としてIT部門と見られています：図の下段右に位置します。

一方で、認可管理は簡単にプロットすることができません。認可とは「コンピュータアプリケーションの機能へアクセスするユーザーの権利と、そのアクセス権を付与すべきレベルについて決定すること。多くのケースで、「権威機関」が定義し、アクセス権を付与しますが、一部のケースでは生得権（患者が自身の医療データにアクセスような）によってアクセス権が付与されます。」。 [^7] 認可はビジネスプラクティスに直接紐づきますが、一般的にIAMグループがそれを実施します。

Amsterdam Informationモデルを利用すると、認可が最も顕著に定義されている場所を特定することができます。認可は組織においてタスクを実行できるようにするものであり、認可は実行フェーズにおいて重要です。認可は組織構造やビジネスプロセスに由来しています。つまり、認可管理を実装することはモデルにおいてBusiness Structoreのエリアにプロットされます。例えば、SoDルールはビジネスプロセスにおいて定義されます：詐欺、権限の乱用やデータ漏洩のリスクが生じする可能性があるため、一人の人間が複数の連続したタスクを実行することは許されません。タスクはプロセスで定義されます。よって、「中段左」のプロセスオーナーが、これらの特定のアクセス制御ポリシーを定義する説明責任を負うことを意味します。

@row
![A figure with nine boxes that line up with three columns, Business, Information, and Technology, and three rows, Direction, Structure, and Execution. Double-ended arrows point between each box only in the horizontal and vertical axes. The second box in the first column has a callout that says "Organogram Process architecture Authorizations SoD business rules"](/assets/images/idpro_bok/90-image4.png)

_Figure 4: Amsterdam Information Model - Authorization as a Business Function_

@row
IT does not own or manage business structure authorizations. It’s the responsibility of the ‘business’ owners, specifically the process owners, line managers, or data owners.

Managing authorizations–defining, granting, and revoking them–is one of the more challenging tasks for any organization. This task is where the concept of RBAC became handy. The concept was created in the mainframe era in solutions like IBM’s Resource Access Control Facility (RACF) and the Access Control Facility 2 (ACF2) system. In the local area networking era, RBAC became the solution for managing this authorization complexity. In the nineties, dedicated identity management solutions started to appear, with authorization solutions exploring the concept of RBAC coming into existence at the turn of the century. These solutions evolved over time, eventually offering identity governance by adding attestation/recertification processes.

@column
ITはビジネス構造認可を所有したり、管理したりしません。それは特にプロセスオーナー、ラインマネージャーやデータ所有者など「ビジネス」オーナーの責任です。

認可を定義し、付与し、取り消すという認可の管理は、組織にとってより困難なタスクの1つです。このタスクは、RBACの概念が便利になったものです。この概念はメインフレームの時代に、IBMのリソース・アクセス・コントロール・ファシリティ（RACF）およびアクセス・コントロール・ファシリティ2（ACF2）システムのようなソリューションにおいて生まれました。ローカルエリアネットワークの時代では、RBACはこの認可の複雑性を管理するためのソリューションとなりました。90年代、専用のアイデンティティ管理ソリューションが登場し始め、今世紀になるとRBACの概念を探求した認可ソリューションが登場しました。これらのソリューションは時間とともに進化し、最終的に証明/再認定のプロセスを追加することでアイデンティティガバナンスを提供するようになりました。

@row
![A figure with nine boxes that line up with three columns, Business, Information, and Technology, and three rows, Direction, Structure, and Execution. Double-ended arrows point between each box only in the horizontal and vertical axes. The second box in the first column has a callout that says "Role Based Access Control Identity Governance Access Management"](/assets/images/idpro_bok/90-image5.png)

_Figure 5: Amsterdam Information Model - RBAC and Identity Governance_

@row
These days, we see vendors moving to a spot in the center. Traditional Identity Management software vendors add authorization management solutions and traditional identity governance vendors add identity and workflow management capabilities. There are also ‘new’ entrants in the market, offering cloud-based solutions such as Identity Governance and Administration offerings.

@column
今日、ベンダーが中央に移動していることが見られます。従来のアイデンティティ管理ソフトウェアのベンダーは認可管理ソリューションを追加し、従来のアイデンティティガバナンスベンダーはアイデンティティとワークフロー管理機能を追加しています。アイデンティティガバナンスと管理などのクラウドベースのソリューションを提供する、「新規」参入者も市場に現れています。

@row
![A figure with nine boxes that line up with three columns, Business, Information, and Technology, and three rows, Direction, Structure, and Execution. Double-ended arrows point between each box only in the horizontal and vertical axes. The center box has three callouts, one saying "AM vendors buying into IdM", the next saying "IdM vendors buying into AM", and "Identity Governance and Administration](/assets/images/idpro_bok/90-image6.png)

_Figure 6: Amsterdam Information Model - IGA_

@row
When evaluating Attribute Based Access Control and Policy Based Access Control models, the same strategic alignment change of responsibility can be seen. Several IT-oriented access control policies exist, such as the requirement to use TLS certificates and zero-trust networking. But other access policies are business oriented. Policies like SoD or privacy-related consent management have a clear relation to the business structure sector in the model.

@column
属性ベースアクセス制御およびポリシーベースアクセス制御モデルの場合、同じような戦略的アライメントの責任の変化が見られます。TLS証明書やゼロトラストネットワークを利用するという要件のように、いくつかのIT部門指向のアクセス制御ポリシーが存在します。しかし、他のアクセスポリシーはビジネス部門指向です。SoDやプライバシーに関する同意管理のようなポリシーは、モデル内のビジネス構造部門との明確な関係があります。

@row
### An Extended Case Study

Information systems were generally developed to support the identity management process and to support authorization management; the current generation of IGA solutions performs their role admirably by supporting the business with reliable identities (based on the HR identity lifecycle) with reliable authorizations. And yet, there still is the issue, IAM is still seen as an IT responsibility. Let me explain this in a case:

> _Case Study - Accountability vs. Responsibility_
> 
> _A financial institution supports its identity governance and RBAC requirements by using a modern IGA solution. The system is integrated within the IT landscape and connects several business applications for provisioning and reconciliation._
> 
> _An external auditor reported a high-risk issue concerning authorizations in the financial accounting system to the CEO._
> 
> _The CEO (Top-left) forwarded the findings to the CTO (Top-right), as the finding was about a system, and so the CEO believed IT had to solve the issue. The CTO forwarded the finding about the authorizations to the IGA product owner in the IT Service delivery department (Bottom-right). Unfortunately, the product owner cannot solve the issue._
> 
> _What went wrong?_
> 

@column
### 更なるケーススタディ

情報システムは一般的にアイデンティティ管理プロセスをサポートし、認可管理をサポートするために開発されます；IGAソリューションの現在の世代は、信頼できる認可によって（HR部門のアイデンティティライフサイクルに基づいて）信頼できるアイデンティティのビジネス部門をサポートすることで、その役割を素晴らしく果たしています。しかし、依然として課題は残っており、IAMはまだIT部門の責任とみられています。これを以下のケースを使って説明します：

> _ケーススタディ - 説明責任 対 責任_
> 
> _ある金融機関が、現代のIGAソリューションを使用することで、そのアイデンティティガバナンスとRBAC要件をサポートしています。システムはITランドスケープに統合され、プロビジョニングと調整のためにいくつかのビジネスアプリケーションに接続しています。_
> 
> _外部監査人は、財務会計システムでの認可に関する高リスクの問題をCEOに報告しました。_
> 
> _CEO（上段左）は、調査報告がシステムに関するものであったため、CTO（上段右）に転送し、CEOはIT部門が問題を過いけるする必要があると信じていました。CTOは認可に関する調査をITサービスデリバリー部門のIGAプロダクトオーナー（下段右）に転送しました。残念ながら、プロダクトオーナーは問題を解決できませんでした。_
> 
> _何が間違っていたのでしょうか？_
> 

@row
> ![A figure with nine boxes that line up with three columns, Business, Information, and Technology, and three rows, Direction, Structure, and Execution. Above the boxes is a callout saying "Audit Finding" with an arrow pointing to the boxes. The upper left corner of the boxes has a 1, and the first box in the first column says "CEO." CEO has an arrow pointing to the third box in the first column that is labelled 2 and says "CTO." CTO has an arrow pointing down to the third box in the third column labeled 3 that says "IGA product owner"](/assets/images/idpro_bok/90-image7.png)
> 
> _Figure 7: Amsterdam Information Model - default IAM communication_
> 

@row
> _The product owner is responsible for the IGA system but not for the authorization decisions themselves; the product owner cannot fix the issues found by the auditor. In short, the product owner is responsible but not accountable for authorizations. Instead, the process owner for the financial business process should be tasked with resolving the issue._
> 
> _Note that, based on the Amsterdam Information Model, there is no direct communication between the IGA product owner, who works at the operational level within IT (bottom-right), and the business process owner (center-left) in the business architecture layer. That communication would be a diagonal link and would interfere with regular, well-structured operations._
> 
> _The advice was for the product owner to escalate back vertically to the CTO on the basis of lacking accountability. The CTO should then advise the CEO to assign the issue to a business process owner:_
> 

@column
> _プロダクトオーナーはIGAシステムに責任がありますが、認可の決定自体ではありません；プロダクトオーナーは、監査人が発見した問題を修正できません。端的に言うと、プロダクトオーナーは認可に対して責任がありますが、説明責任はありません。代わりに、財務ビジネスプロセスに対するプロセスオーナーが問題の解決にあたるべきです。_
> 
> _Amsterdam Informationモデルに基づくと、IT部門に属していて運用レベルの仕事をしているIGAプロダクトオーナー（下段右）と、ビジネスアーキテクチャレイヤーのビジネスプロセスオーナー（中段左）の間に直接のコミュニケーションがないことに注意してください。そのコミュニケーションは対角線であり、規則的で正しく構造化された運用を妨げることになります。_
> 
> _プロダクトオーナーに対するアドバイスは、説明責任がないという根拠でCTOに垂直エスカレーションすることでした。そしてCTOはCEOに、ビジネスプロセスオーナーを問題にアサインするように助言すべきです：_
> 

@row
> ![A figure with nine boxes that line up with three columns, Business, Information, and Technology, and three rows, Direction, Structure, and Execution. Above the boxes is a callout saying "Audit Finding" with an arrow pointing to the boxes. The upper left corner of the boxes has a 1, and the first box in the first column says "CEO." CEO has an arrow pointing down to the second box in the first column that is labelled 2 "Process Owner." Process Owner has two arrows, one pointing across to the third column and down one row to 3 "IGA product owner" and a second arrow pointing down one row and over to the third column to the box that says 3 "IGA product owner"](/assets/images/idpro_bok/90-image8.png)
> 
> _Figure 8: Amsterdam Information Model - Correct Communications Path_
> 

@row
> _(Different paths for the necessary communication could be followed to make the required adaptations to the authorization model in the IGA system.)_

@column
> _（IGAシステムにおける認可モデルに必要な適応をおこなうため、必要なコミュニケーションのために異なる経路がたどられることがあります。）_

@row
## The Way Forward

How do these models solve the issue of lack of stakeholdership in organizations? Does the alignment strategy solve the governance challenge?

First and foremost, the theory can demonstrate that access control, or authorization management, is not an IT responsibility. The ‘business’ is accountable for structuring and implementing authorization models and authorization management. IT can, at best, only support the business by implementing the tools that might help.

This makes the implementation of IAM a new challenge. Implementation is not just an IT project. Implementing an identity management solution can be done in an IT project style, but authorization management is not a project. Authorization management is the never-ending responsibility of managers and (business) owners.

And that leads to this conclusion: An IAM project cannot exist as an IT project. Implementing authorization management results in or requires organizational change and is therefore related to regular governance and control of business responsibilities.

Access Governance is what connects the business governance and control challenge to the IT solutions that are used to enable the organization to execute its mission. The easiest way to activate the business is to find someone who makes a decision on the topic of SoD or find someone who is a stakeholder in the approval process for access requests.

> _Case Study: SoD rules_
> 
> _A financial institution is using a modern IGA solution to manage accounts and authorizations in Active Directory and miscellaneous information systems. This system depends on the concept of SoD. Using the SoD controls, it is impossible to assign two or more conflicting roles to the same employee. There are over 1200 SoD rules in the IGA system._
> 
> _When asked who had defined those SoD rules, the product owner in the IT department had no idea. While the product owner is responsible for making sure the system runs as expected, holding them accountable for the SoD rules is outside their area of responsibility; they may not even know all the parties involved in making those decisions._
> 
> _In an ideal world, the SoD rules would not be applied without an accountable business owner clearly identified. In this case, the financial institution has a large business project ahead of them to ensure the appropriate process owners have reviewed each rule._

A good practice would be only to create roles and (business) rules if a person in the business domain can be assigned as the accountable stakeholder for the role or rule. Governance is not just relying on IT departments to solve issues but having someone accountable for managing the business and implementing the controls to manage the business.

@column
## 前進する

これらのモデルは、組織におけるステークホルダーシップの欠如をどのように解決するでしょうか？アライメント戦略はガバナンスの課題を解決するでしょうか？

何よりもまず、この理論はアクセス制御、つまり認可管理がIT部門の責任ではないことを示します。「ビジネス部門」が認可モデルおよび認可管理の構造化と実装に説明責任があります。IT部門は、良くてもビジネス部門を助けるツールを実装することでサポートすることしかできません。

これは、IAMの実装を新たな課題にします。実装はただのITプロジェクトではなくなります。アイデンティティ管理ソリューションの実装はITプロジェクトのスタイルで実施されますが、認可管理はプロジェクトではありません。認可管理はマネージャーと（ビジネス）オーナーの終わりのない責任です。

そして、これは以下の結論を導きます：IMAプロジェクトはITプロジェクトとして存在することができません。認可管理の実装は、組織の変化という結果になるか、それを要求します、つまり定期的なガバナンスとビジネス責任の制御に関連します。

アクセスガバナンスはビジネスガバナンスと制御の課題をITソリューションにつなぐものであり、ITソリューションは組織がそのミッションを実行することができるようにするために利用されます。ビジネスを実現する最も簡単な方法は、SoDのトピックに決定を下す人を探すか、アクセス要求での承認プロセスにおけるステークホルダーを探すことです。

> _ケーススタディ: SoDルール_
> 
> _ある金融機関は現代のIGAソリューションを利用して、Active Directoryとその他の情報システムにおいてアカウントと認可を管理します。このシステムはSoDの概念に依存します。SoD制御を利用することで、2つ以上の競合するルールを同じ従業員に割り当てることが不可能になります。IGAシステムには1200以上のSoDルールがあります。_
> 
> _誰がこれらのSoDルールを定義するか尋ねると、IT部門のプロダクトオーナーはわかっていません。プロダクトオーナーはシステムが期待通りに動作することを保証する責任がある一方で、SoDルールに対する説明責任を有していることは責任の範囲外です；そのような決定をおこなう当事者全員を知らないかもしれません。_
> 
> 理想的な世界では、説明責任があるビジネスオーナーが明確に特定されない限り、SoDルールは適用されません。この場合、金融機関は適切なプロセスオーナーは各ルールをレビューしたことを保証するための大規模なビジネスプロジェクトを有しています。_

グッドプラクティスは、ビジネスドメインの担当者がロールやルールの説明責任を負うステークホルダーとして割り当てられる場合にのみ、ロールや（ビジネス）ルールを作成することです。ガバナンスとは、問題を解決するためにIT部門に依存することではなく、ビジネスを管理し、ビジネスを管理するための制御を実施する説明責任を負う者を持つことです。

@row
## Conclusion

In today’s digital age, for an organization to succeed, it must have a strong IT function. That IT function will not be at its best, however, if it is missing a close partnership with the business components of the organization. The different parts must pull in the same direction to succeed.

IAM projects can only succeed with a strong business-to-IT alignment. As evidenced by the challenges associated with the organization-wide responsibilities around authorization management, IAM, perhaps more than any other IT-related function, must understand the needs of the business and enable those requirements in the identity systems.

Both parties are responsible for ensuring strategic alignment across the organization, being aware of and working to overcome the barriers of different cultures and jargon in each group.

@column
## 結論

今日のデジタル時代において、組織が成功するためには、強力なIT部門を持っていなければなりません。しかし、組織のビジネス部門との緊密な連携が欠けていると、IT部門は最高の力を発揮できないでしょう。成功するためには、異なる部門が同じ方向に引っ張らなければなりません。

IAMプロジェクトは、強力なビジネスITアライメントがあるときだけ成功します。認可管理に関する組織全体の責任に関連した課題からわかるように、IAMはおそらく他のIT関連機能よりも、ビジネスニーズを理解し、アイデンティティシステムで要件を実現しなければなりません。

両者には、組織全体の戦略的アライメントを確保し、各グループの異なる文化や専門用語の障壁を意識し、それを克服するための努力をする責任があります。

@row
## Acknowledgments

The author wishes to thank IDPro Principal Editor Heather Flanagan for turning the original, hardly English language, text fragments into readable text.

@row
## Author Bio

<!-- ![](/assets/images/idpro_bok/90-image9.jpeg) --> André Koot is Principal Consultant at SonicBee in Amsterdam, The Netherlands. He is a member of the BoK committee of IDPro.

André has over 30 years of experience in information security and over 20 years of experience in Identity and Access Management. He has a background in financial accountancy and business economics.

- - -

[^1]:  Cameron, A. & Grewe, O., (2022) “An Overview of the Digital Identity Lifecycle (v2)”, _IDPro Body of Knowledge_ 1(7). doi: [_https://doi.org/10.55621/idpro.31_](https://doi.org/10.55621/idpro.31) 
    
[^2]:  Bago (Editor), E. & Glazer, I., (2021) “Introduction to Identity - Part 1: Admin-time (v2)”, _IDPro Body of Knowledge_ 1(7). doi: [_https://doi.org/10.55621/idpro.27_](https://doi.org/10.55621/idpro.27 ) 
    
[^3]:  Henderson, John C., and N. Venkatraman. "Strategic alignment: a process model for integrating information technology and business strategies." (1989), [https://dspace.mit.edu/bitstream/handle/1721.1/49138/strategicalignme1989hend.pdf](https://dspace.mit.edu/bitstream/handle/1721.1/49138/strategicalignme1989hend.pdf) , and Dampney, C. N. G., & Andrews, T. B. (1989). Striving for sustained competitive advantage: the growing alignment of information systems and business. CSIRO Australia Division of Information Technology. 
    
[^4]:  [https://cve.mitre.org/](https://cve.mitre.org/) 
    
[^5]:  Strategic alignment, Henderson and Venkatraman, 1993, reprint at
    
    [_https://www.researchgate.net/figure/The-Henderson-and-Venkatraman-strategic-alignment-model-Reprinted-from-Henderson-JC\_fig2\_220220710_](https://www.researchgate.net/figure/The-Henderson-and-Venkatraman-strategic-alignment-model-Reprinted-from-Henderson-JC_fig2_220220710) 
    
[^6]:  Amsterdam Information Model, 1999, reprint at [_https://www.researchgate.net/publication/242321998\_A\_Generic\_Framework\_for\_Information\_Management_](https://www.researchgate.net/publication/242321998_A_Generic_Framework_for_Information_Management) 
    
[^7]:  Flanagan (Editor), H., (2022) “Terminology in the IDPro Body of Knowledge”, IDPro Body of Knowledge 1(9). doi: [_https://doi.org/10.55621/idpro.41_](https://doi.org/10.55621/idpro.41) . 
