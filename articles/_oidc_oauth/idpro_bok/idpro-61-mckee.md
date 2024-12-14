---
layout: columns
title: Introduction to Policy-Based Access Controls (v3)
permalink: /docs/oidc_oauth/idpro_bok/61
date: 2024-09-09
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "アクセス制御", "PBAC"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/61/](https://bok.idpro.org/article/id/61/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

The natural evolution of access controls has caused many organizations to adopt access management paradigms that assign and revoke access based on structured and highly reproducible rules.    One such paradigm is known as Policy-Based Access Control (PBAC), which is most differentiated by two key characteristics:  

1. Where other access control paradigms often optimize for ease of granting user access to all relevant resources, PBAC optimizes for ease of extending resource access to all applicable users.    

2. PBAC facilitates the evaluation of context (time of day, location, etc.) in granting access to a protected resource.  Context is used to express who may access a resource and the conditions under which that access is permissible.  

Shifting the focus of access controls from the user to the resource allows PBAC systems to be particularly resilient against shifts in organizational structure or regulatory obligations.  The inclusion of context (such as an authorized user’s location or device) allows for additional security controls to be expressed and extended within resource permissions themselves, ensuring that all facets of access control are contained and auditable within a single structure.  

Because PBAC accommodates a very precise expression of who may access a resource and under which circumstances, it lends itself to the automation of access provisioning and deprovisioning in a way that provides ease of management as well as increased security and adaptability.


Keywords: Identity, Architecture, Access Control, Digital Identity, Risk, Policies, Automation, PBAC

@column
## 概要

アクセス制御の自然な進化により、多くの組織は構造化された再現性の高いルールに基づいてアクセス権を割り当てたり、取り消したりするアクセス管理パラダイムを採用するようになりました。このようなパラダイムの1つがポリシーベースアクセス制御（PBAC）として知られる、以下の2つの特徴によってもっと差別化されているものです：

1. 他のアクセス制御パラダイムは多くの場合、全ての関連するリソースへのユーザーアクセスの付与を容易におこなうために最適化していますが、PBACは全ての適切なユーザーにリソースアクセスを拡張することを容易におこなうために最適化しています。

2. PBACは、保護されたリソースへのアクセス権の付与におけるコンテキスト（時間帯、場所など）の評価を推進します。コンテキストは、誰がリソースにアクセスしようとしているか、どのアクセスが許可される条件なのかを表現するために利用されます。

アクセス制御の焦点がユーザーからリソースに移動することで、PBACシステムは組織構造や規制上の義務の変化に対して特に耐性を持つことができます。コンテキスト（認可されたユーザーの場所やデバイスなど）を含めることで、追加のセキュリティ制御を表現およびリソースの権限自体を拡張することができ、アクセス制御の全要素が単一の構造に含まれ、監査可能になることが保証されます。

PBACは誰がどのような状況でリソースにアクセスできるかを非常に正確に表現できるため、セキュリティおよび適応性を高めるだけでなく、管理を容易にする方法で、アクセス権のプロビジョニングとデプロビジョニングの自動化に導きます。


Keywords: アイデンティティ, アーキテクチャ, アクセス制御, デジタルアイデンティティ, リスク, ポリシー, 自動化, PBAC

@row
By Mary McKee

© 2021, 2022, 2023 IDPro, Mary McKee

_Please see André Koot’s [_Introduction to Access Control for a primer on access controls_](https://bok.idpro.org/article/id/42/) ._

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction  

To effectively secure resources, access control systems must be designed to adapt to rapid shifts in technology, regulatory obligations, and organizational structure. As organizations embrace more sophisticated technology and seek protection from more sophisticated threats, access management strategies are evolving to address modern concerns.

Most early access management systems utilize what we now refer to as **Discretionary Access Control** ( **DAC)** . With DAC systems (such as access control lists), administrators manually assign privileges to users according to their understanding of need, appropriate use, and organizational rules. As DAC systems grow in users, resources, administrators, and/or age, their reliance on ad hoc management leads to inconsistencies in application and understanding of access. As inappropriate access often goes unnoticed and insufficient access creates visible business challenges, DAC administrators are increasingly incentivized to be liberal with authorizations and conservative with access cleanup. As a result, DAC is often too costly, too inconsistent, and too inflexible for modern needs.

Contemporary access control systems aim to promote consistency and efficiency by granting access to resources through structured rules. Perhaps the best-known model for abstracting access control so that permissions are based on rules is known as **Role-Based Access Control (RBAC)** . Through RBAC, permissions are associated with “roles” assigned to users. This model effectively ensures that users with the same responsibilities are consistently granted the same permissions. It encourages governance by requiring that roles and their associated permissions be defined before they can be used.

Further, RBAC is suitable for use in federated authorization scenarios where resource permissions depend on the information provided by an external user authority. While these are improvements over DAC, RBAC permissions are not resilient against shifts in responsibility structure within an organization and are limited in how permissions can be defined. These drawbacks, covered later in this article, make it difficult for RBAC systems to ensure that users do not have more access than they need to perform intended business functions (also known as the _principle of least privilege_ [^1] ).

**Policy-Based Access Control (PBAC)** is a more robust paradigm for managing permissions through structured rules in federated or non-federated contexts.  
  
While the RBAC model intentionally bundles permissions, PBAC builds on a concept known as **Attribute-based Access Control (ABAC)** to automate fine-grained, decoupled permissions. Leveraging ABAC’s approach of calculating permissions based on user information such as a job code or employment status, PBAC provides increased precision by supporting appropriate access conditions (or context).

@column
## 導入

リソースを効果的に保護するためには、アクセス制御システムは、テクノロジー、規制義務および組織構造の急速な変化に適応できるように設計されていなければなりません。組織がより高度な技術を取り入れ、より巧妙な脅威からの保護を求めるにつれ、アクセス管理戦略も現代の懸念に対応できるように進化しています。

初期のアクセス管理システムのほとんどは、現在私たちが **裁量アクセス制御** （ **DAC** ）と呼んでいるものを利用していました。DACシステム（アクセス制御リストなど）では、管理者が必要性、適切な使用方法および組織のルールを理解した上で、手動でユーザーに特権を割り当てます。DACシステムは、ユーザー、リソース、管理者、利用年数が大きくなるにつれて、その場しのぎの管理に依存するようになり、アクセスの適用と理解に一貫性がなくなります。不適切なアクセスは気づかれないことが多く、不十分なアクセスは目に見えるビジネス上の問題を引き起こすため、DAC管理者は権限を自由に与え、アクセスのクリーンアップを保守的におこなう動機付けがますます強くなります。その結果、DACは現代のニーズに対して、コストがかかりすぎ、一貫性がなく、柔軟性に欠けることが多くなっています。

現代のアクセス制御システムは、構造化されたルールによってリソースへのアクセス権を付与することで、一貫性と効率性を促進することを目的としています。アクセス制御を抽象化し、ルールに基づいて権限を与えるおそらく最もよく知られているモデルは **ロールベースアクセス制御（RBAC）** です。RBACでは、権限はユーザーに割り当てられた「ロール」に関連付けられます。このモデルは、同じ責任を負うユーザーには一貫して同じ権限が与えられることを保証します。ロールとそれに関連する権限を使用する前に定義することを要求することでガバナンスを促進します。

さらに、リソースの権限が外部のユーザー権威機関から提供される情報に依存するような、フェデレーション認可シナリオでの使用においてRBACは適しています。これらはDACに対する改善ですが、RBAC権限は組織内の責任構造の変化に対する弾力性がなく、権限の定義方法にも制限があります。これらの欠点は本記事で後述しますが、RBACシステムでは、ユーザーが意図したビジネス機能を実行するために必要以上のアクセス権を持たないようにすること（ _最小特権の原則_ [^1]）が難しいです。

**ポリシーベースアクセスコントロール（PBAC）** は、フェデレーションまたはフェデレーションではないコンテキストで構造化されたルールを通じて権限を管理するための、より堅牢なパラダイムです。
  
RBACモデルが意図的に権限を束ねるのに対し、PBACは **属性ベースアクセス制御（ABAC）** と呼ばれる概念をもとに、きめ細かく切り離された権限を自動化するものです。ジョブコードや雇用形態などのユーザー情報をもとに権限を計算するABACのアプローチを活用し、PBACは適切なアクセス条件（またはコンテキスト）をサポートすることで精度を向上させます。

@row
## Terminology

*   **Access control system** – a structure that manages and helps enforce decisions about access within an organization.
    
*   **User** or **Subject** – a person or entity who may receive access within an access control system.
    
*   **Resource** or **Object** – an asset protected by access controls, such as an application, system, or door.
    
*   **Action** – a protected operation available for a resource, such as “view”, “edit”, or “submit”.
    
*   **Permission** – a statement of authorization for one or more subjects to perform one or more actions on one or more objects.
    
*   **Context** – conditions under which an action on a resource is authorized for a subject, such as time of access, location of access, or a compliance state.
    
*   **Federated access controls** – an access control architecture that accommodates the separation of user/subject authority and resource/object authority.
    
*   **Discretionary access control** – a pattern of access control system involving static, manual definitions of permissions assigned directly to users.
    
*   **Role-based access control** – a pattern of access control system involving sets of static, manual definitions of permissions assigned to “roles”, which can be consistently and repeatably associated with users with common access needs.
    
*   **Attribute-based access control (“ABAC”) / Claims-based access control (“CBAC”)** – a pattern of access control system involving dynamic definitions of permissions based on information (“attributes”, or “claims”), such as job code, department, or group membership.
    
*   **Policy-based access control** – a pattern of access control system involving dynamic definitions of access permissions based on user attributes (as in ABAC) and context variables for permitting or denying access.
    
*   **Principle of least privilege** – an information security best practice ensuring that users in an access control system do not have more access to resources than is necessary for their intended activities.
    
*   **Segment** – a grouping of subjects that may be useful for authorizations, such as full-time employees, undergraduate students, IT administrators, or clinicians.
    
*   **Abstraction** – the practice of identifying and isolating repeated aspects of operations or business logic so that they can be maintained in one place and referenced in many places.
    

@column
## 用語解説

*   **アクセス制御システム** – 組織内のアクセスに関する決定を管理し、強制することを支援する構造。
    
*   **ユーザー** または **主体** – アクセス制御システム内でアクセス権を受け取ることができる人またはエンティティ。
    
*   **リソース** または **オブジェクト** – アクセス制御によって保護されるアプリケーション、システムやドアなどの資産。
    
*   **アクション** – 「閲覧」、「編集」、「送信」など、リソースに対して利用可能な保護された操作。
    
*   **権限** – 1つまたは複数のオブジェクトに対して1つまたは複数のアクションを実行する、1つまたは複数の主体に対する認可のステートメント。
    
*   **コンテキスト** – アクセスをおこなった時間、場所またはコンプライアンス状態など、リソース上のアクションが主体に認可される条件。
    
*   **フェデレーションアクセス制御** – ユーザー／主体の権威機関とリソース／オブジェクトの権威機関の分離に対応するアクセス制御アーキテクチャ。
    
*   **裁量アクセス制御** – ユーザーに直接割り当てられる静的で手動的な権限定義を含むアクセス制御システムのパターン。
    
*   **ロールベースアクセス制御** – 共通のアクセスの必要性を有しているユーザーに一貫して繰り返し関連付けることができる「ロール」に割り当てられた、静的で手動による権限定義のセットを含むアクセス制御システムパターン。
    
*   **属性ベースアクセス制御（「ABAC」） / クレームベースアクセス制御（「CBAC」）** – ジョブコード、部署、グループメンバーなどの情報（「属性」または「クレーム」）に基づくアクセス許可の動的定義を含むアクセス制御システムパターン。
    
*   **ポリシーベースアクセス制御** – （ABACのような）ユーザー属性と、アクセスを許可または拒否するためのコンテキスト変数に基づくアクセス許可の動的な定義を含むアクセス制御システムのパターン。
    
*   **最小特権の原則** – アクセス制御システムにおいて、ユーザが意図した活動に必要以上のリソースへのアクセス権を持たないようにする情報セキュリティのベストプラクティス。
    
*   **セグメント** – 正規職員、学部生、IT管理者、臨床医などの認可に有用と思われる主体のグループ化。
    
*   **抽象化** – 運用やビジネスロジックの繰り返される側面を識別し分離することで、それらを一箇所で維持し、多くの場所で参照できるようにするプラクティス。
    

@row
## PBAC vs. RBAC: A Comparison

To better understand PBAC structures, it may be helpful to examine how they differ from RBAC.

While the primary focus of RBAC permissions is the user, the primary focus for PBAC permissions is the resource.

RBAC asks, “What types of users do I have, and what may they do in my environment?”. Controls are constructed with **subjects** (who is getting access), **permissions** (what is being accessed or used), and **roles** (what permissions can be assigned to a subject) [^2] . This looks like:

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **Subject** |     | **Role** |     | **Permission** |
| Ada | as  | Editor | may | Modify Documents |

PBAC asks, “What types of resources do I have, and who/how may they be used or managed?” Controls are constructed with **subjects** (who is getting access), **actions** (what behavior is being discussed), **objects** (what resource is being accessed or used), and **context** (environmental or other parameters defining acceptable access) [^3] . This looks like:

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **Object** |     | **Action** |     | **Subject** | **Context** |
| Documents | may be | Modified | by  | Those with “Editor” job code | On managed devices |

Both examples abstract subjects to ensure that all editors are granted the necessary permission. In the RBAC example, Ada acquires the permission because she has been assigned to the “Editor” role through a manual or automated process. In the PBAC example, Ada acquires the permission because the subject definition matches her employee record, though the subject definition could also be a manual process, such as the assignment of a group membership.  
  
To make the most apples-to-apples comparison, imagine that an RBAC system adds Ada to an “Editor” role, and a PBAC system adds her to an “Editor” group membership that is referenced in access policies. Though these actions may seem nearly equivalent, the PBAC architecture offers the following advantages: the flexibility to support different situations (context), the ability to discretely handle changes without impacting other permissions (modularity), and the capacity to handle real-time permission evaluation (symmetry). Each of these factors promotes an organizationally consistent and defensible approach to access control, as illustrated by the following examples:

@column
## PBAC vs. RBAC: 比較

PBACの構造をよりよく理解するためには、RBACとの違いを検証することが有効なはずです。

RBACの権限の主な焦点がユーザーであるのに対し、PBACの権限の主な焦点はリソースです。

RBACは、「どのような種類のユーザーがいて、彼らが私の環境で何をすることができるのか？」を尋ねます。制御は **主体** （誰がアクセスするのか）、 **権限** （アクセスまたは使用されるのは何か）、 **ロール** （主体に割り当てられるのはどのような権限か）で構築されます [^2] 。これは、以下のようになります：

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **主体** |     | **ロール** |     | **権限** |
| Ada | as  | Editor | may | Modify Documents |

PBACは、「どのような種類のリソースがあり、誰が/どのようにそれらを使用または管理することができるのか」を尋ねます。制御は、 **主体** （誰がアクセスするのか）、 **アクション** （どのような行動が議論されているのか）、 **オブジェクト** （どのリソースがアクセスまたは使用されているのか）、そして **コンテキスト** （許容できるアクセスを定義する環境またはその他のパラメータ）で構築されます [^3] 。これは、以下のようになります：

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **オブジェクト** |     | **アクション** |     | **主体** | **コンテキスト** |
| Documents | may be | Modified | by  | Those with “Editor” job code | On managed devices |

どちらの例も、すべての編集者に必要な権限が付与されるように、主体を抽象化しています。RBACの例では、Adaは手動または自動プロセスによって「Editor」ロールに割り当てられているため、権限を取得することができます。PBACの例では、Adaは主体の定義が彼女の従業員レコードと一致するため、権限を取得します。ただし、主体の定義は、グループメンバーシップの割り当てなど、手動プロセスである可能性もあります。
  
最も単純に比較するために、RBACシステムがAdaを「Editor」ロールに追加し、PBACシステムがアクセスポリシーで参照される「Editor」グループメンバーシップに追加すると想像してみましょう。これらのアクションはほぼ同等に見えるかもしれませんが、PBACアーキテクチャには以下の長所があります：さまざまな状況に対応できる柔軟性（コンテキスト）、他の権限に影響を与えずに変更を個別に処理する能力（モジュール性）、リアルタイムの権限評価をおこなう能力（対称性）。これらの各要素は、以下の例で示されるように、アクセス制御に対する組織的な一貫性と防衛的なアプローチを促進します：
To make the most apples-to-apples comparison, imagine that an RBAC system adds Ada to an “Editor” role, and a PBAC system adds her to an “Editor” group membership that is referenced in access policies. Though these actions may seem nearly equivalent, the PBAC architecture offers the following advantages: the flexibility to support different situations (context), the ability to discretely handle changes without impacting other permissions (modularity), and the capacity to handle real-time permission evaluation (symmetry). Each of these factors promotes an organizationally consistent and defensible approach to access control, as illustrated by the following examples:

@row
### Context

Ada’s employer may be subject to legal or compliance concerns that affect how resources may be accessed. For example, when national security regulation (such as export controls) restricts access from certain types of devices, relevant PBAC policies can be amended to include this stipulation.

If the company requires some form of training before resources can be accessed, this too can be articulated as context. A “certification status” attribute can be maintained for Ada based on records referenced from within or outside the authorizing organization. Ada’s permissions can require that this status is current at the time of access. Instead of laborious audit processes or managing infrastructure to revoke and reassign permissions as compliance states change, Ada’s access is automatically blocked when she is not compliant with training and automatically restored when she re-certifies her training. Similarly, if Ada must consent to terms and conditions for the access she has been granted, PBAC context can ensure that this has occurred in advance of any interaction with the resource.

For security reasons, Ada may be expected to only access company resources from safe-listed network spaces or with multi-factor authentication requirements that are more stringent than those of users with lesser permissions. By codifying and enforcing these requirements within the scope of the permission, Ada’s employer can easily reference, manage, and adapt all access requirements in a single place.

@column
### コンテキスト

Adaの雇用主は、リソースへのアクセス方法に影響を与える法的またはコンプライアンス上の懸念を抱いている場合があります。例えば、国家安全保障に関する規制（輸出規制など）により、特定の種類のデバイスからのアクセスが制限されている場合、関連するPBACポリシーを修正して、この規定を含めることができます。

会社がリソースにアクセスする前に何らかのトレーニングを必要とする場合、これもコンテキストとして明確にすることができます。認可をおこなう組織の内外から参照される記録に基づいて、Adaの「認定状況」属性を維持することができます。Adaの権限には、アクセス時にこのステータスが最新であることを要求することができます。手間のかかる監査プロセスや、コンプライアンス状態の変化に応じて権限を取り消したり再割り当てしたりするインフラストラクチャーを管理する代わりに、Adaがトレーニングに準拠していない場合はAdaのアクセス権は自動的にブロックされ、トレーニングが再認定されると自動的に回復させることができます。同様に、Adaが付与されたアクセス権に関する条件に同意しなければならない場合、PBACコンテキストは、リソースとのやりとりの前に、この同意がおこなわれたことを確認することができます。

セキュリティ上の理由から、Adaは安全なネットワークスペースからしか会社のリソースにアクセスできないようにしたり、より弱い権限を持つユーザーよりも厳しい多要素認証の要件を満たしたりすることが期待されているかもしれません。これらの要件を権限の範囲内で明文化し、強制することで、Adaの雇用主はすべてのアクセス要件を一箇所で簡単に参照、管理、適応することができます。

@row
### Modularity

Because permissions granted by PBAC policies are not inherently interconnected as they are with RBAC, they are highly modular and easier to manage with confidence. When an organization needs to add, remove, or modify controls on a resource, policies for that resource can be adapted exactly as needed without impacting other resources.

When permissions are bundled together, as in RBAC, accommodating new business scenarios requires a broad analysis of existing permission groupings. Often, administrators are forced to choose between a “close enough” access bundle that carries unneeded permissions with it or contributing to a proliferation of bundles that become increasingly difficult to understand and maintain.

For example, if senior leadership at Ada’s company selected her to edit sensitive briefings for their investors, it is likely that she would need access atypical for editors. An RBAC system admin charged with granting this access is likely to consider solutions such as:

*   > Giving all editors the access Ada now needs, thus over-privileging other editors.
    
*   > Granting Ada a senior leadership role in addition to the editor role, thus over-privileging Ada.
    
*   > Creating a new role for permissions specific to this need, setting a precedent of provisional role creation for ad hoc needs.
    
*   > Re-engineering roles to offer a cleaner solution for this business scenario, typically a costly exercise.
    

Organizations with evolving access needs will generally not find it practical to redesign RBAC roles each time an access need is not represented by an existing role. The alternatives – over-privileging or over-complicating – promote an increasingly lackadaisical approach to access management within the organization.

@column
### モジュール性

PBACポリシーによって付与される権限は、RBACのような相互関連が本質的にはないため、高度にモジュール化され、機密性を維持して管理しやすくなっています。組織があるリソースに対する制御を追加、削除または変更する必要がある場合、そのリソースのポリシーは、他のリソースに影響を与えることなく、必要に応じて正確に適応させることができます。

RBACのように権限がまとめられている場合、新しいビジネスシナリオに対応するには、既存の権限のグループ分けを幅広く分析する必要があります。多くの場合、管理者は不要な権限が含まれる「概ね充分な」アクセスバンドルか、理解と維持がますます困難になるバンドルを増やすかの選択を迫られます。

例えば、Adaの会社の上層部が、投資家向けの機密資料の編集を彼女に依頼した場合、編集者としては一般的でないアクセス権が必要になる可能性が高い。RBACシステムの管理者は、このようなアクセス権の付与を担当する場合、次のような解決策を検討することになるでしょう：

*   > Adaが必要とするアクセス権をすべての編集者ロールに付与することで、他の編集者に過剰に権限を与える。
    
*   > Adaに編集者ロールだけでなくシニアリーダーのロールを付与し、Adaに過剰な権限を与える。
    
*   > このニーズに特化した権限のための新しいロールを作成し、アドホックなニーズに対する仮設のロール作成の先例を作る。
    
*   > このようなビジネスシナリオに対して、よりクリーンなソリューションを提供するための再エンジニアリングは通常コストがかかります。
    

アクセスニーズが変化する組織では、既存のロールでは表現できないアクセスニーズが発生するたびにRBACロールを再設計することは、一般に現実的ではありません。また、過剰な権限や過剰な複雑化は、組織内のアクセス管理に対してますます無関心な姿勢を助長します。

@row
### Symmetry

When there is a divergence between the criteria for granting access and criteria for revoking access in a system, it is common for the system to accumulate permissions that were at one time appropriate but would not be allowed under current policy. PBAC systems are not susceptible to this permission spread because access control decisions are made in real-time based on current attributes and context.

Since PBAC is an extension of ABAC, PBAC controls easily accommodate fully or partially automated access based on attributes. An institution may wish to automatically grant access to any current employee of a company, any employee who works at Office X, or any employee who works at Office Y and is not currently on personal leave.

Automating how access is assigned simplifies the tasks of automating continuous monitoring of permission validity and revoking permissions that are no longer allowable under current rules. This creates symmetry between provisioning and deprovisioning of access, minimizing system maintenance and remnant permissions.  
  
PBAC is Practical

PBAC scales well because it is adaptable, and this adaptability can make it a practical option for organizations of any size. Time saved with streamlined RBAC roles can be quickly lost if the business impact of modifying a role (or its many associated permissions) is unclear. This can disincentivize active and responsible management of access controls and hamper growth in an organization of any size.

To illustrate how PBAC can be preferable even in a small organization, consider the following scenario:

JE Plumbing starts as a small business comprised of five plumbers and an owner who handles all administration.  
  
Thanks to an excellent reputation and growing customer base, the owner is able to expand the staff to twenty plumbers, who are supported by a business manager, three sales representatives, and two finance specialists.

Over time, JE Plumbing sees an opportunity to expand the company’s coverage area and offerings. To accomplish this, they set up two new locations overseen by two new business managers (one of whom was an internal promotion from a finance specialist position). They grow their residential plumber staff to seventy-five and hire twenty-five commercial plumbers. Finance and sales positions are replicated across the two new offices, growing that team from two to six. A dedicated marketing specialist is hired to cover all three sites.

An RBAC approach to this problem might start with two roles: an admin role for the owner and a technician role for her staff. As the company grows, a business manager might be trusted with the admin role, but new roles would need to be created for the sales and finance specialists. After doubling from two to four roles, the role count doubles again as the company splits the technician role into commercial technician and residential technician, splits the sales and marketing role into distinct roles, formalizes roles for business managers and customer service, and retains the original admin and finance roles.

Though this example looks at JE Plumbing’s development at three points in time, it is unlikely that the company would implement such broad shifts overnight. To preserve security through incremental shifts in responsibility, a small business making strategic organizational adjustments with limited working capital should consider the absence of a role not included in this exercise: that of a full-time IT professional available to perpetually re-engineer access management structures and adapt each system utilizing them.

By contrast, a PBAC approach would start by looking at what resources JE Plumbing needs to secure: work orders, customer information, invoices, inventory, employee personal and licensing information, payroll data, and expense reports. Though responsibility for these functions changes as the company adds staff, the functions themselves remain the same. If the company expanded the nature of its business in addition to the scale, permissions could easily be added to support the new functions without interfering with existing functions.

This simple shift from expressing access controls from user-focused to resource-focused allows for access control complexity to grow linearly rather than exponentially. As a result, JE Plumbing can adapt permissions in step with organizational shifts without managing a ballooning number of roles.

In addition to being more sustainable, PBAC also creates opportunities for the company to reduce risk by setting the context for access. For example:

*   When technicians can see all customer information, customers are at risk of privacy violations, and the company is at risk of an employee exfiltrating that information to help them start their own competing company. Perhaps technicians need to see addresses to navigate to job sites but only need to see information associated with open jobs assigned to them. Customer service may need to see phone numbers and email addresses for all customers but may not need address information.
    
*   Only technicians making rounds need access to job information from out of the office, so restricting other users’ access to internal IP addresses is an easy way to reduce the cyberattack surface for the company’s systems.
    
*   Overexposure of work order information encourages employee speculation about how the business is being run, which can result in misunderstandings or inappropriate disclosures about operational practices.
    
*   When technicians can be assigned to jobs at a business manager’s discretion, there is a risk of a technician being sent on the job with a lapsed license. Policy-based permissioning can require valid licensing before a job assignment can occur.
    

Although organizations with modest access management needs may initially choose to forgo PBAC features such as context limitations on access policies, committing early to PBAC architecture for access controls allows for an organic and natural maturation of access management rules over time - whether it be to accommodate more users, more resources, and/or a more sophisticated security or risk management posture.

@column
### 対称性

システムでアクセスを許可する基準とアクセスを取り消す基準との間に相違がある場合、システムはかつては適切であったが現在のポリシーでは許可されない権限を蓄積するのが一般的です。アクセス制御の決定は現在の属性とコンテキストに基づいてリアルタイムでおこなわれるため、PBACシステムはこの許可の拡散の影響を受けません。

PBACはABACの拡張であるため、PBAC制御は属性に基づいて完全または部分的に自動化されたアクセスに簡単に対応できます。機関は、会社の現在の従業員、オフィスXで働く従業員、またはオフィスYで働いていて現在私用休暇中ではない従業員にアクセス権を自動的に許可したいと考えるかもしれません。

アクセスの割り当て方法を自動化することで、アクセス許可の有効性の継続的な監視を自動化し、現在のルールでは許可されなくなったアクセス許可を取り消すタスクが簡素化されます。これにより、アクセスのプロビジョニングとデプロビジョニングの間に対称性が生まれ、システムのメンテナンスと残りの権限が最小限に抑えられます。

PBACは実用的です

PBACは適応性があるため拡張性に優れており、この適応性により、あらゆる規模の組織にとって実用的な選択肢となります。合理化されたRBACロールで節約された時間は、ロール（またはそれに関連付けられている多くの権限）の変更によるビジネスへの影響がわからない場合、すぐに失われる可能性があります。これは、アクセス制御の積極的かつ責任ある管理を阻害し、あらゆる規模の組織の成長を妨げる可能性があります。

小規模な組織でもPBACがどのように望ましいかを説明するために、以下のシナリオを検討してください：

JE Plumbingは、5人の配管工とすべての管理を担当するオーナーで構成される小規模なビジネスとして始まります。
  
優れた評判と顧客基盤の拡大のおかげで、オーナーはビジネスマネージャー、3人の営業担当者および2人の財務専門家によってサポートされる20人の配管工にまで、スタッフを拡大することができます。

時間の経過とともに、JE Plumbingは同社のサービス提供エリアとサービスを拡大する機会を見出しています。これを達成するために、彼らは2人の新しいビジネスマネージャー（そのうちの1人は財務専門職からの内部昇格者）によって監督される2つの新しいエリアを設定しました。彼らは住宅用配管工のスタッフを75人に増やし、25人の商用配管工を雇っています。財務と販売のポジションは2つの新しいオフィスに複製され、そのチームは2人から6人に増えました。専任のマーケティングスペシャリストが、3つのサイトすべてをカバーするために雇われています。

この問題に対するRBACのアプローチは、オーナーの管理者のロールとスタッフの技術者のロールという2つのロールから始めるでしょう。会社が成長するにつれて、ビジネスマネージャーは管理者のロールで信頼されるかもしれませんが、販売および財務の専門家のためには新しいロールを作成する必要があります。2から4にロールに倍増した後、会社が技術者のロールを商業技術者と住宅技術者に分割し、販売とマーケティングのロールを別のロールに分割し、ビジネスマネージャーと顧客サービスのロールを設定し、元の管理者と財務のロールは維持し、結果としてロール数はさらに2倍になります。

この例では、JE Plumbingの発展を3つの時点で見ていますが、会社がそのような大規模なシフトを一晩で実施する可能性は低いです。責任の段階的な変化を通じてセキュリティを維持するために、限られた運転資本で戦略的な組織調整をおこなっている中小企業は、このシナリオには含まれていないロールがあることを考慮する必要があります：アクセス管理構造を永続的に再設計でき、それらを利用する各システムを適応させるフルタイムのIT専門家のロールです。

対照的に、PBACアプローチは、JE Plumbingが保護する必要があるリソース（作業指示書、顧客情報、請求書、在庫、従業員の個人情報とライセンス情報、給与データ、経費報告書）を調べることから始まります。会社がスタッフを追加するにつれて、これらの機能の責任は変わりますが、機能自体は同じままです。会社が規模に加えてビジネスの性質を拡大した場合、既存の機能に干渉することなく、新しい機能をサポートするためのアクセス許可を簡単に追加できます。

アクセス制御をユーザー重視からリソース重視に表現する、この単純な移行により、アクセス制御の複雑さが指数関数的ではなく直線的に増大することが可能になります。その結果、JE Plumbingは、膨大な数のロールを管理することなく、組織の変化に合わせて権限を適応させることができます。

PBACは、より持続可能であることに加え、アクセスのためのコンテキストを設定することで、リスクを低減する機会も作り出します。例えば：

*   技術者がすべての顧客情報を見ることができると、顧客はプライバシー侵害のリスクにさらされ、会社は従業員がその情報を流用して競合する会社を設立するリスクにさらされます。技術者は作業現場に移動するために住所を見る必要があるかもしれませんが、自分に割り当てられているオープンな仕事に関連する情報のみを見る必要があるかもしれません。カスタマーサービスでは、すべての顧客の電話番号とEメールアドレスを確認する必要がありますが、住所情報は必要ないかもしれません。
    
*   外回りをしている技術者だけが外出先から業務情報にアクセスする必要があるため、他のユーザーの社内IPアドレスへのアクセスを制限することは、会社のシステムに対するサイバー攻撃の領域を減らす簡単な方法です。
    
*   業務指示の情報が過度に公開されると、業務がどのようにおこなわれているかについての従業員の推測が促され、事業運営がどのようになされているか従業員の憶測が助長され、業務慣行についての誤解や、不適切な開示に繋がる可能性があります。
    
*   ビジネスマネージャーの裁量で技術者にジョブを割り当てることができる場合、ライセンスが失効した技術者がジョブに送り込まれる危険性があります。ポリシーベースの権限付与は、ジョブの割り当てがおこなわれる前に有効なライセンスを要求することができます。
    

アクセス管理のニーズがそれほど高くない組織は、当初アクセスポリシーのコンテキスト制限などのPBAC機能を見送るかもしれませんが、アクセス管理のためにPBACアーキテクチャに早期に取り組むことで、より多くのユーザー、より多くのリソース、および/またはより洗練されたセキュリティやリスク管理態勢に対応するため、アクセス管理ルールを時間の経過と共に有機的かつ自然に熟成させることができます。

@row
## When RBAC is Preferable

This article has primarily compared policy-based access controls to role-based access controls due to the prominence of RBAC as an access control strategy.

Some IAM professionals may be interested in implementing PBAC controls but must work with systems that can only support RBAC. In these cases, it is sometimes advantageous to rethink institutional roles in terms of resources or specific work functions rather than permission bundles that will be difficult to adapt over time. As long as an RBAC system accommodates multiple roles for a user, it should be possible to achieve some advantages of PBAC (like modularity) within that system.

When choosing between RBAC and PBAC, it may be helpful to consider that PBAC can be constructed to behave like RBAC more reliably than the reverse. For example, an organization that prefers to think in terms of “roles” may choose to represent group memberships as such, assigning those groups to many resource permissions to the same end effect - one action results in the application of a defined set of permissions. Conversely, options for applying a notion of context to RBAC permissions are often limited.

While the increased flexibility and scalability of PBAC make it a strong choice for protecting sensitive resources, it may be less approachable for casual users of an access management system. Systems with straightforward and fairly static access controls, especially those that delegate access management to end users rather than administrators (such as those where content creators can authorize collaborators), may find that the intuitiveness of a system like RBAC is more advantageous than the flexibility of PBAC.

@column
## RBACが望ましい場合

本稿では、アクセス制御戦略としてRBACが注目されていることから、主にポリシーベースアクセス制御とロールベースアクセス制御を比較しています。

一部のIAM専門家はPBAC制御の実装に興味があっても、RBACしかサポートしていないシステムで作業しなければならない人もいるかもしれない。このような場合、時間の経過とともに適応が難しくなる権限バンドルではなく、リソースや特定の作業機能という観点から組織のロールを再考するほうが有利なことがあります。RBACシステムがユーザーの複数のロールに対応する限り、そのシステム内でPBACのいくつかの長所（モジュール性など）を実現することは可能なはずです。

RBACとPBACのどちらかを選択する場合、PBACはRBACのような動作をするように構築することができ、その反対よりも確実に動作する、ということを考慮すると役立つ場合があります。例えば、「ロール」という用語で考えることを好む組織は、グループメンバーシップをそのように表現し、それらグループに多くのリソース権限を割り当てて、同じ最終効果（あるアクションをおこなうと、定義された一連の権限が適用される）を得ることができます。反対に、RBACの権限にコンテキストの概念を適用する選択肢は、しばしば制限されます。

PBACは柔軟性と拡張性が高いため、機密性の高いリソースの保護には適していますが、アクセス管理システムの一般ユーザーにとってはとっつきにくいかもしれません。単純でかなり静的なアクセス制御をおこなうシステム、特に管理者ではなくエンドユーザーにアクセス管理を委任するシステム（コンテンツ制作者が共同制作者を認可できるシステムなど）では、PBACの柔軟性よりもRBACのようなシステムの直感性の方が有利になる可能性があります。

@row
## Implementing PBAC

The key to building a successful access control environment is accommodating changing business requirements. To promote ease and precision of access management, the system should be neither too rigid nor too abstract.

To achieve this balance in a PBAC implementation, consider the following guiding principles:

@column
## PBACの実装

アクセス制御環境の構築の成功の鍵は、変化するビジネス要件に対応することです。アクセス管理の容易さと正確さを促進するために、システムは、硬直しすぎず、抽象的すぎないことが必要です。

PBACの実施において、このバランスを達成するために、以下の指針を考慮しましょう：

@row
### Build Reusable Components

Managing abstraction in PBAC means isolating parts of your policies that may be applicable to other policies. The most obvious place where this applies is with user segmentation.  
  
For example, if you are constructing a policy to say that:

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **Object** |     | **Action** |     | **Subject** | **Context** |
| User profiles | may be | Updated | by  | Business managers | For full-time employees |

“Business managers” and “full-time employees” are very likely to be used again in other policies. Thus, creating a definition for these segments that can be used by one or more policies is wise.

The ideal way to avoid these definitions becoming too granular and rigid is through access management system implementations that allow for set logic - particularly intersections (membership in set A AND set B), unions (membership in set A OR set B), and complements (membership in set A, BUT NOT set B).

To expand on the previous example, if the policy above requires the following update:

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **Object** |     | **Action** |     | **Subject** | **Context** |
| User profiles | may be | Updated | by  | Business managers  <br>at the Detroit office | For full-time employees  <br>_**at the Detroit office**_ |

The best way to solve this problem is usually [^4] to keep definitions of “business managers” and “full-time employees” and add a third: “Detroit office.”  The “Detroit office” definition can then be used to update the subject of your policy (granting access to the intersection of “business managers” and “Detroit office”) as well as a context variable (scoping that access to the intersection of “full-time employees” and “Detroit office”).

This approach makes it possible to achieve the same ease of assigning a permission to a group of individuals as you might in RBAC, with the benefits of avoiding interdependence between permissions, being able to cleanly segment objects as well as subjects, and supporting specificity through permission contexts (such as user groups, device identifiers, IP address ranges, or document classifications).

@column
### 再利用可能なコンポーネントを構築する

PBACで抽象化を管理するということは、他のポリシーに適用可能なポリシーの一部を分離することを意味します。これが適用される最も明白な場所は、ユーザーのセグメンテーションである。

例えば、以下のようなポリシーを構築している場合：

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **オブジェクト** |     | **アクション** |     | **主体** | **コンテキスト** |
| User profiles | may be | Updated | by  | Business managers | For full-time employees |

「Business managers」と「full-time employees」は、他のポリシーで再び使用される可能性が非常に高いです。したがって、これらのセグメントの定義を作成し、1つまたは複数のポリシーで使用できるようにすることが賢明です。


これらの定義があまりに細かくなったり、あまりにも硬直であったりすることを避ける理想的な方法は、セットロジックを可能にするアクセス管理システムの実装です。特に、交差（集合A AND 集合Bのメンバー）、結合（集合A OR 集合Bのメンバー）、補集合（集合Aのメンバー、集合Bのメンバーでない）です。

先述の例を拡張し、上記の要件からポリシーで次のように更新します：

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **オブジェクト** |     | **アクション** |     | **主体** | **コンテキスト** |
| User profiles | may be | Updated | by  | Business managers  <br>at the Detroit office | For full-time employees  <br>_**at the Detroit office**_ |

この問題を解決する最善の方法は、通常 [^4] 「Business manager」と「full-time employees」の定義を維持し、3番目の定義として「Detroit office」を追加することです。「Detroit office」の定義は、ポリシーの主体（「business managers」と「Detroit office」の交差へのアクセス権の付与）とコンテキスト変数（そのアクセス権を"「full-time employees」と「Detroit office」の交差に限定する）を更新するために使用することができます。

このアプローチにより、RBACと同様に、個人グループへの権限付与が容易になり、権限間の相互依存を避け、オブジェクトと主体を明確にセグメント化し、権限コンテキスト（ユーザーグループ、デバイス識別子、IPアドレス範囲、文書分類など）による特異性をサポートする利点があります。

@row
### Facilitate Governance and Audit

A good access control system will allow auditors and business owners engaged in access governance to understand existing precedents in organizational access controls, analyze how they may need to be extended or modified, and ascertain the business impact of proposed changes.

When designing a PBAC system, it is important to make sure that subjects, actions, objects, and contexts are stored in a way that makes it straightforward to report on access from any of these perspectives. Business owners and auditors should have easy access to reports that answer questions about access users have, users able to access resources of interest, and allowable contexts for any actions defined for a resource.

The expressiveness of PBAC permissions makes it realistic to define all access considerations within policies. This flexibility is advantageous over implementing additional security measures (such as IP restrictions) outside of an organizational access control system. It allows for a single source of truth about circumstances under which access is allowed.

Being able to report on permissions in this way facilitates the examination of current rules for access to a resource. Good reporting may also include users who currently meet these criteria. Though PBAC is often used in federated contexts where identity (and other contextual) information for all potential users is not available to the resource administrator, such user reports can be helpful for spot-checking, especially in the context of a proposed change. Reports on who would gain or lose access under a proposed policy support business owners and auditors in refining controls to best facilitate organizational needs and security.

**Embrace States over Events**  
  
Business processes are often developed with flowcharts, which are focused on events. This often leads to access management systems that are implemented on events that mimic flowcharts, such as assigning access when a new employee is hired.  
  
Being based on observable attributes, PBAC policies tend to be more focused on states, such as an employee’s current position. This offers several advantages:

*   **Fewer states than events:** Access provisioning that is triggered when an employee first enters a position may need to account for nuances between external hires, internal transfers, and promotions. Unexpected events may occur, such as a canceled termination. Rather than tracking all potentially relevant business events, an access policy can simply apply to anyone currently holding the position.
    
*   **Local process changes:** Access management teams are much more likely to be informed of changes to relevant states (e.g., employment, company policy, business functions) than to changes to events (e.g., how many processes can be used to hire staff, changes to the company network, infrastructure upgrades, etc.).  
      
    When departmental processes shift in ways that affect the detection of events driving access, access management teams become responsible for investigating the resulting inconsistencies and may not be confident that their systems are functioning as intended.
    
*   Events occur at a point in time, which makes them more difficult to audit for appropriateness. For example, someone might have access through a legacy process that has since been revised (and should retain access) or because a deprovisioning was attempted (and should lose access) but was not completed. Without a current policy to compare against, it becomes very difficult to determine whether existing permissions are appropriate, further eroding trust in the system.  
      
    Because states are continuously observable, compliance with policies defined by state can be easily validated, and the impact of proposed changes to such policies can be easily measured.
    

To workshop access rules that can generate robust PBAC policies, consider dropping the flowchart arrows and working only with circles representing conditions. Arranging these circles as a Venn or Euler [^5] diagram allows for a discussion of acceptable conditions for access that will result in cleaner and more robust policies.

@column
### ガバナンスと監査を促進する

優れたアクセス制御システムでは、アクセスガバナンスに携わる監査人やビジネスオーナーが組織のアクセス制御における既存の前例を理解し、それらをどのように拡張または変更する必要があるかを分析し、提案された変更がビジネスに与える影響を確認することができます。

PBACシステムを設計するときは、主体、アクション、オブジェクトおよびコンテキストが、これらの観点からアクセスに関するレポートを簡単に作成できる方法で格納されていることを確認することが重要です。ビジネスオーナーと監査人は、ユーザーが持っているアクセス権、関心のあるリソースにアクセスできるユーザーおよびリソースに対して定義されたアクションに許可されるコンテキストに関する質問に答えるレポートに簡単にアクセスできべきです。

PBACの権限の表現力により、ポリシー内ですべてのアクセス権に関する考慮事項を定義することが現実的になります。この柔軟性は、組織のアクセス制御システムの外部に追加のセキュリティ対策（IP制限など）を実装するよりも長所があります。PBACは、アクセスを許可する状況について、信頼できる唯一の情報源を提供します。

この方法で権限について報告できると、リソースへのアクセス権に関する現在のルールの調査が容易になります。優れたレポートには、現在これらの基準を満たしているユーザーも含まれる場合があります。PBACは、リソース管理者が利用できないすべての潜在的なユーザーのアイデンティティ（およびその他のコンテキスト）情報のフェデレーションコンテキストでよく使用されますが、そのようなユーザーレポートは、特に提案された変更のコンテキストでのスポットチェックに役立ちます。提案されたポリシー下で、誰がアクセス権を取得、または失うかに関するレポートは、組織のニーズとセキュリティを最大限に促進するために管理を改善する際に、ビジネスオーナーと監査人をサポートします。

**イベントよりも状態を受け入れる**  
  
ビジネスプロセスは、多くの場合、イベントに焦点を当てたフローチャートで開発されます。多くの場合、新規従業員の採用時にアクセス権を割り当てるなど、フローチャートを模倣するイベントを実装されるアクセス管理システムにつながります
  
PBACポリシーは、観察可能な属性に基づくことから、従業員の現在の役職などの状態により着目する傾向があります。これにはいくつかの利点があります：

*   **イベントより状態のほうが少ない**：従業員が最初に役職に就いたときに引き起こされるアクセスプロビジョニングでは、外部採用、内部異動および昇進の微妙な違いを考慮する必要があるかもしれません。解雇のキャンセルなど、予期しないイベントが発生する可能性があります。関連する可能性のあるすべてのビジネスイベントを追跡するのではなく、アクセスポリシーは現在その役職にあるすべての人に単純に適用できます。
    
*   **ローカルプロセスの変更**：アクセス管理チームは、イベント（例: スタッフを雇用するために使われうるプロセスの数、会社のネットワークの変更、インフラストラクチャのアップグレードなど）の変更よりも、関連する状態（例: 雇用、会社のポリシー、ビジネス機能）の変更について通知される傾向がかなり多いです。
      
    部門のプロセスがアクセス権を駆動させるイベントの検知に影響を与える方法で変化すると、アクセス管理チームは結果として生じる不整合を調査する責任を負うようになり、システムが意図したとおりに機能していると確信できない場合があります。
    
*   イベントはある時点で発生するため、適切かどうかの監査がより困難になります。例えば、誰かが。改訂された（アクセス権を維持するはず）従来のプロセスを使ったり、デプロビジョニング（アクセス権を失うはず）が完了しなかったために、アクセスができる可能性があります。比較する現在のポリシーがなければ、既存のアクセス許可が適切かどうかを判断することが非常に難しくなり、システムに対する信頼がさらに損なわれます。
      
    状態は継続的に観測可能であるため、状態によって定義されたポリシーに対する準拠は簡単に検証でき、そのようなポリシーに対して提案された変更の影響は簡単に測定できます。    

堅牢なPBACポリシーを生成できるアクセスルールを作成するには、フローチャートの矢印を削除し、条件を表す円のみを使用することを検討してください。これらの円をベン図またはオイラー図 [^5] として配置すると、よりクリーンで堅牢なポリシーにつながるアクセスの許容条件について議論できます。

@row

|     |     |
| --- | --- |
| **Event-based Permission Design** | **State-based Permission Design** |
| **Looks like:** Flowcharts  <br>  <br>**Results in:** Rigid and sequential workflows, point-in-time validation, complicated deprovisioning logic. | **Looks like:** Overlapping circles<br><br>**Results in:** Flexible and parallel workflows, continuous validation, harmony between provisioning and deprovisioning. |
| ![](/assets/images/idpro_bok/event-based.jpg) | ![](/assets/images/idpro_bok/state-based.jpg) |

@row
### **Support Separation of Concerns**

More advanced guidance around PBAC may include references to standards such as OASIS’ eXtensible Access Control Markup Language (XACML) [^6] . Such standards can be particularly useful when it is desirable to maintain separation between components of a PBAC system, such as federated systems, or when policies are based on sensitive data.  
  
Consider the example of a scientific instrument subject to federal law requiring all users to be either a citizen or legal permanent resident of their country, and additionally with a clean background check performed within the last three years. To enforce this policy without exposing sensitive information like citizenship, immigration status, and background check results to the instrument, the managing organization could implement a separation of policy evaluation and policy enforcement such that the source systems for this data send the instrument a compliance status rather than the raw information needed to make a local access decision. In federated contexts, similar approaches are useful for reducing sensitive data exchange across organizational boundaries.  
  
@column
### **関心の分離をサポートする**

PBACに関するより高度なガイダンスとしては、OASISのeXtensible Access Control Markup Language（XACML） [^6] のような標準仕様があります。このような標準仕様は、フェデレーションシステムなどPBACシステムのコンポーネント間の分離を維持することが望ましい場合や、機密データに基づくポリシーの場合に特に有用です。
  
連邦法の適用を受ける科学機器で、すべてのユーザーが自国の市民か永住権保持者であり、さらに過去3年以内にクリーンなバックグランドチェックを受けていることを要求する例を考えてみましょう。このポリシーを、市民権、移民のステータス、バックグラウンドチェックの結果のような機密情報を機器にさらすことなく実施するため、管理組織はポリシー評価とポリシー実施を分離し、こデータの情報源となるシステムがローカルアクセス決定に必要な生の情報ではなく、コンプライアンスステータスを機器に送信するようにできます。
  
@row
## Conclusion

Access control systems promote and implement an organization’s access control strategy as changes occur in users, personnel, responsibilities, organizational structure, and legal obligations. Most failures with access management are due to a system implementation that is too manual to scale or too brittle to adapt to changing business needs without costly and time-consuming re-architecture efforts.

While it is common to try to optimize access control systems for efficiency in _granting_ access, a truer measure of a robust access control system is how reliably it can _revoke_ access. Policy-based access controls support the security principle of least privilege by offering logical symmetry between access assignment and revocation. Defining policy for access allows access to be dynamically evaluated for validity and automatically revoked or reported as soon as that access becomes invalid under current policy.

Developing access controls from a resource-first perspective and adding a notion of context to these controls allows PBAC systems to maximize resource security over convenience of access assignment. While these systems can initially be more complex than other approaches, the atomic nature of policies and their relative resilience against the buildup of legacy permissions makes for a system that is much more maintainable over time as compared to more limited rule-based access management systems like RBAC.

@column
## 結論

アクセス管理システムは、ユーザー、担当者、責任、組織構造や法的義務などの変化に応じて、組織のアクセス管理戦略を推進し、実装します。アクセス管理の失敗のほとんどは、システムの実装がスケールするには手作業が多すぎる、あるいは、コストと時間のかかる再設計をせずにビジネスニーズの変化に対応できないほど脆弱であることに起因しています。

アクセス制御システムは、アクセス権を効率的に __付与する__ ために最適化しようとするのが一般的ですが、堅牢なアクセス制御システムの真の指標は、いかに確実にアクセス権を __取り消す__ ことができるかということです。ポリシーベースアクセス制御は、アクセスの割り当てと取り消しの間に論理的な対称性を持たせることで、最小特権のセキュリティ原則をサポートします。アクセスに対するポリシーを定義することで、アクセスの有効性を動的に評価し、そのアクセスが現在のポリシーでは無効となった時点で自動的に取り消すか、報告することができます。

リソースファーストの観点からアクセス制御を発展させ、これらの制御にコンテキストの概念を加えることで、PBACシステムはアクセス割り当ての利便性よりもリソースの安全性を最大限に高めることができます。これらのシステムは、当初は他のアプローチよりも複雑になる可能性がありますが、ポリシーの基本的な性質と、過去の権限の蓄積に対する相対的な回復力により、RBACのような限定的なルールベースのアクセス管理システムと比較して、長期にわたってより保守性の高いシステムとなります。

@row
## Author Bio

Mary McKee began her career as a web application developer, eventually specializing in and leading teams dedicated to maturing processes in Identity Management and Cybersecurity. She now works as Senior Director of Engineering at Cirrus Identity.

Acknowledgments  
The author would like to thank André Koot and Andrew Hindle for their thoughtful responses to earlier versions of this article, and Heather Flanagan, Christienna Fryar, Dave Wible, and Mary Ellen Wible for their feedback and support with its development.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2023-10-27 | V3 published; clarification to Embrace States over Events, Support Separation of Concerns, and author bio |
| 2022-06-03 | V2 published; Clarified scope as an introductory article; replaced section on static access controls; removed section on privacy |
| 2021-04-19 | V1 published |

- - -

[^1]:  “Least Privilege,” [_https://us-cert.cisa.gov/bsi/articles/knowledge/principles/least-privilege_](https://us-cert.cisa.gov/bsi/articles/knowledge/principles/least-privilege) (accessed February 10, 2020) 
    
[^2]:  “Role-based access control,” [_https://en.wikipedia.org/wiki/Role-based\_access\_control_](https://en.wikipedia.org/wiki/Role-based_access_control) (accessed February 10, 2020) 
    
[^3]:  “Attribute-based access control,” [_https://en.wikipedia.org/wiki/Attribute-based\_access\_control_](https://en.wikipedia.org/wiki/Attribute-based_access_control) (accessed February 10, 2020) 
    
[^4]:  The examples in this section are meant to illustrate optimizing for set math capability within a context where both the identity provider (or user attribute store) and the service provider (or resource to be protected) exist within a common environment, and does not extend to federated contexts where a service provider may be interacting with one or more externally controlled identity providers. It is, however, worth noting that PBAC (/ABAC/CBAC) can easily accommodate these externalities. 
    
[^5]:  “Euler diagram,” [_https://en.wikipedia.org/wiki/Euler\_diagram_](https://en.wikipedia.org/wiki/Euler_diagram) , (accessed February 25, 2020) 
    
[^6]:  “eXtensible Access Control Markup Language (XACML) Version 3.0 Plus Errata 01,” [https://docs.oasis-open.org/xacml/3.0/errata01/os/xacml-3.0-core-spec-errata01-os-complete.pdf](https://docs.oasis-open.org/xacml/3.0/errata01/os/xacml-3.0-core-spec-errata01-os-complete.pdf) (accessed May 20, 2022) 
