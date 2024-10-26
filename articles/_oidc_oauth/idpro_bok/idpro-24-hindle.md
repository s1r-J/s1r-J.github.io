---
layout: columns
title: Impact of GDPR on Identity and Access Management
permalink: /docs/oidc_oauth/idpro_bok/24
date: 2024-09-09
modify_date: 2024-10-27
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "GDPR"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/24/](https://bok.idpro.org/article/id/24/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

This article examines the implications of the General Data Protection Regulation (“GDPR”, “Regulation”) on Identity and Access Management (“IAM”) process and system design. It introduces organisational and technical good practices that may help ensure demonstrable compliance with the Regulation as well as improve user experience and customer trust.

Although the focus here is on the GDPR, the approaches described may, by extension, also help in complying with data protection legislation in other geographies including (for example) the California Consumer Privacy Act (“CCPA”), or the Brazilian General Data Protection Law (“LGPD”).

Keywords: GDPR, privacy, CCPA, LGPD

@column
## 概要

この記事では一般データ保護規則（「GDPR」、「Regulation」）がアイデンティティとアクセス管理（「IAM」）プロセスおよびシステム背系に与える影響について検討します。また、同規制への模範的な準拠およびユーザーエクスペリエンスと顧客の信頼を向上させるのに役立つ組織的・技術的なグッドプラクティスを紹介します。

ここではGDPRに焦点をあてますが、（例えば）カリフォルニア州消費者プライバシー法（「CCPA」）やブラジル一般データ保護法（「LGPD」）など、他の地域のデータ保護法を遵守する際にも、説明したアプローチが役立つ可能性があります。

Keywords: GDPR, プライバシー, CCPA, LGPD

@row
Andrew Hindle (CIPP/E, CIPM, CIPT)

© 2020 Andrew Hindle and IDPro

@row
## A Word to the Reader

We assume at least a basic knowledge of data protection and privacy - in particular, the GDPR [^1] and the basic principles outlined in the OECD privacy guidelines [^2] . Even if you are not a security or privacy officer in your organization, understanding the rules will help you have better conversations with your privacy peers.

The privacy regulation landscape is evolving rapidly. Hence, the advice given here cannot be comprehensive and is neither intended nor should be considered as a substitute for legal advice. Whilst a good awareness of and sensitivity to privacy considerations is important for the digital identity professional, the majority of professionals are unlikely to be privacy lawyers. As with any area of regulation, it is always best to seek professional advice if at all uncertain.

Throughout the article, specific ‘good technical practice’ advice will be _underlined; this same advice is also collated into a separate section at the end of the article_ as a checklist to follow for good IAM practices.

@column
## 読者に一言

データ保護とプライバシー、特にGDPR [^1] とOECDプライバシーガイドライン [^2] に概説されている基本原則について、少なくとも基本的な知識を有していることを前提としています。あなたが組織のセキュリティやプライバシーの責任者でなくても、この規則を理解することでプライバシー担当の同僚とより良い会話ができるようになります。

プライバシーに関する規制の状況は急速に変化しています。したがって、ここで示す助言は包括的なものでも、法的助言の代用とすることを意図したり、そのように考えたりすることができるものでもありません。デジタル・アイデンティティの専門家にとって、プライバシーの考慮事項に対する充分な認識と感受性は重要ですが、専門家の大半はプライバシー専門の弁護士である可能性は低いです。どのような規制の分野でも、少しでも不明確なことがあるならば常に専門家の助言を求めるのが最善です。

この記事の中では、具体的な「優れた技術的実践」の助言に __下線が引かれています；この同じ助言は、記事の最後の別のセクションにまとめられ、__ 優れたIAM実践のためのチェックリストとしています。

@row
## Introduction

Privacy conventions, regulations, and laws have been in existence for much longer than most people realise. [^3] As far back as 1948, the United Nations General Assembly enshrined a right to privacy in Article 12 of the Universal Declaration of Human Rights. [^4] In 1980, the OECD issued its “Guidelines on the Protection of Privacy and Transborder Flows of Personal Data,” [^5] which were significantly revised and updated in 2013 (q.v.).

Individual countries and broader trading blocs continue to evolve their data protection and privacy regulations, in part to account for the evolution of technology. It is not uncommon for regulatory frameworks to lag behind technological developments, but changes will continue to be made in light of the impact that the Internet, connected devices, artificial intelligence, and genomics bring. To add to the complexity, the greater global mobility of individuals suggests that the local changes to data protection and privacy regulation impact changes in other jurisdictions. Aside from the changes in Europe, recent years have seen updated privacy regulations emerge in Brazil, Singapore, the Philippines, China, and parts of the United States, to name a few.

This evolution of regulation is important. When viewed through the lens of an ever-changing and evolving regulatory landscape, we can see the GDPR (and other modern privacy regulations) as a set of tools that can help us build better systems, not just as a set of checkboxes that we need to mark off.

Even if you work for an organisation that does not directly do business with Europe, certain elements of the GDPR have a global impact. Other privacy regulations may contain similar provisions; although it would be unwise today to plan for global harmonisation of these regulations, there are increasing commonalities between geographies. Recognize, too, that the GDPR applies equally to any data about individuals, whether it is data within a company about its employees or data about external individuals such as customers. In other words: the GDPR really does affect everyone.

The Regulation includes [^6] a Data Protection by Design requirement. Leaving aside the specific need to comply with the Regulation, these are fundamentally good design principles. They help mitigate business risk (e.g., the less data you have, the less interesting you are to attack, and the less impact any attack will have), and they help reduce administrative overhead and wasted effort (e.g., the less data you have, the less likely it is that you will have duplication or contradictory records).

By definition, since the GDPR is concerned with personal data, these principles have significant implications for how we design and implement systems that use such data, including IAM systems and processes. Indeed, without an IAM foundation which itself complies with the Regulation, it’s simply not possible for a final product to be compliant. (Though note that even if your IAM systems and processes themselves are Regulation-ready, you still need to ensure that your final service is compliant as well!)

The rest of this article will explore the principal considerations teams should have when developing IAM projects that can comply with the needs of the Regulation.

The Regulation applies to the physical representation of data (such as on paper) as much as it does to digital data. We’ll focus here on digital information, but we’ll make reference where appropriate to some specific implications (for example, in the areas of debugging, management reporting and so on.)

We’ll start with some general observations, including commentary on your project team’s composition and project structure. Then we’ll focus on the four stages that data - including Personal Data - goes through during its lifecycle: create, read, update, and delete. For each of these stages, we’ll reference some of the specific areas of the GDPR that apply and identify some architectures, tools, and techniques which can help. Where relevant, we’ll note differences that might apply if you are a ‘data controller’ or a ‘data processor’ - but for the most part, the impact of these differences is more likely to be at the business/legal level, rather than the technical level. We’ll finish with a summary of key takeaways that can also be used as a quick aide-memoire for future projects or team induction.

@column
## 導入

プライバシーに関する規約、規制および法律は、ほとんどの人が認識しているよりもはるかに長く存在しています。 [^3] 1948 年にさかのぼると、国連総会は世界人権宣言の第12条にプライバシーの権利を明記しました。 [^4] 1980年、OECDは「プライバシーの保護と個人データの越境フローに関するガイドライン」 [^5] を発行し、これは2013年に大幅に改訂および更新されました (q.v.)。

個々の国やより広い貿易ブロックは、テクノロジーの進化に対する責任のため、データ保護とプライバシーの規制を進化させ続けています。規制の枠組みが技術開発に遅れをとることは珍しくありませんが、インターネット、接続されたデバイス、人工知能、ゲノミクスがもたらす影響を考慮して、変更は引き続き実施されます。さらに複雑なことに、個人のグローバルな移動性が高いことは、データ保護とプライバシー規制に対する地域内での変更が他の法域の変更に影響を与えることを示唆します。ヨーロッパでの変化は別として、近年、ブラジル、シンガポール、フィリピン、中国および米国の一部で、最新のプライバシー規制が登場しています。

この規制の進化は重要です。絶え間なく変化し進化する規制環境のレンズを通して見ると、GDPR（およびその他の最新のプライバシー規制）は、単にマークをつける必要があるだけのチェックボックスではなく、より良いシステムを構築するのに役立つ一連のツールとして見ることができます。

ヨーロッパと直接取引をおこなっていない組織で働いている場合でも、GDPRの特定の要素はグローバルな影響を及ぼします。他のプライバシー規則には、同様の規定が含まれる場合があります；今日、これらの規制のグローバルな調和を計画することは賢明ではありませんが、地域間の共通点は増えています。GDPRは、企業内の従業員に関するデータであろうと、顧客などの外部の個人に関するデータであろうと、個人に関するあらゆるデータに等しく適用されることも認識してください。つまり、GDPRは本当にすべての人に影響を与えます。

GDPRには [^6] 「データプロテクション・バイ・デザイン」の要件が含まれています。GDPRに準拠するという特定の必要性は別として、これらは基本的に優れた設計原則です。それらはビジネスリスクを軽減するのに役立ち (たとえば、保有するデータが少ないほど、攻撃に対する関心が低くなり、攻撃による影響が小さくなります)、管理上のオーバーヘッドと無駄な労力を削減するのに役立ちます（たとえば、保有するデータが少なくなり、 重複または矛盾する記録が発生する可能性が低くなります）。

定義上、GDPRは個人データに関係しているため、これらの原則はIAMシステムやプロセスなど、そのようなデータを使用するシステムを設計および実装する方法に大きな影響を与えます。実際、IAM基盤自体がGDPRに準拠しなければ、最終製品を準拠させることは不可能です。（ただし、IAMシステムとプロセス自体がGDPRに対応している場合でも、最終的なサービスも準拠していることを確認する必要があります！）

この記事の残りの部分では、GDPRのニーズに準拠できるIAMプロジェクトを開発する際にチームが考慮すべき主な考慮事項について説明します。

GDPRは、デジタルデータと同様に、データの物理的表現（紙など）にも適用されます。ここではデジタル情報に焦点を当てますが、必要に応じていくつかの特定の意味を参照します（たとえば、デバッグ、管理レポートなどの領域）。

プロジェクトチームの構成とプロジェクト構造に関するコメントを含む、いくつかの一般的な観察から始めます。 次に、データ（個人データを含む）がライフサイクル中に通過する4つの段階（作成、読み取り、更新、削除）に焦点を当てます。これらの各段階でGDPRの特定の領域を参照し、適用されるアーキテクチャ、ツールおよびテクニックを特定します。必要に応じて、「データ管理者」または「データ処理者」である場合に適用される可能性のある相違点を記載しますが、ほとんどの場合、これらの相違点の影響は技術レベルよりもビジネス/法務レベルにある可能性が高いです。最後に、将来のプロジェクトやチームの導入のための簡単な備忘録としても利用できる重要なポイントの要約で締めくくります。

@row
### Terminology

*   Data Mapping – “a system of **cataloguing what data you collect** , how it’s used, where it’s stored, and how it travels throughout your organization and beyond.” [^7]
    

*   Data Protection Officer (“DPO”) – An individual who must be appointed in any organization that processes any data defined by the GDPR as sensitive. [^8] The DPO is responsible for “Working towards the compliance with all relevant data protection laws, monitoring specific processes, such as data protection impact assessments, increasing employee awareness for data protection and training them accordingly, as well as collaborating with the supervisory authorities.”(See GDPR Articles 35, 37, 38, and 39 for more detail)
    
*   Personal Data - Personal data are any information which are related to an identified or identifiable natural person. [^9] (See GDPR Article 4 (1) for more detail.)
    
*   Data Protection by Design - data protection through appropriate technology and organizational measures. [^10] See GDPR Article 25 for more detail.
    

@column
### 用語解説

*   データマッピング – 「 **どのデータを収集し、どのように使用し、どこに保存し、どのように組織内外に移動するかをカタログ化する** システム。」 [^7]
    

*   データ保護責任者（「DPO」） - GDPRによって機密として定義されたデータを処理する組織で任命されなければならない個人。 [^8] DPOは、「関連するすべてのデータ保護法の遵守に向けて取り組み、データ保護の影響評価などの特定のプロセスを監視し、データ保護に対する従業員の意識を高め、トレーニングをおこない、監督当局と協力する」ことを担当しています。（詳細については、GDPRの第35、37、38および39条を参照してください）
    

*   個人データ - 個人データとは、識別された、または識別可能な自然人に関連するあらゆる情報です。 [^9] （詳細については、GDPR 第4条(1)を参照してください。）
    
*   データプロテクション・バイ・デザイン - 適切な技術と組織的手段によるデータ保護。 [^10] 詳細については、GDPR第25条を参照してください。
    

@row
## General Observations

@column
## 一般的な観察

@row
### Collaboration with Privacy Advisors

With the principles of Data Protection by Design and Default, as defined by Article 25 of the GDPR, in mind, perhaps the most critical action you can take is to _ensure that privacy requirements are considered at the very start_ of any project.

The GDPR requires many (but not all) organisations to have an appointed Data Protection Officer (“DPO”). Larger organisations may have a team of privacy advisors. If you’re leading a project that involves data about individuals, it is your responsibility to make sure your privacy colleagues are involved. Make sure you _involve the relevant people in your project at the very earliest stage_ . Remember that they may not know about your project unless you tell them! Even if you are not, don’t be afraid to ask who is involved from a privacy standpoint, and then develop a working relationship with your advisor.

Your privacy specialist (if you do not have an experienced DPO) may not have a deep technical background, so you’ll need to make sure you are providing them with the information they need in a format that makes sense to them so that they can provide complete and comprehensive advice. To make conversations more productive and efficient, consider doing additional privacy reading or even investigating publicly recognised qualifications or certifications from relevant privacy trade bodies or other institutions as part of your ongoing professional development.

@column
### プライバシーアドバイザーとの連携

GDPRの第25条で定義されているように、データプロテクション・バイ・デザインおよびバイ・デフォルトの原則を念頭に置いて、おそらく最も重要なアクションは、プロジェクトの __まさに開始時にプライバシー要件が確実に考慮されるようにすることです__。

GDPRでは、多くの (ただしすべてではない) 組織に、任命されたデータ保護責任者（「DPO」）が必要です。大規模な組織には、プライバシーアドバイザーのチームを有しているかもしれません。あなたが個人に関するデータを扱うプロジェクトを主導している場合、同僚がプライバシーに関与していることを確認するのはあなたの責任です。 __非常に初期の段階で、関係者をプロジェクトに参加させる__ ようにしてください。あなたが彼らに言わない限り、彼らはあなたのプロジェクトについて知らない可能性があることを忘れないでください！あなたが主導していない場合でも、プライバシーの観点から誰が関与しているかを恐れずに尋ねてから、アドバイザーと協力関係を築いてください。

プライバシースペシャリスト（経験豊富なDPOがいない場合）は深い技術的なバックグラウンドがない可能性があるため、必要な情報を彼らにとって意味のある形式で提供するようにする必要があり、そうすることで彼らは完全かつ包括的なアドバイスを提供してくれます。会話をより生産的かつ効率的にするために、継続的な専門能力開発の一環として、追加のプライバシーリーディングをおこなったり、関連するプライバシー取引団体やその他の機関から公的に認められた資格や認定を調査したりすることを検討してください。

@row
### Raising Concerns/Whistleblowing

If you are worried that your project or your organisation isn’t taking privacy seriously enough, or if you think you’ve identified an issue that leaves you out of compliance with the GDPR, or - in the worst case - an actual data breach, make sure you know the right channels through which to report this. Larger organisations should have well-established reporting/escalation mechanisms and are also likely to have whistleblowing policies and processes which you can use as a last resort. Smaller organisations may not, and so you’ll need to use your best professional judgement to work out how to most effectively raise concerns. _**Do** keep good records of any such conversations_ but _**do not** include specific examples of Personal Data when reporting issues if it can be avoided_ , lest you make a data breach worse (or unwittingly turn a potential incident into an actual data breach!).

Finally, if your organisation has a DPO, remember that the GDPR imposes quite strict requirements on the independent relationship and reporting lines of the DPO. [^11] These can be helpful reassurances if you find you need to escalate.

@column
### 懸念事項の提起/内部告発

プロジェクトや組織がプライバシーに充分に真剣に取り組んでいないと心配している場合、GDPR準拠から逸脱している問題を発見したと思う場合あるいは最悪の場合、実際のデータ侵害が発生した場合、これを報告するための正しいチャンネルを知っていることを確認する必要があります。大規模な組織では報告/エスカレーションの仕組みが確立されているはずで、最後の手段として利用できる内部告発のポリシーやプロセスも持っている可能性があります。小規模な組織ではそうでない場合もあるため、専門家としての最善の判断によって最も効果的に懸念を表明する方法を見つける必要があります。 __そのような会話はきちんと記録を**おこないましょう**。しかし、問題を報告するさいに可能であれば特定の個人データの例を**含めないようにしましょう**。__ さまなければ、データ侵害を悪化させてしまいます（潜在的な事故を知らず知らずのうちに実際のデータ侵害に変えてしまうことになります！）。

最後に、組織にDPOがいる場合、GDPRはDPOの独立した関係と報告系統にかなり厳しい要件を課していることを忘れないでください。 [^11] これらは、エスカレーションが必要と判断された場合の安心材料になります。

@row
### Personal Data – Definition and Mapping

The GDPR has a very broad definition of what is considered to be personal data: “‘personal data'' means any information relating to an identified or identifiable natural person (‘data subject’); an identifiable natural person is one who can be identified, directly or indirectly, in particular by reference to an identifier such as a name, an identification number, location data, an online identifier or to one or more factors specific to the physical, physiological, genetic, mental, economic, cultural or social identity of that natural person.” [^12]

It is important, then, to be equally broad in your approach. Make sure you fully understand across the entire project when data might be considered to fall into the category of personal data. Remember that even if you are dealing with aggregated or pseudonimised data, the Regulation will still apply if that data can be ‘re-identified’.

Consider a process known as “data mapping” at the start of a project to _discover and map out what personal data might be used where and how_ and monitor and update this data map through the entire lifecycle of the project. Data mapping is “a system of **cataloguing what data you collect** , how it’s used, where it’s stored, and how it travels throughout your organization and beyond.” [^13] Such a process is often part of a data protection impact assessment (“DPIA”) but it can also be helpful in the overall design of your IAM architecture, so it’s never wasted effort.

@column
### 個人情報 - 定義とマッピング

GDPRは、何が個人データとみなされるかについて非常に幅広い定義を持っています：「『個人データ』とは識別された、もしくは識別可能な自然人（『データ主体』）に関するあらゆる情報を意味します；識別可能な自然人とは、氏名、識別番号、位置情報、オンライン識別子などの識別子、またはその自然人の身体的、生理的、遺伝的、精神的、経済的、文化的、社会的アイデンティティに固有の一つ以上の要素を参照して、直接的または間接的に識別できるものを指します。」 [^12]

そのためには、幅広いアプローチをとることが重要です。どのようなデータが個人情報の範疇に入るのか、プロジェクト全体で充分に理解しておく必要があります。集計または匿名化されたデータを扱う場合でも、そのデータが「再識別」可能であれば、この規則が適用されることを忘れないでください。

プロジェクト開始時に「データマッピング」と呼ばれるプロセスを検討し、 __どのような個人データがどこでどのように使用される可能性があるかを発見してマッピング__ し、プロジェクトのライフサイクル全体を通じてこのデータマップを監視・更新します。データマッピングとは、「 **どのようなデータを収集** し、どのように使用し、どこに保存し、組織内外でどのように移動するかを **カタログ化する** システム」です。 [^13] このようなプロセスは、しばしばデータ保護影響評価（「DPIA」）の一部としておこわれますが、IAMアーキテクチャの全体設計にも役立つため、決して無駄な作業ではありません。

@row
### Individual tracking technologies

The use of individual tracking technologies including, but not limited to, cookies, is (at the time of writing) requires more than just the GDPR to consider if a service or website includes their use. [^14] Each EU member state is responsible for issuing its own guidance in line with this directive, which has led to some important divergence in this area; case law is still evolving.

Some cookies can, however, fall under the GDPR - if, for example, they contain information which could be used (perhaps in conjunction with other data) to identify an individual. Hence, although perhaps not a core consideration for the IAM practitioner, it is worth being aware of and alert to potential issues in this area.

@column
### 個人トラッキング技術

Cookieに限らず、個人トラッキング技術の使用は、（本稿執筆時点では）GDPR以上にサービスやウェブサイトにその利用が含まれているかどうかを検討する必要があります。 [^14] EUの各加盟国は、この指令に沿って独自のガイダンスを発行する責任があり、そのためこの分野では重要な乖離が生じています；判例法はまだ進化している最中です。

ただし、一部のCookieは、例えば個人を特定するために利用できる情報（おそらく他のデータと組み合わせることによる）が含まれている場合、GDPRに該当します。したがって、IAMの実務者にとって重要な検討事項ではないかもしれませんが、この分野の潜在的な問題を認識し、注意を喚起することは価値があります。

@row
### Special Circumstances

The guidance given in this article is intended to be generally applicable to all IAM projects. Some projects, however, will have particular circumstances which merit additional care and consideration. Some of these circumstances include children, law enforcement, and certain special category data. In all cases, practitioners should seek independent legal guidance.

@column
### 特殊な事情

この記事に記載されているガイダンスは、すべてのIAMプロジェクトに一般的に適用されることを目的としています。しかし、一部のプロジェクトには追加の注意と検討をおこなうに値する特殊な事情を持っていることがあります。これらの事情には、子ども、法執行機関および特定の特殊なカテゴリのデータが含まれます。いずれの場合も、実務者は独立した法的ガイダンスを求める必要があります。

@row
#### Special Category and Other Sensitive Data

The GDPR makes special provision for certain more sensitive types of data, including (but not limited to) race, sexual orientation, political and religious affiliation, health related data and biometric data. [^15] _If you are handling special category data in these areas, you will need additional safeguards._

@column
#### 特殊なカテゴリとその他の機密データ

GDPRは人種、性的指向、政治的および宗教的帰属、健康関連データ、生体認証データを含む (ただしこれらに限定されない) 特殊な、より機密性の高い類いのデータに対して特別な規定を設けています。 [^15] __これらの領域で特殊カテゴリのデータを処理している場合は、追加の保護が必要になります。__

@row
#### Children

_If your project involves data about Children, you will also need to take special care._ The GDPR defines a Child as being below the age of 16 - but note that individual countries may (and some, including the UK, have) lower this limit to the age of 13 or below [^16] .

@column
#### 子ども

__プロジェクトに子どもについてのデータが含まれている場合、特別な注意を払う必要があります。__ GDPRでは、子供を16歳未満と定義していますが、国によってはこの制限を13歳以下に引き下げる場合があること（英国を含む一部の国ではそのようになっています）に注意してください [^16] 。

@row
#### Law Enforcement and Personal Data

The use of personal data by law enforcement agencies is the subject of separate directives, regulations and laws; these are not considered in this article.

@column
#### 法執行機関と個人データ

法執行機関による個人データの利用は、個別の指令、規制、法律の対象となります；これらについては、この記事では考慮しません。

@row
### Automated Processing, Machine Learning, and Artificial Intelligence

The automated processing of personal data is a special circumstance in its own right, but one which merits a particular level of attention. Automated processing can include everything from machine learning (“ML”), algorithmic processing, the use of blockchain technologies, or artificial intelligence (“AI”). AI/ML, in particular, is a fast-moving field; developers, ethicists, lawmakers, and regulators worldwide and still trying to gauge the complete scope of what might be possible. It is already clear that AI/ML systems can infer or deduce ‘facts’ about individuals that were not part of the original data set (we often see this in user profiling). It’s also clear that an original data set might not itself contain personal data (by definition) but can do once processed.

It’s beyond the scope of this article to explore this area in any depth; the GDPR, however, imposes quite stringent requirements in the case of Automated Decision-Making and Profiling. [^17]

@column
### 自動処理、機械学習、人工知能

個人データの自動処理は、それ自体が特別な状況ですが、特別なレベルの注意が必要です。自動化された処理には、機械学習（「ML」）、アルゴリズム処理、ブロックチェーンテクノロジの使用、または人工知能（「AI」）のすべてが含まれます。特にAI/MLは急速に変化する分野です；世界中の開発者、倫理学者、立法者および規制当局は、（AI/MLが）できることの完全な範囲を測ろうとしています。AI/MLシステムが、元のデータセットの一部ではなかった個人に関する「事実」を推測または推定できることは既に明らかです（これは、ユーザープロファイリングでよく見られます）。また、元のデータセット自体には（定義上では）個人データが含まれていない可能性がありますが、処理されると含まれる可能性があることも明らかです。

この領域を深く掘り下げることは、この記事の範囲を超えています；しかし、GDPRは、自動化された意思決定とプロファイリングについて非常に厳しい要件を課しています。 [^17]

@row
### Greenfield/Brownfield [^18]

GDPR itself makes no distinction between greenfield applications and the refactoring of existing – ‘Brownfield’ – applications to bring them up to a state of compliance. From a practical standpoint, the former affords an easier path to using modern standards and techniques and is often less encumbered with legacy integration/support requirements.

Recognise, however, that GDPR compliance may drive you to review all the applications in your project’s working environment. In some cases, there will be (more or less) simple technical or procedural solutions to achieve compliance. In others, however, you may need to revisit and revise the original business objectives in the light of the Regulation.

@column
### グリーンフィールド/ブラウンフィールド [^18]

GDPR自体は、グリーンフィールドアプリケーションと、既存の「ブラウンフィールド」アプリケーションをリファクタリングして準拠状態にすることを区別していません。現実的な観点からは、前者の方が最新の標準や技術を利用しやすく、レガシー統合やサポートの要件に縛られにくいことが多いようです。

ただし、GDPRの遵守により、プロジェクトの作業環境にあるすべてのアプリケーションを見直す必要が生じる可能性があることを認識しておいてください。場合によっては、コンプライアンスを達成するための（多かれ少なかれ）単純な技術的または手続き的なソリューションが存在することでしょう。しかし、GDPRに照らして当初のビジネス目標を再検討し、修正する必要がある場合もあります。

@row
### Proxy/Delegated Access

This article makes a general assumption that a data subject will be providing and/or accessing data about themselves. That said, there is naturally a variety of cases where someone might quite legitimately be accessing data on behalf of a third party.

In such circumstances, it is crucial to establish and apply appropriate mechanisms of authentication, identification, and authorisation (as recommended variously later in this article) both for the original data subject and for their proxy, along with delegation consent. In some circumstances, consent can arise via legal instruments such as a power of attorney, a court order, or similar. Establish whether this is a requirement for your use-case and design processes accordingly. You should also strongly consider _maintaining a record of delegation consent and other authorisation actions_ where applicable. Standards such as UMA [^19] and Consent Receipt [^20] may help in this regard.

@column
### 代理/委任アクセス

この記事では、データ対象者が自分自身に関するデータを提供および／またはアクセスすることを一般的に想定しています。とはいえ、当然ながら、第三者の代理として正当にデータにアクセスしている人がいるかもしれないなど、様々なケースが存在します。

このような状況では、元のデータ対象者とその代理人の両方に、委任による同意とともに、認証、本人確認および認可の適切な仕組み（この記事の後半で様々な形で推奨されている）を確立し適用することが極めて重要です。状況によっては、委任状、裁判所命令などの法的手段によって同意が得られる場合があります。このような同意がユースケースの要件に一致するかどうかを確認し、それに応じてプロセスを設計してください。また、委任による同意やその他の権限付与の記録を保持することを強く検討する必要があります （該当する場合）。UMA [^19] やConsent Receipt [^20] などの標準規格は、この点で役に立つかもしれません。

@row
### Backups

Having a reliable mechanism to secure your data in the event of a disaster is not only good general practice, it is also, essentially, required by the GDPR. Remember, though, that a poorly designed backup mechanism can potentially put you at greater risk of a breach. Ensure that data in any backup is protected with strong encryption and with other tools including, but not limited to, privileged access/user management – though be aware that these protections can complicate the restoration process. Certain sectors or applications may also require a physical or paper-based backup mechanism. Whilst this is likely to be outside of the immediate scope of responsibility of the digital identity professional, do bear in mind that the GDPR requirements apply equally to data in physical form. Backups also introduce additional complexity in the area of retention.

@column
### バックアップ

災害時にデータを保護するための信頼できるメカニズムを持つことは、一般的な慣行として優れているだけでなく、基本的にGDPRでも義務付けられています。しかし、バックアップの仕組みが不十分だと、情報漏洩のリスクが高まる可能性があることに留意してください。バックアップのデータは、強力な暗号化、特権アクセス/ユーザー管理などのツールで保護されていることを確認してください（ただし、これらの保護は復元プロセスを複雑にする可能性があることに留意してください）。特定の分野やアプリケーションでは、物理的または紙ベースのバックアップメカニズムが必要な場合があります。これはデジタルアイデンティティ専門家の直接的な責任範囲外である可能性が高いですが、GDPRの要件は物理的な形態のデータにも同様に適用されることを念頭に置いておいてください。バックアップは、保存の領域でさらなる複雑さをもたらします。

@row
### Data Journey

@column
### データ・ジャーニー

@row
#### Step One - Create

The first stage of our data journey - ‘create’ - starts at the moment you set out to collect personal data. Do not confuse this with the moment you write the data into a database (or other storage mechanism). Before you even request data from (or about) the data subject, you need to clearly understand and communicate to them what you are collecting and why, along with outlining their data subject rights. These are most commonly expressed via a privacy notice that uses clear and plain language - and you should at least _ensure that the notice accurately reflects the way your system actually works!_

Depending on the lawful basis for processing the relevant data, you may need to obtain _the consent of the data subject for you to collect and process their information_ . How you obtain consent will differ from project to project, depending on what data is being collected and what it is being used for. Your privacy advisor can provide guidance.

From an audit perspective, consider _keeping a record of that consent and/or providing your data subject with a record for themselves_ \- evolving standards such as the _Consent Receipt_ may be applicable here. Do remember, though, that any such receipt or record may itself contain Personal Data!

@column
#### ステップ1 - 作成

データの流れの最初の段階である「作成」は、個人データの収集に着手した時点から始まります。これは、データをデータベース（またはその他のストレージメカニズム）に書き込む瞬間と混同しないでください。データ対象者から（またはデータ対象者について）データを要求する前に、データ対象者の権利の概要を説明するとともに、収集する内容とその理由を明確に理解し、データ対象者に伝達する必要があります。これらは、明確でわかりやすい言葉を使ったプライバシー通知で表現するのが最も一般的です。少なくとも、__あなたのシステムが実際に機能する方法を、通知が正確に反映していることを確認するべきです！__

関連データを処理するための法的根拠によっては、 __データ対象者の情報を収集および処理するために、データ対象者の同意を得る__ ことが必要な場合があります。同意を得る方法は、収集するデータの種類と使用目的によって、プロジェクトごとに異なります。プライバシー・アドバイザーが指導をおこなうことができるでしょう。

監査上の観点から、 __同意の記録を保持すること、および/またはデータ対象者自身にその記録を提供すること__ を検討する必要があります（「 __同意の受領証__ 」などの進化した標準が、ここで適用できるかもしれません）しかし、そのような受領証や記録自体に個人データが含まれている可能性があることを忘れないでください！

@row
##### Create Minimally

If Data Protection by Design and Default formed the first guiding principle for your project, then your second guiding principle should be that of Data Minimisation. Data minimisation is good practice irrespective of compliance requirements: the less you collect or process, the less you have to protect and manage over time. It is also one of the 7 principles established by the GDPR for the handling of personal data. [^21]

The bottom line: When collecting data from a data subject, _collect and keep **as little data as you possibly can**_ in order to meet your requirements. Similarly, for indirect data about a data subject, such as browser fingerprints, [^22] collect and keep as little data as you possibly can. This means you need to have a good understanding of the business rationale for the project, so that you are clear about the justification and so that you can help your colleagues on the business side meet their obligations: it’s always helpful to ask _why_ a given piece of information needs to be collected.

Remember that the GDPR considers data in the aggregate. Consider whether there is any possibility of data your project is collecting being combined with other data the organisation holds in such a way as might result in identification of the individual (see also ‘read’ below). _Avoid repeat collection of data_ that your organisation already holds about an individual. Aside from being a frustrating experience for the user, this also results in duplicate and/or conflicting records, which can cause problems with data accuracy, subject access requests, deletion, and other areas of the Regulation. If you have a large and disparate data map, _consider using data discovery or meta-directory tools to help with visibility and consolidation_ .

Bear in mind that you may be collecting _implicit_ or inferred data, which may also qualify as personal data: IP addresses, for example, or system analytics. These will need handling with the same diligence as data you _explicitly_ request from or on behalf of a data subject. Even if this data is collected and used on a transient basis, it still needs handling correctly.

Consider also creative ways to limit the amount of data you collect. Besides simply collecting less, an organization might use an attribute service for answers to questions such as ‘is the data subject over the age of 18’, instead of collecting and storing the subject’s date of birth, or requiring them to disclose credit card information. Technologies which can provide evidence that an authority has knowledge of certain information without revealing the information itself — zero-knowledge proof [^23] , for instance — is also worth investigation. Be aware, however, that existing legal requirements may not yet take such technologies into account.

As noted earlier, this article mainly considers the impact of the GDPR on digital identity. However, the moment of data collection/creation is often where paper-based processes occur. Even if these are not your direct concern, it’s no bad thing to make sure you understand how any paper records are being processed.

@column
##### 最小限の作成

データプロテクション・バイ・デザイン・アンド・デフォルトがプロジェクトの第一の指針であるとすれば、第二の指針はデータの最小化であるべきです。データの最小化は、コンプライアンス要件に関係なく、優れた実践方法です：収集や処理が少なければ少ないほど、長期にわたって保護・管理する必要が減ります。また、GDPRが定める個人情報の取扱いに関する7つの原則の一つでもあります。 [^21]

要は：データ対象者からデータを収集する場合、要件を満たすために __**できる限り少ないデータ**を収集し、保管すること__ ようにします。同様に、ブラウザの指紋 [^22] などデータ対象者に関する間接的なデータについても、できる限り少ない量のデータを収集し、保管するようにします。つまり、ビジネス上の根拠を明確にし、ビジネスサイドの同僚が義務を果たせるように、充分な理解が必要です。ある情報を収集する必要がある __理由を尋ねること__ は、常に役に立ちます。

GDPRはデータを総体として考えることを忘れないでください。プロジェクトが収集するデータが、組織が保有する他のデータと組み合わされ、個人を特定できる可能性があるかどうかを検討してください（以下の「読み取り」の段落も参照）。個人について組織がすでに持っている __データを繰り返し収集することは避けてください__ 。ユーザーにとってフラストレーションが溜まるだけでなく、記録の重複および/または矛盾が生じ、データの正確性、対象者へのアクセス要求、削除など、GDPRの他の領域で問題を引き起こす可能性があります。大規模でバラバラのデータマップを使用している場合は、 __データ・ディスカバリー・ツールやメタディレクトリ・ツールを使用して、可視化と統合をおこなうことを検討してください__ 。

__暗黙的__ または推論的なデータを収集している場合、それが個人データとして認定される可能性があることを念頭に置いてください：例えば、IPアドレスやシステム分析などです。これらのデータは、データ対象者から __明示的__ に要求されたデータ、またはデータ対象者の代わりに要求されたデータと同じように、慎重に取り扱う必要があります。このようなデータは、たとえ一時的に収集され使用されるとしても、正しく取り扱う必要があります。

また、収集するデータの量を制限するための創造的な方法も検討してください。例えば、データ対象者の生年月日を収集・保存したり、クレジットカード情報を開示させたりする代わりに、「データ対象者は18歳以上か」といった質問に対する回答として属性サービスを利用することが考えられます。情報そのものを明らかにすることなく、ある当局が特定の情報を知っていることを証明できる技術、例えばゼロ知識証明 [^23] も検討に値します。ただし、既存の法的要件では、このような技術はまだ考慮されていない可能性があることに注意が必要です。

先に述べたように、この記事では主にGDPRがデジタル・アイデンティティに与える影響について考察しています。しかし、データの収集/作成の瞬間は、紙ベースのプロセスが発生することが多いです。これらが直接の関心事でないとしても、紙の記録がどのように処理されているかを理解しておくことは悪いことではありません。

@row
##### Possibilities for Federation

Having dealt with the basics, you now need to ask an important question: does your use-case actually need full user account creation. There is a tendency - born out of years of experience - to gravitate towards this as the first port of call in any identity project. Yet, in many cases, it’s unnecessary; or it’s something that only becomes needed later in the customer journey. Established _standards like SAML or OpenID Connect_ support transient identity federation; this is often all you need. In such a case, you are only handling personal data (if at all) for a brief period of time, and so the normal data minimisation principles and precautions for data in transit may be sufficient. ( _use the most current version of TLS, plus additional specific data encryption as necessary_ )

If you do need a user account for technical reasons — session data persistence, for example — can it be made essentially ‘impersonal’ though the use of (for example) pseudonymous federation? Pseudonymisation allows for the user identity to be matched, using an identifier that cannot easily be associated with a known individual. Take care in this case, however: it can be possible to combine data in such a way as to re-identify the information, so defeating the purpose of pseudonymisation. Pseudononymous data is still considered personal data, and as such it must be considered against the requirements of the GDPR.

@column
##### フェデレーションの可能性

基本的なことを扱ったので、次に重要な質問をする必要があります：あなたのユースケースでは、実際に完全なユーザーアカウント作成が必要でしょうか。長年の経験から、アイデンティティ・プロジェクトの最初の段階として、この作業に引き寄せられる傾向があります。しかし、多くの場合、これは不要であり、カスタマージャーニーの後半で初めて必要となるものです。 __SAMLやOpenID Connectのような確立された標準仕様__ は、一時的なアイデンティティ・フェデレーションをサポートしています；多くの場合、必要なものはこれだけです。このような場合、個人データを扱うのは短期間なので、通常のデータ最小化の原則と転送中のデータに対する予防措置で充分な場合があります。（ __TLSの最新バージョンを使用し、必要に応じて特定のデータの暗号化を追加しましょう__ ）

セッションデータの永続化など、技術的な理由でユーザーアカウントが必要な場合、例えば、仮名フェデレーションを使用して、本質的に「非人間的」にすることができるでしょうか？仮名化により、既知の個人と容易に関連付けることができない識別子を使用して、ユーザーIDを照合することができます。しかし、以下の場合に注意が必要です：情報を再識別するような方法でデータを組み合わせることが可能なため、仮名化の目的が達成されない可能性があります。仮名データは依然として個人データとみなされるため、GDPRの要件に照らして検討する必要があります。

@row
##### Storing Data

If you do find you need to persist data — whether pseudonymously or not — you will need to think about where and how you store the data. The usual protections for data at rest are important. U _se appropriate encryption techniques and keep these under routine review:_ cryptography is an area of rapid development (particularly given the advent of quantum cryptography and the evolution of ‘quantum-safe’ algorithms and techniques). You should also ensure that the right processes are in place to _keep supporting systems, applications, and libraries up to date and patched_ .

Other GDPR requirements notwithstanding, modern application design patterns will almost certainly lead you to provide an API for handling your personal data. In such cases, _access to such APIs must be protected, ideally using a protocol such as OAuth_ ; you could also _consider using an API gateway_ . We’ll come back to API protection again later in our data journey.

If you are considering a storage solution using a distributed ledger, you should take extra care. There is now clear consensus that _storing personal data directly in such a ledger is not good practice_ . Some solutions under development today may avoid this particular pitfall, but it is still worth bearing in mind, particularly if you are building your own. Until this area of technology is more stable, the best advice is to proceed with caution; to keep such projects under regular periodic review, even after deployment; and to ensure you have a well-documented and easily implemented _way to reverse out of using the ledger-based solution_ , should that become necessary.

Using a cloud-based data or user store may have benefits from a risk management and privacy perspective. Ensure that you work with your privacy team so that your privacy notice accurately reflects the relationship between you and your provider.

@column
##### データの保存

仮名であろうとなかろうと、データを永続化する必要がある場合は、データを保存する場所と方法について考える必要があります。静止しているデータに対する通常の保護が重要です。 __適切な暗号化技術を利用し、定期的な見直しを実施しましょう：__ 暗号技術は急速に発展している分野です（特に、量子暗号の出現と「量子安全」なアルゴリズムと技術の進化を考慮する必要があります）。また、 __サポートするシステム、アプリケーション、ライブラリを最新の状態に維持し、パッチを適用する__ ための適切なプロセスを確保する必要があります。

GDPRの他の要件はともかく、最新のアプリケーションのデザインパターンでは、個人データを扱うためのAPIを提供することはほぼ間違いないでしょう。このような場合、 __APIへのアクセスは保護されなければならず、理想的にはOAuthなどのプロトコルを使用することです__ ； __APIゲートウェイの使用も検討できます__ 。APIの保護については、データ・ジャーニーの後半で再び触れることにします。

分散型台帳を利用したストレージソリューションを検討している場合は、特に注意が必要です。 __このような台帳に個人データを直接保存するのは良い方法ではない__ 、というのが現在の明確なコンセンサスです。現在開発中のソリューションの中には、この落とし穴を回避できるものもありますが、特に自社で構築する場合は、念頭に置いておく価値があります。この分野の技術がより安定するまでは、慎重に進めることが最善のアドバイスです；つまり、そのようなプロジェクトを展開後も定期的に見直すこと、そして万一その台帳ベースのソリューションの使用を中止する必要が生じた場合に備えて、充分に文書化され容易に実装できる方法を確保しておきましょう。

クラウドベースのデータストアやユーザーストアを利用することは、リスクマネジメントやプライバシーの観点からメリットがある場合があります。個人情報保護チームと協力し、個人情報保護に関する通知があなたとプロバイダーの関係を正確に反映するようにしましょう。

@row
##### Location of Data Storage

The GDPR does not itself impose requirements of data territoriality – that is, it does not require that data be stored in a particular geography – though regulations in other jurisdictions do. You should, at the very least, _develop a flexible architecture that will allow you to segregate data on a regional basis_ should that become necessary — although bear in mind that this could mean collecting additional personal data which you might otherwise not need.

With that said, the GDPR **does** have requirements around the transfer of data outside of the European Union. The transfer of personal data to any Third Country must always be a significant concern in the context of GDPR, and – although solutions can certainly be devised – this is an area of ongoing regulatory development. You will need careful discussion with your privacy adviser to make sure this is being handled correctly.

@column
##### データを保存する場所

GDPR自体はデータの地域性の要件を課していません。つまり、データを特定の地域に保存することを要求していませんが、他の法域の規制ではそのようになっています。少なくとも、必要な場合は __地域ごとにデータを分離できるような柔軟なアーキテクチャを構築する__ 必要があります。ただし、この場合、他の地域では不要な個人データを追加で収集することになる可能性があることを念頭に置いてください。

とはいえ、GDPRにはEU域外へのデータ移転に関する要件が **あります** 。第三国への個人データの移転は、GDPRの文脈では常に重大な懸念事項であり、解決策を考案することは可能ですが、これは現在進行中の規制の分野です。個人情報保護アドバイザーと慎重に話し合い、正しく処理されるようにする必要があります。

@row
#### Step 2 – Read

Any and all _access to the personal data you hold must be kept secure_ . At the most basic level, this means ensuring that you minimise any such access. If you are not already doing so, _consider deploying a Privileged Access/User Management solution_ where applicable. You should also _ensure that even those authorised privileged users, including database and systems administrators, cannot get access to personal data in clear form_ \- even accidentally. Remember that **any** unauthorised access to personal data constitutes a potential data breach. Such a breach may be more or less severe and have greater or lesser consequences… but it is still a breach.

In order to provide useful functionality, whilst avoiding a potential data breach, be sure to use secure modern methods to authenticate and authorise your users, both internal and external. Use _multiple factors of authentication_ ; consider _FIDO authenticators_ ; _avoid SMS_ as a factor; consider modern authorisation standards (and products which support them), including established protocols like _XACML_ , newer standards like User-Managed Access (“ _UMA”)_ and emergent approaches such as _Transactional Authorization_ .

Note that ‘authentication’ is not necessarily the same as ‘verification’. You may not need to establish the user’s actual physical identity to any level of assurance in order to safely satisfy their request. However, where some level of assurance to a real-world identity is required, remember to treat any data used to verify the identity of the user with an appropriate level of security.

If you are pre-populating client-visible forms, be especially careful that such data is _only displayed to the correctly authorised user_ , and that it cannot be cached across the visits of different users.

Modern application design patterns will likely mean that you have an API for ‘read’ operations. As noted earlier, _any such API must be properly protected_ . Consider also adding additional program- or system-level protections: for example, _protecting against multiple sequential reads_ by requiring additional authorisation or by imposing a total read limit or a repeat-time restriction.

Be conscious of other systems which may have access to personal data - security applications (especially ML or AI-driven solutions) and data mining tools, for example. Make sure such systems don’t have unauthorised or unnecessary access to personal data in the clear, and be aware that in some cases, such access might constitute automated decision making or profiling (as referenced earlier).

Consider also unintended consequences. If you have a reporting tool which (for example) generates an Excel spreadsheet of data which can then be emailed, consider (a) whether all the PII needs to be in there; and (b) whether you can provide protection in some automated way upfront (for instance - by _automatically creating an encrypted sheet_ , rather than relying on the user to have it do that for themselves), to help reduce the risk of an accidental breach further down the line.

@column
#### ステップ2 - 読み取り

__保有する個人データへのすべてのアクセス権はセキュアにしておかなければなりません__ 。ほとんどの基本的なレベルでは、これはそのようなアクセス権を最小にすることを意味します。まだおこなっていない場合、必要に応じて __特権アクセス権/ユーザ管理ソリューションの導入を検討してください__ 。 __認証された特権ユーザ、データベース管理者やシステム管理者でさえ、偶然であってもクリアな形式で個人データにアクセスできないようにする__ べきです。個人データへの認可されていないアクセス権は **何であれ** 潜在的なデータ侵害の可能性があることを覚えておいてください。このような侵害は多かれ少なかれ深刻であり、多かれ少なかれ結果をもらしますが、侵害であることには割りません。

潜在的なデータ侵害を回避しながら有用な機能を提供するために、安全な最新の方法を使用して、内部と外部の両方でユーザを認証および認可してください。 __複数の認証要素を使用する__、 __FIDO認証器__ を検討する、要素として __SMSを避ける__ 、__XACML__ などの確立されたプロトコル、ユーザ管理アクセス（「 __UMA__ 」）などの新しい標準仕様、 __トランザクション認可__ のような新しいアプローチなど、最新の認可標準仕様（およびそれらをサポートしている製品）を検討しましょう。

「認証」は必ずしも「検証」と同じではないことに注意してください。ユーザの要求を安全に満たすために、ユーザの実際の物理的なアイデンティティを保証するレベルで確立する必要がない場合があります。ただし、現実世界のアイデンティティに対して保証が必要な場合は、ユーザのアイデンティティを検証するために使用されるデータを適切なレベルのセキュリティで扱うことを忘れないでください。

事前に入力されたクライアントに表示されるフォームを利用する場合、そのようなデータが __正しく認証されたユーザにだけ表示__ され、異なるユーザが訪れたときにキャッシュされないことに特に注意してください。

モダンアプリケーション設計パターンは、「読み取り」APIがあることを意味する可能性があります。前述のとおり、 __そのようなAPIは適切に保護しなければなりません__ 。また、追加のプログラムまたはシステムのレベルでの保護を追加することも検討してください。たとえば、追加の認可を要求したり、読み取り回数制限や繰り返し時間の制限を課したりして、 __複数の連続読み取りから保護します__ 。

セキュリティアプリケーション’特にMLやAI主導のソリューション）やデータマイニングツールなど、個人データにアクセスできる可能性のある他のシステムに注意してください。そのようなシステムが個人データへの認可なしまたは不必要なアクセスをしていないことを明らかにし、場合によっては、そのようなアクセスが自動化された意思決定またはプロファイリングを構成する可能性があることに注意してください（前述のとおり）。

意図しない結果も考慮してください。たとえば、電子メールで送信できるデータのExcelスプレッドシートを生成するレポートツールがある場合、将来的な偶発的な侵害のリスクを減らすために、(a)すべてのPIIをそこに含める必要があるかどうか、(b)事前に何らかの自動化された方法で保護を提供できるかどうか （たとえば、暗号化されたシートをユーザ自身で作成するように頼るのではなく、 __自動作成された暗号化されたシートを利用する__ ）、を検討してください。

@row
###### Data Subject Access Request and Data Portability

The subject of the personal data has the right, under GDPR, to access the personal data you hold about them. [^24] This presents an obvious breach risk. If you are handling a response to a data subject access request, or if you are designing a system to be used for such a case, then you must be _particularly careful to ensure that you correctly authenticate and/or verify the user; that they are properly authorized_ ; and that the data you are sharing does not itself contain the personal data of other data subjects.

You are also required under GDPR to provide all the subject’s personal data in a machine-readable format for data portability. The same security considerations apply in this case.

Somewhat perversely, in order to help satisfy some of these requirements, you may need to collect (or infer) more personal data than you might prefer, although you should always be careful not to collect more data that you absolutely need. For example: you may need to establish what country a given user lives in, is in, or is a citizen of, in order to establish what legislation applies! Depending on your system design, you can perhaps _avoid storing this information_ and instead _request it in real-time_ when the decision needs to be made (and verify it as needed).

@column
###### データ主体のアクセス要求とデータポータビリティ

個人データの主体は、GDPRに基づき、あなたが保持している個人データにアクセスする権利を有します。 [^24] ここには明らかな侵害のリスクがあります。データ主体のアクセス要求への応答を処理している場合、または、そのような場合に使用するシステムを設計している場合は、 __ユーザーを正しく認証および/または検証するように特に注意する必要があります；ユーザーがを適切に認可する必要があります__ ；共有しているデータ自体には、他のデータ主体の個人データが含まれていないことに注意する必要があります。

また、GDPRの下では、データのポータビリティのために、主体のすべての個人データを機械可読形式で提供する必要があります。この場合、同じセキュリティの考慮事項が適用されます。

やや皮肉なことに、これらの要件の一部を満たすために、必要以上の個人データを収集 (または推測) する必要がある場合がありますが、絶対に必要なデータ以外を収集しないように常に注意する必要があります。たとえば、適用される法律を確立するために、特定のユーザーが住んでいる国、居住している国、または市民である国の確認が必要な場合があります。システムの設計によっては、 __この情報を保存するのを避けて__ 、代わりに決定を下す必要があるときに  __リアルタイムでリクエストする__ ことができます（必要に応じて検証することができます）。

@row
###### Data Breach Reporting

Breach reporting is a special case in the context of ‘read’: if you are required to report a breach or a potential breach, you must ensure that you _do not send personal data_ as part of your breach report. If you have automated breach or security reporting tools, make sure these tools don’t accidentally create or worsen a breach by including personal data in their reporting. Consider also the use of privacy software solutions that can help search across data sets securely.

@column
###### データ侵害の報告

データ侵害報告は、「読み取り」のコンテキストにおける特別なケースです：侵害または侵害の可能性を報告する必要がある場合は、侵害報告の一部として __個人データを送信しない__ ようにする必要があります。自動化された侵害またはセキュリティ報告ツールを利用している場合は、これらのツールが報告に個人データを含めてしまうことで、誤って侵害をしたり、侵害の状況を悪化させたりしないようにしてください。データセット全体を安全に検索できるプライバシーソフトウェアソリューションの利用も検討してください。

@row
#### Step 3 - Update

GDPR mandates that data subject should be easily able to correct any personal data you hold about them. _Make sure your system has such a mechanism._ _User self-service solutions_ can be particularly helpful in this regard, as long as they are appropriately easy to find and to use. Again, proper authentication and - in some cases - verification is crucial to mitigate against a potential accidental breach.

It is worth noting that this ‘update’ requirement of the Regulation may have implications for distributed ledger-based solutions. In particular, you should establish whether such a solution will allow for the rectification of a historical record in the ledger (or on the chain). Simply marking the historical record as ‘no longer active’ is unlikely to be sufficient.

@column
#### ステップ3 - 更新

GDPRでは、データ主体が保持している個人データを簡単に修正できるようにする必要があります。 __システムにそのようなメカニズムがあることを確認してください。__ __ユーザーセルフサービスソリューション__ は、見つけやすく使いやすいものであるならば、この点で特に役立ちます。繰り返しになりますが、偶発的な侵害の可能性を軽減するには、適切な認証と、場合によっては検証が不可欠です。

GDPRのこの「更新」要件は、分散型台帳ベースのソリューションに影響を与える可能性があることに注意してください。特に、そのようなソリューションが大腸’またはチェーン）の履歴記録の修正を可能にするかどうかを検討する必要があります。過去の記録を単に「アクティブではない」とマークするだけでは不十分です。

@row
#### Step 4 - Delete

In some instances, the GDPR provides the data subject with a right to request that the data you hold about them be deleted. You will need to make sure you have a straightforward way to do this - and that this mechanism is _secured against accidental or deliberate misuse_ with appropriate safeguards including necessary levels and methods of authentication and authorisation. _Consider maintaining audit logs for such transactions (bearing in mind that you will want to keep the actual personal data out of the log record), and potentially having a time-limited ‘roll-back’ mechanism in the event of an error._

The Regulation also requires that data be stored only for the period it is actually needed. Business requirements, informed by privacy needs, will dictate the length of the retention period; but you will need to design your system such that data can be easily expunged at the end of this period. Consider _maintaining a separate record indicating when the data in question was originally created_ and running an automated task either to report on the data which has reached its retention date (hence flagging it for manual deletion) or to remove it directly.

For large and/or brownfield deployments, you may need to run a discovery process in order to establish what data you actually hold about a given data subject. There exists a variety of software solutions that can facilitate this.

As with ‘Update’, If you have an API (or other facility) which can perform data deletion - and especially if you allow for bulk delete - make sure you _protect against misuse_ . For instance: add an additional (even a manual) _check before a bulk delete_ or require _additional authorisation_ for requests exceeding a certain number of records. You should also ensure you have a way to _routinely back-up data_ and to _restore in the event of a mistake_ (or a deliberate attempt to corrupt data), and consider _forcing a backup_ via your API code before the delete process runs. Recall that retention of any such backup copies must be limited.

@column
#### ステップ4 - 削除

場合によっては、GDPRは、データ対象者が自分について保持しているデータの削除を要求する権利を提供します。これを簡単に実行できる方法があること、また、このメカニズムが必要なレベルの認証および認可方法を含む適切な保護措置により、 __偶発的または意図的な誤用に対して保護されている__ ことを確認する必要があります。 __このようなトランザクションの監査ログを維持し（実際の個人データをログ記録から除外することを念頭に置く）、エラーが発生した場合に時間制限付きの「ロールバック」メカニズムを持つ可能性を検討します。__

また、GDPRでは、データは実際に必要とされる期間のみ保存されることが要求されています。保存期間の長さは、プライバシーのニーズを考慮したビジネス要件によって決定されます；しかし、保存期間が終了した時点でデータを簡単に消去できるようなシステムを設計する必要があります。 __問題のデータがいつ作成されたかを示す別の記録を保持__ し、保持期限に達したデータについて報告する（したがって手動削除のフラグを立てる）か、直接削除する自動タスクを実行することを検討してください。

大規模および/またはブラウンフィールドのデプロイでは、特定のデータ対象者について実際にどのようなデータを保有しているかを確認するために、ディスカバリープロセスを実行する必要がある場合があります。これを容易にする様々なソフトウェアソリューションが存在します。

「更新」と同様に、データの削除をおこなうAPI（またはその他の機能）を持っている場合、特に一括削除を許可している場合は、 __悪用されないように保護する__ 必要があります。例えば、 __一括削除の前にチェック__ を追加で（手動でも）実施したり、一定のレコード数を超えるリクエストには __追加の認可__ を要求したりします。また、 __日常的にデータをバックアップ__ し、__ミス（または意図的にデータを破損させようとする行為）があった場合に復元する__ 方法を確保し、削除処理の実行前にAPIの実装で __強制的にバックアップ__ することを検討する必要があります。このようなバックアップコピーの保持は制限されなければならないことを思い出してください。

@row
## Conclusion

GDPR - and other modern data protection and privacy legislation and regulation - means we have to take extra care in designing, developing, and maintaining our IAM solutions. In particular:

*   Collect only the data we need
    
*   Only keep it for as long as it is needed
    
*   Look after it when it is in our care
    
*   Make sure it can only be accessed by those who should have access
    
*   Make sure it can be appropriately updated
    
*   Dispose of it safely when it is time to do so
    

We already have the tools we need to do this, but we need to be careful to apply those tools in the right way and to ensure that business owners aren’t asking us to do things we shouldn’t be doing:

*   Only create accounts if absolutely necessary; use federation (SAML; OpenID Connect) or other transient or non-identifying information where we can (User Info; Zero-Knowledge Proofs)
    
*   Authenticate users, preferably with strong and multiple factors of authentication (FIDO)
    
*   Authorise users, preferably with modern protocols (XACML and UMA)
    
*   Protect APIs (OAuth)
    

Much of what we need to do isn’t new, and much of it has always been good practice. It’s just not necessarily been standard practice or even top of the list for projects. New privacy regulations give us the opportunity to do things the right way.

@column
## 結論

GDPR、およびその他の最新のデータ保護とプライバシーの法律や規制は、IAMソリューションの設計、開発、および保守に細心の注意を払わなければならないことを意味します。特に以下の点に注意する必要があります：

*   必要なデータのみを収集する
    
*   必要な期間だけ保管する
    
*   保管中は適切に管理するLook after it when it is in our care
    
*   アクセス権を有する者のみがアクセスできるようにする
    
*   適切に更新できるようにする
    
*   廃棄するときは、安全に廃棄する
    

これを実施するのに必要なツールを有しているが、正しい方法でツールを適用し、経営者が私たちにやるべきでないことを求めないように注意する必要があります：

*   絶対に必要不可欠なアカウントだけを作成する；フェデレーション（SAMLやOpenID Connect）や、できるかぎり一時的もしくは非特定情報を用いる（ユーザー情報；ゼロ知識証明）
    
*   できれば、強力で多要素の認証（FIDO）でユーザを認証する
    
*   できれば最新のプロトコル（XACMLやUMA）を用いて、ユーザを認可する
    
*   APIを保護する（OAuth）
    

私たちがしなければならないことの多くは新しいことではなく、その多くは常に良い習慣でした。ただ、これまで必ずしも標準的なやり方ではなく、プロジェクトの最優先事項でもありませんでした。新しい個人情報保護規制は、私たちに正しい方法で物事をおこなう機会を与えてくれます。

@row
## Your IAM Project Checklist

*   Ensure that privacy requirements are considered from the very start of a project, and routinely re-evaluated through the lifetime of the application
    
*   Involve the relevant people (people who represent organizations consuming the IAM data as well as those serving as sources of truth for your IAM data, together with your privacy peers) in your project at the very earliest stage.
    
*   Do keep good records of any conversations around potential data breaches but do not include specific examples of Personal Data when reporting issues.
    
*   Map what, where, and how personal data might be used; this will be valuable input to a more complete Data Protection Impact Assessment (DPIA)
    
*   If you are handling special category data as defined by GDPR and/or your local or sectoral privacy regulations, you will need additional safeguards.
    
*   If your project involves data about Children, you will also need to take special care.
    
*   Ensure that your organization’s or service’s privacy notice accurately reflects the way the system actually works!
    
*   Collect the consent of the data subject for you to collect and process their information.
    
*   Keep a record of that consent and/or providing your data subject with a record for themselves.
    
*   Explore the Consent Receipt specification and emerging implementations.
    
*   Collect as little data as you possibly can (data minimization).
    
*   Avoid repeat collection of data.
    
*   Consider using data discovery or meta-directory tools to help with visibility and consolidation.
    
*   Explore zero-knowledge proof technologies and implementations and investigate whether such solutions should form a part of your deployment
    
*   Instead of creating an account, consider instead using transient identity federation and/or single sign-on. If account creation cannot be avoided, consider using pseudonymous federation and/or single sign-on to reduce the amount of identifiable personal data you hold.
    
*   Use the most current version of TLS plus additional specific data encryption as necessary.
    
*   Use appropriate encryption techniques and keep these under routine review.
    
*   Keep supporting systems, applications, and libraries up to date and patched.
    
*   Protect access to APIs that handle personal data, ideally using a protocol such as OAuth.
    
*   Storing personal data directly in a distributed ledger is not good practice.
    
*   Develop a flexible architecture that will allow you to segregate data on a regional basis.
    
*   The transfer of personal data to any Third Country (as defined in the Regulation) must always be a significant concern.
    
*   Access (physical and digital) to the personal data you hold must be kept secure.
    
*   Consider deploying a Privileged Access/User Management solution.
    
*   Ensure that even those authorised privileged users, including database and systems administrators, cannot get access to personal data in clear form.
    
*   Use multiple factors of authentication; consider FIDO authenticators; avoid SMS as a factor; consider modern authorisation standards (and products which support them), including established protocols like XACML, newer standards like UMA and emergent approaches such as Transactional Authorization.
    
*   Be careful that Personal Data is only displayed to the correctly authorised user, and that it cannot be cached across the visits of different users.
    
*   Be particularly careful to ensure that you correctly authenticate the user and that they are properly authorized.
    
*   Avoid storing personally identifiable information, and instead request it in real-time when the decision needs to be made (and verify it as needed).
    
*   If you discover a breach in your system, do not send personal data as part of your breach report.
    
*   Make sure your system has a self-service mechanism to support the correction and/or deletion of a user’s personal data.
    
*   Consider maintaining audit logs for such transactions (bearing in mind that you will want to keep the actual personal data out of the log record).
    
*   Consider maintaining a separate record indicating when the data in question was originally created and running an automated task either to report on data which has reached its retention date (hence flagging it for manual deletion) or to remove it directly, in line with your privacy policy and notice
    
*   Check before a bulk delete and require additional authorisation for requests exceeding a certain number of records.
    
*   Ensure you have a way to routinely back-up data and to restore in the event of a mistake (or a deliberate attempt to corrupt data), and consider forcing a backup via your API code before the delete process runs.
    

@column
## IAMプロジェクトチェックリスト

*   プロジェクトの初期段階からプライバシー要件が考慮され、アプリケーションのライフタイムを通じて定期的に再評価されるようにする。
    
*   関係者（IAMデータを消費する組織の代表者、IAMデータの信頼できる情報源となる人々、およびプライバシー関係者）を、非常に早い段階からプロジェクトに参加させる。
    
*   データ侵害の可能性に関する会話は適切に記録しておくが、問題を報告する際に個人データの具体例を含めないこと。
    
*   個人情報が、どこで、どのように利用されるかをマップ化し、より完全なデータ保護インパクトアセスメント（DPIA）の貴重なインプットとする。
    
*   GDPRや地域・部門別の個人情報保護規則で定義された特殊カテゴリーデータを扱う場合、追加の保護措置が必要になる。
    
*   子どもに関するデータを扱うプロジェクトでは、特に注意が必要である。
    
*   組織やサービスのプライバシー通知が、実際のシステムの仕組みを正確に反映していることを確認する！
    
*   データ対象者の情報を収集し処理することについて、データ対象者の同意を得る。
    
*   同意の記録を保持すること、および/または、データ対象者自身に記録を提供する。
    
*   同意の受領書の標準仕様と新しい実装を検討する。
    
*   できるだけ少ないデータを収集する（データの最小化）。
    
*   既に持っている個人データを繰り返し収集することを避ける。
    
*   データディスカバリーツールやメタディレクトリツールを使用することを検討し、データの可視化と統合をおこなう。
    
*   ゼロ知識証明技術と実装を調査し、そのようなソリューションがお客様の展開の一部を構成すべきかどうかを調査する。
    
*   アカウントを作成する代わりに、一時的なIDフェデレーションやシングルサインオンを使用することを検討する。アカウント作成が避けられない場合は、仮名認証やシングルサインオンの利用を検討し、保有する個人情報の量を削減する。
    
*   最新バージョンのTLSに加え、必要に応じて特定データの暗号化をおこなう。
    
*   適切な暗号化技術を使用し、定期的に見直す。
    
*   サポートするシステム、アプリケーション、ライブラリを常に最新に維持する。
    
*   個人情報を扱うAPIへのアクセスは、OAuthなどのプロトコルを用いて保護することが理想的である。
    
*   分散型台帳をストレージとして個人データを保存するのは良い事例ではない。
    
*   地域ごとにデータを分離できるような柔軟なアーキテクチャを構築する。
    
*   個人データの第三国（GDPRで定義されている）への移転は、常に重大な懸念事項でなければならない。
    
*   個人情報へのアクセス（物理的、デジタル的）はセキュアでなければならない。
    
*   特権アクセス/ユーザ管理ソリューションの導入を検討する。
    
*   データベースやシステムの管理者を福得て認証された特権ユーザでさえクリアフォームで個人情報にアクセスできないことを保証する。
    
*   多要素の認証を利用する；FIDO認証器を検討する；要素としてSMSは避ける；XACMLのような確立されたプロトコルを含むモダンな認可標準仕様（およびそれらをサポートする製品）、UMAのようなさらに新しい標準仕様およびトランザクショナル認可のような新規の手法を検討する。
    
*   個人情報は正しく認可されたユーザだけに表示され、異なるユーザの訪問時にキャッシュされないことを注意する。
    
*   正しくユーザを認証していることとユーザが正しく認可されていることを保証することに特に注意する。
    
*   個人を特定できる情報の保存を避け、代わりに決定を下す必要があるときにリアルタイムにリクエストする（そして必要であればそれを検証する）。
    
*   システムに違反を見つけた場合、違反報告の一部として個人情報を送らないようにする。
    
*   システムに、ユーザの個人情報の修正および/または削除をおこなうことができるセルフサービス機能があることを確認する。
    
*   そのようなトランザクションの監査ログを保持することを検討する（実際の個人情報をログ記録から除外することを肝に銘じる）。
    
*   プライバシーポリシーと通知にしたがって、目的のデータがいつ最初に作成されたを示す別のレコードを管理し、保持期限に達したデータを報告する（つまり、手動での削除のためにフラグを立てる）ために、または直接それを削除するために自動化されたタスクを実行する。
    
*   一括削除の前に確認し、一定のレコード数を超えるリクエストには追加の認可を要求する。
    
*   定期的にデータをバックアップし、ミスによるイベント（または意図的なデータ破損）における復元する方法があることを確認し、 削除プロセスの実行前にAPI実装を介して強制的にバックアップすることを検討する。
    

@row
- - -

[^1]:  For an overview, read the IDPro Body of Knowledge GDPR article. The full text of the regulation can be found at [_https://eur-lex.europa.eu/eli/reg/2016/679/oj_](https://eur-lex.europa.eu/eli/reg/2016/679/oj) 
    
[^2]:  Organisation for Economic Co-operation and Development, “The OECD Privacy Framework,” 2013, [_https://www.oecd.org/sti/ieconomy/oecd\_privacy\_framework.pdf_](https://www.oecd.org/sti/ieconomy/oecd_privacy_framework.pdf) 
    
[^3]:  An overview of the history of the GDPR can be found at [_https://cloudprivacycheck.eu/latest-news/article/a-brief-history-of-data-protection-how-did-it-all-start/_](https://cloudprivacycheck.eu/latest-news/article/a-brief-history-of-data-protection-how-did-it-all-start/) 
    
[^4]:  United Nations, “The Universal Declaration of Human Rights,” 1948, [_https://www.un.org/en/universal-declaration-human-rights/_](https://www.un.org/en/universal-declaration-human-rights/) 
    
[^5]:  Organisation for Economic Co-operation and Development, “OECD Guidelines on the Protection of Privacy and Transborder Flows of Personal Data,” 2013,
    
    [_http://www.oecd.org/sti/ieconomy/oecdguidelinesontheprotectionofprivacyandtransborderflowsofpersonaldata.htm_](http://www.oecd.org/sti/ieconomy/oecdguidelinesontheprotectionofprivacyandtransborderflowsofpersonaldata.htm) 
    
[^6]:  See Article 25 of the Regulation 
    
[^7]:  KJ Dearie, “What is Data Mapping? The Importance of Data Mapping for GDPR Compliance,” Termly, 30 October 2018, [_https://termly.io/resources/articles/gdpr-data-mapping/_](https://termly.io/resources/articles/gdpr-data-mapping/) 
    
[^8]:  “GDPR: Data Protection Officer,” Intersoft Consulting, [_https://gdpr-info.eu/issues/data-protection-officer/_](https://gdpr-info.eu/issues/data-protection-officer/) 
    
[^9]:  “GDPR: Personal Data,” Intersoft Consulting, [_https://gdpr-info.eu/issues/personal-data/_](https://gdpr-info.eu/issues/personal-data/) 
    
[^10]:  “GDPR: Privacy by Design,” Intersoft Consulting, [_https://gdpr-info.eu/art-25-gdpr/_](https://gdpr-info.eu/art-25-gdpr/) 
    
[^11]:  See in particular Article 38 of the Regulation. 
    
[^12]:  Article 4 of the Regulation 
    
[^13]:  Dearly, “What is Data Mapping? The Importance of Data Mapping for GDPR Compliance,” [_https://termly.io/resources/articles/gdpr-data-mapping/_](https://termly.io/resources/articles/gdpr-data-mapping/) 
    
[^14]:  European Parliament, Council of the European Union,
    
    “Directive 2009/136/EC of the European Parliament and of the Council,” November 2009, [_http://data.europa.eu/eli/dir/2009/136/oj_](http://data.europa.eu/eli/dir/2009/136/oj) 
    
[^15]:  See Article 9 of the Regulation. 
    
[^16]:  See Article 8 of the Regulation. 
    
[^17]:  See Article 22 of the Regulation. 
    
[^18]:  Greenfield is a term used to describe a project with no prior work to constrain its development. Brownfield, in contrast, refers to projects with predetermined limitations based on having to work in an existing platform or under pre-existing constraints. 
    
[^19]:  Specifications and Auxiliary Documents, User Managed Access Working Group, Kantara Initiative, [_https://kantarainitiative.org/confluence/display/uma/Specifications+and+Auxiliary+Documents_](https://kantarainitiative.org/confluence/display/uma/Specifications+and+Auxiliary+Documents) 
    
[^20]:  Lizar, Mark and David Turner, eds. “Consent Receipt Specification,” Consent & Information Sharing Working Group, Kantara Initiative [_https://kantarainitiative.org/file-downloads/consent-receipt-specification-v1-1-0/_](https://kantarainitiative.org/file-downloads/consent-receipt-specification-v1-1-0/) 
    
[^21]:  “The Principles,” Information Commissioner’s Office Guide to the General Data Protection Regulation (GDPR), https://ico.org.uk/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/principles/. 
    
[^22]:  Katarzyna Szymielewicz, Bill Budington, “The GDPR and Browser Fingerprinting: How it Changes the Game for the Sneakiest Web Trackers,” Electronic Frontier Foundation, 19 June 2018, [_https://www.eff.org/deeplinks/2018/06/gdpr-and-browser-fingerprinting-how-it-changes-game-sneakiest-web-trackers_](https://www.eff.org/deeplinks/2018/06/gdpr-and-browser-fingerprinting-how-it-changes-game-sneakiest-web-trackers) 
    
[^23]:  “Zero-knowledge proof,” Wikipedia, last updated 24 January 2020, [_https://en.wikipedia.org/wiki/Zero-knowledge\_proof_](https://en.wikipedia.org/wiki/Zero-knowledge_proof) . 
    
[^24]:  “Art. 15 GDPR Right of access by the data subject,” Intersoft Consulting, [_https://gdpr-info.eu/art-15-gdpr/_](https://gdpr-info.eu/art-15-gdpr/) 
