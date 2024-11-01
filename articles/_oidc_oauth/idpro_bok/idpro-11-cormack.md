---
layout: columns
title: An Introduction to the GDPR (v3)
permalink: /docs/oidc_oauth/idpro_bok/11
date: 2024-09-09
modify_date: 2024-11-01
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "法律", "GDPR"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/11/](https://bok.idpro.org/article/id/11/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

The General Data Protection Regulation (GDPR) applies to any processing (including collection, storage, or sharing) of data relating to identifiable (including by serial numbers, IP addresses, etc.) individuals who are physically in Europe. This scope may well cover international or online Identity and Access Management (IAM) activities, as well as all IAM activities actually conducted in Europe. All such processing must conform to seven principles: lawfulness, fairness & transparency; purpose limitation; data minimisation; accuracy; storage limitation; integrity & confidentiality; accountability. Individuals have rights of information; subject access; rectification, erasure & restriction. Processing must be for one of six legal bases: contract, legal obligation, vital interests, public interests, legitimate interests, or consent. Each basis has its own requirements; some confer additional rights on individuals.

Keywords: Law, GDPR, Europe


@column
## Abstract

一般データ保護規則（GDPR）はヨーロッパに物理的に存在する個人の特定に関するデータ（シリアル番号、IPアドレスなどを含む）の全ての処理（収集、保管や共有を含む）に適用されます。この範囲は、ヨーロッパで実際におこなわれるアイデンティティとアクセス管理（IAM）の活動と同様に、国際的もしくはオンラインのIAM活動も含んでいる可能性があります。このような処理は全て7つの原則を準処しなければなりません：合法性、公正性および透明性；目的の制限；データの最小化；正確性；保管制限；完全性および機密性；説明責任。個人は以下のものを有しています。情報の権利；対象へのアクセス；修正、消去および制限。処理は以下の6つの法的根拠の1つでなければなりません：契約、法的義務、重要な利益、公共の利益、正当な利益、同意。それぞれの法的根拠は独自の要件があります；個人に関する追加の権利を与えるものです。

Keywords: 法律, GDPR, ヨーロッパ


@row
By Andrew Cormack, Chief Regulatory Adviser at Jisc

© 2022 Andrew Cormack, IDPro

@row
## Introduction

The _General Data Protection Regulation (GDPR)_ , [^1] which came into force in all EU member states on May 25, 2018, applies when processing ‘any information relating to an identified or identifiable natural person’. [^2] The inclusion of ‘identifiable’ makes it much broader than most privacy laws: IP addresses, MAC addresses of personal devices, account numbers, and even unique patterns or combinations of attributes may be sufficient to bring an activity within its scope. ‘Processing’ is not limited to digital formats: personal information prepared for, or derived from, digital processing is covered, as well as the content of any structured filing system. The range of activities covered is similarly wide: including ‘collection, recording, organisation, structuring, storage, adaptation or alteration, retrieval, consultation, use, disclosure by transmission, dissemination or otherwise making available, alignment or combination, restriction, erasure or deletion’. [^3] Since the GDPR covers all individuals physically in Europe – there is no citizenship or similar requirement – it is very likely to apply to the international or online activities of organisations elsewhere in the world, as well as to all organisations in Europe.

IAM activities are likely to be regulated by the GDPR; however, effective IAM may make it easier for organisations to comply with the law’s requirements. The behaviour it prescribes is increasingly expected, not only in Europe, but in the increasing number of countries subscribing to the Council of Europe’s Convention 108. [^4] Within Europe there are significant fines for contravention of the GDPR, but following its principles should have benefits for the reputation and efficient operation of organisations anywhere in the world.

This article is not a complete guide to the GDPR but covers those aspects most relevant to IAM. It first describes the general principles and obligations that apply to all personal data processing; then examines the permitted legal bases for processing and the specific obligations and rights associated with them. Finally, examples show how IAM activities can help organisations conform to the GDPR’s requirements.

@column
## 導入

2018年5月25日にすべてのEU加盟国で施行された一般データ保護規則（ __GDPR__ ） [^1] は、「特定された、または特定可能な自然人に関するあらゆる情報」 を処理する場合に適用されます。 [^2] 「識別可能なもの」を含めることで、ほとんどのプライバシー法よりもはるかに広くなっています：IPアドレス、個人用デバイスのMACアドレス、アカウント番号、さらには属性の固有のパターンや組み合わせでさえ、活動をその範囲内に収めるのに充分な場合があります。「処理」はデジタル形式に限定されません：デジタル処理のために準備された、またはデジタル処理から派生した個人情報、および構造化されたファイルシステムの内容が対象となります。対象となる活動の範囲も同様に広いです：「収集、記録、組織化、構造化、保管、適応または変更、検索、協議、使用、伝送による開示、普及またはその他の方法で利用可能にすること、アライメントまたは組み合わせ、制限、消去または削除」を含みます。 [^3] GDPRは、ヨーロッパ内の物理的にすべての個人を対象としているため（市民権や同様の要件はありません）、ヨーロッパ内のすべての組織だけでなく、世界の他の場所にある組織の国際活動やオンライン活動にも適用される可能性が非常に高いです。

IAMアクティビティはGDPRによって規制される可能性が高いです；しかし、有効なIAMによって、組織が法律の要件に準拠しやすくなる場合があります。同規則が規定する振る舞いは、欧州だけでなく、欧州評議会の条約108 [^4] に加入する国の増加によってますます期待されています。欧州内では、GDPRに違反した場合に多額の罰金が科されますが、その原則に従うことは、世界のどこにいても、組織の評判と効率的な運営に利益をもたらすはずです。

この記事はGDPRの完全なガイドではありませんが、IAMに最も関連する側面をカバーしています。最初に、すべての個人データ処理に適用される一般的な原則と義務について説明します；次に、処理のために許可された法的根拠と、それに関連する具体的な義務と権利を調査します。最後に、組織がGDPRの要件に適合するために、IAMアクティビティがどのように役立つかを例で示します。

@row
## Terminology

*   **General Data Protection Act (GDPR).** Formally, Regulation 2016/679 of the European Union, in force May 25, 2018. Available at [https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679)
    
*   **Personal Data.** Defined in Article 4(1) of the GDPR: “‘personal data’ means any information relating to an identified or identifiable natural person (‘data subject’); an identifiable natural person is one who can be identified, directly or indirectly, in particular by reference to an identifier such as a name, an identification number, location data, an online identifier or to one or more factors specific to the physical, physiological, genetic, mental, economic, cultural or social identity of that natural person;”. Note: “natural person” (human) is used to distinguish from companies and other corporate entities that are “legal persons”.
    
*   **Processing.** Defined in Article 4(2) of the GDPR: “‘processing’ means any operation or set of operations which is performed on personal data or on sets of personal data, whether or not by automated means, such as collection, recording, organisation, structuring, storage, adaptation or alteration, retrieval, consultation, use, disclosure by transmission, dissemination or otherwise making available, alignment or combination, restriction, erasure or destruction”. Note that even this long list of activities is not exhaustive: other activities may also fall within the definition of “processing”. Additional rules, in Article 22, apply to “automated individual decision-making, including profiling”. These generally have the effect of strengthening the rights of information and objection described later and may limit the use of automation for some high-impact decisions.
    
*   **Special Category Data (SCD).** Categories of data that are regarded as particularly sensitive, so subject to additional regulation. Defined in Article 9(1) of the GDPR as “personal data revealing racial or ethnic origin, political opinions, religious or philosophical beliefs, or trade union membership, and the processing of genetic data, biometric data for the purpose of uniquely identifying a natural person, data concerning health or data concerning a natural person’s sex life or sexual orientation”; Article 10’s “personal data relating to criminal convictions and offences” requires similar treatment, so is normally considered as another category of SCD.
    
*   **Data Controller.** Defined in Article 4(7) of the GDPR: “‘controller’ means the natural or legal person, public authority, agency or other body which, alone or jointly with others, determines the purposes and means of the processing of personal data;”. [^5] This article uses the term “organisation” as a synonym for “data controller”, since organisations involved in IAM will normally be data controllers.
    
*   **Data Processor.** Defined in Article 4(8) of the GDPR for situations where an organisation processes personal data solely on the instructions of others. A Data Processor must not determine the purposes of processing, for example by processing in its own interests, or, beyond limited technical choices, the means of doing so. Data Processors are regulated by Article 28: in particular they must have a contract with the Data Controller that covers all the subjects listed in Article 28(3). Data Processors are excluded from some, but not all, of the liabilities and duties of Data Controllers.
    
*   **Data Subject.** Defined in Article 4(1) of the GDPR (see “Personal Data” above) as the formal term for the human to whom personal data relates. This article uses the term “individual” as a synonym for “data subject”.
    

@column
## 用語解説

*   **一般データ保護法（GDPR）** 正式には、欧州連合規則2016/679、2018年5月25日発効。[https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679)より入手可能。
    
*   **個人データ** GDPR第4条1項に定義されています：「『個人データ』とは、識別された又は識別可能な自然人（『データ主体』）に関するあらゆる情報を意味し、識別可能な自然人とは、特に氏名、識別番号、位置情報、オンライン識別子等の識別子又は当該自然人の身体的、生理的、遺伝的、精神的、経済的、文化的若しくは社会的アイデンティティに固有の一つ以上の要素を参照して直接又は間接的に識別できる者のことをいう」（同）。
    
*   **加工**  GDPRの第4条2項に定義されています。「『加工』とは、収集、記録、整理、構造化、保管、適応または変更、検索、相談、使用、送信による開示、普及またはその他の方法による利用可能化、整合または結合、制限、消去または破壊など、自動化された手段であるかどうかにかかわらず個人データまたは個人データの集合に対して行われるあらゆる操作または一連の操作のことを意味する」。なお、この長いリストは完全なものではなく、他の活動も「加工」の定義に含まれる場合があります。第22条では、「プロファイリングを含む、自動化された個人の意思決定」についての追加規則が適用されます。これらの規定は、一般的に、後述する情報提供および異議申し立ての権利を強化するものであり、影響力の大きい意思決定については、自動化の使用を制限することができます。
    
*   **特別カテゴリーデータ（SCD）** 特に機密性が高いとされ、追加的な規制の対象となるデータのカテゴリー。 GDPR第9条1項において「人種または民族的出身、政治的意見、宗教的または哲学的信条、労働組合への加入を明らかにする個人データ、および遺伝データ、自然人を一意に識別するための生体データ、健康に関するデータ、自然人の性生活または性的指向に関するデータの処理」として定義されており、同第10条の「犯罪歴および犯罪に関する個人データ」も同様の扱いが求められるため、通常はSCDのひとつのカテゴリーとみなされます。
    
*   **データ管理者** GDPR第4条7項に定義されています：「『管理者』とは、個人データの処理の目的と手段を単独でまたは他の者と共同で決定する自然人または法人、 公的機関、機関、その他の機関を意味する。」 [^5] 本稿では、『組織』という用語を『データ管理者』と同義語として使用するが、これは、IAMに関与する組織が、通常データ管理者となるためです。
    
*   **データ処理者** GDPR第4条8項に定義されており、組織が他社の指示のみに基づいて個人データを処理する場合を指す。データ処理者は、自らの利益のために処理を行うなど、処理の目的を決定してはならず、また、限られた技術的選択の範囲を超えて、処理の手段を決定してはなりません。 データ処理者は、データ管理者との間で第28条3項に記載されたすべての対象者をカバーする契約を締結しなければなりません。データ処理者は、データ管理者の責任と義務の一部（すべてではないが）から除外されます。
    
*   **データ対象者** GDPR第4条1項（上記「個人データ」参照）において、個人データが関係する人間の正式な用語として定義されている。本稿では、「個人」という用語を「データ対象者」と同義語として使用します。
    

@row
## Rules for Personal Data

The GDPR places most of its obligations on organisations that “determine\[…\] the purposes and means of the processing of personal data” (Art 4(7)): these organisations are referred to as _Data Controllers_ . Some organisations may process data solely on behalf of others – not determining the purposes and means – these are known as _Data Processors_ and have fewer obligations. Since IAM systems are likely to act as data controllers, their main obligations are described here. The fundamental obligations on all data controllers are to act in accordance with seven principles, and to satisfy obligations to, and rights of, individuals (“ _data subjects_ ”) whose information they process.

@column
## 個人データに関する規則

GDPRは、その義務のほとんどを「個人データの処理の目的と手段を\[…\]決定する」組織に課しています（第4条7項）：これらの組織は __データ管理者__ と呼ばれます。一部の組織は、目的と手段を決定せずに、他の組織に代わってデータを処理する場合があります。これらはデータ処理者として知られており、義務はより少なくなります。IAMシステムはデータ管理者として機能する可能性が高いため、その主な義務をここで説明します。すべてのデータ管理者の基本的な義務は、7つの原則に従って行動し、情報を処理する個人（「 __データ主体__ 」）に対する義務と権利を満たすことです。

@row
### Principles (Art 5)

According to GDPR Article 5, the following principles apply to all processing of personal data:

*   **Lawfulness, Fairness, Transparency** : all processing must be covered by one of the six legal bases set out in the GDPR (see below) and must not breach other laws; it should not be deceptive, any activities that individuals might be surprised by should be explained and justified as must any adverse effects on individuals; organisations should be open about their processing, in particular through the rights to information and subject access described below.
    
*   **Purpose Limitation** : the purposes for which information is processed must be clearly stated; existing information may only be used for new purposes if, either, the new purpose is compatible with the existing ones (roughly summarised as ‘not surprisingly different’), or it is required by law, or each individual has given consent to the new purpose. IAM systems should be designed to serve a single purpose and any proposals to re-use their data for other purposes should be reviewed for compatibility with that purpose and with the information provided to users.
    
*   **Data Minimisation** : the data and processing must be relevant to the purpose, sufficient to achieve it (“adequate”), but not excessive. Well-defined IAM systems should contribute to data minimisation: for example, federated systems can reduce disclosure by using opaque identifiers (“pseudonyms”) that allow an individual to be recognised when they return to a system, without identifying them. IAM systems should be designed to collect, use and disclose the minimum personal data required for each function. If a function can be delivered with anonymous or pseudonymous data, then it should be. This is the basis for Data Protection by Design, discussed in GDPR Article 25.
    
*   **Accuracy** : personal data must be accurate and up to date. Although individuals have the right to correct errors in their data (see “right of rectification” below) organisations should not rely on them doing so as the sole, or even principal, way to ensure accuracy. IAM systems that act as a single source of truth for their organisations should make accuracy significantly easier to achieve; those that do not should be accompanied by appropriate policies, processes and workflows to ensure that their information is, and remains, accurate.
    
*   **Storage \[time\] Limitation** : personal data must not be kept for longer than needed for the stated purpose(s). Before collecting personal data, organisations should know, and declare, how long they will keep it for, either in relation to a fixed time period (e.g., ‘six months’), or a known event (e.g., ‘until you leave’). Organisations should have processes to ensure their stated retention periods are implemented; at the end of them data should be deleted or anonymised. The purposes of archiving, research, and statistics may allow personal data to be kept for longer, but subject to specific conditions in both European and national laws.
    
*   **Integrity and Confidentiality** : organisations must use appropriate technical and organisational controls to protect the security of personal data. What is appropriate will depend on the sensitivity of the data and the purpose: it is likely to change both as new protective technologies and approaches become available and as new threats and risks become apparent. The GDPR imposes specific obligations if there is a breach of security, which are described below. IAM systems should help both by holding their own personal data securely, and as a component of the access control systems used to prevent unauthorised access to personal data elsewhere in the organisation.
    
*   **Accountability** : organisations must be able to demonstrate that they are complying with the principles and other requirements of the Regulation. This will normally require both documentation showing that these principles and requirements were considered in the design of the system, and audit logs (which themselves may contain personal data) confirming that normal operations and responses to events such as breaches and any exercise of individual rights were, in fact, conducted in accordance with them.
    

@column
### 原則（第5条）

GDPR第5条によると、次の原則が個人データのすべての処理に適用されます：

*   **合法性、公平性、透明性**：すべての処理は、GDPRに定められた6つの法的根拠（下記参照）のいずれかによってカバーされなければならず、他の法律に違反してはなりません；それは欺くものであってはならず、個人が驚くかもしれない活動は、個人への悪影響と同様に説明され、正当化されるべきです。組織は、特に以下に説明する情報と被験者へのアクセスの権利を通じて、その処理についてオープンにする必要があります。
    
*   **目的の制限**：情報を処理する目的を明確に示す必要があります。既存の情報は、新しい目的が既存の目的と互換性がある（「驚くほど変わらない」と大まかに要約されている）場合、または法律で義務付けられている場合、または各個人が新しい目的に同意した場合にのみ、新しい目的に使用することができます。IAMシステムは、単一の目的を果たすように設計する必要があり、そのデータを他の目的に再利用する提案は、その目的とユーザーに提供される情報との互換性について検討する必要があります。
    
*   **データの最小化**：データと処理は目的に関連し、目的を達成するのに充分（「適切」）である必要がありますが、過度ではありません。明確に定義された IAMシステムは、データの最小化に貢献する必要があります。たとえば、フェデレーションシステムは、不透明な識別子（「仮名」）を使用することで開示を減らすことができます。IAMシステムは、各機能に必要な最小限の個人データを収集、使用、および開示するように設計する必要があります。関数が匿名または仮名のデータで配信できる場合は、そうする必要があります。これは、GDPR第25条で説明されているデータ・プロテクション・バイ・デザインの基礎です。    
    
*   **正確性**：個人データは正確かつ最新のものでなければなりません。個人にはデータのエラーを修正する権利がありますが（以下の「修正の権利」を参照）、組織は、正確性を確保するための唯一の、または主要な方法として、個人による修正に頼るべきではありません。組織にとって信頼できる唯一の情報源として機能するIAMシステムは、精度の達成を大幅に容易にするはずです。そうでないものには、適切なポリシー、プロセス、およびワークフローを伴って、情報が正確であり、正確であることを保証する必要があります。
    
*   **保管 \[時間\] 制限**：個人データは、記載された目的のために必要以上に長く保管してはなりません。 組織は、個人データを収集する前に、一定の期間（例えば「6か月」）または既知のイベント（例えば「退職するまで」）に関連して、個人データを保持する期間を把握し、宣言する必要があります。組織は、定められた保持期間が確実に実施されるようにするためのプロセスを持つ必要があります。それらの最後に、データを削除するか匿名化する必要があります。アーカイブ、研究、および統計の目的により、個人データをより長期間保持できる場合がありますが、欧州法および国内法の両方の特定の条件に従う必要があります。
    
*   **完全性と機密性**：組織は、個人データのセキュリティを保護するために、適切な技術的および組織的管理を使用する必要があります。何が適切かは、データの機密性と目的によって異なります。新しい保護技術とアプローチが利用可能になるにつれて、また新しい脅威とリスクが明らかになるにつれて、変更される可能性があります。GDPRは、セキュリティ違反が発生した場合に特定の義務を課します。これについては以下で説明します。IAMシステムは、自身の個人データを安全に保持することと、組織内の他の場所での個人データへの不正アクセスを防止するために使用されるアクセス制御システムのコンポーネントの両方を支援する必要があります。
    
*   **説明責任**：組織は、規則の原則およびその他の要件を遵守していることを証明できなければなりません。通常、これらの原則と要件がシステムの設計で考慮されたことを示す文書と、通常の運用と、侵害や個人の権利の行使などのイベントへの対応がおこなわれたことを確認する監査ログ（それ自体に個人データが含まれる場合があります）の両方が必要になります。実際には、それらに従って実施されました。
    

@row
### Obligations and Rights

Three groups of “rights” apply to all processing of personal data except where limited exceptions, set out in the specific Articles, apply. The first group creates an obligation on organisations towards all those whose information they process; the second and third require organisations to have systems to handle requests from individuals who exercise their rights:

*   **Rights to Information** : to support the above Principles, organisations are required to provide at least a minimum set of information to all those whose personal data are processed: who the organisation is, what data are being processed, why, for how long, whether automated decisions are involved; any other organisations or further processing involved; how to exercise your rights. Article 13 applies when data are collected directly from the individual; Article 14 when an organisation obtains personal data from another source (including public sources).
    
*   **Subject Access Right** : individuals have a general right, under Article 15, to ask and be told whether their data are being processed, what data, why, for how long, whether automated decisions are involved; the source of the data and any recipients; how to exercise their rights. In addition, if this can be done without affecting the rights of others, the individual has a right to receive a copy of their own data. Determining what to release, and when, can be complex, especially when the requester’s identity may be uncertain. IAM systems built around guidance from regulators [^6] can reduce the risk of error or fraud.
    
*   **Rights of Rectification/Erasure/Restriction** : Article 16 (“rectification”) entitles individuals to correct inaccurate personal data, including to add additional information. Article 17 (“erasure”) entitles individuals to have their personal data deleted if there is no lawful basis for it to be kept. This might arise, for example, when excessive information is held, if it has been kept beyond its retention time, or, if it was being processed on the basis of consent (see below) when that consent has been withdrawn. Article 18 (“restriction”) entitles an individual to block further processing of their data (including deletion) while a rectification or objection right is being processed, or as an alternative to erasure if the individual needs the data for a legal claim. IAM systems that provide a single point of truth and control should make it easier to implement these rights.
    

@column
### 義務と権利

3つの「権利」グループは、特定の条項で規定された限定的な例外が適用される場合を除き、個人データのすべての処理に適用されます。最初のグループは、組織が情報を処理するすべての人々に対する義務を生じさせます。2番目と3番目のグループは、組織が、権利を行使する個人からの要求を処理するシステムを持つことを要求しています：

*   **情報を得る権利** : 上記の原則を支えるため、組織は、個人情報が処理されるすべての人に対し、少なくとも、組織が誰であるか、どのデータが処理されているか、なぜ、どのくらいの期間、自動的な決定がおこなわれているか；他の組織やさらなる処理がおこなわれているか；権利を行使する方法などの一連の情報を提供しなければなりません。第13条は、データが本人から直接収集される場合に適用され、第14条は、組織が他の情報源（公的情報源を含む）から個人データを取得する場合に適用されます。
    
*   **対象者アクセス権** : 個人は、第15条に基づき、自己のデータが処理されているかどうか、どのようなデータが、なぜ、どのくらいの期間処理されているか、自動的な決定がおこなわれているか；データのソースと受領者；権利行使の方法について問い合わせ、説明を受ける一般的な権利を有しています。さらに、他人の権利に影響を与えることなくそれが可能な場合、個人は自身のデータのコピーを受け取る権利を有します。何をいつ公開するかの判断は、特に要求者の身元が不明な場合には、複雑なものになる可能性があります。規制当局のガイダンス [^6] に基づいて構築されたIAMシステムは、エラーや不正行為のリスクを低減することができます。
    
*   **修正、消去、制限の権利** : 第16条（修正）は、不正確な個人情報を修正する権利であり、追加情報を追加する権利も含まれます。第17条（「消去」）では個人情報を保持するための合法的な根拠がない場合、個人情報を消去する権利を有します。これは、例えば、過剰な情報が保持されている場合、保管期限を超えて保持されている場合、または同意に基づいて処理されていた場合（下記参照）、その同意が撤回された場合に発生する可能性があります。第18条（「制限」）は、個人に対して、修正または異議申し立ての権利が処理されている間、あるいは法的請求のためにデータが必要な場合に消去に代わる手段として、データのさらなる処理（削除を含む）を阻止する権利を与えるものである。真実と管理の一元化を実現するIAMシステムにより、これらの権利の行使が容易になるはずです。
    

@row
## Legal Bases for Processing

To be lawful, any activity that involves processing personal data must be covered by one of the six legal bases set out in Article 6 of the GDPR. Note that the basis applies to a particular processing activity, not to a dataset. As illustrated in the example below, an IAM system may involve several different legal bases. While IAM professionals should probably not be determining the Legal Bases on behalf of their organisations, they need to be aware of the implications of that choice.

Various types of personal data – including race, ethnicity, and health – are considered higher risk and processing must be for one of the purposes set out in Article 9, as well as having an Article 6 basis. The requirements on processing these types – known as _Special Category Data_ – are often set in national, rather than European, legislation. IAM systems that process them should therefore consult lawyers familiar with the relevant national schemes. Similarly, although the GDPR highlights the extra risks involved in children’s personal data, the specific additional requirements – including the age below which someone is considered a child – are largely set at national level, so are not covered here.

Each of the Article 6 bases imposes additional conditions on processing, both by its definition and, in some cases, by explicit additions. Several of the bases also create additional obligations for organisations processing personal data and/or rights for individuals whose personal data are processed. The following sections describe these legal bases; here they are set out in the likely order of preference for organisations, rather than that in which they are listed in the legislation; those at the bottom of the list are significantly more onerous.

@column
## 処理の法的根拠

合法であるためには、個人データの処理を伴うすべての活動は、GDPRの第6条に規定されている6つの法的根拠のいずれかによってカバーされる必要があります。根拠はデータセットではなく、特定の処理活動に適用されることに注意してください。以下の例に示すように、IAMシステムにはいくつかの異なる法的根拠が含まれる場合があります。IAMの専門家は、恐らく多くの場合、組織に代わって法的根拠を決定するべきではありませんが、その選択の意味を認識する必要があります。

人種、民族性、健康状態など、さまざまな種類の個人データはリスクが高いと見なされ、処理は、第9条に定められた目的の1つのために、第6条の根拠を持たなければなりません。 __特殊なカテゴリデータ__ として知られているこれらの種類のデータの処理に関する要件は、多くの場合、欧州ではなく国内の法律で設定されています。したがって、それらを処理するIAMシステムは、関連する国内のスキームに精通した弁護士に相談する必要があります。 同様に、GDPR は子供の個人データに伴う追加のリスクを強調していますが、子供と見なされる年齢を含む特定の追加要件は主に国レベルで設定されているため、ここでは説明しません。

第6条のそれぞれの根拠は、その定義と、場合によっては明示的な追加された定義の両方によって、処理に追加の条件を課しています。また、いくつかの根拠は、個人データを処理する組織に追加の義務を課したり、個人データが処理される個人に権利を課したりします。以下のセクションでは、これらの法的根拠について説明します。ここでは、法律に記載されている順序ではなく、組織にとって優先される可能性が高い順序で記述されています。リストの一番下にあるものは、かなり面倒です。

@row
### Necessary for the Performance of a Contract

Five of the legal bases begin “necessary for…”. Regulators have confirmed that this means there must be no less intrusive way to achieve the purpose.

The inclusion of “performance of” indicates that there must be a particularly close link between the processing and the subject of the contract; the individual whose data are processed must also be a party to the contract. However, the term “contract” is likely to be widely interpreted, covering many situations where parties have made an agreement, even without a formal contract document. If stopping processing would make that agreement impossible to fulfil, then “necessary for contract” may well be an appropriate basis. This is likely to apply to many IAM systems, for example those provided for internal use by an employer or educator. Even for stand-alone IAM systems – so long as there is a direct relationship between the individual and the IAM provider – using “necessary for contract” may be a useful way to distinguish the minimum data and processing without which the service cannot function from optional data that the system can use but does not need. The latter should use the basis of “consent” described below. The European Data Protection Board’s Guidelines clarify that ancillary functions including service improvement, fraud prevention and online behavioural advertising are likely to need a different legal basis [^7] .

Where personal data are processed on this basis, the GDPR introduced a Right to Portability (Article 20) covering data “which \[the individual\] has provided”. This right may therefore cover only a subset of the information available under the general Subject Access Right, though the information must be provided “in a structured, commonly used and machine readable format”. So far, Regulators have only provided high-level guidance on this right, [^8] including suggesting that CSV might fulfil the format requirements, so further developments are likely.

@column
### 契約の履行のために必要

法的根拠のうち5つは「...のために必要」で始まります。規制当局は、これは目的を達成するために、より侵入性の低い方法があってはならないことを意味することを確認しています。

「履行」を含めることは、処理と契約の対象との間に特に密接な関係がなければならないことを示します；データが処理される個人は、契約の当事者でもある必要があります。しかし、「契約」という用語は広く解釈される可能性が高く、正式な契約文書がなくても、当事者が合意した多くの状況をカバーしています。処理を停止してその契約を履行することが不可能になる場合は、「契約に必要」が適切な根拠となる可能性があります。これは、雇用主や教育者が内部使用のために提供しているシステムなど、多くのIAMシステムに適用される可能性があります。スタンドアロンのIAMシステムであっても、個人とIAMプロバイダーの間に直接的な関係がある限り、「契約に必要」を使用することは、サービスが機能できない最小限のデータと処理と、システムが使用できるが必要としないオプションのデータを区別するのに役立つ場合があります。後者は、以下に説明する「同意」の基礎を使用する必要があります。欧州データ保護委員会のガイドラインは、サービス改善、詐欺防止、オンライン行動広告などの補助機能には、異なる法的根拠が必要になる可能性が高いことを明確にしています [^7] 。

これに基づいて個人データが処理される場合、GDPRは「\[個人\]が提供した」データを対象とするポータビリティ権（第20条）を導入しました。したがって、この権利は、一般的な対象者アクセス権の下で利用可能な情報のサブセットのみを対象とすることができますが、情報は「構造化され、一般的に使用され、機械で読み取り可能な形式で」提供する必要があります。これまでのところ、規制当局はこの権利に関する高レベルのガイダンスしか提供しておらず [^8] 、CSVがフォーマット要件を満たす可能性があることを示唆しているため、さらなる進展が見込まれます。

@row
### Necessary for Compliance with a Legal Obligation

Where a European or Member State law requires an organisation to process personal data, this is likely to be the appropriate legal basis. It is possible that this might apply to some national IAM schemes, and those in regulated industry sectors, but otherwise it is unlikely to be relevant.

@column
### 法的義務の遵守のために必要

欧州または加盟国の法律が組織に対して個人データの処理を要求している場合、これが適切な法的根拠となる可能性が高いです。一部の国のIAM制度や規制された産業部門に適用される可能性はありますが、それ以外には該当する可能性は低いでしょう。

@row
### Necessary in Order to Protect Vital Interests

This legal basis may apply when there is a threat to life or serious injury. We should hope that it is not relevant to our IAM systems!

@column
### 重要な利益を保護するために必要

この法的根拠は、生命または重大な傷害に対する脅威がある場合に適用される可能性があります。私たちのIAMシステムには関係ないことを祈るばかりです！

@row
### Necessary for the Performance of a Task Carried out in the Public Interest

This legal basis is typically used where a law permits processing for a public interest task but does not require it. Since national, and other statutory, IAM schemes will normally be subject to a legal requirement (see “legal obligation” above), rather than a permission, it seems unlikely to be relevant to IAM systems.

This basis gives individuals the Right to Object to processing, as described under “legitimate interests” below.

@column
### 公共の利益のために実行されるタスクの実施のために必要

この法的根拠は通常、法律が公共の利益のための処理を許可していますが、それを要求していない場合に使用されます。国およびその他の法的なIAM制度は通常、許可ではなく法的要件（上記の「法的義務」を参照）の対象となるため、IAMシステムに関連する可能性は低いと思われます。

この根拠は、以下の「正当な利益」に記載されているように、個人に処理に対する異議申し立ての権利を与えます。

@row
### Necessary for the Legitimate Interests of the Controller or a Third Party

Whereas the first four bases cover specific situations defined in law the last two (“legitimate interest” and “consent”) are more flexible and are therefore subject to more onerous requirements to protect individuals. This Legitimate Interests basis requires not just that the processing be necessary to achieve a specific purpose (the “interest”) but also that that interest be “legitimate” and, uniquely, that the benefits of processing not be overridden by its risks to individuals. A processing activity may be necessary for a legitimate interest, but still be unlawful if it cannot satisfy this balancing test.

Legitimate interest will, however, often be the most appropriate legal basis for multi-lateral IAM, for example where identity assertions are provided to external organisations ancillary to a contract for some other purpose. Organisations participating in federations – whether as identity providers, service providers, attribute authorities, or otherwise – are unlikely to know enough about the user’s reason for making a particular request to know whether it is necessary for a contract or, conversely, a situation where the individual is able to give free consent. Rather than trying to communicate that information among multiple parties or establishing a mesh of contracts among them, it is often simpler to consider the interest of each individual organisation in providing the service that the individual – by initiating an authentication or authorisation process – has requested of them.

This basis can only be used if “such interests are not overridden by the interests or fundamental rights and freedoms of the \[individual\] which require protection of personal data” (Article 6(1)(f)). Before an IAM organisation considers releasing (or requesting) information on this basis, it must therefore consider what risks might arise to the individual as a result of that disclosure. The mention of “fundamental rights and freedoms” indicates that risks beyond just data protection should be considered. Although this might appear onerous, the process can often be simplified, and implemented in the form of attribute release policies, by considering the types of data involved and what is known about the entities that will receive the information. Releasing a low-risk attribute to an organisation that has committed (or is required by its own applicable laws) to only use such data for service provision might be considered an acceptable risk, given that the individual must first have chosen to request federated authentication to that organisation’s services.

When using the legitimate interests basis, each individual has a “Right to Object” under Art.21. The legal requirement is to consider whether the organisation has “compelling legitimate grounds” for continuing the processing, in which case it may do so. In practice, since IAM systems should, in any case, only be processing the minimum information necessary to provide their service to users, an objection is effectively a request to stop using those parts of the service that rely on Legitimate Interests. An organisation might, therefore, respond to such a request by checking that that is, indeed, the individual’s intention.

@column
### 管理者または第三者の正当な利益のために必要な場合

最初の4つの根拠が法律で定められた特定の状況を対象としているのに対し、最後の2つ（「正当な利益」と「同意」）はより柔軟であるため、個人を保護するためのより厳しい要件に従わなければならないのです。この正当な利益の根拠は、特定の目的（「利益」）を達成するために処理が必要であるだけでなく、その利益が「正当」であること、そして特に、処理による利益が個人に対するリスクによって打ち消されないことを独自に要求しています。処理活動は、正当な利益のために必要であっても、このバランス・テストを満たすことができない場合は、依然として違法となる可能性があります。

しかし、正当な利益は、たとえばアイデンティティ・アサーションが他の目的のために契約に付随して外部組織に提供される場合など、多国間IAMにとって最も適切な法的根拠となることが多いです。フェデレーションに参加する組織は、アイデンティティプロバイダ、サービスプロバイダ、属性認証局またはその他のいずれであっても、特定の要求をおこなうユーザーの理由について、それが契約に必要であるか、逆に個人が自由な同意を与えることができる状況であるかを知るために十分な情報を持っているとは思われません。複数の当事者間でその情報を伝達しようとしたり、当事者間で契約のメッシュを確立したりするよりも、認証または認可プロセスを開始することによって、個人が要求したサービスを提供する各組織の利益を考慮する方が単純であることが多いです。

この根拠は、「そのような利益が、個人データの保護を必要とする\[個人\]の利益または基本的権利および自由によって打ち消されない」場合にのみ使用できます（第6条1項（f））。したがって、IAM組織がこのような根拠に基づいて情報の公開（または要求）を検討する前に、その開示の結果、個人にどのようなリスクが生じるかを検討する必要があります。「基本的な権利と自由」に言及していることから、データ保護以外のリスクも考慮する必要があることがわかります。負担が大きいように見えますが、関係するデータの種類と情報を受け取る主体について知っていることを考慮すれば、このプロセスはしばしば単純化され、属性公開ポリシーの形で実施することができます。サービス提供のためにのみデータを使用することを約束した（または独自の適用法で要求された）組織に低リスクの属性を開示することは、個人が最初にその組織のサービスへのフェデれーティッド認証を要求することを選択しなければならないことを考えると、許容できるリスクと考えられるかもしれません。

正当な利益を根拠とする場合、各個人は第21条に基づいて「異議申し立ての権利」を有します。法的な要件は、組織が処理を継続する「説得力のある正当な理由」を有しているかどうかを検討することであり、有している場合、処理を継続することができます。実際には、IAMシステムは、いかなる場合でも、ユーザにサービスを提供するために必要な最低限の情報しか処理しないはずなので、異議申し立ては、事実上、正当な利益に依存するサービスの部分の使用を停止するよう要求することになります。したがって、組織は、そのような要求に対して、それが本当に個人の意図であるかどうかを確認することで対応することができます。

@row
### Consent

The only legal basis that does not contain the word “necessary” is that the individual has given consent to processing. However, this is subject to significant conditions – in Article 7 and Recitals 32, 42 & 43 – which are likely to make consent inappropriate for much of the processing involved in IAM. Consent must be indicated by “a clear affirmative act establishing a freely given, specific, informed and unambiguous indication of the \[individual’s\] agreement”; it must be possible to withdraw consent at any time, as easily as it was given; consent will not be valid “if the \[individual\] has no genuine or free choice or is unable to refuse or withdraw consent without detriment”. Consent might be used where an IAM system can contain additional information, or support other processing, that is not necessary for its core function (for example nicknames), but in this case the individual has an absolute right to have that additional information removed, or the extra processing terminated, at any time.

In addition, consent sought by an employer, public authority, or other organisation with similar power over the individual is presumed not to be free. Consent must not be sought as a condition of providing a service. Organisations relying on consent must be able to demonstrate that it was obtained in accordance with these conditions. As for “contract” above, the Right to Portability applies to information obtained using consent.

@column
### 同意

「必要」という言葉が含まれていない唯一の法的根拠は、個人が処理に同意することです。しかし、これは非常に重要な状態（第7条および全文32、42、43）の対象になり、それはIAMに関連する多くの処理で同意が不適切になる可能性があります。同意とは「自由に与えられた、具体的で、情報に基づいた、明白な\[個人の\]賛同の意思表示に基づいた明確な肯定的な行動」によって示されなければなりません；同意が与えられたのと同じくらい簡単に、いつでも同意を取り消すことができなければなりません；「\[個人が\]、真に、自由な選択がなく、または不利益なしに同意を拒否したり、撤回できない場合」、同意は無効になります。同意は、IAMシステムがそのコア機能（例えばニックネーム）に必要ではない、追加情報や他の処理をサポートできる場合に利用されることがありますが、この場合は個人がいつでも追加情報を削除したり、追加のプロセスを終了させる絶対的な権利を有しています。

加えて、雇用主や公的機関、個人に対して同じような権力を有する他の組織が求める同意は自由ではないと推定されます。サービス提供の条件として同意を求めてはいけません。同意に依存する組織は、これらの条件にしたがって同意が得られたことを証明しなければなりません。上記の「契約」に関して、ポータビリティの権利は同意を得て取得した情報にも適用されます。

@row
### Summary

The “necessary” bases – usually either contract, legitimate interest, or legal obligation – are more suitable for the information necessary to maintain the relationship between the individual and the IAM system. With these, the organisation does not have to worry whether lawful consent was obtained, nor that it might be withdrawn on a whim. Consent should be reserved for information that the IAM system can handle but does not need: circumstances that are much more likely to satisfy the requirements for it to be valid. Consent, according to the UK’s Data Protection Regulator, should be an offer to the individual to enter into a deeper, more trusting, relationship. [^9]

@column
### サマリ

一般的に契約、正当な利益、法的な義務のような「必要な」根拠は、個人とIAMシステム間の関係を維持するために必要な情報により適しています。これらにより、組織は合法的な同意が得られたかどうか、気まぐれに同意を撤回される可能性を心配する必要がなくなります。同意は、IAMシステムが利用するが必須ではない情報のために事前に取得するべきです。これは、同意が有効であるという要件を満たす可能性が高いです。イギリスのデータ保護規則によれば、同意は個人がより深く、より信頼できる関係になるために個人に提供されるべきであるとしています。 [^9]

@row
### International Transfers

Any transfer of personal data from a country within the European Economic Area to one outside (commonly referred to as an “export”) requires its own legal basis. The full list of possible bases can be found in Articles 45-49. In practice, and unlike the previous Data Protection Directive, it will usually be possible to use the same legal basis for international IAM operations as those within Europe: regular transfers of personal data (for example between a customer organisation and a non-European IAM supplier) should normally be covered by a contract including one of the sets of Standard Contract Clauses; [^10] occasional, ad hoc, low-risk transfers should be able to use the legitimate interests basis; consent may be used where the individual is free to choose whether or not their personal information are transferred. Arrangements for international transfers are subject to change: for example both the original US Safe Harbor scheme and the Privacy Shield that replaced it have been declared invalid by the European Court of Justice; the latter case (“Schrems II”) also added new obligations for exporting organisations using the Standard Contract Clauses: new versions of the Clauses were issued by the European Commission in June 2021. [^11] Organisations operating international IAM systems should be aware of developments.

@column
### 国際的な転送

欧州経済圏内の国から外部の国への個人情報の転送（一般的に「輸出」と呼ばれます）には、独自の法的根拠が必要となります。可能性がある根拠の完全なリストは第45条から第49条に記載されています。実際には以前のデータ保護指令と異なり、通常国際的なIAM運用には欧州内の運用と同じ法的根拠を利用することができます：個人情報の定期的な転送（例えば顧客組織と非欧州IAM提供者の間）は通常、標準契約条項のひとつを含む契約によってカバーされる必要があります; [^10] 時折、アドホックに発生するリスクの低い転送は、正当な利益を根拠に利用できる必要があります；同意は、個人情報を転送するかどうかを個人が自由に選択できる場合に利用されます。国際的な転送の取り決めは変更される可能性があります：例えば、以前のアメリカのセーフハーバースキームとそれに変わるプライバシーシールドの両方は欧州司法裁判所によって無効であると宣言されました；後者（「Schrems II」）では、標準契約条項を利用した組織を輸出するための新しい義務が追加されました：現在、欧州委員会によって新しいバージョンの条項が提案されています。 [^11] 国際的なIAMシステムを運用する組織は開発に注意する必要があります。

@row
## Security

As well as requiring organisations to take proactive measures to protect the security of personal data, Article 33 of the GDPR introduces significant reporting requirements when an organisation becomes aware of a “breach of security leading to the accidental or unlawful destruction, loss, alteration, unauthorised disclosure of, or access to, personal data transmitted, stored or otherwise processed”. The wide definition of “breach” and the inclusion of “accidental” means that organisations should be particularly careful when designing, testing, and documenting processes that may alter, delete, or disclose data. All such breaches must be reported to the Regulator unless they are “unlikely to result in a risk to rights and freedoms of natural persons”. Loss of an encrypted memory stick, while the decryption key remains secure, is often given as an example of a breach that may not need to be reported. The expectation is that such reports will be sent within 72 hours: if not, then a satisfactory explanation for the delay must be included. Where a breach is likely to involve a “high risk” to individuals’ rights and freedoms, then a notification to affected individuals is required under Article 34.

The GDPR recognises in Recital 49 that the ability to detect, contain, and remedy security breaches is an important part of keeping data secure. Indeed, it has been suggested that failure to do so may itself be a breach of Article 33. [^12] Processing of personal data such as access and activity logs required for those purposes is recognised as a legitimate interest (so permitted, subject to the balancing test). Such logs must, of course, be held and processed securely. IAM can play a significant role in mitigating security breaches, by disabling compromised accounts quickly and effectively; its logs may also provide early warning when an organisation is under attack.

To meet the GDPR’s tight timescale for understanding and reporting breaches, organisations must plan, prepare, resource, and practice how they will respond to security incidents. This could include assessing which types of breach of the IAM system would require notification to regulators, individuals, or neither, as well as identifying and establishing contact with the internal and external partners whose help would be required.

@column
## セキュリティ

GDPRの第33条では、組織が個人データのセキュリティを保護するために積極的な対策を講じることを要求するだけでなく、組織が「転送、保管またはその他の方法で処理された個人データへの偶発的もしくは違法な破壊、紛失、改竄、不正な開示またはアクセスにつながるセキュリティ違反」に気がついた場合の重要な報告要件を導入しています。「違反」の広範な定義と「偶発的」の包含は、組織がデータを変更、削除または開示する可能性のあるプロセスを設計、テストおよび文書化する際に特に注意する必要があることを意味します。そのような違反はすべて、「自然人の権利と自由にリスクをもたらす可能性が低い」場合を除き、規制当局に報告する必要があります。暗号化されたメモリースティックの紛失は、報告する必要のない侵害の例としてよく挙げられますが、解読キーは安全なままです。このようなレポートは72時間以内に送信されることが期待されます：そうでない場合は、遅延について十分な説明を含める必要があります。侵害が個人の権利と自由に「高リスク」を伴う可能性が高い場合、影響を受ける個人への通知が第34条に基づいて義務付けられています。

GDPRは備考49で、セキュリティ違反を検出、封じ込め、修復する能力がデータを安全に保つための重要な部分であることを認識しています。実際、そうしないこと自体が第33条の違反である可能性があることが示唆されています。 [^12] これらの目的に必要なアクセスログやアクティビティログなどの個人データの処理は、正当な利益として認識されます（許可され、バランステストの対象となります）。もちろん、このようなログは安全に保持および処理する必要があります。IAMは、侵害されたアカウントを迅速かつ効果的に無効にすることにより、セキュリティ侵害を軽減する上で重要な役割を果たすことができます；そのログは、組織が攻撃を受けているときに早期警告を提供することもあります。

侵害を確認して報告するためのGDPRの厳しいタイムスケールを満たすために、組織はセキュリティ・インシデントへの対応方法を計画、準備、調達および実践する必要があります。これには、IAMシステムのどのタイプの侵害が規制当局または個人への通知を必要とするか、または通知を必要としないかを評価することならびに支援が必要となる内部および外部のパートナーとの連絡を特定して確立することが含まれます。

@row
## IAM Examples

The following examples show ways that IAM systems can support the GDPR.

@column
## IAM事例

IAMシステムでGDPRをサポートする方法を以下の例で紹介します。

@row
### Example 1: Outsourced Office Systems

John works at a small business, which has contracted with a cloud service provider to run its HR and office software services. As agreed in that contract, the service provider subcontracts the operation of email and document sharing to Google. John’s employer enters the information necessary for his employment role into a series of webforms; the service provider sets up the necessary accounts and document permissions. John’s personal data is processed on the basis that it is necessary for his contract of employment; only the information required to set up his email and document account is passed to Google.

In this example, John is the Data Subject and his employer is the Data Controller. Provided they only use information to provide the contracted services, the service provider and Google are Data Processors. If either were to use data for their own purposes – for example, to display customised adverts – then they would be Data Controller for that processing and be required to fulfil all the Data Controller’s obligations.

@column
### 事例1：オフィスシステムのアウトソーシング

Johnはとある中小企業に勤めており、その企業は、人事およびオフィスソフトウェアサービスの運営をクラウドサービスプロバイダーと契約しています。その契約では、サービスプロバイダーは、電子メールと文書共有の運用をGoogleに委託しています。Johnの雇用主は、彼の雇用上の役割に必要な情報を一連のウェブフォームに入力し、サービスプロバイダーは必要なアカウントと文書のアクセス許可を設定します。Johnの個人データは、彼の雇用契約に必要であるという理由で処理され、彼の電子メールと文書のアカウントを設定するために必要な情報のみがGoogleに渡されます。

この例では、Johnがデータ対象者であり、彼の雇用主がデータ管理者です。契約したサービスを提供するためだけに情報を使用するのであれば、サービスプロバイダーとGoogleはデータ処理者です。どちらかが自分たちの目的のためにデータを使用する場合（例えば、カスタマイズされた広告を表示する場合）、その処理についてはデータ管理者となり、データ管理者のすべての義務を果たすことが要求されることになります。

@row
### Example 2: Federated Access Management

Janet is a professor at the University of Erewhon. The university has a central IAM system containing the details of all staff required for them to do their jobs. This information is stored and processed on the legal basis that it is necessary for Janet’s contract of employment with the university: without doing so, it would be impossible to perform that contract. The IAM system acts as a single point of truth, so ensuring that information is up to date throughout the university and that any correction requests can be easily implemented.

The IAM system also allows Janet to store optional information, such as her personal interests, that will appear on her staff webpage. Since she can add, change, or remove these at any time, without affecting her work, the appropriate legal basis is consent.

The university is also a member of an Authentication & Authorisation Infrastructure (AAI) Federation. When Janet accesses a website of another Federation member (for example, a journal publisher), she can choose to log in with her university credentials. A wide variety of organisations are Federation members since – with the university taking responsibility for providing verified information and ensuring its users’ good behaviour – this allows them to receive and process considerably less personal data, in accordance with the data minimisation principle. Janet needs to access some of these for her work, but others may be just for personal interest. Since neither the university nor the sites wish to work out which sites are necessary for contract and which accessed with free consent (where Janet needs to access a site for work, her consent cannot be free) they both use the legal basis that the processing is necessary in their legitimate interest in helping Janet access the information she wants.

The legitimate interests basis requires the university to balance the risks of releasing information against the benefits. Since the federation agreement requires members only to use authentication and other attributes for the purposes of service provision and personalisation, and not to attempt to identify pseudonymous users, the university assesses that there is very little risk in releasing a unique opaque identifier and Janet’s status as a member of staff to any Federation member; it has therefore configured its systems to release that information by default when a user requests a federated login. This is sufficient both for Janet to access online journals, and to verify her entitlement to a staff discount at the local health club.

The Federation has defined a class of services that are specifically designed for Research and Education use, and that require a name and email address in addition to the opaque identifier and status. This additional requirement is mentioned in the services’ privacy notices. Although this disclosure involves a slightly higher risk, the university is satisfied that this is justified by the greater benefit; such services will therefore receive the additional information by default. This allows Janet to use discussion groups and virtual research environments in her field.

Where services ask for more information, the university will perform an individual assessment of the benefit and risk. This may indicate that additional measures, such as a bilateral contract or the free consent of each individual, are required to reduce the risk of the disclosure.

In this example, Janet is the Data Subject. Both the university and the service provider are Data Controllers, since the service provider chooses which services to offer to Janet.

@column
### 事例2：統合アクセス管理

JanetはErewhon大学の教授です。同大学は、職員が業務を遂行するために必要な全職員の詳細情報を含む中央IAMシステムを持っています。この情報は、Janetの大学との雇用契約に必要であるという法的根拠に基づいて保管・処理されます。そうしなければ、その契約を履行することは不可能です。IAMシステムは信頼できる唯一の情報源として機能するため、大学全体で情報が最新であることを保証し、修正要求があれば簡単に実行することができます。

また、IAMシステムによって、Janetは自分の個人的な興味などの任意情報を保存し、スタッフのウェブページに表示させることができます。Janetは、自分の仕事に影響を与えることなく、いつでもこれらの情報を追加、変更、削除できるため、適切な法的根拠は「同意」です。

また、同大学はAuthentication & Authorisation Infrastructure（AAI）連盟のメンバーでもあります。Janetが他の連盟メンバー（例えばジャーナル出版社）のウェブサイトにアクセスする際、大学の認証情報でログインすることを選択することができます。大学が検証された情報を提供し、ユーザーの適切な行動を確保する責任を負うことで、データ最小化の原則に基づき、個人データの受信と処理を大幅に減らすことができるため、さまざまな組織が連盟のメンバーになっています。Janetは、仕事のためにこれらのサイトにアクセスする必要がありますが、他のサイトは個人的な興味でアクセスすることもあります。大学もサイトも、どのサイトが契約に必要で、どのサイトが自由な同意でアクセスしたかを調べようとはしないので（Janetが仕事でサイトにアクセスする必要がある場合、彼女の同意は自由ではありえない）、Janetが望む情報にアクセスできるようにするという正当な利益のために処理が必要であるという法的根拠を用いることになります。

正当な利益の根拠は、情報を公開するリスクと利益のバランスをとることを大学に要求しています。フェデレーション契約では、メンバーは認証と他の属性をサービス提供とパーソナライゼーションのためにのみ使用し、仮名ユーザーを識別しようとしないことが要求されているので、大学は、ユニークな不透明識別子とJanetのスタッフとしての地位をフェデレーションメンバーに公開するリスクはほとんどないと評価しています。Janetがオンラインジャーナルにアクセスするにも、地元のヘルスクラブでスタッフ割引を受ける資格を確認するにも、この情報で十分です。

Federationは、特に研究・教育利用を目的としたサービスのクラスを定義し、不透明な識別子とステータスに加えて、名前と電子メールアドレスを要求しています。この追加要件は、各サービスのプライバシー通知で言及されています。この開示には若干のリスクが伴いますが、より大きな利益によって正当化されると大学側は考えており、そのようなサービスではデフォルトで追加情報を受け取ることになります。これにより、Janetはディスカッショングループや仮想研究環境を自分の専門分野で利用することができるようになりました。

サービスがより多くの情報を求める場合、大学は利益とリスクの個別評価を実施します。これにより、開示のリスクを軽減するために、二者間契約や各個人の自由な同意などの追加的な措置が必要であることが示される場合があります。

この例では、Janetがデータ対象者です。サービス提供者はJanetに提供するサービスを選択するため、大学およびサービス提供者の両方がデータ管理者です。

@row
## Author Bio

Andrew Cormack is Chief Regulatory Adviser at Jisc. He has been involved in the technical and policy development of federated identity systems in the UK, Europe, and globally for more than fifteen years. He has spoken and written extensively on how digital technologies can be used to improve privacy and data protection and, more recently, on the application of the GDPR to them. His publications can be found at [https://orcid.org/0000-0002-8448-2881](https://orcid.org/0000-0002-8448-2881) and his blogs at [https://community.jisc.ac.uk/blogs/regulatory-developments](https://community.jisc.ac.uk/blogs/regulatory-developments) .

@row
## Change Log

| Date | Change |
| --- | --- |
| 2021-06-30 | Updated based on [https://github.com/IDPros/bok/issues/42](https://github.com/IDPros/bok/issues/42) , https://github.com/IDPros/bok/issues/41 |
| 2022-09-30 | Updated information on The EU Standard Contract Clauses |

@row
- - -

[^1]:  “EU General Data Protection Regulation (GDPR): Regulation (EU) 2016/679 of the European Parliament and of the Council of 27 April 2016 on the protection of natural persons with regard to the processing of personal data and on the free movement of such data, and repealing Directive 95/46/EC (General Data Protection Regulation),” OJ 2016 L 119/1. 
    
[^2]:  GDPR Art.4(1) 
    
[^3]:  GDPR Art.4(2) 
    
[^4]:  “Council of Europe Data Protection website,” Council of Europe, accessed October 10, 2019, https://www.coe.int/en/web/data-protection/home. 
    
[^5]:  Note that some public authorities are excluded from GDPR, notably institutions of the European Union itself and law enforcement and national security agencies when performing those tasks. These will normally be subject to other legislation that applies the same principles: for example, Regulation 2018/1725 for EU bodies and Directive 2016/680 for law enforcement. 
    
[^6]:  See, for example, the UK Regulator at https://ico.org.uk/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/individual-rights/right-of-access/ 
    
[^7]:  European Data Protection Board, “Guidelines 2/2019 on the processing of personal data under Article 6(1)(b) GDPR in the context of the provision of online services to data subjects,” Version 2.0, 8 October 2019, https://edpb.europa.eu/sites/default/files/files/file1/edpb\_guidelines-art\_6-1-b-adopted\_after\_public\_consultation\_en.pdf. 
    
[^8]:  “Guidelines on the right to "data portability",” revision (wp242rev.01), European Commission, last modified October 27, 2017, https://ec.europa.eu/newsroom/article29/item-detail.cfm?item\_id=611233. 
    
[^9]:  “When is consent appropriate?” Information Commissioner’s Office, accessed October 10, 2019, https://ico.org.uk/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/consent/when-is-consent-appropriate/#when3. 
    
[^10]:  “Standard Contractual Clauses: Standard contractual clauses for data transfer between EU and non-EU countries,” European Commission, accessed October 10, 2019, https://ec.europa.eu/info/law/law-topic/data-protection/data-transfers-outside-eu/model-contracts-transfer-personal-data-third-countries\_en. 
    
[^11]:  European Commission, “Standard Contractual Clauses (SCC),” website, [https://ec.europa.eu/info/law/law-topic/data-protection/international-dimension-data-protection/standard-contractual-clauses-scc\_en](https://ec.europa.eu/info/law/law-topic/data-protection/international-dimension-data-protection/standard-contractual-clauses-scc_en) (accessed 27 September 2022). 
    
[^12]:  “Guidelines on Personal data breach notification under Regulation 2016/679,” Article 29 Data Protection Working Party, last revised and adopted on February 6, 2018, https://ec.europa.eu/newsroom/article29/document.cfm?action=display&doc\_id=49827 
