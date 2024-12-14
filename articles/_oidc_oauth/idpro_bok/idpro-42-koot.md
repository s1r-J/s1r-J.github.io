---
layout: columns
title: Introduction to Access Control (v4)
permalink: /docs/oidc_oauth/idpro_bok/42
date: 2024-09-09
modify_date: 2024-12-07
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "アクセス制御"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/42/](https://bok.idpro.org/article/id/42/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

As the name implies, Identity and Access Management (IAM) is split into two functions: managing identity information and performing access control. Arguably, if there was no access control requirement there would be no need for identity management. It is therefore the focus for IAM professionals. At its core, access control is ensuring users are authenticated to access protected resources. This is accomplished by managing user entitlements and satisfying the requirements of relying applications so that users can only access the systems and information they are entitled to access. This article looks at the history of access management, the expected current functionality, and the trends to be expected.

Keywords: Access Control, Authorization, Governance, Risk, Authentication, Future

@column
## 概要

名前が示すとおり、アイデンティティとアクセス管理（IAM）は2つの機能に分けられます：アイデンティティ情報の管理とアクセス制御の実行。おそらく、アクセス制御の要件が存在しない場合、アイデンティティ管理も必要がありません。つまり、アクセス制御はIAM専門家の焦点です。アクセス制御の核心は、保護されたリソースへのアクセスのためにユーザーを認証することを保証することです。ユーザーのエンタイトルメントを管理し、リライングアプリケーションの要件を満たすことで、ユーザーがアクセス権限のあるシステムおよび情報にだけアクセスすることで実現されます。本稿では、アクセス管理の歴史、現在期待される機能と今後期待されるトレンドについて見てきます。

Keywords: アクセス制御、認可、ガバナンス、リスク、認証、将来

@row
By André Koot

© 2022 IDPro, André Koot

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction

Access control, as a concept, has a long history. But in order to investigate the current challenges and solutions, let’s start by evaluating a very old, traditional model of classified government documents.

Information in documents stored in files should not typically be accessible to everyone. The information may be classified, and only people with a required clearance level should be able to access classified files. In a physical form, this control is relatively simple: a folder with highly classified information is visually classified by a ‘Top Secret’ or ‘For Your Eyes Only´stamp. [^1]

But this simple example already addresses different fundamental concepts of security.

First, there’s the information itself. The information can be classified as Top Secret, but that must be defined by someone with the correct level of authority, like the owner of the information, the document, or the folder. Then, it must be clear what the impact of the classification level is; the classification level is needed to differentiate different levels of access to and usage of the information. The owner of the folder will probably have some guidance as to what levels of classification can be applicable and what type of user can get access.

Second, there is the clearance level of an actor, the user of the information. In this case, the secret service agent will have been identified and vetted to be trusted in such a way that access to different security levels of information is allowed.

Third, the classification level and the clearance level will have to be mapped in order to ensure that only the person with the correct security clearance level can access the classified information. The owner will classify a document and will accept that a specific security level can only be accessed by a pre-defined trust level of an agent.

And fourth: before giving the folder to the secret service agent, the person who is responsible for storing and retrieving the file in an archive (the file manager or access controller) must verify if the agent who requests the file is in fact the rightful user. The access controller will, therefore, try to identify the agent; the agent has to prove the right to access. This verification can be done by showing the secret service badge and a signed letter to prove that the agent has permission to access the folder. The file manager will, of course, also have to validate that the signature on the letter is correct.

Only after these responsibilities have been fulfilled will the folder be handed over to the secret service agent. The hand-over is then registered in a journal.

The access controller will always oversee the access, and that’s been made easy by checking the stamp on the folder. Theft of information—e.g., data leakage—is also quite physical in this example: the folder is removed. A folder with the 'Top secret' stamp should also not be found lying around unobserved.

In this scenario, access control is quite simple: you can literally observe access infractions. Access is granted by physically handing over the folder to a person with the corresponding clearance level, indicated by a personal badge, and may be enforced further by restricting access to a specific location.

We can see the following topics:

1.  Classification of information: this is an aspect of risk management
    
2.  Classification of users: this is an aspect of identity management
    
3.  Authorization mapping: this belongs to authorization management
    
4.  Authentication: this verification is part of both identity management and access management
    
5.  Access granted: this is access control
    

Since the advent of the computer, there has been a need to control access to systems, documents, and other protected resources. In the early era of computers, processes analogous to the old spy movie era were used to model access control mechanisms. Concepts like ‘owner of a resource’ and ‘reader of a resource’ were used. Programmers developed access control mechanisms like Discretionary Access Control (DAC) (“you may never bypass the access controller,” a feature that can still be found in the Windows NTFS file system) and Mandatory Access Control (MAC) (“you can only access the data in a specific location” such as a dedicated workstation in a specific room). [^2] , [^3] The fast growth of information technology resulted in a growing need to develop and improve access control. The increase in the number of users, the number of systems, and the exponential growth of the information processed makes it evident that the paper world metaphor is not sustainable in the digital world.

It was soon realized that the concept of trust levels—e.g., managing the clearance level of an individual document reader—is hard to implement. Because so many actors are playing along and there is no longer a physical security control in place (you cannot see the red lint). Instead, there can even be multiple copies of a folder or file in multiple locations, and theft no longer means that the data is gone, but data will probably be copied without the consent of the owner. What was physically easy to implement is not easy to implement in the digital world. But the lessons learned in identification, authentication, authorization, access control, logging, and auditing, have been kept.

Access to information, data, services, and systems, as well as access to physical locations, is governed by security policies. These security policies must be formalized and need to be enforced by the owner of the resource. In doing so, the owner will try to manage the risk involved in access, such as the risk of abuse of information, data leakage, theft, fraud, and other security threats. In order to be in control, the owner needs to have the assurance of the level of security capable of being achieved by the security controls that have been put in place.

Apart from the concepts of access control, ownership in itself is a complex topic. Looking at the concept of data ownership, many criteria to establish ownership can be identified. Someone can be the owner of information because:

*   They created the data.
    
*   They funded the data processing facility.
    
*   The data is about this person (e.g., a medical record of a patient)
    

There can be many more criteria to identify the owner, but this is part of data governance and out of scope for this article. In the case of medical files, the object, the patient, has several inherent rights to the data, making this person partly accountable for the access decision.

@column
## 導入

概念としてのアクセス制御には長い歴史があります。しかし、現在の課題と解決策を調査するために、まず、非常に古い伝統的な政府の機密文書のモデルを評価することから始めましょう。

ファイルに保存されている文書の情報は、通常、誰もがアクセスできるものではありません。情報は機密情報である可能性があり、必要な機密情報の取り扱い許可のレベルを持つ人だけが機密ファイルにアクセスできるようにすべきである。物理的な形式では、この制御は比較的簡単です：高度に機密化された情報が含まれるフォルダは、「トップシークレット」または「フォーユアアイズオンリー」のスタンプが押されています。 [^1]

しかし、この単純な例では、すでに異なるセキュリティの基本的な概念を扱っています。

まず、情報そのものです。情報をトップシークレットに分類することはできますが、情報・文書・フォルダの所有者など、適切なレベルの権限を持つ人が定義しなければなりません。そして、分類レベルがどのような影響を与えるかを明確にしなければなりません；分類レベルは、情報へのアクセスレベルや情報の使用の違いを区別するために必要です。フォルダの所有者は、どのようなレベルの分類が適用可能か、どのようなタイプのユーザーがアクセスできるかについて、おそらく何らかのガイダンスを持っているでしょう。

第二に、情報の利用者であるアクターのクリアランスレベルです。この場合、シークレットサービスのエージェントは、異なるセキュリティレベルの情報へのアクセスが許可されるような方法で、信頼されるように識別され、審査されているでしょう。

第三に、正しいセキュリティクリアランスレベルを持つ人物のみが機密情報にアクセスできるようにするため、分類レベルとクリアランスレベルをマッピングする必要があります。所有者はドキュメントを分類し、エージェントの事前定義された信頼レベルによってのみ特定のセキュリティレベルにアクセスできることを受け入れます。

そして第四に、シークレットサービスのエージェントにフォルダを与える前に、アーカイブにファイルを保存し、取り出す責任を負う人（ファイルマネージャまたはアクセスコントローラー）は、ファイルを要求するエージェントが実際には正当なユーザーであるかどうかを検証しなければなりません。したがって、アクセスコントローラーはエージェントを特定しようとします；エージェントはアクセス権を証明する必要があります。この検証は、エージェントがそのフォルダにアクセスする権限を持っていることを証明するために、シークレットサービスのバッジと署名入りの手紙を見せることで実施できます。ファイル管理者は、もちろん、手紙の署名が正しいことを検証しなければなりません。

これらの責任を果たした後、フォルダーはシークレットサービスエージェントに引き渡されます。そして、引き渡しはジャーナルに記録されます。

アクセスコントローラーが常にアクセスを監視し、フォルダのスタンプをチェックすることでアクセスを容易にすることができました。この例では情報の窃取、例えばデータ漏洩、も非常に物理的です：フォルダが削除されます。「トップシークレット」スタンプのあるフォルダが。人目につかずに落ちていることを見つけることもできないはずです。

このシナリオでは、アクセス制御は非常に単純です：文字通りアクセス違反を監視することができます。アクセスは、個人バッジで示されたクリアランスレベルに対応する人物に物理的にフォルダを渡すことで許可され、さらに特定の場所へのアクセスを制限することで実施することができます。

以下のようなトピックを見ることができます：

1.  情報の分類：これはリスク管理の一側面です
    
2.  ユーザーの分類：これはアイデンティティ管理の一側面です
    
3.  認可マッピング：これは認可管理に属します
    
4.  認証：この検証は、アイデンティティ管理とアクセス管理の両方の一部です
    
5.  アクセス許可：これはアクセス制御です
    

コンピュータの登場以来、システム、文書、その他の保護されたリソースへのアクセスを制御する必要性が生じてきました。コンピュータの初期の時代には、昔のスパイ映画の時代に類似した処理がアクセス制御機構のモデルとして使われていました。「リソースの所有者」「リソースの閲覧者」といった概念が使われｍした。プログラマーは、任意アクセス制御（DAC）（「アクセス制御装置を決してバイパスしてはならない」、WindowsのNTFSファイルシステムに今でも見られる機能）や強制アクセス制御（MAC）（「特定の部屋の専用ワークステーションなど、特定の場所でしかデータにアクセスできない」）などのアクセス制御機構を開発しました。 [^2] , [^3] 情報技術の急速な発展により、アクセス制御の開発、改善の必要性が高まりました。ユーザー数の増加、システム数の増加、処理する情報の指数関数的な増加により、紙の世界の比喩がデジタル世界では持続不可能であることが明白になったのです。

すぐに、信頼レベルの概念 (個々のドキュメント閲覧者のクリアランスレベルの管理など) を実装することは困難であることがわかりました。多くのアクターが一緒に作業しており、物理的なセキュリティ制御がなくなっているためです (赤い線は表示されません) 。代わりに、フォルダまたはファイルの複数のコピーが複数の場所に存在する可能性があり、窃取はデータが失われたことを意味するのではなく、所有者の同意なしにデータがコピーされる可能性があります。物理的に簡単に実行できることを、デジタルの世界で実行するのは簡単ではありません。ただし、識別、認証、認可、アクセス制御、ロギングおよび監査で学んだ教訓は維持されています。

情報、データ、サービスおよびシステムへのアクセス、および物理的な場所へのアクセスは、セキュリティポリシーによって管理されます。これらのセキュリティポリシーは形式化する必要があり、リソースの所有者によって適用される必要があります。これにより、所有者は情報の悪用、データ漏洩、窃取、詐欺およびその他のセキュリティ上の脅威のリスクなど、アクセスに関連するリスクを管理しようとします。コントロールされるためには、所有者は導入されたセキュリティ制御によって達成できるセキュリティレベルの保証を持っている必要があります。

Apart from the concepts of access control, ownership in itself is a complex topic. Looking at the concept of data ownership, many criteria to establish ownership can be identified. Someone can be the owner of information because:
アクセス制御の概念とは別に、所有権自体は複雑なトピックです。データ所有権の概念を見ると、所有権を確立するための多くの基準を特定できます。情報の所有者になれるのは、次のような理由からです：

*   彼らはデータを作成しました。
    
*   彼らはデータ処理施設に資金を提供しました。
    
*   データがこの人物に関するものです（例えば、患者の医療記録）
    

所有者を特定するための基準は他にも多くありますが、これはデータガバナンスの一部であり、この記事の範囲外です。医療ファイルの場合、対象である患者は、データに対するいくつかの生得権を有しており、アクセスの決定に対して部分的に責任を負います。

@row
### Terminology

*   Identification – Uniquely establish a user of a system or application.
    

*   Authentication – The ability to prove that a user or application is trustworthy and has the authority to access a protected resource by validating the credentials of an access requester (a user, a process, a system, or a thing).
    

*   Multi-factor Authentication (MFA) – An approach whereby a user’s identity is validated to the trust level required according to a security policy for a resource being accessed using more than one factor (something you know (e.g., password), something you have (e.g., smartphone), something you are (e.g., fingerprint).
    

*   Authorization – Determining a user’s rights to access functionality with a computer application and the level at which that access should be granted. In most cases, an ‘authority’ defines and grants access, but in some cases, access is granted because of inherent rights (like patient access to his/her own medical data).
    
*   Accountability – The obligation of a person to accept the results of one’s actions, be they positive or negative. This person is probably also a type of owner.
    
*   Protected Resource - A system, process, service, information object, or physical location that is subject to access control as defined by the owner of the resource and by other stakeholders, such as a business process owner or risk manager.
    
*   Access Control – Controlling who can have access to data, systems, services, resources, and locations. The ‘Who’ can be a user, a device or thing, or a service.
    
*   Access Governance – The assurance that all access has been given based on the correct decision criteria and parameters.
    
*   Access Policy – Definition of the rules to allow or disallow access to secured objects.
    
*   Access Requester – The person, process, system, or thing that seeks to access a protected resource.
    
*   Access Supplier – The component granting access to data, systems, and services after the access policy requirements (set in the Policy Administration Point) have been met by the Access Requester.
    
*   Policy Engine - It is a security component that validates whether an actor is allowed to access a protected resource, following the requirements in an access policy. A policy engine can be seen as a component that exists of a PDP and a PAP combined.
    
*   Policy Enforcement Point (PEP) – The authority that will only let an access requester connect to the access supplier if the Policy Decision Point allows it.
    
*   Policy Decision Point (PDP) – The policy engine validates access requests and provides attributes against the access policy (as defined in the Policy Administration Point).
    
*   Policy Administration Point (PAP) – The location where the different types of owners define the access policy.
    
*   Policy Information Point – The authority that refers to the (external) trusted providers of attributes that will be used in the Access Decision. An example is the credly.com service that administers Open Badges of certifications, such as CIDPRO™ or the Certified Information Systems Security Professional (CISSP).
    

@column
### 用語解説

*   識別 - システムやアプリケーションのユーザを一意に証明すること。
    

*   認証 - ユーザーまたはアプリケーションが信頼でき、保護されたリソースへアクセスする権限を有していることを、アクセスリクエスター（ユーザー、プロセス、システムやモノ）のクレデンシャルを検証することで証明する能力。
    

*   多要素認証（MFA） - アクセスするリソースに対して、セキュリティポリシーに従って要求される信頼レベルまで、1つ以上の要素（知っているもの（例：パスワード）、持っているもの（例：スマートフォン）、そうであるもの（例：指紋））を使ってユーザーのアイデンティティを検証するアプローチ。
    

*   認可 - コンピュータアプリケーションの機能にアクセスするユーザーの権利と、そのアクセスを許可すべきレベルを決定すること。ほとんどの場合、「権限」がアクセス権を定義し付与しますが、場合によっては、生得権（患者が自分自身の医療データにアクセスできるなど）によりアクセス権が付与されることもあります。
    
*   説明責任 - 自分の行為の結果を、それが肯定的なものであれ否定的なものであれ、受け入れる義務。この人もおそらく所有者の一種です。
    
*   保護されたリソース - システム、プロセス、サービス、情報オブジェクトまたは物理的な場所で、リソースの所有者およびビジネスプロセスオーナーやリスクマネージャーなどの他の利害関係者によって定義されたアクセス制御の対象。
    
*   アクセス制御 - データ、システム、サービス、リソース、場所に誰がアクセスできるかを制御すること。「誰」は、ユーザー、デバイスやモノ、またはサービスです。
    
*   アクセスガバナンス - すべてのアクセスが正しい判断基準やパラメータに基づいておこなわれたことを保証すること。
    
*   アクセスポリシー - 保護されたオブジェクトへのアクセスを許可または拒否するためのルールを定義すること。
    
*   アクセスリクエスター - 保護されたリソースにアクセスしようとする人、プロセス、システム、またはモノ。
    
*   アクセスサプライヤー - アクセスリクエスターが、アクセスポリシーの要件（ポリシー管理ポイントに設定）を満たした後、データ、システムおよびサービスへのアクセスを付与するコンポーネント。
    
*   ポリシーエンジン - アクターがアクセスポリシーの要件に従って保護されたリソースへのアクセスを許可されているかどうかを検証するセキュリティコンポーネント。ポリシーエンジンはPDPおよびPAPを組み合わせたコンポーネントとみなすことができます。
    
*   ポリシー実施ポイント（PEP） - ポリシー決定ポイントが許可した場合にのみ、アクセスリクエスターにアクセスサプライヤーへの接続を許可する権限。
    
*   ポリシー決定ポイント（PDP） - ポリシーエンジンは、（ポリシー管理ポイントに定義された）アクセスポリシーに照らして、アクセス要求を検証し、属性を提供すること。
    
*   ポリシー管理ポイント（PAP） - 異なるタイプの所有者がアクセスポリシーを定義する場所。
    
*   ポリシー情報ポイント - アクセス判断で使用される属性の（外部の）信頼できるプロバイダーを参照する機関。例として、CIDPRO™やCertified Information Systems Security Professional（CISSP）のような認定資格のオープンバッジを管理するcredly.comサービスがあります。
    

@row
### Acronyms

*   ABAC – Attribute-Based Access Control
    
*   ACL – Access Control List
    
*   AIAC – Artificial Intelligence-Supported Access Control
    
*   CBAC – Context-Based Access Control or Claims-Based Access
    
*   CIAM – Consumer Identity and Access Management
    
*   CRM – Customer Relationship Management
    
*   DAC – Discretionary Access Control
    
*   MAC – Mandatory Access Control
    
*   PBAC – Policy-Based Access Control
    
*   PAP – Policy Administration Point
    
*   PDP – Policy Decision Point
    
*   PEP – Policy Enforcement Point
    
*   RBAC – Role-Based Access Control or (less frequently) Rule-Based Access Control
    
*   ReBAC – Relation-Based Access Control
    
*   SCIM – System for Cross-domain Identity Management
    
*   SoD – Segregation of Duties
    

@column
### 略語

*   ABAC – 属性ベースのアクセス制御
    
*   ACL – アクセス制御リスト
    
*   AIAC – 人工知能対応のアクセス制御
    
*   CBAC – コンテキストベースのアクセス制御またはクレームベースのアクセス制御
    
*   CIAM – 消費者向けのアイデンティティとアクセス管理
    
*   CRM – 顧客関係管理
    
*   DAC – 任意アクセス制御
    
*   MAC – 強制アクセス制御
    
*   PBAC – ポリシーベースアクセス制御
    
*   PAP – ポリシー管理ポイント
    
*   PDP – ポリシー決定ポイント
    
*   PEP – ポリシー実施ポイント
    
*   RBAC – ロールベースアクセス制御または（頻度は低いが）ルールベースアクセス制御
    
*   ReBAC – 関係ベースアクセス制御
    
*   SCIM – クロスドメインアイデンティティ管理システム
    
*   SoD – 職務分掌
    

@row
## AAA: Authentication, Authorization, Accountability

Just as we showed in the classified document example above, in order to get access, a validated identity is key. The ideas behind this paradigm can be summarized by the concepts of AAA.

@column
## AAA: 認証、認可、説明責任

上記の機密文書の例で示したように、アクセス権を得るためには、検証されたアイデンティティが鍵となります。このパラダイムの背景にある考え方は、AAAという概念に要約されます。

@row
### Authentication

Authentication is the process of proving that the user with a digital identity who is requesting access is the rightful owner of that identity. It can be as simple as using a password or as complex as providing a digital certificate. Both the Access Supplier and the Access Requester must be able to manage and consume the results of the authentication process.

@column
### 認証

認証とは、アクセスを要求しているデジタルアイデンティティを持つユーザーが、そのアイデンティティの正当な所有者であることを証明するプロセスです。認証には、パスワードのような単純なものから、デジタル証明書を提供するような複雑なものまであります。アクセスサプライヤーとアクセスリクエスターの両方が、認証プロセスの結果を管理および消費できる必要があります。

@row
#### Challenge - Response

The user might provide proof of this rightful usage by providing a secret that only the access requester and the access supplier know, like a secret code or a password. The underlying mechanism is called Challenge-Response. The Access Supplier challenges the Access Requester to prove his or her identity, and the subject will have to respond in the way the Access Supplier expects. The simplest way to do a challenge-response is by asking for a password or pin-code. But also, the CAPTCHA feature on many websites is a form of challenge-response: prove that you are a human being. [^4]

@column
#### チャレンジ - レスポンス

ユーザーは、アクセスリクエスターとアクセスサプライヤーだけが知っている秘密コードやパスワードのような機密情報を提供することで、この正当な利用の証明をおこなうかもしれません。この基礎となるメカニズムは、チャレンジ・レスポンスと呼ばれます。アクセスサプライヤーはアクセスリクエスターに自分のアイデンティティを証明するよう要求し、対象者はアクセスサプライヤーが期待する方法で応答する必要があります。チャレンジ・レスポンスをおこなう最も簡単な方法は、パスワードまたはPINコードの入力を求めることです。また、多くのWebサイトにあるCAPTCHA機能もチャレンジ・レスポンスの一種です：この場合、あなたが人間であることを証明します。 [^4]

@row
#### Knowledge – Possession - Being

But other than a CAPTCHA challenge, a known secret can be shared. It may not be sufficient to assure the rightful access because by sharing a password or by finding a password lying around (on a piece of paper, for instance), others may pretend to be the rightful owner. This weakness of the known-secret model means that the trust level of an access requester who uses just a password may not be sufficient for some applications.

After identification and even authentication, there is a degree of uncertainty in identifying the rightful owner, which should result in further evaluation of the level of access. A low level of confidence may be enough to give access to public information, but it will probably be insufficient to provide access to classified information.

Adding more proof of identity can be done by demanding more specific and unique identifiers. These more trusted authentication means cannot be easily copied or easily shared or stolen (it is not impossible, but the cost of copying a secure physical token can be too high to make it economically unsound to forfeit). In practice, this is done by introducing additional factors, such as tokens, certificates, and biometric proof. Requesting these additional proofs of identity can be requested either at the start of a session at the first authentication or during a session after a previous low-trust authentication has been found insufficient for getting access to a secured resource. In this case, the low-trust access can be enhanced by performing a ‘step-up’ authentication, requiring additional factors: the first step during login could be using a password, and then a second higher-level step could involve the use of a token or biometric proof.

@column
#### 知識 – 所有 - 生体

しかし、CAPTCHAチャレンジ以外では既知の秘密を共有することができます。なぜなら、パスワードを共有したり、（例えば付箋紙に書かれた）パスワードを見つけたりすることで、他の人が正当な所有者のふりをする可能性があるからです。このような既知の秘密モデルの弱点は、パスワードだけを使用するアクセスリクエスターの信頼レベルが、一部のアプリケーションにとっては不十分である可能性があることを意味します。

識別と認証の後でも、正当な所有者の識別にはある程度の不確実性があり、アクセスのレベルをさらに評価する必要があります。低レベルの信頼は、公開情報へのアクセスを提供するのに十分かもしれませんが、機密情報へのアクセスを提供するにはおそらく不十分です。

身元確認をさらに追加するには、より具体的で一意の識別子を要求します。これらのより信頼できる認証手段は、簡単にコピーしたり、簡単に共有したり、盗んだりすることはできません（不可能ではありませんが、安全な物理的なトークンをコピーするコストが高すぎて、没収することが経済的に不健全になる場合があります）。実際には、トークン、証明書、生体認証などの追加的な要素を導入することでこれを実現します。これらの追加的な身元確認の要求は、セッションの開始時に最初の認証でおこなうか、保護されたリソースへのアクセス権を得るには、それまでの信頼性の低い認証では不十分であると判明した後にセッション中におこなうことができます。この場合、信頼性の低いアクセスは、追加要素を必要とする「ステップアップ」認証を実行することで強化できます：ログイン時の最初のステップではパスワードを使用し、その後の2つ目の高いレベルのステップではトークンまたはバイオメトリック証明を使用することができます。

@row
### Authorization

Authorization, often a synonym for the phrase access control, is the next step in getting access after the phase of authentication. It is the act of granting access to a specific resource, such as a computer application or a specific function within an application.

Authorization is closely related to the concept of authority. Someone, such as an owner, is accountable and, because of the ownership, is mandated to authorize others to access the protected resource. This accountability does not imply that the other person becomes the owner, but it does mean that several permissions, such as ‘read’ or ‘delete,’ can be executed. The owner stays accountable throughout the lifecycle of the data. Some of the tasks of the owner can be delegated to others in such a way that, for instance, a line manager may, within the boundaries set by the owner, grant read access to a resource to an employee.

@column
### 認可

認可は、しばしばアクセス制御という言葉と同義語であり、認証フェーズの後にあるアクセスを得るための次のフェーズです。コンピュータアプリケーションやアプリケーション内の特定の機能など、特定のリソースへのアクセスを許可するアクションです。

認可は、権限の概念と密接に関連しています。所有者のような誰かが説明責任を負い、所有者であるがゆえに、保護されたリソースに他者がアクセスすることを認可することが義務付けられています。この説明責任は、他者が所有者になることを意味するものではありませんが、「読み取り」や「削除」などのいくつかの権限を実行できることを意味します。所有者は、データのライフサイクルを通じて説明責任を負い続けます。所有者のタスクの一部は、他者に委任することができます。たとえば、ラインマネージャーが、所有者が設定した境界の中で、従業員にリソースへの読み取りアクセス権を付与することができるようになります。

@row
#### Mainstream Access Control Methods

Currently, many organizations have security policies embedded in various applications, operating systems, and networking components. These controls are implemented in the form of Access Control Lists (ACLs), Roles, and DAC business rules. But these controls have to be designed and implemented in every relevant component. And these controls have to be designed in a consistent manner. If, for instance, a Segregation of Duties (SoD) restriction is defined for a specific process, every system, application, platform, app, and network component must support the SoD rule. If one of the many components is lacking SoD control, then the organization is not in control.

This decentralized implementation of security policies makes it challenging to implement centrally managed organization-wide controls. It is likely that not all controls are similar and that the security policy and conformity must be verified for every system or platform access request.

@column
#### 主流のアクセス制御手法

現在、多くの組織では、さまざまなアプリケーション、オペレーティングシステムおよびネットワーキングコンポーネントにセキュリティポリシーが埋め込まれています。これらの制御は、アクセス制御リスト（ACL）、ロールおよびDACビジネスルールの形で実装されています。しかし、これらの制御は、関連するすべてのコンポーネントで設計され、実装される必要があります。そして、これらの制御は一貫した方法で設計される必要があります。例えば、特定のプロセスに対して職務分掌（SoD）制限が定義されている場合、すべてのシステム、アプリケーション、プラットフォーム、アプリ、ネットワークコンポーネントがSoDルールをサポートしなければなりません。数あるコンポーネントのうち1つでもSoDの制御が欠落していれば、組織は制御不能に陥ってしまいます。

このようにセキュリティポリシーの実装が分散しているため、一元管理された組織全体の統制を実施することが困難になっています。すべての制御が類似しているわけではなく、システムやプラットフォームのアクセス要求ごとにセキュリティポリシーと適合性を検証する必要があると思われます。

@row
#### Modern Access Control

In modern implementations of access control, a policy engine is used to evaluate access policies centrally, and policy enforcement should encompass the ‘risk level’ evaluation. The business process owner, or data owner, tasked with managing access risk, will define the policies for which they are accountable. In some cases, there are multiple ‘business owners,’ and each is responsible for their part of the corporate security policy. This assignment of business owners can result in continuously changing access control policies.

There is much development in this area, with applications no longer maintaining the ACLs of users. Instead, they rely on identity management authorization systems that will, based on one or more access policies, make the decision regarding a user’s access request. Different stakeholders in a company are responsible for different policies. All applicable policies must be evaluated before access is granted. This method of fine-grained access control is a type of MAC.

@column
#### 現代のアクセス制御

現代のアクセス制御の実装では、ポリシーエンジンがアクセスポリシーを一元的に評価するために使用され、ポリシーの施行は「リスクレベル」の評価を含めるべきです。アクセスリスクを管理する役割を担うビジネスプロセスオーナーまたはデータオーナーは、自らが責任を負うべきポリシーを定義します。場合によっては、複数の「ビジネスオーナー」が存在し、それぞれが企業のセキュリティポリシーの一部に対して責任を負うこともあります。このようにビジネスオーナーが割り当てられることで、アクセス制御ポリシーが継続的に変更される可能性があります。

この分野では多くの開発がおこなわれており、アプリケーションはもはやユーザーのACLをメンテナンスすることはありません。その代わりに、1つまたは複数のアクセスポリシーに基づいて、ユーザーのアクセス要求に関する決定をおこなうアイデンティティ管理認可システムに依存しています。企業内のさまざまなステークホルダーが、さまざまなポリシーに責任を負っています。アクセス権が付与される前に、適用されるすべてのポリシーが評価されなければなりません。このきめ細かなアクセス制御の方法は、MACの一種です。

@row
### Accountability

Accountability is a key responsibility in access governance. Making sure that every access decision is accounted for by an authorized person implies that ownership must be addressed. The owner must be informed about all activities under their control in order to be successfully accountable for the data under their stewardship.

Registering all activities in access control is an essential quality requirement. This record can vary in complexity from logging every authorization request (like granting or revoking authorizations or roles to and from people) to logging changes of authorizations within roles. The existence of this register is essential to be truly in control of access. The same is true for the identification and authentication process. There must be assurance from the part of the login mechanism, the operating systems, and the IAM solutions applied to make sure that every access request is validated.

@column
### 説明責任

説明責任は、アクセスガバナンスにおける重要な責任です。すべてのアクセス決定が認可された人によって説明されるということを確認することは、所有権に対処しなければならないことを意味します。所有者は、管理責任下にあるデータに対して説明責任を負うために、制御下にあるすべてのアクティビティについて通知を受けなくてはなりません。

アクセス制御にすべてのアクティビティを記録することは、重要な品質要件です。この記録の複雑さは、すべての認可要求のログ記録（人々に対する認可またはロールの付与またはその取り消しなど）から、ロール内の認可の変更のログ記録まで様々です。この記録の存在は、アクセスを真に制御するために不可欠です。同じことが識別および認証プロセスにも当てはまります。すべてのアクセス要求が検証されることを確認するために、ログインメカニズム、オペレーティングシステムおよび適用されるIAMソリューションの一部からの保証がなくてはなりません。

@row
### Specific Access Control Considerations

Access control is not only a business decision. Other considerations inform how this activity must take place, including how users will engage with the control mechanisms as well as legal implications for what is (and isn’t) required.

@column
### 特定のアクセス制御の考慮事項

アクセス制御は、ビジネス上の決定だけではありません。その他の考慮事項は、ユーザーが制御メカニズムにどのように関与するか、何が必要であるか（または必要でないか）についての法的影響などを含めて、このアクティビティをどのように実行しなければならないかを決めます。

@row
#### The Human Factor

The user who needs to cope with the security controls can themselves be a roadblock on the path toward effective ’control.’ User experience (UX) is a critical success factor in every information security project. If the security controls are too strict, users may be deterred, or they may try to circumvent the control. This avoidance on the part of the user is often seen in consumer access: if a customer portal is not built with a focus on the user, then consumers tend to go elsewhere. That is a missed opportunity, resulting in low conversion rates. Consumer Identity and Access Management (CIAM) solutions are developed to prevent this behavior.

The lessons learned in CIAM are also being implemented in workforce IAM: UX is starting to make an impact. For instance, if a user accesses a company intranet portal from their home location regularly in a prescribed way, like using a VPN, the access control system could validate this behavior as a factor in the authentication process. It could decide not to require the repeated use of multi-factor authentication since it is a trusted user making use of a known, trusted connection; it’s a well-known context resulting in better control of access.

@column
#### 人的要素

セキュリティ制御に対処する必要があるユーザー自身が、効果的な「制御」への道のりの障害になる可能性があります。ユーザーエクスペリエンス（UX）は、すべての情報セキュリティプロジェクトにおいて重要な成功要因となります。セキュリティ制御が厳しすぎると、ユーザーが抑止されたり、制御を回避しようとしたりする可能性があります。このユーザー側の回避は、多くの場合、消費者アクセスと見なされます：カスタマーポータルがユーザーに焦点を当てて構築されていない場合、消費者は別の場所に移動する傾向があります。これは機会を逃し、コンバージョン率の低下につながります。Consumer Identity and Access Management（CIAM）ソリューションは、この動きを防ぐために開発されています。

CIAMで学んだ教訓は、従業員IAMにも導入されています：UXは影響を与えはじめています。たとえば、ユーザーがVPNを使用するなど、所定の方法で自宅から会社のイントラネットのポータルに定期的にアクセスする場合、アクセス制御システムはこの動作を認証プロセスの一要素として検証できます。既知の信頼できる接続を使用する信頼できるユーザーであるため、多要素認証を繰り返し使用する必要がないことを決定できます；これはよく知られた状況であり、アクセスをより適切に制御できます。

@row
#### Legal Implications

Access control has historically been looked at as a way to support business processes and is part of a larger information security and risk mitigation policy. The question of legal implications directly tied to access control practices varies from business to business, from sector to sector, and from jurisdiction to jurisdiction. There is no unambiguous answer as to the direct legal requirement for most access control practices as these policies are often woven into a larger program that is driven in part by any number of laws, regulations, or standards. Part of the role of an access control program or system is to ensure that it is flexible enough to support the larger risk management programs of the business or organization. In this way, questions about legal requirements and compliance implications can be addressed organically, allowing the organization the confidence it needs to operate and move forward.

In separate articles in the IDPro BoK, different aspects of laws and regulations will be illustrated in more detail.

@column
#### 法的影響

アクセス制御は、歴史的にビジネスプロセスをサポートする方法と見なされており、より大きな情報セキュリティおよびリスク軽減ポリシーの一部となっています。アクセス制御のプラクティスに直接関連する法的影響の問題は、企業ごと、部門ごと、法域ごとに異なります。しばしば、これらの方針は多くの法律や規制、標準仕様によって部分的に推進されるより大きな計画に織り込まれるため、ほとんどのアクセス制御のプラクティスに対する直接的な法的要件について明確な答えはありません。アクセス制御プログラムまたはシステムの役割の一部は、企業または組織のより大きなリスク管理計画を支持するのに充分な柔軟性を確保することです。このようにして、法的要件とコンプライアンスへの影響に関する問題に組織的に対処できるため、組織は、組織を運営し前進するための自信を得ることができます。

IDPro BoKの別の記事では、法律と規制のさまざまな側面について詳しく説明しています。

@row
## Current state of Access Control

@column
## アクセス制御の現況

@row
### Mainstream Access Control Mechanisms

Several mechanisms support the implementation of access control. This section covers the more common ones: Access Control Lists (ACLs), Role-based Access Controls (RBACs), and Attribute-based Access Controls (ABACs).

@column
### 主流のアクセス制御メカニズム

アクセス制御の実装をサポートする機構はいくつかあります。このセクションでは、より一般的なものを取り上げます：アクセス制御リスト（ACL）、ロールベースアクセス制御（RBAC）、属性ベース制御（ABAC）です。

@row
#### Access Control Lists

Access control to a protected resource is based on the classification level of the resource. Every resource will be classified by the owner (or a delegated person) in order to define the security level of the resource. Based on the security level, security controls must be put in place to ensure the correct level of access. The access available, i.e., the permissions that can be granted, are also known as entitlements (fine-grained permissions to access resources). One of the earliest and best-known implementations of entitlements is by using ACLs In an ACL, the owner of the file defines what users can have what type of access: read, write, update, delete, whatever the owner accepts as usage. This concept is easy to understand and easy to manage for individual objects. And if the number of objects is limited, controlling access via ACL’s can be enough. But when the number of users and the number of objects grows, ACL’s can be a restricting factor.

Every owner of a file will need to define the ACL for the object. This distributed method of control implies that central control of access is non-existent. But, from an auditing perspective: it’s relatively simple to find out who has access to a protected resource since that is registered in the ACL of the resource.

The concept of ACLs will be explained in a future article in the BoK.

@column
#### アクセス制御リスト

保護されたリソースへのアクセス制御は、リソースの分類レベルに基づきます。すべてのリソースは、リソースのセキュリティレベルを定義するために、所有者（または委任された者）によって分類されます。セキュリティレベルに基づいて、正しいアクセスレベルを保証するためのセキュリティ制御が実行されなければならなりません。利用可能なアクセス、すなわち付与可能な権限は、エンタイトルメント（リソースへのアクセスに対するきめ細かい許可）とも呼ばれます。エンタイトルメントの最も古く、最もよく知られた実装の1つは、ACLの利用です。ACLでは、ファイルの所有者が、どのユーザーがどのような種類のアクセスをおこなえるかを定義します：読み取り、書き込み、更新、削除、所有者が使用と認めるものすべて。このコンセプトは理解しやすく、個々のオブジェクトの管理も簡単です。また、オブジェクトの数が限られている場合は、ACLによるアクセス制御で十分です。しかし、ユーザーの数やオブジェクトの数が増えてくると、ACLは制限要因になり得ます。

ファイルの所有者は全員、そのオブジェクトのACLを定義する必要があります。この分散制御の方法は、アクセスの中央制御が存在しないことを意味します。しかし、監査の観点から：リソースのACLに登録されているので、保護されたリソースに誰がアクセスしているかを調べるのは比較的簡単です。

ACLの概念については、今後BoKで解説していく予定です。

@row
#### Role-Based Access Control

Managing ACLs can be a tedious task. Managing access to resources on a user by user or entitlement by entitlement basis faces issues as populations grow. At some point, the issue of scale meant that a new access management approach was needed. RBAC is an approach of granting access to resources on a group level instead of on an individual level. In order to realize this, an intermediate component needs to be in place after that of the access controller. A role manager or a role owner has to be able to map the role of a user to an entitlement to a secured resource. This mapping looks easy enough, but in practice, this means that this person needs to work with different other responsible persons in an organization to make sure that the authorizations are not conflicting with the business processes and organizational structures of the organization. In the access governance article, this concept and the complexity connected with the governance model is further explained.

In the example of an internal company website, every company employee is made a member of a group called ‘Company Employees.’ The resource—in this case, the main page of the internal website—is secured in such a manner that access is granted only if a user is a member of this group. Another example is the line manager who can make a new employee member of the role account manager and behold, the access permissions connected to the role account manager, are available to the new employee. This non-individual oriented way of granting access makes managing access a lot easier.

A system owner can also create ‘roles’ within an information system to prevent the need for managing individual entitlements. The system owner of a Customer Relationship Management (CRM) system can define a role for ‘customer manager’ and group system authorizations (such as reading a customer record from a database or filling in a form) to that role.

In RBAC, we can identify a multilevel role model. On the one hand, we can identify the grouping of identities organizationally or hierarchically, defining organizational or business roles. On the other hand, there is a grouping of authorizations or permissions on an application function or platform level called system or application roles. Connecting organizational roles to application roles creates a very efficient way of granting and revoking authorizations. But it is also very easy to complicate authorization management by nesting groups: for instance, employees working on the service desk can be made members of the group ’ServiceDesk'. This group then could be made a member of the group Windows Administrators. By doing this, it will soon become hard to find out who has the authorizations of a Windows administrator. That would be not just the group of people who are members of the Windows Administrator role but also employees who are members of the role of ServiceDesk employee. This nesting can frustrate the insight by no small means; many IAM projects fail by the lack of un-nesting possibilities. Nesting also limits the auditability of RBAC environments; groups have to be un-nested in order to evaluate authorizations and potential conflicting authorizations.

Implementations, pros and cons, will be explained later in a future article about RBAC in the BoK.

@column
#### ロールベースアクセス制御

ACLの管理は退屈な作業です。ユーザーごとのリソースへのアクセス、またはエンタイトルメントベースのエンタイトルメントによるリソースへのアクセスの管理は、人口の増加に伴う問題に直面します。ある時点で、規模の問題は、新しいアクセス管理アプローチが必要であることを意味しました。RBACは、リソースへのアクセスを個人レベルではなくグループレベルで付与するアプローチです。これを実現するには、中間コンポーネントがアクセスコントローラのコンポーネントの後に配置されている必要があります。ロール管理者またはロール所有者は、ユーザーのロールを保護されたリソースへの資格にマップできる必要があります。このマッピングは簡単に見えますが、実際には、この担当者は組織内の他の責任者と協力して、認可がビジネスプロセスまたは組織の組織構造と競合しないようにする必要があります。アクセスガバナンスの記事では、この概念とガバナンスモデルと接続した複雑さについてさらに解説しています。

社内Webサイトの例では、すべての会社従業員が「会社従業員」というグループのメンバーになっています。リソース、この場合は内部Webサイトのメインページ、はユーザーがこのグループのメンバーである場合にのみアクセスが許可されるようにセキュリティで保護されます。別の例では、ラインマネージャーは新しい従業員をロールアカウントマネージャーにすることができ、注視しており、ロールアカウントマネージャーに関連付けられたアクセス許可を新しい従業員が利用できます。この個人指向ではないアクセスの付与方法により、アクセスの管理がはるかに簡単になります。

システム所有者は情報システム内に「ロール」を作成して、個々のエンタイトルメントを管理する必要がなくなるようにできます。カスタマーリレーションシップマネジメント（CRM）システムのシステム所有者は、「カスタマーマネージャー」のロールを定義し、そのロールに対してシステム認可（データベースからのカスタマーレコードの読み取りやフォームへの入力など）をグループ化することができます。

RBACでは、マルチレベルのロールモデルとみなすことができます。一方では、組織的または階層的なアイデンティティのグループ化とみなすことができ、組織的またはビジネス上の役割を定義することができます。また一方で、システムロールまたはアプリケーションロールと呼ばれる、アプリケーション機能またはプラットフォームレベルでの認可または権限のグループ化があります。組織ロールをアプリケーションロールに接続すると、認可の付与と失効について非常に効率的な方法が作成されます。しかし、グループをネストすることによって認可管理を複雑にすることも非常に簡単です：例えば、サービスデスクで作業する従業員をグループの「ServiceDesk」のメンバーにすることができます。その後、このグループをWindows管理者グループのメンバーにすることができます。これにより、Windows管理者の権限を持つ人を見つけることがすぐに難しくなります。これは、Windows管理者ロールのメンバーであるユーザーのグループだけでなく、ServiceDesk従業員ロールのメンバーである従業員でもあります。このネスティングは、少なからず見通しを妨げる可能性があります；多くのIAMプロジェクトは、ネスティング解除の可能性の欠如によって失敗します。ネストは、RBAC環境の監査可能性も制限します；グループは、認可と競合する可能性のある認可を評価するためにネストされていない必要があります。

実装、長所、短所については、BoKのRBACに関する今後の記事で後ほど説明します。

@row
#### Attribute-Based Access Control

ABAC builds on the RBAC model by introducing additional controls based on business logic. A major failing of the RBAC model is its static nature. Once an entitlement has been granted, it generally is always available to an end-user, until it is manually revoked. This longevity means that users wind up carrying access with them from role to role if proper cleanup actions are not taken. To address this, ABAC expands on the model, taking into consideration different characteristics of users and users’ attributes at the moment of determining if access should be granted. As a result, an access management system can make a decision based on the entitlements of a given user, as well as the time of day, the location of the user (e.g., on network or remote, geolocation based on IP address) the type of device (e.g., personal, organization owned, desktop or tablet), and other worker metadata. ABAC can be used both in real-time to control access at the time of the transaction, or passively controlling the assigned roles and entitlements based on user metadata. Both approaches require strong input and support from resource owners, Role managers, and people or organization managers to understand the needs of the user as well as additional support from analysts to help define the business logic.

For example: The Customer Relations Management process owner could define that everyone with the attribute ‘Business Role = Account manager’ can access the resource only if attribute ‘Allowed Time = defined office hours’. Multiple variations of this dynamic access control philosophy will be described later in a future IDPro BoK article.

@column
#### 属性ベースアクセス制御

ABACは、RBACモデルをベースに、ビジネスロジックに基づく追加の制御を導入したものです。RBACモデルの大きな欠点は、その静的な性質にあります。一旦エンタイトルメントが付与されると、手動で取り消されるまで、エンドユーザーは常にそのエンタイトルメントを利用できます。このような長期間性は、適切な後処理がおこなわれない場合、ユーザーがロールからロールへとアクセス権を持ち運ぶことになることを意味します。そこで、ABACはこのモデルを発展させ、アクセスを許可すべきかどうかを判断する時点で、ユーザーのさまざまな特性や属性を考慮するようにします。その結果、アクセス管理システムは、あるユーザーのエンタイトルメントだけでなく、時間帯、ユーザーの場所（ネットワーク上かリモートか、IPアドレスに基づくジオロケーションなど）、デバイスの種類（個人所有、組織所有、デスクトップ、タブレットなど）、その他の従業員のメタデータに基づいて判断することができるようになりました。ABACは、トランザクションの時点でアクセスを制御するリアルタイムでの利用と、ユーザーメタデータに基づいて割り当てられたロールとエンタイトルメントを制御するパッシブでの利用の両方が可能です。どちらのアプローチも、ユーザーのニーズを理解するために、リソースオーナー、ロールマネージャー、人または組織マネージャーからの強力なインプットとサポート、およびビジネスロジックの定義を支援するアナリストからの追加サポートが必要です。

例：顧客関係管理プロセスのオーナーは、属性「ビジネスロール = アカウントマネージャー」を持つ全員が、属性「許可時間 = 定められた営業時間」の場合にのみリソースにアクセスできると定義することができます。この動的アクセス制御の考え方の複数のバリエーションについては、将来のIDPro BoKの記事で述べます。

@row
## The Future Direction of Access Control

Access Control by means of ACLs and RBACs is relatively static; the combination between a user and his or her authorizations are set and do not vary easily, and other authorizations require changes. But people move between jobs, change devices, change location, or get new tasks in a new context. Also, the risk level assigned to a protected resource can change because of a change in context or a change in applicable laws and regulations. Relevant changes may include:

*   Extended organizations, internationalization, collaboration and federation, flexible workforce, meaning that in daily operations, people outside the scope of the traditional HR-operations may need to get access.
    
*   Moving data processing to the cloud - leading to the development of new protocols, such as SCIM (System for Cross-domain Identity Management (the first time the acronym was used, it was called Simple Cloud Identity Management, I suppose this was deemed too simple or restricting ☺). [^5]
    

*   New privacy regulations, such as the GDPR. [^6]
    
*   The usage of mobile apps, using modern protocols like OpenID Connect requires a flexible access control topology.
    

*   Enforcing end-user consent and control - developments like User-Managed Access (UMA). [^7]
    
*   Move to API-based access to micro-services - leading to new access management architectures based on protocols like OAuth2.
    

These restrictions and changes show that a more dynamic method for managing access is needed. The future direction of access control takes this into account, and various developments can be identified.

@column
## アクセス制御の将来の方向性

Access Control by means of ACLs and RBACs is relatively static; the combination between a user and his or her authorizations are set and do not vary easily, and other authorizations require changes. But people move between jobs, change devices, change location, or get new tasks in a new context. Also, the risk level assigned to a protected resource can change because of a change in context or a change in applicable laws and regulations. Relevant changes may include:
ACLやRBACによるアクセス制御は比較的静的です；ユーザーとそのユーザーの認可との組み合わせは決まっていて簡単には変化せず、他の認可も変更が必要です。しかし、人は職を転々とし、デバイスを変え、場所を変え、新しいコンテキストで新しいタスクを手に入れます。また、保護されたリソースに割り当てられたリスクレベルは、コンテキストの変化や適用される法律や規制の変更によて変わることがあります。関連する変化には以下のようなものがあります：

*   組織の拡大、国際化、コラボレーションおよびフェデレーション、フレキシブルな労働力、つまり日常業務の中で、従来の人事業務の範囲外の人がアクセス権を必要とすることが出てくる可能性があります。
    
*   データ処理のクラウド化 - SCIM（System for Cross-domain Identity Management、当初はSimple Cloud Identity Managementと呼ばれていましたが、シンプルすぎる、制約が多いと判断されたのでしょう）等の新しいプロトコルが開発されるに至ります。 [^5]
    
*   GDPRなどの新たな個人情報保護規制。 [^6]
    
*   OpenID Connectのような最新のプロトコルを用いたモバイルアプリの利用には、柔軟なアクセス制御のトポロジーが必要です。
    
*   エンドユーザーの同意と制御を強化する - UMA（User-Managed Access）のような開発。 [^7]
    
*   マイクロサービスに対するAPIベースのアクセスへの移行 - OAuth2などのプロトコルに基づく新たなアクセス管理アーキテクチャの導入につながります。
    

このような制約や変化は、よりダイナミックなアクセス管理手法が必要であることを示しています。今後のアクセス制御の方向性は、この点を考慮した上で、様々な開発が考えられます。

@row
### Dynamic Authentication

Access control is not a static event. When a user starts a session accessing services requiring a low-risk level, then identification with a username and password combination may be sufficient. When later on in the session, another trust level is required. For instance, when performing a transaction, additional identification, like a token, might be needed.

In order to adapt to these session dynamics, authentication in itself should also be a continuous process through, for example, the new concept of behavioral biometrics. Examples of changing needs for trust in the identity:

*   User switches context (such as location). This switch could effectively place the user in another trust zone, and the session should be re-evaluated
    
*   A user opens an email attachment, which by itself requires a higher trust level. This action should enforce additional authentication, such as Multi-Factor Authentication.
    

Adaptive authentication is a secure, dynamic, and ﬂexible form of authentication. It enables validating multiple factors to determine the authenticity of a login attempt before granting access to a resource. The factors that are used for user validation can depend on the risk associated with granting a particular user access and may involve adjusting the authentication strength based on the actual context.

@column
### 動的な認証

アクセス制御は、静的な事象ではありません。ユーザーが低リスクのサービスにアクセスするセッションを開始する場合、ユーザー名とパスワードの組み合わせによる識別で十分な場合があります。しかし、セッションの後半になると、別の信頼レベルが要求されます。例えば、トランザクションの実行時には、トークンのような追加的な識別が必要になるかもしれません。

このようなセッションのダイナミクスに適応するために、認証自体も、例えば行動バイオメトリクスの新しい概念などを通じて、継続的なプロセスであるべきです。以下は、アイデンティティにおけるトラストの要求の変化の例です：

*   ユーザがコンテキストを切り替えます（場所など）。この切り替えは、ユーザを事実上別の信頼ゾーンに置く可能性があり、セッションを再評価する必要があります
    
*   ユーザがEメールの添付ファイルを開くと、それだけでより高い信頼レベルが要求されます。この場合、多要素認証のような追加認証をおこなう必要があります。
    

アダプティブ認証は、セキュアで、動的で、柔軟性のある認証方式です。リソースへのアクセスを許可する前に、ログイン試行の信頼性を判断するために、複数の要素を検証することができます。ユーザー検証に使用される要素は、特定のユーザーにアクセスを許可することに関連するリスクに依存することができ、実際のコンテキストに基づいて認証強度を調整することを含むことができます。

@row
#### Policy-Based Access Control (PBAC)

A dynamic, ﬂexible method is required for access control to become effective and efficient in extended organizations in collaboration environments with a flexible workforce. Policy-based Access Control (PBAC) is the paradigm to provide this flexibility. PBAC, also known as Claims-based Access Control or Content-based Access Control, takes some of the business logic introduced in the ABAC model and enhances it by layering additional context evaluation and dynamic step-up capabilities

The context of an access requester can change dynamically. The dynamic nature of policy management and enforcement could require step-up authentication within a session to cater for the higher trust level needed if the defined risk controls require it. A policy engine will be responsible for checking if the user attributes and context information at the time that access is requested, comply with the access policies defined by the owners of the security policies. Context information might include time of day, geographical location, or device type. The scalability of access is also enabled by making it possible to collect attributes from different trusted and pre-defined attribute providers. As an example: this person can access the Risk Management reports, but only if this person has the CRISC certificate. ISACA provides this certificate, so a lookup in the ISACA registry could answer the question regarding the CRISC certification (the mapping of the Access Requester to the ISACA member is out of scope for this discussion). [^8]

The central component in this architecture is Policy Decision Point, which evaluates access policies and returns a response to the access request. The Policy Enforcement Point then enforces the response either by code embedded in the application or, increasingly, via an API gateway. The Policy Enforcement Engine is a discretionary component in the access request ﬂow.

As a further natural development, AIAC and ReBAC have to be mentioned.

@column
#### ポリシーベースアクセス制御（PBAC）

フレキシブルな労働力と協業する環境にあって拡大していく組織において、アクセス制御を効果的かつ効率的にするにはダイナミックでフレキシブルな方法が必須です。ポリシーベースアクセス制御（PBAC）はこの柔軟性を提供するパラダイムです。クレームベースアクセス制御やコンテンツベースアクセス制御としても知られるPBACは、ABACモデルで導入されたビジネスロジックの一部を採用し、追加のコンテキスト評価と動的ステップアップ機能を加えること強化してます。

アクセス要求者のコンテキストは動的に変化する可能性があります。ポリシー管理と適用の動的な性質は、定義済のリスク制御がより高い信頼レベルを必要とするとき、それを満たすための追加認証をセッション内で必要とするでしょう。ポリシーエンジンは、アクセス権が要求されたときのユーザー属性やコンテキスト情報がセキュリティポリシーのオーナーによって定義されているアクセスポリシーに準拠しているかを検証する責任があります。コンテキスト情報は、時刻や地理的な場所、デバイスの種類などが含まれる場合があります。別の信頼できる、事前に定義している属性プロバイダーから属性を収集できるようにすることで、アクセス権のスケーラビリティも可能になります。例：ある人がリスク管理レポートにアクセスすることができますが、CRISC証明書を持っている場合に限定することができます。ISACAはこの証明書を提供しており、ISACAレジストリを検索するとCRISC証明書に関する質問に回答することができるでしょう（ISACAメンバーへのアクセス要求者のマッピングはこの議論のスコープ外です）。 [^8]

このアーキテクチャの中心コンポーネントは、アクセスポリシーを評価してアクセス要求に対してレスポンスを返すポリシー決定ポイントです。ポリシー実行ポイントは、アプリケーションに組み込まれているコードやさらにはAPIゲートウェイを介することでレスポンスを強化します。ポリシー実行エンジンはアクセス要求フローにおける任意のコンポーネントです。

将来の発展として、AIACとReBACについても言及しなければなりません。

@row
### Relation-Based Access Control

A new concept in access control is ReBAC, or Relation-Based Access Control. ReBAC addresses the possibility of making access control decisions using the relationship between the access requester and the other identities who can potentially be affected by the access control decision. These access decisions can be deduced from (amongst other services) social media network relationships of the access requester. An attribute such as ‘reputation’ can be evaluated and considered. ReBAC relies on the availability of large, distinct data sets (incorporating data from HR/Sourcing & Access/entitlement/behavior) and on AI to conduct the evaluations and recommendations for access decisions.

The direction for ReBAC is not yet entirely clear, and the development is not mature enough for mainstream implementation. We foresee the potential for implementation as part of predictive role mining technologies for dynamic ABAC implementations. [^9]

@column
### 関係ベースアクセス制御

ReBAC、関係ベースアクセス制御、はアクセス制御の新しいコンセプトです。ReBACは、アクセス要求者とアクセス制御の決定によって影響を受ける可能性がある他のアイデンティティとの関係性を使ってアクセス制御の決定をおこなう可能性に対処します。これらのアクセス決定は、（他のサービス内でも）アクセス要求者のソーシャルメディアネットワークの関係性から推定されます。「評判」のような属性は評価され、考慮されます。ReBACは大規模で個別のデータセット（HR/Sourcingおよびアクセス/エンタイトルメント/振る舞いを統合したデータ）の可用性と、AIに依存してアクセス決定の評価と推奨を実施します。

ReBACの方向性はまだはっきりとしておらず、開発は主流の実装に充分なほど成熟していません。動的ABAC実装の予測ロールマイニングテクノロジーの一部として実装される可能性を予見しています。 [^9]

@row
### Artificial Intelligence Supported Access Control (AIAC)

We can expect much more in this area when we add the concept of artificial intelligence (AI). With a robust environment that classifies sensitive resources, it’s now possible to take a sophisticated risk management approach to dynamic access control whereby the identity manager solution will alert on access requests that exceed normal risk levels. AI will also monitor access control requests alerting on out-of-normal activity. As such, it can be an addition to current RBAC and ABAC implementations. This concept is not yet mainstream, and we can hardly predict the direction, but AI and machine learning may add some value.

@column
### 人工知能サポートのアクセス制御（AIAC）

人工知能（AI）の概念を追加すると、この分野でさらに多くのことが期待できます。機密性の高いリソースを分類する堅牢な環境により、動的アクセス制御に対する洗練されたリスク管理アプローチを採用できるようになりました。これにより、アイデンティティ管理ソリューションは、通常のリスクレベルを超えるアクセス要求について警告を発します。また。AIは異常なアクティビティを警告するアクセス制御リクエストを監視します。そのため、現在のRBACおよびABAC実装への追加となる可能性があります。この概念はまだ主流ではなく、その方向性を予測することはほとんどできませんが、AIと機械学習は何らかの価値を追加する可能性があります。

@row
### User Control and Consent

Privacy laws and regulations create a new awareness of access to personally identifiable information (PII). These laws and regulations have driven the concept of data ownership and consent by customers, employees, or patients. Data owners expect to be in control of their personal information, and in many cases, laws and regulations are mandating this. Several technological platforms have begun to spring up to fill this data ownership gap. Solutions like User-Managed Access, by Kantara Initiative, have made their way in the new access paradigms. Facilitated by the further development of protocols like OAuth, implementation of the concepts is made easier. [^10]

@column
### ユーザー制御と同意

プライバシーに関する法律や規制は、個人を特定できる情報（PII）へのアクセスに対する新たな意識を生み出しています。これらの法律と規制は、顧客、従業員、または患者によるデータの所有権と同意の概念を推進しています。データ所有者は個人情報の管理を期待しており、多くの場合、法律や規制がこれを義務付けています。このデータ所有権のギャップを埋めるために、いくつかの技術的なプラットフォームが登場し始めています。カンタラ・イニシアティブのユーザーマネージドアクセスのようなソリューションが、新しいアクセスパラダイムに対応しています。OAuthのようなプロトコルがさらに発展しているため、この概念の実装が容易になっています。 [^10]

@row
## Conclusion

Mainstream access control mechanisms like RBAC and ACL’s have a long tail and will continue to have valid use cases in many organizations. However, as companies, governments, and organizations begin to require communications and collaborations outside of their traditional four walls, other ways of controlling access are required.

Mainstream access control methods are not able to deliver the growing need for ﬂexible access control in a changing world. Modern access governance requires modern access control methods. There is a clear need for dynamic access control. Interestingly, the tools are becoming available, and implementation need not interfere with the current best practices: adaptive authentication, and PBAC can be added to an existing identity and access architecture. It takes some planning, based on a roadmap. And of course, it requires implementing elements of access governance.

@column
## 結論

RBACやACLのような主流のアクセス制御メカニズムには長い歴史があり、今後も多くの組織で有効なユースケースがあります。しかし、企業、政府機関、組織が従来の4つの壁の外でのコミュニケーションやコラボレーションを必要とするようになると、他の方法でアクセスを制御することが必要になってきます。

主流のアクセス制御手法では、変化する世界で高まる柔軟性のあるアクセス制御のニーズに対応できません。現代的なアクセスガバナンスには、現代的なアクセス制御手法が必要です。動的アクセス制御の必要性は明らかです。興味深いことに、ツールが利用可能になりつつあり、実装は現在のベストプラクティスに干渉する必要がありません：アダプティブ認証およびPBACは既存のアイデンティティとアクセスアーキテクチャに追加することができます。そのためには、ロードマップに基づいた計画が必要です。そしてもちろん、アクセスガバナンスの要素を実装する必要があります

@row
### Author Bio

<!-- ![A person wearing a suit and tie smiling at the camera Description automatically generated](/assets/images/idpro_bok/image1.jpg) --> André Koot is IAM and Security Consultant at SonicBee. His IAM experience comes from a financial accounting and auditing background. This background of anti-fraud detection and prevention business processes led to research in the area of authorization and access control principles.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2020-06-17 | V1 published |
| 2021-04-19 | Author affiliation change |
| 2021-09-30 | Updated definition for authentication |
| 2022-12-15 | V4 published: clarification to Policy Engine definition; minor editorial updates |

- - -

[^1]:  Wikipedia contributors, "Classified information," _Wikipedia, The Free Encyclopedia,_ [https://en.wikipedia.org/w/index.php?title=Classified\_information&oldid=1120242140](https://en.wikipedia.org/w/index.php?title=Classified_information&oldid=1120242140) (accessed November 24, 2022). 
    
[^2]:  Davis, Shannon, “A Look at Discretionary Access Control,” blog, TED Systems, 1 December 2020, [https://www.tedsystems.com/look-at-discretionary-access-control/](https://www.tedsystems.com/look-at-discretionary-access-control/) (accessed November 23, 2022). 
    
[^3]:  Rouse, Margaret, “mandatory access control (MAC),” TechTarget, December 2013, [_https://searchsecurity.techtarget.com/definition/mandatory-access-control-MAC_](https://searchsecurity.techtarget.com/definition/mandatory-access-control-MAC) (accessed November 23, 2022). 
    
[^4]:  Wikipedia contributors, "CAPTCHA," _Wikipedia, The Free Encyclopedia,_ [https://en.wikipedia.org/w/index.php?title=CAPTCHA&oldid=1122595810](https://en.wikipedia.org/w/index.php?title=CAPTCHA&oldid=1122595810) (accessed November 24, 2022). 
    
[^5]:  “SCIM: System for Cross-domain Identity Management,” [_http://www.simplecloud.info/_](http://www.simplecloud.info/) (accessed November 23, 2022). 
    
[^6]:  “EU General Data Protection Regulation (GDPR): Regulation (EU) 2016/679 of the European Parliament and of the Council of 27 April 2016 on the protection of natural persons with regard to the processing of personal data and on the free movement of such data, and repealing Directive 95/46/EC (General Data Protection Regulation),” OJ 2016 L 119/1. 
    
[^7]:  Kantara Initiative, “UMA Specifications,” wiki page, last updated Jul 27, 2022, [https://kantara.atlassian.net/wiki/spaces/uma/pages/29229182/UMA+Specifications](https://kantara.atlassian.net/wiki/spaces/uma/pages/29229182/UMA+Specifications) (accessed 23 November 2022). 
    
[^8]:  ISACA home page, [_https://www.isaca.org/_](https://www.isaca.org/) (accessed November 23, 2022). 
    
[^9]:  “Data Mining and Predictive Analytics: Things We should Care About,” Inside Big Data, 24 November 2018, [_https://insidebigdata.com/2018/11/24/data-mining-predictive-analytics-things-care/_](https://insidebigdata.com/2018/11/24/data-mining-predictive-analytics-things-care/) . 
    
[^10]:  Wikipedia contributors, "Classified information.” 
