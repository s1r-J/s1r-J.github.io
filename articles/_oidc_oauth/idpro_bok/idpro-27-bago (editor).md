---
layout: columns
title: "Introduction to Identity - Part 1: Admin-time"
permalink: /docs/oidc_oauth/idpro_bok/27
date: 2024-09-09
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "管理時間", "admin-time"]
---

@row
## Abstract

This article introduces the concepts of digital identity and identity and access management (IAM). It also discusses the constituents that identity professionals serve, compares and contrasts business-to-employee (B2E) and business-to-consumer (B2C) identity use cases, and considers IAM technologies from the perspective of administrative, or admin-time, technologies. IAM technologies and use cases that focus on active, live interactions, or run-time, are mentioned for comparison.

Keywords: Digital Identity, B2E, B2C, Systems

@column
## Abstract

この記事ではデジタル・アイデンティティと、アイデンティティとアクセス管理（IAM）の概念を紹介しています。また、アイデンティティ専門家が提供する構成要素について議論し、企業対従業員（B2E）および企業対消費者（B2C）のアイデンティティ・ユースケースを比較および対比し、 管理および管理時間の観点からIAMテクノロジーを考察します。比較のため、アクティブでライブなやり取り（つまり実行時）に焦点を当てたIAMテクノロジーおよびユースケースについて説明します。

Keywords: デジタル・アイデンティティ, B2E, B2C, システム

@row
By Ian Glazer, edited by Espen Bago

© 2021 IDPro, Ian Glazer

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code)._

@row
## Introduction: How to Approach Identity and IAM

Digital identity is a big topic; it touches every aspect of an enterprise’s technical systems and services. This article is not going to offer a taxonomy of identity. Instead, it supports the idea that every individual and organization will likely approach digital identity from a different perspective and level of understanding, given their specific (yet perfectly valid) needs for their local identity system or service.

Identity is an often-debated term. Long-time practitioners and new members of the industry alike struggle with what “identity” means. This article suggests there is not a one-size-fits-all, definitive definition of identity. Instead, it encourages the reader to consider their own local context and adapt the rough definitions here to fit their organization.

This article takes a contextual approach, showing some possible ways of dividing up the IAM world and offering some examples of usage in context. Keep in mind that IAM is not just about technology. It is about the profession itself and us as practitioners.

@column
## イントロダクション：どのようにアイデンティティとIAMに関わるか

デジタル・アイデンティティは大きなトピックです。エンタープライズのシステムおよびサービスの全ての面に関わっています。この記事ではアイデンティティの分類には触れません。代わりに、ローカルのアイデンティティ・システムまたはサービスに対して特定の（ただし完全に正当な）ニーズが存在する前提で、 全ての個人と組織が異なる観点と理解度をもってデジタル・アイデンティティに関わる可能性が高いことを支持します。

アイデンティティは頻繁に議論される単語です。長年の実践者と業界の新参者は「アイデンティティ」の意味について同じように悩んでいます。この記事ではアイデンティティの万能で最も正確な定義は存在しないことを提唱しています。代わりに、読者が自分たちのコンテキストを検討し、その組織に合うようにここでの大まかな定義を適応することを推奨します。

この記事では、IAMの世界を分類するための考えられるいくつかの方法を示し、状況に応じた使い方の例をいくつか紹介することでコンテキストに合った関わり方を取り上げます。IAMは単なる技術のことではないことに注意してください。IAMはプロフェッショナルそのものであり、私たち実践者そのものなのです。

@row
### Terminology

Access Certification – Certification is the ongoing review of who has which accesses (i.e., the business process to verify that access rights are correct).

Entitlement Management – Cataloging and managing all the accesses an account may have. This is the business process to provision access.

Identity Analytics and Intelligence (IdA) - Identity analytics and intelligence mean looking at entitlement data, looking at the assignment of that, and trying to figure out and define what risk looks like. IdA provides a risk-based approach for managing system identities and access, with the intention of centralizing governance, visibility, and reporting for access-based risk.

Identity Governance and Administration - a discipline that focuses on identity life cycle management and access control from an administrative perspective.

Identity Proofing - accruing evidence to support “who this is.” Identity proofing is the last, but not the least, important part of this admin-time section. This is the process of collecting and verifying information about a person for the purpose of providing an account or a corresponding credential. This is typically performed before an account is created or the credential is issued, or a special privilege is granted.

Joiner/Mover/Leaver: The joiner/mover/leaver lifecycle of an employee identity considers three stages in the life cycle: joining the organization, moving within the organization, and leaving the organization.

Privileged Account Management - focusing on special control for risky high-level access. Privileged Account Management (PAM) is a mechanism for getting those special accounts under control.

Role Management - a way to group access rules to make them more manageable

Role-Based Access Control (RBAC) - the use of roles at run-time; a way to govern who gets access to what through the use of roles.

Sources of “Truth” - where authoritative data about individuals live.

User Provisioning and Lifecycle Management - how user records get where they need to be but only as long as they are needed

@column
### 用語

アクセス確認（Access Certification） - アクセス確認は、誰がどこにアクセスしたかを継続的な再確認することです。(すなわち、アクセス権が正しいかどうかを検証するビジネスプロセスです)

エンタイトルメント管理（Entitlement Management） - アカウントが持つ可能性のあるすべてのアクセスをカタログ化して管理します。これは、アクセスを提供するためのビジネスプロセスです

アイデンティティ・アナリティクス＆インテリジェンス（IdA）（Identity Analytics and Intelligence） - アイデンティティ・アナリティクス＆インテリジェンスとは、エンタイトルメント・データを見て、その割り当てを見て、リスクがどのようなものかを把握し、定義しようとすることを意味します。IdAは、システムのアイデンティティとアクセスを管理するためのリスクベースのアプローチを提供し、アクセスベースのリスクに対するガバナンス、可視性、レポートを一元化することを目的としています。

アイデンティティ・ガバナンスと管理（Identity Governance and Administration） - 管理の観点からアイデンティティのライフサイクル管理とアクセスコントロールに焦点を当てた学問分野。

身元確認（Identity Proofing） - 「これが誰なのか」を裏付ける証拠を積み重ねること。身元確認はこの管理時間セクションの最後であり、少なくない重要な部分である。これは、アカウントまたは対応するクレデンシャルを提供する目的で、人に関する情報を収集し、検証するプロセスです。これは通常、アカウントが作成されるか、クレデンシャルが発行されるか、または特別な特権が付与される前に実行されます。

Joiner/Mover/Leaver (ジョイナー/ムーバー/リーバー) - 従業員アイデンティティの参加/移動/離脱のライフサイクルでは、組織への参加、組織内での移動、および組織からの離脱という3つの段階を考慮します。

特権アカウント管理 - リスクの高いハイレベルなアクセスに対する特別なコントロールに焦点を当てる。PAM（Privileged Account Management）は、これらの特別なアカウントを制御するための仕組みです。

ロール管理 - アクセスルールをグループ化し、より管理しやすくする方法。

ロールベースアクセス制御 (RBAC) - 実行時のロール使用;ロールを使用して誰が何にアクセスできるかを管理する方法。

「真実」 の情報源 - 個人に関する信頼できる（権威ある）データが存在する場所。

ユーザー・プロビジョニングとライフサイクル管理 - ユーザーの記録が必要なときに必要な期間だけ取得できる方法。

@row
### Constituencies - who is it that we serve?

It is easy to lose the forest for the trees in the world of IAM, as there are so many little bits, nuances, abbreviations, and random factoids. Thinking about the ultimate stakeholder for whom the identity work is being done is one way to keep your focus on the big picture.

There are a variety of different constituencies that we serve as identity professionals, which means a variety of different technologies are needed to help them. These groups may include the traditional employee or the more complex groups such as customers, non-paid employees, contractors, and those not within the usual confines of an organization.

Whether that constituency covers employees, business partners, citizens, or students, in everything you do as an identity professional, you should keep the individual’s experience in mind. Holding the individual in mind grants more context and a broader view. This approach helps you to realize that “Hey, the reason why I am doing this automated provisioning project is that we’re about to hire 5000 new people, and we’ve got to make them productive on their first day of work.”

@column
### 顧客 - 私たちは誰にサービスを提供するのか？

IAMの世界には、非常に多くの小さな断片、ニュアンス、略語およびまとまりのない事実があるため、木を見て森を見ずになりがちです。アイデンティティに関する作業をおこなう最終的なステークホルダーについて考えることが全体像に焦点を合わせ続けるための方法のひとつです。

アイデンティティの専門家としてサービスを提供する先には様々な異なる顧客層が存在することは、彼らを支援するために様々な異なるテクノロジーが必要であることを意味します。これらのグループには、従来通りの従業員や、顧客、無給の従業員、請負業者および通常の組織の範囲内にない人々など、より複雑なグループが含まれる場合があります。

従業員、ビジネス・パートナー、市民、学生などどのような対象であっても、アイデンティティの専門家としておこなうすべての活動において、個人の経験を念頭に置く必要があります。個人を意識することで、より多くのコンテキストと幅広い視野を得ることができます。このアプローチは、「私がこの自動プロビジョニング・プロジェクトをおこなう理由は、これから5000人の新人を雇うからで、彼らの仕事初日を生産的にしなければならない」ということを認識するのに役立ちます。

@row
#### Business-to-Employee (B2E): Making Employees Productive

For employees and contractors, the primary concern is productivity. The business wants their staff to be productive on day one and want their access removed immediately on separation. The mission here is to get the right access to the right people at the right place at the right time. That’s what identity professionals are trying to do: get the appropriate access to people so they can be productive.

More often than not, the Human Resources (HR) department is in charge of employee data, and the HR system is the source of truth. Challenges with this include:

*   Potential data integrity issues
    
*   The organization may have multiple HR systems.
    
*   Other non-employee data may (or may not!) reside in this HR system.
    

Regardless of the challenges involved, this is most typically our source of truth because if someone shows up in the HR system, they are going to get paid, so we need to make them productive; that’s a very practical source of truth.

If there is one quote to think about with employee identity, it is “Who has access to what?” It is about making sure that the right people have access to the right stuff. The governing lifecycle, in this case, is the one known as “Joiner/Mover/Leaver”:

*   People **join** an organization.
    
*   Their roles change as they **move** within the organization.
    
*   Eventually, they **leave** an organization.
    

The HR system (or systems) acts as a source of truth for employee lifecycle events and related data, such as role or job codes.

Although contractors have similar identity and access-related needs, they may not share the same sources of truth. There may be instances where the HR system does not include the contractor population. Finding a singular source of truth for a contractor can be a real challenge in many enterprises. Some use their procurement system, some use bespoke systems, some use spreadsheets, and some even use their user account provisioning system. For temporary or seasonal workers, it may be most efficient to use a social media identity provider to onboard these types of short-term staff, provided that the organization can obtain the necessary level of assurance.

@column
#### 企業対従業員（B2E）：従業員の生産性を向上させる

従業員や請負業者にとって、一番の関心事は生産性です。企業は、従業員が初日から生産的に働くことを望み、離職後は直ちにアクセス権を削除することを望んでいます。ここでの使命は、適切な人に適切な場所で適切な時間に適切なアクセス権を与えることです。これこそ、アイデンティティの専門家が目指しているもの、適切なアクセス権を人々に提供して彼らが生産的に働けるようにすることです。

多くの場合、人事（HR）部門が従業員データを管理しており、人事システムが信頼できる情報源となっています。これには、以下のような課題があります：

*   データの整合性に問題がある可能性
    
*   組織には複数の人事システムが存在するかもしれないこと
    
*   非従業員データが、この人事システムに存在する可能性（もしくは存在しない可能性）
    

以上のような課題はありますが、これが我々のほとんどの一般的な信頼できる情報源です。従業員が人事システム上に存在するということは、給料が支払われるということであり、彼らの生産性を高める必要があります。つまりこれは非常に実用的な信頼できる情報源です。

従業員のアイデンティティについて考えることを一言で表すと、「誰が何にアクセスできるのか？」になります。適切な人に適切なモノへのアクセス権を確実に提供することです。ここでは、ライフサイクルの管理は、「Joiner/Mover/Leaver」として知られています。

* 人は、組織に **参加** します。

* 人は、組織内の異動によってその役割も **変化** します。

* やがて、人は組織を **離脱** します。

HRシステム（複数のこともあります）は、従業員のライフサイクル・イベントと役割や職務コードなど関連データについての信頼できる情報源として機能します。

請負業者にも同様にアイデンティティとアクセスに関するニーズがありますが、同じ信頼できる情報源は共有しないでしょう。人事システムには、請負業者の情報が含まれていない場合があります。多くの企業において、請負業者のための信頼できる情報源を見つけることは難しいです。購買システムを使ったり、特注システムを使ったり、プレッドシートを使ったり、さらにはユーザーアカウントのプロビジョニングシステムを使ったりすることもあります。派遣社員や季節労働者の場合、組織が必要なレベルの保証を得られる前提で、短期スタッフの受け入れにソーシャルメディアのアイデンティティ・プロバイダーを利用することが最も効率的かもしれません。

@row
#### Business-to-Business (B2B): Connecting to Partners

The next constituency is our business partners. In every industry, we need to connect with our business partners. This connection is really about making sure that members of your supply (or value) chain can interact with you: You are giving them apps to use to work with you, but where do the identity records for these people come from?

Ideally, partners arrive with the identity bits provided by their organization. In that case, we are dealing with the business partner’s system of record, likely their HR system, and you are one degree removed from it. This distance often means that you have delegated the administration of doing life cycle management. However, in high-risk applications, the owner of the application may want to control the access rather than trusting the business partner.

From an IAM perspective, B2B and B2E are very similar. The key difference is the source of truth. Often the enterprise doesn’t have a system that specifically tracks individuals who are employees of their business partners. Instead, they delegate the management of those people to other systems, either in their own enterprise or in the partner’s organization. More often than not, the IAM systems become a de facto source of truth for individual partner identities.

@column
#### 企業対企業（B2B）：パートナーとの連携

次は、ビジネスパートナーです。どの業界においても、ビジネスパートナーとのつながりは必要です。この繋がりは、サプライ（またはバリュー）チェーンのメンバーが、あなたと連携できるようにすることを指します。一緒に仕事するために使うアプリを提供しますが、ビジネスパートナーたちのアイデンティティ情報はどこから来るのでしょうか？

理想的には、ビジネスパートナーのアイデンティティは彼らが所属する組織から提供されたものを利用します。その場合、ビジネスパートナー側で保有するシステム（恐らくHRシステム）の情報を扱うことになりますが、あなたはそこから一段階離れた場所にいます。しばしば、この距離はビジネスパートナーのアイデンティティのライフサイクル管理を委任することを意味します。しかし、リスクの高いアプリケーションでは、ビジネスパートナーを信頼するよりもアプリケーションの所有者がアクセス制御したいと思うかもしれません。

IAMの観点からは、B2BとB2Eは非常に似ています。主な違いは信頼できる情報源です。多くの場合、ビジネスパートナーの従業員個人を具体的に追跡するシステムを企業は保有していません。代わりに、それらのビジネスパートナーの従業員の管理を彼ら自身の企業またはパートナーの組織のいずれかのシステムに委任します。ほとんどの場合、IAMシステムは個人のパートナーのアイデンティティに対する事実上の信頼できる情報源になります。

@row
#### Business-to-Consumer (B2C): Digitally Engage

Last but not least is Business-to-Consumers (B2C). B2C is about bringing whatever the awesome thing is that your organization does or sells to the people. When you talk to the people in your business building the consumer-facing service, you’ll often hear them describe the way a consumer interacts like this: “The person is going to do this, and then the person is going to do this.” And an identity professional would ask questions like “How did that person get there?” and the answer would be, “Well, yeah, they logged in.” And suddenly, you realize that the people building the service have no idea what we as identity professionals do at all. This lack of understanding is an amazing opportunity to make that awesome thing that your organization does get to the right people. That is your mission.

But in this world, the life cycles are different. It is about the individual, the citizen, the consumer. In many ways, they are in control of the life cycle, not you, and you have to be able to accommodate that.

The mission of the business is, “I want to deliver an awesome experience.” No one is in the business of just giving people an account and calling it a day. In a B2C setting, you cannot say, “Great! You can log in; I am done here.” No, that is just the beginning of the relationship. There is a focus on the customer experience, and we as identity professionals are helping deliver that experience. We are a critical onramp for it.

B2C use cases illustrate that we, as identity professionals, are not alone in our enterprises. We cannot get our jobs done without our peers in security and privacy. There are three legs in this stool to make it work. For privacy, identity provides operational controls, especially in the context of access to data. And for security, identity offers a valuable framework. We put the “who” in the “who the heck is on my network” kind of questions. So if you are working in a B2C (or B2B) setting, and you have not met your peers in the privacy and the security team, go seek them out. They have valuable tools that you can help enrich and that can help you as well.

@column
#### 企業対消費者（B2C）：デジタルなエンゲージ

最後に、企業対消費者（B2C）です。B2Cとは、組織が実施したり販売したりする素晴らしい何かを人々に提供することです。消費者向けサービスを構築している企業の担当者と話すと、消費者がやり取りすることを次のように説明することをよく耳にするでしょう：「その人はこれをしようとしていて、それからこれをしようとしています」。すると、アイデンティティの専門家は、「その人はどうやってそこにたどり着いたのですか？」と質問をするとその答えは、「ええ、彼らはログインしました」です。そして唐突に、サービスを構築している人々はアイデンティティの専門家としての私たちが何をしているのか全く分かっていないということに気が付きます。この理解の欠如は、あなたの組織が作っている素晴らしいものを適切な人々に提供するための素晴らしい機会です。それがあなたの使命です。

しかし、ここではライフサイクルに違いがあります。ライフサイクルは個人、市民、消費者に関するものです。多くの場合で、あなたではなく彼らがライフサイクルを管理しており、あなたはそれに対応する必要があります。

ビジネスの使命は、「素晴らしい体験を提供したい」です。人々にただアカウントを与えて、それで終わりというビジネスをしている人は誰もいません。B2Cの場合、「素晴らしい！ログインできます。ここで終わりです。」とはなりません。それは繋がりの始まりにすぎません。カスタマーエクスペリエンスに重点が置かれており、アイデンティティの専門家として私たちはその体験の提供を手助けしています。私たちはそのための重要な合流車線の役割を果たすのです。

B2Cのユースケースでは、アイデンティティの専門家として私たちが企業内で孤独でないことを示しています。セキュリティとプライバシーを担当する同僚がいなければ、仕事を成し遂げることはできません。このスツールは3本の脚（軸）がありますことで機能します。プライバシーにとって、アイデンティティは特にデータへのアクセスという文脈で、運用上の制御を提供します。また、セキュリティにとって、アイデンティティは貴重なフレームワークを提供します。アイデンティティの専門家は、「誰が私のネットワークにいるのか」という質問の「誰」を埋めます。したがって、B2C（またはB2B）で仕事をしていて、プライバシーおよびセキュリティチームの同僚に会ったことがない場合、彼らを探しに行ってください。彼らは、あなたが改善させることができ、あなたを助けてくれる貴重なツールを持っています。

@row
## Technologies Involved - Admin-time vs. Run-time

Having established the constituencies we serve, it is time to look at some of the technologies we use to do that. One approach among many valid ways of sorting out the various technologies and terms is to split the world into administrative (or admin-time) and run-time discussions.

Essentially, the technologies and disciplines used to set things up are on the admin-time side, and the things that are being used when the user is logging in or going through a forgot-password process are on the run-time side.

@column
## 関連する技術 - 管理時間 vs. ランタイム

私たちがどのような人々にサービスを提供するのかがわかったところで、そのために利用する技術のいくつかについて考えましょう。様々な技術や用語を整理する有効な方法の一つは、管理（管理時間）とランタイムを分けて議論する方法です。

基本的に、物事を設定するために使用される技術や分野は管理時間に分類され、ユーザーがログインしたりパスワード忘れ対応をしたりするさいに使用される技術や分野はランタイムに分類されます。

@row
### Admin-time Technologies

The three main areas within the admin-time sphere are:

*   Sources of “Truth” - where authoritative data about individuals live.
    
*   Identity Governance and Administration - a discipline that is really about life cycle management and access control from an administrative perspective.
    
*   Identity Analytics and Intelligence - of particular interest to large firms to help assure access is correct.
    

Two additional areas are also admin-time but do not always fit in the same bucket. Some industry analysts like to add these categories:

*   Privileged Account Management - focusing on special control for risky high-level access.
    
*   Identity Proofing - accruing evidence to support “who this is.”
    

@column
### 管理時間に関する技術

アドミン時間領域内の主な領域は以下の3つです。

- 信頼できる情報源 - 個人に関する権威あるデータが存在する場所

- アイデンティティ・ガバナンスと管理 - 管理の観点からライフサイクル管理とアクセス制御に関する分野

- アイデンティティ分析とインテリジェンス - 大企業が特に関心を持つ、アクセスが正しいかどうかを保証するためのもの

さらに以下の2つの領域も管理時間ですが、必ずしも同じバケツに入るわけではありません。一部の業界アナリストは、これらを追加することを好んでいます：

- 特権アカウント管理 - リスキーな高レベルのアクセス権に対する特別なコントロールに焦点を当てる

- 身元確認 - 「この人は誰なのか」を裏付ける証拠の収集

@row
#### Sources of “Truth”

How do I know who someone is? That may be too difficult a question to answer from both a metaphysical and practical perspective. We can instead rephrase it to: “How can I find reasonably good, authoritative records about people? I need to send their paycheck somewhere.” Or, “I need the shipping address of my business partner. How do I find this data?” [^1]

For employees, the answer tends to be HR. For partners, it tends to be that delegated admin one step removed from their HR system. And in consumer settings, things get more complicated. In low-risk areas, the answer is the individual. They are the authoritative source for much of the information you will use. For convenience, this may come from a social media profile, for instance. But in higher risk areas such as financial or medical, the answer may include authoritative sources such as their institution of higher learning or their local government. In an educational setting, a student information system may serve as a source of truth for students.

Data quality is an essential element here. We depend on data for doing things like ensuring people have the right access. But the data from the source of truth is not always reliable, so we may have to operate under the assumption that data quality issues may exist.

@column
#### 信頼できる情報源

どうすればその人が何者かわかるでしょうか？形而上学的な観点からも実用的な観点からも、あまりにも難しい質問かもしれません。その代わりに、こう言い換えることができます：「どうすれば、その人についての合理的で権威のある記録を見つけることができるのか？その人の給料をどこかに送金する必要がある」。あるいは、「ビジネス・パートナーの配送先が必要だ。このデータはどうやって探せばいいのだろう？」 [^1]

従業員の場合、その答えはHRシステムとなる傾向にあります。ビジネス・パートナーにとって、HRシステムからは離れた管理者に委任する傾向にあります。そして、消費者の場合には、さらに複雑なことになります。リスクの低い領域であれば、答えは個人です。これは利用するであろう多くの情報の信頼できる情報源となります。より簡単に、例えばソーシャルメディアのプロフィールから取得することもあります。しかし、金融や医療のようなリスクの高い領域では、答えは高等教育期間や地方自治体のような信頼できる情報源が含まれます。教育分野では、学生情報システムは学生にとって信頼できる情報源として機能する可能性があります。

ここでは、データの質は重要な要素です。ある人が正しいアクセス権を有していることを保証するためにデータに依存しています。しかし、信頼できる情報源からのデータは常に信頼できるわけでないため、データ品質に問題が存在する可能性があるという前提の下で操作をおこなう必要があります。

@row
#### Identity Governance and Administration

These are the tools that manage who has access to what. They are the tools that rely on a source of truth (the who) to govern entitlements (the access) in target systems (the what) via connectors.

Identity Governance and Administration (IGA) tools are traditionally more focused on employees, contractors, or students. These tools can often be thought of as more traditional, enterprise-centric tools related to ERP systems.

This area is considerably larger than the other five areas of the admin-time sphere, and our coverage here will focus on the following subsections of it:

*   User Provisioning and Lifecycle Management - how user records get where they need to be but only as long as they are needed
    
*   Entitlement Management – the business process to provision access
    
*   Role Management - a way to group access rules to make them more manageable
    
*   Role-Based Access Control (RBAC) - the use of roles at run-time
    
*   Access Certification – the business process to verify that access rights are correct
    

@column
#### アイデンティティ・ガバナンスと管理

これらは誰が何にアクセスできるのかを管理するツールです。これらは、コネクタを介してターゲットシステム（何に）で資格（アクセス権）を管理するために、信頼できる情報源（誰が）に依存しているツールです。

アイデンティティ・ガバナンスと管理（IGA）ツールは伝統的に従業員、請負業者や学生によりフォーカスしています。これらのツールは、多くの場合、ERPシステムに関連した従来型のエンタープライズ中心のツールと考えられます。

この領域は管理時間の範疇にある他の5つの領域よりもかなり大きく、ここでは以下のサブセクションに焦点を当てます：

*   ユーザー・プロビジョニングとライフサイクル管理 - 必要な場所に必要な期間だけユーザーレコードを取得する方法
    
*   エンタイトルメント管理 – アクセス権をプロビジョニングするためのビジネスプロセス
    
*   ロール管理 - アクセスルールをより制御しやすくするためにグループ化する方法
    
*   ルールベースアクセス制御(RBAC) - ランタイムでのロールの利用
    
*   アクセス権認定 – アクセス権が正しいことを検証するビジネスプロセス
    

@row
##### User Provisioning and Lifecycle Management

User provisioning is the mechanism that helps create, maintain, and eventually remove user accounts in target systems. This mechanism can listen to joiner/mover/leaver events from sources of truth (for example, a connector to the HR system listening for events such as the addition of a new hire). That event then triggers the provisioning system to evaluate the user through business rules in order to undertake required actions, such as create a new user account in Active Directory. The mechanism also has rules describing what those triggered actions are, such as to start setting up access based on some attributes from the new hire data. That typically means assigning entitlements, which can be something that requires approval. For basic entitlements like “birthright” access, we may not need approval. For example, all employees should get access to the productivity suite and email, none of which require approval. If, on the other hand, someone wants to obtain access to the mainframe as a sysadmin, that is going to take some approval. You will have both types — access requiring explicit approval as well as access that does not — in almost all organizations.

A common mistake is to try to automate everything. Avoid this! There are hundreds, if not thousands, of systems and services in your enterprise. Trying to automate provisioning to all of that is just diminishing returns. So what then should be automated? The candidates to look for are the systems with the largest user populations or the highest turnover in those systems. Automation is essential for high-volume or high-velocity systems. Other candidates are systems with too many requests for your helpdesk team to manage, or the ones so sensitive that you want to lock down the rules of who gets access to it. Those make sense to automate.

Day one access systems are excellent candidates for automation. Partly because it is to some extent non-controversial; you get email, you get productivity, you get inside the employee portal, maybe you get VPN. Creating these user accounts has to happen for all new employees and represents a large administrative burden ripe for automation.

After day one onboarding and for the vast number of remaining systems, you are going to provision additional access manually. This means either people will ask for access and/or you will manually create the account (often because you do not need to do it very often.) And in some cases, that system that you want to create an account in exists away from your sphere of direct influence; you will not have a connector to the system. For such systems, the only way you can get to it is by opening up a support ticket, and a human will have to directly access the system to create or change the user account. These typically do not need to be automated.

Lastly, provisioning systems are often involved in setting up passwords. This involvement means that provisioning systems often need to have aggregate password content rules. That exposes all sorts of challenges because different systems can have radically different internal rules and password capabilities. For example, you may have a password content rule that mandates the inclusion of a special character. Because of system proclivities, a person could provide a password with a special character that the Oracle database could not accept, but Active Directory could. User provisioning (or password management) systems have to deal with these potential problems as gracefully as possible.

@column
##### ユーザー・プロビジョニングとライフサイクル管理

ユーザー・プロビジョニングは、ターゲットシステムでユーザーアカウントを作成、管理および最終的に削除するのに役立つメカニズムです。このメカニズムは、信頼できる情報源からJoiner/Mover/Leaverイベントを待ち受けています（たとえば、HRシステムへのコネクターが新規雇用による追加のようなイベントを待ち受けるなど）。次に、そのイベントはプロビジョニングシステムをトリガーし、Active Directoryに新しいユーザーアカウントを作成するなどの必要なアクションを実行するため、ビジネスルールを通じてユーザを評価します。このメカニズムには、トリガーされたアクションが何であるかを記述するルールもあります。例えば、入社初日から、いくつかの属性に基づいてアクセス権の設定を開始するような場合です。これは一般的にエンタイトルメントの割り当てであり、承認が必要となることもあります。生まれながらの」アクセス権のような基本的なエンタイトルメントについては、承認は必要ないでしょう。例えば、全従業員は承認の必要なく、オフィススイートや電子メールにアクセスできるようにすべきです。一方、誰かがシステム管理者としてメインフレームへのアクセスする権利が欲しい場合、それには承認が必要にります。明示的な承認が必要なアクセス権とそうでないアクセス権の両方が、ほとんどすべての組織には存在しています。

よくある間違いは、すべてを自動化しようとすることです。これを避けてください！企業には数千とは言わないまでも数百のシステムとサービスが存在します。全てを自動プロビジョニングしようとすることは、成果を減らすことになります。では、何を自動化する必要があるでしょうか。候補はシステム内の最大のユーザー人口を持つシステムまたは最もユーザーの出入りがあるシステムです。大容量または高速なシステムに自動化は不可欠です。他の候補としては管理をおこなうヘルプデスクチームにリクエストが多すぎきるシステムや、機密性が高くするために誰がアクセスできるのかを定めるルールを変更できないようにしたいシステムなどです。それらは自動化するのが理にかなっています。

入社初日にアクセスするシステムは、自動化の優れた候補です。部分的には、それがある程度議論の余地がないためです。電子メールを取得し、オフィススイートを使い、従業員ポータルにアクセスし、おそらくVPNを取得します。これらのユーザーアカウントの作成は、すべての新入社員に対して実施しなければならず、自動化するのに非常によい例です。

入社初日のオリエンテーションのあと、残りの多くのシステムでは、手動で追加のアクセス権をプロビジョニングすることになります。これは人々がアクセス権を要求知ると手動でアカウントを作成することを意味します（頻繁に実施する必要はないでしょうから）。また、場合によっては、アカウントを作成したいシステムが自分の直接の影響範囲外に存在し、そのシステムとのコネクターがないことがあります。そのようなシステムでは、サポートチケットを発行して、人間が直接システムにアクセスしてユーザーアカウントを作成・変更するしかありません。これらは通常、自動化する必要はありません。

最後に、プロビジョニングシステムは、しばしばパスワードの設定に関与します。このことは、プロビジョニングシステムが、パスワードの内容に関するルールを集約する必要があることを意味します。システムによって内部ルールやパスワードの機能が大きく異なるため、さまざまな課題が発生します。例えば、特殊文字の使用を義務付けるパスワードコンテンツルールがあるとします。例えば、パスワードの内容に特殊文字の使用を義務付けたとします。あるユーザーが、Oracleデータベースでは受け入れられないが、Active Directoryでは受け入れられる特殊文字を含むパスワードを提供した場合、ユーザー・プロビジョニング（またはパスワード管理）システムは、このような潜在的な問題にできる限りグレースフルに対処しなければなりません。

@row
##### Entitlement Management

Now we have a source of truth and users flow into a data repository, and that triggers our user provisioning systems and starts creating users in our target applications or services. But it is not enough just to create a user account; we also have to know what that account can do. This set of actions is what we call entitlement management. Entitlement management can get really detailed really fast because the total of all the little privileges that govern what a user can do in a system can be extremely numerous. It is not unheard of to have hundreds, if not thousands, of individual privileges in a system. Those privileges are often aggregated into user groups or roles, which can also become quite numerous. It is like grains of sand on the beach, which is why we try to aggregate them together. Imagine you have three employees, one system, and four privileges in it: Create Purchase Order (PO), Update PO, Read PO, and Delete PO. Connecting each person to the right collection of privileges is possible, but it becomes unmanageable very quickly.

That’s where layers of abstraction come in: We put this thing in between the user and the privileges called an entitlement. We say, “This allows you to manage purchase orders.” And it is these things that the provisioning system hands out, instead of the detailed privileges themselves, because there are way too many discrete privileges to keep track of. We abstract the details and instead say, “Here’s an ability,” or “Here’s something associated with your job responsibility.” Unfortunately, those discrete, detailed privileges still need to exist in order to allow the level of granularity an organization’s business processes require, and to provide the level of instruction to the system that can be coded into the environment.

Entitlement management means cataloging all the accesses a person can have, which can be a massive undertaking. For example, a medium-sized bank may have ten major systems (but often a lot more), which means you may have thousands upon thousands of privileges, which are aggregated into a thousand or so entitlements. You then need to figure out how to map that to the business needs. Entitlement management is this cataloging process.

Ideally, you are bundling privileges together into sets that make some semblance of sense for people and the organization. For example, imagine that you want to gather all the entitlements together that someone who works in purchasing would need. Or that you want to make sure you have put together the relevant entitlements that someone who is a business partner - at the gold tier but not the silver tier - has access to. This level of efficiency is what you and your identity colleagues are working towards to make access to enterprise resources manageable.

It also tends to be mandatory work if you’re ever going to do Segregation of Duty [^2] analysis, for example for Sarbanes-Oxley (SOX) [^3] compliance or General Data Protection Regulation (GDPR) [^4] compliance requirements, where we have to identify combinations of accesses that together are dangerous. For example, people who can authorize payments to partners should not be able to create a fraudulent partner and pay them.

@column
##### エンタイトルメント管理

今、私たちは信頼できる情報源を持ち、ユーザーはデータリポジトリに流れ込み、それがユーザー・プロビジョニング・システムをトリガーして、ターゲットのアプリケーションやサービスにユーザーを作成し始めます。しかし、ユーザーアカウントを作成するだけでは充分ではありません；そのアカウントが何を実施できるかについても知る必要があります。この一連のアクションをエンタイトルメント管理と呼んでいます。エンタイトルメント管理は、ユーザーがシステムで何ができるかを管理する小さな権限をすべて合わせると、非常に膨大な数になるため、すぐに詳細な情報を得ることができます。1つのシステム内に数千でなくとも数百の個人の権限が存在することも珍しくはありません。しばしば、これら権限はユーザーグループやロールに集約されますが、これらも非常に多くなります。まるで砂浜の砂粒のようであるため、集約しようとするのです。3人の社員と1つのシステム、そこに4つの権限（発注書（PO）の作成、POの更新、POの閲覧、POの削除）が存在することを想像してください。各人が適切な権限のコレクションに接続することは可能ですが、すぐに管理不能になります。

そこで、抽象化されたレイヤーが登場します：ユーザーと権限の間にエンタイトルメントと呼ばれるものを配置します。「この権限で発注書を管理できます」と説明します。プロビジョニング・システムは詳細な権限自体を提供せず、これらを提供します。なぜなら、権限の数が多すぎて管理しきれないからです。そのため、詳細な権限を抽象化し、「これが能力です」や「これはあなたの職責に関連するものです」と表現するのです。残念ながら、組織のビジネス・プロセスが必要とするきめ細かさを実現し、環境にコード化できるレベルの指示をシステムに提供するためには、こうした個別の詳細な権限が依然として存在する必要があります。

エンタイトルメント管理とは、ある人が持つことのできるすべてのアクセス権をカタログ化することであり、これは膨大な作業になります。例えば、中規模の銀行では、10個の主要なシステム（しばしば、もっと多い）があり、何千もの権限があり、それが1000以上のエンタイトルメントに集約されている可能性を意味します。そして、それをどのようにビジネスニーズに対応させるかを考える必要があります。エンタイトルメント管理は、このようなカタログ化作業です。

理想的なのは、人と組織にとってある程度意味のある権限をまとめておくことです。例えば、購買担当の人が必要とするすべての権限を集めたいとします。あるいは、ビジネス・パートナー（シルバーではなくゴールド層）がアクセスできるような関連する権限をまとめたいとします。このようなレベルの効率化は、あなたとあなたのアイデンティティ専門家の同僚が、エンタープライズ・リソースへのアクセスを管理しやすくするために取り組んでいることなのです。

また、Sarbanes-Oxley (SOX) 法 [^3] 準拠やGDPR（General Data Protection Regulation、EU一般データ保護規則）[^4] の準拠要件などのために、一緒にすると危険な権限の組み合わせを特定する必要があります。例えば、パートナーへの支払いを承認できる人は、不正なパートナーを作って支払いをすることができないようにする必要があります。特定のために職務分掌 [^2] の分析ををおこなう場合、エンタイトル管理は必須の作業になる傾向にあります。

@row
##### Role Management

But even when we have worked these entitlements down to a level where they are manageable entities in themselves, using them effectively will be very challenging. The answer to that challenge for many, though not all, organizations is to try to do something called Role Management. You may have heard of it as Role-Based Access Control (RBAC). The essence of it is as follows: in some organizations, job functions are very regular. Regular job functions are most typically found in hierarchical organizations. On the other end of the scale, this works quite poorly in matrixed organizations; that is because it is hard to pinpoint, for example, the three top job responsibilities, as they are always shifting.

Role management can be useful for saying, “These types of job responsibilities need this kind of access, so let’s call that thing a Role.” Additionally, sometimes you have this thing called a technical role, which is saying, “Here are the low-level bits you’re going to need to do your job,” and it becomes a handy bundle to assign to people. Imagine roles as a grouping to which you might provide access in a common way. You should only create roles if you are going to provision or control access to a group differently. At the highest level, you could only have a handful of roles, and you should review them regularly as your organization evolves.

@row
##### ロール管理

エンタイトルメントを減らしていき、専門家でなくとも管理可能なレベルまで落とし込んだとしても、それらを効果的に利用することは非常に困難です。すべてではありませんが、多くの組織でのこの課題に対する答えは、ロール管理と呼ばれるものを実施することです。RBAC（Role-Based Access Control）と聞いたことがあるかもしれません。その本質は次の通りです：ある組織では、職務は非常に規則的です。規則的な職務は、最も一般的に階層型の組織で見られます。一方、マトリックス型の組織では、この仕組みは非常にうまく機能しません。それは、たとえば上位3つの職務責任が常に変化しているために、職務を特定が難しいからです。

ロール管理は、「こういう職責にはこういうアクセスが必要だから、これをロールと呼ぼう」と言えるときに便利です。さらに、技術的なロールと呼ばれるものがあり、これは「仕事をするのに必要な低レベルのビットはこれだ」と言うもので、人に割り当てるのに便利なまとまりとなります。ロールは、共通した方法でアクセス権を提供するためのグループ分けと想像してください。ロールは、あるグループに対して異なる方法でアクセス権をプロビジョニングまたは制御する場合にだけ、ロールを作成すべきです。最高レベルでは、ほんの一握りのロールしか持つことができず、組織の発展に応じて定期的に見直すべきです。

@row
##### Role-Based Access Control

RBAC is just a way to govern who gets access to what through the use of roles. There is no need to overthink it. It works great in regular, hierarchical, homogeneous organizations. Not surprisingly, it works really well for places like the US Department of Defense. It does not work great for the 150-person start-up; do not try to do that.

When overthinking RBAC, or over time in general, you can get what we call a “role explosion,” where you have more roles than you have people. Some of the salty veterans say, “oh yeah, I survived that. They told me that was a good idea. It was a horrible idea.” Try to avoid this situation; it rarely ends well.

@column
##### ロールベースアクセス制御

RBACはロールを使って誰が何にアクセスできるかを管理する方法に過ぎません。考えすぎる必要はありません。一般的な階層的で均質な組織では、非常に効果的です。驚くことではありませんが、米国国防総省のようなところでは非常にうまく機能します。150人規模のスタートアップ企業ではうまくいきません；この方法を採用しないようにしましょう。

RBACを考えすぎると、あるいは一般的に時間が経つと、「ロール爆発」と呼ばれる、人の数よりロールの数が多くなる現象が発生することがあります。熟練しあベテランの中には、「ああそうだ、私はそれを乗り越えたんだ。彼らはそれが良いアイデアだと言っていた。でも、あれはひどいアイデアだった」。このような状況は避けるようにしましょう；良い結果になることはまずありません。

@row
##### Access Certification

At this point, people have access. They are productive on day one. They are productive on day two. On day three, they start to become a privileged threat because they have too _much_ access. And the best way to get more and more capabilities in an enterprise is to simply change jobs. You go from doing this job to another job, and if your business rules didn’t explicitly prevent the continuation of access, experience shows that you do not lose your old access, you just keep it on top of new accesses.

Another instance of accumulating accesses is when you onboard someone new, with the dreaded situation of “Whose access should we model you after.” Anyone who has gone through any kind of IT security audit knows how horrifying an audit can be. A common answer to the question of whom to model a set of new accesses to give to a new employee is their boss. The boss is likely to be the biggest source of access violation around because they have accreted access over years. They are a horrible person to emulate for this purpose, from a risk management perspective.

Certification is the ongoing review of who has which accesses, a process that became popular with the introduction of the Sarbanes Oxley law (SOX) in the United States. It is a great tool to prevent people from keeping access they no longer need. An auditor might say that this should be done quarterly, something that quickly becomes very fatiguing. Better methods may be to trigger reviews based on changes to entitlements, changes to overall user risk, or to try to detect if someone deviates from a norm. In other words, we want to certify whether, if compared to a set of peers, you are an outlier. We want to figure out why that is. It is a powerful way to make sure you don’t have issues with the access and entitlements that you’ve assigned in a non-automated fashion.

All of the mentioned elements add up to a lot of data flowing around. With all the users, times all the systems, times all the entitlements, times all the roles, times all the privileges, the total is staggering. How can we make sense of it all?

@column
##### アクセス権認定

この時点で、ユーザーはアクセス権を持っています。1日目は生産的です。2日目も生産的です。3日目になると、ユーザーは非常に大きすぎるアクセス権を有しているため、特権的な脅威になり始めます。そして企業内でますます多くの権限を持つための最善策は、単純に職務を変えることです。ある職務から別の職務に異動し、ビジネスルールがアクセス権の継続を明確に停止しない限り、以前のアクセス権を失効させずに、新しいアクセス権を追加することけんけんしています。

アクセス権を蓄積するもうひとつの例は、「誰のアクセス権をモデルにすべきか」という恐ろしい状況で、 新しい人物を追加するときです。あらゆる種類のITセキュリティ監査を経験したことがある人であれば、 監査がどれほど恐ろしいものであるかをわかっています。新しい従業員に与える新しいアクセス権のモデルを誰にするか、という質問に対する一般的な回答は、その上司です。上司は何年にもわかってアクセス権を増大させてきたため、アクセス権違反の最大の原因となる可能性があります。リスク管理の観点から、上司はこの目的のためにエミュレートするには恐ろしい人物です。

認定とは誰が何のアクセス権を持っているかを継続的にレビューすることであり、 アメリカ合衆国ではSarbanes Oxley（SOX）法の導入によって広まったプロセスです。不必要なアクセス権をユーザーが保持しないようにするための非常に優れたツールです。監査人は四半期ごとにおこなうべきであると言うかもしれませんが、 これはすぐに非常に重荷になります。より良い方法としては、エンタイトルメントの変更や全体的なユーザーリスクの変更に基づいてレビューを開始する、 または誰かが規則から逸脱する可能性を検知しようとすることです。言い換えると、同僚達と比較したときにユーザーが外れ値になっているかどうかを認定したいのです。外れ値になった原因を解明したいのです。これは、自動化されていない方法で割り当てられたアクセス権とエンタイトルメントに問題がないことを確認するための強力な方法です。

All of the mentioned elements add up to a lot of data flowing around. With all the users, times all the systems, times all the entitlements, times all the roles, times all the privileges, the total is staggering. How can we make sense of it all?
以上の全要素をあわせると、大量のデータが流れます。全てのユーザー、掛ける全てのシステム、掛ける全ての資格、掛ける全てのロール、掛ける全ての権、その合計は驚異的です。どのようにしてそれら全てを理解するのでしょうか？

@row
#### Identity Analytics

One of the ways is through identity analytics (IdA) and intelligence, which is more than just reporting on “Who has access to what.”

Identity analytics and intelligence mean looking at entitlement data, looking at the assignment of that, and trying to figure out and define what risk looks like. What does a normal user look like? Compared to that, what does a heavily privileged user look like? What does the model of a system administrator look like compared to developers, someone working in finance, or someone working in the field sales organization?

The goal is to find commonalities of outliers among user populations and to understand what access-related risk looks like in the organization. Other goals of IdA include being able to group commonly assigned entitlements together as candidate roles, to identify over-privileged users, to discover undocumented high privileged access rights assigned to regular, non-privileged accounts. IdA can also accurately measure and report on user, account, entitlement, application, departmental, and organizational risk posture.

IdA provides a risk-based approach for managing system identities and access, with the intention of centralizing governance, visibility, and reporting for access-based risk.

It uses dynamic risk scores and advanced analytics to determine the associated level of risk and to derive key indicators for automating account provisioning, de-provisioning, authentication, and privileged access management. This approach reduces the identity attack surface by identifying (for remediation) unnecessary, unused, and outlier access.

Another feature of this admin-time function of risk determination is that the indicators and data it produces can be integrated with, and used by, your run-time systems. For example, during the login process: If we know that a person is not particularly risky, then they might not need to be challenged for additional authentication factors. But if, on the other hand, that person has a lot of privilege and power in the systems, and maybe they deviate from the norm in their job role, then they might need to provide additional verification. Run-time risk determination analysis such as this can be partly or fully automated, depending on the quality of the indicator data and the maturity of the organization using them.

@column
#### アイデンティティ分析

その方法のひとつは、アイデンティティ分析（IdA）とインテリジェンスを利用することですが、「誰が何にアクセスできるか」について報告するだけはありません。

アイデンティティ分析とインテリジェンスとは、エンタイトルメントデータを見て、その割り当てを確認し、どのようなリスクがあるかを把握し、定義しようとすることを意味します。通常のユーザーとは何でしょうか？それに比べて、強い権限を持つユーザーとは何でしょうか？システム管理者のモデルは、開発者、財務担当者やフィールドセールスの組織で働く従業員と比べるとどのようなものでしょうか？

その目的は、ユーザー集団内の外れ値の共通点を見つけることと組織においてどのようなアクセス権に関連したリスクがあるのかを理解することです。その他のIdAの目的には、共通して割り当てられているエンタイトルメントを候補ロールとしてグループ化すること、過剰な権限を持つユーザーを特定すること、通常の非特権アカウントに割り当てられた文書化されていない高い特権的なアクセス権を発見することが含まれます。また、IdAによってユーザー、アカウント、エンタイトルメント、アプリケーション、部門および組織のリスク状況を正確に測定し、報告することができます。

IdAはシステムのアイデンティティとアクセス権を管理するためのリスクに基づくアプローチを提供し、アクセス権に基づくリスクに対するガバナンス、可視性および報告を一元化することを目的としています。

IdAは、動的なリスクスコアと高度な分析機能を用いて、関連するリスクレベルを判断し、アカウントのプロビジョニング、デプロビジョニング、認証、特権アクセス管理を自動化するための重要な指標を導き出します。このアプローチは、不要なアクセス、使用されていないアクセス、異常なアクセスを特定（修復のため）することで、アイデンティティの攻撃対象を減らします。

リスク定義の管理時間の機能の別の特徴は、作成された指標とデータをランタイムシステムと統合し、使用できることです。例えば、ログイン処理中：ある人物が特に危険な人物でないことが分かっていれば、追加の認証要素を要求する必要はないかもしれません。しかし、その一方で、その人物がシステム内で多くの特権と権力を持ち、職務上の役割において規範から逸脱している可能性がある場合は、追加検証を実施する必要があるかもしれない。このようなランタイムのでリスク判定分析は、指標データの品質とそれを使用する組織の成熟度に依存して、部分的または完全に自動化することができます。

@row
### Privileged Account Management

Some of the user accounts out there are special. Your sysadmin accounts, your root accounts, and so on. These accounts are not necessarily tied to people. But they are super privileged user accounts. We may have a whole team of people that have to act like the root administrator. Privileged Account Management (PAM) is a mechanism for getting those special accounts under control. You can essentially check them in and out as needed: “Hey, I need to go in and apply a zero-day patch, so I need to act like the root administrator for this,” and the system will grant the relevant access for that purpose, after validating who the user is. It may also record the screen, so that as the user is performing their actions, what’s going on is being logged. One use case for this could be when having a third-party service vendor who’s going to come in and do maintenance on specialized pieces of equipment, where we need to have an audit log of the actions that they took. This log would be like the record function in privileged account management. Another important function is scrambling the password for these special accounts, so that no one retains the password to the root or sysadmin account after the job is done, such as the patch job in the example above.

@column
### 特権アカウント管理

世の中には、特別なユーザーアカウントもあります。sysadminアカウント、rootアカウントなどなど。これらのアカウントは、必ずしも人と結びついているわけではありません。しかし、これらは超特権ユーザーアカウントです。ルート管理者のように行動しなければならない人がチーム全体にいるかもしれません。特権アカウント管理（PAM）は、これら特別なアカウントを管理下に置くための仕組みです。基本的には、必要に応じてチェックインとチェックアウトをおこないます：「ゼロデイパッチを適用する必要があるので、ルート管理者のように行動する必要があります」と宣言すると、システムはそのユーザーが誰であるかを確認した後、その目的のために適切なアクセスを付与します。また、画面を録画して、ユーザーが操作しているときに何が起こっているかを記録することもできます。例えば、サードパーティのサービスベンダーが特殊な機器のメンテナンスに来た場合、彼らが実施したアクションの監査ログが必要になることがあります。このログは、特権アカウント管理における記録機能のようなものでしょう。もう一つの重要な機能は、特別なアカウントのパスワードを同じにしないことです。前述の例のようなパッチ作業終了後に、rootやsysadminアカウントのパスワードを保持する人がいないようにします。

@row
### Identity Proofing

Identity proofing is the last, but not the least, important part of this admin-time section. This is the process of collecting and verifying information about a person for the purpose of providing an account or a corresponding credential. This is typically performed before an account is created or the credential is issued, or a special privilege is granted. It also tends to be a lengthier process the first time we encounter a particular individual, as opposed to the secondary proofing required for purposes of account recovery.

The process is often found in regulated industries, such as in banking, with requirements for doing Know Your Customer (KYC) and anti-money laundering. These require government documents to be presented in some fashion, proved to be accurate and valid, and then associated with the individual. This is the proofing process.

Depending on the account or credential to be issued, there are different ways of doing proofing, many tied to government-issued identity. In contrast, others are based on what we call self-asserted.

In an enterprise setting, B2E, relating to employees, proofing is a very common process, involving background checks and showing documentation (for example, your passport or a driver’s license) to get your job. For employees, we want to do this because this is how we will get a new job. But for a B2B setting, it is a very different situation. How do we onboard a new business partner? In addition to making sure who that person is, we may need proof that this is the organization we want to work with and that _this_ person is someone we want to work _within_ that organization. These different criteria make for a very different kind of proofing process.

What about identity proofing in B2C use cases? How does one know and trust a new customer who makes a claim about themselves? Here it is a question of how much we need to care about that. There is a trade-off in the B2C world between velocity versus veracity. For some organizations and apps, the priority will be velocity - to get people registered quickly and into the app as fast as possible. The user journey is optimized for this. They’ll have very limited access, and the threshold for user registration is very low.

For others, the priority is veracity, either because of the brand experience, because of the business they’re in, because of what they want to deliver in terms of value, or related to the chance of fraud. In this case, the enterprise wants more verifiable data about the person. The enterprise determines it is important to have a higher level of assurance that the new customer is really the person they claim to be.

@column
### 身元確認

身元確認は、この管理時間セクションの最後ですが、重要な部分でもあります。身元確認はアカウントまたは対応するクレデンシャルを提供する目的で、個人に関する情報を収集し、検証するプロセスです。通常はアカウントの作成またはクレデンシャルの発行、あるいは特別な権利を付与する前に実行されます。また、アカウント回復を目的に必要とされる二次的な確認とは異なり、特定の個人に初めて出会った場合にはより長いプロセスとなる傾向があります。

このプロセスは、Know Your Customer（KYC）の要件やマネーロンダリング対策要件がある銀行などの規制産業でよく見受けられます。これらの業界では、政府発行の身分証明書を何らかの形で提示し、それが正当かつ有効であることを証明し、その上で個人と関連付ける必要があります。これが身元確認のプロセスです。

発行されるアカウントまたはクレデンシャルに応じて様々な身元確認方法があり、その多くは政府発行のアイデンティティに関連付けられています。対照的に、自己主張に基づくものもあります。

B2Eのような企業において。従業員に関する身元確認は非常に一般的なプロセスであり、バックグラウンドチェックをおこない、身元確認（例えば、パスポートや運転免許証）を提示して仕事を得ます。従業員にとって、これが新しい職に就く方法だからです。しかし、B2Bでは状況が大きく異なります。どうやって新しいビジネスパートナーを獲得するのでしょうか？その人物が誰であるかを確認するだけでなく、それが一緒に仕事をしたい組織であり、 _この_ 個人が一緒に仕事をしたい組織に _所属している_ ことを検証する必要があるかもしれません。これら異なる基準は、非常に異なる種類の検証プロセスを生み出します。

B2Cユースケースでの身元確認はどうでしょうか？自分自身を主張する新しい顧客をどうやって知り、信用するのでしょうか？ここでの問題は私たちがどれだけそのことを気にかけなければならないのか、です。B2Cの世界では、速度と正確性にトレードオフがあります。一部の組織やアプリでは、優先順位は速度になります。ユーザーをすばやく登録させ、アプリにできるだけ早く登録させることです。ユーザー・ジャーニーはこのために最適化されています。アクセス権は非常に制限され、ユーザー登録の障壁は非常に低くなります。

また、ブランド・エクスペリエンスのため、業界のため、価値の観点から提供したいもののため、または詐欺の可能性があるため、それら何れか理由で、正確性が優先される場合もあります。この場合、企業はその人物に関連したより検証可能なデータを求めています。企業は、新しい顧客が実際にその顧客であることについてより高いレベルで保証することが重要であると定義しています。

@row
## Conclusion

Digital identity, as we indicated at the beginning, is a big topic. We’ve touched on the constituencies IAM serves, the technologies involved, governance, analytics, privileged accounts, and identity proofing. Each of those topics can (and hopefully will, in future versions of the IDPro Body of Knowledge) fill out an entire chapter by itself.

The article offered the IAM practitioner a chance to understand some of the major considerations that will impact their systems and services; readers need to consider their own local context and adapt the rough definitions offered here to fit their own unique organization. A future article will dive into the concept of run-time technologies.

@column
## 結論

冒頭で示したように、デジタル・アイデンティティは大きなトピックです。私たちは、IAMがサービスを提供する対象者、関連する技術、ガバナンス、分析、特権アカウントおよび身元確認について触れました。これらのトピックはそれぞれ、それだけで1つの章を構成することができます（そして願わくば、IDPro Body of Knowledgeの将来のバージョンではそうなることを期待しています）。

この記事は、IAMの実務者に、システムやサービスに影響を与える主な検討事項を理解する機会を提供しました。読者はそれぞれの状況を考慮し、ここで提供された大まかな定義をそれぞれの組織に適したものへと変える必要があります。今後の記事では、ランタイム・テクノロジーの概念について掘り下げていく予定です。

@row
## Author Bios

Ian Glazer

<!-- ![A person with a beard Description automatically generated with medium confidence](/assets/images/idpro_bok/iglazer.jpg) -->Ian Glazer is the Vice President for Identity Product Management at Salesforce. His responsibilities include leading the product management team, product strategy, and identity standards work. Prior to that, he was a research vice president and agenda manager on the Identity and Privacy Strategies team at Gartner, where he oversaw the team’s research. He is the founder and president of IDPro, the professional organization for digital identity management. He was also a founding member of the Management Council and Board of Directors for the US Identity Ecosystem Steering Group (IDESG). During his decade-plus time in the identity industry, he has co-authored a patent on federated user provisioning, co-authored the Service Provisioning Markup Language (SPML) Version 2 specification, contributed to the System for Cross-Domain Identity Management (SCIM) Version 2 specification, and is a noted blogger, speaker, and photographer of his socks.

Espen Bago

<!-- ![Profile photo for Espen Bago](/assets/images/idpro_bok/ebago.jpg) -->Espen Bago realized in 2002 that as system administrator, he’d been working in identity already for a while and decided from there to fully explore what this Identity thing was all about. He’s been an independent Identity Advisor and coordinator to large enterprises for the last few years, but in 2021 became Identity Manager for the Norwegian Labour and Welfare Administration. As such, his goal is to make certain that identities – and the real persons this represents – are not forgotten when governments inevitably go all-in digital. He’s also a founding member of IDPro and a member of the IDPro Body of Knowledge Committee and the IDPro Certification Committee.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2021-06-30 | Editorial updates; addition of a Terminology section; update to B2E section |

[^1]: An organization does not always need to know "who" a person is to any level of specificity. They just need to know things like "is this the same person each time" or "is this account authorized to perform this action."

[^2]: AICPA, “Segregation of Duties,” accessed on 11 January 2020, [https://www.aicpa.org/interestareas/informationtechnology/resources/value-strategy-through-segregation-of-duties.html](https://www.aicpa.org/interestareas/informationtechnology/resources/value-strategy-through-segregation-of-duties.html)

[^3]: United States. 2002. _Sarbanes-Oxley Act of 2002,_ \[Washington, D.C.\]: \[U.S. G.P.O.\], [https://www.govinfo.gov/content/pkg/PLAW-107publ204/pdf/PLAW-107publ204.pdf](https://www.govinfo.gov/content/pkg/PLAW-107publ204/pdf/PLAW-107publ204.pdf).

[^4]: _EU General Data Protection Regulation (GDPR):_ Regulation (EU) 2016/679 of the European Parliament and of the Council of 27 April 2016 on the protection of natural persons with regard to the processing of personal data and on the free movement of such data, and repealing Directive 95/46/EC (General Data Protection Regulation), OJ 2016 L 119/1, [https://ec.europa.eu/info/law/law-topic/data-protection/data-protection-eu\_en](https://ec.europa.eu/info/law/law-topic/data-protection/data-protection-eu_en).
