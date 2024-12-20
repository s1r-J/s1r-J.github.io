---
layout: columns
title: A Peek into the Future of Decentralized Identity (v2)
permalink: /docs/oidc_oauth/idpro_bok/51
date: 2024-09-09
modify_date: 2024-12-21
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "自己主権型アイデンティティ", "デジタルウォレット", "デジタルカード", "分散型アイデンティティ"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/51/](https://bok.idpro.org/article/id/51/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

As digital transformation sweeps across the globe, it has affected everyone – from citizens to employees, from corporations to governments. Digital identity is a foundational enabler for business processes in the digital economy. Decentralized identity is the next evolution of digital identity capabilities and brings with it an opportunity to streamline how people interact with other institutions, physical objects, and with one another. This paper considers the future world of decentralized identity and offers clarity around the benefits of decentralized identity, terminology, sample scenario, and a sample technical implementation, while also addressing some of the limitations of this model. This paper further grounds the reader in the current state of decentralized identity capabilities while outlining the evolution of identity practices from past to present.

Keywords: Self-sovereign identity, Digital wallet, Digital Card, Decentralized Identity

@column
## 概要

デジタルトランスフォーメーションが全世界に広がり、市民から従業員、企業から政府まで全てのひとに影響を与えています。デジタルアイデンティティは、デジタル経済におけるビジネスプロセスを可能にする基盤です。分散型アイデンティティはデジタルアイデンティティ能力の次の進化であり、人々が他の機関、物理的なオブジェクトやお互いにやり取りをおこなう方法を合理化する機会をもたらします。本書では、分散型アイデンティティの未来の世界について考察し、分散型アイデンティティの利点、用語、サンプルシナリオそしてサンプルの技術的実装について明確にし、いくつかのこのモデルの限界についても取り扱います。さらに、本稿は読者に対して、過去から現在までのアイデンティティプラクティスの進化について概略しながら、分散型アイデンティティ能力の現在の状況について根拠を提供します。

Keywords: 自己主権型アイデンティティ, デジタルウォレット, デジタルカード, 分散型アイデンティティ

@row
Leo Sorokin

© 2022 IDPro, Leo Sorokin

@row
## Introduction

Digital identity is rapidly gaining criticality in our world as organizations digitally transform. Identity plays a pivotal role in a digital transformation and can empower both governments and businesses to provide secure whilst restricted access to data for any stakeholder whether employee, partner, customer, or citizen. Digital identity is becoming a vital component of security in a world with data proliferation on a myriad of devices and a network perimeter that is ever-more challenging to define.

One active area under development in the identity space is the concept of _decentralized identity_. Decentralized identity is a fundamental shift from _account-based credentials_ toward _verifiable credentials_ and is a major philosophical as well as technical change in the way identity-related information is acquired and presented. The World Wide Web Consortium (W3C) is working on publishing standards around _Verifiable Credentials_ and _Decentralized Identifiers_.[^1],[^2] However, as with any technology standard, it must be broadly adopted by the community for it to be useful at scale.

Today, a person’s digital identity (and associated personal data) is strewn across many online services, with access to such services being primarily performed via a username and password. Such an account-based credential is usually provisioned directly by the service provider, or by a large and rather centralized identity provider (IdP), such as Google, Facebook, or Twitter with which a service provider application will federate. This account-based federated model, however, has some significant limitations: the IdP may stop offering its services to third-parties; the identity supported by this IdP may be compromised thus impacting every service provider application that uses that identity; the IdP may track an individual’s activities across multiple services; and an IdP may decommission the account being used for authentication. There are many challenges with the federated identity model, but going back to identity silos where each service provider provisions and manages its own set of credentials for its users, resulting in users having to manage dozens of such account-based credentials is not ideal either.

Decentralized identity strives to place the individual at the center of digital identity experiences by attempting to insert the individual at the center of identity data exchange. At its simplest, decentralized identity attempts to map physical wallets and the physical cards within them to a very similar concept in the digital world – a digital wallet with digital cards.

Today, there are many that are very excited about the potential of this model as well as many that are skeptical. Although decentralized identity and the concepts underpinning it attempt to solve the challenges we have had with digital identity over the past few decades, it is still too early to predict how individuals, governments, and corporations will approach it, and how each of these actors will be able to derive value from it.

@column
## 導入

デジタルアイデンティティは、組織のデジタルトランスフォーメーションとともに私たちの世界で急速に重要性を増しています。アイデンティティは、デジタルトランスフォーメーションにおいて重要な役割を果たし、政府と企業の両方に従業員、パートナー、顧客、市民など、あらゆる利害関係者にデータへのアクセスを制限しながら安全に提供できるようにします。デジタルアイデンティティは、無数のデバイス上にねずみ算式に増えるデータと今までにないほど定義することが難しいネットワーク境界を持つ世界において、セキュリティの重要なコンポーネントとなってきています。

アイデンティティ業界おにいて開発中のアクティブな領域の一つは、 __分散型アイデンティティ__ の概念です。分散型アイデンティティは、 __アカウントベースのクレデンシャル__ から __検証可能なクレデンシャル__ への根本的なシフトであり、アイデンティティに関連した情報の取得および提示方法の哲学的および技術的な大きな変化です。World Wide Web Consortium（W3C）は __検証可能なクレデンシャル__ および __分散型アイデンティティ__ に関連した標準仕様の公開に取り組んでいます。[^1],[^2] しかし、他の技術標準仕様と同じく、大規模に有用であるためにはコミュニティによって広く採用されなければなりません。

今日では、個人のデジタルアイデンティティ（および関連する個人データ）は多くのオンラインサービスに散らばっており、それらサービスへのアクセスには主にユーザー名とパスワードを使います。このようなアカウントベースクレデンシャルは、一般的にサービスプロバイダーから直接、または、サービスプロバイダーアプリケーションがフェデレーションをおこなったGoogleやFacebook、Twitterのような大規模で非常に中央集権化されたアイデンティティプロバイダー（IdP）によって、プロビジョニングされます。しかし、このアカウントベースのフェデレーティッドモデルはいくつかの重大な制限があります：IdPは第三者に対してそのサービスの提供を停止する可能性があります：このIdPがサポートするアイデンティティが侵害される可能性があり、つまりこのアイデンティティを利用するすべてのサービス提供者のアプリケーションに影響を受ける可能性があります；IdPは複数のサービスをまたいで個人のアクティビティを追跡するかもしれせん；IdPは認証に利用されているアカウントを廃止する可能性があります。フェデレーティッドアイデンティティモデルには多くの課題がありますが、各サービスプロバイダーがユーザに対してクレデンシャルをプロビジョニングして管理しているアイデンティティサイロに話を戻すと、ユーザーが多数のそのようなアカウントベースクレデンシャルを管理しなければならないことも理想的ではありません。

分散型アイデンティティは、データ交換の中心に個人を加えることで、デジタルアイデンティティエクスペリエンスの中心に個人を据えようとしています。最も単純には、分散型アイデンティティは物理的な財布と物理的なクレジットカードを、デジタル世界内の非常によく似た概念、デジタルカードを備えたデジタルウォレットにマッピングしようとしています。

今日、このモデルの可能性に非常に興奮している人も、懐疑的な人もたくさんいます。分散型アイデンティティとそれを支える概念は、過去数十年にわたってデジタルアイデンティティで私たちが抱えてきた課題を解決しようとしていますが、個人、政府および企業がそれにどのようにアプローチするか、これらの各アクターがそこからどのように価値を引き出すことができるかを予測するにはまだ時期尚早です。

@row
### Decentralized Identity Benefits

A decentralized identity system can be used to replace a traditional username and password during a typical _authentication_ sequence. This is perhaps the first use-case most will think about. However, authenticating in a passwordless manner is possible today even without any decentralized identity components. As such, the true value of decentralized identity can be more easily understood during _authorization_. During authorization, the service provider may mitigate risk by requiring the individual to present one or more digitally signed attestations commensurate with the level of risk that specific transaction entails and the level of value being obtained. This capability could be leveraged to increase trust between the parties, improve the user experience for the individual, while at the same time lowering costs for the business.

The purpose of decentralized identity is to empower individuals to own and control their digital identity and how their identity data is accessed and used. The premise behind decentralized identity decouples it from the notion of a username and password or the traditional account-based model. A digital identity is not yet another username and password-based account that is provisioned and maintained by a third party. With a decentralized identity model, the individual can be both authenticated and authorized to perform a transaction with one service, and then present the same identity information to another entity with which the individual might prefer to interact. In addition, the individual can become their own identity provider, which is more difficult to accomplish with the centralized or federated models we have today.

Decentralized digital identity and the _personal_ _data_ associated with it should enable the individual to have more control over how that data is accessed and used. As a byproduct of this philosophy, personal data should be presented by the individual to service providers on an as-needed basis, with specific terms of use. This principle is fundamental to decentralized identity. In a decentralized identity ecosystem, there is no one single central authority; value is exchanged in a more peer-to-peer manner. Since the individual controls and owns their personal data, they are the ones to enable other parties to access it by granting them specific permissions. This is in stark contrast to today’s reality where personal data may be shared and stored by third parties outside the individual’s control with the individual having no means of specifying the terms of use under which the identity-related information is shared.

In a decentralized identity environment, it may be possible to possess a digital card for a drivers’ license, credit card, or even a passport, and have them available on a mobile device. In another scenario, it may help when traveling abroad while having to visit a doctor. Today, it would be very cumbersome and not practical to share medical history and medications with a doctor, other than through a simple verbal explanation. However, with a healthy decentralized identity ecosystem of issuers and verifiers, it would be possible to share important medical information in a digital privacy-preserving manner, thus enabling the doctor to make a better medical decision and provide the patient with a much better service. An additional example is a mortgage lender that may need the homeowner to provide proof of active property insurance. To that end, the homeowner can present the property insurance information to the mortgage lender and the lender can periodically verify the current status of the insurance policy on its own without unnecessarily burdening the homeowner with having to constantly present this documentation to the lender for verification on a recurring schedule. While centralized or federated identity might also support these use cases, decentralized identity might be better suited for them.

Decentralized identity may enable new business models and value exchange. It may pave the path for fully digital-only experiences that remove the requirement for individuals to present themselves in-person to perform high value transactions. Decentralized identity may also enable a better in-person user experience in a variety of situations without requiring a person to carry a physical wallet at all. There are also potential benefits for businesses to streamline how they might verify and build trust with their customers. There is definite potential here, but only time and the market will tell if the great expectations for decentralized identity will be fully realized in practice over the long term.

@column
### 分散型アイデンティティの利点

分散型アイデンティティシステムを使用することで、典型的な __認証__ シーケンス中における従来のユーザー名とパスワードを置き換えることができます。おそらく、これはほとんどの人が考える最初のユースケースです。しかし、パスワードレスな方法による認証は、今日では分散型アイデンティティコンポーネントがなくても可能です。そのため、分散型アイデンティティの真の価値は、 __認可__ においてより簡単に理解できます。認可処理時、サービスプロバイダーはリスクを軽減するために、個人に対して特定のトランザクションに伴うリスクのレベルと得られる価値のレベルに見合った1つ以上のデジタル署名された証明書の提示を要求します。この機能を活用して当事者間の信頼を高め、個人のユーザーエクスペリエンスを向上させると同時に、ビジネスのコストを削減できます。

分散型アイデンティティの目的は、個人が自身のデジタルアイデンティティを所有、管理し、どのようにアイデンティティデータへのアクセスおよび使用するかを管理できるようにすることです。分散型アイデンティティの背後にある前提は、ユーザー名とパスワード、または従来のアカウントベースのモデルの概念から切り離されています。デジタルアイデンティティは、サードパーティによってプロビジョニングおよびメンテナンスされる別のユーザー名とパスワードベースのアカウントではありません。分散型アイデンティティモデルを使用すると、個人は1つのサービスでトランザクションを実行するための認証と認可の両方を受けることができ、その後、個人がやり取りをおこないたい別のエンティティに同じアイデンティティ情報を提示できます。さらに、個人は自身のアイデンティティプロバイダーになることができ、これは現在の中央集権またはフェデレーションのモデルでは実現がより困難です。

分散されたデジタルアイデンティティとそれに関連付けられた __個人データ__ により、個人はそのデータへのアクセス方法と使用方法をさらにに制御できるようになります。この哲学の副産物として、個人データは必要に応じて個人がサービスプロバイダーに特定の使用条件とともに提示する必要があります。この原則は、分散型アイデンティティの基本です。分散型アイデンティティのエコシステムでは、単一の中央権威機関は存在しません；値は、よりピアツーピアな方法で交換されます。個人は自分の個人データを管理および所有しているため、特定の権限を付与することで、他の関係者が個人データにアクセスできるようにします。これは、個人データが個人の制御の及ばない第三者によって共有および保存される可能性があり、個人はアイデンティティに関連した情報が共有される利用条件を指定する手段を有していない今日の現実とはまったく対照的です。

分散型アイデンティティ環境では、運転免許証やクレジットカード、あるいはパスポートなどのデジタルカードを所持し、モバイルデバイスで利用することができるかもしれません。別のシナリオでは、海外旅行で医者にかかるときにも役立つかもしれません。現在、医師と病歴や薬を共有するためには、簡単な口頭での説明以外は非常に面倒で現実的ではありません。しかし、IssuerとVerifierの健全な分散型アイデンティティエコシステムがあれば、重要な医療情報をデジタルプライバシーを保護した形で共有することが可能になり、医師はより良い医療判断を下し、患者にはより良いサービスを提供できるようになるでしょう。また、住宅ローンの貸し手は、住宅所有者に有効な損害保険の証明書を提出してもらう必要があります。分散型アイデンティティエコシステムがあれば、住宅所有者は住宅ローン貸し手に損害保険情報を提示することができ、貸し手がおこなう検証のためにこの証明書を貸し手に提示するという住宅所有者の不必要な負担なしに保険条件の現在の状況を定期的に検証することができます。中央集権型またはフェデレーション型のアイデンティティもこれらのユースケースをサポートする可能性がありますが、分散型アイデンティティの方が適しているでしょう。

分散型アイデンティティは、新しいビジネスモデルや価値交換を可能にするかもしれません。高価値の取引をおこなうために個人が直接姿を現す必要性をなくし、完全にデジタルだけの体験への道を開く可能性があります。また、分散型アイデンティティは物理的な財布を持ち歩くことなく、さまざまな状況においてより良い対面でのユーザー体験を可能にするかもしれません。また、企業にとっても、顧客との信頼関係を検証、構築する方法を効率化できる潜在的な利点があります。確かに可能性はありものの、分散型アイデンティティへの大きな期待が、長期にわたって実際に完全に実現されるかどうかは時間と市場のみが知ります。

@row
### Decentralized Identity Terminology

The following are the primary components involved in a decentralized identity experience. These definitions have been simplified to make it easier to understand the actors and how they interact:

*   _Self-sovereign identity_ is a term that describes a digital movement that is founded on the principle that an individual should own and control their identity without the intervening administrative authorities.
    
*   _Verifiable credentials_ are attestations that an issuer makes about a subject. Verifiable credentials are digitally signed by the issuer.
    
*   _Issuer_ is the entity that issues verifiable credentials about subjects to holders. Issuers are typically a government entity or corporation, but an issuer can also be a person or device.
    
*   _Holder_ is the entity that holds verifiable credentials. Holders are typically users but can also be organizations or devices.
    
*   _Verifier_ is the entity that verifies verifiable credentials so that it can provide services to a holder.
    
*   _Verifiable presentations_ are the packaging of verifiable credentials, self-issued attestations, or other such artifacts that are then presented to verifiers for verification. Verifiable presentations are digitally signed by the holder and can encapsulate all the information that a verifier is requesting in a single package. This is also the place where holders can describe the specific terms of use under which the presentation is performed.
    
*   _User agent_ or _digital agent_ is the software application that holders use (typically a mobile device app) that receives verifiable credentials from issuers, stores them, and presents verifiable credentials to verifiers for verification.
    
*   _Identity hub_ or _repository_ is the place where users can store their encrypted identity-related information. An identity hub can be anywhere – on the edge, on the cloud, or on your own server. Its purpose is to store personal data. Some implementations may allow other entities to access the identity hub of the user if the user specifically grants such access. You can think of an identity hub as the individual’s personal data store.
    
*   _Decentralized Identifier (DID)_ is an identifier that is created and anchored in a decentralized system such as a blockchain or ledger and can represent any entity in the ecosystem – an issuer, a holder, a verifier, and even an identity hub.
    
*   _Digital cards_ represent verifiable credentials that users collect over time and are stored as part of the user agent or the identity hub of the user. It’s somewhat simpler to refer to them as digital cards rather than verifiable credentials when speaking about them.
    
*   _Digital wallet_ represents a digital metaphor for a physical wallet and is generally represented by the combination of the user agent and the underlying capabilities of the computing device, such as secure storage and secure enclaves on a mobile phone. The digital wallet contains digital cards.
    
*   _dPKI_ is a decentralized public key infrastructure and is usually implemented via an immutable blockchain or ledger – a place where DIDs can be registered and looked up alongside the associated public keys of the DID and its metadata. dPKI can be described more generally as the _verifiable data registry_, as the dPKI is just one of many possible implementations for a verifiable data registry. While this paper refers to dPKI, the reader should be aware that a verifiable data registry need not necessarily be “decentralized”.
    
*   _Universal resolver_ is an identifier resolver that works with any decentralized identifier system through DID drivers. The purpose of a universal resolver is to return a DID document containing DID metadata when given a specific DID value. This capability is very useful because DIDs can be anchored on any number of disparate dPKI implementations.
    

The figure below highlights some of the terminology just outlined with the major actors and their relationships. It also represents the sample scenario we will cover later in this document.

@column
### 分散型アイデンティティの用語解説

以下は分散型アイデンティティに関する主な構成要素です。これらの定義は、アクターとそれらがどのように相互作用するかを理解しやすくするために簡略化されています：

*   __自己主権型アイデンティティ__ は、行政当局に介入されることなく、個人が自分のアイデンティティを所有し、管理すべきであるという原則に成り立つデジタルムーブメントを表す用語です。
    
*   __検証可能なクレデンシャル__ とは、Issuerが主体に関して作成する証明書です。検証可能なクレデンシャルは、Issuerによってデジタル署名されています。
    
*   __Issuer__ とは、 検証可能なクレデンシャルをHolderに発行するエンティティです。Issuerは通常、政府機関または企業ですが、個人またはデバイスであることもあります。
    
*   __Holder__ とは、検証可能なクレデンシャルを保持するエンティティです。Holderは通常、ユーザーですが、組織またはデバイスである場合もあります。
    
*   __Verifier__ とは、検証可能なクレデンシャルを検証するエンティティであり、Holderにサービスを提供します。
    
*   __検証可能なプレゼンテーション__ は、検証可能なクレデンシャル、自己発行アテステーションまたは検証のためにVerifierに提示されるその他の成果物をまとめたものです。検証可能なプレゼンテーションはHolderによってデジタル署名され、Verifierが要求しているすべての情報を1つのパッケージにカプセル化できます。また、これは提示が実行される特定の使用条件をHolderが記述できる機会です。
    
*   __ユーザーエージェント__ または __デジタルエージェント__ とはHolderが使用するソフトウェアアプリケーション（通常はモバイルデバイスアプリ）であり、Issuerから検証可能なクレデンシャルを受領し、保存し、検証のためにVerifierに検証可能なクレデンシャルを提示します。
    
*   __アイデンティティハブ__ または __リポジトリ__ とは、ユーザーが暗号化されたアイデンティティ関連情報を保存できる場所です。アイデンティティハブは、エッジ、クラウド、または独自のサーバーのどこにでも配置できます。アイデンティティハブの目的は個人データを保存することです。実装によっては、ユーザーが明示的に許可した場合、他のエンティティがユーザーのアイデンティティハブにアクセスできることがあります。アイデンティティハブは、個人の個人データストアと考えることができます。
    
*   __分散型識別（DID）__ とは、ブロックチェーンや台帳などの分散型システムで作成およびアンカーされた識別子であり、Issuer、Holder、Verifier、そしてアイデンティティハさえも、エコシステム内の任意のエンティティとして表現することができます。
    
*   __デジタルカード__ とは、ユーザーが時間の経過と共に収集する検証可能なクレデンシャルを表し、ユーザーエージェントまたはユーザーのアイデンティティハブの一部として格納されます。それらについて話すときは、検証可能なクレデンシャルではなく、デジタルカードと呼ぶ方がいくぶん簡単です。
    
*   __デジタルウォレット__ は物理的な財布のデジタルメタファーであり、一般的にユーザーエージェントと、携帯電話上の安全なストレージやセキュアエンクレーブなどのコンピューティングデバイスの基本機能の組み合わせによって表現されます。デジタルウォレットにはデジタルカードが入っています。
    
*   __dPKI__ とは分散型公開鍵基盤（decentralized public key infrastructure）であり、通常は不変なブロックチェーンまたは台帳、つまりDIDを登録し、DIDとそのメタデータに関連した公開鍵と共に検索できる場所を介して実装されます。dPKIは、 __検証可能なデータレジストリ__ の多くの可能な実装の1つにすぎないため、dPKIはより一般的には __検証可能なデータレジストリ__ として呼称できます。この文書ではdPKIについて言及していますが、検証可能なデータレジストリは必ずしも「分散」されている必要はないことに注意してください。
    
*   __ユニバーサルリゾルバ__ は、DIDドライバを通じてあらゆる分散型識別子システムと協働する識別子リゾルバです。ユニバーサルリゾルバの目的は、特定のDID値が与えられたときに、 DIDメタデータを含むDIDドキュメントを返すことでし。DIDはいくつもの異なるdPKI実装にアンカーされる可能性があるため、この機能は非常に有用です。
    

下図は先ほど説明した用語の一部を、主要なアクターとその関係で強調し、表しています。また、本書で後に取り上げるサンプルシナリオを表しています。

@row
![Digram of the issuance and presentation of verifiable credentials, starting with the issuer and moving on to the holder and verifier. Each of these actors touch the dPKI.](/assets/images/idpro_bok/decentralized-fig1.jpg)

Figure - Verifiable Credential Issuance and Presentation

@row
It is essential to note that no personally identifiable information should be stored on the decentralized public key infrastructure. Personal identity data is stored as part of the individual’s digital wallet or identity hub in a secure location.

Usually, the holder will present verifiable credentials to verifiers during a business transaction in real-time, like the way we currently present our passport at a border crossing. However, in more advanced scenarios, some implementations may enable the holder to grant a verifier-specific access to data in the holder’s identity hub. That way, the verifier can access data that the individual has allowed access to, instead of the individual having to manually present verifiable credentials to the verifier on a recurring schedule. Nevertheless, the more traditional approach still requires the holder to present verifiable credentials to the verifier explicitly, but the verifier will have the ability to periodically check the status of the credential, such as whether or not the credential has been revoked by the issuer, on its own without burden to the holder.

Now that you are armed with an understanding of the terminology, let’s take a closer look at a sample scenario.

@column
個人を特定できるような情報は分散型公開鍵基盤に保存されるべきでないことに注意することが重要です。個人のアイデンティティデータは、個人のデジタルウォレットまたはアイデンティティハブの一部として、安全な場所に保存されます。

通常、現在私たちが国境検問でパスポートを提示する方法のように、Holderはビジネストランザクション中に検証可能なクレデンシャルをリアルタイムにVerifierに提示します。しかし、より高度なシナリオの場合、一部の実装ではHolderのアイデンティティハブ内のデータへのVerifier専用のアクセス権をHolderが付与することができます。この方法であれば、個人が定期的なスケジュールでVerifierに検証可能なクレデンシャルを手動で提示する必要がなくなり、個人がアクセスを許可したデータにVerifierがアクセスできるようになります。それでも、より伝統的なアプローチはHolderがVerifierに検証可能なクレデンシャルを明示的に提示することを必要としますが、クレデンシャルがIssuerによって失効されているかどうかなどクレデンシャルのステータスをVerifierはHolderの負担なく独自に定期的にチェックする能力を持つことになります。

用語の理解を深めたところで、サンプルシナリオを詳しく見ていきましょう。

@row
## Decentralized Identity Scenario

The example below is meant to provide an end-to-end use-case of the value and utility of a decentralized identity ecosystem. It is not a comprehensive or exhaustive description of all that is possible with decentralized identities as it represents just one possible decentralized identity flow.

Suppose Sam wants to purchase vehicle insurance from Example Insurance, but to get a good rate, Example Insurance requires proof that Sam is a graduate of ABC University. In our decentralized identity scenario, the actors are as follows:

*   Sam as the verifiable credential subject and holder.
    
*   ABC University as the verifiable credential issuer.
    
*   Example Insurance as the verifiable credential verifier.
    

The following sequence of steps represents a flow where the end-goal is for Sam to receive a digital diploma from ABC University and then present it for verification to Example Insurance in order to claim the automobile insurance discount:

1.  Sam receives an email from ABC University congratulating Sam on graduating while also providing a QR code Sam can use to scan with Sam’s mobile phone. Sam has an app on Sam’s phone that is registered to handle such a request. This app represents Sam's _digital wallet_ that will hold all the _digital cards_ that were collected over time. Sam scans the QR code, the digital wallet app launches, and Sam is informed that in order to receive Sam’s digital diploma Sam needs to sign-in to the ABC University website.
    
2.  In our case, Sam presses on the link and enters Sam’s existing credentials to authenticate on the University's website or if Sam didn't have such a credential, Sam may be asked to come in person to the registrar's office to do ID proofing and receive their credentials. Once Sam provides their existing credentials, Sam is informed that Sam can go ahead and _accept_ this digital card from ABC University. Once Sam accepts the card, Sam is asked to secure this operation with a biometric, such as a fingerprint, face, or even a PIN. After Sam performs this action, the card is now securely stored in Sam's digital wallet. Sam can inspect the card, view the data that the card has about Sam (which was attested to by the university), such as Sam’s full name, major, graduation date, and issue date. Also, Sam can view the activity that this card was involved in, such as when it was issued, to whom it was presented, and how it was used - all of this can be done from the digital wallet app on Sam's phone. Each such activity can be considered as a _digital_ _receipt_ or _verifiable history_ that Sam can use to track who has (or had) access to the data for this card. These digital receipts are stored locally along with the card in Sam's digital wallet, which is always under Sam's control. More generally, we can also refer to this digital card as a _verifiable credential_.
    
3.  Now, to claim Sam’s discount, Sam navigates to the Example Insurance website on Sam’s mobile phone and notices the _Verify Credentials_ button. This is a deep link and when Sam presses it, the digital wallet app opens with a permission request. The permission request indicates that Example Insurance needs to receive a ABC University alumni digital card for Sam to get Sam’s discount. Note that Sam doesn't have to authenticate to Example Insurance with a username and password nor use a federated IdP. Sam can simply present the digital diploma Sam already possesses in Sam’s digital wallet. In our scenario, Sam only presents Sam’s ABC University alumni digital card to Example Insurance, but Sam could also present other digital cards Sam has in Sam’s digital wallet such as a digital card that proves Sam is a resident of a specific territory or to prove Sam’s current address. Once Sam authorizes the permission request with Sam’s biometric such as a fingerprint scan, Example Insurance now receives the digital card and is able to verify that it was indeed issued to Sam by ABC University, and it is indeed Sam who is presenting this digital card to Example. Once Example Insurance completes the verification, it can now offer a discount to Sam! Sam can now view that Sam’s digital wallet app has a receipt for this card, indicating that this card was presented to Example Insurance on a given date and for a specified purpose with Example’s terms and conditions. Some implementations may further enable Sam to _revoke_ the access Example Insurance has to view Sam’s digital card. This revocation action may generate another _receipt_ that clearly indicates the date and time Sam revoked Example's access to Sam’s digital card. Once again, Sam can accomplish all this from Sam’s digital wallet app on Sam’s mobile phone, and all the digital cards that Sam collects over time and Sam’s associated receipts are under Sam's control.
    
4.  Sam can collect many such digital cards in Sam’s digital wallet and at some point may even need to present multiple cards, such as in the case if Sam wants to attend an advanced enterprise architecture training academy, both proving Sam is a ABC University alumni as well as a certified enterprise architect. The academy can then instantly verify both credentials presented and enable Sam to access Sam’s advanced training material.
    

It is important to clarify that Sam sends a _verifiable presentation_ to Example Insurance. The verifiable presentation contains a nested artifact which is the _verifiable credential_ Sam has received from ABC University. In this manner, Example Insurance that is acting as the verifier, can verify the following two critical elements:

*   Based on the digital signature of the _verifiable credential_, Example Insurance verifies that the verifiable credential is authentic and was indeed issued by ABC University to Sam
    
*   Based on the digital signature of the _verifiable presentation_, Example Insurance verifies that it is indeed Sam who is performing this credential presentation
    

After Example insurance has verified the above, it is able to confidently present Sam with Sam’s vehicle insurance discount.

@column
## 分散型アイデンティティシナリオ

以下の例は、分散型アイデンティティエコシステムの価値と実用性に関するエンドツーエンドのユースケースを提供することを目的としています。これは、分散型アイデンティティフローの1つの可能性に過ぎないため、分散型アイデンティティで可能なことすべてを包括的または網羅的に説明するものではありません。

SamはExample Insuranceから自動車保険を購入したいとし、良いレートで購入するためには、Example InsuranceはSamがABC大学の卒業生であることの証明を要求します。この分散型アイデンティティシナリオでは、アクターは以下の通りです：

*   検証可能なクレデンシャルの主体であり、HolderとしてのSam。
    
*   検証可能なクレデンシャルのIssuerとしてのABC大学。
    
*   検証可能なクレデンシャルのVerifierとしてのExample Insurance。
    

以下の一連のステップは、SamがABC大学からデジタル卒業証書を受け取り、自動車保険の割引を請求するために、それをExample Insuranceに提示して検証することを最終目的とするフローを表しています：

1.  SamはABC大学から卒業を祝う電子メールを受け取り、同時にSamの携帯電話でスキャンできるQRコードも提供されました。Samの携帯電話には、このようなリクエストを処理するためのアプリが登録されています。このアプリはサムの __デジタルウォレット__ であり、これまでに収集した __デジタルカード__ がすべて保持されています。SamがQRコードを読み取ると、デジタルウォレットのアプリが起動し、Samのデジタル卒業証書を受け取るためには、SamがABC大学のウェブサイトにサインインする必要があることが通知されます。
    
2.  この場合、Samはリンクを押し、Samの既存のクレデンシャルを入力して大学のウェブサイトで認証するか、Samがそのようなクレデンシャルを持っていなかった場合、Samは身元確認をおこない、クレデンシャルを受け取るために教務課に直接来るように依頼されるかもしれません。Samが既存のクレデンシャルを提供すると、Samは、ABC大学からこのデジタルカードを受け取ることができることを知らされる。Samが既存のクレデンシャルを提供すると、SamはABC大学からデジタルカードを __受け取る__ ことができると通知されます。Samがこのカードを受け取ると、Samはこの操作を指紋、顔のような生体認証あるいはPINで保護するように求められます。Samがこのアクションを完了させると、カードはSamのデジタルウォレットに安全に格納されます。Samはカードを点検し、カードが持っているSamに関するデータ（大学が認証したもの）、例えばSamのフルネーム、専攻、卒業日、発行日などを閲覧することができます。また、このカードがいつ発行され、誰に提示され、どのように使用されたかといった、このカードが関与した活動を見ることができ、これらはすべてSamの携帯電話のデジタルウォレットアプリから実行できます。このような活動はそれぞれ __デジタル領収証__ や __検証可能な履歴__ とみなすことができ、Samはこのカードのデータに誰がアクセスできるのか（またはしたのか）を追跡するためにこれらを利用できます。デジタル領収書は、Samのデジタルウォレットにカードとともにローカルに保存され、常にSamの管理下に置かれます。より一般的には、このデジタルカードは __検証可能なクレデンシャル__ と呼ぶこともできます。
    
3.  今、Samの割引を請求するために、SamはSamの携帯電話でExample Insuranceのウェブサイトに移動し、 __クレデンシャル検証__ ボタンに気づきます。これはディープリンクで、Samがこれを押すと、デジタルウォレットアプリが開き、許可要求が表示されます。許可要求は、Example InsuranceがSamの割引を受けるために、ABC大学の卒業生デジタルカードを受け取る必要があることをSamに示しています。Samは、ユーザー名とパスワードでExample Insuranceを認証する必要もなく、フェデレーションされたIdPを利用する必要もないことに注意してください。Samは、Samのデジタルウォレットに既に保持しているデジタル卒業証書を提示するだけでよいのです。このシナリオでは、SamはExample InsuranceにSamのABC大学の卒業生デジタルカードを提示するだけですが、Samのデジタルウォレットにある他のデジタルカード、Samが特定の地域の住民であることを証明するデジタルカードやSamの現住所を証明するカードなどを提示することも可能です。Samが指紋スキャンなどのSamのバイオメトリクスで許可要求を認可すると、今度はExample Insuranceがデジタルカードを受け取り、それが確かにABC大学からSamに発行され、Example Insuranceにこのデジタルカードを提示しているのは確かにSamであることを検証することができるようになります。Example Insuranceは検証を完了すると、今度はSamに割引を提供することができます！Samは、Samのデジタルウォレットアプリにこのカードの領収書があり、このカードがExample Insuranceに所定の日付に所定の目的でExample Insuranceの条件に従って提示されたことを領収書が示していることを確認できます。さらに、一部の実装ではSamはExample InsuranceがSamのデジタルカードを閲覧するために有するアクセス権を __取り消す__ ことを可能にします。この取り消し動作は、SamがExample InsuranceのSamのデジタルカードへのアクセス権を取り消した日付と時刻を明確に示す別の __領収書__ を生成することができます。再び、SamはSamの携帯電話上のSamのデジタルウォレットアプリからこの全てを完了でき、Samがこれまでに収集したすべてのデジタルカードとSamの関連する領収書はSamの制御下にあります。
    
4.  Samは、Samのデジタルウォレットにこのようなデジタルカードを多数収集することができ、ある時点では複数のカードを提示する必要さえあるかもしれません。例えば、Samが高度なエンタープライズアーキテクチャのトレーニングアカデミーに参加したい場合、SamがABC大学の卒業生であり、かつ認定エンタープライズアーキテクチャであることの証明が必要です。アカデミーは提示された両方のクレデンシャルを即座に確認し、Samに上級トレーニング教材にアクセス権を与えることができます。
    

Samが __検証可能なプレゼンテーション__ をExample Insuranceに送信することを明確にすることが重要です。検証可能なプレゼンテーションには、SamがABC大学から受け取った __検証可能なクレデンシャル__ であるネストされたアーティファクトが含まれています。このようにして、VrifierであるExample Insuranceは、以下の2つの重要な要素を検証することができます：

*   __検証可能なクレデンシャル__ のデジタル署名に基づいて、Example Insuranceは検証可能なクレデンシャルが本物であり、ABC大学からSamに確かに発行されたことを検証します。
    
*   __検証可能なプレゼンテーション__ のデジタル署名に基づいて、Example Insuranceはこのクレデンシャルプレゼンテーションを実行しているのが本当にSamであることを検証します。
    

Example Insuranceは上記を検証した後、自信を持ってSamにSamの車両保険割引を提示することができます。

@row
### Decentralized Identity Technical Implementation

The following sequence is a technical explanation of the same scenario presented above. It outlines the steps that must be taken to setup the decentralized identity experience as well as the verifiable credential issuance and presentation flows. However, this scenario assumes that the decentralized public key infrastructure (dPKI) has already been setup and will not be detailed here.

@column
### 分館型アイデンティティの技術的な実装

次のシーケンスは、上記と同じシナリオの技術的な説明です。分散型アイデンティティエクスペリエンスをセットアップするために実行しなければならないステップと、検証可能なクレデンシャルの発行および提示のフローについて概説します。ただし、このシナリオでは分散型公開鍵基盤（dPKI）が既にセットアップされていることを前提としており、ここでは詳しく説明しません。

@row
#### Setup

1.  ABC University represents the issuer. A generates a decentralized identifier (DID) tied to a public/private key pair and registers their DID on the dPKI. The private key is stored by the ABC University IT team in a Key Vault or Hardware Security Module. The corresponding public key is published to a decentralized ledger such as a blockchain so that anyone can find it.
    
2.  ABC University IT publishes a DID document that associates its DID to the registered public Domain Name System (DNS) domain, such as A.edu. This represents a domain linkage verifiable credential. ABC University IT can host this file on their website which both proves ownership of the domain and the specific DID. The verifier (such as Example Insurance) can use this DID document to confirm the DID ownership for ABC University and ensure that the verifiable credential it receives is indeed issued by ABC University and not by some other issuer claiming to be ABC University.
    
3.  ABC University IT develop a contract that describes the requirements for the issuance of the verifiable credential. For example, ABC University IT can specify which attestations should be self-issued directly by the user, and which other verifiable credentials, if any, the individual must first provide. In our scenario, the IT team has mandated that the student authenticate with a federated IdP that supports the OpenID Connect protocol, so that it will be able to receive a security token and extract claims from it, such as first name, last name, and student number. The issuer will then be able to map it to attributes it will issue in the verifiable credential. Importantly, ABC University will indicate the schema(s) to which the verifiable credential will conform, so that other verifiers around the world will be able to consume the content of the verifiable credential those verifiers receive.
    
4. Finally, ABC University IT administrators can setup and customize the branding of the soon-to-be-issued verifiable credential cards such as card color, logos, icons, images, and helpful text. The administrators can customize the helpful text strings via metadata that will appear as part of the cards based on the attestations issued with the card for credential data. This will help design the look and feel of verifiable credential alumni cards issued by ABC University, and ensure the issued digital cards reflect the brand of the university. In the future, these graphical elements should be standardized so that students enjoy a consistent digital card visual rendering experience regardless of which vendor develops the user agent or digital agent the student chooses to use.
    

@column
#### セットアップ

1.  ABC大学はIssuerを表します。ABC大学は、公開鍵と秘密鍵のペアに関連付けられた分散識別子（DID）を生成し、そのDIDをdPKIに登録します。秘密鍵は、ABC大学のITチームによってKey Vaultまたはハードウェアセキュリティモジュールに格納されます。対応する公開鍵は、ブロックチェーンなどの分散台帳に公開され、誰でも見つけることができます。
    
2.  ABC大学のIT部門は、そのDIDをA.eduのような登録済みパブリックドメインネームシステム（DNS）ドメインに関連付けるDIDドキュメントを発行します。これは、ドメインリンケージされた検証可能なクレデンシャルを表します。ABC大学のIT部門は、ドメインの所有権と特定のDIDの両方を証明するこのファイルを自分のウェブサイトでホストすることができます。Verifier（保険会社のような）はこのDIDドキュメントを使用して、ABC大学のDID所有権を確認し、受け取った検証可能なクレデンシャルが本当にABC大学によって発行されたものであり、ABC大学を名乗る他のIssuerによって発行されたものではないことを確認できます。
    
3.  ABC大学のIT部門は、検証可能なクレデンシャルの発行要件を記述した契約を作成します。たとえば、ABC大学のIT部門は、ユーザが直接自己発行すべきか証明書を指定し、他の検証可能なクレデンシャルがある場合は、どのクレデンシャルをその個人が最初に提供しなければならないかを指定できます。このシナリオでは、ITチームはOpenID ConnectプロトコルをサポートするフェデレーションされたIdPで学生が認証することを義務付けており、これによってセキュリティトークンを受け取り、そこから姓、名、学生番号のようなクレームを抽出できます。Issuerはそれを検証可能なクレデンシャルで発行する属性にマッピングできます。重要なことは、ABC大学は検証可能なクレデンシャルが準拠するスキーマを示し、世界中の他のVerifierは受け取った検証可能なクレデンシャルのコンテンツを消費できるようにすることです。
    
4. 最後に、ABC大学のIT管理者は、カードの色、ロゴ、アイコン、画像および役立つテキストなど、間もなく発行される検証可能なクレデンシャルカードのブランディングを設定およびカスタマイズすることができます。管理者はクレデンシャルデータのカードとともに発行される証明書に基づき、カードの一部として表示されるメタデータを介して、役立つテキスト文字列をカスタマイズすることができます。これにより、ABC大学が発行する検証可能なクレデンシャル卒業生カードのルック＆フィールをデザインし、発行されたデジタルカードが大学のブランドを反映することを保証します。将来的には、これらのグラフィック要素を標準化し、学生が使用するユーザーエージェントやデジタルエージェントをどのベンダーが開発しても、一貫したデジタルカードの視覚的レンダリング体験を享受できるようにするべきです。
    

@row
#### Verifiable Credential Issuance

1.  The credential issuance request flow begins when Sam scans a QR code using Sam’s mobile phone. The purpose of the issuance request is for Sam’s user agent to retrieve the requirements for credential issuance as dictated by the issuer and to display the appropriate UX to the user via the user agent. As such, the QR code is displayed on the ABC University website and scanning the QR code opens Sam's digital wallet mobile app and triggers an issuance request retrieval operation from the user agent to ABC University. Once the user agent receives the issuance request from ABC University, it begins the flow to issue the credential. The issuance request is digitally signed by ABC University and the user agent can verify the authenticity of such a request. The issuance request includes a reference to the contract that describes how the user agent should render the UX and what information Sam needs to provide in order to be given a verifiable alumni credential.
    
2.  After the user agent verifies that the request is genuine, it renders the UX to Sam. Because of the specific requirement that A has for issuing digital alumni cards in our scenario, Sam needs to sign in with Sam’s existing ABC University account, which, in turn, will issue a security token to the user agent with claims such as Sam's first name and last name, degree, and graduation date. (Note that during setup above, the issuer can be configured to accept security tokens from any trusted and compliant OpenID Connect identity provider and the user agent will use this identity provider during the issuance process.) Therefore, when the individual presses ‘Login to ABC University’ on the user agent, the user agent can redirect the individual to authenticate with the IdP, and it is there the individual can perform standard authentication tasks such as entering their username and password, performing Multi-Factor Authentication (MFA), accepting terms of service, or even paying for their credential. All this activity occurs on the client side via the user agent (e.g., a mobile app). When the user agent finally receives the security token from the IdP, it can pass it along to the issuer which can then extract claims from it, as mentioned above, and inject these as attributes into the resulting verifiable credential, potentially enriching the claims with information obtained from other sources. As well, after the individual authenticates with the IdP, the user agent can display additional input fields that the individual is free to self-select. After the individual has provided all the required information, the user agent can verify that it has all the necessary issuer requirements fulfilled, and it can go ahead and ask if Sam would like to accept the card.
    
3.  In our scenario, when Sam accepts the card, Sam is asked to use a biometric gesture such as a fingerprint scan. This action generates a private/public key pair for Sam’s DID whereby the private key is stored on the mobile phone in a secure enclave, and the public key is published to a distributed ledger.
    
4.  Finally, the issuer receives all the required information alongside Sam’s DID and issues the digital card to Sam who then receives the verifiable credential, which is a JSON Web Token (JWT) following the W3C standard for verifiable credentials. The JWT includes both the DID of the subject, Sam, and the DID of the issuer, ABC University, as well as the type of the credential, and any attestations such as first name, last name, major, and graduation date. It also contains a way to find out the credential's revocation status in case the credential is later revoked by the issuer - ABC University. This verifiable credential is digitally signed by the issuer's DID.
    
5.  Once the user agent validates the verifiable credential received from ABC University, it inserts this digital card into Sam's digital wallet as a card Sam can now present to other organizations such as Example Insurance.
    

@column
#### 検証可能なクレデンシャルの発行

1.  クレデンシャル発行要求フローは、Samが自分の携帯電話を使用してQRコードをスキャンしたときに開始されます。発行リクエストの目的は、SamのユーザーエージェントがIssuerが指示するクレデンシャル発行の要件を取得し、ユーザーエージェントによってユーザーに適切なUXを表示することです。そのため、ABC大学のウェブサイトにQRコードが表示され、QRコードをスキャンするとSamのデジタルウォレットモバイルアプリが開き、ユーザーエージェントからABC大学への発行要求取得操作がトリガーされます。ユーザーエージェントはABC大学から発行要求を受け取ると、クレデンシャルを発行するためのフローを開始します。発行要求はABC大学によってデジタル署名されており、ユーザーエージェントはそのような要求の真正性を検証することができます。発行要求には、ユーザーエージェントがどのようにUXをレンダリングすべきか、また検証可能な卒業生クレデンシャルを付与されるためにSamが提供する必要がある情報は何かを記述した契約への参照が含まれています。
    
2.  ユーザーエージェントはリクエストが本物であることを確認した後、ユーザーエージェントはSamに対してUXをレンダリングします。このシナリオではABC大学がデジタル卒業生カードを発行するという特別な要件があるため、SamはSamの既存のABC大学アカウントでサインインする必要があり、その結果、Samの姓名、学位、卒業日のようなクレームを含むセキュリティトークンがユーザエージェントに発行されます。（上述のセットアップ中にIssuerは信頼され準拠したOpenID Connectアイデンティティプロバイダーからセキュリティトークンを受け取るように設定することができ、ユーザエージェントは発行プロセス中にこのアイデンティティプロバイダーを使用することになることに注意してください。）したがって、個人がユーザエージェント上で「Login to ABC University」を押すと、ユーザエージェントは個人をIdPでの認証にリダイレクトすることができ、そこで個人はユーザー名とパスワードの入力、多要素認証（MFA）の実行、サービス条件の受け入れ、またはクレデンシャルの払い出しなどの標準的な認証タスクを実行できるようになります。この活動はすべて、ユーザーエージェント（モバイルアプリなど）を介してクライアント側でおこなわれます。ユーザーエージェントが最終的にIdPからセキュリティトークンを受け取ると、それをIssuerに渡すことができ、Issuerは前述のようにそこからクレームを抽出し、これらを検証可能なクレデンシャルに属性として注入し、他のソースから得た情報でクレームを充実させる可能性があります。同様に、個人がIdPで認証した後、ユーザーエージェントは個人が自由に選択できる追加の入力フィールドを表示することができます。個人が必要な情報をすべて提供した後、ユーザーエージェントは必要なIssuer要件がすべて満たされていることを確認し、Samがカードを受け入れるかどうかを尋ねることができます。
    
3.  このシナリオでは、Samがカードを受け取ると、Samは指紋スキャンなどのバイオメトリックジェスチャーを使用するよう求められます。この動作により、SamのDIDのために秘密鍵と公開鍵のペアが生成され、秘密鍵は携帯電話のセキュアエンクレーブに保存され、公開鍵は分散台帳に公開されます。
    
4.  最後に、IssuerはSamのDIDと共にすべての必要な情報を受け取り、デジタルカードをSamに発行します。Samは検証可能なクレデンシャルのW3C標準仕様に従うJSON Web Token（JWT）である検証可能なクレデンシャルを受け取ります。このJWTには、主体であるSamのDIDとIssuerであるABC大学のDIDの両方およびクレデンシャルの種類と姓、名、専攻、卒業日などの証明書が含まれます。また、クレデンシャルが後にIssuerであるABC大学によって取り消された場合に備えて、クレデンシャルの失効状態を調べる方法も含まれています。この検証可能なクレデンシャルは、IssuerのDIDによってデジタル署名されています。
    
5.  ユーザーエージェントは、ABC大学から受け取った検証可能なクレデンシャルを検証すると、このデジタルカードを、SamがExample Insuranceのような他の組織に提示できるカードとしてSamのデジタルウォレットに追加します。
    

@row
#### Verifiable Credential Presentation

1.  When Sam visits the Example Insurance website on their mobile phone to receive a discount on their vehicle insurance, Sam presses the ‘Verify Credentials’ button on the Example website (which is a deep link) or simply scans a QR code generated by Example via their mobile phone. This generates a presentation/verification request for Sam to verify Sam’s ABC University alumni status. The request describes the type of card(s) that Sam should present to Example Insurance, such as Sam’s digital alumni card from ABC University, and this request is digitally signed by the verifier's DID, which in our case, is Example Insurance. The presentation request can also include Example's terms of service.
    
2.  After the signature of the request is verified by the user agent, Sam is presented with a UI on the user agent indicating that Example Insurance is requesting permission to see Sam’s ABC University alumni card with a reason as to why Example needs to see it (such as for Sam to be able to receive their discount).
    
3.  After Sam approves the request with a biometric gesture, such as with a fingerprint scan on the mobile phone, the verification response, which is essentially a presentation of a credential response (also known as a verifiable presentation), is sent to Example Insurance. The response is signed by Sam's private key and includes the verifiable credential issued by ABC University to Sam nested inside the JWT payload.
    
4.  Example Insurance attempts to match the person performing the presentation of the credential with the subject of the nested verifiable credential to ensure that it is indeed Sam who is presenting it to Example Insurance, and not anybody else. Therefore, the DID of Sam is present in both the outer JWT payload since Sam is performing the presentation of the credential, as well as inside the nested JWT payload as the subject of the verifiable credential issued by ABC University. Once Example Insurance confirms that the DID in the presentation matches the subject of the issued credential, Sam is both authenticated to the Example Insurance website and authorized to claim Sam’s discount! This is much better than simply possessing a username and password, since, in this mechanism, Example Insurance knows that the person presenting this credential is the same person to whom the card was issued. With a username and password, someone else can use it to impersonate you. In this architecture, however, this is significantly harder to do. Someone else will need to take control of Sam's private key stored on Sam’s phone's secure enclave to be able to accomplish this malevolent task.
    
5.  At last, Example Insurance can extract the data it requires from the verifiable credential such as Sam's first name, last name, major, graduation date, and go ahead and present Sam with Sam’s vehicle insurance discount!
    
6.  The credential verification flow completes when Sam stores a signed receipt by Example Insurance that will be associated with the card in Sam’s wallet. Sam now has a single place where Sam can view all the websites where Sam has presented Sam’s alumni card over time. In our scenario, the receipt includes information about Example Insurance, the reason Example needed to receive the card, Example's terms and conditions, and the date the receipt was generated. This signed receipt is associated with the card in Sam's digital wallet and will always be under Sam's possession.
    
7.  Some implementations may further enable Sam to go ahead and decide to revoke Example's access to Sam’s ABC University digital alumni card. Example should thus implement the necessary revocation measures to ensure it complies with Sam's request. The verifier should then cease to use the data from the card Sam presented to it. Sam can later prove that Sam issued a revocation request if such a need arises, and this can help with General Data Protection Regulation (GDPR) compliance.
    

@column
#### 検証可能なクレデンシャルの提示

1.  Samが自動車保険の割引を受けるために携帯電話でExample IssuranceのWebサイトにアクセスすると、SamはExample IssuranceのWebサイトの「Verify Credentials」ボタン（ディープリンク）を押すか、単にExample Issuranceよって生成されたQRコードを携帯電話を介してスキャンします。これにより、SamがABC大学の卒業生であることを確認するための提示/検証のリクエストが生成されます。リクエストにはSamがExample Issuranceに提示する必要があるカードのタイプ、ABC大学からのSamのデジタル卒業生カードのように記述されており、このリクエストはVerifierのDID、この場合はExample Issuranceによってデジタル署名されています。提示リクエストには、Example Issuranceの利用規約を含めることもできます。
    
2.  リクエストの署名がユーザーエージェントによって検証された後、Samに対してユーザーエージェントにUIが表示され、Example IssuranceがSamの ABC大学卒業生カードを確認する権限を要求していることが、Example Issuranceがそれを確認する必要がある理由と共に表示されます（Samが割引を受けられるようにするため、など）。
    
3.  Samが携帯電話での指紋スキャンなどのバイオメトリックジェスチャを使用して要求を承認した後、基本的にクレデンシャルレスポンスの提示（検証可能なプレゼンテーションとも呼ばれます）である検証レスポンスがExample Issuranceに送信されます。このレスポンスはSamの秘密鍵によって署名され、ABC大学がSamに発行した検証可能なクレデンシャルがJWTペイロード内にネストされています。
    
4.  Example Issuranceは、クレデンシャルの提示をおこなっている人物とネストされた検証可能なクレデンシャルの主体を照合して、それを提示しているのは確かにSamであり他の誰でもないことを確認しようとします。したがって、Samがクレデンシャルの提示をおこなっているため、SamのDIDはABC大学によって発行された検証可能なクレデンシャルの主体としてネストされているJWTペイロード内だけでなく、外側のJWTペイロードにも存在しています。提示されたDIDと発行されたクレデンシャルの主体が一致することをExample Issuranceが確認すると、SamはExample IssuranceのWebサイトに対して認証され、Samの割引を請求することを認可されます！これは、単にユーザー名とパスワードを所有するよりもはるかに優れています。このメカニズムでは、Example Issuranceはこのクレデンシャルを提示している人物がカードを発行された人物と同じであることを知っているからです。ユーザー名とパスワードを使用すると、他の誰かがそれを使用してあなたになりすますことができます。しかし、このアーキテクチャでこれを実施することは非常に困難です。この悪意のあるタスクを実行するには、Samの電話のセキュアエンクレーブに保存されているSamの秘密鍵を他の誰かが制御する必要があります。
    
5.  最後に、Example Issuranceは検証可能なクレデンシャルからSamの名、姓、専攻、卒業日のような必要なデータを抽出し、Samの自動車保険の割引をSamに提供できます！
    
6.  Samのウォレット内のカードに関連付けられるExample Issuranceによって署名された領収書をSamが保存すると、クレデンシャルの検証フローが完了します。これによって、Samが過去にSamの卒業生カードを提示したすべてのWebサイトを表示できる1つの場所をSamは手に入れました。このシナリオでは、領収書にはExample Issuranceに関する情報、Example Issuranceがカードを受け取る必要があった理由、Example Issuranceの契約条件および領収書が生成された日付が含まれています。この署名済みの領収書はSamのデジタルウォレット内のカードに関連付けられており、常にSamの所有物になります。
    
7.  さらに、一部の実装では、Samが将来的にExample IssuranceによるSamのABC大学のデジタル卒業生カードへのアクセス権を取り消すことを決定できることがあります。したがって、Example IssuranceはSamのリクエストに準拠することを確かにするため、必要な取り消し手段を実装するべきです。VerifierはSamが提示したカードからのデータの使用を停止する必要があります。Samはそのような必要が生じた場合に、Samが取り消しリクエストを発行したことを後から証明でき、一般データ保護規則（GDPR）への準拠に役立ちます。
    

@row
#### Scenario Summary

In our simple use-case above, the issuer of a verifiable credential was ABC University, but in other contexts, the issuer can be an employer, a government agency, a device, a daemon process, or even the individual. Likewise, a verifier can also be any of the previously mentioned actors. The decentralized identity ecosystem is very broad and the standards allow for opportunities to unlock a more flexible, secure, and privacy-preserving way to perform digital interactions in a myriad of contexts.

The components presented in the flow above are based on open standards. The verifiable credentials issuance and presentation flows depend on the foundational specification of the _W3C Verifiable Credentials Standard_, and the decentralized system, such as blockchains and ledgers, are based on _W3C Decentralized Identifiers_ work. The purpose of the decentralized ledger technology is to support a decentralized public key infrastructure (dPKI). The dPKI anchors DIDs and their public keys and thus enables ownership of DIDs to be validated without relying on only a few privileged identity providers or certification authorities.

The Decentralized Identity Foundation is leading the effort on decentralized identity, but more work remains to fully define the space.[^3] For example, the decentralized identity community is discussing how to enable better privacy preservation by empowering Sam to present Sam’s age in a privacy-preserving way without unnecessarily disclosing Sam’s exact date of birth to the verifier. Another area under discussion is how to empower Sam with performing self-owned key recovery in case Sam loses or damages Sam’s phone, so that Sam can more easily retrieve all Sam’s previously acquired digital cards back onto a different device or onto a different user agent in a more seamless manner.

@column
#### シナリオのまとめ

上記の単純なユースケースでは、検証可能なクレデンシャルのIssuerはABC大学でしたが、他のコンテキストでは、Issuerは雇用者、政府機関、デバイス、デーモンプロセス、または個人である可能性もあります。同様に、Verifierも先に述べたアクターのいずれかになる可能性があります。分散型アイデンティティエコシステムは非常に広範であり、標準仕様は無数の文脈でデジタルインタラクションを実行するための、より柔軟で安全かつプライバシーを保護する方法を解き放つ機会を提供することができます。

上記のフローで提示されるコンポーネントは、オープンな標準仕様に基づいています。検証可能なクレデンシャルの発行と提示のフローは __W3C Verifiable Credentials Standard__ の基礎仕様に依存し、ブロックチェーンや台帳などの分散システムは __W3C Decentralized Identifiers__ のワークに基づいています。分散台帳技術の目的は、分散型公開鍵基盤（dPKI）をサポートすることです。dPKIはDIDとその公開鍵をアンカーし、少数の特権的なアイデンティティプロバイダーや認証局だけに依存することなく、DIDの所有権を検証することができるようになります。

分散型アイデンティティファウンデーションは分散型アイデンティティの取り組みを主導していますが、この空間を完全に定義するためにはさらに多くの作業が残っています。[^3] 例えば、分散型アイデンティティコミュニティでは、VerifierにSamの正確な生年月日を不必要に開示することなく、プライバシーを保護する方法でSamの年齢を提示することを可能にし、より優れたプライバシー保護を可能にする方法について議論しています。また、Samが携帯電話を紛失したり破損したりした場合に、Samに自己所有の鍵のリカバリー能力を持たせて、Samが以前取得したすべてのデジタルカードを別のデバイスや別のユーザーエージェントによりシームレスに復元できるようにする方法も検討されています。

@row
### Decentralized Identity Limitations

While decentralized identity has the potential to improve an individual’s productivity and digitize existing business processes for governments and corporations, it does have known limitations and areas where further research or investigation would be required. A decentralized identity ecosystem can only be successful when it achieves critical mass adoption by governments, businesses, and individuals. When Apple released the first iPhone, it ushered in a new and immediate change in the user experience the moment the purchaser took possession of their new device. In contrast, an individual may not gain much benefit in obtaining a verifiable credential from an issuer unless they can then use that verifiable credential with many verifiers. A digital passport, for example, is only useful to a citizen if it can be used at most airports and border crossings around the world. Organizations may hesitate to be issuers or verifiers of verifiable credentials unless there is already a healthy ecosystem in place, but that ecosystem cannot develop unless there are entities willing to issue and verify these new credentials.

Decentralized identity is a digital identity. Without the necessary technology to hold a digital wallet, such as on a mobile phone or some sort of computing device, it will be very difficult for the promise of digital identity to be realized by all individuals around the world. If an individual loses their device or decides to share their device with others without proper precautions, it can become a challenge to recover their data onto a different device or to prove who performed a specific interaction. Asking the average person to understand this and to safeguard their private key material remains a significant challenge to decentralized key management.

In most decentralized identity use-cases, the developers assume all parties involved have access to the Internet. That may not be the case. Other scenarios that take the individual away from Internet access leave open the question of how verifiable credentials can be verified in such scenarios. Verifying verifiable credentials requires looking up information on the dPKI, or at the very least, checking if a credential that is being presented has been revoked, and that requires network connectivity. In purely disconnected offline environments this poses a challenge, and a potential hurdle to decentralized identity adoption in specific contexts and situations.

The promise of decentralized identity is to empower individuals to own and control their digital identity and personal data. However, if a person provides a verifiable credential containing personal data to the service provider, the service provider is able to copy this data to its own databases for marketing purposes or to be able to continue providing services to the user. The individual can attempt to revoke access that the service provider has to the verifiable credential but there is no guarantee that the service provider will honor such a request and delete all the data it has stored about the user. This would be a very challenging problem to solve via strictly technological measures and would most likely require legal and policy frameworks in place to ensure everyone’s personal data is protected, to ensure audit records are kept, and to establish a documented process for dispute management and resolution.

@column
### 分散型アイデンティティの限界

分散型アイデンティティは個人の生産性を向上させ、政府や企業の既存のビジネスプロセスをデジタル化する可能性を秘めていますが、さらなる研究や調査が必要な既知の限界や分野があります。分散型アイデンティティエコシステムは、政府、企業および個人によるクリティカルマス採用を達成した場合にのみ成功することができます。Appleが最初のiPhoneをリリースしたとき、購入者が新しいデバイスを所有した瞬間に、ユーザーエクスペリエンスに新しい即時の変化をもたらしました。対照的に、個人は多くのVerifierと検証可能なクレデンシャルを使用できない限り、Issuerから検証可能なクレデンシャルを取得することによる利益を多く得ることができないでしょう。たとえば、デジタルパスポートは世界中のほとんどの空港や国境検問所で使用できる場合にのみ、市民にとって有用です。組織は健全なエコシステムが既に整っていない限り、検証可能なクレデンシャルのIssuerまたはVerifierになることを躊躇するかもしれませんが、これら新しいクレデンシャルを発行して検証するエンティティがない限り、そのエコシステムは発展しません。

分散型アイデンティティはデジタルアイデンティティです。携帯電話や何らかのコンピューティングデバイスなど、デジタルウォレットを保持するために必要な技術がなければ、デジタルアイデンティティの約束が世界中のすべての個人によって実現されることは非常に困難です。個人がデバイスを紛失したり、適切な予防措置を取らずにデバイスを他の人と共有することを決めたりした場合、データを別のデバイスに復元したり、誰が特定の操作を実行したかを証明したりすることが難しくなる可能性があります。平均的な人にこれを理解し、秘密鍵を保護するように求めることは、分散型鍵管理にとって依然として重大な課題です。

ほとんどの分散型アイデンティティユースケースでは、開発者は関係者全員がインターネットにアクセスできると想定しています。そうでないこともあります。個人をインターネットアクセスから遠ざける他のシナリオでは、そのようなシナリオで検証可能なクレデンシャルをどのように検証できるかという疑問が残ります。検証可能なクレデンシャルを検証するには、dPKIに関する情報を検索するか、少なくとも提示されているクレデンシャルが取り消されているかどうか、およびネットワーク接続が必要であるかどうかを確認する必要があります。純粋に切断されたオフライン環境では、これは課題を提起し、特定のコンテキストや状況で分散型のアイデンティティを採用するための潜在的な障害となります。

分散型アイデンティティの約束は、個人が自分のデジタルアイデンティティと個人データを所有し、制御できるようにすることです。しかし、個人データを含む検証可能なクレデンシャルをサービスプロバイダーに提供する場合、サービスプロバイダーはマーケティング目的やユーザーにサービスを提供し続けるために、このデータを独自のデータベースにコピーすることができます。個人は、サービスプロバイダーが検証可能なクレデンシャルに対して持っているアクセスの取り消しを試みることができますが、サービスプロバイダーがそのような要求を受け入れ、ユーザーについて保存したすべてのデータを削除するという保証はありません。これは、厳密に技術的な手段で解決することは非常に困難な問題であり、すべての人の個人データが確実に保護され、監査記録が確実に保持され、紛争管理と解決のための文書化されたプロセスを確立するために、法的および政策的枠組みが必要になる可能性が最も高いです。

@row
## Final Words

Decentralized identity can enable entirely new business opportunities and empower citizens to be more in control of their identity and personal data. Today, IT administrators need to perform cryptographic key exchange ceremonies to establish trust between two organizational entities. This does not scale when doing business with dozens or perhaps hundreds of other vendors in a more ad-hoc manner. Today, when a bank issues a credit card to a customer, that customer can use that credit card to make purchases with almost any merchant worldwide. In such a scenario, it is not feasible to expect every merchant to exchange cryptographic keys a-priori with every possible bank that issues credit cards. A decentralized identity ecosystem can enable a similar concept to credit card associations by introducing governance authorities and frameworks for many different trust communities in a wide array of industry verticals. As a result, merchants, or other verifiers, can avoid setting up multiple trust federations – they can simply ask the issuer to present additional proofs proving that the issuer is indeed a member of a specific governance authority with which the verifier already has an established trust relationship.

One of the major hurdles for adopting blockchain today in enterprise scenarios is the lack of a decentralized identity infrastructure. After all, it’s not very logical to have a decentralized blockchain network if all the identities on it are still relying on centrally controlled accounts. Furthermore, in a decentralized identity ecosystem, consumers will be more easily able to track which websites they visit online and with whom they transact. You will know which businesses have your personal data, and you will be able to revoke access to it should you so desire. Instead of sharing paper documents or physical cards, you will be able to share digital documents and digital cards in a fully digital, privacy-preserving, and auditable manner. For organizations, this may reduce GDPR-related risk since personal data will be stored in the identity hub under the individual’s control, while the organization will only have access to specific data as granted by the user. Furthermore, the individual may have the opportunity to revoke access to their data, and this may simplify the GDPR compliance for an organization as well as streamline such requests for the individual. As well, GDPR compliance may be eased for an organization as it will be able to possess cryptographic proof as evidence that the individual has indeed provided them with specific data.

As discussed, the digital wallet contains a digital agent app with which the user interacts. Such digital or user agents are mostly based on open source software. The individual can download a user agent from a commercial corporation, or perhaps even a government entity. An individual may even develop their own user agent from existing open source software. Conceptually, an individual must trust the user agent and it should be under the individual’s control.

While it is extremely challenging to attempt to predict how the decentralized identity landscape will evolve given its nascent state, current trends are indicating government interest to ease the burden on citizens and businesses via government-issued digital IDs. Tailwinds from the unprecedented global COVID-19 pandemic are urging government institutions to streamline citizen and business access to government-provided services. As well, increasingly stringent regulatory compliance requirements and further demand by users for better user experience and increased convenience may further drive demand for digital identity in the form of verifiable credential exchange. Finally, verifiable credentials may prove very useful in situations where the same credential must be presented both online in digital transactions as well as in offline in-person interactions, since this can result in increased business efficiencies for the enterprise and a more consistent and simplified user experience.

@column
## 最後に

分散型アイデンティティは、まったく新しいビジネスチャンスを可能にし、市民が自分のアイデンティティと個人データをより自由にコントロールできるようにできます。今日、IT管理者は、2つの組織体間の信頼を確立するために暗号鍵交換式を実行する必要があります。これでは、何十、何百ものベンダーとその場しのぎの取引をしている場合、スケールアップできません。今日、銀行が顧客にクレジットカードを発行すると、その顧客はそのクレジットカードを使って世界中のほとんどすべての加盟店で買い物をすることができます。このようなシナリオでは、すべての加盟店がクレジットカードを発行する可能性のあるすべての銀行と事前に暗号鍵を交換することを期待するのは現実的ではありません。分散型アイデンティティエコシステムは、幅広い業種のさまざまな信頼コミュニティに対してガバナンス当局とフレームワークを導入することで、クレジットカード協会と同様の概念を実現できます。その結果、加盟店やその他のVerifierは、複数のトラストフェデレーションを設定する必要がなくなり、Verifierがすでに信頼関係を確立している特定のガバナンス当局のメンバーであることを証明する追加の証明をIssuerに提示するよう求めるだけでよくなります。

今日、エンタープライズなシナリオでブロックチェーンを採用するための大きなハードルの1つは、分散型アイデンティティインフラストラクチャの欠如です。結局のところ、分散型ブロックチェーンネットワーク上のすべてのアイデンティティが依然として中央で管理されたアカウントに依存しているのであれば、あまり論理的ではありません。さらに、分散型アイデンティティエコシステムでは、消費者がオンラインでどのウェブサイトを訪問し、誰と取引したかをより簡単に追跡できるようになります。どの企業が自分の個人データを保有しているかを把握し、希望すればそのアクセス権を取り消すことができるようになります。紙の文書や物理的なカードを共有する代わりに、デジタル文書やデジタルカードを完全にデジタル化し、プライバシーを保護し、監査可能な方法で共有することができるようになります。組織にとっては、個人データは個人の管理下でアイデンティティハブに保存され、組織はユーザーから許可された特定のデータのみにアクセスできるため、GDPR関連のリスクを軽減できる可能性があります。さらに、個人は自分のデータへのアクセス権を取り消すことができるため、組織にとってはGDPR準拠が容易になるとともに、個人にとってはそうした要求が合理化される可能性があります。また、組織は個人から特定のデータが提供されたことを証明する暗号学的な証拠を保有することができるため、組織のGDPR遵守が容易になる可能性があります。

前述のように、デジタルウォレットにはユーザーがインタラクションするためのデジタルエージェントアプリが含まれています。このようなデジタルまたはユーザーエージェントは、ほとんどがオープンソースソフトウェアに基づいています。個人は、営利企業や、おそらく政府機関からユーザーエージェントをダウンロードすることができます。個人は、既存のオープンソースソフトウェアから独自のユーザーエージェントを開発することもできます。概念的には、個人はユーザーエージェントを信頼しなければならず、それは個人の制御下にあるべきです。

分散型アイデンティティがどのように発展していくかを予測することは、その初期段階において非常に困難ですが、現在の傾向として、政府が発行するデジタルアイデンティティによって市民や企業の負担を軽減することに政府が関心を示していることが挙げられます。前例のない世界的なCOVID-19の大流行が追い風となり、政府機関は市民や企業が政府提供のサービスにアクセスできるよう合理化することを強く求めています。また、規制コンプライアンス要件がますます厳しくなり、より優れたユーザー体験と利便性の向上を求めるユーザーの要求が、検証可能なクレデンシャルの交換という形でデジタルアイデンティティに対する需要をさらに押し上げる可能性があります。最後に、検証可能なクレデンシャルは、同じクレデンシャルをオンラインデジタル取引とオフラインの対面取引の両方で提示する必要がある状況で非常に有用である可能性があります。これにより、企業のビジネス効率が向上し、ユーザー体験がより一貫性があり、簡素化されるためです。

@row
## Conclusion

Decentralized identity is a conceptual shift from the way the identity and access management community has been approaching identity in the past, yet it is able to co-exist with the account-based identity model that has existed for decades. Decentralized identity can add a lot of value to transactions that require high assurance of trust to make authorization decisions. If an individual continues to authenticate with a website using a traditional “account”, it does not preclude the individual from having to present verifiable credentials in order to, say, transfer large sums of money to another individual or organization. This offers the possibility to unlock a myriad of new opportunities for digital commerce and enable consumers, employees, and citizens around the world to transact on the web in a more secure, safe, and privacy-preserving manner. It may pave the path for a digital wallet with digital cards, like the way we all use a physical wallet and physical cards today. Verifiable credentials are easy to reason over because many of them will simply be digital representations of the physical cards we already carry in our wallets every day.

We are still at the early days of decentralized identity. It is not a technology that a single company can simply release to the market. It requires both standards as well as collaboration between the private and public sector to have a healthy ecosystem of _issuers_, _holders_, and _verifiers_. When we finally reach critical mass adoption, digital experiences may look and feel much different from the experiences of today. Decentralized identity is an exciting development in the identity space, and it has the potential to offer more trustworthy digital experiences and unlock more value for everyone.

@column
## 結論

分散型アイデンティティは、アイデンティティおよびアクセス管理コミュニティがこれまでおこなってきたアイデンティティのアプローチ方法からの概念的な転換でありながら、何十年も存在してきたアカウントベースのアイデンティティモデルと共存することができます。分散型アイデンティティは、認可の判断に信頼に対して高い保証を必要とする取引に大きな価値を与えることができます。個人が従来の「アカウント」を使用してウェブサイトで認証を続ける場合、例えば、別の個人または組織に大金を送金するために、その個人が検証可能なクレデンシャルを提示しなければならないことを排除するものではありません。これにより、デジタル商取引の新たな機会が無数に生まれ、世界中の消費者、従業員、市民がより安全、安心かつプライバシー保護された方法でウェブ上で取引できるようになる可能性があります。今日、私たちが物理的な財布と物理的なカードを使用しているように、デジタルカードによるデジタルウォレットへの道を切り開くかもしれないのです。検証可能なクレデンシャルは、私たちが毎日財布に入れている物理的なカードをデジタルに置き換えただけのものなので、簡単に推論することができます。

私たちはまだ、分散型アイデンティティの黎明期にいます。これは、一企業が単純に市場にリリースできる技術ではありません。 __Issuer__ 、 __Holder__ 、 __Verifier__ の健全なエコシステムを構築するためには、標準化だけでなく、民間と公共のセクター間の協力が必要です。最終的にクリティカルマスの採用に至った場合、デジタル体験のルック＆フィールは現在とは大きく異なるものになるかもしれません。分散型アイデンティティは、アイデンティティ分野におけるエキサイティングな開発であり、より信頼性の高いデジタル体験を提供し、すべての人にさらなる価値を解放する可能性を持っているのです。

@row
## Change Log

| Date | Change |
| --- | --- |
| 2020-10-30 | V1 published |
| 2022-02-28, 2023-03-31 | Editorial changes only (changed example business names to non-Microsoft specific ones; changed A University to ABC University) |

@row
## Author Bio

<!-- ![Photo of Leo Sorokin, author](/assets/images/idpro_bok/Photo-Leo-Sorokin.jpg) --> Leo Sorokin has over 10+ years of experience in various solution architecture and enterprise architecture roles with large organizations in the financial, manufacturing, and software industries. He is currently a Cloud Solutions Architect at Microsoft helping the largest Canadian organizations adopt cloud technology. Leo has extensive experience with identity, service-oriented architecture, application integration, cloud-native application and hybrid-cloud architecture, as well as security software architecture. Leo is also TOGAF® 9 Certified, a Microsoft Certified Azure Solutions Architect and holds a Computer Science degree from York University. Leo has also taught technology related courses in several educational institutions.

- - -

[^1]:  "Verifiable Credentials Data Model 1.0," W3C Recommendation, World Wide Web Consortium (W3C), 19 November 2019, https://www.w3.org/TR/vc-data-model/.
    
[^2]:  “Decentralized Identifiers (DIDs) v1.0,” W3C Working Draft, World Wide Web Consortium (W3C), 27 October 2020, https://www.w3.org/TR/did-core/.
    
[^3]:  Decentralized Identity Foundation (DIF), \[Online\]. Available: https://identity.foundation/.
