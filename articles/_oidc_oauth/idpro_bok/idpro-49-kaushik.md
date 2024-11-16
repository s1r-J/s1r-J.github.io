---
layout: columns
title: Designing MFA for Humans
permalink: /docs/oidc_oauth/idpro_bok/49
date: 2024-09-09
modify_date: 2024-11-12
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "MFA", "多要素認証", "2FA", "2要素認証"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/49/](https://bok.idpro.org/article/id/49/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article describes how to deploy a thoughtful, consumer-friendly multi-factor authentication (MFA) program that will allow the IAM practitioner to successfully deliver on both the security and usability needs of their authentication systems. The approach is based on a framework of six pillars: determining the viability of different forms of MFA, allowing a multimodal rollout of MFA options, encouraging adoption, supporting MFA across all services and access channels, designing support processes, and creating a trusted environment where MFA can offer additional security to both the consumer and the company.

Keywords: MFA, Multifactor Authentication, 2FA, Two-Factor Authentication, Strong Authentication, SCA, Human-Centric Design, Usability, UX

@column
## 概要

本記事は、IAM実務者が認証システムのセキュリティとユーザビリティの両方のニーズを上手く満たせるような、思慮深く、消費者に優しい多要素認証（MFA）プログラムをデプロイする方法について説明します。このアプローチは6つの柱のフレームワークに基づいています：様々な形式のMFAの実行可能性を判断すること、MFAオプションのマルチモーダルな展開を可能にすること、採用を奨励すること、すべてのサービスとアクセスチャネルでMFAをサポートすること、サポートプロセスを設計すること、MFAが消費者と企業の両方にさらなるセキュリティを提供できるような信頼された環境を構築することです。

Keywords: MFA, 多要素認証, 2FA, 2要素認証, 強力な認証, SCA, 人間中心デザイン, ユーザビリティ, UX

@row
By Nishant Kaushik

© 2020 IDPro, Nishant Kaushik

@row
## **Introduction -** **Designing MFA For Humans**

If every year is The Year of PKI, then when exactly was The Year of Two-Factor Authentication? Was it 2012, when the _epic hacking of Mat Honan_ highlighted just how vulnerable all of our digital lives are? [^1] , [^2] , [^3] , [^4] Was it 2014, when the even higher profile [_iCloud leaks of celebrity photos_](https://en.wikipedia.org/wiki/ICloud_leaks_of_celebrity_photos) pushed various consumer services to rush offering two-factor authentication an option available to users? [^5] Or did it really arrive in 2018, at least for financial institutions, when PSD2 delivered a regulation with some real teeth? [^6] , [^7]

@column
## **導入 -** **人間のためのMFA設計**

毎年がPKIの年なら、2要素認証の年はいつだったのでしょうか？ _Mat Honanの壮大なハッキング事件_ によって、私たちのデジタルライフがいかに脆弱であるかが浮き彫りになった2012年でしょうか？ [^1] , [^2] , [^3] , [^4] [_iCloudによる有名人の写真流出事件_](https://en.wikipedia.org/wiki/ICloud_leaks_of_celebrity_photos) をきっかけに、さまざまな消費者向けサービスが2要素認証の提供を急ぎ、ユーザーが利用できるようになった2014年でしょうか？ [^5] それとも、少なくとも金融機関にとっては、PSD2が実質的な効力を持つ規制が導入された2018年に、本当に到来したのでしょうか？ [^6] , [^7]

@row
### Terminology

*   Adaptive Authentication - Adaptive authentication aims to determine and enforce the authentication level required at any time during a user session - when the session is commenced, during the session when access requirements force a re-evaluation, or when the session token expires. The factors to be used in achieving that authentication level are determined dynamically based on the access control policy governing the resources being accessed, and a variety of environmental conditions and risk factors in effect at that time for that user.
    
*   Account Takeover - Account takeover is a form of identity theft and fraud, where a malicious third party successfully gains access to a user’s account credentials.
    
*   Continuous Authentication - Continuous authentication is a mechanism that uses a variety of signals and measurements to determine during a user session if there is any change in the confidence that it is still the same user that authenticated at the beginning of the session, and trigger an authentication action if there is a drop in confidence.
    
*   PSD2 - PSD2 (the Revised Payment Services Directive, Directive (EU) 2015/2366) is an EU Directive, administered by the European Commission (Directorate General Internal Market) to regulate payment services and payment service providers throughout the European Union (EU) and European Economic Area (EEA). It contains many requirements specifically related to Strong Client Authentication.
    
*   Social Engineering - Social engineering is a method of manipulating people so they give up confidential information, such as passwords or bank information, or grant access to their computer to secretly install malicious software.
    
*   Step-Up Authentication - A method to increase the level of assurance (or confidence) the system has regarding a user’s authentication by issuing one or more additional authentication challenges, usually using factors different from the one(s) used to establish the initial authenticated session. The need for increasing the level of assurance is typically driven by the risk associated with the sensitive resource the user is attempting to access.
    
*   Threat Modeling - Threat modeling is an analysis technique used to help identify threats, attacks, vulnerabilities, and countermeasures that could impact an application or process.
    
*   Two-Factor Authentication (2FA) - A specific case of Multi-Factor Authentication (see: [_IDPro’s Consolidated Terminology_](https://bok.idpro.org/article/id/41/) ) where two factors must be checked to validate a user’s identity.
    

@column
### 用語解説

*   アダプティブ認証 - アダプティブ認証は、ユーザーセッションの開始時、ユーザーセッション中にアクセス要件の再評価が必要になったとき、またはユーザーセッショントークンの有効期限が切れたときなど、ユーザーセッション中にいつでも必要な認証レベルを決定して実施することを目的としています。その認証レベルを達成するために使用される要素は、アクセスされるリソースを管理するアクセス制御ポリシー、およびそのユーザーに対してその時点で有効なさまざまな環境条件とリスク要因に基づいて動的に決定されます。
    
*   アカウントの乗っ取り - アカウントの乗っ取りとは、悪意のある第三者がユーザーのアカウントクレデンシャルへのアクセスに成功することによる、個人情報の盗難や詐欺の一種。
    
*   継続的認証 - 継続的認証とは、さまざまなシグナルと測定値を利用して、ユーザーセッション中に、セッションの最初に認証したユーザーと同じであるという確信に変化があるかどうかを判断し、確信が低下した場合に認証アクションをトリガーするメカニズムです。
    
*   PSD2 - PSD2（欧州決済サービス指令第2版）とは、EUおよびEU経済圏（EEA）の全体の決済サービスおよび決済サービスプロバイダを制御するために、 欧州委員会によって管理されるEU指令です。これには特に強力なクライアント認証に関する様々な制限が含まれています。
    
*   ソーシャルエンジニアリング - ソーシャルエンジニアリングとは、人間を操作してパスワードや銀行口座情報のような機密情報を提供するようにしたり、コンピュータへのアクセス権を許可させて秘密裏に悪意のあるソフトウェアをインストールさせたりするような手法を指します。
    
*   ステップアップ認証 - 一般的に、最初に認証セッションを確立するために利用した要素と異なる要素を利用し、1つ以上の追加の認証チャレンジを発行することでシステムがユーザーの認証に関して有している保証（もしくは信頼度）を高める方法。保証レベルを高める必要性は、通常、ユーザーがアクセスしようとしている機密リソースに関連するリスクによって生じます。
    
*   脅威モデル -  脅威モデルとは、アプリケーションやプロセスに影響を与えうるアイデンティティに対する脅威、攻撃、脆弱性および対策を分析するために利用される分析方法です。    
*   2要素認証（2FA） - ユーザーのアイデンティティを検証するために2つの要素をチェックする必要がある多要素認証（参照：[_IDPro’s Consolidated Terminology_](../41/)）の特定のケース。
    

@row
### The Struggle is Real

Two-factor authentication (2FA) is not new. IAM practitioners are certainly familiar with it through their professional lives (remember keychains full of hardware tokens?), but organizations still struggle with rolling out 2FA to customers. Why?

@column
### 闘争は現実である

2要素認証（2FA）は目新しいものではありません。IAMの実務者は、プロフェッショナルとして生活を通して2要素認証に精通していますが（ハードウェアトークンでいっぱいのキーチェーンを覚えていますか？）、組織は未だに2FAを顧客に展開することに苦労しています。なぜでしょうか？

@row
![A close up of a cell phone Description automatically generated](/assets/images/idpro_bok/image1.jpg)

_Figure 1: Remember carrying these?_

@row
The simple reason is that while employees are a captive audience that will submit to whatever painful, inconvenient mechanism they are forced to adopt (ok, except for mobile device management on their personal phones), customers are a different story. The customer experience matters, and if it is not done well, people are either not going to enable it (when it is optional), will work their way around it, or decide not to engage at all.

For any organization starting down the path of implementing 2FA, it can be confusing and challenging. They find an extensive list of factors spread across the “something you \_\_\_” categories, but little guidance on how to put a good 2FA scheme in place. It’s like getting all the parts in a model kit, but without the instruction manual.

@column
シンプルな理由は、従業員は（個人携帯のモバイルデバイス管理を除けば）苦痛を伴う不便な仕組みであっても強制的に受け入れなければならない囚われの聴衆ですが、顧客は別の話であるからです。カスタマーエクスペリエンスは重要であり、それを損なう場合、人々は2FAを有効にしない（オプションである場合）か、2FAを回避するか、まったく関与しないことを選びます。

どのような組織でも2FAの実装の道を始めることは、ややこしく、挑戦的になる可能性があります。彼らは、「あなたが選べる\_\_\_」カテゴリの要素の広範なリストを見つけますが、良い2FAスキームを導入する方法に関するガイダンスはほとんどありません。取扱説明書もないのに、モデルキットのすべての部品を取得するようなものです。

@row
![An image showing options for various factors: Something You know (Knowledge), including password, personal information KBA, dynamic KBA, PIN, Security Questions KBA); Something you Have (Possession), including TOTP Hard Token, OTP via Email, OTP via SMS, token/cookie, device (mobile), push notification, TOTP soft token, code cards, security keys, cryptographic authentication; Something You Are (inherence) , including Fingerprint, Voice recognition, face recognition.](/assets/images/idpro_bok/image2.jpg)

_Figure 2: A vast menu to choose from_

@row
Most organizations simply end up taking the approach of picking an additional factor that they can simply tack on to the end of their password authentication step, and then call it a day. Unfortunately, that simplified approach falls far short of successfully addressing the problem, resulting in continued breach vectors, brittle infrastructure, and unsatisfied customers.

@column
ほとんどの組織は、パスワード認証の最後に追加要素を選んで、それで終わりというアプローチを取っています。残念ながら、このような単純なアプローチでは、問題解決には程遠く、侵入経路の拡大、インフラの脆弱化、顧客の満足度の低下となります。

@row
### Thinking in Factors

Multi-factor authentication (MFA) aside, the goal of any authentication framework is to validate that the returning person (or thing) is the same one that the system saw last time, _to the required level of assurance_ . That last part is what makes authentication difficult to implement well. Measuring the assurance of authentication is subjective, and cannot be normalized across organizations, industries, or end-user communities since a critical element in evaluating the assurance of authentication is trying to determine how easy or likely it is for an adversarial party to get around it. Determining this correctly requires doing threat modeling and risk analysis (more on that later), and then translating this into how to authenticate in different contexts.

This requirement for assurance is where factors of authentication become relevant. Factors make the abstract concrete by giving the authentication framework something tangible to evaluate, invoke, and measure. An important evolution that has happened is the realization that _not all factors are created equal_ . This realization has expanded the kind of factors that can be used, while also creating the understanding that the same level of authentication assurance can be achieved using different sets of factors that are not numerically the same (i.e., one set of 2 factors can achieve the same level of assurance as a different set of 4 factors). The requirements around assurance are helping drive the discussion away from 2FA and towards **MFA** .

One important consideration that overshadows all of this is the nature of the factors and their impact on the user experience. When authentication factors translate into explicit challenges (or “active” factors) that an end-user has to engage with (as opposed to “passive” factors that work silently in the background), then the impact on usability will drive organizations to try and reduce the number of factors used in the authentication process. One way that they can compensate is to invoke additional (active) factors when the risk associated with the access request is elevated (often called **step-up authentication** or **adaptive authentication** ). An even more refined approach to evaluating authentication assurance and risk is **continuous authentication** , which recognizes that the assurance level degrades over the life of the user session given how identity or access information may change during the session, and that passive factors can be used to constantly measure any changes or degradation to that assurance level, and determine if step-up authentication is required to bump the assurance level back up.

In all of these approaches, the factors of authentication are the control vector that allows the authentication framework to measure, achieve, and maintain the assurance level of the authenticated session as required by the business.

@column
### 要素について考える

多要素認証（MFA）はともかく、認証のフレームワークの目標は、戻ってきた人（または物）が、システムが前回見たものと同じものであることを、 __必要な保証レベルで__ 検証することです。この「必要な保証レベルで」の部分が、認証をうまく実装することを難しくしています。認証の保証を評価するための重要な要素は、攻撃者が認証を回避することがいかに容易であるか、または可能性が高いかを判断することであるため、認証の保証の測定は主観的であり、組織、業界またはエンドユーザーのコミュニティ間で正規化することができません。これを正しく判断するには、脅威のモデリングとリスク分析（詳細は後述）をおこない、これをさまざまなコンテキストでの認証方法に反映させる必要があります。

この保証の要件は、認証の要素が関連します。要素は、認証フレームワークに評価、呼び出しおよび測定できる具体的なものを与えることで、抽象的なものを具体化します。重要な進化として、 __すべての要素が同じであるわけではない__ という認識を持つことです。この認識により、利用できる要素の種類が拡大し、また、数値的に同じではない異なる要素のセットを利用して、同じレベルの認証保証を達成できることが理解できるようになります（たとえば、1セットの2要素で異なるセットの4要素と同じレベルの保証を達成することができます）。保証に関する要件は、2FAから **MFA** に向けての議論を促進するための助けになります。

これらすべてを覆い隠す重要な考慮事項の1つは、認証要素の性質と、それがユーザーエクスペリエンスに与える影響です。認証要素が、エンドユーザーが関与しなければならない明示的な課題（または「アクティブ」要素）に変換される場合（バックグラウンドで静かに機能する「パッシブ」要素とは対照的）、ユーザビリティへの影響により、組織は認証プロセスで使用する要素の数を減らそうとします。それを補償する方法の1つは、アクセス要求に関連するリスクが高まったときに、追加の（アクティブな）要素を呼び出すことです（しばしば **ステップアップ認証** または **アダプティブ認証** と呼ばれます）。認証の保証とリスクを評価するためのさらに洗練されたアプローチは**継続的な認証** であり、これはセッション中にアイデンティティやアクセス情報が変化する可能性があるため、ユーザーセッションの生存期間中に保証レベルが低下することを認識し、パッシブ要素を使用して保証レベルの変化または低下を常に測定し、保証レベルを上げるためにステップアップ認証が必要かどうかを判断できるようにするものです。

これらのすべてのアプローチにおいて、認証の要素は、認証フレームワークがビジネスの要求に応じて認証されたセッションの保証レベルを測定、達成および維持できるようにする制御ベクトルです。

@row
## **A Framework for Designing Your MFA Schema**

MFA has become an imperative across industries, user bases and threat models, and the challenges and practices described below apply equally to both small and large organizations. It lays out a basic framework to build an MFA program that should prove useful to product teams, employees, and clients. This framework is built on six pillars that address the challenge of balancing security, usability and privacy.

@column
## **MFA計画を設計するためのフレームワーク**

MFAは業界、ユーザー基盤および脅威モデルを超えて必須となっており、以下に説明する課題とプラクティスは、小規模組織と大規模組織の両方に等しく適用されます。ここでは、製品チーム、従業員およびクライアントにとって有用であることが証明されるMFAプログラムを構築するための基本的なフレームワークについて説明します。フレームワークは、セキュリティ、ユーザビリティ、プライバシーのバランスを取るという課題に取り組む6つの柱で構成されています。

@row
### 1\. Viability

The first pillar of that framework is **Viability** . When going through the long list of factors possible, implementors and decision makers must assess which of those factors is viable for their MFA scheme. Assessing viability has multiple considerations:

*   User Acceptance: Think of the people that make up your user base, and what factors they’d be willing to accept and use.
    
*   Cost: Think about the cost of the factor, and whether that is a cost that the business will bear, or the customer will bear. Hardware tokens are great, but expensive. Is the business buying it for their customers, or are they expecting the customer to buy it themselves?
    
*   Threat Model: Consider the threat model associated with the factor. A USB device can be a very secure authentication factor, where the user has to plug the key into a port on their desktop in order to authenticate. But research studies have shown that people will often leave them plugged into their desktop even when they leave the office, virtually negating its assurance as a possession factor. Discussing this in detail is out of scope for this article, but do note that there is a need to introduce threat modeling as a core discipline in identity management.
    
*   Effectiveness: Consider the effectiveness of the factor. For example: security questions, a widely deployed form of MFA, are universally acknowledged as being ineffective in this age of public social media profiles and social engineering threats.
    
*   Regulatory Compliance: In many cases, regulatory compliance can enter the equation, since regulators are increasingly rendering opinions on which factors are acceptable for different industries.
    

@column
### 1\. 実行可能性

フレームワークの最初の柱は **実行可能性** です。可能性のある要素の長いリストを検討する場合、実装者と意思決定者はこれらの要素のうちのどれがMFA計画に適しているかを評価する必要があります。実行可能性の評価には複数の考慮事項があります：

*   ユーザーの受容：あなたのユーザー基盤を構成している人々と、彼らがどのような要素を喜んで受け入れ、利用するかを考えましょう。
    
*   コスト：要素のコスト、そしてれが企業が負担するコストなのか、顧客が負担するコストなのかを考えましょう。ハードウェアトークンは素晴らしいですが、高価です。それを顧客のために企業側が購入しますか、それとも顧客が購入してくれることを期待しますか？
    
*   脅威モデル：要素に関連する脅威モデルについて検証しましょう。ユーザーは認証するためにUSBデバイスをデスクトップのポートに差し込む必要があるため、USBデバイスは非常にセキュアな認証要素です。しかし、調査研究によると、ユーザーは外出先でもUSBデバイスをデスクトップに接続したままにしていることが多く、所持する要素としての安全性は事実上否定されています。この点について詳しく説明することはこの記事の範囲外ですが、脅威のモデリングをアイデンティティ管理の中心分野として取り込む必要性があることに留意してください。    
    
*   有効性：要素の有効性を検討しましょう。例えば、MFAの一形態として広く普及している秘密の質問は、ソーシャルメディアのプロフィールが公開され、ソーシャルエンジニアリングの脅威があるこの時代には効果がないことは誰もが認めるところです。
    
*   法規制の遵守：多くの場合、法規制の遵守が条件に含まれることがあります。なぜなら、規制当局が業界ごとにどの要素が許容されるかについて意見を述べることが多くなっている￥ためです。
    

@row
### 2\. Multimodal

The second pillar of the framework is **Multimodal** . When implementing 2FA, the goal is to have each user employ at least two factors when authenticating. However, that does not mean that the business should only support two factors. Not all factors work for all users, and when a business is trying to increase the number of customers turning on MFA, they must offer options (i.e., be multimodal) that work with their vast and diverse user base. The idea that they can find two factors that work for everyone leads them to a least common denominator approach, and that’s how so many industries have ended up with SMS OTP as the de facto “standard” in MFA, and a weakening of the security model. [^8]

@column
### 2\. マルチモーダル

フレームワークの2つ目の柱は、 **マルチモーダル** です。2FAを実装する場合、各ユーザーが認証時に少なくとも2つの要素を採用することが目標となります。しかし、だからといって、2つの要素しかサポートしてはいけないというわけではありません。すべての要素がすべてのユーザーに有効なわけではなく、企業がMFAを有効にする顧客数を増やそうとする場合、膨大で多様なユーザー基盤に対応するオプションを提供する（つまり、マルチモーダルにする）必要があります。すべての人に有用な2つの要素を見つけることができるという考えは、最小公倍数のアプローチにつながり、その結果、非常に多くの業界でSMS OTPがMFAの事実上の「標準」となり、セキュリティモデルが弱体化することになったのです。 [^8]

@row
![A hand holding a cellphone Description automatically generated](/assets/images/idpro_bok/image3.jpg)

_Figure 3: Different strokes for different folks_

@row
Offering choice allows a business to address the varying capabilities, preferences, and circumstances of their end-users, and avoid a “one size fits all” approach that alienates customers and often weakens security.

Being multimodal will necessarily require the authentication platform become adaptive, not just to risks, but also to user (cap)abilities. This ability to adapt will require the authentication service/platform/provider to create intelligent user flows – a concept commonly being referred to as orchestration. [^9]

@column
選択肢を提供することで、企業はエンドユーザーのさまざまな能力、好み、状況に対応することができ、顧客を遠ざけ、しばしばセキュリティを弱めることになる「ワンサイズ・フィット・オール」のアプローチを回避することができます。

マルチモーダルであるためには、認証プラットフォームが、リスクだけでなく、ユーザーの能力にも適応できるようになる必要があります。この適応能力により、認証サービス／プラットフォーム／プロバイダーは、インテリジェントなユーザーフロー（一般にオーケストレーションと呼ばれる概念 [^9] ）を作成する必要があります。

@row
### 3\. Adoption

The third pillar is the one that is the most misunderstood - **Adoption** . The reality is that unlike enterprise environments where the business can mandate MFA, the customer environment requires a business to convince their end-users to start using MFA. While acceptance for this pattern is growing, in general this is easier said than done. [^10]

Organizations need to make UX research a core element of their IAM program, especially as they design their MFA scheme. It is a critical and foundational element to creating the right set of messaging, training, and incentive components that the business will have to incorporate into their rollout plan to drive adoption. [^11]

@column
### 3\. Adoption

3つ目の柱は最も誤解されているもので、 **導入** です。現実には、企業がMFAを義務付けることができるエンタープライズ環境とは異なり、コンシューマー環境では企業がエンドユーザーにMFAを利用開始するよう説得する必要があります。このパターンは受け入れられつつありますが、一般的には言うのは簡単ですが、実行するのは難しいです。 [^10]

組織は、特にMFA計画を策定する際に、UX 調査をIAMプログラムのコア要素に実施する必要があります。これは、企業が採用を促進するためにロールアウト計画に組み込む必要がある、適切なメッセージ、トレーニング、およびインセンティブコンポーネントのセットを作成するために重要かつ基本的な部分です。 [^11]

@row
### 4\. Omnichannel

An overlooked pillar when designing MFA is **Omnichannel** . Businesses have often failed to recognize that MFA should not apply just to their web or mobile channels; they must be deployed across all their customer-facing channels. This ties back to the pillar on multimodality. Businesses are engaging with customers and partners across many channels – web, mobile, call center, in-person, chat, smart home assistants, and more - and each channel usually brings a completely different way of authenticating the end-user.

This inconsistency frustrates end-users, creates a headache for customer-facing staff and IT staff, and delights bad actors. Attackers look for the weakest link across those channels, and go after that one, exploiting not only the weakness of the channel but also the frustration that customers and employees feel. The result is rampant account takeover attacks and fraud. [Watch this video](https://youtu.be/fHhNWAKw0bY) of a classic social engineering attack that exploits weaknesses in the customer service authentication process to take over an account.

Businesses today have a pressing imperative to transition away from an inconsistent hodge-podge of varying authentication models and bring some consistency and equality of security levels across their various channels.

@column
### 4\. オムニチャネル

MFAを設計する際に見落とされがちな柱は、 **オムニチャネル** です。 多くの企業は、MFAをWebチャネルやモバイルチャネルだけに適用すべきではないことを認識していません；それらは、顧客向けのすべてのチャネルに展開する必要があります。これは、マルチモーダリティの柱に関連します。企業は、Web、モバイル、コールセンター、対面、チャット、スマートホームアシスタントなど、さまざまなチャネルで顧客やパートナーとやり取りしており、通常、チャネルごとにまったく異なる方法でエンドユーザーを認証しています。

この不一致は、エンドユーザーを苛立たせ、顧客対応スタッフとITスタッフを悩ませ、悪意のある人物を喜ばせます。攻撃者は、これらのチャネル全体で最も弱いリンクを探し、チャネルの弱点だけでなく、顧客や従業員が感じるフラストレーションも悪用して、そのリンクを追跡します。その結果、アカウント乗っ取り攻撃と詐欺が蔓延しています。顧客サービス認証プロセスの弱点を悪用してアカウントを乗っ取る、典型的なソーシャルエンジニアリング攻撃の[このビデオをご視聴ください](https://youtu.be/fHhNWAKw0bY)。

今日の企業は、さまざまな認証モデルの一貫性のない寄せ集めから移行し、さまざまなチャネルにわたって一定の一貫性とセキュリティレベルの平等をもたらすことが急務となっています。

@row
### 5\. Processes

The fifth pillar of the framework is the one that most organizations do not pay enough attention to: **Processes** . Enabling and maintaining MFA for individual customers involves many different processes, each of which needs to be properly designed:

*   **Enrollment** : If the enrollment process is flawed, the assurance of your MFA is suspect from the very beginning. Many organizations will allow users to set up their second factor after they have authenticated solely using their first, and that is a massive vulnerability point in the overall security scheme.
    
*   **Backup / Alternate** : No authentication factor is immune from loss or destruction, so the business has to think about ways to not only allow, but proactively encourage, customers to set up additional authenticators as backups. And those backups must have the same strength as the primary; otherwise, this creates a backdoor for attackers.
    
*   **Escape Paths** : Not all authentication factors are always available for use, and the alternate mechanism may not be available. Consider what happens to push notification-based authentication for someone working in a part of the building, or on a plane, where they get no signal. It is not out of the question that they left their FIDO security key that they use as a backup safely locked in their office drawer. Locking them out under those circumstances can prove to be hugely problematic and result in workarounds that open up exploitation vectors. Escape paths may not be appropriate in all circumstances; consider carefully whether they should be designed into your system.
    
*   **Recovery** : Consider how the business will support an end-user that has lost their authentication factor(s), so that they are not faced with the dire consequence of being permanently locked out (think of all the horror stories of bitcoin wallets irrecoverably locked up because their owner lost the hardware token containing their private key). Recovery paths must also be designed properly to avoid having them turn into backdoors for bad actors. _Never_ use an authentication factor as the verification factor for also doing recovery (e.g., every service that uses SMS OTP as a second factor of authentication, and also as a way of resetting a forgotten password). This effectively creates a backdoor that turns a 2FA scheme into a one-factor authentication scheme.
    
*   **Deprovisioning** : Of course, the business must to consider how to invalidate a factor that is no longer available to the customer, or is no longer acceptable to the business because of vulnerabilities or issues discovered in it (whether it be at an individual level or system wide).
    

Importantly, escape paths and recovery flows need to be treated as _exceptions_ with higher risks associated with them. That implies increasing the risk evaluation and security of those flows, which often means adding friction. It is important to remember that in these circumstances, customers will frequently be understanding of the increased scrutiny in those paths (provided the business offers adequate explanations). One of the techniques emerging for these exception flows is the use of identity verification tools (e.g., document-based identity proofing) in these scenarios.

@column
### 5\. プロセス

フレームワークの5つ目の柱は、ほとんどの組織が十分に注意を払っていない **プロセス** です。個々の顧客のMFAを有効にして維持するには、さまざまなプロセスが必要であり、それぞれを適切に設計する必要があります：

*   **登録**：登録プロセスに不備があると、最初からMFAの保証度が疑わしくなります。多くの組織は、ユーザーが最初の要素のみを使用して認証した後、2番目の要素を設定することを許可します。これは、セキュリティスキーム全体における大きな脆弱点です。
    
*   **バックアップ / 代替** :  損失や破壊の影響を受けない認証要素はないため、企業は顧客が追加のオーセンティケーターをバックアップとしてセットアップすることを許可するだけでなく、積極的に奨励する方法を検討する必要があります。これらのバックアップは、プライマリと同じ強度を持つ必要があります；そうしないと、攻撃者のバックドアが作られることになります。
    
*   **エスケープパス**：すべての認証要素が常に使用できるわけではなく、代替メカニズムが使用できない場合があります。建物の一部や飛行機の中のように信号が届かない場所で働いている人にプッシュ通知ベースの認証を適用するとどうなるかを考えてみてください。彼らがバックアップとして使用するFIDOセキュリティキーをオフィスの引き出しに安全に保管したままにしておくことも考えられます。このような状況で彼らを締め出すと、非常に問題が大きくなり、悪用のベクトルを開く回避策をもたらす可能性があります. エスケープパスは、すべての状況で適切であるとは限りません；それらをシステムに組み込む必要があるかどうかを慎重に検討してください。
    
*   **リカバリ**：認証要素を失ったエンドユーザーをビジネスがどのようにサポートするかを検討し、永久にロックアウトされるという悲惨な結果に直面しないようにします（ビットコインウォレットが、所有者が秘密鍵を含むハードウェアトークンを紛失したためにリカバリ不能な状態でロックされたという恐ろしい話を考えてみてください）。リカバリパスも適切に設計して、悪意のある人物のバックドアにならないようにしなければなりません。リカバリを実行するために検証要素として認証要素を使用 __しない__ でください (たとえば、SMS OTPを認証の2番目の要素として使用し、忘れたパスワードをリセットする方法としても使用するすべてのサービス)。これにより、2FAスキームを1要素認証スキームに変えるバックドアが効果的に作成されます。
    
*   **デプロビジョニング**：当然、企業は、脆弱性や問題が発見された（個人レベルであろうとシステム全体であろうと）ために、顧客が利用できなくなった、または企業にとって受け入れられなくなった要素を無効にする方法を検討する必要があります。
    

重要なのは、エスケープパスとリカバリフローは、リスクが高い　__例外__ として扱う必要があることです。このことは、これらのフローのリスク評価とセキュリティを強化することを意味し、多くの場合、摩擦が増えることを意味します。このような状況では、（ビジネスが適切な説明を提供している場合、）多くの顧客はこれらの経路で検証が強化されていることを理解していることを認識することが重要です。これら例外フローのために出現した手法の1つは、これらのシナリオでアイデンティティ検証ツール（ドキュメントベースの身元確認など）を使用することです。

@row
### 6\. Trusted Environment

The sixth and final pillar of the framework is establishing a **Trusted Environment** within which to execute MFA. It will not matter how good or strong a business’s factors of authentication are if the environment within which those factors are being accepted, stored, transmitted, and evaluated is compromised, allowing them to be stolen, manipulated, or replayed. Keyloggers that capture secrets, malware apps that intercept SMS codes or steal keys, malicious WiFi, reverse proxies, and rogue cell towers that capture and replay credentials or tokens – threats like these reduce the effectiveness of MFA and degrade organizational trust in those factors. All multi-factor authentication projects must be part of a larger security program that enforces defense-in-depth (or, to use the industry term du jour, **zero-trust security** ) to not only leverage the factors of authentication, but also look at the health of the devices and hardware being used and the networks being relied upon, as well as other signals of risk, in order to build trust in (hopefully) the simple act of authenticating your customer.

@column
### 6\. 信頼された環境

フレームワークの6つ目、そして最後の柱は、MFAを実行するための **信頼された環境** の確立です。認証要素が受け入れられ、保存され、伝送され、評価される環境が侵害され、認証要素が盗まれたり、操作されたり、リプレイされたりする場合には、企業の認証要素がいかに優れていても、あるいは強くても意味がありません。機密情報を取得するキーロガー、SMSコードを傍受したりキーを盗んだりするマルウェアアプリ、認証情報やトークンを取得・リプレイする悪意のあるWiFi、リバースプロキシ、不正なセルタワーなど、こうした脅威はMFAの効果を低下させ、これらの要素に対する組織の信頼を低下させます。全ての多要素認証のプロジェクトは、多重防衛（業界用語でいうところの **ゼロトラストセキュリティ** ）を実施する大規模なセキュリティプログラムの一部でなければならず、認証要素を活用するだけでなく、使用しているデバイスやハードウェア、依存しているネットワーク、その他のリスクシグナルを監視し、顧客の認証という単純な行為に対する信頼を（できれば）構築します。

@row
## Conclusion

This framework offers guidance for rolling out a strong and usable MFA service for their users. The considerations of factor viability, multimodal support, adoption rates, omnichannel applicability, and the infrastructure that guarantees a trusted environment, applies to any organization in any sector, and should be considered at every stage -- designing, building, and rollout – of any MFA program.

May all your authentications be strong, and all your customers be happy, engaged, and protected.

\[This article is adapted from my talks at EIC, Identiverse, and Identity Week. You can watch the Identiverse talk [_here_](https://youtu.be/8gUNPMDWZRo) .\]

@column
## 結論

このフレームワークは、ユーザーにとって強力で使いやすいMFAサービスをロールアウトするためのガイダンスを提供します。要素の実行可能性、マルチモーダル対応、導入、オムニチャネルへの適用性、信頼できる環境を保証するインフラなどの考慮事項は、あらゆる分野のあらゆる組織に適用され、あらゆるMFAプログラムの設計、構築、展開の各段階で検討されるべきものです。

すべての認証が強固なものとなり、すべての顧客が満足し、関与し、保護されることを祈ります。

\[この記事はEIC、Identiverse、Identity Weekでの私の講演から抜粋したものです。Identiverseでの講演は[_こちら_](https://youtu.be/8gUNPMDWZRo)から見ることができます。\]

@row
## Author Bio

<!-- ![A person wearing glasses and looking at the camera Description automatically generated](/assets/images/idpro_bok/image4.jpg) --> Nishant Kaushik is the CTO of Uniken, the first security platform that tightly integrates identity, authentication and channel security. He brings over 15 years of experience in the identity management industry architecting and delivering market leading products, with stints at Thor Technologies, Oracle, SCUID and CA Technologies. His current role allows him to focus on his latest passion of solving the user experience problem in delivering exceptional security by leveraging identity. Nishant is a recognized thought leader and notorious photoshopper of the identirati, regularly speaking at conferences and provoking discussion through his blog (blog.talkingidentity.com) and on twitter (@NishantK).

_**Nishant Kaushik**_

_**CTO, Uniken Inc.**_

- - -

[^1]:  Berinato, Scott, “Only Mostly Dead,” CSO Online, 23 May 2002, https://www.csoonline.com/article/2113027/only-mostly-dead.html. 
    
[^2]:  Stiennon, Richard, “The new Entrust: is 2011 the year of PKI?” Forbes, 9 May 2011, https://www.forbes.com/sites/richardstiennon/2011/05/09/the-new-entrust-is-2011-the-year-of-pki/#2bdb8f5a171e. 
    
[^3]:  Hils, Adam, “2015 Network Security Predictions: 8 Things That Won’t Happen,” blog, Gartner, 29 December 2014, https://blogs.gartner.com/adam-hils/2015-8-network-security-trends-that-wont-gain-t-raction/. 
    
[^4]:  Honan, Matt, “How Apple and Amazon Security Flas Led to My Epic Hacking,” Wired, 6 August 2012, https://www.wired.com/2012/08/apple-amazon-mat-honan-hacking/. 
    
[^5]:  Wikipedia contributors, "ICloud leaks of celebrity photos," _Wikipedia, The Free Encyclopedia,_ [_https://en.wikipedia.org/w/index.php?title=ICloud\_leaks\_of\_celebrity\_photos&oldid=974755004_](https://en.wikipedia.org/w/index.php?title=ICloud_leaks_of_celebrity_photos&oldid=974755004) (accessed September 21, 2020). 
    
[^6]:  __[Directive 2015/2366/EU](http://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32015L2366) of the European Parliament and of the Council of 25 November 2015 on payment services in the internal market, amending Directives 2002/65/EC, 2009/110/EC and 2013/36/EU and Regulation (EU) No 1093/2010, and repealing Directive 2007/64/EC,__ European Commission, 12 January 2016, https://ec.europa.eu/info/law/payment-services-psd-2-directive-eu-2015-2366/law-details\_en. 
    
[^7]:  Constantin, Lucian, “What is PSD2? And how will it impact the payments processing industry,” CSO Online, 13 September 2019, https://www.csoonline.com/article/3390538/what-is-psd2-and-how-it-will-impact-the-payments-processing-industry.html. 
    
[^8]:  Suau, Roxanne, “SMS OTP Authentication: Not As Safe As You May Think,” blog, Pradeo, 17 February 2020, https://blog.pradeo.com/sms-otp-authentication-not-safe. 
    
[^9]:  Goldberg, Joel, “Workflow Orchestration: An Introduction,” DevOps Blog, BMC, 15 October 2019, [https://www.bmc.com/blogs/workflow-orchestration/](https://www.bmc.com/blogs/workflow-orchestration/) . 
    
[^10]:  Camp, L. Jean, Sanchari Das, “Studies of 2FA, Why Johnny Can’t Use 2FA and How We Can Change That,” RSA Conference2019, video session, 12 February 2020, [https://www.youtube.com/watch?v=UH9yWvvp4k8](https://www.youtube.com/watch?v=UH9yWvvp4k8) . 
    
[^11]:  Das, Sianchari, Andrew Dingman, L. Jean Camp, “Why Johnny Doesn’t Use Two Factor: A Two-Phase Usability Study of the FIDO U2F Security Key,”in _2018 International Conference on Financial Cryptography and Data Security (FC),_ 2018, [https://fc18.ifca.ai/preproceedings/111.pdf](https://fc18.ifca.ai/preproceedings/111.pdf) . 
