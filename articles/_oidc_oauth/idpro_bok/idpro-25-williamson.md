---
layout: columns
title: Introduction to Project Management for IAM Projects (v3)
permalink: /docs/oidc_oauth/idpro_bok/25
date: 2024-09-09
modify_date: 2025-05-05
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "ガントチャート", "プロジェクト管理", "アジャイル"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/25/](https://bok.idpro.org/article/id/25/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article serves as an introduction to the practice of project management for an IAM project, describing basic project management terminology and practices. Given the number of systems an IAM project generally impacts, excellent project management is essential for the stakeholders involved.

Keywords: Gantt chart, Project Management, Agile

@column
## 概要

この記事は、IAMプロジェクトのプロジェクトのマネジメントのプラクティスの入門であり、基本的なプロジェクト管理の用語解説とプラクティスについて説明しています。IAMプロジェクトは一般的に影響を与えるシステムが多いため、関係者にとって優れたプロジェクト管理が不可欠です。

Keywords: ガントチャート, プロジェクト管理, アジャイル

@row
By Graham Williamson, Corey Scholefield

© 2022 Corey Scholefield, Graham Williamson, IDPro

_Please visit our [GitHub repository](https://github.com/IDPros/bok) to [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) and comment on this article._

@row
## Importance of Project Management

IAM practitioners may be familiar with the scenario of an IAM project proceeding under the control of an IT systems group without a formal project manager. While this method of deploying a new product or service may be considered an expedient way to get a system installed or updated, it is likely to cost the organization more money in the long term. An IAM service is connected to many critical systems within an organization. Making changes to that service without considering the possible impact on the various connected systems, managing the required resources, or keeping all stakeholders advised of the effort will almost certainly result in a substandard deployment.

Project management has a cost: typically between 5-10% of a project's total expenditure, but it represents the best return compared to any other investment an organization is likely to be afforded.

@column
## プロジェクトマネジメントの重要性

IAMの実務者は、正式なプロジェクトマネージャーを置かずにITシステムグループの管理下でIAMプロジェクトを進めるというシナリオに慣れているかもしれません。新製品やサービスをデプロイするこの方法は、システムをインストールまたは更新するために便利な方法と考えられるかもしれませんが、長期的には組織のコストが高くなる可能性があります。IAMサービスは、組織内の多くの重要なシステムに接続されています。接続されている様々なシステムへの影響の可能性を考慮せず、必要なリソースを管理せず、すべての利害関係者にその取り組みを知らせずに、IAMサービスを変更すると、ほぼ間違いなく標準以下のデプロイとなります。

プロジェクト管理にはコストがかかります：通常、プロジェクトの総支出の5～10%程度ですが、組織が受けられる可能性のある他の投資と比較すると最高のリターンが得られます。

@row
### Terminology

*   Project - a time-limited activity to achieve a defined outcome(s)
    
*   Project Charter - documented authority for the project manager to proceed with a project; it will usually include a succinct statement of the project's purpose.
    
*   Schedule -- a document that defines the activity and resources required to achieve the planned deliverable(s) and outcome(s)
    
*   Gantt Chart - a popular schedule format that displays both activity and timeframes in a single chart
    
*   Project Plan - a document that describes a project; it will usually include a scope statement, schedule, resource plan, communications plan, and quality plan
    
*   Task - lowest-level of defined activity; multiple tasks will typically be grouped into stages or project phases
    
*   Agile project management - a framework that uses a continuous, iterative process to deliver a defined piece of functionality, typically a component of a product or service. Scrum is a popular framework. [^1]
    

Readers interested in pursuing information on project management should review the Project Management Institute (PMI) Framework and the PMI Body of Knowledge for further information. [^2]

@column
### 用語解説

*   プロジェクト - 定義された成果を達成するための期間限定の活動
    
*   プロジェクト憲章 - プロジェクトマネージャーがプロジェクトを進めるための権限を文書化したもの；通常、プロジェクトの目的を簡潔に記述した文章が含まれます。
    
*   スケジュール - 計画された成果物と結果を達成するために必要な活動とリソースを定義した文書
    
*   ガントチャート - 活動と時間枠の両方を1つのチャートに表示する人気のスケジュール形式
    
*   プロジェクト計画 - プロジェクトを説明する文書；通常、スコープステートメント、スケジュール、リソース計画、コミュニケーション計画および品質計画が含まれます
    
*   タスク - 定義された活動の最低レベル；通常、複数のタスクはステージまたはプロジェクトフェーズにグループ化されます
    
*   アジャイルプロジェクト管理 - 継続的で反復的なプロセスを使用して定義済みの機能、通常は製品またはサービスのコンポーネントを提供するフレームワーク。スクラムは人気のあるフレームワークです。 [^1]
    

プロジェクト管理に関する情報を追求することに関心のある読者は、プロジェクト管理協会（PMI）フレームワークとPMI Body of Knowledgeで詳細情報を確認してください。 [^2]

@row
### Characteristics of a Project Manager

In the IT sector, a project manager often has little authority over staff or project stakeholders. They are expected to bring a project in on time and within budget with minimal assistance from upper management and minimal visibility within the organization. In reality, a project manager needs sufficient authority and resources to adequately monitor and manage the project. They also need regular communications with a steering committee consisting of representatives from upper management with the necessary authority to assign resources and remove roadblocks.

Two prime characteristics are essential to a project manager:

|     |     |
| --- | --- |
| Predictability | Management doesn't like surprises. Therefore, a project manager should determine and report on a project's duration and related costs to a defined degree of confidence. |
| Flexibility | Gone are the days when a project manager slavishly follows an approved Gantt chart to the detriment of anyone who wants a change. These days, IT projects will typically undergo several baseline changes during execution to accommodate scope changes, dependencies on other projects, and changes in resource availability. |

Project managers require competence in the five components of project management:

*   Planning
    
*   Organizing
    
*   Resourcing
    
*   Directing
    
*   Controlling
    

@column
### プロジェクトマネージャーの特徴

IT部門では、プロジェクトマネージャーはスタッフやプロジェクトの利害関係者に対してほとんど権限を持たないことがよくあります。彼らは上層部からの支援を最小限に抑え、組織内での可視性を最小限に抑えて、プロジェクトを予定どおりに予算内に収めることが期待されています。実際には、プロジェクトマネージャーには、プロジェクトを適切に監視および管理するための十分な権限とリソースが必要です。また、リソースを割り当て障害を取り除くために必要な権限を持つ上層部の代表者で構成される運営委員会との定期的な連絡も必要です。

プロジェクトマネージャーには、次の2つの主要な特性が不可欠です：

|     |     |
| --- | --- |
| 予測可能性 | 経営陣は驚きが好きではありません。したがって、プロジェクトマネージャーは、プロジェクトの期間と関連するコストを、定義された信頼度で決定し、報告するべきです。 |
| 柔軟性 | プロジェクトマネージャーが承認されたガントチャートに執拗に従い、変更を望む人が不利益を被る時代は終わりました。最近のITプロジェクトでは通常、スコープの変更、他のプロジェクトへの依存関係およびリソースの可用性の変化に対応するために、実行中にいくつかのベースラインの変更がおこなわれます。 |

プロジェクトマネージャーは、プロジェクト管理の5つのコンポーネントの能力を必要とします：

*   計画
    
*   組織化
    
*   リソース管理
    
*   方針指導
    
*   コントロール
    

@row
## PMI Framework

By definition, projects are time-bound; they must have a start and a finish. A major upgrade might be project work if it requires significant resources and coordination of stakeholders. Operational or regular maintenance work is never a project and does not require the skills of a project manager.

Projects are not unexpected; something will instigate the need for a project. Before a project starts, there will be some preparatory work to define the concept and scope for the project.

Between the commencement and completion of a project, there are discrete stages that comprise the project work. It is not until after project completion that the deliverable will enter an operational status and become business as usual.

@column
## PMIフレームワーク

定義によれば、プロジェクトには期限があります；プロジェクトには開始と終了がなければなりません。大規模なアップグレードをおこなう場合、多大なリソースと利害関係者の調整が必要であれば、プロジェクト作業となる可能性があります。運用や定期的なメンテナンスはプロジェクトではなく、プロジェクトマネージャーのスキルも必要ありません。

プロジェクトは予期せぬものではありません；何かがきっかけとなってプロジェクトの必要性が生じます。プロジェクトが始まる前、プロジェクトのコンセプトやスコープを定義するための準備作業があります。

プロジェクトの開始から完了までの間に、プロジェクト作業を構成する個別の段階があります。成果物が運用状態に入り、通常通りの業務になるのは、プロジェクト完了後です。

@row
![Diagram showing the basic project lifecycle, from Concept to Planning to Execution to Operations. ](/assets/images/idpro_bok/PM-figure1.png)

Figure - The Project Lifecycle

@row
### Concept

Projects come out of a need. In the IAM world, examples of such a need include reducing costs and improving security by using identity information more effectively for onboarding and offboarding staff or a need for an enterprise LDAP directory upgrade. Such projects are typically initiated by an IT resource rather than a business resource, though a line-of-business resource might also initiate a project (e.g., to move an application from an on-premises environment to the cloud to save capital expenditure budget). The project sponsor will communicate the requirement, set the project charter, and evaluate the required activity's cost and duration. The sponsor will typically fund this stage and then engage a project manager to complete the planning stage.

@column
### 概念

プロジェクトはニーズから生まれます。IAMの世界ではこのようなニーズの例として、スタッフのオンボーディングとオフボーディングにアイデンティティ情報をより効果的に使用することによるコストの削減とセキュリティの向上や、エンタープライズLDAPディレクトリのアップグレードなどが挙げられます。このようなプロジェクトは、通常、ビジネスリソースではなくITリソースによって開始されますが、ビジネス部門のリソースがプロジェクトを開始することもあります（たとえば、資本支出予算を節約するために、アプリケーションをオンプレミス環境からクラウドに移行する場合など）。プロジェクトスポンサーは要件を伝え、プロジェクト憲章を設定し、必要な活動のコストと期間を評価します。通常、スポンサーはこの段階で資金を調達し、その後、プロジェクトマネージャーを起用して計画段階を完了させます。

@row
### Planning Stage

Once the approval to proceed has been received, the project manager will engage with the stakeholders to define the project scope. Having a clear scope around an IAM project is critical to its success. Since IAM touches virtually every application in a company and is at the core of cybersecurity protection processes, the scope can quickly expand beyond the original intent and budget if not managed carefully. As participation by one or more representatives of each relevant application is required, the project scope will also define the stakeholders. For instance, if the Finance Administration application is to be integrated with the IAM system, a representative from the Finance Department must be engaged as a stakeholder in the project.

A project initially focused on deploying an identity management package to provision staff—for example, establishing Active Directory records and email accounts—might see a request for including provisioning into corporate applications. Or someone in Corporate Governance may request additional functionality such as periodic attestation reporting and re-certification. The project manager must ensure that the appropriate stakeholders are engaged and respond to requests for input. The project manager does not decide whether requested functionality should be included; that decision is made via a Steering Committee or project sponsor and reviewed when the full scope of the project is defined.

Once the scope has been determined, the project manager will engage subject matter experts to quantify the work required and construct the project budget and schedule. The planning stage will develop a project plan that will include:

|     |     |
| --- | --- |
| Schedule | The schedule will define the timeframe and resources required for the project to calculate the cost. A schedule is typically expressed via a Gantt chart in classic project management. A high-level Gantt chart is also helpful for Agile project management. |
| Stakeholder Analysis | The project manager will construct a list of project stakeholders. This list will typically include the sponsor, finance manager, human resources (HR) manager, system owners, and representatives from the IT groups that will be engaged in the project. |
| Resource Plan | A basic tenet of project management is that the desired resources are never available; they are typically fully engaged in other activities. The project manager must negotiate with the appropriate stakeholders to get the desired resources assigned and alter the project schedule accordingly. |
| Communications Plan | The project communications plan defines the "who" and the "how" for a project manager to report on project progress. The project team will likely have a file folder, wiki, or SharePoint site for the project. The project manager will regularly email a project report to the Stakeholders and send meeting agendas and status summaries to the steering committee before the project review meetings. The project plan should include a communications register that logs all communications with the stakeholders and within the project team. |
| Quality Management | A mechanism to ensure adequate quality in project deliverables should be defined. This mechanism should include management reviews of project documentation and properly constructed test and release procedures. |
| Risk Management | A project manager constructs a risk register that identifies the anticipated risks, quantifies them in terms of probability and impact, and includes appropriate risk mitigation activities. |

At the end of the planning stage, there should be a good understanding of the project activities, timeframe, and cost. Typically, the project cost and duration will be known within a 10% margin.

In terms of time and money, this understanding of project costs allows the organization to make an informed decision as to whether they want to dedicate the necessary resources to a project. A decision not to proceed with a project is as successful an outcome for a project manager as a decision to proceed. It means that the organization has been spared the expenditure of resourcing a project that might otherwise have proceeded, only to be prematurely terminated when the costs blow out, resulting in associated sunk costs.

@column
### 計画段階

プロジェクトの進行が承認されると、プロジェクトマネージャーはステークホルダーと協力して、プロジェクトのスコープを定義します。IAMプロジェクトのスコープを明確にすることは、プロジェクトの成功に不可欠です。IAMは企業内のほぼすべてのアプリケーションに関わり、サイバーセキュリティ保護プロセスの中核であるため、慎重に管理しなければ、スコープが当初の意図と予算を超えて急速に拡大する可能性があります。関連する各アプリケーションの1人以上の代表者が参加する必要があるため、プロジェクトスコープによって利害関係者も定義されます。例えば、財務管理アプリケーションをIAMシステムに統合する場合、財務部門の代表者をプロジェクトの利害関係者として参加させなければなりません。

Active Directoryのレコードと電子メールアカウントの確立など、当初はスタッフのプロビジョニングのためのアイデンティティ管理パッケージの導入に重点を置いていたプロジェクトが、企業アプリケーションへのプロビジョニングを含めるように要求されることがあります。あるいは、コーポレートガバナンスの担当者が、定期的な認証レポートや再認定などの追加機能を要求するかもしれません。プロジェクトマネージャーは、適切な利害関係者が関与し、インプットの要求に応じるようにしなければなりません。プロジェクトマネージャーは、要求された機能が含まれるべきかを決定しません；その決定は、運営委員会またはプロジェクトスポンサーを通じておこなわれ、プロジェクトの全スコープが定義された時点で見直されます。

スコープが決まったら、プロジェクトマネージャーは専門家を交えて必要な作業を数値化し、プロジェクトの予算とスケジュールを組み立てます。計画段階では、以下のようなプロジェクト計画を策定します:

|     |     |
| --- | --- |
| スケジュール | コストを算出するために、スケジュールはプロジェクトに必要な機関とリソースを定義します。古典的なプロジェクトマネジメントでは、スケジュールは一般的にガントチャートで表現されます。アジャイルプロジェクトマネジメントでも、ハイレベルなガントチャートが役に立ちます。 |
| ステークホルダー分析 | プロジェクトマネージャーは、プロジェクトのステークホルダーのリストを作成します。このリストには、スポンサー、財務マネージャー、人事（HR）マネージャー、システムオーナー、プロジェクトに携わるITグループの代表者などが含まれるのが一般的です。 |
| リソース計画 | プロジェクトマネジメントの基本的な考え方として、望んでいるリソースは絶対に確保できないということです；望んでいるリソースは通常、他の活動に完全に従事しています。プロジェクトマネージャーは、適切なステークホルダーと交渉して、望むリソースを割り当て、それに応じてプロジェクトのスケジュールを変更しなければなりません。 |
| コミュニーケーション計画 | プロジェクトコミュニケーション計画では、プロジェクトマネージャーがプロジェクトの進捗を「誰に」「どのように」報告するのかを定義します。プロジェクトチームは、プロジェクト用のファイルフォルダ、Wiki、またはSharePointのサイトを持つことになるでしょう。プロジェクトマネージャーは、ステークホルダーに定期的にプロジェクトレポートをメールし、プロジェクトのレビューミーティングの前にミーティングの議題とステータスのサマリーを運営委員会に送信します。プロジェクト計画には、ステークホルダーとプロジェクトチーム内のすべてのコミュニケーションを記録するコミュニケーションレジスターを含めるべきです。 |
| 品質管理 | プロジェクトの成果物において適切な品質を確保するためのメカニズムを定義する必要があります。このメカニズムには、プロジェクト文書のマネジメントレビューや、適切に構築されたテストおよびリリース手順を含むべきです。 |
| リスクマネジメント | プロジェクトマネージャーは、予想されるリスクを特定し、確率と影響の観点から定量化し、適切なリスク軽減活動を含むリスクレジスターを構築します。 |

計画段階の最後では、プロジェクトの活動、期間およびコストを十分に理解するべきです。通常、プロジェクトのコストと期間は10%以内ののマージンがあります。

時間とお金の面では、このようにプロジェクトのコストを理解することで、組織が必要なリソースをプロジェクトに専念させたいかどうかについて十分な情報に基づいた決定を下すことができます。プロジェクトを続行しないという決定は、プロジェクトマネージャーにとっては、続行するという決定と同じくらい成功した成果です。これは、コストが吹き飛んで早々に打ち切られ、関連するサンクコストが発生するだけだった本来であれば進められていたはずのプロジェクトにリソースを投入する費用を、組織が節約できたことを意味します。

@row
### Deployment Stage

The project deployment stage will vary depending on how the project is managed: via a classic (waterfall) mechanism or an Agile project management approach.

@column
### デプロイ段階

プロジェクトのデプロイ段階は、プロジェクトの管理方法、つまり古典的な（ウォーターフォール）の仕組みまたはアジャイルプロジェクトアプローチによって変わります。

@row
#### Classic

In classic project management, the project manager will manage all project activities according to a detailed schedule that shows all the individual tasks, assigned resources, and duration. They will also schedule a regular project team meeting to review the project’s progress against the schedule and note any impediment to be escalated to the steering committee for resolution.

At the Steering Committee meeting, the committee will formally accept the project deliverables, approve the phases, and resolve any issues or roadblocks that the project manager identifies. Again, the project manager cannot extend the project scope, schedule, or budget without Steering Committee approval.

The components of a classically managed project are:

|     |     |
| --- | --- |
| Team meetings | The project team should hold regular progress-review meetings (weekly or bi-weekly). These meetings allow everyone to mark progress against the Gantt chart and determine what issues, if any, must be escalated to the steering committee. |
| Steering committee | The project manager will periodically present to the steering committee to review progress on the project schedule and act on any issues the team has identified. The project status report should include the progress made since the last meeting, any issues to be resolved by the steering committee, and the planned activities for the next period. |
| Phase transitions | The project schedule (Gantt chart) will show the project's phases. At the end of each phase, the steering committee will review the deliverables for that phase and determine whether a phase transition can be approved. |
| Deliverable acceptance | Each project deliverable should be formally accepted. This acceptance will typically involve the appropriate stakeholder(s) who must agree that the deliverable has been produced to an adequate quality level. |
| Project closure | A project should always include a proper project closure procedure. This procedure will typically involve a formal project review that will document the activities that went well and any learnings from the project. "Those who don't learn from history are doomed to repeat it." |

@column
#### 古典的

古典的なプロジェクト管理では、プロジェクトマネージャーはすべての個々のタスク、割り当てられたリソースおよび期間を示す詳細なスケジュールに従って、すべてのプロジェクト活動を管理します。また、定期的なプロジェクトチームミーティングをスケジュールして、スケジュールに対するプロジェクトの進捗状況を確認し、解決のために運営委員会にエスカレーションする障害を記載します。

運営委員会の会議で、委員会はプロジェクトの成果物を正式に受け入れ、フェーズを承認し、プロジェクトマネージャーが特定した問題や障害を解決します。また、プロジェクトマネージャーは運営委員会の承認なしに、プロジェクトのスコープ、スケジュールまたは予算を拡張することはできません。

古典的に管理されているプロジェクトのコンポーネントは：

|     |     |
| --- | --- |
| チームミーティング | プロジェクトチームは、定期的に（毎週または隔週で）進捗確認ミーティングを開催すべきです。このミーティングでは、全員がガントチャートに対する進捗をマークし、もし問題があれば運営委員会にエスカレーションする必要があることを決定することができます。 |
| 運営委員会 | プロジェクトマネージャーは、プロジェクトスケジュールの進捗状況を確認し、チームが認識した問題点に対処するために、定期的に運営委員会に報告します。プロジェクト状況報告には、前回の会議以降の進捗状況、運営委員会で解決すべき問題点、次期の活動計画などを記載します。 |
| フェーズの遷移 | プロジェクトのスケジュール（ガントチャート）には、プロジェクトのフェーズが表示されます。各フェーズ終了時に、運営委員会でそのフェーズの成果物を確認し、フェーズ移行が承認されるかどうかを判断します。 |
| 成果物受入 | プロジェクトの各成果物は、正式に受け入れられるべきです。この受入には、通常、適切なステークホルダーが関与し、成果物が適切な品質レベルで作成されたことに合意しなければなりません。 |
| プロジェクト終了 | プロジェクトには、常に適切なプロジェクト終了手順があるべきです。通常、この手順では正式なプロジェクトレビューが含まれ、うまくいった活動やプロジェクトからの学びを文書化します。「歴史から学ばない者は、それを繰り返す運命にある。」 |

@row
#### Agile

Many organizations have now adopted Agile project management for smaller projects that don’t warrant the cost of a classic project management approach. These projects are typically an activity that exceeds the capacity of the normal operations staff. For instance, a significant upgrade, or migration to cloud services, will likely require a system outage or out-of-hours cutover activity. The execution of such project work must be managed. Agile project management ensures appropriate stakeholders are engaged and issues are addressed promptly, without waiting for steering committee approval.

Agile methodology divides a project into ‘scrums’ that are then further divided into ‘sprints.’ Each activity comprising a sprint will be put up in a tile on the project wall and will be moved from the "To Do" activity list to "In Progress" and then to "Done." A review meeting, sometimes called a "stand-up," will be held every few days to review current activity and document any issues or roadblocks.

|     |     |
| --- | --- |
| Project wall | The essence of Agile project management is visibility. The Project Wall provides a physical or virtual place where the project team can view the completed, current, and waiting tasks and resource assignments. |
| Sprints & Scrum | These terms are used differently depending upon the context. Scrum is a framework that uses an iterative process to deliver a defined piece of functionality. It could be a product, service, or a new piece of functionality for an existing product (e.g., deploy a DBMS connector to the IAM environment). A sprint usually describes a scrum component, a time-limited activity that contributes to a scrum deliverable (e.g., 30 days for developing the reporting module). |
| Deliverable acceptance | One area that can suffer when using an Agile project management approach is reviewing and accepting deliverables. Acceptance testing will verify that the requirements established for a viable product have been achieved and are demonstrable. A sprint team sometimes advises on completing a piece of work and moves to the next without formal acceptance of the deliverable. A mechanism to record the acceptance of a module or deliverable is needed. |
| Project closure | A team meeting can be dedicated to the requisite project review in a classically managed project. It is sometimes difficult to manage the project closure in an Agile project, in which many participants have contributed to the outcome. In either project management model, a mechanism is required for all participants to agree that a project has been completed and that the resources used can be reassigned. |

@column
#### アジャイル

多くの組織は現在、古典的なプロジェクト管理アプローチのコストを保証しない小規模なプロジェクトにアジャイルプロジェクト管理を採用しています。一般的にこれらのプロジェクトは、通常の運用スタッフの能力を超える活動です。例えば、大幅なアップグレードやクラウドサービスへの移行には、システムの停止や時間外カットオーバーアクティビティが必要になる可能性があります。このようなプロジェクト作業の実行は管理されなければなりません。アジャイルプロジェクト管理により、運営委員会の承認を待たずに、適切な利害関係者が関与し、問題が迅速に対処されます。

アジャイル方法論は、プロジェクトを「スクラム」に分け、さらに「スプリント」に分けます。スプリントを構成する各アクティビティは、プロジェクトウォールにタイルに貼られ、「To Do」アクティビティリストから「In Progress」、そして「Done」に移します。「スタンドアップ」と呼ばれることもあるレビューミーティングはを数日おきに開催し、現在のアクティビティをレビューし、問題や傷害があれば文書化します。

|     |     |
| --- | --- |
| プロジェクトウォール | アジャイルプロジェクト管理の本質は可視性です。プロジェクトウォールは、プロジェクトチームが完了、進行中、待機中のタスクとリソース割り当てを閲覧できる物理的または仮想的な場所を提供します。 |
| スプリント＆スクラム | これらの用語は、文脈に応じて使われ方が異なります。スクラムはイテレーティブなプロセスを使用して定義された機能を提供するフレームワークです。これは、製品、サービスまたは既存の製品の新しい機能（DBMSコネクタをIAM環境にデプロイするなど）である可能性があります。スプリントは通常、スクラムコンポーネント、スクラム成果物に貢献する期間限定のアクティビティ（レポートモジュールの開発に30日など）を表します。 |
| 成果物受入 | アジャイルプロジェクト管理アプローチを使用するときに苦しむ可能性がある領域の1つは、成果物のレビューと受入です。受入テストでは、実用最小限の製品に対して確立された要件が達成され、実証可能であることを検証します。スプリントチームは、成果物を正式に受け入れることなく、作業の完了についてアドバイスし、次の作業に移動する場合があります。モジュールまたは成果物の受入を記録するメカニズムが必要です。 |
| プロジェクト終了 | チームミーティングは、古典的に管理されたプロジェクトで必要なプロジェクトレビュー専用にすることができます。多くの参加者が結果に貢献しているアジャイルプロジェクトでは、プロジェクトの終了を管理することが難しい場合があります。どちらのプロジェクト管理モデルでも、すべての参加者がプロジェクトが完了し、使用されたリソースを再割り当てできることに同意するためのメカニズムが必要です。 |

@row
## PMO Issues

In large organizations with a Project Management Office (PMO), an IAM project must follow corporate procedures. Typically, a PMO will have defined gating factors, or ‘gates,’ through which all projects must pass. For instance, there will normally be a project approval gate in which the appropriate managers will review the project plan and indicate their approval. There will usually be a gate in the form of a budget review to approve the assignment of resources. Similarly, there might be a gate in the form of an architecture review to approve the solution architecture. Finally, the governance outcomes should be reviewed as a necessary gate for the project. The PMO should orchestrate all these activities.

One of the benefits of a PMO is the visibility it gives to projects within an organization. This visibility is beneficial to the IAM team; it allows them to ensure any projects with an identity component are properly identified and accommodated in the appropriate work program. For instance, if an authentication gateway is being installed, any application undergoing development should be modified to use the gateway rather than maintaining LDAP lookups. Without a PMO, it is sometimes difficult for the IAM team to impact projects.

A PMO provides the opportunity to educate project managers on identity issues and to insert IAM requirements into IT projects within an organization. A project manager will use the PMO framework to:

1.  manage the project through the project gates;
    
2.  communicate the project's progress to the organization's management;
    
3.  gain acceptance within the organization that the project goals were achieved within the approved budget and schedule.
    

@column
## PMOの仕事

プロジェクトマネジメントオフィス（PMO）を持つ大規模な組織では、IAMプロジェクトは会社の手続きに従わなければなりません。通常、PMOにはすべてのプロジェクトが通過しなければならないゲーティング要素または「ゲート」と呼ばれるものが定義されています。例えば、通常、プロジェクト承認ゲートがあり、適切な管理者がプロジェクト計画をレビューし、承認を示します。通常、リソースの割り当てを承認するための予算審査という形のゲートがあります。同様に、ソリューションアーキテクチャを承認するために、アーキテクチャレビューの形でゲートがあるかもしれません。最後に、プロジェクトに必要なゲートとして、ガバナンスの成果をレビューすべきです。PMOはこれらすべての活動を指揮すべきです。

PMOの利点の1つは、組織内のプロジェクトに可視性を与えることです。この可視性はIAMチームにとって有益です；IAMチームは、アイデンティティコンポーネントを持つプロジェクトを適切に識別され、適切な作業プログラムに適合するようにできます。たとえば、認証ゲートウェイをインストールする場合、開発中のアプリケーションはLDAPルックアップを維持するのではなく、ゲートウェイを使用するように変更するべきです。PMOがない場合、IAMチームがプロジェクトに影響を与えることは難しい場合があります。

PMOは、アイデンティティに関する問題についてプロジェクトマネージャーを教育し、組織内のITプロジェクトにIAM要件を追加する機会を提供します。プロジェクトマネージャーは、PMOのフレームワークを使用して次のことをおこないます：

1.  プロジェクトゲートを通じてプロジェクトを管理します；
    
2.  プロジェクトの進捗を組織の経営陣に伝えます；
    
3.  プロジェクトのゴールが承認された予算とスケジュールの中で達成されたことを組織内で承認します。
    

@row
## IAM Projects

It’s often said that a good project manager can keep a project on track regardless of the topic. While this may be true, if a project manager for an IAM project is not competent in the subject, they will be disadvantaged. It is recommended that they engage a project lead who is familiar with the components of an IAM environment and understands the competency of the skills-base within the organization. If an organization cannot complete a project with in-house resources, the project manager will need to engage contractors to work on the project.

@column
## IAMプロジェクト

優秀なプロジェクトマネージャーは、トピックにかかわらずプロジェクトを軌道に乗せられるとよく言われています。これは真実かもしれませんが、IAMプロジェクトのプロジェクトマネジャーはその主題に精通していない場合、不利になります。IAM環境のコンポーネントに精通し、組織内のスキルベースの能力を理解しているプロジェクトリーダーを採用することを推奨します。組織が社内のリソースでプロジェクトを完了できない場合、プロジェクトマネージャーはプロジェクトに取り組む契約業者を雇用する必要があります。

@row
### Example Project

Let’s assume the project is commenced to replace the existing IAM processes used to onboard new staff members or contractors with a new system purchased from an IAM solution vendor. The sections below work through the different project management stages for such a project.

@column
### プロジェクトの例

例えば、新しいスタッフや契約業者がオンボードする際に使用する既存のIAMプロセスを、IAMソリューションベンダーから購入した新しいシステムに置き換えるプロジェクトが開始されたと仮定しましょう。以下のセクションでは、このようなプロジェクトのさまざまなプロジェクト管理の段階を説明します。

@row
### Planning

The single most important element to define for an IAM project is the project scope. The IAM environment touches so many operational components and processes within an organization; the PM's role means they must clearly communicate to all stakeholders the full scope of the project. To properly determine the scope of an IAM project requires the PM to understand the nature of the IAM solution and its impact on other systems in the organization. The [Addendum](#addendum-questions-for-an-iam-project-manager-to-ask) suggests some questions that should be asked in the planning phase of an IAM project.

The PM is responsible for ensuring the scope of the project is clear. Too many IAM projects proceed with misunderstandings regarding the project scope. The IAM project lead, for example, might think the project is to implement a provisioning module, whereas the application owner might think the goal is to provide better authentication functionality. The auditor, in turn, might want improved governance. Reaching a common agreement on the scope will focus all stakeholders on the extent of the project.

The following items are often inside the scope of a project of this nature:

*   configuring and deploying the IAM tool
    
*   integrating with the email system
    
*   integrating with the system(s) that provide enterprise resource planning (ERP) functions (i.e., the computer systems that support the organization's operations)
    

The HR and financial management systems, however, are out of scope of this example project. While tight integration with HR could improve both the HR and IAM systems—the HR system potentially able to increase its span of control, and the IAM system benefitting from tight integration with HR for better provisioning of staff entitlements (e.g., training status, project membership, and employment status of staff)—the HR department is often reticent to make any changes to their onboarding and offboarding procedures. Evidence of a well-managed project may alleviate this fear.

The Finance department also has challenges that discourage them from agreeing to anything that will impact their systems. They typically maintain a fine-grained authentication capability within the financial management system and often distrust any external entity’s capability to do this. Externalizing access control to the IAM system will typically be less expensive and improve security, but working with Finance will require its own focused effort.

In scope will be the applications that will rely on the IAM system. The PM must communicate with each system's owners and determine what data attributes are required for users accessing each system. For example, the email system will need to know a user’s first and last names and, likely, middle initial, to construct their digital identifier correctly. It might also need to know their department or group memberships. Ideally, email systems should participate in a company’s single-sign-on (SSO) solution, i.e., users will be authenticated as part of the SSO solution used in the organization.

The computer applications that provide operational functionality to users should also use the organization’s SSO solution. In the real world, such applications might include a production machine, a process control system, an asset control system, a learning management system, a health monitoring facility, a vehicle registration application, and so on. Any computer system that must be protected via an access control mechanism that ensures users only get access to the facilities to which they are entitled should be integrated into the organization’s SSO solution. The project manager for an IAM project must ensure the requirements for these applications are canvassed at the commencement of the project.

@column
### 計画

IAMプロジェクトで最も重要なのは、プロジェクトのスコープを定義することです。IAM環境は、組織内の多くの運用コンポーネントやプロセスに関わります；PMの役割は、すべての利害関係者にプロジェクトの全範囲を明確に伝える必要があります。IAMプロジェクトの範囲を適切に決定するために、PMはIAMソリューションの性質と、組織内の他のシステムへの影響を理解する必要があります。[付録](#addendum-questions-for-an-iam-project-manager-to-ask)では、IAMプロジェクトの計画段階でおこなうべき質問をいくつか示しています。

PMは、プロジェクトのスコープが明確にする責任があります。あまりにも多くのIAMプロジェクトが、プロジェクトのスコープに関して誤解を抱えたまま進行しています。例えば、IAMプロジェクトのリーダーは、プロジェクトがプロビジョニングモジュールを実装することだと思っているかもしれませんが、アプリケーションオーナーはより優れた認証機能を提供することが目標だと思っているかもしれません。一方、監査役はガバナンスの強化を望んでいるかもしれない。スコープについて共通の合意を得ることで、すべての利害関係者がプロジェクトのスコープに集中できます。

このような性質のプロジェクトのスコープには以下の項目が含まれることが多いです：

*   IAMツールの設定とデプロイ
    
*   Eメールシステムとの統合
    
*   エンタープライズリソースプランニング（ERP）機能（つまり、組織の運用をサポートするコンピュータシステム）を提供するシステムとの統合
    

しかし、HRシステムと財務管理システムは、この例のプロジェクトのスコープ外です。HRシステムとの緊密な統合により、HTシステムとIAMシステムの両方が改善される可能性があります。HRシステムは制御範囲を拡大できる可能性があり、IAMシステムはスタッフの資格（トレーニング状況、プロジェクトメンバー、スタッフの雇用状況など）のより適切なプロビジョニングのためのHRシステムとの緊密な結合によってメリットが得られます。人事部はオンボードとオフボードの手順を変更することに消極的な場合が多いのです。プロジェクトが適切に管理されていることを示す証拠があれば、このような懸念は解消されるかもしれません。

財務部にも、システムに影響を与えるものに賛成することを思いとどまらせる課題があります。一般的に彼らは財務管理システム内にきめ細かな認証機能を維持しており、しばしば外部エンティティの機能を信頼していません。IAMシステムへのアクセス制御を外部化することは一般的に安価でセキュリティが向上しますが、一方で財務部と連携するには独自の集中的な取り組みが必要になります。

スコープにはIAMシステムに依存するアプリケーションが含まれます。PMは各システムのオーナーと連絡を取り、ユーザが各システムにアクセスするさいに必要なデータ属性を決定しなければなりません。例えば、Eメールシステムはデジタルアイデンティティを正しく構築するため、ユーザの氏名、ミドルネームの頭文字を知る必要があります。また、ユーザの部署やグループも把握する必要があるかもしれません。理想的には、Ｅメールシステムは企業のシングルサインオン（SSO）ソリューションに参加するべきであり、つまり、ユーザは組織で使用されるSSOソリューションの一部として認証されます。

ユーザに運用機能を提供するコンピュータアプリケーションでも、組織のSSOソリューションを利用すべきです。現実世界でもそのようなアプリケーションには、生産機械、プロセス管理システム、資産管理システム、学習管理システム、健康管理施設、車両登録アプリケーション等が含まれるでしょう。ユーザが資格をもつ施設にのみアクセスできるようにするアクセス管理システムを介して保護しなければならないコンピュータシステムは組織のSSOソリューションに統合されるべきです。IAMプロジェクトのプロジェクトマネージャーは、プロジェクトの開始時にこれらのアプリケーションの要件を確認する必要があります。

@row
### Organizing

The success of an IAM project depends on how well it is organized. This dependency relates to how well the PM utilizes the hierarchy within the organization. Often, the execution of an IAM project is left to the people in the IAM unit within the company. This is poor practice because the IAM unit has an operational role in maintaining the IAM environment; an IAM project, however, is a time-limited initiative that will stretch the ability of the IAM unit and divert resources from their task of managing the IAM environment. While personnel with IAM experience should be involved in the deployment project, if they are seconded from the IAM unit, they should be backfilled with other personnel while they are engaged in the IAM project.

The following activities are recommended for the successful ‘organizing’ of an IAM project:

*   Establish a steering committee – this should include the project sponsor, appropriately high-level personnel in the IT department, HR, Finance, Manufacturing, Sales & Marketing, and any other business unit directly impacted by the project. A steering committee will periodically review the project’s progress and resolve any issues raised by the PM.
    
*   Hold appropriate committee reviews – the PM must be aware of all gating factors and committees that must review the project’s progress. These will include the PMO’s gating (phase exit) meetings, governance reviews to ensure audit compliance, enterprise architecture committees ensuring that IAM systems comply with supported technology platforms, and finance reviews ensuring budget support for the project.
    
*   Document a communications register – this should list to whom and via what mechanism the PM will send their project progress reports. It should include the frequency (e.g., bi-weekly), the mechanism (e.g., email, website, or other notification tools), and the media (e.g., Word document, MS Project file, etc.).
    
*   Verify the support of a Quality Assurance (QA) program – responsible for the quality of project deliverables (such as the documents, milestones, or other deliverables). This program is particularly important to establish the accuracy (both in format and content) of the data files supporting the test plan. Identity data should be suitably anonymized for test purposes and must be restorable for regression testing.
    
*   Create a risk register - The project team should compile a risk register that identifies the risks to the project’s ability to meet its schedule, cost, and quality constraints. Each risk should be assessed for probability and impact. An IAM project should not proceed with any risk evaluated as ‘high.’
    

@column
### 組織化

IAMプロジェクトの成功は、プロジェクトがいかによく管理されているかに依存します。この依存は、PMが組織内のヒエラルキーをどれだけうまく活用しているかに関係しています。しばしば、IAMプロジェクトの実行は社内のIAM部門の人々に任されています。IAM部門にはIAM環境を維持する運用上の役割があるため、良い方法ではありません；しかし、IAMプロジェクトはIAM部門の能力を拡張し、IAM環境の管理タスクからリソースを転用する期間限定の新しい取り組みです。IAMの経験をもつ担当者はデプロイプロジェクトに関与するべきですが、その担当者がIAM部門から配置換えされていた場合、担当者がIAMプロジェクトに従事する間に他の担当者で埋め合わせするべきです。

以下のアクティビティは、IAMプロジェクトの成功した「組織化」のために推奨されます:

*   運営委員会を設立する - これにはプロジェクトスポンサー、プロジェクトに直接影響を受けるIT部門、HR部門、財務部門、生産部門、販売営業部門および他のビジネス部門の適切な高レベルの担当者に含まれるべきです。運営委員会は定期的にプロジェクトの進捗状況をレビューし、PMによって提起された問題を解決します。

*   適切な委員会のレビューを開催する - PMはすべてのゲーティング要素とプロジェクトの進行状況をレビューしなければならない委員会を認識しなければなりません。これらはPMOのゲーティング（フェーズ終了）ミーティング、監査コンプライアンスを確保するためのガバナンスレビュー、IAMシステムがサポートされているテクノロジープラットフォームに準拠していることを確認するエンタープライズアーキテクチャ運営委員会、プロジェクトの予算サポートを確保するための財務レビューが含まれます。
    
*   コミュニケーション登録簿を文書化する - PMがプロジェクトの進捗報告を誰に、どのような方法で送るかをリストアップします。これは、頻度（例えば、隔週）、メカニズム（例えば、電子メール、ウェブサイトまたは他の通知ツール）、およびメディア（例えば、Word文書、MSプロジェクトファイルなど）を含むべきです。
    
*   品質保証（QA）プログラムのサポートを検証する - プロジェクトの成果物（文書、マイルストーン、またはその他の成果物など）の品質に責任を負います。このプログラムは、テスト計画をサポートするデータファイルの正確さ（形式と内容の両方）を確立するために特に重要です。アイデンティティデータは、テスト目的のために適切に匿名化されるべきであり、回帰テストのために復元可能でなければなりません。
    
*   リスク登録簿の作成 - プロジェクトチームは、プロジェクトのスケジュール、コスト、品質の制約を満たす能力に対するリスクを特定するリスク登録簿をコンパイルするべきです。各リスクは、確率と影響を評価するべきです。IAMプロジェクトは、リスクが「高い」と評価された状態で進めるべきではありません。
    

@row
### Resourcing

It’s a project management maxim that the preferred resources are never available. Good staff are very busy and cannot be easily seconded to a project. In an IAM project, it is essential that personnel with detailed knowledge of the company’s identity management systems and policies be involved. The PM must be able to negotiate the availability of critical personnel and modify the project schedule accordingly.

As noted above, the project’s budget must accommodate backfilling personnel seconded to the project. If it is necessary to ’buy in’ resources, the steering committee will typically decide on the final resourcing plan and may choose to use contractors for the maintenance activity and assign experienced IAM staff to the IAM deployment project. Since the PM of an IAM project typically has no functional authority within the organization, they must use the steering committee to get the right resources assigned to the project at the right time.

A perennial problem for an IAM project is how to build IAM staff competence in a new IAM tool being acquired. The options include:

*   Send selected staff from the IAM unit for training prior to the deployment activities
    

> It is unrealistic to expect, even experienced, IAM staff to develop competence in the new package without hands-on experience.

*   Engage the vendor to do the deployment with IAM staff observing.
    

> This engagement is the most realistic option because it puts some onus on the vendor to ‘make it work’ and ensure technology transfer to the IAM staff.

*   Engage the vendor for a turn-key project with the IAM unit engaged to undertake acceptance testing on the transition to operational status.
    

> This engagement is not ideal since, without the IAM team's active involvement, the IAM solution's successful integration into the organization’s operations will be difficult.

@column
### リソース管理

プロジェクトマネジメントの格言に、「望ましいリソースは決して手に入らない」というのがあります。優秀なスタッフは非常に多忙であり、簡単にプロジェクトに出向くことはできません。IAMプロジェクトでは、企業のアイデンティティ管理システムやポリシーについて詳しい知識を持つ人材の参画が不可欠です。PMは、重要な人材の入手可能性を交渉し、それに応じてプロジェクトのスケジュールを修正する能力がなければなりません。

前述のとおり、プロジェクトの予算は、プロジェクトに出向している人員の埋め戻しに対応する必要があります。リソースを「買い入れる」必要がある場合、通常、運営委員会が最終的なリソーシングプランを決定し、保守活動には請負業者を使用し、IAMデプロイプロジェクトには経験豊富なIAMスタッフを配置することを選択できます。IAMプロジェクトのPMは、通常、組織内の職務権限を持たないため、運営委員会を利用して適切なリソースを適切なタイミングでプロジェクトに割り当てなければなりません。

IAMプロジェクトの永続的な問題は、獲得される新しいIAMツールでIAMスタッフの能力をどのように構築するかです。次のオプションがあります：

+   デプロイ活動に先行し、IAM部門から選抜したスタッフをトレーニングに向かわせます
    

> 経験のあるIAMスタッフであっても、ハンズオン経験なしに新しいパッケージで能力を開発することに期待することは非現実的です。

*   IAMスタッフが監視しながらデプロイを実施するベンダーを雇用します。
    

> この雇用は、ベンダーに「機能させる」責任を負わせ、IAMスタッフへの技術移転を確実にするため、最も現実的なオプションです。

*   IAM部門が運用状態への移行において受け入れテストを実行するターンキープロジェクトのためにベンダーを雇用します。
    

> この雇用は、IAMチームの積極的な関与がなければIAMソリューションを組織の運用にうまく統合することが困難であるため、理想的ではありません。

@row
### Directing

The Directing element of an IAM project will vary greatly depending on whether a classical or an Agile project management methodology is followed.

@column
### 方針指導

IAMプロジェクトのディレクション要素は、古典的なプロジェクト管理方法論に従うか、アジャイルプロジェクト管理方法論に従うかによって大きく異なります。

@row
#### Classic

The Gannt chart becomes the main tool for directing the project. The PM will ensure tasks are commenced on time and progress to plan by conducting a weekly or biweekly review of the schedule in periodic team meetings. Team members will report on the progress to plan for each task to which they are assigned. For tasks behind schedule or expecting to encounter problems, the PM will attempt to put a contingency in place. If a slip occurs, the PM must go back to the steering committee with a recommended strategy and seek approval or additional direction (for example, the direction to accept the slip and modify the Gantt chart or the direction to invest the resources necessary to restore the original schedule). If the steering committee approves the change, the project schedule can be re-baselined.

@column
#### 古典的

ガントチャートは、プロジェクトを指揮するための主要なツールになります。PMは、毎週または隔週で行われる定期的なチームミーティングでスケジュールの見直しをおこない、タスクが予定通りに開始され、計画通りに進捗していることを確認します。チームメンバーは、自分が担当する各タスクの計画に対する進捗を報告します。スケジュールの遅れているタスクや問題の発生が予想されるタスクについては、PMはコンティンジェンシー（予備費）を設けるよう試みます。スリップが発生した場合、PMは推奨戦略を携えて運営委員会に戻り、承認または追加の指示（たとえば、スリップを受け入れてガントチャートを修正する指示や、元のスケジュールに戻すために必要なリソースを投入する指示）を求めなければなりません。もし運営委員会がその変更を承認すれば、プロジェクトスケジュールは再びベースライン化されます。

@row
#### Agile

The PM will establish regular ‘stand-up’ meetings, typically several times a week, at which each ‘sprint’ is reviewed and tasks moved on the Project Wall from ‘waiting’ to ‘current’ to ‘completed.’ Each scheduled task will be discussed, and any impediments to completing a ‘sprint’ will be noted by the PM and addressed with appropriate management. For instance, transition to production might occur during non-business hours requiring coordination with multiple business units. The PM must ensure agreement, and appropriate resourcing, from involved parties.

The PM will raise unresolved issues with the appropriate managers.

@column
#### アジャイル

PMは通常、週に数回、定期的な「スタンドアップ」ミーティングを設け、各「スプリント」をレビューし、プロジェクトウォール上のタスクを「未着手」から「着手」、「完了」へと移動させます。予定されている各タスクが議論され、「スプリント」の完了を阻害する要因があれば、PMが指摘し、適切な管理者とともに対処します。例えば、生産への移行が営業時間外におこなわれ、複数のビジネス部門との調整が必要になることがあります。PMは、関係者の同意と適切なリソースを確保しなければなりません。

PMは未解決の問題を適切な管理者に報告します。

@row
### Controlling

Control is probably the PM function that is most often performed poorly in IAM projects.

Control is a function of project management that provides feedback to the PM regarding the likelihood that the project will meet its schedule and budget constraints. PMs will typically assume that if they have planned well, organized the communication and quality assurance, adequately resourced their project, and properly directed the project tasks, nothing can go wrong. But the stories are legion that IAM projects have overrun because they impact so many functions within an organization. Managing this impact is where control comes in. Given that you cannot manage something if you cannot measure it, monitoring progress to plan is at the core of the control function. A tried-and-true tool in the PM’s toolkit is Earned Value Analysis (EVA). EVA involves calculating the budgeted cost of work scheduled (BCWS), the budgeted cost of work performed (BCWP), and the actual cost of work performed (ACWP). These calculations will compare the percent completion against the budget spent and quickly identify a project experiencing overspend or over-budget issues.

As an example, a project’s progress might be depicted as follows:

@column
### コントロール

コントロールは、IAMプロジェクトで最もよく実行されないPMの機能と考えられます。

コントロールとは、プロジェクトマネジメントの機能の一つで、プロジェクトがスケジュールと予算の制約を満たす可能性についてPMにフィードバックすることです。PMは通常、うまく計画し、コミュニケーションと品質保証を組織化し、十分なリソースを確保し、プロジェクトのタスクを適切に指示すれば、何も問題は起きないと考えるでしょう。しかし、IAMプロジェクトは、組織内の多くの機能に影響を与えるため、プロジェクトがオーバーランしたという話は枚挙にいとまがありません。この影響を管理することが、コントロールの出番です。測定できないものは管理できないため、計画に対する進捗を監視することが管理機能の中核になります。PMのツールキットで試行錯誤してきたものが、アーンドバリュー分析（EVA）です。EVAでは、予定作業の予算コスト（BCWS）、実行作業の予算コスト（BCWP）、実行作業の実績コスト（ACWP）を計算します。これらの計算により、費やした予算に対する完成度を比較し、支出超過や予算超過の問題が発生しているプロジェクトを迅速に特定することができます。

例えば、あるプロジェクトの進捗を次のように表現することができる：

@row
![A line graph showing a sample budget cost schedule. ](/assets/images/idpro_bok/PM-figure2.png)

Figure - Sample Budget Cost Schedule

@row
The BCWS shows the project’s schedule. It’s a two-month project with a budget of $53,000 (Y axis in thousands of dollars). The current spend is $55,000 with two weeks to go. The budgeted cost of the work performed to date is $45,000. So the EVA clearly shows the project is behind on its deliverables and is currently $10,000 overspent on its budget.

Another tool is calculating a project’s performance indices using quick ratios to gauge the probability of an on-time and in-budget project completion. Common indices are:

*   Cost Variance: CV = BCWP - ACWP
    
*   Scheduled Variance: SV = BCWP - BCWS
    
*   Cost Performance Index: CPI = BCWP/ACWP
    
*   Schedule Performance Index: SPI = BCWP/BCWS
    
*   Critical Ratio: CR = CPI \* SPI
    

A third useful tool is the S curve, which tracks the resource burn rate to ensure the project expenditure reduces appropriately, particularly at the end of a project. In the example above, the Actual Cost curve is not adhering to the ‘S’ shown in the scheduled work curve. Management of the resource burn rate is important for IAM projects since additional tasks, such as system documentation, are often not properly accommodated in the project schedule at project inception. These should not be added to the scope of the project. Instead, they should be completed as part of standard operations (i.e., outside the project).

@column
BCWSは、プロジェクトのスケジュールを示します。これは、予算が53,000ドル（Y軸は千ドル）の2ヶ月のプロジェクトです。現在の支出は55,000ドルで、あと2週間あります。現在までに実行された作業の予算コストは​​45,000ドルです。したがって、EVAはプロジェクトが成果物に遅れをとっており、現在予算を10,000ドル超過していることを明確に示しています。

別のツールは、予定どおりに予算内でプロジェクトが完了する確率を測定するため、迅速な比率を使用してプロジェクトのパフォーマンス指標を算出することです。一般的な指標は次のとおりです：

*   コスト差異： CV = BCWP - ACWP
    
*   スケジュール差異： SV = BCWP - BCWS
    
*   コストパフォーマンス指標： CPI = BCWP/ACWP
    
*   スケジュールパフォーマンス指標： SPI = BCWP/BCWS
    
*   臨界比： CR = CPI \* SPI
    

3つ目の便利なツールはS字カーブであり、これはリソースの燃焼率を追跡し、特にプロジェクト終了時にプロジェクトの支出が適切に削減されるようにします。上記の例では、アクチュアルコストカーブは、スケジュールされた作業カーブに示されている「S」に沿っていません。IAMプロジェクトでは、リソースの燃焼率を管理することが重要であり、これはシステムドキュメントなどの追加タスクが、プロジェクト開始時のプロジェクトスケジュールに適切に組み込まれていないことが多いためです。これらはプロジェクトのスコープに追加しないでください。代わりに、標準的な操作の一部として（つまり、プロジェクト外で）完了する必要があります。

@row
## Organizational Variances

When managing an identity project, it is worth understanding the type of organization for which the project is being undertaken.

@column
## 組織的な差異

アイデンティティプロジェクトを管理する場合、プロジェクトが実施される組織の種類を理解することに価値があります。

@row
### Public Sector

When managing a project for a government department, there will often be organizational structures that make it difficult. In a project to deploy an enterprise-level solution for a large government agency with multiple departments, there were two major obstacles. Firstly, only five of the departments in the agency agreed to participate in the project; the two largest departments declined to be involved. Secondly, the agency engaged an internal technology unit to deploy all their IT projects, making it difficult to engage with the end-users directly.

The first obstacle resulted in a meeting at which the benefits of the solution were explained, and the department personnel in attendance agreed to take a ‘watching brief’ as to how the project developed. They agreed to proceed with the solution once they observed a successful deployment. The second obstacle was overcome by inserting a ‘workshop’ task in the schedule that required participation by knowledgeable persons from the involved departments. The workshop was very successful, with participants demanding ongoing involvement in the project.

Part of the stakeholder analysis for public sector projects is to understand the motivation of the sponsor and other involved public servants; their motivation it’s not always to benefit the agency for which they work; it is sometimes to advance their career.

@column
### 公共部門

政府部門向けのプロジェクトを管理する場合、組織構造によってそれが難しくなることが多くあります。複数の部門を有する規模の大きな政府機関に対してエンタープライズレベルのソリューションをデプロイするプロジェクトでは、2つの大きな難題がありました。まず、このプロジェクトへの参加に同意したのは、政府機関内の5つの部署だけでした；2つの大きな部署は参加を拒否されました。次に、この機関はすべてのITプロジェクトを内部の技術部門に任せていたため、エンドユーザーと直接関わることが困難でした。

最初の難題は、このソリューションの利点を説明するミーティングにつながり、出席していた部署の人たちは、このプロジェクトがどのようにデプロイされるかを「見守る」ことに同意しました。デプロイに成功すると、このソリューションの導入を進めることに同意しました。2つ目の難題は、関係部署の有識者が参加する「ワークショップ」というタスクをスケジュールに入れることで克服しました。このワークショップは大成功で、参加者はこのプロジェクトに継続的に参加することを要望しました。

公共部門のステークホルダー分析の一環として、スポンサーや関係する公務員のモチベーションを理解することがあります；彼らのモチベーションは、必ずしも所属する機関の利益のためとは限りません；キャリアアップのためである場合もあります。

@row
### Private Sector

There is a danger to commercial projects that the scope will be too narrow. Because projects in the private sector are typically cost-constrained, there will be a reluctance to engage widely to build a comprehensive list of stakeholders that will ensure wide benefit across the company. When identifying items that will extend the scope, the project manager will often be told to place them in ‘phase 2’.

While this might make commercial sense, the project manager should ensure the Steering Committee understands the ramifications of not extending the project to include the requirements of a wider stakeholder cohort. It is far better to include requirements in the scope of the initial project than to be forced to extend the project once work has started. The scope must be determined before the schedule is developed and before the execution of the project commences. Adding new requirements during the execution phase will require the project to be re-baselined, which will involve more work and should be avoided.

@column
### 民間部門

商用プロジェクトには、スコープが狭すぎるという危険があります。民間部門のプロジェクトは一般的にコスト制約があるため、会社全体に幅広い利益をもたらす包括的なステークホルダー一覧を作成するために大きく関与することには消極的です。スコープを拡張するアイテムを見極める場合、プロジェクトマネージャーは、それらを「フェーズ2」に配置するように指示されることがよくあります。

これは商業的には理にかなっているかもしれませんが、プロジェクトマネージャーは、より多くのステークホルダーコホートの要件を含めるようにプロジェクトを拡張することを実施しない影響を運営委員会が理解していることを確認する必要があります。要件を最初のプロジェクトのスコープに含める方が、作業が開始された後にプロジェクトを拡張することを余儀なくされるよりもはるかに優れています。スコープは、スケジュールを作成する前、およびプロジェクトの実行を開始する前に決定する必要があります。実施段階で新しい要件を追加すると、プロジェクトのベースラインを再設定する必要がありますが、これにはより多くの作業が必要となるので避けるべきです。

@row
### Academia

Managing an identity project in the academic sector can be quite complicated. The administrative staff are divided into two large cohorts: administrative officers who keep the university or school operating and academic staff with diverse identity management requirements. If the institution is involved in research, there will be a further requirement to participate in cross-institutional identity federations to access documents from remote locations.

Then there’s the student cohort which consists of undergraduates, graduates, higher-degree by research students, and staff enrolled as students. Alumni comprise an additional cohort that may need to be considered.

When determining the scope, the project manager must agree on the user base to be accommodated. It is also noted that academics typically engage in a wide and diverse range of applications that might need to be accommodated by the IAM infrastructure.

@column
### 学術分野

学術分野でのアイデンティティプロジェクトの管理は、非常に複雑になる場合があります。管理スタッフは2つの大きなコホートに分けられます：大学または学校の運営を維持する管理職員と、さまざまなアイデンティティ管理要件を持つ教員です。その機関が研究に関与している場合、リモートからドキュメントにアクセスするために、機関間のアイデンティティフェデレーションに参加するという追加の要件があります。

次に、学部生、大学院生、高等学位を目指す研究生、およびおよび学生として登録されたスタッフで構成される学生コホートがあります。卒業生は、考慮する必要があるかもしれない追加のコホートを構成します。

スコープを決定するさい、プロジェクトマネージャーは、対応するユーザーベースに同意する必要があります。また、学者は通常、IAMインフラストラクチャで対応する必要があるかもしれない幅広く多様なアプリケーションに従事していることにも注意してください。

@row
## Conclusion

Project management methodology should be applied to all IAM projects, even small ones. Project management ensures that a structured process is applied to the activity and that the impact of the activity on affected business units will be considered and, if necessary, included in the planning. Failure to manage an IAM activity as a project will raise the likelihood of mistakes being made and additional costs being incurred. [^3]

@column
## 結論

プロジェクト管理の方法論は、たとえ小規模なものであっても、すべてのIAMプロジェクトに適用するべきです。プロジェクト管理は、構造化されたプロセスが活動に適用され、影響を受ける事業部門への活動の影響が考慮され、必要に応じて計画に盛り込まれることを保証します。IAMアクティビティをプロジェクトとして管理しないと、ミスが発生したり、追加のコストが発生したりする可能性が高くなります。 [^3]

@row
## Author Bios

Graham Williamson

<!-- ![Photo of Graham Williamson](/assets/images/idpro_bok/PM-author1.jpg) --> Graham Williamson is an IAM consultant working with commercial and government organizations for over 20 years with expertise in identity management and access control, enterprise architecture and service-oriented architecture, electronic commerce, and public key infrastructure, as well as ICT strategy development and project management. Graham has undertaken major projects for commercial organizations such as Cathay Pacific in Hong Kong and Sensis in Melbourne, academic institutions in Australia such as Monash University and Griffith University, and government agencies such as the Queensland Government CIO’s office and the Northern Territory Government in Australia and the Ministry of Home Affairs in Singapore.

Corey Scholefield

<!-- ![Photo of Corey Scholefield](/assets/images/idpro_bok/PM-author2.jpg) --> Corey is currently a Sr. Technical Product Manager with Workday, supporting operations engineering service delivery for Workday's cloud-ERP suite. Corey has a background in public-sector identity management, having spent over 15 years working in higher education, with positions at both University of Victoria and BCNET in British Columbia, Canada.

At BCNET, Corey led a federated-identity service bureau that supported regional adoption of eduroam and SAML capabilities under the umbrella of the Canadian Access Federation. At the University of Victoria, Corey's team established an identity-management program that supported campus-wide access-management needs. Corey has deployed many IDAM technologies, including OpenLDAP, CAS SSO, Sun IDM, Shibboleth IDP, and SailPoint IdentityIQ.

@row
## Change Log

|     |     |
| --- | --- |
| Date | Change |
| 2021-06-21 | Editorial updates; substantive revisions to IAM Projects section |
| 2022-09-30 | Substantive revisions to Planning Stage, Agile; new section on Organizational Variances |

@row
## Addendum: Questions for an IAM Project Manager to ask

@column
## 付録：IAMプロジェクトマネージャーが尋ねるべき質問

@row
### Identity Management

*   How are user accounts created when a new staff member joins the organization? Are employees and contract staff provisioned differently?
    
*   How are user attributes collected/determined?
    
*   What is the business process surrounding end-users being granted entitlements to access given applications? Is user self-service supported? Is there an approval workflow to gather authorization for establishing user entitlements?
    
*   Is there a different process for privileged accounts (e.g., accounts with admin privileges)?
    
*   What repositories of identity information exist in the organization (e.g., LDAP directories, Databases, Active Directory), and what interfaces to the identity management environment are needed (e.g., SCIM import, REST API, Webservices Gateway; CSV import)?
    
*   What is the business process for disabling an account and eventually deleting it?
    

@column
### アイデンティティ管理

*   新しいスタッフが組織に加わると、ユーザーアカウントはどのように作成されますか？社員と契約社員ではプロビジョニング方法が異なりますか？
    
*   ユーザー属性はどのように収集/決定されますか？
    
*   エンドユーザーに特定のアプリケーションへのアクセス権限を付与するためのビジネスプロセスはどのようなものですか？ユーザーによるセルフサービスはサポートされていますか？ユーザー権限の確立に必要な認可を得るための承認ワークフローはありますか？
    
*   特権アカウント（例：管理者権限を持つアカウント）には異なるプロセスがありますか？
    
*   組織にはどのようなアイデンティティ情報のリポジトリ（例：LDAPディレクトリ、データベース、Active Directory）が存在し、アイデンティティ管理環境にはどのようなインターフェイスが必要ですか（例：SCIMインポート、REST API、Webサービスゲートウェイ；CSVインポート）？
    
*   アカウントを無効にして最終的に削除するためのビジネスプロセスは何ですか？
    

@row
### Access Control

*   What authentication mechanisms are supported (e.g., local application database, corporate LDAP directory, Active Directory, RADIUS)?
    
*   Are multiple assurance levels supported (e.g., assurance elevation for sensitive resources)?
    
*   Is MFA supported (e.g., U2F, DUO, push authenticators)?
    
*   Is SSO supported? Is it only for web apps, or are other applications supported as well?
    
*   How are SaaS apps supported (e.g., periodic synchronization of identity data, SAML)?
    
*   How are user entitlements within an application managed (e.g., internally within the app, via an attribute passed in an HTTP header message, SAML assertion, Active Directory group membership)?
    
*   How are application administrator rights managed (e.g., manually, via approval workflow)?
    

@column
### アクセス制御

*   どのような認証メカニズムがサポートされていますか（例：ローカルアプリケーションデータベース、企業のLDAPディレクトリ、Active Directory、RADIUS）？
    
*   複数の保証レベル（例：機密リソースの保証の高度化）がサポートされていますか？
    
*   MFA（例：U2F、DUO、プッシュ認証）はサポートされていますか？
    
*   SSOはサポートされていますか？Webアプリのみですか、それとも他のアプリケーションもサポートされていますか？
    
*   SaaSアプリはどのようにサポートされていますか（例：アイデンティティデータの定期的な同期、SAML）？
    
*   アプリケーション内のユーザーエンタイトルメントはどのように管理されますか（例：アプリ内部、HTTPヘッダーメッセージで渡される属性、SAMLアサーション、Active Directoryグループメンバーシップ経由）？
    
*   アプリケーション管理者の権限はどのように管理されますか（例：手動、承認ワークフロー経由）？

@row
### Governance

*   What governance processes (e.g., re-certification/attestation reporting) are required? What audit processes must be supported?
    
*   What governance interfaces are required to collect user account information from corporate applications (e.g., REST API, SCIM, Webservice gateway, service-bus messaging, CSV export)?
    

@column
### ガバナンス

*   どのようなガバナンスプロセス（例：再認定/証明報告）が必要ですか？どのような監査プロセスがサポートされていますか？
    
*   企業アプリケーションからユーザー管理情報を収集するためにどのような監査インタフェースが必要ですか？（例：REST API、SCIM、Webサービスゲートウェイ、サービスバスメッセージング、CSVエクスポート）？
    

@row
- - -

[^1]:  Scrum Alliance, “Your Quick Guide to All Things Scrum,” accessed 29 June 2021, [https://www.scrumalliance.org/about-scrum/overview](https://www.scrumalliance.org/about-scrum/overview) . 
    
[^2]:  Project Management Institute website, [https://www.pmi.org/](https://www.pmi.org/) , accessed 29 June 2021. 
    
[^3]:  Project Management Institute, "PMBOK® Guide and Standards - Practice Standards & Framework," accessed 29 June 2021, [https://www.pmi.org/pmbok-guide-standards/framework](https://www.pmi.org/pmbok-guide-standards/framework) . 
