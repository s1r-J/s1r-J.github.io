---
layout: columns
title: Identifiers and Usernames
permalink: /docs/oidc_oauth/idpro_bok/16
date: 2024-09-09
date: 2024-12-15
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "ユーザー名", "識別子"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/16/](https://bok.idpro.org/article/id/16/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

An identifier is the way an identity management system or other entity refers to a digital identity. The identifier used by the system, however, likely differs from the identifier used directly by the user and will definitely differ from identifiers in another domain. This article reviews the concept of identifiers as they relate primarily to people, both from a user’s perspective and a system’s perspective, and their impact on the systems that use them.

Keywords: Digital Identity, Usernames, Identifiers

@column
## 概要

識別子は、アイデンティティ管理システムまたはその他エンティティがデジタルアイデンティティを参照する方法です。しかし、システムによって利用される識別子は、ユーザーによって直接利用される識別子と異なる可能性が高く、他の領域の識別子とは確実に異なります。この記事は、ユーザーの視点とシステムの視点の両方から、主に人と関係する識別子の概念と、識別子を利用するシステムに与える影響についてレビューします。

Keywords: デジタルアイデンティティ, ユーザー名, 識別子

@row
By Ian Glazer

© 2020 Ian Glazer and IDPro

@row
## Introduction

@column
## イントロダクション

@row
### What are identifiers and usernames?

In the physical world, we use a variety of ways to identify a person or a thing. From serial numbers to mailing addresses to license plates to nicknames, humans select a specific thing from a collection of similar things via an identifier. In the online world, this behavior is no different. Computer systems and people who work with them use identifiers to distinguish between similar items. More formally, and in the context of identity management, we can think of an identifier as the way an identity management system refers to a digital identity.

However, the person associated with that digital identity may not use the same identifier that the system uses. In fact, it is highly likely that they do not. Likely the person uses a human-friendly identifier. For the sake of differentiation, let’s call the way a person in control of a digital identity identifies themselves to a system a username.

@column
### 識別子とユーザー名とは何か？

物理的な世界では、私たちは人や物を識別するために様々な方法を用いています。シリアル番号、住所、ナンバープレート、ニックネームなど、人間は識別子によって類似したものの集まりの中から特定のものを選び出します。ネットの世界でも、この動作は変わりません。コンピュータシステムとそれを扱う人々は、識別子を使用して類似のものを区別しています。より正式には、アイデンティティ管理のコンテキストでは、アイデンティティ管理システムがデジタルアイデンティティを参照する方法として識別子を考えることができます。

しかし、そのデジタルアイデンティティに関連する人物は、システムが使用するのと同じ識別子を使用しないかもしれません。実際、そうでない可能性が高いです。その人物は、人間に適した識別子を使用している可能性が高いです。区別するために、デジタルアイデンティティを管理する人がシステムに対して自分自身を識別する方法をユーザー名と呼ぶことにしましょう。

@row
### Why consider identifiers and usernames?

How systems refer to digital identities and how people refer to their digital identity in a system are crucially important. Identifiers and usernames are one of the most commonly used components of a digital identity management system. They have implications for usability, security, customer satisfaction, and system operations, and enable (or prevent) cross-system correlation and user account management. They have applicability in business to employee (B2E), business to business (B2B), business to customer (B2C), and business to business to customer (B2B2C) use cases.

Failing to consider identifiers, and especially usernames can have direct, negative impacts on the projects and systems you are working on.

@column
### なぜ識別子とユーザー名を考慮するのか？

システムがデジタルアイデンティティをどのように参照するのか、および人々がシステム内で自分のデジタルアイデンティティをどのように参照するのかは、非常に重要です。識別子およびユーザー名は、デジタルアイデンティティ管理システムで最も一般的に使用されるコンポーネントの1つです。これらはユーザビリティ、セキュリティ、顧客満足度およびシステム運用に影響を与え、システム間の相関とユーザーアカウント管理を可能にします（または阻害します）。B2E（Business to Employee）、B2B（Business to Business）、B2C（Business to Customer）、B2B2C（Business to Business to Customer）のユースケースで適用できます。

識別子、特にユーザー名への考慮を怠ると、取り組んでいるプロジェクトやシステムに直接、悪影響を及ぼす可能性があります。

@row
### Types of Identifiers

Identifiers come in two varieties: internal and external. Internal identifiers are the means by which a system refers to a digital identity. Formats of internal identifiers can vary greatly. One common format of internal identifiers is a universal unique identifier (UUID.) Specified in the IETF RFC 4122, UUIDs come in 4 variants or versions. [^1] Many systems use UUID version 4 (often referred to as UUID4), which are randomly generated identifiers. An example of a UUID4 is: d5372288-697b-42bf-928a-562aca0deeaf.

But not all internal identifiers are UUIDs. Systems can use other means of uniquely identifying a specific thing from a collection of similar things. Examples include identifiers that have specific meaning to the system but are meaningless outside of the system, such as the following identifier, “005o0000000s4Hu.”

The second variety of identifier is an external identifier. An external identifier is the means by which a person in control of a digital identity refers to that identity when interacting with a system. These include but are not limited to a telephone number, email address, nickname, or handle.

In some cases a system identifier can be used by both internal and external purposes. Since email addresses must be unique within an organization i.e. a company, or domain i.e. college or physicians, the member’s ‘net id’ i.e. first part of their email address, will be used within corporate systems as a user’s identifier. A net-id could be comprised of first initial, second initial, last name and a number that ensures uniqueness.

@column
### 識別子の種類

識別子には2つの種類があります：内部と外部です。内部識別子は、システムがデジタルアイデンティティを参照する手段です。内部識別子の形式は大きく異なる場合があります。内部識別子の一般的な形式の1つは、Universal Unique Identifier（UUID）です。IETF RFC 4122で指定されているUUIDには、4つのバリアントまたはバージョンがあります。 [^1] 多くのシステムは、ランダムに生成された識別子であるUUIDバージョン4（UUID4と呼ばれることが多い）を使用します。UUID4の例はd5372288-697b-42bf-928a-562aca0deeafです。

しかし、すべての内部識別子がUUIDというわけではありません。システムは、類似したものの集まりから特定のものを一意に識別する他の手段を使用できます。例えば、「005o0000000s4Hu」のような、システムにとっては特定の意味を持つが、システムの外では意味のない識別子が含まれます。

2つ目の識別子は、外部識別子です。外部識別子は、デジタルアイデンティティを制御する人物がシステムと対話するときにそのアイデンティティを参照する手段です。これらには、電話番号、Eメールアドレス、ニックネーム、またはハンドルネームが含まれますが、これらに限定されません。

場合によっては、システムアイデンティティを内部目的と外部目的の両方で使用できます。Eメールアドレスは組織内、つまり企業内、または大学や医師などのドメイン内で一意でなければならないため、メンバーの「ネットID」、つまりEメールアドレスの最初の部分は、企業システム内でユーザーの識別子として使用されます。ネットIDは、最初のイニシャル、2番目のイニシャル、姓および一意性を保証する番号で構成できます。

@row
### Terminology

*   Internal identifier: the way an identity management system refers to a digital identity
    
*   External identifier: the means by which a person in control of a digital identity refers to that identity when interacting with a system
    
*   Username: a common term used for an external identifier
    

@column
### 用語解説

*   内部識別子：アイデンティティ管理システムがデジタルアイデンティティを参照する方法
    
*   外部識別子：デジタルアイデンティティを管理する人がシステムと対話する際にそのアイデンティティを参照する手段
    
*   ユーザー名：外部識別子に使用される一般的な用語
    

@row
## Aspects of Usernames

When considering what the format of usernames should be, an identity practitioner must consider the five guiding principles of usernames. The practitioner should consider username format in greenfield situations as well when new B2C or B2B2C services are being created, at the very least. Often, especially in B2B scenarios, usernames have formats established in previous generations of systems, and those formats take on an almost mythic quality. It is not reasonable to simply change username formats, and needless to say, changing username formats, especially in an enterprise B2B setting, is not an undertaking one should take lightly.

Cloud applications are a potential area of username confusion. For a multitenant application, usernames should be common, i.e., the username for a digital identity in one application is the same as that used in another application. However, in some cases a user sets up an account in a SaaS application and selects another username. If this application is subsequently interfaced to the identity management environment a transformation mechanism will be required. API gateways or identity provider services maintaining multiple usernames are options.

The five guiding principles identity practitioners should consider are that usernames:

*   [_Are not a secret_](#secret)
    
*   [_Must be classified as public data_](#public)
    
*   [_Must be memorable_](#memorable)
    
*   [_Must be unique_](#unique)
    
*   [_Must be recoverable_](#recoverable)
    

@column
## ユーザー名の側面

ユーザー名の形式がどうあるべきかを検討するとき、アイデンティティ実務者はユーザー名の5つの基本原則を考慮する必要があります。実務者は、少なくとも、新しいB2CまたはB2B2Cサービスが作成されている場合と同様に、未開拓の状況でユーザー名の形式を考慮するべきです。多くの場合、特にB2Bシナリオでは、ユーザー名には前世代のシステムで確立された形式があり、それらの形式はほとんど神話的な品質を帯びています。ユーザー名の形式を単純に変更することは合理的ではありません。言うまでもなく、ユーザー名の形式を変更することは、特に企業のB2B設定では軽々しくおこなうべきではありません。

クラウドアプリケーションは、ユーザー名が混乱する可能性のある領域です。マルチテナントのアプリケーションでは、ユーザー名は共通であるべきで、つまり、あるアプリケーションのデジタルアイデンティティのユーザー名は、別のアプリケーションで使用されるものと同じであるべきです。しかし、あるユーザーがSaaSアプリケーションでアカウントを設定し、別のユーザー名を選択する場合があります。このアプリケーションをその後アイデンティティ管理環境と整合させる場合、変換メカニズムが必要となります。APIゲートウェイや、複数のユーザ名を管理するアイデンティティプロバイダーサービスが選択肢となります。

アイデンティティ実務者が考慮すべき5つの指針となる原則は、次のようなユーザー名です：

*   [_秘密ではない_](#秘密)
    
*   [_公開データとして分類しなければならない_](#公開)
    
*   [_記憶可能でなければならない_](#記憶可能)
    
*   [_ユニークでなければならない_](#ユニーク)
    
*   [_リカバリ可能でなければならない_](#リカバリ可能)
    

@row
### Secret

There is an instructive lesson in the United States’ Social Security Number (SSN) as an anti-pattern for usernames. [^2]

SSN was meant as an internal identifier. Originally it was something the Social Security Administration would use to tie a human to their earned wages and eventually to their entitlements; it was something that they would use for their business processes. They shared this internal identifier with people and their employers to make business processes run. However, the use of this internal identifier grew. Businesses began to use SSN as a way for people to identify themselves to the business; in essence, business turned this internal identifier into a username. This secondary use was based on the idea that only the person would know their SSN and thus, because it was secret, the holder of the SSN would be assumed to be the correct person. And this is where things went wrong.

The need for this specific secret permeated so many of our business processes throughout our economy. This need has created a massive amplifier for damage when data brokers and others have breaches.

The lesson of SSN is that usernames cannot be secrets. If you share an internal identifier with a party outside of your organization, you have turned that internal identifier into public information, and thus it cannot be a secret.

If you have a username or an internal identifier that has to be treated like a secret, then you do have an authentication mechanism on your hands, not a username. And this means that it needs to be treated akin to a password.

As a pointer to an advanced topic for a later date, consider this- biometrics, broadly speaking, cannot be secrets. A person cannot keep their fingerprints, facial geometry, or irises secret. Because of this, a system or process can use biometrics as external identifiers. But because they are “just” identifiers, some degree of authentication is required to ensure the person actually intends to present their biometric. This degree of uncertainty is why liveness detection and attention detection are so crucial. For example, it is insufficient to accept a fingerprint biometric without also checking that the finger is real, has blood pumping through it, and [_isn’t a fake made of gelatin_](https://www.theregister.co.uk/2002/05/16/gummi_bears_defeat_fingerprint_sensors/) . [^3]

@column
### 秘密

ユーザー名のアンチパターンとして、米国の社会保障番号（SSN）が有益な教訓となります。 [^2]

SSNは、内部識別子としての意味を持っています。もともとは、社会保障庁がある人とその人が稼いだ賃金、ひいては受給資格を結びつけるために使うものでした；社会保障庁がその業務処理に使うものだったのです。社会保障庁は、この内部識別子を人々や雇用主と共有し、ビジネスプロセスを回していました。しかし、この内部識別子の利用が拡大しました。企業はSSNを人々が企業に対して自身を識別するための方法として使い始めました；要するに、企業はこの内部識別子をユーザー名に変えたのです。この二次利用は、SSNは本人しか知らないので、秘密であることから、SSNの持ち主が正しい人物であると想定される、という考えに基づいていました。そして、ここからが問題でした。

この特定の秘密の必要性は、経済全体を通して私たちのビジネスプロセスの非常に多くの部分に浸透しています。この必要性により、データブローカーなどが情報漏洩を起こしたときの損害の巨大な増幅器を作り出しました。

SSNの教訓は、ユーザー名は秘密ではありえないということです。内部識別子を組織外の関係者と共有する場合、その内部識別子を公開情報に変えてしまうことになるので、秘密ではありえません。

もし、ユーザー名や内部識別子を秘密のように扱わなければならないのであれば、ユーザー名ではなく、認証機構を手にしたことになります。つまり、パスワードと同じように扱う必要があるのです。

後日の高度なトピックのための助言として、次のことを考えてみてください - 広義には、バイオメトリクスは秘密にすることはできません。人は、自分の指紋、顔の形状、または虹彩を秘密にすることはできません。このため、システムやプロセスでは、バイオメトリクスを外部識別子として使用することができます。しかし、バイオメトリクスは「単なる」識別子であるため、人が実際にバイオメトリクスを提示する意図があることを確認するために、ある程度の認証が必要です。このような不確実性があるからこそ、活性度検出や注目度検出が非常に重要なのです。例えば、指が本物であること、血液が流れていること、 [_ゼラチンでできた偽物でない_](https://www.theregister.co.uk/2002/05/16/gummi_bears_defeat_fingerprint_sensors/) ことを確認せずに指紋生体認証をおこなうことは不十分です。 [^3]

@row
### Public

It is not enough to make sure that usernames are not secrets. Identity practitioners must also classify usernames as public in one’s data classification scheme. This action applies to employees, partners, and customers alike.

Classifying usernames as public does not mean attributes related to the individual are public. Such attributes cannot reasonably or safely be used in a username. Consider a simple four-level data classification system:

*   Public: this data can be shared across organizational boundaries freely and with a low level of concern.
    
*   Restricted: this data is essential to business process and likely cannot leave organizational boundaries. Only data subjects, employees, and contractors can have access to this data.
    
*   Confidential: this data is crucial to business operations. Significant harm may occur if this data transits organizational boundaries.
    
*   Secret: this data is extremely organizationally sensitive. Only a small select group of people and systems can have access.
    

In an ideal world, an airline or hotel loyalty number (another kind of identifier) is likely classified “Restricted.” Usernames must be classified as “Public.” Airline or hotel loyalty identifiers demonstrate the problem of an identifier that is “public” but contains attributes that have value.

In addition, classifying usernames as public reinforces the idea that identifiers cannot be secrets.

As a clarification, the recommendation is that the username should be classified as public data, in a data classification system. That does not mean that usernames should be publicized (e.g., listed on a public site) – that is a self-inflicted enumeration attack.

@column
### 公開

ユーザー名が秘密ではないことを確認するだけでは不十分です。アイデンティティ実務者は、データ分類スキームでユーザー名を公開として分類する必要もあります。このアクションは、従業員、パートナーおよび顧客に同様に適用されます。

ユーザー名を公開と分類しても、個人に関する属性が公開されるわけではありません。そのような属性は、ユーザー名に合理的にまたは安全に使用することはできません。シンプルな4つのレベルのデータ分類システムを考えてみましょう：

*   公開：このデータは、組織の境界を越えて自由に、低レベルの懸念で共有できます。
    
*   制限付き：このデータはビジネスプロセスに不可欠であり、おそらく組織の境界を越えることはできません。データ主体、従業員および受託業者だけがこのデータにアクセスできます。
    
*   社外秘：このデータは事業運営にとって重要です。このデータが組織の境界を通過すると、重大な損害が発生する可能性があります。
    
*   秘密：このデータは組織的に非常に繊細です。少数の選ばれた人やシステムのグループのみがアクセスできます。
    

理想的な世界では、航空会社またはホテルのロイヤルティ番号（別の種類の識別子）は「制限付き」に分類される可能性があります。ユーザー名は「公開」として分類しなくてはなりません。航空会社またはホテルのロイヤルティ識別子は、「公開」であるにもかかわらず、価値のある属性を含む識別子であるという問題を示しています。

さらに、ユーザー名を公開として分類すると、識別子を秘密にすることはできない、という考えが強まります。

明確化のために、データ分類システムでユーザー名を公開データとして分類することをお勧めします。これは、ユーザー名を公開する（例えば、公開サイトにリスト化する）べきだという意味ではありません。それは、自ら招いた列挙攻撃です。

@row
### Memorable

Part of the canon of US literature is Herman Melville’s Moby Dick. And its first sentence reads “Call me Ishmael.” Ishmael, the username, is not the most important part of that sentence – the “call me” part is. The power to name something is the power to control it. And by naming himself Ishmael takes control over himself, away from the Reader and away from the author.

In support of self-determination, people have to give themselves names, and in the digital world, this is crucially important. Usernames need to be self-generated in B2C and B2B2C settings, which is to say the person should have the power to create their preferred username. It is important to also consider self-generated usernames in B2B and B2E settings as well.

Many enterprises have a standard username format and they bring that preference to B2C and B2B use cases. A classic username format is First Initial, Last Name. For example, Sally Smith would get a username of “ssmith” and if that wasn’t unique a random number would be added. This habit-based username format, although reasonably effective, doesn’t support a desire for self-determination which is so crucial in B2C use cases.

Failure to support memorable usernames means increased account recovery calls, more on-screen help, and more customer support needs. And it also leads to duplicate identifiers because people often forget the identifier they used to register.

When building a username scheme, one needs to provide choice to the user. If asked for email as username and then on the next screen the user says, ‘do not use email to talk to me’, then there is significant cognitive dissonance. In order to provide choice, consider supporting multiple username schemes such as email addresses and user-created nicknames. Supporting multiple schemes adds a level of complexity, but the user empowerment that brings with it engenders self-determination and customer satisfaction.

@column
### 記憶可能

アメリカ文学の代表作にHerman Melvilleの『Moby Dick』という作品があります。その最初の文には、「Call me Ishmael.」とあります。Ishmaelというユーザー名はこの文で最も重要な部分ではなく、それは「call me」の部分です。名前をつける力は、それを制御する力です。そして、Ishmaelは自分自身を名付けることによって、読者から、そして作者から、自分自身を制御することができるのです。

自己決定を支援するために、人々は自分自身に名前を付ける必要があり、デジタル世界では、これは非常に重要なことです。B2CやB2B2Cでは、ユーザー名は自分で作成する必要があります。B2BやB2Eにおいても、ユーザー名を自分で作成することは重要です。

多くの企業には標準的なユーザー名形式があり、B2CやB2Bのユースケースにもその好みが適用されています。古典的なユーザ名形式は、ファーストネームのイニシャルとラストネームです。例えば、Sally Smithは「ssmith」というユーザー名を使い、それがユニークでない場合はランダムな数字が追加されます。この習慣に基づいたユーザー名形式は、それなりに効果的ではありますが、B2Cのユースケースで非常に重要な自己決定欲求をサポートするものではありません。

覚えやすいユーザー名に対応していない場合、アカウント回復のための電話や画面上のヘルプが増え、カスタマーサポートのニーズが高まります。また、登録時に使用した識別子を忘れてしまうことが多いため、識別子の重複にもつながります。

ユーザー名スキームを作るとき、ユーザーに選択肢を提供する必要がある。もし、ユーザー名としてEメールを要求され、次の画面でユーザーが「私と話すのにEメールを使わないでください」と言った場合、重大な認知的不協和が発生します。選択肢を提供するために、Eメールアドレスやユーザーが作成したニックネームなど、複数のユーザー名スキームをサポートすることを検討してください。複数の方式をサポートすることで、複雑さが増しますが、それによってもたらされるユーザーへの権限委譲は、自己決定と顧客満足を生み出します。

@row
### Unique

Usernames need to be unique. Internal identifiers need to be unique. Neither statement should be controversial, but there is nuance here.

It is not enough to say a username must be unique; one must consider the scope of uniqueness. Is the username unique:

*   at the individual service level?
    
*   at the tenant level (if you are multi-tenant)?
    
*   within a namespace with a service or set of services?
    
*   globally across all of your services?
    
*   universally?
    

Is there a clear picture of the scope being designed for? Even if there is, that picture may change; practitioners need to consider if the future might include merging internal systems or have to support various merger and acquisition activities in the future.

Also, uniqueness has implications depending on the type of identifier. Usernames and internal identifiers do not have to have the same scope of uniqueness. For example, while an internal identifier needs to be globally unique, a username might be unique only in a subset of systems in the enterprise. Internal identifiers have to be unique at the service-scope, e.g., unique in a specific enterprise service. To mitigate potential data subject reidentification, then those identifiers ought to be globally-scoped unique. Meanwhile, a person might use their email address to log into multiple systems - a service-level scoped unique username.

In addition, do not, in the same system, make the username and the internal identifier the same value. In some regards, this was one of the mistakes the US made with the Social Security Number. [^4] Practitioners should not make them the same value if only because changing either later can be enormously challenging. Furthermore, a common username scheme of choice is an email address, and these can change over a person’s life based on life events such as marriage and divorce. Accommodating such changes to the username in a scheme where the username and internal identifier are the same requires that all systems with the “old” username/internal identifier need to be aware of the change and updated; in a complex environment, that task may be nearly impossible.

A final consideration is username reuse. Yahoo email allows people to use email addresses that were once used by someone else. Phone numbers are regularly reused. In this case, the username may still be unique but the person in possession of that username has changed. This transitional period is a difficult situation to be in if for no other reason than the new possessor of the email or phone looks like an attacker in many cases.

@column
### ユニーク

ユーザー名は一意である必要があります。内部識別子は一意である必要があります。どちらの主張も議論の余地がないはずですが、ここにはニュアンスがあります。

ユーザー名が一意でなければならないと言うだけでは不十分です。一意性の範囲を考慮する必要があります。以下の範囲で、ユーザー名は一意ですか？：

*   個々のサービスレベルで？
    
*   テナントレベルで（マルチテナントの場合）？
    
*   1つのサービスまたは複数のサービスの名前空間内で？
    
*   あなたの全サービスにおいて？
    
*   世界で？
    

スコープが設計されているという明確なイメージはありますか？たとえあったとしても、そのイメージは変わるかもしれません：実務者は、将来的に内部システムの統合を含む可能性があるかどうか、または将来的になさまざまな合併および買収活動をサポートする必要があるかどうかを検討する必要があります。

また、一意性は識別子の種類に応じて意味を持ちます。ユーザー名と内部識別子は、一意性の範囲が同じである必要はありません。たとえば、内部識別子はグローバルに一意である必要がありますが、ユーザー名は企業内のシステムのサブセットでのみ一意である場合があります。内部識別子は、サービススコープ内で一意である必要があります、例えば特定のエンタープライズサービスで一意であるなど。データ主体の再識別の可能性を軽減するために、これらの識別子はグローバルスコープで一意である必要があります。一方、ユーザーは自分のEメールアドレスを使用して複数のシステムにログインすることがあり、これはサービスレベルをスコープとする一意のユーザー名です。

また、同じシステム内で、ユーザ名と内部識別子を同じ値にしないようにします。ある意味では、これは米国が社会保障番号で犯した過ちの一つです。 [^4] どちらかを後で変更することが非常に困難であるため、実務者はこれらを同じ値にすべきではありません。さらに、一般的なユーザー名スキームとして選ばれるのはEメールアドレスであり、これらは結婚や離婚などのライフイベントによって人生の中で変わる可能性があります。ユーザー名と内部識別子が同じスキームで、このようなユーザー名の変更に対応するには、「古い」ユーザー名と内部識別子を持つすべてのシステムが変更を認識し、更新する必要があります；複雑な環境では、この作業はほとんど不可能かもしれません。

最後に、ユーザー名の再利用について考えてみましょう。Yahoo Eメールでは、かつて他の人が使っていたEメールアドレスを使うことができます。電話番号も定期的に再利用されています。この場合、ユーザー名はまだ一意であっても、そのユーザー名を所持する人は変わっています。この過渡期は、Eメールや電話の新しい所持者が、多くの場合攻撃者に見えるという理由だけでも、難しい状況です。

@row
### Recoverable

Usernames need to be recoverable, which is to say, that there needs to be a way to get a person back to their digital identity. Recovery means re-attaching the person to the digital identity; it does not necessarily mean they will use the same username over again.

In this regard, recovery is more than just reminding the person of what email address they used to log in. Consider telling a person that the email address they used was their old work email address that they cannot access. That leaves the person little recourse but to call the help desk… or move on to a new service.

Recovery is a re-association and to do this safely, it often requires re-proofing the individual is who they claim to be. Especially in B2C scenarios, such a re-proofing process requires considerable thought as it has significant security and customer satisfaction implications.

@column
### リカバリ可能

ユーザー名は回復可能である必要があり、つまり、その人をデジタルアイデンティティに戻す方法が必要ということです。リカバリとは、その人をデジタルアイデンティティに再び結びつけることです；必ずしも同じユーザー名を再び使用することを意味するわけではありません。

この点で、リカバリは、ログインに使用したEメールアドレスを思い出させるだけではありません。その人が使用したEメールアドレスは、アクセスできない昔の職場のEメールアドレスであることを伝えることを考えてみてください。そうすると、その人はヘルプデスクに電話するか、新しいサービスに移行するしかありません。

リカバリは再関連付けであり、これを安全におこなうには、多くの場合要求しているその個人が本人であることを再証明する必要があります。特にB2Cのシナリオでは、このような再確認のプロセスは、セキュリティと顧客満足度に大きな影響を与えるため、かなりの配慮が必要です。

@row
## Conclusions

Identifiers are necessary to an identity system, with internal and external identifiers serving different purposes. While the two types of identifiers can be the same, the IAM practitioner should consider this with caution.  External identifiers, also known as usernames, should consider these five guiding principles:

*   Usernames should not be considered a secret.
    
*   Usernames must be classified as public data.
    
*   Usernames must be memorable.
    
*   Usernames must be unique.
    
*   Usernames must be recoverable.
    

Each principle has implications for the identity practitioner to consider as they develop an identity management system. Constructing a username framework is part of the ‘identity orchestration’ task.

@column
## 結論

識別子はアイデンティティシステムにとって必要であり、内部識別子と外部識別子は異なる目的を果たします。2種類の識別子を同じにすることは可能ですが、IAM実務者はこれを慎重に考慮すべきです。ユーザー名としても知られる外部識別子は、以下の5つの指針を考慮すべきです：

*   ユーザー名は秘密と考えるべきではない。
    
*   ユーザー名は公開データとして分類しなければならない。
    
*   ユーザー名は記憶可能でなければならない。
    
*   ユーザー名はユニークでなければならない。
    
*   ユーザー名はリカバリ可能でなければならない。
    

各指針は、アイデンティティ実務者がアイデンティティ管理システムを開発する際に考慮すべき意味を持ちます。ユーザ名のフレームワークを構築することは、「アイデンティティオーケストレーション」タスクの一部です。

- - -

[^1]:  Leach, P., Mealling, M., and R. Salz, "A Universally Unique IDentifier (UUID) URN Namespace", RFC 4122, DOI 10.17487/RFC4122, July 2005, <https://www.rfc-editor.org/info/rfc4122>. 
    
[^2]:  Carolyn Pucket, “The Story of the Social Security Number, Social Security Bulletin, Vol. 69, No 2, 2009, [_https://www.ssa.gov/policy/docs/ssb/v69n2/v69n2p55.html_](https://www.ssa.gov/policy/docs/ssb/v69n2/v69n2p55.html) . 
    
[^3]:  John Leyden, “Gummi bears defeat finger print sensors,” The Register, 16 May 2002, [_https://www.theregister.co.uk/2002/05/16/gummi\_bears\_defeat\_fingerprint\_sensors/_](https://www.theregister.co.uk/2002/05/16/gummi_bears_defeat_fingerprint_sensors/) . 
    
[^4]:  Pucket, see _Expanding Uses of the SSN_ , [_https://www.ssa.gov/policy/docs/ssb/v69n2/v69n2p55.html_](https://www.ssa.gov/policy/docs/ssb/v69n2/v69n2p55.html) . 
