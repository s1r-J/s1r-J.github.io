---
layout: columns
title: Managing Identity in Customer Service Operations
permalink: /docs/oidc_oauth/idpro_bok/65
date: 2024-09-09
modify_date: 2025-05-17
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "アイデンティティ", "運用", "カスタマーサービス", "リスク"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/65/](https://bok.idpro.org/article/id/65/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article will establish recommendations for best practices when managing the identities of your end-users in a customer service environment, considering the risks of both external and malicious insider threats. The following recommendations are built from the authors’ experiences and observations, and the recommendations included should be considered a starting point to inspire discussion. More rigorous study is necessary to further refine guidelines for this subject.

Keywords: identity, operations, customer service, nontechnical, administrator, risk, workforce, operational

@column
## 要約

本記事では、カスタマーサービス環境におけるエンドユーザーのアイデンティティ管理のベストプラクティスを、外部および内部両方の悪意のある脅威のリスクを考慮しつつ、推奨事項として提案します。以下の推奨事項は著者の経験と観察に基づいて構築され、議論を促すための出発点として考えるべきです。この話題についてさらに精緻なガイドラインをつくるにはさらに徹底的な研究が必要です。

Keywords: アイデンティティ, 運用, カスタマーサービス, 非技術的, 管理者, リスク, 人員, 運用的

@row
By Arynn Crow, Senior Technical Program Manager, AWS Identity

and Jp Rowan, Staff Solutions Architect, Auth0

© 2021 IDPro, Arynn Crow, Jp Rowan

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code)._

@row
## Introduction

Even in today’s highly automated world, there are many jobs that still just need a human. For many organizations, customer service is one of those jobs; when your end users have problems and have exhausted their ability to self-serve, they will turn to your customer service (CS) operations team for support with any number of the services or features you offer. Your CS team is on the frontline and feels your users’ pain points more acutely than any other department. Their job, and your users’ expectations of them, is to resolve any problem quickly and easily. Therein lies the tension and a core problem for the security-minded identity professional: how do we deliver on our promises of good experience and convenience to our customers while upholding our responsibility to protect their identities? 

The cross-section of customer service, IAM, and security is an area that has received comparatively little attention across industry publications and working groups. It is essential to get identity management in CS right due to the consequences for your users and organization for getting it wrong.[^1]

@column
## イントロダクション

高度に自動化された現代社会でも、人間が必要な仕事はまだ多くあります。多くの組織では、カスタマーサービスがそのような仕事のひとつです；エンドユーザーが問題を抱え、セルフサービスを使い切ったとき、カスタマーサービス（CS）運用チームに、提供しているサービスや機能のサポートを依頼します。CSチームは、最前線にいるため、他のどの部署よりもユーザーの苦痛を痛感しています。彼らの仕事、そして彼らへのユーザーの期待は、どんな問題でも迅速かつ簡単に解決することです。セキュリティを重視するアイデンティティプロフェッショナルにとって、そこには緊張感があり、核となる問題があります；顧客のアイデンティティを保護する責任を果たしながら、顧客に良い体験と利便性を約束するにはどうしたらよいでしょうか？

カスタマーサービス、IAM、およびセキュリティの断面は、業界の出版物やワーキンググループでは比較的あまり注目されていない分野です。CSにおいてアイデンティティ管理を正しくおこなうことは、誤ったさいのユーザーと組織への影響を考えると、非常に重要です。[^1]

@row
### Terminology/Glossary

**Account Recovery -** The process of updating a user’s credentials within a scenario where the user cannot validate those credentials  

**Account Takeover -** Account takeover is a form of identity theft and fraud, where a malicious third party successfully gains access to a user’s account credentials.[^2]

**Agent (also “Customer Service Agent”)** - The person responsible for communicating with and solving problems on behalf of customers or end-users. 

**Channel** - The communication avenue between you and your end-user, or your agent and their customer. This could be phone, chat, social media, or others. 

**Credentials -** Any attribute or shared secret that can be used to authenticate a user.

**Fractured Identity** - A case where a single end-user has multiple disparate digital identities.

**Impersonation -** A scenario where a user is able to perform actions as though they are a known user other than themself.

**Knowledge-Based Authentication (KBA) -** A method of authentication that uses information known by both the end-user and the authentication service but is not necessarily a secret.

**Personal Data -** Personal data are any information which are related to an identified or identifiable natural person.[^3]

**Social engineering -** Social engineering is a method of manipulating people so they give up confidential information, such as passwords or bank information, or grant access to their computer to secretly install malicious software.[^4]

**Step-up Authentication -** A method to increase the level of assurance (or confidence) the system has regarding a user’s authentication by issuing one or more additional authentication challenges, usually using factors different from the one(s) used to establish the initial authenticated session. The need for increasing the level of assurance is typically driven by the risk associated with the sensitive resource the user is attempting to access.[^5]

**Threat Modeling -** Threat modeling is an analysis technique used to help identify threats, attacks, vulnerabilities, and countermeasures that could impact an application or process.[^6]

**Username -** An identifier unique to the authentication service used in conjunction with a shared secret to authenticate a user.

@column
### 用語解説／用語集

**アカウントリカバリー -** ユーザーの資格情報を検証できないシナリオで、ユーザの資格情報を更新するプロセス。

**アカウントの乗っ取り -** アカウントの乗っ取りは、悪意のある第三者がユーザーのアカウント資格情報へのアクセスに成功する、アイデンティティの窃盗や詐欺の一形態です。[^2]

**エージェント（または「カスタマーサービスエージェント」）** - 顧客やエンドユーザーに代わって問題を解決するためにコミュニケーションをとる担当者。

**チャンネル** - あなたとあなたのエンドユーザーまたはあなたのエージェントとその顧客との間のコミュニケーション手段。電話、チャット、ソーシャルメディアなど。

**クレデンシャル -** ユーザーの認証に使われた属性または共有されたシークレット。

**バラバラになったアイデンティティ** - 1人のエンドユーザーが複数の異なるデジタルアイデンティティを有しているケース。

**なりすまし -** ユーザーが知っているユーザーのふりをしてアクションを実行するようなシナリオ。

**ナレッジベース認証（KBA） -** 必ずしもシークレットとは限らない、エンドユーザーと認証サービスの両方が知っている情報を利用して認証をおこなう方法。

**個人情報 -** 個人情報とは識別されたまたは識別可能な自然人に関連した情報です。[^3]

**ソーシャルエンジニアリング -** ソーシャルエンジニアリングとは、パスワードや銀行口座情報のような機密情報を提供する、またはコンピュータに悪意のあるソフトウェアを秘密裏にインストールするようにアクセス権を提供するように人々を操作する方法です。[^4]

**ステップアップ認証 -** ユーザーの認証に関連して1つまたは複数の追加の認証チャレンジ（通常これらは最初の認証セッションを確立した要素とは異なる要素を利用します）を発行することでシステムの保証（または信頼性）のレベルを高くする方法。保証レベルを高める必要性は、一般的にユーザーがセンシティブなリソースにアクセスしようとしたときに発生するリスクによって生じます。[^5]

**脅威モデリング -** 脅威モデリングとはアプリケーションやプロセスに影響するであろう脅威、攻撃、脆弱性および対策を特定する助けとなる分析手法です。[^6]

**ユーザー名 -** ユーザーを認証するために共有されたシークレットと組み合わせて利用される、認証サービスで一意となる識別子。

@row
## Why is this different from the rest of my IAM stack?

At first blush, it may be hard to see where customer service – a very operational function of the organization – fits into your otherwise very technical IAM strategy. In fact, CS operations are a critical part of your **IAM strategy,** not only because they represent your organization to customers during important moments (“Why can’t I log in to your service my multimillion-dollar business relies on?”), but also because CS operational processes create rich attack vectors for motivated social engineers. We rely on CS agents (“agents” hereafter) to help our customers when they can’t help themselves; to ensure their success in this endeavor, we entrust agents with access to private customer data and elevated privileges, from account creation to recovery. Your IAM system could be built with the most secure, sophisticated technology available, but your organization will be perpetually vulnerable unless your CS operational touchpoints are also hardened.

The number of touchpoints between your identity services and your customer service will vary by your type of organization and by the maturity of your organization for automating self-service functions for sensitive account functions. The most common use cases include:

*   **General inquiries –** Typically low-risk support requests that do not require modifying account data or divulging personally-identifying information. These requests could include order status updates, troubleshooting, checking balances, etc.
    
*   **Transactional support –** Requests to execute changes on behalf of the account holder, such as making a payment, placing or canceling orders, modifying subscriptions, or adding addresses
    
*   **Account creation and onboarding –** Establishing information about a new administrator or user during account setup, or adding additional delegated users to a “base” account in a nested account schema.
    
*   **Account recovery and state changes** – Highly sensitive requests to restore account access to an end-user, terminate an account, or transfer account ownership to another user
    
*   **Compliance-related requests** - Data Subject Access Requests (GDPR), data deletion requests, Right to Know (CCPA), or similar requests that fall into the scope of a data privacy framework. These operations are sensitive because they deal with potentially large volumes of private customer data, which can result in additional penalties for mishandling.
    

These use cases likely feel similar to those you must consider elsewhere within your IAM systems, so what makes CS operations different? Your end-users, especially customers, have high expectations about the availability of customer service; the communication channels agents use to interact with customers extend beyond your application stack. Complicating matters further is the reality that the tools you deploy to authenticate and authorize end-users in your web or application environment may be unavailable or impractical to you in a CS environment. Agents often operate across a blend of phone calls, online chats, ticketing, in-person kiosks, social media, and embedded in third-party applications like WeChat. These diverse conditions challenge the application of consistent security rituals like authentication, even if they’ve been implemented on your online login portal.  Organizations looking to preserve both their customer experience and security must weigh the risks of executing functions on the customer’s behalf against their relative certainty of a given actor’s identity; ideally, this decision-making process should be formalized in an internal framework to ensure decisions are applied consistently and can be inspected.

@column
## なぜこれは他のIAMスタックと異なるのでしょうか？

一見すると、カスタマーサービス（組織のまさに運用上の機能）が、それ以外のまさに技術的なIAM戦略のどこに適合するかを理解するのは難しいかもしれません。実際、重要な瞬間に顧客に対して組織を代表するという理由だけでなく（「数百万ドル規模のビジネスが依存しているサービスにログインできないのはなぜですか？」）、またCSの運用プロセスは、動機を持ったソーシャルエンジニアに対して豊富な攻撃ベクトルを生み出すため、CSオペレーションは**IAM戦略**の非常に重要な部分です。私たちは、CSエージェント（以下、「エージェント」）に頼って、顧客自身ではどうすることもできない場合に支援します；この取り組みを確実に成功させるために、アカウントの作成から回復まで、個人の顧客データへのアクセスと昇格された特権をエージェントに委ねています。IAMシステムは、利用可能な最も安全で洗練されたテクノロジーを使用して構築できますが、CSの運用上のタッチポイントも強化しない限り、組織は永続的に脆弱になります。

アイデンティティサービスとカスタマーサービス間のタッチポイントの数は、組織の種類や、機密性の高いアカウント機能のセルフサービス機能を自動化するための組織の成熟度によって異なります。最も一般的なユースケースは次のとおりです：

*   **一般的な問い合わせ –** アカウントデータの変更や個人を特定できる情報の漏洩が必要ではない一般的な低リスクのサポートリクエストです。これらのリクエストには、注文ステータスの更新、トラブルシューティング、残高の確認などが含まれる場合があります。
    
*   **トランザクションサポート –** 支払い、注文または注文キャンセル、サブスクリプションの変更、または住所の追加など、アカウント所有者に代わって変更を実行するリクエスト。
    
*   **アカウントの作成とオンボーディング –** アカウントのセットアップ中に新しい管理者またはユーザーに関する情報を確立する、またはネストされたアカウントスキーマにおいて「ベース」アカウントに追加の委任されたユーザーを追加します。
    
*   **アカウントの回復と状態の変更** – エンドユーザーに対するアカウントアクセスの復元、アカウントの終了、またはアカウントの所有権を別のユーザーに移譲する機密性の高いリクエスト
    
*   **コンプライアンスに関連したリクエスト** - データ主体アクセス要求（GDPR）、データ削除要求、知る権利（CCPA）、またはデータプライバシーフレームワークの範囲に入る同様のリクエスト。これらの操作は潜在的に大量の個人顧客データを扱うため、取り扱いを誤ると追加の罰則が科せられる可能性があり、注意が必要です。
    

これらのユースケースは、IAMシステム内の他の場所で考慮する必要があるものと似ていると思われますが、CSオペレーションの違いは何でしょうか？エンドユーザー、特に顧客、は顧客サービスの可用性に高い期待を持っています；エージェントが顧客と対話するために使用するコミュニケーションチャンネルは、アプリケーションスタックを超えて拡張されます。さらに事態を複雑にしているのは、Webまたはアプリケーション環境でエンドユーザーを認証・認可するためにデプロイしているツールが、CS環境では利用できないか、実用的でない可能性があるという現実です。エージェントは、多くの場合、電話、オンラインチャット、チケット、対面キオスク、ソーシャルメディア、およびWeChatなどのサードパーティアプリケーションへの埋め込みを組み合わせて運用します。これらの雑多な状況は、たとえオンラインログインポータルに実装されていたとしても、認証などの一貫したセキュリティ手順の適用に対して挑戦的な壁となります。カスタマーエクスペリエンスとセキュリティの両方を維持しようとしている組織は、顧客に代わって機能を実行するリスクと、特定のアクターのアイデンティティの身元の相対的な確実性を比較検討する必要があります；理想的には、この意思決定プロセスは内部フレームワークで形式化され、決定が一貫して適用され、検査できるようにすべきです。

@row
## Establishing Assurance

Key to formalizing a framework for consistency, establishing levels of assurance for the available authentication methods will provide a baseline to determine what types of transactions should be permitted.  The concept of assurance levels will likely have already been established as part of the rest of your existing access control policies, but in this case, these levels should be adapted to align with the channels and constraints of your CS interactions. It is likely your customers will have multiple interactions with customer support, and you may track those collective interactions as a “case” or something similar.  For the purpose of establishing an assurance level, we will need to look more granularly at the individual interaction, which we will refer to as a “session.”

For each session with an agent, the transactions that your agent is allowed to perform should be predicated on the current assurance level.  Assurance level will depend on the communication channel or other circumstances but can be increased in a way that your agents are enabled to assist your users without introducing unnecessary risk.

Considering the challenges and constraints that your users will face in a session, it may be necessary to introduce authentication methods that otherwise would not be used for authenticating into your applications or for other self-service workflows.

In comparison to your application stack, it may seem abstract to refer to the process your users are going through in a CS interaction as authentication.  In reality, the same primitives can be applied in these scenarios. Designing your authentication methods will help to assess the current assurance level while also reconciling the unique conditions that come into play in a CS session.

@column
## 保証の確立

フレームワークに一貫性を正式に組み込むための鍵は、利用可能な認証方法の保証レベルを確立することにより、どのような種類のトランザクションを許可すべきかを決定するためのベースラインを提供することです。保証レベルの概念は、既存のアクセス制御ポリシーの一部としてすでに確立されている可能性が高いですが、この場合、これらのレベルをCSインタラクションのチャンネルおよび制約に合わせて調整する必要があります。顧客は、カスタマーサポートと複数のやり取りをおこなう可能性があり、それらのやり取りを「ケース」または同様のものとして追跡することができます。保証レベルを設定するためには、個々のやり取りをよりきめ細かく調べる必要があり、ここでは「セッション」と呼びます。

エージェントとの各セッションで、エージェントが実行できるトランザクションは、現在の保証レベルを前提にすべきです。保証レベルは、コミュニケーションチャンネルやその他の状況によって異なりますが、不必要なリスクを発生させることなく、エージェントがユーザーを支援できるようにするために、保証レベルを上げることが可能です。

ユーザーがセッションで直面する課題や制約を考慮すると、アプリケーションやその他のセルフサービスワークフローへの認証に、他では使用されない認証方法を導入することが必要かもしれません。

アプリケーションスタックと比較すると、CSインタラクションでユーザーが通過するプロセスを認証と呼ぶのは抽象的に見えるかもしれません。実際には、これらのシナリオで同じ基本要素を適用することができます。認証方法を設計することで、現在の保証レベルを評価し、CSセッションで発生する固有の条件に合わせて調整することができます。

@row
## Authenticating Through an Application

Your agents and users might communicate through a support portal, contact form, or similar channel directly integrated within your application stack. If so, users will ideally be authenticating through the same service they would for any other application.  If that is the case, then authentication and your associated assurance framework should map directly with the actions your agents are allowed to perform.

@column
## アプリケーションを通じた認証

エージェントやユーザーがサポートポータル、コンタクトフォーム、またはアプリケーションスタックに直接統合された同様のチャンネルを通じてコミュニケーションをとるかもしれません。その場合、ユーザーは他のアプリケーションと同じサービスを通じて認証するのが理想的です。その場合、認証とそれに関連する保証フレームワークは、エージェントが実行できるアクションに直接対応すべきです。

@row
## Authenticating With an Agent

Alternatively, customers may need to rely on an external channel to communicate, and therefore the burden of authentication may fall on your agents. In this case, the goal remains the same, to establish proof the user is who they claim to be.  

Notably in the CS experience, some interactions might be very low risk, and it may be acceptable to complete the transaction with an assurance level that would not be acceptable for application access.  In contrast, higher-risk operations warrant higher-fidelity authentication methods, or even Step-Up authentication, which requires progressively greater assurance relative to the requested action.[^7]  Furthermore, some authentication methods used within a CS interaction may be completely unique to your application stack.

There are many options when it comes to authenticating a user in a customer service interaction. A common theme with all of these authentication methods is the need to create an association with the user’s digital identity ahead of time.  Establishing a high assurance level in your customer service sessions requires options tailored to the channels that you communicate through.  Those options are only available if you establish the channel or method prior to the session.  Creating a secure customer service interaction requires planning and implementation that starts much higher in your IAM stack.

@column
## エージェントによる認証

あるいは、顧客がコミュニケーションをとるために外部チャネルに依存する必要がある場合、認証の負担がエージェントにかかってくるかもしれません。この場合にも目標は同じであり、ユーザーが本人であることを証明することです。

CSエクスペリエンスで注目すべきは、一部のやり取りは非常にリスクが低く、アプリケーションアクセスには許容できない保証レベルでトランザクションを完了することが許容される場合があります。一方、高リスクの操作では、より信頼性の高い認証方法、または要求されたアクションに対して段階的に高い保証を要求するステップアップ認証が必要とされます。[^7] さらに、CSインタラクションで利用される一部の認証方法は、アプリケーションスタックに固有である場合があります。

カスタマーサービスでのやり取りでユーザーを認証する場合、多くの選択肢があります。これらの認証方法に共通するテーマは、ユーザーのデジタルアイデンティティとの関連付けを事前に作成する必要があることです。カスタマーサービスのセッションで高い保証レベルを確立するためには、コミュニケーションチャンネルに合わせた選択肢が必要です。これらの選択肢は、セッションの前にチャンネルまたは方法を確立している場合にのみ利用できます。安全なカスタマサービスを実現するには、IAMスタックの上位から計画と実装をおこなう必要があります。

@row
### Knowledge-Based Authentication

Knowledge-Based Authentication or (KBA) is possibly the most common, but also the least secure, second-factor mechanism to authenticate your users.  KBA involves authenticating a user by asking a set of questions that your user would know the answer to.  Common KBA questions include user credentials such as email or username, Social Security Number, date of birth, mother’s maiden name, but can be custom or something more specific to the user’s interaction with your product. The challenge with knowledge-based questions is that it is particularly difficult to ask a question your user both knows the answer to and that no one else would know the answer to.  KBA is hard to store and validate in a secure manner. Unlike a password that can be stored and validated using a one-way hash, KBA answers are typically stored in plain text, which also make them particularly susceptible to being exposed to nefarious actors.

KBA is generally a weak form of authentication, which has been discouraged by the National Institute of Standards and Technology (NIST) in other environments.[^8] It should be understood that having knowledge of a user does not prove they are the account owner or should be entitled to make changes to an account. As an example, children in a household will likely have information about their parents’ email addresses, physical addresses, and birth dates, but should not be entitled to access or change information on utility provider accounts their parents own. This information is also sometimes readily accessible online or is a major target for theft (e.g., social security numbers) and is available in criminal databases. Even exposing this information to your agents for the purposes of verification creates a vulnerability. When deciding if KBA is appropriate for some operations in your organization, you should consider the likelihood that the information has already been compromised. 

@column
### ナレッジベース認証

ナレッジベース認証（KBA）は最も一般的である可能性がありますが、ユーザーを認証するための最も安全でない第2要素メカニズムでもあります。KBAでは、ユーザーが答えを知っている質問をおこなうことで、ユーザーを認証します。一般的なKBAの質問には、Eメールやユーザー名、社会保障番号、生年月日、母親の旧姓などのユーザーの資格情報が含まれますが、独自のものや、ユーザーと製品のやり取りに固有のものもあります。知識ベースの質問の課題は、ユーザーが答えを知っていて、他の誰も答えを知らないような質問をすることが特に困難であることです。KBAを安全な方法で保管および検証することは困難です。一方向ハッシュを使用して保管および検証できるパスワードとは異なり、KBAの回答は通常プレーンテキストで保存されるため、特に悪意のあるアクターにさらされやすいです。

一般的にKBAは弱い認証方式であり、他の環境では米国国立標準技術研究所（NIST）によって非推奨とされています。[^8] ユーザーについての知識を持っていてもそのユーザーがアカウントの所有者であることを証明するものではなく、アカウントを変更する権利を持つべきであることを理解する必要があります。例えば、世帯内の子どもは、親のEメールアドレス、物理的な住所、および生年月日に関する情報を持っている可能性が高いですが、親が所有している電力会社のアカウントに関する情報にアクセスしたり変更したりする権利を持つべきではありません。この情報は、オンラインで容易にアクセスできる場合もあれば、窃盗の主要な標的（例、社会保障番号）となり、犯罪データベースで入手できる場合もあります。この情報を検証目的でエージェントに公開するだけでも、脆弱性が生じます。KBAが組織内の一部の操作に適しているかどうかを判断する場合は、情報がすでに侵害されている可能性を考慮する必要があります。

@row
### PIN Authentication

PINs and passcodes, like passwords, fall into the category of a memorized secret.[^9]   The intent is to provide similar verification to a password but in a format that can easily conform to a constrained communication channel.  PINs can easily be entered into a phone; passcodes can be communicated verbally.

Although PINs can be stored as a one-way hash, due to limited variability in characters they are more easily decrypted. Additionally,  if they are provided directly to an agent, PIN authentication suffers similar shortcomings of KBA.  As such, whether or not PINs are stronger than methods like KBA is highly dependent on how they are deployed.

@column
### PIN認証

PINやパスコードは、パスワードと同様に記憶シークレットに分類されます。[^9] その意図は、パスワードと同様の検証を、制約されたコミュニケーションチャンネルに容易に適合できる形式で提供することです。PINは電話で入力することが容易です；パスコードは口頭で伝えることができます。

PINは一方向ハッシュとして保存できますが、文字のばらつきが限られているため、より簡単に復号できます。さらに、PINがエージェントに直接提供される場合、PIN認証にはKBAと同様の欠点があります。そのため、PINがKBAのような方式よりも強力かどうかは、そのデプロイ方法に大きく依存します。

@row
### Social Authentication

A less obvious option, but valid when leveraging an external application, is to leverage proof of access to the communication channel.  In cases where the support channel leverages a social messaging platform (Twitter, WhatsApp, Facebook, Slack), it is possible to access the tool as a form of authentication.

An important step here is that the association of the existing user account and social provider needs to be made ahead of the customer service interaction in order to consider it a valid authentication method.    While a viable option, it is important to consider all the common risks associated with social authentication.  Social identity providers do not always verify ownership of email or phone number; they can be created at-will by an end-user and are susceptible to attack outside of the controls of your organization.

Registered Communication Channel (SMS, Phone, and Email) Authentication

Sending a one-time passcode to your user via SMS, email, or phone call is another common method of authentication used to validate a CS session. The code sent to the user is only valid for a single use and should be time-bound; if exposed to your agent or through a man-in-the-middle attack, it does not carry the same risk of being replayed like a memorized secret (KBA, PIN, passwords, etc.). 

The use of SMS authentication does suffer some weaknesses.  An attacker could gain possession of the user’s phone or perform a SIM swap attack.[^10]  Furthermore, requesting a user to communicate a one-time passcode to an agent normalizes the behavior which could be used as part of a phishing attack.  Despite these flaws, SMS continues to be a popular option due to ease of customer use and widespread adoption in application authentication.  

@column
### ソーシャル認証

あまり明確ではありませんが、外部アプリケーションを活用する場合に有効なオプションは、コミュニケーションチャンネルへのアクセスの証明を活用することです。サポートチャンネルがソーシャルメッセージングプラットフォーム（Twitter、WhatsApp、Facebook、Slackなど）を利用している場合、認証方式としてツールにアクセスすることが可能です。

ここで重要なステップは、既存のユーザーアカウントとソーシャルプロバイダーの関連付けを有効な認証方法と見なすため、カスタマーサービスとのやり取りの前におこなう必要があることです。実行可能な選択肢ではありますが、ソーシャル認証に関連するすべての一般的なリスクを考慮することが重要です。ソーシャルアイデンティティプロバイダーは、必ずしもEメールや電話番号の所有権を検証しません；エンドユーザーが任意に作成することができ、組織の制御外で攻撃されやすくなります。

登録済みコミュニケーションチャンネル（SMS、電話、およびEメール）認証

ワンタイムパスコードをSMS、Eメール、または電話でユーザーに送信することも、CSセッションの検証に利用される一般的な認証方法の1つです。ユーザーに送信されたコードは、1回の使用にのみ有効であり、時間制限があるべきです；エージェントにさらされたり、中間者攻撃を受けたりしても、記憶シークレット（KBA、PIN、パスワードなど）のように再利用されるリスクはありません。

SMS認証の利用には、いくつかの弱点があります。攻撃者はユーザーの電話を入手したり、SIMスワップ攻撃をおこなったりする可能性があります。[^10] さらに、エージェントにワンタイムパスコードを通信することをユーザーに要求すると、フィッシング攻撃の一部として利用される可能性のある動作が正常とみなされます。これらの欠陥にもかかわらず、SMSは顧客の使いやすさとアプリケーション認証での広範な採用により、依然として人気のある選択肢です。

@row
### Voice Biometrics

Biometrics are increasingly common authenticators across the web, appreciated for their convenience and improved security over methods like password-based authentication. Naturally, organizations have begun deploying these methods in their customer service environments as well, such as by deploying voice biometrics in phone channels to provide low-friction authentication. The appeal of tackling the hard problem of sufficient assurance in customer service with something convenient and secure like biometrics is obvious, but a few challenges you need to consider are:

*   There will be different regulatory requirements in each country you operate (or, as with the US, even different regions within the same country may have different requirements). The perception your end users have about biometric ethics may impact the way you collect, store, and apply biometric data. User privacy is paramount.
    
*   If you do not already offer or plan to offer biometric sign-in on your web platform, you’re faced with the prospect of building or buying a system only for your customer service channel. In that scenario, you will need to campaign to get your customers to register a biometric specifically for contacting customer service (which they likely hope to never need); alternatively, some organizations “passively” enroll callers into voice authentication.
    

Biometric implementation in customer service is a complex topic that will require the cooperation of your security, software engineering, and legal teams to ensure you’re implementing the correct authenticator for your organization’s needs and adhering to all compliance requirements. 

@column
### 音声バイオメトリクス

バイオメトリクスは、その利便性とパスワード認証などの方式に比べて高い安全性が評価され、Web上でますます一般的な認証手段となっています。当然ながら、組織はカスタマーサービス環境においても、摩擦の少ない認証を提供するため、電話チャンネルにおいて音声バイオメトリクスを導入するなどにより、これらの方式を導入し始めています。カスタマーサービスにおける十分な保証という難しい問題に、バイオメトリクスのような便利で安全なもので取り組むことの魅力は明らかですが、考慮が必要とされる課題もあります:

*   運用をおこなう国ごと（もしくは、米国と同様に同じ国内でも地域によって）に異なる規制要件が存在します。エンドユーザーのバイオメトリクスに関する倫理観は、生体データの収集、保管、および適用方法に影響を与える可能性があります。ユーザーのプライバシーは最重要事項です。
    
*   Webプラットフォームに生体認証サインインを提供していない、または提供する予定がない場合、カスタマーサービスチャンネルのためだけにシステムを構築または購入する必要性に直面します。その場合、顧客はカスタマーサービスに連絡するために生体認証を登録するようキャンペーンをおこなう必要があります（顧客は、それが必要ないことを望んでいると思われます）；あるいは、一部の組織では発信者を音声認証に「受動的に」登録することもあります。
    

カスタマーサービスにおけるバイオメトリクスの実装は複雑なトピックであり、セキュリティ、ソフトウェアエンジニアリング、そして法務の各チームが協力し、組織のニーズに合った正しい認証方法を実装し、すべてのコンプライアンス要件を遵守する必要があります。

@row
## Device Authentication

In cases where your users have installed an application on their device, it might be possible to leverage that device as a form of authentication. The most common way is to have the agent trigger a push notification to be sent to the user’s device.  The service the agent used to trigger the notification then waits for a response back from the device to notify the agent the message has been accepted.  This method provides a particularly high level of assurance since it leverages an existing session with your application and proof of possession of the device.

@column
## デバイス認証

ユーザーが自分のデバイスにアプリケーションをインストールしている場合、そのデバイスを認証手段として活用することができるかもしれません。最も一般的な方法は、エージェントがユーザーのデバイスに送信されるプッシュ通知をトリガーすることです。そして、エージェントが通知をトリガーするために利用したサービスは、メッセージが受け入れられたことをエージェントに通知するために、デバイスから戻ってくる応答を待機します。この方法は、アプリケーションとの既存のセッションとデバイスの所有証明を利用するため、特に高い保証レベルを提供します。

@row
## Account Recovery

We are distinguishing account recovery from routine authentication to underscore the increased sensitivity and need for special diligence. Your first goal with account recovery should be for your users to not need it often, as a result of proactive account and security hygiene. Your second goal should be to avoid relying on manual recovery for your customers, such as intervention with customer service, because it is a high-risk operation. Many organizations find that they cannot achieve both objectives and enable their customer service representatives to assist with break-glass account recovery measures when end-users have forgotten or lost access to all their means of authentication, such as by modifying the user’s email or password. There are a few common methods of verifying identity when users need assistance recovering their accounts:

*   Use of established authenticators previously associated with the account. These methods are strong but may be of limited utility by use case. 
    
*   Use of KBA. Even in low-risk use cases, KBA is weak and should be avoided; if this is not possible, bias towards challenge questions that are more extensive than your low-level authentication questions, cannot be obtained online (such as order history questions known only to you and your customer), and cannot be easily phished from your frontline operations. 
    
*   Use of real-world identity documents, such as driver’s license and utility bills. If you didn’t collect these documents from your user previously for comparison, these should be used in combination with another method to ensure the person who provides you with a document is the correct account owner. 
    

Ultimately, account recovery is a high-risk operation; your users may contact you because they’ve lost access to any authenticators they could use to self-recover, which means you will be faced with the choice of accepting that your user will be unable to recover their account, or accepting a degradation in your overall security posture. If you maintain a high bar for creating and logging into your accounts, but a weak one for recovering them, this information could proliferate online and be used exploitatively. Always notify your customers about changes to account identifiers and credentials, and give them the option to report, approve, or revert changes initiated with low assurance.

Your organization will need to decide its tolerance for risk in account recovery - or if any risk is acceptable at all - versus its user experience, which may vary depending on what types of accounts you manage. As an example, high-value, high-risk sectors, like large Business to Business accounts, may warrant different processing than retail consumer or public library accounts; there may even be cases where it is appropriate to delegate part of this function to your legal team for more intensive identity verification than your operations will be able to execute.  

More on account recovery is available in the IDPro Body of Knowledge article, “Account Recovery.”[^11]

@column
## アカウントリカバリー

アカウントリカバリーを通常の認証と区別することで、より繊細で特別な注意の必要性が強調されます。アカウントリカバリーの第一の目標は、積極的なアカウントとセキュリティ衛生の結果として、ユーザーが頻繁にリカバリーを必要としないようにすることです。第二の目標は、カスタマーサービスへの介入など、手動によるアカウントリカバリーが高リスクであるため、それに頼らないようにすることです。多くの組織では、エンドユーザーがEメールやパスワードを変更するなどして、認証手段をすべて忘れたり、アクセスできなくなったりした場合に、両方の目的を達成できず、カスタマーサービス担当者がブレークガラスアカウントのリカバリー方法を支援できないことに気づきます。ユーザーがアカウントリカバリーの支援を必要とする場合の身元確認方法には、いくつかの一般的な方法があります：

*   アカウントに事前に関連付けられた確立された認証方式の利用。これらの方法は強力ですが、ユースケースによって実用性が制限される場合があります。
    
*   KBAの利用。リスクの低いユースケースであったとしても、KBAは脆弱で回避すべきです；それが不可能な場合、低レベルな認証質問よりも広範囲で、オンラインで取得できず（あなたとあなたの顧客しか知らない注文履歴の質問など）、現場の運用から簡単にフィッシングできないチャレンジ質問に偏らせます。
    
*   運転免許証や公共料金の請求書など、現実世界の身分証明書の利用。比較のためにユーザーからこれらの書類を事前に収集していない場合、書類を提供した人物がアカウントの正当な所有者であることを確認するため、他の方法と組み合わせて利用すべきです。
    

結局、アカウントリカバリーはリスクの高い操作です；ユーザーがセルフリカバリーに利用できる認証方式すべてにアクセスできないため、ユーザーがあなたにコンタクトをしてくる可能性があり、これはユーザーがアカウントをリカバリーできないことを受け入れるか、全体的なセキュリティ体制を低下させることを受け入れるかの選択を迫られることになります。アカウントの作成とログインのハードルを高くし、アカウントのリカバリーのハードルを低くした場合、この情報がネット上で拡散され、悪用される可能性があります。アカウントの識別子と資格情報の変更について、常に顧客に通知し、低い保証で開始された変更を報告、承認、または元に戻すオプションを提供します。

組織は、アカウントリカバリーのリスクに対する許容度、またはリスクを許容できるかどうかを、管理するアカウントの種類によって異なるユーザーエクスペリエンスと比較して決定する必要があります。たとえば、企業間取引の大口顧客など、高価値かつ高リスクの分野では、消費者向け小売店や公共図書館の顧客とは異なる処理が必要となる場合があります；業務で実行可能な範囲を超えてより厳格に身元確認をおこなうために、この機能の一部を法務チームに委任することが適切な場合もあります。

アカウントリカバリーの詳細については、IDPro Body of Knowledgeの記事「Account Recovery」[^11] で入手可能です。

@row
## Controls

Understanding that your CS operations teams may have access to elevated data and privileges, it is important to have controls in place to prevent misuse (intentional or otherwise) and identify problems quickly. These controls should be considered for all areas within your organization, but there may be additional complexities in organizations with large CS environments.

@column
## 管理

CS運用チームは、高度なデータや特権にアクセスできる可能性を理解し、誤用（意図的か否かを問わず）を防止し、問題を迅速に特定するための管理体制を整備することが重要です。これらの管理は、組織内のすべての領域で検討すべきですが、大規模なCS環境を持つ組織では、さらに複雑な問題が発生する可能性があります。

@row
### Permissions controls

In fast-changing environments where seconds matter, operations management will be keen to ensure there is as little downtime for their employees as possible and that the agents have sufficient privileges necessary to perform their jobs. The decision to aim for immediate issue resolution at first contact by assigning extended privileges to the agent is a recipe for overprovisioning. Over time, with insufficient baselining and auditing procedures, this effect can snowball; employees will continue to collect privileges as the demands of their job evolve. Over time (especially in large, complex organizations), the governance conventions of the resources and policies gating those resources shift, leading to role, policy, or attribute explosion, depending on your governance system. This also leads to overprovisioning and, worse, an inability to effectively audit potentially over-provisioned users, as the administrator may not understand what privileges should be removed. 

A full analysis of different access control governance models is beyond the scope of this article; other resources, like the IDPro Body of Knowledge “Introduction to Access Control” and “Policy-Based Access Control” offer a more detailed overview of the advantages and disadvantages of Policy-Based Access Control, Role-Based Access Control, and Attribute-Based Access Control.[^12] While the fundamentals of access control do not change for your operations team, depending on the size of your organization, the scale and complexity might; you may find that your operations access needs more drastic and frequent change than sales, engineering, management, et cetera.  Finally, it is imperative that your team or IAM resource administrators have mechanisms for auditing privilege use against your organization’s policies to ensure your controls are working as intended and preventing misuse.  

@column
### パーミッション制御

一刻を争う変化の激しい環境では、運用管理者は従業員のダウンタイムをできるだけ少なくし、エージェントに業務遂行に必要な十分な権限を付与することを望みます。エージェントに拡張された権限を割り当てることで、最初のコンタクトですぐに問題を解決しようとする決定は、過剰なプロビジョニングの元凶となります。ベースライン設定と監査手順が不十分なまま時間が経過すると、この影響は雪だるま式に大きくなります；従業員は自分の仕事の要求が進化するにつれて、権限を集め続けることになります。時間の経過とともに（特に大規模で複雑な組織の場合）、リソースのガバナンス規約とそのリソースを制限するポリシーが変化し、ガバナンスシステムによっては、ロール、ポリシー、または属性の爆発が発生します。これはオーバープロビジョニングにもつながり、さらに悪いことに、管理者がどの権限を削除すべきかを理解できないため、オーバープロビジョニングされた可能性のあるユーザーを効果的に監査することができなくなります。

様々なアクセス制御のガバナンスモデルの完全な分析はこの記事の範囲外です；IDPro Body of Knowledgeの「Introduction to Access Control」や「Policy-Based Access Control」のような他のリソースは、ポリシーベースのアクセス制御、ロールベースのアクセス制御、および属性ベースのアクセス制御の長所と短所についての詳細な概説が掲載されています。[^12] アクセス制御の基本は運用チームと変わりませんが、組織の規模によっては、その規模や複雑さが変わるかもしれません；営業、エンジニアリング、マネジメントなどよりも運用アクセスのほうが大規模に頻繁に変更する必要がある可能性があります。最後に、チームまたはIAMリソース管理者には、組織のポリシーに照らして権限の利用を監視するメカニズムを用意し、意図したとおりに制御が機能し、誤用を防止できるようにすることが不可欠です。

@row
## Risks/Consequences

Administrators of IAM operational functions will, by nature of the job, encounter a number of unique scenarios and edge cases within their organizations beyond what can be fully cataloged in this article. Operations environments can be fast-paced and quick to change, adapting to support the organization as it evolves; nevertheless, it is critical to remain diligent. The channels through which users interact with customer support are desirable attack vectors.  Bringing a human into the equation creates the opportunity for exploitation that your application stack would otherwise not be vulnerable to.   

The coming paragraphs acknowledge the most common risks, known anti-patterns, and suggested best practices as a reference.  This list should not be considered definitive; it is a good starting point to avoid common pitfalls.

@column
## リスク／結果

IAM運用機能の管理者は、仕事の性質上、この記事で完全にカタログ化できるものを超えて、組織内で多数の固有のシナリオとエッジケースに遭遇します。運用環境は速いペースで変化し、組織の進化に合わせて適応します；にもかかわらず、勤勉であり続けることが不可欠です。ユーザーがカスタマーサポートとやり取りするチャンネルは、格好の攻撃ベクトルです。人間を介入させることで、本来であればアプリケーションスタックが脆弱になることのないような攻撃を受ける機会が生まれます。

以降の段落では、最も一般的なリスク、既知のアンチパターン、および推奨されるベストプラクティスを参考として示します。このリストは決定的なものではありません；よくある落とし穴を避けるための良い出発点です。

@row
### Social Engineering

The industry is increasingly acknowledging the significance of the threat posed by social engineers; a 2020 Verizon Data Breach Investigation found phishing and other forms of social engineering were involved in 22% of attacks.[^13] Customer service agents are especially vulnerable because they are your direct line to the public, they’re entrusted with sensitive privileges necessary to resolve tough customer problems, and they likely have a vested, performance-driven interest in making your customer happy. Unmitigated, this can be a severe risk for your organization.

**Do:**

*   **Provide access only to resources that are required to perform the job**. This mitigates damage in case your agent is targeted in a social engineering attack.
    
*   **Routinely educate personnel on the most common types of phishing and engineering attacks.** Ensure they know how to recognize and escalate suspected attacks. Phishing attacks are constantly evolving and becoming more sophisticated; continuous monitoring and updating on current trends is an important part of agent education
    
*   **Establish regular audits of your resources and access rights** to ensure you are continuing to enforce least privilege even as job functions change over time.
    
*   Establish a thorough catalog of the resources your organization maintains and an understanding of their relative sensitivity; require progressively higher-fidelity proofs to gain access to more sensitive resources for both employees and end-users, such as management chain approvals, additional identification, or other checks as appropriate. 
    

Do Not:

*   **Use information that is easily accessible to the public** - online or offline - as part of your account authentication or recovery processes 
    

@column
### ソーシャルエンジニアリング

業界は、ソーシャルエンジニアによってもたらされる脅威の重要性をますます認識しています。2020年のVerizon Data Breach Investigationでは、フィッシングやその他のソーシャルエンジニアリングが攻撃の22%に関与していることが判明しました。[^13] カスタマーサービスエージェントは、外部との直接の連絡窓口であり、顧客の困難な問題を解決するために必要な機密特権を委ねられており、さらに顧客を満足させることに強い関心を持ち、パフォーマンスを重視しているため、特に脆弱です。対策しなければこれは、組織にとって重大なリスクになる可能性があります。

**おこなうべき：**

*   **職務の実行に必要なリソースのみへのアクセスを許可します**。これにより、エージェントがソーシャルエンジニアリング攻撃の標的となった場合の被害を軽減できます。

*   **最も一般的な種類のフィッシング攻撃とエンジニアリング攻撃について、定期的に担当者への教育を実施してください**。疑わしい攻撃を認識し、エスカレーションする方法を周知徹底してください。フィッシング攻撃は常に進化し、より巧妙化しています；最新の傾向を継続的に監視し、アップデートすることは、担当者教育の重要な部分です。

*   **リソースとアクセス権の定期的な監査を実施**して、職務が時間の経過とともに変化しても最小限の権限が継続して適用されていることを確認します。
    
*   組織が維持するリソースの完全なカタログを作成し、それらの相対的な機密性を把握します；従業員とエンドユーザーの両方が、より機密性の高いリソースにアクセスできるようにするために、管理チェーンの承認、追加の識別、その他の適切なチェックなど、徐々に忠実度の高い証明を要求します。 
    

おこなうべきでない：

*   アカウント認証またはリカバリープロセスの一環として、オンラインまたはオフラインで**パブリックに簡単にアクセスできる情報を使用する**
    

@row
### Account Takeover

In a customer service interaction, account takeover is made possible by allowing an attacker to modify a victim’s credentials from something the victim knows and has access to, to something the attacker knows and has access to. Credential changes are the catalyst to a chain of events that can result in a valid user losing all access to their account and instead place full control in the attacker’s hands.  This is the worst case and common result of poor controls within a customer service stack.

It is important to note that credentials can be more than just a password.  If a phone number or email address can be used as a channel for account recovery, they too should be considered a credential.  

Do:

*   Leverage existing authentication methods to establish a secure session with users in customer service interactions.  Whenever possible, use existing authentication workflows to establish a legitimate session with your users.
    
*   **Align your session assurance levels with those applied to your applications.** Only when the assurance level matches the requirements for a specific transaction should it also be allowed in a customer service interaction.
    
*   **Leverage existing self-service channels for account recovery when possible.**  All self-service account recovery channels should have been threat modeled with the design of your IAM stack and therefore would not require additional vetting for the purpose of customer service interactions
    
*   **Notify the end-user in the case that a credential has been updated in a customer service interaction.** A message should be sent to all possible (prior) validated communication channels to notify an end-user when a credential has been updated by a Customer Service Agent.
    
*   **Establish controls that allow for changes made by a Customer Service Agent to be reversed by the end-user.** In addition to notification, end-users should have the option to escalate or reverse credential changes enacted against their accounts that they did not authorize. 
    

Do Not:

*   **Allow users to update credentials in Customer Service interactions** unless you can satisfy the level of authentication required for these high-risk operations as required by your risk framework
    

@column
### アカウント乗っ取り

顧客サービスのやり取りでは、攻撃者が被害者の資格情報を、被害者が知っていてアクセスできるものから、攻撃者が知っていてアクセスできるものに変更できるようにすることで、アカウントの乗っ取りが可能になります。資格情報の変更は、正当なユーザーが自分のアカウントへのすべてのアクセスを失い、代わりに攻撃者の手に完全に制御される可能性がある一連のイベントの触媒です。これは、カスタマーサービススタック内の制御が不十分な場合の最悪のケースであり、よくある結果です。

資格情報は単なるパスワード以上のものであることに注意することが重要です。電話番号またはEメールアドレスをアカウントリカバリーのチャンネルとして使用できる場合は、それらも資格情報と見なすべきです。

おこなうべき：

*   既存の認証方法を活用して、カスタマーサービスのやり取りでユーザーとの安全なセッションを確立します。可能な限り、既存の認証ワークフローを使用して、ユーザーとの正当なセッションを確立します。

*   **セッション保証レベルをアプリケーションに適用されるレベルに合わせます。**保証レベルが特定のトランザクションの要件に一致する場合にのみ、カスタマーサービスのやり取りで許可すべきです。

*   **可能であれば、アカウントリカバリーのために既存のセルフサービスチャンネルを活用します。**すべてのセルフサービスアカウントリカバリーチャンネルは、IAMスタックの設計を使用して脅威をモデル化すべきであるため、カスタマーサービスのやり取りを目的として追加の審査をおこなう必要はありません。
    
*   **カスタマーサービスのやり取りで資格情報が更新された場合、エンドユーザーに通知します。**資格情報がカスタマーサービスエージェントによって更新されたときにエンドユーザーに通知するために、すべての可能な（以前に）検証されたコミュニケーションチャンネルにメッセージを送信すべきです。
    
*   **カスタマーサービスエージェントがおこなった変更をエンドユーザーが元に戻すための管理を確立します。**通知に加えて、エンドユーザーはアカウントに対して実行された認可していない資格情報の変更をエスカレートまたは元に戻すオプションを持つべきです。
    

おこなうべきでない：

*   リスクフレームワークで要求される、リスクの高い操作に必要な認証レベルを満たすことができない限り、**カスタマーサービスのやり取りでユーザーが資格情報を更新できるようにする**
    

@row
### Impersonation

Within an application, impersonation occurs when actions are taken on behalf of a user, without being initiated by that user, are unidentifiable as such. Because customer service agents will often need to perform actions on behalf of other users or possibly replicate another user’s experience, it is quite possible that the tools provided to the Customer Service Agents might result in enabling impersonation.  

Typically, impersonation occurs because it is simply easier to have a customer service agent login on behalf of the user they are assisting than it is to build out the necessary tooling for them to perform their job securely.  Once operationalized, tools and workflows that rely on impersonation create opportunities for users to be harmed without notice and are an enticing target for attackers that wish to wreak havoc without a trace.

Do:

*   **Build tools that allow Customer Service Agents to manage end-user data outside of the core application.**  Separating the customer service use cases from your core applications makes it easier to audit the actions taken by your agents and helps to avoid scenarios where impersonation might accidentally occur
    
*   **Require end-users confirmation before Customer Support Agents can perform actions on their behalf.**  Establishing consent workflows helps build trust with your users and helps to ensure that elevated actions taken by agents are scoped to specific user interactions.
    

Do not:

*   **Allow Customer Service Agents to login as an end-user.** Any scenario where a customer service agent is acting on behalf of an end-user or needs to replicate the end-user experience must be auditable as such.  All actions taken by the agent should be recorded in the system of record as such.
    

@column
### なりすまし

アプリケーション内では、あるユーザーの代わりに、そのユーザーによって開始されることなく、そのユーザーと識別できないアクションが実行されるときに、なりすましが発生します。カスタマーサービスエージェントは、しばしば他のユーザーの代わりにアクションを実行したり、他のユーザーのエクスペリエンスを再現する必要があるため、カスタマーサービスエージェントに提供されるツールがなりすましを可能にする可能性は充分にあります。

一般的に、なりすましは、カスタマーサービスエージェントが安全に業務を遂行するために必要なツールを構築するよりも、支援対象のユーザーの代わりにログインする方が簡単なために発生します。なりすましに依存したツールやワークフローが運用されると、ユーザーが気づかないうちに被害を受ける機会が生まれ、証跡なく破壊することを望む攻撃者にとって魅力的なターゲットとなります。

おこなうべき：

*   **カスタマーサービスエージェントが、コアアプリケーションの外でエンドユーザーデータを管理できるようなツールを構築します。**カスタマーサービスのユースケースをコアアプリケーションから分離することで、エージェントがおこなったアクションの監査が容易になり、なりすましが偶然に発生するシナリオを回避することができます。
    
*   **カスタマーサポートエージェントが代理でアクションを実行する前に、エンドユーザーの確認を要求します。**同意ワークフローを確立することで、ユーザーとの信頼を構築し、エージェントがおこなう高度なアクションが特定のユーザーとのやり取りに限定されることを保証することに役立ちます。
    

おこなうべきでない：

*   **カスタマーサービスエージェントがエンドユーザーとしてログインできるようにします。**カスタマーサービスエージェントがエンドユーザーの代理として行動する、またはエンドユーザーのエクスペリエンスを再現するシナリオは、そのように監査可能でなければなりません。エージェントがおこなったすべてのアクションは、そのように記録システムに記録されるべきです。
    

@row
### Fractured Identity

Fractured identity occurs when a user is unintentionally associated with multiple accounts.  In the case of customer service interactions, this typically occurs when agents establish a new user identity for an existing known user or when a user identity created in a customer service interaction cannot be reconciled with their digital identity.  Creating multiple digital identities for an end-user results in a poor end-user experience and can typically result in more overhead expenses wasted to reconcile the fracture.

Do:

*   **Create tooling to search for user accounts by fuzzy terms and multiple indexes.** Fractured identities are often introduced when friction is introduced into an agent’s workflow and identifying the existing account is more effort than the agent feels is worth the effort. Tooling to find the appropriate user accounts should be implemented with diligence to ensure it aligns with the necessary privacy controls avoiding overexposure of customer data.  
    
*   **Create tooling that allows a user to link disparate accounts.** If you have circumstances where fractured account identities might be common, creating self-service tooling to link or merge accounts will save time and minimize frustration for both your agents and customers.
    

Do Not:

*   **Make credentials immutable.** Users will always have justifiable cause to want to update their email, phone number, or username.  
    

@column
### バラバラになったアイデンティティ

バラバラになったアイデンティティは、ユーザーが意図せずに複数のアカウントに関連付けられる場合に発生します。カスタマーサービスとのやり取りでは、エージェントが既存の既知のユーザーに対して新しいユーザーアイデンティティを作成した場合や、カスタマーサービスとのやり取りで作成されたユーザーアイデンティティをデジタルアイデンティティと照合できない場合に、通常このような現象が発生します。エンドユーザーのために複数のデジタルアイデンティティを作成すると、エンドユーザーエクスペリエンスが低下し、断片化を照合するために多くの費用を浪費する結果になることが一般的です。

おこなうべき：

*   **ファジーな単語と複数のインデックスを使用してユーザーアカウントを検索するツールを作成します。**エージェントのワークフローに摩擦が生じ、既存のアカウントを特定することが、エージェントがその労力に見合うと感じるよりも多くの労力を要する場合、バラバラになったアイデンティティがしばしば発生します。適切なユーザーアカウントを発見するためのツールは、顧客データの過剰な露出を避けるために、必要なプライバシー制御と一致するように慎重に実装すべきです。
    
*   **異なるアカウントをリンクすることをユーザーに許可するツールを作成します。**アカウントアイデンティティがバラバラになることがよくある環境では、アカウントをリンクまたはマージするためのセルフサービスツールを作成すると、エージェントと顧客の両方にとって時間の節約とフラストレーションの最小化になります。
    

おこなうべきでない：

*   **クレデンシャルを変更できないようにします。**ユーザーは常に自分のEメール、電話番号、またユーザー名を更新したいと思う正当な理由があるはずです。
  
    

@row
### Unnecessary Friction

The most secure application is one that doesn’t exist. In that vein, it is easy to dismiss the user experience, and therefore any friction incurred by implementing rigorous security controls, as a cost of doing business securely. However, the tradeoff isn’t that simple. Bad security experiences have potential risk and financial implications; users who can find workarounds for aggravating security controls will use them. Inefficient processes can also impact your bottom line: every second that your agents spend on the phone or chat attempting to identify a customer is money spent. Review your processes to ensure there are no duplicated steps and verify that there are pathways for customers to authenticate via the same convenient factors they would employ in your web environment (such as hardware authenticators and biometrics). 

**Do:**

*   **Match the level of assurance to the risk of the operation.** It may be more appropriate for more onerous authentication processes to start with a basic level of assurance and use step-up authentication later on if necessary. Deciding which process to use might require you to work closely with your operations teams to categorize different types of actions and assign appropriate authentication methods.
    
*   **Go for stronger proofs instead of layers of weaker proofs.** Delegate as many authentication procedures as possible to something the customer **has** or something the customer **is,** as opposed to knowledge-based authentication, for both security and user experience.  
    

**Do Not:** 

*   Pile on authentication layers if they aren’t necessary to achieve an appropriate level of assurance for the support your customer needs. 
    

@column
### 不要な摩擦

最も安全なアプリケーションは、存在しないアプリケーションです。この観点から、ユーザーエクスペリエンス、つまり、厳格なセキュリティ制御を実装することによって生じる摩擦を、安全なビジネス遂行のためのコストとして片付けることは簡単です。しかし、トレードオフはそれほど単純ではありません。よくないセキュリティエクスペリエンスは、潜在的なリスクと金銭的な影響をもたらします；厄介なセキュリティ制御に対する回避策を見つけられるユーザーは、それを使用するでしょう。非効率なプロセスは、収益にも影響します：電話やチャットでエージェントが顧客を識別するために費やす時間は、1秒ごとに金銭に換算されます。重複した手順がないようにプロセスを見直し、顧客がWeb環境で使用するのと同じ便利な要素（ハードウェア認証やバイオメトリクスなど）を使って認証できる経路があるかどうかを検証します。

**おこなうべき：**

*    **保証のレベルを運用のリスクに適合させます。**より負担の大きい認証プロセスでは、基本的な保証レベルで開始し、必要であれば後でステップアップ認証を使用する方が適切かもしれません。どのプロセスを使用するかを決定するには、運用チームと緊密に連携して、さまざまなタイプのアクションを分類し、適切な認証方法を割り当てる必要があるかもしれません。

*   **Go for stronger proofs instead of layers of weaker proofs.** Delegate as many authentication procedures as possible to something the customer **has** or something the customer **is,** as opposed to knowledge-based authentication, for both security and user experience.
*   **弱い証明の積み重ねではなく、より強い証明の積み重ねを目指します。**セキュリティとユーザーエクスペリエンスの両面から、知識ベースの認証ではなく、できるだけ多くの認証手続きを顧客が**持っている**もの、あるいは**顧客自身である**ものに委ねましょう。 
    

**おこなうべきでない：** 

*   顧客が必要とするサポートに対して適切なレベルの保証を得るために必要でない認証レイヤーを重ねます。
    

@row
## Conclusion

Some concepts from this article may be new to you or instead may offer new ways of looking at and addressing age-old problems for Identity. Because there are likely as many facets to your operations as there are to your business or organization, measures to address their challenges securely won’t be one-size-fits-all. It is important to establish a strong partnership between your operations and security teams to solve problems collaboratively. Drawing from the use cases and best practices within this article, as well as other resources within, you will be well-equipped to start these conversations within your organization and begin building or improving a strategy to meet your user needs while protecting their data. 

@column
## 結論

この記事から得られるコンセプトの中には、あなたにとって新しいものもあれば、代わりにアイデンティティの古くからの問題に対する新しい見方や対処法を提供するものかもしれません。運用には、ビジネスや組織と同じようにさまざまな側面があるため、その課題に安全に対処するための方法は、一律ではありません。運用チームとセキュリティチームが強力なパートナーシップを確立し、共同で問題を解決することが重要です。この記事で紹介したユースケースとベストプラクティス、その他のリソースを活用することで、組織内でこのような会話を始め、データを保護しながらユーザーニーズを満たす戦略の構築や改善をおこなうための十分な準備が整うはずです。

@row
- - -

[^1]:  As demonstrated by the 2020 Twitter security incident, in which numerous high-profile accounts were compromised, support tooling is a low-complexity vector for high-impact attacks. See: “An Update on Our Security Incident” Twitter, July 2020. [https://blog.twitter.com/en\_us/topics/company/2020/an-update-on-our-security-incident.html](https://blog.twitter.com/en_us/topics/company/2020/an-update-on-our-security-incident.html)
    
[^2]:  “Terminology in the IDPro Body of Knowledge,” IDPro Body of Knowledge, accessed 17 April 2021, [https://bok.idpro.org/article/id/41/](https://bok.idpro.org/article/id/41/).
    
[^3]:  Ibid.
    
[^4]:  Ibid.
    
[^5]:  Ibid.
    
[^6]:  Ibid.
    
[^7]:  Kaushik, Nishant, “Designing MFA for Humans,” IDPro Body of Knowledge, 30 October 2020, [https://bok.idpro.org/article/id/49/](https://bok.idpro.org/article/id/49/).
    
[^8]:  “NIST 800-63b FAQ”. January 2020. [https://csrc.nist.gov/publications/detail/sp/800-63b/final](https://csrc.nist.gov/publications/detail/sp/800-63b/final)
    
[^9]:  Paul Grassi (NIST), Elaine Newton (NIST), James Fenton (Altmode Networks), Ray Perlner (NIST), Andrew Regenscheid (NIST), William Burr (Dakota Consulting), Justin Richer (Bespoke Engineering), Naomi Lefkovitz (NIST), Jamie Danker (DHS), Yee-Yin Choong (NIST), Kristen Greene (NIST), Mary Theofanos (NIST). “Digital Identity Guidelines: Authentication and Lifecycle Management,” Section 5.1.1.1, National Institute of Standards and Technology Special Publication 800-63B, June 2017. [https://csrc.nist.gov/publications/detail/sp/800-63b/final](https://csrc.nist.gov/publications/detail/sp/800-63b/final)
    
[^10]:  Barrett, Brian, “How to Protect Yourself Against a SIM Swap Attack,” Wired, 19 August 2018, [https://www.wired.com/story/sim-swap-attack-defend-phone/](https://www.wired.com/story/sim-swap-attack-defend-phone/).
    
[^11]:  Saxe, Dean, “Account Recovery,” IDPro Body of Knowledge, 19 April 2021, [https://bok.idpro.org/article/id/64/](https://bok.idpro.org/article/id/64/).
    
[^12]:  Koot, André, “Introduction to Access Control,” IDPro Body of Knowledge, 17 June 2020, [https://bok.idpro.org/article/id/42/](https://bok.idpro.org/article/id/42/) and McKee, Mary, “Policy-Based Access Control,” IDPro Body of Knowledge, 19 April 2021, [https://bok.idpro.org/article/id/61/](https://bok.idpro.org/article/id/61/).
    
[^13]:  “2020 Verizon Data Breach Incident Report” P 7. Gabriel Bassett, C. David Hylender, Philippe Langlois, Alexandre Pinto, and Suzanne Widup.  [https://enterprise.verizon.com/resources/reports/dbir/2020/introduction/](https://enterprise.verizon.com/resources/reports/dbir/2020/introduction/)
