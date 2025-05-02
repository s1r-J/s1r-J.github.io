---
layout: columns
title: Ethics and Digital Identity
permalink: /docs/oidc_oauth/idpro_bok/104
date: 2024-09-09
modify_date: 2025-04-20
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "デジタルアイデンティティ", "倫理", "価値観", "哲学"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/104/](https://bok.idpro.org/article/id/104/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article describes how identity professionals can relate their work to ethics and how imperative it is to ensure that ethical discussions and value conversations are conducted in the field of identity and access management. By providing a general introduction to ethics and what ethical theories are, this article lays the foundation for an understanding and clear perspective on the topic of ethics that can seem so far away from technology. But technology, although not good or bad, is never neutral and most often value-laden. And when we assign identity we assign power. Identity and access impact various values and these are described in this article as well, again building the bridge between ethics and technology. The article concludes with methods to apply ethics in everyday work as an identity professional.

Keywords: digital identity, ethics, values, philosophy, design

@column
## 概要

この記事では、アイデンティティ専門家が自分の仕事を倫理とどのように関連付けることができるか、またアイデンティティとアクセス管理の分野で倫理的な議論と価値観の対話を実施することがいかに不可欠であるかを解説します。本記事では倫理および倫理理論とは何かについて一般的な入門を提供することで、技術から遠く離れているようにみえる倫理の話題について理解し、明確な視点を持つための基礎を築きます。しかし、テクノロジーは良いものでも悪いものでもないが、決して中立的なものではなく、多くの場合、価値観をともなっています。そして、私たちがアイデンティティを割り当てるとき、私たちは権力を割り当てることになります。アイデンティティとアクセスは様々な価値観に影響を与え、これについても記事で紹介しており、再び倫理とテクノロジーの架け橋となっています。記事は、アイデンティティの専門家として日々の仕事に倫理を適用するための方法についてで締めくくっています。

**Keywords:** デジタルアイデンティティ, 倫理, 価値観, 哲学, 設計

@row
By Henk Marsman

© 2024 IDPro, Henk Marsman

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code)._

@row
## Introduction

Technology has impacted every day since the beginning of human history. It has changed power balances, helped to promote or restrict freedom of speech, and either advanced or reduced human rights. For example, the printing press changed society by providing knowledge to anyone who could read. If it is true that “knowledge is power” then putting information into the hands of more people changed the power balance. However, information was not equitably distributed and there were fewer benefit to those who could not read. Furthermore, not everything that was written was truthful (you heard it here first!). Technological advancements create opportunities not only for those who mean well, but also for those who mean to cause harm.

Digital technology - and specifically digital identity (and IAM) - are evolving rapidly. These developments do not just affect how organizations manage their workforce (identity and access), their customer interactions (customer authentication), or how identity providers offer federation services. Globally, nations are developing digital identity solutions for their national identification schemes. In Europe, for example, there is the amended eIDAS Regulation that stipulates every EU citizen to be able to use a digital identity wallet by 2026 (note: these are member state digital wallets and identities – there will not be a European identity or wallet). In other regions, biometrically-linked national identities are more commonly stored in centralized databases. Meanwhile, some nations reject the notion of a mandatory federally-issued identity altogether – they may be more inclined to follow the progress of ISO’s Mobile Driver’s License (MDL) set of standards.

Are these developments good? Should we even ask that ourselves that question? Yes we should. Why? Because technically perfect solutions can lead to harm when they are used in practice. A very good facial recognition solution that is used to recognize users’ emotions and deliver better service may also be used for surveillance systems or to exert undue influence on a population. It it is our professional responsibility to give these risks an appropriate level of attention. This is ethics.

Ethics is time spent on thinking about and talking about the impact of something and whether it is good or bad. Ethics is about what we value, and whether this has been adequately addressed in the design, roll-out, or operation of (in the case of IDPro members) a digital identity solution.

Identity professionals need to include ethical discussions and value conversations in their work, not just as a moral imperative but also because this leads to better solutions. This article lays out the foundations of ethical thought, proposes and defines a set of values for Digital Identity practitioners, and some high-level tools for engaging in ethical discussion. A second article, “Ethics for Digital Identity and Identity-Driven Algorithms” by Mike Kiser, delves into ethics related to Digital Identity and Algorithms and offers a deeper look at the Ethical Canvas tool for practitioners.[^1]

@column
## 導入

人類の歴史が始まって以来、テクノロジーは毎日に影響を与えてきました。テクノロジーはパワーバランスを変え、言論の自由を促進したり制限したりするのに役立ち、人権を進歩させたり後退させたりしてきました。例えば、印刷機は文字を読むことができる人々に知識を与え、社会を変えました。「知は力なり」が真実ならば、情報をより多くの人の手に渡すことでパワーバランスは変化しました。しかし、情報は平等には分配されず、文字を読めない人々への恩恵は少なかったです。さらに、書かれていることがすべて真実だったわけではありません（ここで初めて聞いた！）。テクノロジーの進歩は、善意の人々だけでなく、危害を加えようとする人々にも機会を与えます。

デジタル技術、特にデジタル・アイデンティティ（およびIAM）は急速に進化していまし。こうした発展は、組織が従業員を管理する方法（アイデンティティとアクセス）、顧客とやり取りする方法（顧客認証）またはアイデンティティ・プロバイダーがフェデレーション・サービスを提供する方法に影響を与えるだけではありません。世界的に、各国は国家アイデンティティ・スキーム用のデジタル・アイデンティティ・ソリューションを開発しています。たとえば欧州では、改正eIDAS規則があり、2026年までにすべてのEU市民がデジタル・アイデンティティ・ウォレットを使用できるようにすることを規定しています（注：これらは加盟国のデジタル・ウォレットおよびアイデンティティであり、欧州のアイデンティティやウォレットは存在しません）。他の地域では、バイオメトリクスに紐づいた国民アイデンティティは中央集中型のデータベースに保管されるのが一般的です。一方、連邦政府発行の強制的なアイデンティティという概念を完全に拒否する国もあります。それらの国々は、ISOのモバイル運転免許証（MDL）の標準仕様の発展に従う傾向が強いかもしれません。

これらの発展は良いことなのでしょうか？そう自問すべきでしょうか？そうです、自問すべきです。なぜでしょう？技術的に完璧なソリューションでも、実際に使われると害になることがあるからです。ユーザーの感情を認識し、より良いサービスを提供するために使用される非常に優れた顔認識ソリューションも、監視システムに使用されたり、集団に不当な影響を及ぼすために使用されたりする可能性があります。このようなリスクに適切なレベルで注意を払うことは、私たちの専門家としての責任です。これが倫理です。

倫理とは、何かが及ぼす影響やそれが良いことなのか悪いことなのかについて考え、話し合うことに費やされる時間です。倫理とは、私たちが何を重視するかということであり、（IDProメンバーの場合）デジタ ル・アイデンティティ・ソリューションの設計、デプロイまたは運用においてこれが適切に対処されているかどうかということです。

アイデンティティの専門家は、倫理的な議論と価値観の対話を業務に含める必要があります。これは、道徳的な要請としてだけでなく、より良い解決策につながるからです。本稿では、倫理的思考の基本を示し、デジタル・アイデンティティ実務者のための一連の価値観と倫理的議論に参加するための高レベルのツールを提案し、定義します。Mike Kiserによる2番目の記事「Ethics for Digital Identity and Identity-Driven Algorithms」では、デジタル・アイデンティティとアルゴリズムに関連する倫理を掘り下げ、実務者向けのツール「Ethical Canvas」を詳しく解説しています。 [^1]

@row
## Ethics vs Law

Ethics and law are not the same – and despite some assertions by vendors out there, a solution cannot be “ethically compliant.” The realm of law is where, depending on locality, polity and legal system, clear (well, ideally clear) rules are enshrined regarding what is acceptable, unacceptable, and what penalties apply to unacceptable behaviour. Law is continually updated because of changes in the world - especially changes to what we value. For example: long time ago voting by women was not valued, now it is, so the law has changed. Our laws are a result of ethics, but that statement cannot be reversed. Being lawful does _not_ automatically mean being ethical: upholding the law and staying within the boundaries of the law can still be combined with morally despicable behaviour.

The realm of ethics involves discussion and thought about what is right and wrong, and why these are right and why those are wrong. While some ethical paradigms, namely Duty Ethics (which will be explored below), may seem law-like, it is still the moral discussion that is more important than the rule itself.

As stated above, laws often result from the practice of ethics: when society reaches a normative conclusion that something is ethically right or wrong, it may be enshrined in law, regulations, trust frameworks, contracts, or other institutional controls. For example, it is not uncommon for individuals that hold a degree, obtain an accreditation or join an association to underwrite a statement that they will conduct themselves professionally including applying ethical guidelines in their work, for example for software engineers in Canada that are member of the order of engineers.[^2] IDPro also has this in their value statement.[^3]

@column
## 倫理と法律

倫理と法律は同じではありません。また、ベンダーの主張にもかかわらず、ソリューションが「倫理に準拠している」ということはありえません。法律の領域は、地域、政治形態、法体系によって何が許容され、何が許容されないか、許容されない行動にはどのような罰則が適用されるかについて、明確な（まあ、理想的には明確な）ルールが定められています。法律は、世の中の変化、特に私たちの価値観の変化に応じて絶えず更新されます。例えば、一昔前は女性による投票が評価されていませんでしたが、今では評価されています。私たちの法律は倫理の結果ですが、この言葉は逆向きにはできない。法を守り、法の枠内にとどまることは、道徳的に卑劣な行為と結びつく可能性があります。

倫理の領域では、何が正しくて何が間違っているのか、なぜそれが正しくてなぜそれが間違っているのかについて議論し、考えます。倫理的なパラダイム、すなわち義務倫理（これについては後述します）の中には、法律のように見えますが、それでも重要なのはルールそのものよりも道徳的な議論です。

上述のように、法律はしばしば倫理の実践から生まれます：社会が、あることが倫理的に正しいあるいは間違っているという規範的結論に達したとき、それは法律、規制、トラスト・フレームワーク、契約、その他の制度的統制に明記されるかもしれません。例えば、学位を取得したり、認定を受けたり、団体に加入したりする個人が、仕事において倫理的ガイドラインを適用することを含め、プロフェッショナルとして行動するという声明を引き受けることは珍しいことではありません。例えば、カナダのソフトウェアエンジニアがOrder of the Engineerに所属している。　[^2] IDProもバリュー・ステートメントにこれを含んでいます。 [^3]

@row
## Examples of Identity Ethics

Ethics become practical very fast in use cases. For example, when an organization deploys a passwordless authentication solution to its workforce and makes use of a swipe function app, how will this impact people with disabilities? Are they able to use it, or will they be excluded? Do they need to use another, more cumbersome, authentication tool? How will the solution affect those with visual or motor differences ? Are they able to use it? Or doesn’t the organization care, because the product is perfectly designed, and these are so-called “edge cases” (get to them in the infamous “Phase 2”)? What is important to the organization? What values are at stake here?

The same applies to customer identity management (CIAM) solutions. The way they are designed and how they operate impacts which customers are able to access services. An ethical discussion includes whether all people have an equal opportunity to become a customer and interact. So for example a CIAM solution may offer benefits to customers that buy in the app. But that means excluding, or at least disallowing benefits, for those users who do not have a smartphone (either because they cannot afford one or cannot use it). These discussions inevitably lead into the realm of the real world, where not all individuals are able-bodied, high-earning urban natives. These conversations force organizations to consider people outside their target demographic – those who do not regularly use digital technologies or those who need to get by on a minimum wage or allowance. These trade-offs are discussed later in this article.

Trade-offs become even more impactful in relation to government services and national identity. For example, refugees that want to register in their host country may be asked to use a registration tool that contains a drop-down list of nationalities: what if the one the refugee wants to select is not available? This was the case when Rohingya refugees fled to Bangladesh: they were not able to register the nationality they wanted.[^4]

The long-standing Aadhaar system in India is also worth observing to highlight ethical tensions.[^5] Aadhaar is a unique identity registration and identification system in India, where it has been incredibly successful. One of the system’s founding values was voluntary use: that an Aadhaar account would not be obligatory or compulsory in order to access services. After a decade in use, however, its adoption has grown and service providers have gravitated towards its substantial benefits (e.g. strong authentication and de-duplication). Aadhaar is now integrated into other services, like mobile telephony and banking. The result is that in practice Indians increasingly miss out on benefits, or need to put in additional effort, when they do not want, or cannot use Aadhaar. It is arguably less optional, therefore, as a citizen. Is this an ethical development? And who should pay attention to these shifts in use?

These examples demonstrate why technology itself is not good or bad ... but is also never neutral.[^6] They exemplify a few core tenets at the heart of this article:

1.  Design choices lead to (ethical) consequences in the real world.
    
2.  There are inevitable trade-offs between values that must be weighed and prioritized.
    
3.  These evaluations are subject to cultural differences in values and ethics.[^7]
    
4.  That technology never operates in isolation and should be designed with respect to its interfaces with business, operational, legal, and societal context (in the case of the Rohingya, the context of legal identity and humanitarian law).
    

Because "when you are assigning identity, you are exercising power, and you are defining their possibilities."[^8]

@column
## アイデンティティ倫理の例

倫理は、ユースケースにおいて非常に早く実用化されます。例えば、ある組織がパスワードレス認証ソリューションを従業員に導入し、スワイプ機能アプリを利用する場合、障害者にどのような影響があるでしょうか？彼らは利用できるのでしょうか、それとも排除されるのでしょうか？もっと面倒な別の認証ツールを使う必要があるのでしょうか？このソリューションは、視覚や運動機能に障害のある人々にどのような影響を与えるのでしょうか？その人たちは使えるのでしょうか？それとも、製品は完璧に設計されており、これらはいわゆる「エッジケース」（悪名高い「フェーズ2」で取り上げる）であるため、組織は気にしないのでしょうか？組織にとって何が重要なのでしょうか？どのような価値観がここで問題なのでしょうか？

同じことが顧客ID管理（CIAM）ソリューションにも当てはまります。それらの設計方法と運用方法は、どの顧客がサービスにアクセスできるかに影響します。倫理的な議論には、すべての人が顧客になって対話する機会が平等にあるかどうかが含まれます。例えば、CIAMソリューションは、アプリ内で購入した顧客に特典を提供するかもしれません。しかしそれは、スマートフォンを持っていないユーザー（スマートフォンを買う余裕がないか、使いこなせないかのどちらか）を排除するか、少なくとも特典を与えないことを意味します。このような議論は、必然的に現実世界の領域へと引き戻され、そこでは、すべての個人が健常で高収入の都市出身者というわけではありません。このような話し合いによって、組織はターゲット層以外の人々、つまりデジタル・テクノロジーを定期的に利用しない人々や、最低賃金や小遣いで生活する必要のある人々を考慮せざるを得なくなります。これらのトレードオフについては、この記事で後述します。

政府サービスと国民アイデンティティの関係では、トレードオフはさらに大きな影響を与えます。例えば、難民が受け入れ国で登録しようとする場合、国籍のドロップダウンリストを含む登録ツールを使うよう求められることがあります：難民が選択したい国籍が選択できなかった場合、どうなるでしょうか？ロヒンギャ難民がバングラデシュに逃れてきたとき、このようなケースがありました：彼らが要望する国籍で登録することができなかったのです。 [^4]

倫理的緊張を浮き彫りにするために、インドで長年続いているAadhaarシステムも観察する価値があります。 [^5] Aadhaarはインド独自のアイデンティティ登録・識別システムであり、信じられないほどの成功を収めています。システム設立時の価値観のひとつは、自発的な利用でした：サービスを利用するためにAadhaarアカウントを取得することは義務でも強制でもないというものでした。しかし、稼働してから10年後、その普及は拡大し、サービス・プロバイダーはその実質的なメリット（例えば、強力な認証や重複排除）に引き寄せられるようになりました。Aadhaarは現在、携帯電話や銀行など他のサービスに統合されています。その結果、インド人がAadhaarを使いたくなかったり、使えなかったりすると、実際には恩恵を受けられなかったり、余計な労力を必要としたりすることが増えています。そのため、市民としての選択性は間違いなく低下しています。これは倫理的な発展なのでしょうか？また、誰がこのような利用の変化に注意を払うべきなのでしょうか？

これらの例は、なぜテクノロジーそのものが良いものでも悪いものでもない...しかし、決して中立でもないのかを示しています。 [^6] これらは、この記事の核となるいくつかの信条を体現しています：

1.  設計における選択は、現実世界において（倫理的な）結果をもたらす。
    

2.  価値観の間には、秤にかけて優先順位をつけなければならないトレードオフが避けられない。
    
3.  これらの評価は、価値観や倫理観の文化的な違いに左右される。 [^7]
    
4.  テクノロジーは決して単独で機能するものではなく、ビジネス、業務、法律、社会的文脈（ロヒンギャの場合は法的アイデンティティと人道法の文脈）とのインターフェイスを考慮して設計されるべきである。
    

なぜなら、「アイデンティティを付与するということは、権力を行使するということであり、彼らの可能性を定義するということだからです」。 [^8]

@row
## Ethics

Ethics or moral philosophy is concerned with what is right and what is wrong. It is about discussions of values and what is important, how values can be compared, and ultimately reach a conclusion about what is right or wrong. We distinguish between the main ethical theories, the main ethical values, and the process of ‘doing ethics’. To be clear, this paragraph can never do justice to the wide and depth of moral philosophy, it should be considered a very high level and brief introduction.

| The most common used example to explain ethics – the **trolley problem** |     |
| --- | --- |
| Almost every introductory textbook in ethics uses the famous trolley problem. This problem starts with a trolley going down the track and the brakes malfunction. The trolley will hit five persons that are standing down the track and they will all die (in this example). But you can flip a switch that will make the trolley switch tracks, and on the other track there is only one person (that will get hit and die). Should you flip the switch? And in a next version there is a terminally ill person standing on the bridge over the tracks. If you push this person of the bridge onto the tracks the trolley will stop before it hits the five persons. Would you do that?[^9] | ![A drawing of a person standing on a bridge Description automatically generated](wiki-trolley.png)<br><br>_Image from [wikipedia](https://en.wikipedia.org/wiki/Trolley_problem)._ |

@column
## 倫理

倫理学や道徳哲学は、何が正しくて何が間違っているかに関わるものです。価値観や何が重要かについて議論し、価値観をどのように比較し、最終的に何が正しいか間違っているかの結論を導き出すものです。私たちは、主な倫理理論、主な倫理的価値観、そして「倫理をおこなう」プロセスを区別します。はっきり言って、この段落は道徳哲学の広さと深さを正当に評価することはできず、非常にレベルが高く短い導入部と考えるべきです。

| 倫理を説明する最もよく使われる例 -  **トロッコ問題** |     |
| --- | --- |
| 倫理の入門書のほとんどに、有名なトロッコ問題が使われています。この問題は、線路を走るトロッコのブレーキが故障したところから始まります。トロッコは線路の先に立っている5人の人にぶつかりそうになっており、ぶつかれば彼らは全員死んでしまいます（この例では）。しかし、あなたがスイッチを入れれば、トロッコは線路を切り替えることができ、もう一方の線路にはたった1人しかいません（その人は轢かれて死にます）。スイッチを入れるべきでしょうか？そして次のバージョンでは、線路にかかる橋の上に末期患者が立っています。この人を橋から線路に突き落とせば、トロッコは5人にぶつかる前に止まります。あなたならそうしますか？ [^9] | ![A drawing of a person standing on a bridge Description automatically generated](wiki-trolley.png)<br><br>_Image from [wikipedia](https://en.wikipedia.org/wiki/Trolley_problem)._ |

@row
### Ethical theories

Ethical theories are rooted in society, history and culture and are always in development, just like humanity itself. Perhaps the closest to a global agreement on ethics are the declarations on human rights (the Universal Declaration of Human Rights (UN), the International Covenant on Civil and Political Rights, the Charter of Fundamental Rights of the European Union and the Convention on the Rights of the Child[^10]). Importantly, despite centuries of efforts by philosophers, there is no one universal & globally acceptable theory of ethics (note that ethics is not religion, most religions claim to have moral truth). The following section describes four major schools of ethical thought, humbly noting that one article can never do justice to all ethical philosophies: there are many that contain elements of these four ‘mainstream’ ethical theories and there are others focusing on specific disciplines, such as Environmental Ethics and or political theories.[^11]

The four theories that are detailed in this article are utilitarianism, duty ethics, virtue ethics and communal ethics.[^12]

| Ethical theories |     |     |     |
| --- | --- | --- | --- |
| Utilitarianism | Duty Ethics | Virtue Ethics | Communal Ethics |

@column
### 倫理理論

倫理理論は、社会、歴史および文化の根底にあり、人類そのものと同じように常に発展しています。おそらく、倫理のグローバルな同意に最も近いのは人権でしょう（世界人権宣言（UN）、市民的及び政治的権利に関する国際規約、欧州連合基本権憲章、子どもの権利条約 [^10] ）。重要なことに、哲学者による何世紀にもわたる努力があっても、普遍的かつ世界的に通用する倫理理論というものは存在しません（倫理は宗教ではないことに注意してください、ほとんどの宗教は道徳的真理があると主張します）。以下のセクションでは、倫理思想の主要な4つの学派について説明しますが、1つの記事ですべての倫理哲学を正しく評価できないということに謙虚に留意していただきたい：これら4つの「主流」の倫理理論の要素を含むものも多くあり、環境倫理学や政治理論など特定の分野に焦点を当てたものもあります。 [^11]

本稿で詳細に述べている4つの理論は、功利主義、義務倫理、美徳倫理、共同体倫理です。 [^12]

| 倫理理論 |     |     |     |
| --- | --- | --- | --- |
| 功利主義 | 義務倫理 | 美徳倫理 | 共同体主義 |

@row
#### Utilitarianism

This is the ethics of usefulness. It is a form of consequentialism,[^13] meaning the result of an action determines whether the action is right.[^14] Utilitarianism states that when something is useful, it is right. The most common philosopher of utilitarianism is Jeremy [Bentham](https://plato.stanford.edu/entries/bentham/) (1748-1832), and one typical statement he made was saying that utilitarianists want _the greatest happiness of the greatest number_. Utilitarians could say that when lying brings about good results, lying is good.

The challenges with utilitarianism relate to the distribution of utility or happiness and the potential for harms. Criticisms are often boiled down to “who values the outcome” and “who determines what is valuable?”.[^15] It may be extremely difficult to measure “utility.” For example, saying ‘if it brings more revenue, it is good’ is clearly Utilitarian. However, when it comes with costs to the health of employees or customers, or even lives, it is ethically unjust. Or is it? Who gets to do this math?

A modern example of this playing out is self-driving technology: given that self-driving cars will be safer in future, does the utility of future lives saved justify unfettered testing on today’s roadways?[^16]

@column
#### 功利主義

これは有用性の倫理です。これは結果主義 [^13] の一形態であり、行動の結果が行動の正しさを決定するということです。 [^14] 功利主義は、何かが有用であるとき、それは正しいというものです。功利主義の最も一般的な哲学者は、Jeremy [Bentham](https://plato.stanford.edu/entries/bentham/)（1748-1832）であり、彼が用いた有名な言葉は、功利主義者は _最大多数の最大幸福_ を求める、です。功利主義はで、嘘が良い結果をもたらせば、嘘は良いこととなります。

功利主義の課題は、有用性または幸福の分配と害悪の可能性に関係します。しばしば、批判は「誰が結果に価値を見出すのか」「何が価値あるものかを誰が決定するのか」という点に集約されます。 [^15] 「有用性」を測ることは極めて難易度が高いでしょう。例えば、「収益が上がるなら良いことだ」というのは明らかに功利主義的です。しかし、それが従業員や顧客の健康、あるいは命に関わるものであれば、倫理的に不公正です。そうでしょうか？誰がこの計算をするのでしょう？

現代における例は、自動運転技術です：将来、自動運転車はより安全なものになるでしょうが、将来の人命救助という実用性が、現在の道路で無制限にテストすることを正当化するでしょうか？ [^16]

@row
#### Duty Ethics

Other philosophers consider duties (adherence to an adopted moral code) to be more important than the result of an action. One of the leading philosophers of Duty Ethics (also known as Deontology) is Immanuel [Kant](https://plato.stanford.edu/entries/kant/) (1724-1804), who described the ‘categorical imperative’ that determines whether an action is permissible based on whether it can be applied universally – i.e. asking the question “what if everyone did that?”. Importantly a Duty may mean that certain actions are right to do – even when they do not result in utilitarian benefits (i.e. even if they make no one any happier). When the rule is ‘you should always speak the truth’ then that guides the decision on whether something is right or wrong. Duty Ethicists say that lying is never good, because we have a duty to be upright and honest all the time. They care less for the consequences, as long as the rules were followed or the duties are fulfilled.[^17] This can give rise to conflicts, for example, in situations where lying could save someone’s life or the variations on the Trolley Problem.

This means that, while a Utilitarian may consider torture to obtain critical information, a Duty Ethicist will always disapprove of torture and instead apply the so-called Golden Rule that mandates “do unto others what you would want to be done to yourself.” And because these are universal rules, according to duty ethicists, they are often in a framework that guides ethical decisions and ensures that everyone is aware of the moral expectations. Critics of Duty Ethics might suggest, however, that there are many acts for which universality cannot be easily established in the real world. Furthermore, there are certainly cases in which Duties come into conflict and a rigid adherence to doctrine may induce harms. Duty Ethics does not wholly enable technologists to navigate trade-offs.

In the Digital Identity industry, many agree with Article 6 of the United Nations Universal Declaration on Human Rights: that we have a duty to ensure that all people have a right to legal personhood before the law. If a vendor deploys a Digital Legal Identity system that is later used by malevolent government actors to commit human rights abuses, Duty Ethics asserts that the deployment was still moral as long as it was motivated by that duty – even if those abuses would have been preventable (e.g. by implementing privacy-by-design best practices). On another level, similarly, meeting a deadline by delivering an identity management solution without some critical controls would be rejected by the Duty Ethicist, as the duty of delivering quality would be violated (although the buyer might not even notice and the goal of timelines (utilitarian) can be achieved).

@column
#### 義務倫理

他の哲学者は、行為の結果よりも義務（採用された道徳規範の遵守）のほうが重要であると考えています。義務倫理（脱存在論としても知られます）の代表的な哲学者の一人はImmanuel [Kant](https://plato.stanford.edu/entries/kant/)（1724-1804）であり、彼はある行為が普遍的に適用できるかどうかに基づいて許されるかどうかを決定する「定言命法」を説明しました。つまり、「すべてのひとがそのことをしたらどうか？」という問いかけをおこなうこと。重要なのは、ある行為が功利主義的な利益をもたらさない場合であっても（つまり、誰も幸せにならない場合であっても）、義務はある行為が正しいことを意味するということです。「常に真実を話すべきである」というルールがある場合、そのことが、正しいか間違っているかの判断の指針となります。義務倫理主義者は、私たちには常にまっすぐ正直であるという義務があるため、嘘をつくことは決して良いことではないと言います。彼らは、ルールが守られ、義務が果たされている限り、その結果はあまり気にしません。 [^17] このことは、例えば、嘘をつくことで人の命が救われるような状況や、トロッコ問題のバリエーションにおいて、対立を生む可能性があります。

つまり、功利主義者は重要な情報を得るために拷問を考慮するかもしれませんが、義務倫理主義者は常に拷問を否定し、その代わりに「自分がされたいことを他人にもする・といういわゆる黄金律を適用します。また、義務倫理主義者によれば、これらは普遍的なルールであるため、倫理的な決定を導き、誰もが道徳的な期待に気づいていることを保証する枠組みの中にあることが多いです。しかし、義務倫理を批判する人たちは、現実の世界では普遍性が容易に確立できない行為が数多く存在することを指摘するかもしれません。さらに、義務が対立するケースも確かに存在し、教義を厳格に遵守することが弊害を誘発する可能性もあります。義務倫理は、技術者がトレードオフを乗り越えることを完全に可能にするものではありません。

デジタルアイデンティティ業界では、国連世界人権宣言の第6条、すなわち、すべての人が法の下で合法的な人格を持つ権利を確保する義務があることに、多くの人が同意しています。ベンダーがデジタルリーガルアイデンティティシステムをデプロイし、それが後に悪意のある政府関係者に使用されて人権侵害がおこなわれたとしても、義務倫理は、そのデプロイがその義務によって動機付けられている限り道徳的であると主張します。別のレベルでは、同様に、いくつかの重要な管理を行わずにアイデンティティ管理ソリューションを納品して期限に間に合わせることは、品質を提供するという義務に違反することになるため、義務倫理主義者によって拒否されることになります（ただし、買い手は気づかないかもしれないし、期限（功利主義）の目標は達成できます）。

@row
#### Virtue Ethics

Philosophers of Virtue Ethics consider the ultimate objective to be a moral life of virtuous habits. The virtuousness of an action (not the result!) determines whether it is right or wrong. When it is a virtue to help each other, then helping each other is the right thing to do regardless of whether it was motivated by duty (as in Duty Ethics) or whether it achieves positive results (Utilitarianism). Obviously this raises the question, similar as with duties: “what are the virtues?”, “who decides what is virtuous?”, and “what is the end-goal?” [Aristotle](https://plato.stanford.edu/entries/aristotle/), Plato, and Socrates are considered the main thinkers that developed this theory. In their time (ancient Greek civilization) their formulation of Virtue Ethics also included a clear view on what humans were meant to be, what their objective is (their ‘teleos’ in Greek) and that all actions to achieve that were good. Some examples of virtues are courage, compassion, modesty, honesty and kindness. Kant’s main critique of Virtue Ethics included the notion that a person with virtuous habits but malevolent intent would lead to a very effective malevolence (e.g. a really good thief). And, of course, utilitarians would agree since thievery does not optimize the total amount of happiness (unless that thief is Robin Hood[^18] or otherwise philanthropically inclined…).

Taking the same Digital Identity System example above, Virtue Ethicists would consider it moral, not if driven by the duty to provide identity for all, but instead if it has been designed virtuously. In order to cultivate the virtue of autonomy with individuals they could propose a self-sovereign identity (SSI) solution that supports more autonomy than another (central or federated) type of identity management solution (where third parties, like institutions, play a determining role in controlling the identity and data). This may also cover virtues of inclusion, a process of ethical reckoning, etc.

@column
#### 美徳倫理

美徳倫理の哲学者は、徳の高い習慣を持つ道徳的な生活を究極の目的と考えます。行為（結果ではありません！）の美徳は、正しいか間違っているかを決定します。助け合うことが美徳である場合、助け合うことは（義務倫理における）義務によって動機付けられたものであろうと、肯定的な結果をもたらすのか（功利主義）にかかわらず、正しいことです。当然、これは義務と同じような疑問をもたらします：「美徳とは何か？」「何が美徳なのかをだれが決めるのか？」そして、「最終目標は何か？」[Aristotle](https://plato.stanford.edu/entries/aristotle/)、PlatoそしてSocratesは、この理論を発展させた重要な思想家と考えられています。当時（古代ギリシャ文明）、美徳倫理の公式には、人間がどうあるべきか、人間の目標は何か（ギリシャ語で「teleos」）、それを達成するための行動はすべて良いものであるという明確な見解も含まれていました。美徳の例には、勇気、思いやり、謙虚、正直そして優しさなどがあげられます。美徳倫理に対するKantの主たる批判は、徳の高い習慣を持ちながら悪意のある人は、非常に効果的な悪意（例えば、真に優れた泥棒）につながるという考えを含みます。当然、功利主義者も盗難行為が幸福の総量を最適にするわけではありません（泥棒がRobin Hood [^18] など博愛主義に傾倒しているならば別ですが）。

前述のの同じデジタルアイデンティティシステムを例にとると、美徳倫理学者は、すべての人にアイデンティティを提供する義務に駆られるのではなく、徳を持って設計されている場合に、それを道徳的であると考えます。個人との自律の美徳を培うために、他の（中央集権またはフェデレーション）タイプのアイデンティティ管理ソリューション（機関などの第三者がアイデンティティおよびデータの管理において決定的な役割を果たす）よりも多くの自律をサポートする自己主権型アイデンティティ（SSI）ソリューションを提案することになります。これはまた、インクルージョンの美徳、倫理的清算のプロセスなども対象となります。

@row
#### Communitarianism

This more modern theory of Communitarianism considers the communal aspects and suggests that, in fact, ethics cannot be separated from its socio-historic context. One of the proponents is [Alasdair MacIntyre](https://en.wikipedia.org/wiki/Alasdair_MacIntyre) (1929) who wrote ‘After Virtue’ (1981). It rejects the Virtue Ethics practice of separating the ends (outcomes) from the means (virtues in this case). In this paradigm, the community is the source of meaning, values, and therefore ethical practice. This occurs via community sense-making, which is a function of language, meaning, history, religion. Ethics in this theory includes the impact on the society and the community, not just what a development does in a community (but also what it does to it).

There is some critique on the communitarianism theory. Individual values like self-determination, moral autonomy, right to privacy (including control over your data) can sometimes conflict with accountability and obligations towards others (which are more relational and societal) and the responsibility for ones actions, as values more related to communitarianism[^19].

@column
#### 共同体主義

より現代的な共同体主義の理論は、共同体的な側面を考慮し、実際には倫理は社会歴史的なコンテキストからは分離できないことを示唆しています。提唱者の一人は、「After Virtue」（1981）を書いた[Alasdair MacIntyre](https://en.wikipedia.org/wiki/Alasdair_MacIntyre)（1929）です。目的（結果）と手段（この場合は美徳）を切り離す美徳倫理の実践を否定しています。このパラダイムでは、共同体が意味、価値そして倫理的実践の源泉であるとします。これは、言語、意味、歴史、宗教の機能である共同体のセンスメイキングによって生じます。この理論での倫理は、社会および共同体にあたる影響を含み、共同体でどのような発展があったのかだけではありません（共同体に何をしたのかを含みます）。

共同体主義理論にも批判はあります。自己決定、道徳的自律性、プライバシーの権利（自身のデータの管理を含む）のような個人の価値観は、（より関係的、社会的な）他者に対する説明責任や義務、自身の行動に対する責任において、より共同体との関係のある価値観と、ときおり衝突します。 [^19]

@row
#### Overview and Example

The overview of the four theories also gives examples of probable statements made, using these theories. In addition an example is given to further clarify what type of arguments and reasoning are associated with the various theories.

| Overview of Ethical Theories |     |     |     |
| --- | --- | --- | --- |
| Utilitarianism | Duty Ethics | Virtue Ethics | Communal Ethics |
| Result, outcome, consequence. It is right if the result is right. The means serve the end. | Duty, principle. Even when it lands you in trouble you carry out your duty. | Character building, virtue development. Whatever makes us a better person. | Community and relations. What makes a better society, creates a stronger social fabric. |
| ‘It is OK to cut a few corners and hide some mistakes to get the product launched on time’ | ‘We have to be transparent with regards to the risks of our product, it is our duty to inform every user fully’ | ‘This design forces the user to active consider options, we want to cultivate this behavior in the user’ | ‘This feature brings people together based on similarities instead of creater bigger divisions’ |

Using Artificial Intelligence as an example the four theories could view the developments related to AI like this:

*   Utilitarianism: good because it speeds up production processes, helps students deliver essays more quickly, allows doctors to diagnose patients quicker and better
    
*   Duty ethics: worrisome since AI is going to take over some of the human duties, yet technology can never be held accountable
    
*   Virtue ethics: good because it allows humans to focus more on cultivating virtuous habits, yet bad because it is used for creating essays, yet bad when it makes humans lazy (as an example)
    
*   Communitarism: bad because of the impact on society, the ‘race for the brain stem’ and the destabilization of democratic processes, fake news, etc.
    

So was it useful, did you do your duty, or were you to develop a virtue, or consider the community/society? Having philosophers thinking and discussing this for centuries is at least a sign that we won’t be able to come to a definite answer this decade. (just kidding)

If we want to have maximum positive impact in the world through our work as identity professionals, we need to be conscious of these ethical theories and make sure we bring the right (design) reasons to the table before we make choices. Outcomes matter, so too do the values and the virtues that have been selected to achieve those outcomes. And, embracing communitarianism means that valuable outcomes and practices may differ around the world. With this said, this paper recommends that Identity professionals - and really any professional - begin with understanding the difference between ‘but this will provide a good result’ and ‘but this is what we ought to do’ and ‘but this is what professional with integrity would build’ and ‘but this is what our community needs’, followed by a clear articulation of the values their work is designed to uphold.

@column
#### 概観と例

4つの理論の概観では、それぞれの理論を使ったら、可能性がありそうな発言の例も挙げています。さらに、各理論についてどのようなタイプの議論や推論に関連してるからを明確にするための例も示しています。

| 倫理理論の概要 |     |     |     |
| --- | --- | --- | --- |
| 功利主義 | 義務倫理 | 美徳倫理 | 共同体主義 |
| 結果、業績、成果。結果が正しければ、正しいです。手段は目的のためにあります。 | 義務、原則。たとえトラブルに巻き込まれたとして、義務を遂行します。 | 人格形成、積徳。私たちをより良い人間にするものなら何でも。 | 共同体と関係。より良い社会を作るものは、より強固な社会基盤をつくります。 |
| 「製品を予定通りに発売するために、多少の手抜きやミスの隠蔽をしても問題ありません」 | 「私たちの製品のリスク関する透明性がなければならない、すべてのユーザーに充分な情報を伝えることが私たちの義務です」 | 「このデザインは、ユーザーに積極的に選択肢を検討させることになり、ユーザーにこのような行動を育てたいと思っています」 | 「この機能は、より大きな分断をもたらすのではなく、類似点によって人々を結びつけます」 |

人工知能を例にとると、4つの理論はAIによる開発を次のように見るでしょう：

*   功利主義：生産工程をスピードアップさせ、学生がより早く小論文を提出できるようになり、医師が患者をより早く、より良く診断できるようになるので良いものです
    
*   義務倫理：AIが人間の義務の一部を引き継ぐことになるので心配だが、テクノロジーは決して責任を負うことができません。
    
*   美徳倫理：人間がより徳の高い習慣を身に着けることに集中できるようになるので良いものですが、小論文の作成に使われるために悪いものであり、（一例として）人間を怠惰にするため悪いものです
    
*   共同体主義：社会への影響、「脳幹の獲得競争」、民主的プロセスの不安定化、フェイクニュースなどの理由から悪いものです
    

では、役に立ったのか、義務を果たしたのか、徳を積むためだったのか、共同体・社会のことを考えるためだったのでしょうか？哲学者たちが何世紀にもわたってこのことを考え、議論してきたということは、少なくともこの10年で明確な答えを導き出すことはできないだろうということの表れです。 (冗談です）

アイデンティティの専門家としての仕事を通じて世界に最大限のポジティブな影響を与えたいのであれば、私たちはこれらの倫理理論を意識し、選択をおこなう前に正しい（設計上の）理由をテーブル上に並べる必要があります。成果は重要であり、その成果を達成するために選択された価値観や美徳もまた重要です。そして、共同体主義を受け入れるということは、価値ある成果と実践が世界中で異なる可能性があるということです。本稿では、アイデンティティの専門家（そして本当にあらゆる専門家）が、「しかし、これは良い結果をもたらすだろう」、「しかし、これは我々がすべきことだ」、「しかし、これは誠実な専門家が構築するものだ」、「しかし、これは我々のコミュニティが必要としているものだ」の違いを理解することから始め、その後に、自分たちの仕事が守るようにしている価値観を明確に示すことを推奨します。

@row
### Values to Uphold (or not)

When grappling with ethics on a project, the key questions are about

1.  What is valued?,
    
2.  How those values relate to each other
    
3.  How can the project honour and reflect those values more than before.
    

This section proposes and explains several values relevant to Digital Identity. Note that IDPro is releasing another article, “Ethics for Digital Identity and Identity Driven Algorithms” by Mike Kiser, in which a slightly differing set of values is discussed.[^20] There is a large overlap to be expected in values that differing authors hold and discuss, and at the same time each individual will bring their own emphasis, based on their context, background, culture, technical specialism and experience. This shows that in ethics the conversation is essential, and not having a final definitive exhaustive list of values (as that does not exist).

In practice, ethics is a process of discussing, weighing, navigating, documenting, and measuring values. Rather than adopting one or the other, the authors and the BoK Editorial Committee encourage practitioners to use these and other best-practice inputs to develop contextually appropriate value-sets. Further resources are highlighted at the end of both articles.

@column
### 守るべき（守らない）価値観

プロジェクトで倫理に取り組む場合、重要な質問は

1.  何が価値あるものなのか？、
    
2.  互いの価値難はどのように関係しているのか
    
3.  プロジェクトが、以前よりもそれらの価値観を尊重し、反映するにはどのようにすればよいのか
    

このセクションではデジタルアイデンティティに関連するいくつかの価値観を提案し、説明します。IDProはMike Kiserによる別の記事「Ethics for Digital Identity and Identity Driven Algorithms」を公開しており、そこではわずかに異なる価値観について議論んしています。 [^20] 様々な著者が抱え、議論する価値観には大きな幸福が予想されますが、同時に各個人は自身の状況、背景、文化、専門技能および経験に基づいて独自に重視することを持っています。これは、倫理において対話が不可欠であり、最終的で決定的で包括的な価値観のリストを有しているわけではない（そのようなものは存在しない）ことを示しています。

実際には、倫理とは価値観について議論し、評価し、導き、文書化し、測定するプロセスです。著者とBoK編集委員会は、実践者たちにある価値観や別の価値観だけを採用するよりも、これらおよびその他のベストプラクティスを使って適切な価値セットを開発することを推奨しています。両方の記事の最後にはさらなるリソースについて紹介されています。

@row
#### Well-Being

Human well-being is also expressed in the Hippocratic oath: “do no harm,” but the concept must involve more than a mere defensive approach. This is a widely accepted assertion, also found in the various human rights instruments. But what does it mean? And whose well-being?

Well-being for one group may mean it comes at the expense of another. Especially in the global supply and production chains there is growing recognition for a fair distribution of benefits and a fair distribution of the costs of production (not just financially, but also in terms of pollution, waste, etcetera). Also, the question arises what exactly is well-being: is it more income, or perhaps less income but more freedom? Perhaps it is privacy… but perhaps it is strong counter-fraud controls in the ecosystem. Are those two aspects of well-being sometimes in tension? This means exploring and documenting the interplay of interests for all parties. Key is the conversation to a) at least recognize this value and b) discuss the questions of what well-being, whose well-being and impact on well-being c) identify the requisite trade-offs. Some research in this area has been done by Women in Identity.[^21]

@column
#### 幸福

人間の幸福もヒポクラテスの誓い「害を与えない」において表現されていますが、その概念委は単なる防御的なアプローチ以上のものが含まれていなければなりません。これは広く受け入れられている主張であり、様々な人権宣言にも見られます。しかし、これはどういう意味でしょうか？そして誰の幸福でしょうか？

あるグループの幸福は、ほかのグループの犠牲を伴うことがあります。特に、グローバルなサプライチェーンおよび再選チェーンでは、公正な利益分配と構成や生産コストの分配（財務的だけでなく、汚染や廃棄物などの観点からも）について認識されるようになってきました。また、幸福は正確に何かという疑問も生じます：より多くの収入でしょうか、収入は少なくても自由なことでしょうか？もしかすると、プライバシーのことかもしれません...しかしエコシステムにおける強力な詐欺対策である可能性もあります。幸福のこれら2つの側面は、特には緊張関係にあるのでしょうか？これらはすべての関係者の利益の相互作用を調査し、文書化することを意味します。重要なことは、a）少なくとも価値に認識し、b）何が幸福なのか、誰の幸福なのか、幸福への影響という疑問について議論し、c）必要なトレードオフを特定する、という対話です。この分野のいくつかの研究は、Women in Identity [^21] によって実施されています。

@row
#### Autonomy

Autonomy refers to individuals having the freedom to decide what to do and exercising control over their own life. Most often defined as “freedom from external control or influence,” this applies within the boundaries that are set in society. Importantly, autonomy does not mean individuals can steal or abuse others. Autonomy can also include the autonomy of making up one’s mind. Often, legal frameworks (like Europe’s General Data Protection Regulation) and Digital Identity implementations uphold this value through the concept of consent.

The book _Beyond Data_ by Elizabeth Renieris[^22] considers where the usefulness of consent ends and further regulation is required. A car offers a tangible example: you can’t buy one without brakes and a seatbelt, but you can select the brand, the horsepower and the color. What should be regulated (brake, seatbelt) and what should be for the user to decide? And a similar discussion starts related to the digital identity wallet that every citizen of EU Member States can use to authenticate and share data, where full control by the user realizes (a form of) self-sovereign identity (SSI) and on the other hand we know how easy users share data online or click ‘accept’, so where should control be augmented with restrictions? How should regulators address the risk of oversharing data[^23]?

@column
#### 自律性

自律性とは、個人が自分の行動をけてする自由を持ち、自分の人生をコントロールすることを指します。しばしば、「外部からのコントロールや影響からの自由」というように定義されますが、これは社会で差が目られた範囲内に提供されます。重要なのは、自律性は個人が盗んだり、他者をいじめたりしないことを指します。また、自律性は自分の意思を決定する自律性を含みます。多くの場合、法的な枠組み（欧州の一般データ保護規則のような）およびデジタルアイデンティティ実装は、同意の概念を通じでこの価値を支持します。

Elizabeth Renierisによる著書 _Beyond Data_ [^22] では、同意の有用性がいつ終わりを迎えたのか、そしてさらなる規則について検討しています。自動車は具体的な例を提供します：ブレーキとシートベルトのない車は購入できませんが、ブランド、馬力や色は選択することができます。何が規制されるべき（ブレーキ、シートベルト）で、何はユーザーが決められるべきでしょうか？同様の議論がEU加盟国のすべての市民が認証、データの共有のために利用されるデジタルアイデンティティウォレットに関連して開始されおり、ユーザーによる完全な制御が自己主権型アイデンティティ（SSI）（の一形態）を実現させますが、一方でユーザーがデータをオンラインで共有したり、「受け入れる」をクリックしたりすることがいかに簡単であるかに浮いて知っており、ではどこに制限を加えるべきでしょうか？どのように規制当局はデータの過度な共有のリスクに対処するべきでしょうか [^23] ？

@row
#### Agency

Agency is the capacity to act under one’s own free will. Everybody is influenced continuously, but when technologies enable manipulation and coercion, it deprives people of autonomy and agency: people lose their ‘free will’, either knowingly or unknowingly (e.g., in cases of misinformation or algorithmic manipulation[^24]), then this is generally considered unethical.

@column
#### 主体性

主体性とは、自らの自由意志に基づいて行動する能力のことです。誰もが絶えず影響を受けていますが、テクノロジーによって操作や強制が可能になると、人々の自律性と主体性が奪われます：人々は、（誤った情報やアルゴリズムによる操作の場合など [^24] ）知ってか知らずか、「自由意志」を失うことになり、これは一般的に非倫理的とみなされます。

@row
#### Equality

Equality is the state of being equal, especially in status, rights and opportunities. Equality means each individual or group of people is given the same resources and opportunities, regardless of their circumstances. Digital technologies can create more opportunity for equality by expanding the ways that people can interact when digital is offered as an additional channel. However, just as easily, digital technologies can create more inequality through their design by targeting mainstream users, which can make it more difficult for those outside of the mainstream to participate. For instance, this ca an occur via prerequisites, such as digital literacy, devices, connectivity, or power.

@column
#### 平等性

平等性とは、特に地位、権利や機会において同じである状態です。平等性は、各個人や人々の各グループに環境に関係なく、同じリソースと機会が与えらえることを指します。デジタル技術は、人々が追加のチャンネルとしてデジタルが提供されることで、人々が交流できる方法が広がり、人々に平等性のさらなる機会を作りだすことができます。しかし、デジタル技術は主流なユーザーを対象とする設計によって不平等を生み出すことになり、それは主流ではない人々が参加することを難しくします。例えば、これはデジタルリテラシー、デバイス、接続性や電力のような前提条件によって、このような事態が発生するでしょう。

@row
#### Transparency

For users to hold practitioners accountable for decisions in design, development of solutions and their implementation(s), the reasons must be transparent to end users. True transparency not only answers the question of why, _but it breaks down the how_ in a simple way. When applying this to identity, it is critical to use language that is easily understandable to the end user, as technical jargon can quickly become complex.

This transparency is more than just disclosure for disclosure’s sake — it enables autonomy of individuals by having clear visibility on what is happening and why. It enables the stakeholders to timely identify necessary changes to the system when the purpose changes of over time or when the operations of the solution do not meet the purposes anymore. It minimizes the risk of ending up in the sitation where ‘this is just how the system works, we do not know why exactly but we can’t change it’, leading to unintended results (and potentially including harm).

@column
#### 透明性

設計、ソリューションの開発および実装についての決定に対してユーザーが実務者に説明責任を持たせるには、その理由がエンドユーザーに対する透明性がなくてはなりません。真の透明性はなぜという問いに答えるだけでなく、単純に _どのようにという問いに分解する_ ことです。これをアイデンティティに適用する場合、すぐに専門用語が複雑になってしまうため、エンドユーザーにとって容易に理解できる用語を使うことが重要です。

この透明性は、単に開示のための開示だけでなく、何がなぜ起きているかという疑問に明確に可視化することで、個人の自律性を有効にすることです。時間とともに目的が変化したり、ソリューションの運用が目的に一致しなくなった場合、ステークホルダーがタイムリーに必要なシステム変更を特定することが可能になります。「これがシステムがどのように動いているかであり、なぜなのかはわからないですが、変更することはできません」、という状態になって意図しない結果になる（潜在的な危険性を含む）というリスクを最小化することになります。

@row
#### Fairness (Lack of Bias)

For Identity Systems to promote fairness, it must expose its own biases. Detection is successful only when the full range of bias is understood, and organizations such as IBM have helpfully provided a taxonomy of bias, ranging from bias due to doing too much, too quickly (shortcut bias) — to false assumptions of sound judgement (impartiality bias) — to more direct prejudices (self-interest bias). [^25]

The value of fairness can also include that those who put in effort also should get reward (either through income or other benefits).

@column
#### 公平性（バイアスの排除）

アイデンティティシステムが公平性を促進するには、バイアスを明らかにしなければなりません。すべての範囲のバイアスが理解されてはじめて検出に成功し、IBMのような組織はバイアスの分類法を提供しており、あまりにも多くのことをあまりに早くおこなうこと（ショートカットバイアス）、健全な判断の誤った想定（公平性バイアス）や直接的な偏見（利己的バイアス）にまで及びます。 [^25]

公平性の価値観にも、努力した人も褒美（収入やその他の利益）を得るべきだという考えも含まれます。

@row
### Principles for Digital Identity

Various frameworks of principles and guidelines for the development of national Digital Identity solutions have appeared in the early 2020s. This article will not explore these but merely mention the many principles[^26] and a study on how principles and values differentiate based on the sociopolitical configurations[^27].

@column
### デジタルアイデンティティの原則

2020年代初頭に、国家のデジタルアイデンティティソリューションを開発するためのさまざまな原則とガイドラインの枠組みが登場しました。この記事では、これらについて検討するのではなく、単に多くの原則 [^26] と、社会政治的な構成に基づいて原則と価値観がどのように異なるかについての研究 [^27] について言及します。

@row
## Applied Ethics

With some background on the main ethical theories and a set of values, this paper turns its attention to how to ‘do ethics.’ This section describes several methods that have been developed to include ethics in technological design processes. When abstracted, every approach generally contains at least these four main elements:

1.  Consider the context and the use case (what do we have here)
    
2.  Identify all stakeholders (who do we have here)
    
3.  Discuss the use case (what values are impacted)
    
4.  Adjust the design/operation of the solution.
    

The scope for this evaluation should not be limited to technical functionality and, instead, should extend to the end-to-end experience of the actors in the eco-system. This broad view is essential in facilitating a holistic ethical discussion. This is true whether implementing a commercial authentication solution or a national Digital Identity eco-system that integrates with global payments.

Having completed those stages, the changes can be implemented. However, ethics needs to be continuously practiced. For example, when asbestos was invented it was great because it was so fire-resistant; only later did we find out it was a carcinogen. Another example is DDT, which was an insect repellent that worked really well to increase crop yields … until we found out it also poisoned ground water.[^28]

This could also happen to Digital Identity and Access Management solutions as solutions take root in the real world and technologies move on (e.g. encryption practices will need to move on with quantum computing), so continuous assessment of their impact on individual and society is required.

@column
## 適用される倫理

主な倫理理論と一連の価値観に関する背景を見てきましたが、本稿では「倫理を実践する」方法について目を向けます。このセクションでは、技術設計プロセスに倫理を含めるいくつかの手法について説明します。抽象化すると、すべてのアプローチでは一般的に少なくとも以下の4つの要素を含んでいます：

1.  コンテキストとユースケースの検討（ここに何があるのか）
    
2.  全てのステークホルダーの特定（ここに誰がいるのか）
    
3.  ユースケースの議論（影響を受ける価値観は何か）
    
4.  ソリューションの設計／運用の調整
    

この評価の範囲は技術的な機能に限定するべきではなく、エコシステムにおけるアクターのエンドツーエンドの体験まで拡張すべきです。この幅広い観点は、全体的な倫理的議論を促進するために不可欠です。商業的な認証ソリューションやグローバルな決済機能と連携する国家的なデジタルアイデンティティエコシステムを実装する場合でも同じです。

これらの段階を完了させることで、変革が実行できます。しかし、倫理は継続的な実践を必要とします。例えば、アスベストが発明されたとき、非常に高い耐火性があることから優れたものだとされていました；その後になって、発がん性物質であることがわかりました。ほかの例はDDTであり、DDTは昆虫忌避剤であり、農作物の収穫を増やすために非常に良いものでした...地下水を汚染していることを発見するまでは。 [^28]

このことはデジタルアイデンティティとアクセス管理のソリューションが、実世界で根付き、テクノロジーが変化することで、起きうることであり（例 暗号化の観衆が量子コンピュータによって変化する必要が出てくるかもしれません）、個人と社会への影響を継続的に測定することが必要です。

@row
### Value Sensitive Design

Value Sensitive Design (VSD) is a framework to systematically integrate values of ethical importance into technological designs, described by [Batya Friedman et al.](https://dl.acm.org/doi/pdf/10.1145/242485.242493) In 1996, and expanded in the following years. The methodology has three parts that it addresses: empirical, conceptual and technical. The empirical part identifies relevant stakeholders and their values and priorities, the conceptual part explores these values and their trade-offs, and the technical part clarifies how the technology either gives rise to value issues, or can ‘implement’ values in the design of technology. For technology that continues to change (i.e., it does not remain fixed after go-live) reflexivity is added as a fourth aspect, which periodically reflects on the technological design, its operation, and the values of ethical importance that play a role.[^29]

@column
### バリューセンシティブなデザイン

バリューセンシティブなデザイン（VSD）とは、1996に[Batya Friedmanら](https://dl.acm.org/doi/pdf/10.1145/242485.242493)によって発表され、その後拡張された、倫理的に重要な価値観をテクノロジー設計に体系的に統合するためのフレームワークです。この方法論は3つの部分があります：経験的、概念的、技術的。経験的な部分は関連するステークホルダーおよび価値観と優先事項を特定し、概念的な部分は価値観とトレードオフを探求し、技術的な部分ではテクノロジーがどのように価値観の問題を引き起こすか、テクノロジーの設計においてどのように価値観を「実装」できるかを明らかにします。常に変わり続けるテクノロジーには（つまり、稼働後も留まることがない）、第四の側面として再帰性が追加されます。再帰性とは、テクノロジーの設計、その運用、そして役割を果たす倫理的な重要な価値観について定期的な振り返りをおこなうことです。 [^29]

@row
### Guidance Ethics

The [guidance ethics approach (GEA)](https://ecp.nl/publicatie/guidance-ethics-approach/) positions the ethical observer not as a judge to a process or a result, but as a guide and consultant. This has evolved as a method where a workshop is conducted to discuss a new technology (such as digital wallets for digital identity and attributes). Facilitators gather all relevant stakeholders, discuss the use case, and deep dive into the impact of this technology. This is a guided value conversation during which the group discusses what values are impacted and, towards the end of the workshop, the actionable items and deliberations for the (design of the) technology are formulated. For example: when applying Digital Identity wallets for age verification (for buying alcohol online) the value of health was identified, but **also** the safety (of the cashier), autonomy and ease of use. In this approach theorists, designers and practitioners are jointly discussing the technology and the use case(s).[^30]

@column
### 指導倫理

[指導倫理アプローチ（GEA）](https://ecp.nl/publicatie/guidance-ethics-approach/)は、倫理的オブザーバーをプロセスや結果に対する審判としてではなく、指導やコンサルタントとして位置付けるものです。これは、新しいテクノロジー（デジタルアイデンティティや属性のためのデジタルウォレットなど）について議論するためにワークショップを実施する手法として発展してきました。ファシリテーターは全ての関係するステークホルダーを集め、そのユースケースについて議論し、このテクノロジーの影響について深く掘り下げます。これはガイドされた価値観の対話であり、グループはどのような価値観が影響を受けるのかについて議論し、ワークショップの終盤に向けて、実行可能な項目とテクノロジー（の設計に）ついての検討事項が策定されます。例：デジタルアイデンティティウォレットを年齢確認（酒類のオンライン販売のため）に適用する場合、健康だけでなく、（レジ係の）安全性、自律性および使いやすさとう価値について **も** 確認されました。このアプローチでは、思想家、設計者、実務者が共同で議論とユースケースについて議論します。 [^30]

@row
### Ethics Canvas

The [ethics canvas](https://link.springer.com/chapter/10.1007/978-3-319-99605-9_23) is based on the value proposition canvas,[^31] but adds the dimension of impact (the consequence space), where impact on the individual and society is described. Choices and outcomes may be explored and centrally documented using an ethics canvas. Identification of the affected individuals, their relationships, and worldviews help to give concrete insight into what groups might be in conflict and what trade-offs are being implicitly agreed to with each decision/implementation choice. This allows for all participants — from designers to implementers — to contemplate the ramifications of their decisions, and to embed a mindset that seeks to underscore the morality of their actions more clearly. This central document establishes the ethical standard that all participants agree to abide by; it is a guiding force throughout the rest of the process.[^32]

@column
### 倫理キャンバス

[倫理キャンバス](https://link.springer.com/chapter/10.1007/978-3-319-99605-9_23)は、バリュープロポジションキャンバス [^31] をもとにしていますが、影響の次元（結果空間）が追加され、これには個人および社会への影響を記述します。選択と結果は、倫理キャンバスを用いて探求し、一元的に文書化することができます。影響を受ける個人、関係性、世界観を特定することで、どのようなグループが対立している可能性があるのか、また、それぞれの決定／実装の選択においてどのようなトレードオフが暗黙のうちに合意されているかについて具体的に把握することができます。これによって、すべての参加者、設計者から実務者まで、が自分たちの決定の影響について熟考し、自分たちの行動の道徳性をより明確しようとする考えを根付かせることができます。この中心的な文書は、すべての参加者が遵守することに同意する倫理基準を確立するものであり、プロセスの残りの部分を通して指針となるものです。 [^32]

@row
### Example of Applied Ethics in Digital Identity

The 2013 process for the development of the British Columbia (BC) Services Card[^33] reports how this process successfully realized civil participation to discuss values and impact. The lessons learned were that the forum, panel and survey worked well. The clarity of the need and the aspect of ‘reporting back’ to those who provided input (do not merely use them for input at the start), painted a clear picture of what was to be achieved and how it will look like (practical and concrete). Lastly, it will make sure everyone is heard, including those groups in the population with a ‘softer’ voice.

Another example is the Horizon2020 IMPULSE (“Identity management in public services”) project that developed an innovative digital wallet for citizens to assess SSI and blockchain based approach to digital identity could be implemented into the public administration. The project [published](https://doi.org/10.1007/s44206-024-00113-2) on the assessment of ethical societal and legal issues. IMPULSE used a decentralised and SSI management system based on a verifiable credential (VC) model (using blockchain). Users request identity verifiable credentials through a digital onboarding process with biometric face recognition and document validation. From there the users present identity verifiable credentials for authentication to online public services. The ethical assessment was done with a deontological approach and a Value Sensitive Design approach.

@column
### デジタルアイデンティティへの倫理の適用例

2013年のブリティッシュコロンビア州（BC）サービスカード [^33] の開発プロセスは、このプロセスが価値観と影響について議論するために市民参加をどのように実現させたのかについて報告しています。ここからの教訓は、フォーラム、パネル、調査がうまく機能したことでした。必要性の明確さと意見を提供した人たちに「報告する」という側面があることが、何が達成され、（現実的かつ具体的に）どのようになるのかという絵を描きました。最後に、全ての人の声、「よりソフトな」声を持つ人々のグループも含めて聞くようにすることです。

別の例がHorizon2020 IMPULSE（「Identity management in public services」）プロジェクトであり、このプロジェクトではデジタルアイデンティティに対してSSIとブロックチェーンに基づくアプローチを行政に導入できるかを評価するため、市民向けの革新的なデジタルウォレットを開発しました。このプロジェクトは倫理的な社会的、法的問題の評価について[公開](https://doi.org/10.1007/s44206-024-00113-2)しました。IMPULSEは、（ブロックチェーンを使った）検証可能なクレデンシャル（VC）モデルに基づいた分散型かつSSIの管理システムを利用しました。ユーザーは、生体認証による顔認証と身分証明書の検証によるデジタルオンボーディングプロセスを通じてアイデンティティVCを要求します。そして、ユーザーはオンライン公的サービスに対して認証のためにアイデンティティVCを提示します。倫理的な評価は、義務倫理学的アプローチとバリューセンシティブデザインアプローチによって実施されました。

@row
## Finally

It takes time and dedicated conversation to create ethical identity solutions that have been built to express a clear set of values. One of the values most business hold is that a good cost-benefit analysis is done before expending resources on a project. The cost-benefit analysis for ‘being ethical’ seems hard to make, and isn’t it something that everyone should be? Who wants to be unethical? In addition there is evidence of a a positive business case. Inclusive solutions that take more time and effort to develop can result in more revenue/use because they achieve higher adoption. In general, businesses with an ethical approach to doing business outperform comparable companies by 12,3 percentage points in 5 years on the Large Cap Index.[^34]

Ethical behavior affords premium pricing, attracts ethical employees and associates – so the whole network becomes more ethical (investors, business partners, etc.).

For identity professionals it is important and possible to create solutions that contain the results of ethical and value-driven conversations. This leads to better results, whether working on enterprise IAM solutions, customer and market solutions, or even national solutions and global standards.

@column
## 終わりに

明確な価値観を表現するために構築された倫理的アイデンティティソリューションを生み出すには、時間と熱心な対話が必要です。ほとんどのビジネスが持っている価値観の一つは、プロジェクトにリソースを費やす前に、適切な費用便益分析をおこなうことです。「倫理的であること」の費用便益分析は難しいと推測されますが、誰もがそうあるべきものではないだろうか？誰が非倫理的でありたいと思うだろうか？さらに、ポジティブなビジネスケースの証拠もあります。開発のためにより多くの時間と労力を要するインクルーシブソリューションは、より高い採用率を達成するため、より多くの収益／利用をもたらす可能性があります。一般的に、ビジネスをおこなう上で倫理的なアプローチを採用している企業は、大型株指数で比較可能な企業を5年間で12,3％ポイント上回っています。 [^34]

倫理的な行動はプレミアム価格をもたらし、倫理的な従業員や仲間を引き付け、ネットワーク全体（投資家、ビジネスパートナーなど）がより倫理的になります。

アイデンティティの専門家にとって、倫理的で価値感主導の対話の結果を含むソリューションを作成することは重要であり、可能です。これは、企業のIAMソリューション、顧客や市場のソリューション、あるいは国家的ソリューションやグローバルスタンダードのいずれに取り組む場合でも、より良い結果につながります。

@row
## Other sources

The whitepaper [“Human-Centric Digital Identity: for Government Officials,”](https://openid.net/human-centric-digital-identity-whitepaper/) co-branded by 13 non-profits (including UNHCR) describes the connection between Human Rights and Digital Identity Initiatives, specifically Legal Identity, and includes five paradigms on digital identity.

A book on [Ethics for People Who Work in Tech](https://www.routledge.com/Ethics-for-People-Who-Work-in-Tech/Steen/p/book/9780367542436), detailing more on the ethical thoughts and the various approaches to applying ethics.

More on ethics at the ‘e’ in the [Stanford Encyclopedia of Philosophy](https://plato.stanford.edu/contents.html#e).

A a 4 page workshop report on ‘ethical digital identities’ ([https://dl.acm.org/doi/abs/10.1145/3526073.3527586](https://dl.acm.org/doi/abs/10.1145/3526073.3527586)) with a problem description and a specific definition of an ethical digital identity (EDI) - a digital identity of an object (e.g. unique identifier) that also states what ethical ‘level of assurance’ is given.

@row
- - -

[^1]:  Kiser, M. (2024) “Ethics for Digital Identity and Identity-Driven Algorithms.” IDPro Body of Knowledge 1(14) doi: [https://doi.org/10.55621/idpro.105](https://doi.org/10.55621/idpro.105).
    
[^2]:  Engineers Canada. “Public Guideline on the Code of Ethics | Engineers Canada,” n.d. [https://engineerscanada.ca/guidelines-and-papers/public-guideline-on-the-code-of-ethics#-the-code-of-ethics](https://engineerscanada.ca/guidelines-and-papers/public-guideline-on-the-code-of-ethics#-the-code-of-ethics). \[Accessed 31 July 2024\]
    
[^3]:  IDPro. “IDPro® Mission, Vision, Values, Services - IDPro,” n.d. [https://idpro.org/mission-vision-services](https://idpro.org/mission-vision-services). \[Accessed 31 July 2024\]
    
[^4]:  Covered in [https://msf.org.au/rohingya-worlds-largest-stateless-population](https://msf.org.au/rohingya-worlds-largest-stateless-population), but more complex than mentionable in one sentence
    
[^5]:  Government of India, Unique Identification Authority of India. “Aadhaar,” n.d. [https://uidai.gov.in/en/](https://uidai.gov.in/en/). \[Accessed 31 July 2024\]
    
[^6]:  Melvin Kranzberg, “Technology and History: Kranzberg’s Laws,” _Technology and Culture_ 27.3 (1986): 547.
    
[^7]:  Note that public and private actors may hold and promote different values, but values vary across cultures as well as well.
    
[^8]:  Francesca Morpurgo, “Panel: Human Rights by Design for a Fast-Changing World.” European Identity & Cloud Conference 2024, https://www.kuppingercole.com/sessions/5564/2.
    
[^9]:  See a Yale lectured on the Trolley Problem (lectures 14-15) at [https://oyc.yale.edu/philosophy/phil-181/](https://oyc.yale.edu/philosophy/phil-181/) and assess your own morality versus others at moralsensetest.com
    
[^10]:  Respectively [https://www.un.org/en/about-us/universal-declaration-of-human-rights](https://www.un.org/en/about-us/universal-declaration-of-human-rights); [https://www.ohchr.org/en/instruments-mechanisms/instruments/international-covenant-civil-and-political-rights](https://www.ohchr.org/en/instruments-mechanisms/instruments/international-covenant-civil-and-political-rights); [https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=OJ:C:2007:303:TOC](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=OJ:C:2007:303:TOC); and [https://www.ohchr.org/en/instruments-mechanisms/instruments/convention-rights-child](https://www.ohchr.org/en/instruments-mechanisms/instruments/convention-rights-child) See more Human Rights Instruments at https://www.ohchr.org/en/instruments-listings
    
[^11]:  See [Environmental Ethics (Stanford Encyclopedia of Philosophy)](https://plato.stanford.edu/entries/ethics-environmental/) for example
    
[^12]:  The book by Michael Sandell on Theories of Justice provides an excellent further exploration of these theories.
    
[^13]:  “Consequentialism (Stanford Encyclopedia of Philosophy),” October 4, 2023. [https://plato.stanford.edu/entries/consequentialism/](https://plato.stanford.edu/entries/consequentialism/). \[Accessed 31 July 2024\]
    
[^14]:  Another type of consequentialism is hedonism, which basically states that when it gives pleasure, it is right.
    
[^15]:  “Bernard Williams (Stanford Encyclopedia of Philosophy),” January 28, 2023. [https://plato.stanford.edu/ENTRIES/williams-bernard/](https://plato.stanford.edu/ENTRIES/williams-bernard/). \[Accessed 31 July 2024\]
    
[^16]:  “‘Elon Musk’s Appetite for Destruction.’” Narrated by James Cronin. The New York Times, February 26, 2023. https://www.nytimes.com/2023/02/26/podcasts/the-daily/elon-musk-tesla-self-driving.html.
    
[^17]:  Furthermore, they believe that the duty itself must be the motivation for the act. For more on Duty Ethics see “BBC - Ethics - Introduction to Ethics: Duty-based Ethics,” n.d. [https://www.bbc.co.uk/ethics/introduction/duty\_1.shtml](https://www.bbc.co.uk/ethics/introduction/duty_1.shtml).
    
[^18]:  Vincenti, Alexander. “Hero or Thief: Evaluating the Morality of Robin Hood’s Actions.” The Glen Echo, May 25, 2021. [https://theglenecho.com/2021/05/25/hero-or-thief-evaluating-the-morality-of-robin-hoods-actions/](https://theglenecho.com/2021/05/25/hero-or-thief-evaluating-the-morality-of-robin-hoods-actions/). \[Accessed 31 July 2024\]
    
[^19]:  Mattei, Luca, Francesca Morpurgo, Carmela Occhipinti, Lorenzo Maria Ratto Vaquer, and Tetiana Vasylieva. “Self-Sovereign Identity Model: Ethics and Legal Principles.” _Digital Society,_ vol. 3, no. 2 (June 7, 2024). https://doi.org/10.1007/s44206-024-00113-2.
    
[^20]:  Kiser, https://doi.org/10.55621/idpro.105.
    
[^21]:  Women in Identity. “Code of Conduct: The Human Impact of Identity Exclusion,” n.d. [https://www.womeninidentity.org/cpages/code-of-conduct](https://www.womeninidentity.org/cpages/code-of-conduct). \[Accessed 31 July 2024\]
    
[^22]:  Renieris, Elizabeth M. _Beyond Data: Reclaiming Human Rights at the Dawn of the Metaverse_. MIT Press, 2023.
    
[^23]:  Identified in this study https://pure.tudelft.nl/ws/portalfiles/portal/136174101/soups2022\_korir.pdf and in one Member States’ political debates (the Netherlands) [https://www.tweedekamer.nl/kamerstukken/detail?id=2024Z03994&did=2024D09367](https://www.tweedekamer.nl/kamerstukken/detail?id=2024Z03994&did=2024D09367) and [https://open.overheid.nl/documenten/ronl-0662761f27b090409a5b68476bf4e550c69c9562/pdf](https://open.overheid.nl/documenten/ronl-0662761f27b090409a5b68476bf4e550c69c9562/pdf).
    
[^24]:  Wong, Julia Carrie. “The Cambridge Analytica Scandal Changed the World – but It Didn’t Change Facebook.” _The Guardian_, March 19, 2019. [https://www.theguardian.com/technology/2019/mar/17/the-cambridge-analytica-scandal-changed-the-world-but-it-didnt-change-facebook](https://www.theguardian.com/technology/2019/mar/17/the-cambridge-analytica-scandal-changed-the-world-but-it-didnt-change-facebook)
    
[^25]:  Jones, M. Tim. “Machine learning and bias.” IBM Developer, August 27, 2019. [https://developer.ibm.com/articles/machine-learning-and-bias/](https://developer.ibm.com/articles/machine-learning-and-bias/). \[Accessed 31 July 2024\]
    
[^26]:  Henkmarsman. “Principles and Codes of Conduct.” ThroughIdentity - Henk Marsman, March 23, 2023. [https://henkmarsman.wordpress.com/2023/03/23/principles-and-codes-of-conduct/](https://henkmarsman.wordpress.com/2023/03/23/principles-and-codes-of-conduct/).
    
[^27]:  Whitley, Edgar A., and Emrys Schoemaker. “On the Sociopolitical Configurations of Digital Identity Principles.” _Data & Policy_ 4 (2022): e38. [https://doi.org/10.1017/dap.2022.30](https://doi.org/10.1017/dap.2022.30).
    
[^28]:  Wikipedia. 2024. "DDT." Wikimedia Foundation. Last modified July 23, 2024. https://en.wikipedia.org/wiki/DDT.
    
[^29]:  Friedman, Batya. “Value-sensitive Design.” _Interactions_ 3, no. 6 (December 1, 1996): 16–23. [https://doi.org/10.1145/242485.242493](https://doi.org/10.1145/242485.242493).
    
[^30]:  ECP | Platform Voor De InformatieSamenleving. “Guidance Ethics Approach - ECP | Platform Voor De InformatieSamenleving,” February 28, 2022. https://ecp.nl/publicatie/guidance-ethics-approach/.
    
[^31]:  B2B International. “What Is the Value Proposition Canvas? - B2B International,” March 7, 2024. [https://www.b2binternational.com/research/methods/faq/what-is-the-value-proposition-canvas/](https://www.b2binternational.com/research/methods/faq/what-is-the-value-proposition-canvas/).
    
[^32]:  Reijers, Wessel, Kevin Koidl, David Lewis, Harshvardhan J. Pandit, and Bert Gordijn. “Discussing Ethical Impacts in Research and Innovation: The Ethics Canvas.” In _IFIP Advances in Information and Communication Technology_, 299–313, 2018. [https://doi.org/10.1007/978-3-319-99605-9\_23](https://doi.org/10.1007/978-3-319-99605-9_23).
    
[^33]:  British Columbia, Ministry of Technology, Innovation and Citizens’ Services. “DIGITAL SERVICES CONSULTATION: Fall 2013 | Minister’s Response.” _govTogetherBC_, March 2014. [https://engage.gov.bc.ca/govtogetherbc/engagement/digital-services-consultation-results/](https://engage.gov.bc.ca/govtogetherbc/engagement/digital-services-consultation-results/).
    
[^34]:  Ethisphere | Good. Smart. Business. Profit.®. “World’s Most Ethical Companies - Ethisphere | Good. Smart. Business. Profit.®,” May 3, 2024. [https://ethisphere.com/worlds-most-ethical-companies/](https://ethisphere.com/worlds-most-ethical-companies/). \[Accessed 31 July 2024\]
