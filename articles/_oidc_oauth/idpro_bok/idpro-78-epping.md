---
layout: columns
title: Authentication and Authorization (v2)
permalink: /docs/oidc_oauth/idpro_bok/78
date: 2024-09-09
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "認証", "認可", "フェデレーション"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：https://bok.idpro.org/article/id/78/

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article describes the fundamentals of authentication and authorization, two core components of Identity and Access Management. It also delves into federation and Identity Providers, common tools for performing authentication and authorization in an organization.

Keywords: authentication, authorization, federation

@column
## 概要

この記事では、アイデンティティおよびアクセス管理の2つの中核コンポーネントである、 認証と認可の基本について説明しています。また、組織での認証と認可を実行するための一般的なツールであるフェデレーションとアイデンティティ・プロバイダーについても詳しく説明します。

キーワード: 認証, 認可, フェデレーション

@row
## By Mark Morowczynski (Microsoft) and Michael Epping (Microsoft)

© 2022 IDPro, Mark Morowczynski, and Michael Epping

Updated by the IDPro Body of Knowledge Committee for v2

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction

This article describes authentication and authorization, two core components to a sound Identity and Access Management strategy. Organizations typically have multiple tools that leverage authentication and authorization, both on-premises and in the cloud. The core concepts of each are described, and common ways authentication and authorization are used are explored.

@column
## イントロダクション

この記事では、健全なアイデンティティとアクセス制御戦略の中核をなす2つのコンポーネントである、認証と認可について説明します。組織には通常、オンプレミスとクラウドの両方で認証と認可を活用する複数のツールがあります。それぞれのコア・コンセプトについて説明し、認証と認可を使用する一般的な方法について説明します。

@row
### Terminology

_Many of these terms have been sourced from the “Terminology in the IDPro Body of Knowledge”._ [^1]

| Term | Definition |
| --- | --- |
| Access Control Lists | Access Control Lists are definitions around who or what are allowed or denied access to a resource. For example, a file share may have an Access Control List that allows Marketing Department users to read and write, IT Department users to read-only, and denies all other users’ access. |
| Attribute-Based Access Control (ABAC) | A pattern of access control system involving dynamic definitions of permissions based on information (“attributes”, or “claims”), such as job code, department, or group membership. |
| Authentication | Authentication is the process of proving that the user with a digital identity who is requesting access is the rightful owner of that identity. Depending on the use-case, an ‘identity’ may represent a human or a non-human entity; may be either individual or organizational; and may be verified in the real world to a varying degree, including not at all. |
| Authorization | Determining a user’s rights to access functionality with a computer application and the level at which that access should be granted. In most cases, an ‘authority’ defines and grants access, but in some cases, access is granted because of inherent rights (like patient access to his/her own medical data). Authorization is evaluating what access or rights an identity should have in an environment. |
| Directory | A directory is a central repository for user identities and the attributes that make up those identities. A user identity might be John Smith with firstName attribute as John, lastName attribute as Smith, title attribute as Director, and Department attribute as Marketing. The attributes in the directory can be used to make authorization decisions about what this user should have access to in applications. |
| Identification | Uniquely establish a user of a system or application. |
| Identity Federation | An identity federation is a group of computing or network providers that agree to operate using standard protocols and trust agreements. In a Single Sign-On (SSO) scenario, identity federation occurs when an Identity Provider (IdP) and Service Provider (SP) agree to communicate via a specific, standard protocol. The enterprise user will log into the application using their credentials from the enterprise rather than creating new, specific credentials within the application. By using one set of credentials, users need to manage only one credential, credential issues (such as password resets) can be managed in one location, and applications can rely on the appropriate enterprise systems (such as the HR system) to be the source of truth for a user’s status and affiliation.<br><br>Identity federations can take several forms. In academia, multilateral federations, where a trusted third party manages the metadata of multiple IdPs and SPs, are fairly common. |
| Identity and Access Management | Identity and Access Management (IAM) is the discipline used to ensure the correct access is defined for the correct users to the correct resources for the correct reasons. |
| Identity Information Authority, aka Sources of “Truth” | This represents one or more data sources used by the IDM as the basis for the master set of principal/subject identity records. Each IIA may supply a subset of records and a subset of attributes. Sometimes the IIA is distinguished from the Identity Information Provider or IIP. We use IIA to include the service that actually provides the information as well as the root authority. This corresponds to Identity Information Source in ISO/IEC 24760-2 and Identity Sources in Internet2. |
| Identity Provider | An Identity Provider (IdP) performs a service that sends information about a user to an application. This information is typically held in a user store, so an identity provider will often take that information and transform it to be able to be passed to the service providers, AKA apps. The OASIS organization, which is responsible for the SAML specifications, defines an IdP as “A kind of SP that creates, maintains, and manages identity information for principals and provides principal authentication to other SPs within a federation, such as with web browser profiles.” |
| Multi-Factor Authentication | An approach whereby a user’s identity is validated to the trust level required according to a security policy for a resource being accessed using more than one factor (something you know (e.g., password), something you have (e.g., smartphone), something you are (e.g., fingerprint). |
| Relying Party | A component, system, or application that uses the IDP to identify its users. The RP has its own resources and logic. Note that the term ‘relying service’ is used in the ISO/IEC standards to encompass all types of components that use identity services, including systems, sub-systems, and applications, independent of the domain or operator. We will use the more common Relying Party (or RP). An RP roughly corresponds to the Agency Endpoint in the FICAM model or to Identity Consumers in the Internet2 model. |
| Role-based access control | A pattern of access control system involving sets of static, manual definitions of permissions assigned to “roles”, which can be consistently and repeatably associated with users with common access needs. Role-based access control is a control scheme in which roles are granted to identities, and those roles determine what access to resources those identities should have. Basic roles might be “admin” and “read-only user” – an admin would be able to make changes to a system and a read-only user would only be able to view resources. |

@column
### 用語解説

_これら用語の多くは「IDPro Body of knowledgeの用語」に基づきます。_  [^1]

| 用語 | 定義 |
| --- | --- |
| アクセス制御リスト | アクセス制御リストとは、リソースへのアクセスを許可／拒否されるユーザーまたは対象の定義です。例えば、ファイル共有にはマーケティング部門のユーザーが読み取りと書き込みを許可し、IT部門のユーザーは読み取り専用とし、他のすべてのユーザーのアクセスは拒否ことができます。 |
| 属性ベースアクセス制御 (ABAC) | ジョブコード、部署、グループメンバーシップなどの情報（「属性」または「クレーム」）に基づくアクセス許可の動的定義を含むアクセス制御システムのパターン。 |
| 認証 | 認証は、アクセスを要求しているデジタルアイデンティティを持つユーザーが、そのIDの正当な所有者であることを証明するプロセスです。 ユースケースに応じ、「アイデンティティ」は人間または人間以外のエンティティを表す場合があり、個人または組織の場合があります。実世界では、全く検証されていない場合も含め、様々な程度で検証される可能性があります。 |
| 認可 | コンピュータ・アプリケーションの機能にアクセスするユーザーの権利と、そのアクセスをどのレベルで許可すべきかを決定すること。ほとんどの場合、「権限」がアクセスを定義して付与しますが、個人の権利のためにアクセスが付与される場合もあります（患者が自分自身の医療データにアクセスするように）。権限付与は、ある環境においてIDがどのようなアクセスまたは権利を持つべきかを評価することです。 |
| ディレクトリ | ディレクトリは、ユーザーIDとそのIDを構成する属性の中央リポジトリです。ユーザーIDはJohn Smithで、firstName属性はJohn、lastName属性は Smith、title属性はDirector、Department属性はMarketingであるとします。ディレクトリ内の属性は、このユーザーがアプリケーションでどのようなアクセス権を持つべきかを決定するために使用されます。 |
| 識別 | システムやアプリケーションのユーザーを一意に確立すること。  |
| アイデンティティフェデレーション | アイデンティティフェデレーションは、標準プロトコルと信頼協定を使用して動作することに同意するコンピューティングプロバイダまたはネットワークプロバイダのグループです。シングルサインオン（SSO）シナリオでは、アイデンティティフェデレーションは、アイデンティティプロバイダ（IdP）とサービスプロバイダ（SP）が特定の標準プロトコルを介して通信することに同意したときに発生します。企業ユーザーは、アプリケーション内で新しい特定のクレデンシャルを作成するのではなく、企業のクレデンシャルを使用してアプリケーションにログインします。1セットのクレデンシャルを使用することにより、ユーザーは1つのクレデンシャルのみを管理する必要があり、クレデンシャルの問題（パスワードのリセットなど）は1箇所で管理でき、 アプリケーションはユーザーのステータスや所属に関する真実の源として適切な企業システム（人事システムなど）に依存することができます。<br><br>アイデンティティフェデレーションはいくつかの形態をとることができます。アカデミアでは、信頼できる第三者が複数の IdP および SP のメタデータを管理する多者間フェデレーションがかなり一般的です。 |
| アイデンティティとアクセス管理 | Identity and Access Management (IAM) は、正しいユーザーが正しい理由で正しいリソースに正しくアクセスできるように定義するために使用される規則である。 |
| Identity Information Authority, aka Sources of “Truth” | This represents one or more data sources used by the IDM as the basis for the master set of principal/subject identity records. Each IIA may supply a subset of records and a subset of attributes. Sometimes the IIA is distinguished from the Identity Information Provider or IIP. We use IIA to include the service that actually provides the information as well as the root authority. This corresponds to Identity Information Source in ISO/IEC 24760-2 and Identity Sources in Internet2. |
| IDプロバイダー | ID プロバイダー (IdP) は、ユーザーに関する情報をアプリケーションに送信するサービスを実行する。この情報は通常、ユーザー ストアに保持されるため、ID プロバイダーは多くの場合、その情報を取得して変換し、サービス プロバイダー (AKA アプリ) に渡すことができます。SAML 仕様を担当する OASIS 組織は、IdP を次のように定義している。「プリンシパルの ID 情報を作成、維持、および管理し、Web ブラウザ プロファイルなどを使用して、フェデレーション内の他の SP にプリンシパル認証を提供する SP の一種。」 |
| 多要素認証 | 複数の要素 (ユーザーが知っているもの (パスワードなど)、ユーザーが持っているもの (スマートフォンなど)、 ユーザーであるもの (指紋など)) を使用してアクセスされるリソースのセキュリティ ポリシーに従って、ユーザーの ID が必要な信頼レベルで検証されるアプローチ。 |
| Relying Party | A component, system, or application that uses the IDP to identify its users. The RP has its own resources and logic. Note that the term ‘relying service’ is used in the ISO/IEC standards to encompass all types of components that use identity services, including systems, sub-systems, and applications, independent of the domain or operator. We will use the more common Relying Party (or RP). An RP roughly corresponds to the Agency Endpoint in the FICAM model or to Identity Consumers in the Internet2 model. |
| ロールベースアクセス制御 | 「ロール」に割り当てられたアクセス許可の静的な手動定義のセットを含むアクセス制御システムのパターン。これは、共通のアクセス ニーズを持つユーザーに一貫して繰り返し関連付けることができる。ロールベースのアクセス制御は、ロールが ID に付与される制御スキームであり、それらのロールは、それらの ID が持つべきリソースへのアクセス権を決定します。基本的な役割は「管理者」と「読み取り専用ユーザー」。管理者はシステムに変更を加えることができ、読み取り専用ユーザーはリソースを表示することしかできません。 |

@row
Conceptually, authentication, sometimes abbreviated as AuthN, is the process of ensuring ownership of an account at the time the account is used to access a resource or establish a session. You complete authentication dozens of times a day and don’t even realize it. When you log in to your computer with your username and password, you just did authentication. Then when you log in to check your email through a browser or an application like Outlook, you again authenticate to prove you own or are otherwise responsible for that email account. When you pick up your mobile device and use a biometric like a fingerprint or your face to unlock the device, you again complete authentication. If you go to the ATM to withdraw money, you first need to provide a card and then a PIN. If you successfully authenticate, then the ATM can trust that you are the owner of the account. Authentication can take different forms for different resources:

@column
概念的には、認証（AuthNと略されることもあります）は、リソースへのアクセスやセッションの確立にアカウントが使用される時点で、アカウントの所有権を確実にするプロセスです。あなたは、一日に何十回も認証を完了していますが、それに気づいていません。ユーザー名とパスワードを使ってコンピュータにログインするとき、あなたは認証をおこなっただけです。次に、ブラウザやOutlookのようなアプリケーションで電子メールをチェックするためにログインするとき、あなたは再び、あなたがその電子メールアカウントを所有しているか、そうでなければ責任があることを証明するために認証をおこないます。モバイル・デバイスを手に取り、指紋や顔などのバイオメトリクスを使ってデバイスのロックを解除すると、再び認証が完了します。ATMに行ってお金を引き出す場合、まずカードを提示し、次にPINを入力します。認証に成功すれば、ATMはあなたがその口座の所有者であると信用できます。認証は、リソースに応じてさまざまな形をとることができます：

@row
<img class="image image--xl" src="/assets/images/idpro_bok/78-image1.png" alt="Diagram Description automatically generated" />

Figure : The user and their different authentication factors

@row
There are many different possible authentication factors, such as memorized secrets, hardware tokens, and biometrics. These are often referred to as “something you know,” “something you have,” and “something you are.” The most common factor is username and password. Also growing in popularity is the use of multifactor authentication methods. The most common is a text message or phone call, although these are no longer the strongest options available. There are also methods like One Time Passcode (OTP) software apps or hardware keys, where the password can be used only once and is usually valid for a limited duration. There are also different authenticator apps where a push notification is sent to the device and approved by the end-user. Physical FIDO2 security keys and biometrics like fingerprints and facial recognition are becoming more common and passkeys are rolling out to replace the standard password authentication ceremony entirely. [^2] Non-human identities also need to authenticate. Computers and services authenticate to each other using things like certificates, shared secrets (really just a password for an application), or other protocols developed for this purpose. Authentication, it’s not just for people!

Authentication is often the first step when an entity wants to access a resource. We must first determine which identity is trying to access the resource and determine if it is the legitimate identity or an imposter. Then we can move on to the next step, determining what access, if any, should be granted or denied to the identity.

@column
記憶している秘密情報、ハードウェアトークンやバイオメトリクスなど、認証の要素には様々なものが考えられます。これらはしばしば、「あなたが知っているもの」、「あなたが持っているもの」、「あなたであるもの」と呼ばれます。最も一般的な要素はユーザー名とパスワードです。また、人気が高くなっているものとして、多要素認証方式の利用があります。最も一般的な方法はテキストメッセージや電話ですがこれらはもはや最強のオプションではありません。また、ワンタイムパスワード（OTP）ソフトウェアアプリやハードウェアキーといった、パスワードは一回きりしか利用できず、一般的に限られた時間しか正当ではないような方法もあります。さらに、プッシュ通知がデバイスに送信され、エンドユーザーによって承認されるような認証器アプリもあります。物理的なFIDO2セキュリティキーや指紋や顔認証のようなバイオメトリクスは、より一般的になりつつあり、パスキーは標準的なパスワード認証方式を完全に取って代わるように展開されています。 [^2] 非人間のアイデンティティも認証が必要です。コンピュータおよびサービスは証明書、共有した秘密情報（実際にはアプリケーションのためのただのパスワード）やこの目的のために開発されたその他のプロトコルを使って互いに認証します。認証は、人間だけのものではありません！

しばしば認証はエンティティがリソースへのアクセスをおこないたいときの最初のステップです。まずどのアイデンティティがリソースへのアクセスを試みるのかを決定する必要があり、それが正当なアイデンティティか偽物かを判断しなければなりません。それから次にステップへ進み、もしあればアイデンティティにどのアクセス権を付与するか、拒否するかを決定します。

@row
## What is Authorization?

The next critical part of Identity and Access Management is authorization, sometimes abbreviated as AuthZ. Conceptually you can think of this as what an entity is allowed to do. Once the system or services knows who you are through authentication, you will be granted rights or permissions to do things through authorization. Authentication helps verify you are the same subject every time; authorization determines if you as the subject are allowed to access or do whatever action you are trying to do. These rights can be as simple as viewing a file (a grant permission) or denying the ability to view a file (a deny permission). You’ve probably experienced this when someone sent you a file or a link to a site and you received an “Access Denied” error message. You don’t have the authorization to access that resource. You’ve also experienced this when you were able to view a file or access a site. There was just no message saying you were allowed to do it! You’ve probably come across hundreds if not thousands of authorization decisions a day and not even realized it (unless you get stopped, of course).

@column
## 認可とは？

アイデンティティおよびアクセス管理において次に重要な部分は、認可（AuthZと略されることもあります）です。概念的には、これはエンティティに何を許可するかというように捉えることができます。システムまたはサービスが認証によってあなたが誰であるかを知ると、あなたは認可によって物事をおこなう権利または許可が与えられます。認証は、あなたが毎回同じ主体であることを検証するのに役立ち、認可はあなたが主体として、あなたがアクセスすることや実行しようとしているアクションが許可されているかどうかを決定します。これらの権限は、ファイルの閲覧（許可）またはファイル閲覧の拒否（拒否）というような単純なものです。誰かがあなたにファイルやサイトへのリンクを送ったとき、「Access Denied（アクセス拒否）」というエラーメッセージが表示された経験はないでしょうか。あなたはそのリソースにアクセスする権限を持っていないということです。もしくは、ファイルを見たり、サイトにアクセスできた経験をしたこともあるでしょう。ただ、許可されたというメッセージがなかっただけです！あなたはおそらく、1日に何百、何千もの認可決定に遭遇していますが、それに気づいていないのです（もちろん、アクセス拒否をされないかぎり）。

@row
Authorization decisions can be made based on many factors. To start with a common one, if you have a specific role assigned to your account, you might have permissions in the system to add, modify, delete, or view things. This authorization architecture is commonly referred to as Role-Based Access Control (RBAC). For example, if you hold the role of administrator in a system, you might be able to manage all aspects of that system. Alternatively, if you hold the role of a reader in the system, then you may be able to view all the same things as the administrator, but you don’t have the ability to make any changes.

@column
認可決定は多くの要因に基づいています。一般的なものから始めると、あなたのアカウントに特定のロールが割り当てられている場合、システムにおいて追加、変更、削除または閲覧の権限を有しているかもしれません。この認可アーキテクチャは一般的にロールベースアクセス制御（RBAC）と呼ばれています。例えば、システムの管理者のロールを有している場合、そのシステムのすべての側面を管理することができるかもしれません。反対に、システムにおいて閲覧者のロールを有している場合、管理者と全く同じものを閲覧できるかもしれませんが、何かしらの変更を加えることはできません。

@row
Similarly, there are Attribute-Based Access Control (ABAC) systems where users may be granted specific rights depending on attributes on their account. For example, if you are a member of the sales organization, you would probably be a member of a sales group in your corporate directory or have a Department attribute set to “Sales”. This group membership or attribute would grant you access to the sales shared network folder or a file-sharing site. But you wouldn’t be able to access the engineering shared network folder or engineering site. Only those that were a member of the engineering department would be able to. These decisions are made typically by Access Control Lists (ACLs) determined by the system administrator. RBAC and ABAC are large topics unto themselves, deserving of their own articles. [^3]

@column
同様に、アカウントの属性に応じてユーザーに特定の権限が与えられる属性ベースアクセス制御（ABAC）システムが存在します。例えば、営業組織のメンバーであれば、企業ディレクトリの営業グループのメンバーであり、部門属性は「営業」となっているでしょう。このグループのメンバーや属性は営業共有ネットワークフォルダまたはファイル共有サイトへのアクセスを許可します。しかし、エンジニア共有ネットワークフォルダやエンジニアサイトへのアクセスはできません。これらはエンジニア部門のメンバーだけがアクセスできます。これらの決定は、一般的にシステム管理者によって設定されたアクセス制御リスト（ACL）によって実現されます。RBACとABACにはそれ自体が大きなトピックであり、それぞれ独自の記事を書くに値します。 [^3]

@row
Another example of authorization based on information about the user could be their job title. When a regular user logs into their HR application, they see information about themselves. How many hours they’ve worked, their manager, their pay stub, and information about their benefits. They are only authorized to view their own information. Their manager has a similar view about their own information but may also have additional information they can see about their employees. They can see all the hours worked for their direct employees but can’t see that about other employees in the organization. Based on their title, they are only authorized to see that additional information about their direct reports. Finally, the head of HR might expect to see a wide range of information about the company. They might expect to see total hours worked for everyone in the company, total payroll, and benefits spent. Because they hold the title of Head of HR, they are authorized to see all this information.

@column
ユーザーに関する情報に基づく認可のもう一つの例として、役職があります。一般ユーザーが人事アプリケーションにログインすると、自分自身に関する情報を閲覧できます。勤務時間、マネージャー、給与明細や福利厚生に関する情報などです。一般ユーザはは自分の情報を閲覧する権限だけがあります。マネージャーは、自分の情報を閲覧するできることは同じですが、部下に関する情報を閲覧するこもできます。マネージャーは、直属の部下の勤務時間をすべて閲覧できますが、組織内の他の従業員については閲覧できません。役職に基づいて、直属の部下の追加情報を閲覧する権限だけが認可されています。最後に、人事部長は会社に関する幅広い情報を閲覧できることを期待するかもしれません。社内の全員の総労働時間、総支給額や福利厚生費用などを閲覧できることを期待するかもしれません。人事部長の役職を持つ人々は、これら全情報を閲覧することが人枯れている。

@row
Authorization applies to non-human accounts as well. A service account can hold roles in most directories. It would have the same permissions as any human account with that role. Service accounts can also be members of groups. A common example of this is the service that runs the backups on Windows servers. Depending on the design, it might require membership to a high privilege group, like Backup Operators, in order to backup and restore files on the system. [^4]

@column
認可は人間以外のアカウントにも適用されます。サービスアカウントは、ほとんどのディレクトリでロールを持つことができます。そのロールを持つ人間のアカウントと同じ権限を持ちます。サービスアカウントもグループのメンバーになることができます。よくある例は、Windowsサーバーのバックアップを実行するサービスです。設計によっては、システムのファイルをバックアップおよびリストアするためにBackup Operatorsのような特権グループへの追加が必要な場合があります。 [^4]

@row
At this point, the concept of authorization should be clear and may seem straightforward. Authorization grants or denies permissions to various resources for both human and non-human accounts. However, the implementation details of this can be extremely complex. In our example above, the sales team and engineering team have access to separate corporate resources. But what do we do when they need to collaborate on something? Engineering has a new product coming out, and the sales team needs to be able to sell it. Do we add the sales team to the engineering group? Should we add the engineering team to the sales group? Or do we create a NEW group called Sales-Engineering and add the sales group and the engineering group to that new group? This addition of a new group might seem like the correct solution, but what do we do when the operations group also needs to work with engineering to ensure the production of the product meets engineering standards. Operations also need to work with sales to ensure the supply chain is aligned with their sales projections. Do we create more groups for all three teams to work together? As you can see, this starts to grow and get out of hand. Having an authorization design for these types of scenarios is important before you start implementing an Identity and Access Management (IAM) solution as well as how you will handle exception cases that will arise.

@column
この時点では、認可の概念は明確であり、単純に思えるかもしれません。認可は人間と非人間のアカウントの両方に対して、様々なリソースへの許可を付与したり拒否したりします。しかし、この実装の詳細は非常に複雑です。上記の例では、営業チームとエンジニアチームは別々の企業リソースにアクセスできます。しかし、何か共同作業が必要な場合はどうすればよいでしょうか？エンジニアチームが新製品を発売することになり、営業チームがそれを販売できるようにする必要があります。営業チームをエンジニアグループに追加すべきでしょうか？エンジニアチームを営業グループに追加するべきでしょうか？それとも、営業・エンジニアという新しいグループを作り、営業グループとエンジニアグループをその新しいグループに加えるべきでしょうか？新しいグループの追加は正しい解決策のように思えますが、製品の生産がエンジニアリング基準に適合していることを保証するため、運用グループもエンジニアと協力する必要がある場合はどうすればよいでしょう。また、オペレーション部門はサプライチェーンが販売予測に合致していることを確認するため、営業部門と協力する必要があります。3つのチームが協力するために、さらにグループを作成するでしょうか？ご覧のように、これはどんどん大きくなり、手に負えなくなります。このようなタイプのシナリオを想定した認可設計をおこなうことは、アイデンティティとアクセス管理（IAM）ソリューションの実装を開始する前に、発生する例外ケースをどのように処理するかと同様に重要です。

@row
Lastly, we also need to make sure we are following the concept of least privilege when it comes to authorization. Least privilege is part of a robust strategy to ensure that users and service accounts only have the minimum permissions necessary to perform their. It is easy to grant more permissions such that things will work in an effort to make the authorization process simpler, but we’ll pay the price later for those decisions, often in catastrophic ways. It’s also often much more difficult to remove permissions from users and non-human accounts after they have been implemented. Take the time at the start to ensure least privilege is being followed for authorization decisions. Your future self will thank you.

@column
最後に、認可については最小権限の概念に従っていることを保証する必要があります。最小権限とは、ユーザーやサービスアカウントがその実行に必要な最小限の権限しか持たないことを保証するための強固な戦略の一部です。認可プロセスを単純化して物事がうまくいくように多くの権限を付与することは簡単ですが、後でその決定の代償をしばしば破滅的な方法で払うことになります。また、実装後にユーザーや非人間のアカウントから権限を削除することはは、はるかに困難な場合が多いです、最小権限を保証するため、最初に時間を取ってから認可の決定をおこないましょう。将来のあなた自身があなたに感謝するでしょう。

@row
## The Role of Identity Providers and Federation

Both authentication and authorization may occur within a single system or application or may be externalized via an identity federation. If you have an application that doesn’t reside on your corporate intranet (i.e., is a cloud-hosted service), your users will still need to authenticate. [^5]

The identity provider, frequently abbreviated as IdP or IDP, handles the authentication of the user. The authentication can be via a web browser using forms-based authentication, integrated windows authentication (IWA), or an application using a web API. It’s really user authentication as a service. There are common on-premises IdPs as well as cloud services that can be used as IdPs. These IdPs are commonly also doing some degree of authorization. Suppose a user is not able to authenticate to the IdP because they do not have an account or they do not have access assigned to a particular application. In that case, the IdP will not issue the user any assertion that can be used to access the application. If the user successfully authenticates, then the IdP issues assertions to the application/relying party.

Assertions, sometimes also referred to as claims, are pieces of information that are sent to the application/resource provider that, in this case, identifies the user and any additional information about the user that the application needs to function. These pieces of information are also referred to as attributes. The firstName attribute may be provided as an assertion and have values such as “John” or “Jane”. The information requested and sent varies from application to application, but information such as title, manager, employee ID, etc., can be included in the assertion.

Before a user can authenticate and have information sent as an assertion to the application and access it, a federation trust needs to be set up. [^6] The setup details vary between federation protocols, but the IdP and the application will essentially exchange some information, such as the IdP public key and the application’s endpoints for authentication. This information is typically in the metadata of the trust. Standards, such as FastFed, define how this metadata should be formatted to establish application and IdP trust. [^7]

Federation and IdPs allow us to control authentication and authorization for applications even outside the corporate network. These are important tools, especially in modern environments where cloud applications and services continue to proliferate. Organizations must be able to authenticate users, validate they are who they say they are, authorize them, and grant them the appropriate access based on who they are, everywhere – including on-premises and the cloud.

@column
## アイデンティティ・プロバイダーの役割とフェデレーション

認証と認可の両方を単一のシステムまたはアプリケーションでおこなわれる場合もあれば、アイデンティティ・フェデレーションを利用して外部で実施されることもあります。企業のイントラネット条に存在しないアプリケーションがある場合（つまり、クラウドにホストされたサービス）でもユーザは認証を必要とします。 [^5]

アイデンティティ・プロバイダー（しばしばIdPまたはIDPと省略されます）はユーザーの認証を処理します。認証は、ウェブブラウザを介したフォームベース認証、統合Windows認証（IWA）またはWeb APIを介したアプリケーションで実施されます。これはまさにサービスとしてのユーザー認証です。一般的なオンプレミスのIdPと同じようにクラウドサービスのIdPもあります。これらのIdPはもある程度の認可を実施します。ユーザーがアカウントを持っていなかったり、特定のアプリケーションに割り当てられたアクセス権を有していなかったりすることで、ユーザーがIdPで認証できないとします。この場合、IdPはアプリケーションへのアクセスに利用できるアサーションを発行できません。ユーザーが認証に成功した場合、IdPはアプリケーション/リライングパーティに対してアサーションを発行します。

アサーション、時折クレームとも呼ばれます、はこの場合にはユーザーを識別するアプリケーション/リソース・プロバイダーに送られる情報の断片であり、アプリケーションが動作に必要なユーザーに関する追加情報です。このような情報の断片は属性と呼ばれることもあります。firstName属性はアサーションとして提供され、「John」や「Jane」のような値になります。要求される情報や送信される情報はアプリケーションによって異なりますが、アサーションにはタイトル、マネージャーや従業員IDなどの情報が含まれます。

ユーザが認証し、情報をアサーションとしてアプリケーションに送信してアクセスする前に、フェデレーション・トラストを設定する必要があります。 [^6] セットアップの詳細はフェデレーション・プロトコルによって異なりますが、IdPとアプリケーションは本来は認証のためにIdPの公開鍵やアプリケーションのエンドポイントなど、いくつかの情報を交換します。通常、このような情報はトラストのメタデータに存在します。FastFedなどの標準仕様は、アプリケーションとIdPのトラストを確立するために、このメタデータをどのような形式にすべきかを定義しています。 [^7]

フェデレーションとIdPは、企業ネットワークの外でもアプリケーションの認証と認可を制御できるようにします。これらは、特にクラウド・アプリケーションとサービスが急激に増加し続けているモダンな環境では重要なツールです。組織は、オンプレミスやクラウドを含むあらゆる場所で、ユーザーを認証し、本人であることを主張するひとがそうであることを確認し、認可し、その人に応じて適切なアクセス権を付与できなければなりません。

@row
## Conclusion

This document is a review of two core IAM concepts: authentication and authorization. These concepts are used in every organization to validate identities and grant those identities the appropriate access once they’ve been determined to be legitimate. Validating the legitimacy of an identity is crucial to keeping attackers out of organizations’ systems. Granting the least permissions necessary to the identity is also recommended; it mitigates the damage if and when the wrong user or a compromised account accesses or has higher-than-necessary level of privilege in a system, thus reducing the blast radius of any nefarious actions as much as possible. Federation via Identity Providers (IdPs) is a common way to perform this authentication and authorization today, as applications and services are increasingly found outside corporate networks. Authentication and authorization techniques can protect these resources and identities regardless of location.

@column
## 結論

本書ではIAMの中核となる2つの概念、認証と認可について概観しました。これらの概念は、アイデンティティを検証し、正当であると判断されたら適切なアクセス権をアイデンティティに付与するために、すべての組織で利用されています。アイデンティティの正当性を検証することは、組織のシステムから攻撃者を締め出すために極めて重要です。アイデンティティに必要最小限の権限を付与することも推奨されます。これは、誤ったユーザまたは侵害されたアカウントがシステムにアクセスしたり、必要以上に高い権限レベルを持ったりした場合の損害を軽減し、悪意のある行為の爆破範囲をできる限り小さくすることになります。今日、アイデンティティ・プロバイダー（IdP）を介したフェデレーションは認証と認可を実行する一般的な方法であり、これは企業ネットワーク外でのアプリケーションやサービスの利用が増加しているためです。認証と認可の技術は、場所に関係なく、これらのリソースとアイデンティティを保護することができます。

@row
## Author Bios

Michael Epping is a Program Manager in the Azure AD Engineering team at Microsoft. He is part of the customer experience team; his role is to accelerate the adoption of cloud services across enterprise customers. Michael helps customers deploy Azure AD features and capabilities via long-term engagements that can last years, as well as working within the engineering organization as an advocate on behalf of those customers. Michael has more than nine years of experience working with customers to deploy Microsoft products like Azure AD, Intune, and Office 365.

Mark Morowczynski (@markmorow) is a Principal Program Manager on the customer success team in the Microsoft Identity division. He spends most of his time working with customers on their deployments of Azure Active Directory. Previously he was Premier Field Engineer supporting Active Directory, Active Directory Federation Services, and Windows Client performance. He was also one of the founders of the AskPFEPlat blog. He has spoken at various industry events such as Black Hat 2019, Defcon Blue Team Village, GrayHat, several BSides, Microsoft Ignite, Microsoft Inspire, Microsoft MVP Summits, The Experts Conference (TEC), The Cloud Identity Summit, SANs Security Summits, and TechMentor. He can be frequently found on Twitter as @markmorow arguing about baseball and sometimes making funny gifs.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2021-09-30 | V1 published |
| 2022-12-15 | V2 published; terminology section expanded (ABAC, Identification, Identity Information Authority, Relying Party); included reference to passkeys; removed information on PKI |

- - -

[^1]:  “Terminology in the IDPro Body of Knowledge,” IDPro Body of Knowledge, updated 30 September 2021, [https://bok.idpro.org/article/id/41/](https://bok.idpro.org/article/id/41/) . 
    
[^2]:  For more information on FIDO2, see Fido Alliance, “FIDO2: WebAuthn & CTAP – Moving the World Beyond Passwords,” website, [https://fidoalliance.org/fido2/](https://fidoalliance.org/fido2/) (accessed 28 September 2021); ; for more information on passkeys, see FIDO Alliance, “Passkeys,” website, [https://fidoalliance.org/passkeys/](https://fidoalliance.org/passkeys/) (accessed 10 November 2022). 
    
[^3]:  For more information, see Koot, André, “Introduction to Access Control,” IDPro Body of Knowledge, 17 June 2020, [_https://bok.idpro.org/article/id/42/_](https://bok.idpro.org/article/id/42/) , and McKee, Mary, “Policy-Based Access Control,” IDPro Body of Knowledge, 19 April 2021, [_https://bok.idpro.org/article/id/61/_](https://bok.idpro.org/article/id/61/) . 
    
[^4]:  For more information on managing non-human accounts, see Williamson, Graham and André Koot, “Non-human Account Management,” IDPro Body of Knowledge,30 October 2020, [https://bok.idpro.org/article/id/52/](https://bok.idpro.org/article/id/52/) . 
    
[^5]:  For more information on identity federations and sources of truth, see Lunney, Patrick, “Federation in the Enterprise,” IDPro Body of Knowledge, 19 April 2021, [https://bok.idpro.org/article/id/62/](https://bok.idpro.org/article/id/62/) , and Dingle, Pam, “Introduction to Identity - Part 2: Access Management,” IDPro Body of Knowledge, 17 June 2020, [https://bok.idpro.org/article/id/45/](https://bok.idpro.org/article/id/45/) . 
    
[^6]:  For more information on IAM architectures, see Dobbs, G. B., (2021) “IAM Reference Architecture”, _IDPro Body of Knowledge_ 1(6). doi: [https://doi.org/10.55621/idpro.76](https://doi.org/10.55621/idpro.76) 
    
[^7]:  OpenID Foundation, Fast Federation (FastFed) Working Group, website, [_https://openid.net/wg/fastfed/_](https://openid.net/wg/fastfed/) (accessed 31 August 2021). 
