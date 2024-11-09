---
layout: columns
title: Laws Governing Identity Systems (v2)
permalink: /docs/oidc_oauth/idpro_bok/8
date: 2024-09-09
modify_date: 2024/11/10
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "GDPR", "法律"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/8/](https://bok.idpro.org/article/id/8/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

Identity systems and their participants are governed by a myriad and complex set of laws, regulations, and contractual requirements. This article offers a high-level overview of the legal environment that governs identity systems, focusing on three different levels of legal rules: General Law, Generic Identity System Law, and Individual Identity System Rules.

Keywords: GDPR, System Law, General Law, Rules, Contract, California


@column
## 概要

アイデンティティシステムとその参加者は無数の複雑な一連の法律、規制および契約要件によって管理されています。本記事では、3つの異なるレベルの法規制、つまり一般法、汎用アイデンティティシステム法および個別のアイデンティティシステム規則に焦点を当てながら、アイデンティティシステムを管理する法的環境の大まかな概要を提供します。

Keywords: GDPR, システム法, 一般法, ルール, 契約, カリフォルニア


@row
Thomas J. Smedinghoff

© 2021, IDPro, Thomas J. Smedinghoff

@row
## Table of Contents

[Abstract 1](#abstract)

[Introduction 2](#introduction)

[Terminology 2](#terminology)

[The Identity System Legal Environment 2](#the-identity-system-legal-environment)

[The Legal Rules Governing Identity Systems 5](#the-legal-rules-governing-identity-systems)

[Level 1 – General Law 5](#level-1-general-law)

[Level 2 – Generic Identity System Law 8](#level-2-generic-identity-system-law)

[Level 3 – Individual Identity System Rules 9](#_Toc75947543)

[Author Bio 12](#author-bio)

[Change Log 12](#change-log)

@row
## Introduction

What are the legal rules that govern identity systems? What obligations do those rules impose on the participants involved?

The reality is that identity systems and their participants are governed by a myriad and complex set of laws, regulations, and contractual requirements, and the obligations they impose are not always clear. To make sense of it all, it is best to focus first on the legal environment that governs identity systems.

@column
## 導入

アイデンティティシステムを管理する法的規則は何でしょうか？これらの規則は、関与する参加者にどのような義務を課すでしょうか？

現実には、アイデンティティシステムとその参加者は、無数かつ複雑な一連の法律、規制および契約上の要件によって管理されており、それらが課す義務は必ずしも明確ではありません。すべてを理解するには、まずアイデンティティシステムを管理する法的な環境に注目するのが最善です。

@row
### Terminology

*   Consumer Protection Law - laws and regulations that are designed to protect the [rights](https://en.wikipedia.org/wiki/Rights) of individual [consumers](https://en.wikipedia.org/wiki/Consumers) and to stop unfair, deceptive, and fraudulent business practices.
    
*   Contract Law – laws that relate to making and enforcing agreements between or among separate parties.
    
*   Fraud Law – laws that protect against the intentional misrepresentation of information made by one person to another, with knowledge of its falsity and for the purpose of inducing the other person to act, and upon which the other person relies with resulting injury or damage.
    
*   Identity Theft Law – laws governing crimes in which the perpetrator gains access to sensitive personal information belonging to the victim (such as birth dates, passwords, email addresses, driver’s license numbers, social security numbers, financial records, etc.), and then uses this information to impersonate the victim for personal gain, such as to commit fraud, establish credit in the victim’s name, or access the victim’s accounts.
    
*   Privacy Law - laws that regulate the collection, use, storage, and transfer of personal data relating to identified or identifiable individuals.
    
*   Tort Law - the body of law that covers situations where one person’s behavior causes injury, suffering, unfair loss, or harm to another person, giving the injured person (or the person suffering damages) a right to bring a civil lawsuit for compensation from the person who caused the injury. Examples include battery, fraud, defamation, negligence, and strict liability.
    

@column
### 用語解説

*   消費者保護法 - 個々の[消費者](https://en.wikipedia.org/wiki/Consumers)の[権利](https://en.wikipedia.org/wiki/Rights)を保護し、不公正、欺瞞的、詐欺的な商慣行を阻止することを目的とした法律および規制。
    
*   契約法 -  異なる当事者間での合意の作成および施行に関連する法律。
    
*   詐欺法 - 虚偽であることを知りながら、他者に行動を起こさせて他者が怪我をおったり、損害を受けたりするようにすることを目的として、意図的に情報を詐称することに対する法律。
    
*   個人情報窃取法 - 加害者が被害者の機密個人情報（生年月日、パスワード、Eメールアドレス、運転免許証番号、社会保障番号、財務記録など）へのアクセス権を入手し、その情報を使って詐欺や被害者の氏名を使って信頼を獲得する、被害者のアカウントにアクセスするような個人の利益のために被害者になりすますという犯罪を管理するための法律。
    
*   プライバシー法 - 識別された、または識別可能な個人に関する個人データの収集、利用、保管、転送を規制する法律。
    
*   不法行為法 - ある人の行動が他者に傷害、苦痛、不当な損失または危害を引き起こす状況を対象とする法律の体系であり、傷害を被った人（または損害を被った人）に、その原因を作った人からの賠償を求める民事訴訟をおこす権利を与えます。例えば、暴行、詐欺、名誉毀損、過失、厳格責任が含まれます。
    

@row
## The Identity System Legal Environment

At a high level, the legal environment that governs the operation of any identity system consists of three different levels of legal rules, categorized as follows:

*   Level 1: General Law : The first level is law that applies generally to all business and personal activities. This law covers a wide variety of subjects and is not written with identity systems in mind, although it is frequently applied to identity system activities where appropriate. Examples of general law that might affect the operation of an identity system include contract law, tort law, privacy law, warranty law, and consumer protection law.
    
*   Level 2: Generic Identity System Law : The second level of legal rules consists of law written specifically to govern identity systems generally. Level 2 identity management laws typically apply to all identity systems within a jurisdiction and are often relatively high level in nature. At present, however, very few such Level 2 laws exist. Examples of such generic identity system law include Virginia’s Electronic Identity Management Act [^1] and the Draft Provisions on the Cross-border Recognition of IdM and Trust Services [^2] being developed by the UN Commission on International Trade Law (UNCITRAL). In many jurisdictions, Level 2 law for identity systems does not yet exist.
    
*   Level 3: Individual Identity System Rules : The third level of legal rules consists of the set of system-specific rules written to govern the operation of a particular identity system. These rules provide the technical, business, and operational specifications and rules for the identity system, specify the rights and responsibilities of the participants and govern the relationships between the various parties. They can be quite detailed but apply only within the confines of the identity system they were written to govern.
    

For private sector identity systems, these legal rules are typically contract-based, are often referred to as a trust framework or system rules, and apply only to those system participants who have contractually agreed to be bound to them. Examples include the SAFE Identity Trust Framework (previously the SAFE-BioPharma Trust Framework), [^3] the Sovrin Governance Framework, [^4] and the SecureKey Concierge Trust Framework. [^5]

For government identity systems, these Level 3 legal rules are often embodied in a law or regulation enacted by the government and thus automatically apply to all those who participate in the identity system. Examples include the eIDAS Regulation in the European Union, [^6] the Identity Documents Act in Estonia, [^7] and the Aadhaar Act in India. [^8] In some cases, however, government identity systems also use contract-based trust frameworks, such as the Trusted Digital Identity Framework (TDIF) [^9] for the Australian national federated identity system.

The Level 3 portion of the legal environment for any identity system is under the control of the developers of that identity system (government or private sector). That is, the operators of a private sector identity system are free to make up the Level 3 system rules and design them in the manner best suited to meet the goals of that specific identity system. However, where such rules are contract-based, they will apply only to the participants that agree to be bound by them, and they may be supplemented (and in some cases overruled) by existing laws and regulations at Levels 1 or 2. In other words, the Level 3 rules designed for any specific identity system must comply with existing law – a challenge made all the more difficult for identity systems that cross jurisdictional boundaries.

The structure of this identity system legal environment

is summarized on the diagram below.

@column
## アイデンティティシステムの法的環境

大まかなには、あらゆるアイデンティティシステムの運用を管理する法的環境は、以下のように分類された3つの異なるレベルの法的規則で構成されています：

*   レベル1: 一般法 : 最初のレベルは、すべてのビジネスおよび個人活動に一般的に適用される法律です。この法律は広範な主題を対象としており、アイデンティティシステムを念頭に置いて書かれているわけではありませんが、適切な場合にはアイデンティティシステムの活動に適用されることが多くあります。アイデンティティシステムの運用に影響を与える可能性のある一般法の例としては、契約法、不法行為法、プライバシー法、保証法および消費者保護法などがあります。
    
*   レベル2: 汎用アイデンティティシステム法 : 法的規制の2つ目のレベルは、特にアイデンティティシステム全般を管理するために書かれた法律から構成されます。レベル2のアイデンティティ管理法は通常、法域内のすべてのアイデンティティシステムに適用され、多くの場合、性質が比較的高度です。しかし現在では、そのようなレベル2の法律はほとんど存在しません。そのような汎用アイデンティティシステム法の例には、バージニア州の電子アイデンティティ管理法 [^1] や、国連国際貿易法委員会（UNCITRAL）によって作成中のIdMおよびトラストサービスの国境を越えた承認に関する草案 [^2] があります。多くの法域では、アイデンティティシステムのレベル2にあたる法律はまだ存在しません。
    
*   レベル3: 個別のアイデンティティシステム規則 : 法的規則の3つ目のレベルは、特定のアイデンティティシステムの運用を管理するために書かれた一連のシステム固有の規則で構成されています。これらの規則は、アイデンティティシステムの技術、ビジネスおよび運用の仕様と規則を提供し、参加者の権利と責任を特定し、さまざまな当事者間の関係を管理します。これらはかなり詳細に記述することができまｓが、管理するために記述されたアイデンティティシステムの範囲内にのみ適用されます。
    

民間のアイデンティティシステムの場合、これらの法的規則は一般に契約ベース、しばしばトラストフレームワークまたはシステム規則と呼ばれる、であり、契約に拘束されることに同意したシステム参加者にのみ適用されます。例としては、SAFE Identity Trust Framework（以前は SAFE-BioPharma Trust Framework） [^3] 、Sovrin Governance Framework [^4] 、およびSecureKey Concierge Trust Framework [^5] が存在します。

政府のアイデンティティシステムの場合、これらのレベル3の法的規則は、多くの場合政府によって制定された法律または規制で具体化され、したがってアイデンティティシステムに参加するすべての人に自動的に適用されます。例としては、欧州連合のeIDAS規則 [^6] 、エストニアのアイデンティティ文書法 [^7] 、およびインドのAadhaar法 [^8] があります。しかし、場合によっては、政府のアイデンティティシステムは、オーストラリア国家連携アイデンティティシステムのTrusted Digital Identity Framework（TDIF） [^9] のような契約ベースのトラストフレームワークを利用することもあります。

あらゆるアイデンティティシステムの法的環境のレベル3部分は、そのアイデンティティシステムの開発者（政府または民間企業）の管理下にあります。つまり、民間企業のアイデンティティシステムの運用者は、レベル3のシステム規則を自由に作成し、その特定のアイデンティティシステムの目的を達成するために最適な方法で設計することができます。ただし、そのような規則が契約ベースである場合、その規則に拘束されることに同意した参加者にのみ適用され、レベル1またはレベル2の既存の法律および規則によって補完される（場合によっては覆される）可能性があります。言い換えれば、特定のアイデンティティシステム向けに設計されたレベル3の規則は、既存の法律に準拠しなければなりません。この課題は、法域の境界を越えるアイデンティティシステムにとってさらに難しくなります。

このアイデンティティシステムの法的環境の構造は、

下の図にまとめられています。

@row
![Three levels of rules governing identity systems: General Law, Generic Identity System Law, and Invidual Identity System Rules ](/assets/images/idpro_bok/laws-governing-idsystems-image001.jpeg)

@row
This structure of the identity system legal environment is very similar to that which governs a credit card system (such as Amex ® , Discover ® , MasterCard ® , or Visa ® ). Each credit card system is governed by Level 3 system rules developed by the operator of that system (e.g., the MasterCard Rules [^10] and the Visa Core Rules and Visa Product and Service Rules [^11]). Those rules provide the technical, business, and operational specifications for the specific credit card system and govern the relationships between the various parties. They are made binding on the parties that participate in the system (e.g., credit card holders, merchants, issuing banks, processors, etc.) by contract.

Those Level 3 credit card system rules and the associated contracts are also governed by: (1) Level 1 general law (e.g., the law of contracts, the law of negligence, etc.), and (2) Level 2 generic credit card system law written to regulate all credit card systems (e.g., Regulation Z [^12] in the US). Like the legal environment governing identity systems, this combination of Level 3 system rules and contracts and Level 1 and 2 law forms the legal environment in which each credit card system operates.

@column
アイデンティティシステムの法的環境の構造は、クレジットカードシステム（Amex ® 、Discover ® 、MasterCard ® やVisa ® のような）を管理するものと非常に似ています。それぞれのクレジットカードシステムは、そのシステムの運用者によって作成されたレベル3のシステム法(例えば、MasterCard Rules [^10] 、Visa Core Rules and Visa Product and Service Rules [^11] )によって管理されています。これらのルールは技術、ビジネスおよび運用の仕様を特定のクレジットカードシステムに提供しており、様々な関係者間の関係を管理しています。ルールはシステムに参加する関係者’クレジットカード所有者、加盟店、発行銀行、処理業者など）を契約によって縛ります。

これらのレベル3のクレジットカードシステムのルールと関連する契約は、（1）レベル1の一般法（例えば、契約法、過失法など）、および (2) すべてのクレジットカードシステムを規制するために書かれたレベル2の一般的なクレジットカードシステムの法律（例: 米国のレギュレーションZ [^12] ）にも準拠しています。 アイデンティティシステムを管理する法的環境と同様に、レベル3のシステムのルールと契約およびレベル1とレベル2の法律の組み合わせによって、各クレジットカードシステムが運用される法的環境が形成されます。

@row
## The Legal Rules Governing Identity Systems

@column
## アイデンティティシステムを管理する法的規則

@row
### Level 1 – General Law

Currently, most law applicable to identity systems is general law (Level 1). Typically, this law was written for a purpose completely unrelated to identity management (e.g., tort law, contract law, warranty law, privacy law, etc.) and without considering how it might apply to identity systems. In fact, in many cases it was written before the concept of identity systems even existed. And in some cases, the law developed over hundreds of years via common law and court decisions. Nonetheless, such general law often applies to identity system-related activities, often in ways that were unanticipated at the time of its original adoption.

Identity systems primarily deal in information. Thus, the Level 1 law that applies to identity systems will typically include those laws that address various aspects of transactions involving information. This primarily includes law governing the following aspects of information:

@column
### レベル1 - 一般法

現在、アイデンティティシステムに適用されるほとんどの法律は一般法（レベル1）です。通常、この法律はアイデンティティ管理とはまったく関係のない目的（不法行為法、契約法、保証法、プライバシー法など）のために書かれており、アイデンティティシステムにどのように適用されるかを考慮していません。実際、多くの場合、アイデンティティシステムの概念が存在する前に作成されました。また、場合によっては、法律というものは慣習法や裁判所の判決を通じて、何百年もかけて発展してきました。にもかかわらず、一般的な法律は、多くの場合、最初の採用時には予期されていなかった方法で、アイデンティティシステム関連の活動に適用されます。

アイデンティティシステムは主に情報を扱います。したがって、アイデンティティシステムに適用されるレベル1の法律には、通常、情報を含むトランザクションのさまざまな側面に対処する法律が含まれます。これには主に、情報の次の側面を管理する法律が含まれます。

@row
> \-- Collection, Use, and Transfer of Identity Information

Identity information about individuals is personal data, and identity system processes typically involve the collection and processing (by an identity provider, attribute provider, or its agents) and disclosure (to a relying party) of such personal data about a subject. Thus, _**privacy**_ laws will regulate the collection, storage, use, and transfer of identity information and will have a major impact on all identity system participants and all identity system transactions. This may include, for example, imposing limits on what data may be collected, requirements regarding notices of collection practices, limits on the use that may be made of such data, and restrictions on the transfer of such data to third parties and/or across country boundaries.

@column
> \-- アイデンティティ情報の収集、利用および転送

個人に関するアイデンティティ情報は個人データであり、アイデンティティシステムプロセスは通常、主体に関する個人データの（アイデンティティプロバイダー、属性プロバイダーまたはそのエージェントによる）収集および処理ならびに（リライングパーティーへの）開示を含みます。したがって、 _**プライバシー**_ 法はアイデンティティ情報の収集、保管、利用および転送を規制し、アイデンティティシステムの全ての参加者および全てアイデンティティシステムトランザクションに大きな影響を与えることになります。これには、例えば、収集できるデータの制限、収集慣行の通知に関する要件、データの利用に関する制限、第三者および／または国境を越えたデータの転送に関する制限を課すことができます。

@row
> \-- Accuracy of Identity Information

A key concern of all participants in an identity system relates to the accuracy and reliability of the identity information they are communicating or relying upon. Inaccurate identity data can cause a variety of problems for persons who rely on that data, as well as liability for those who provide it.

Laws governing providing false or incorrect information, whether intentionally or negligently, will be relevant in the evaluation of the rights, obligations, and liabilities of the participants in identity systems, including identity providers, attribute providers, and data subjects.

Key among them are _**fraud**_ laws and _**identity theft**_ laws. Fraud involves a representation of fact (or material omission of fact) that is intended to deceive another to their material detriment. Identity theft occurs when a party acquires, transfers, possesses, or uses someone’s personal information in an unauthorized manner, with the intent to commit, or in connection with, fraud or other crimes.

Even in the absence of fraud, the tort of _**negligent misrepresentation**_ can create liability for communicating false information. This occurs where the information is intended for the guidance of others in their business transactions, but the information provider did not exercise reasonable care in determining the accuracy of the information prior to the communication. Thus, in certain circumstances, an incorrect assertion of one or more identity attributes might qualify as a negligent misrepresentation.

This tort of negligent misrepresentation creates a duty to exercise reasonable care or competence to verify facts and creates liability for incorrect representations made without exercising reasonable care about the accuracy of the facts asserted. However, it does not make the supplier of information (e.g., the identity provider) a guarantor of the accuracy of an identity assertion. Generally, the information provider does not have liability for inaccurate or “false” information unless the provider failed to exercise reasonable care in obtaining or communicating the information.

To the extent that incorrectly communicated identity information damages the reputation of the data subject, the tort of _**defamation**_ may also be relevant. Defamation involves a false or disparaging statement of fact about a person that is published to a third party causing the person to suffer harm. It is possible that incorrect identity or attribute assertions could be considered defamatory in certain situations. For example, asserting an inaccurate attribute – e.g., age, medical information, sexual orientation, political affiliation, or employment -- might be considered defamatory in certain cases where the named person suffered harm as a result.

The accuracy or reliability of identity attribute information communicated to a relying party by an identity provider or attribute provider may also be governed by _**warranty**_ law. A warranty is an assurance, promise, or guaranty by one party to another party that facts or conditions are true and may be relied upon by the other party.

A warranty may be either express or implied. An _express warranty_ arises from specific statements made by one party to another. Such statements may be made in writing, such as in a contract or advertisement, or may be made orally, such as by a sales representative. For example, an identity provider’s published processes may include a warranty regarding the quality of the information it provides to relying parties.

An _implied warranty_ is an unspoken, unwritten promise created by law that arises from the nature of the transaction and the inherent understanding by the recipient rather than from the express representations of the provider. Implied warranties are based upon the common law principle of “fair value for money spent.” Thus, for example, a court could conceivably conclude that identity providers make implied warranties regarding the reasonableness of the processes they used to collect and verify identity attribute data.

Finally, it is important to note that some privacy laws also regulate the accuracy of personal data. The EU GDPR, for example, requires that personal data maintained by data controllers (such as identity providers) must be “accurate and, where necessary, kept up to date” and that “every reasonable step must be taken to ensure that personal data that are inaccurate … are erased or rectified without delay.” Article 5(1)(d). In addition, it provides that “The data subject shall have the right to obtain from the controller without undue delay the rectification of inaccurate personal data concerning him or her.” Article 16.

@column
> \-- アイデンティティ情報の正確性

アイデンティティシステムのすべての参加者の主要な懸念は、通信しているまたは依存しているアイデンティティ情報の正確性および信頼性に関連します。不正確なアイデンティティデータは、そのデータに依存する人にさまざまな問題を引き起こし、それを提供する人に責任を負わせる可能性があります。

意図的であろうと過失であろうと、虚偽または不正確な情報の提供を統制する法律は、アイデンティティプロバイダ、属性プロバイダおよびデータ主体などのアイデンティティシステムの参加者の権利、義務および責任を評価する際に関連します。

中でも重要なのは、 _**詐欺**_ に関する法律と _**アイデンティティ窃取**_ に関する法律です。詐欺には、他者を欺いてその重大な不利益をもたらすことを意図した事実の表現（または重大な事実の省略）が含まれます。アイデンティティ窃取は、詐欺やその他の犯罪をおこなう、またはそれに関連する目的で、不正な方法で誰かの個人情報を取得、転送、所有または利用する場合に発生します。

詐欺がない場合でも、 _**過失による不当表示**_ という不法行為は、虚偽の情報を伝達したことに対する責任を生じさせる可能性があります。これは、情報が他の商取引のガイダンスを意図したものであるにもかかわらず、やりとりの前に情報提供者が情報の正確さを判断する上で合理的な注意を払わなかった場合に発生します。したがって、特定の状況では、1つ以上のアイデンティティ属性の不正確な表明が過失による不当表示として認められる場合があります。

この過失による不当表示という不法行為は、事実を確認するために合理的な注意または能力を行使する義務を生じさせ、主張された事実の正確性について合理的な注意を行使せずにおこなわれた不正確な表示に対する責任を生じさせるものです。しかし、それは情報の供給者（たとえばアイデンティティプロバイダ）をアイデンティティアサーションの正確性の保証人にするものではありません。一般に、情報提供者は、情報の入手または伝達において合理的な注意を払わなかった場合を除き、不正確なまたは「偽」の情報に対して責任を負いません。

不正に伝達されたアイデンティティ情報がデータ主体の評判に損害を与える限り、_**名誉毀損**_ の不法行為も関連する可能性があります。名誉毀損には、第三者に公表され、その人が損害を被る原因となった、ある人についての虚偽のまたは中傷的な事実の記述が含まれます。特定の状況では、不正確なアイデンティティや属性の表明が名誉棄損とみなされる可能性があります。たとえば、年齢、医療情報、性的指向、政治的所属、雇用など不正確な属性を開示することは、指名された人物が結果として損害を被った特定のケースでは、名誉毀損と見なされる可能性があります。

アイデンティティプロバイダまたは属性プロバイダによってリライングパーティに伝達されたアイデンティティ属性情報の正確性または信頼性は、 _**保証**_ 法によって管理される場合もあります。保証とは、ある当事者が他の当事者に対して、事実または状態が真実であり、他の当事者によって信頼される可能性があることが保証（assurance）、約束または保証（guaranty）することです。

保証は、明示または暗黙のいずれかになります。 __明示的な保証__ は、当事者の一方が他方に対しておこなった特定の記述から生じます。そのような記述は、契約書や広告など書面でおこなわれる場合もあれば、営業担当者など口頭でおこなわれる場合もあります。たとえば、アイデンティティプロバイダーの公開プロセスには、リライングパーティに提供する情報の品質に関する保証が含まれる場合があります。

__暗黙の保証__ は、プロバイダの明示的な表示からではなく、取引の性質および受領者による固有の理解から発生する、法律によって作成される暗黙の不文律の約束です。暗黙の保証は、「費やしたお金に対する公正な価値」という判例法の原則に基づいています。したがって、たとえば裁判所はアイデンティティプロバイダがアイデンティティ属性データを収集および検証するために使用したプロセスの合理性に関して暗黙の保証をおこなうと結論付けることが考えられます。

最後に、一部のプライバシー法は個人データの正確さも規制していることに注意することが重要です。たとえば、EU GDPRはデータ管理者（アイデンティティプロバイダなど）が保持する個人データは「正確で、 必要な場合は最新に保たれなければならない」し、「不正確な個人データを... 遅滞なく消去または修正するためにあらゆる妥当な措置を講じなければならない」ことを要求しています。さらに、第16条「データ主体は、自己に関する不正確な個人データの修正を、不当な遅延なく管理者から取得する権利を有する。」と規定しています。

@row
> \-- Availability, Retention, and Deletion of Identity Information

In the case of identity systems where an identity provider, relying party, or other identity system participant retains data about a data subject, the availability, retention, and deletion of such identity information can be regulated by a variety of Level 1 laws.

_**Privacy law**_ (e.g., GDPR and the California Consumer Privacy Act (CCPA) [^13]) often regulates the availability of personal data (and hence identity data) to the data subject. In particular, such laws often impose on identity providers a duty to provide individual data subjects with access to the data it has collected about them, as well as information regarding the purposes for which it collects and processes such data, and the recipients or categories of recipients to whom the data are disclosed

Numerous laws also impose _**data retention**_ obligations on companies regarding their corporate records. These laws may apply to and require both identity providers and relying parties to retain certain identity data for a particular period of time.

Finally, however, _**privacy**_ laws (such as the GDPR) may impose limits on the retention of personal data. And increasingly, privacy laws (such as GDPR and CCPA) grant data subjects are right to request that data about them be deleted or erased.

@column
> \-- アイデンティティ情報の利用可能性、保持および削除

アイデンティティプロバイダ、リライングパーティまたは他のアイデンティティシステム参加者がデータ主体に関するデータを保持するアイデンティティシステムの場合、アイデンティティ情報の利用可能性、保持および削除は、さまざまなレベル1の法律によって規制される可能性があります。

_**プライバシー法**_ （たとえば GDPRおよびカリフォルニア消費者プライバシー法（CCPA） [^13] ）は、データ主体が個人データ（したがって、アイデンティティデータ）を利用できることを規制することが多いです。特に、そのような法律はしばしばアイデンティティプロバイダに、アイデンティティプロバイダが収集した自分についてのデータへのアクセス、そのようなデータを収集し処理する目的およびデータが開示される受信者または受信者のカテゴリに関する情報を個々のデータ対象者に提供する義務を課しています。

多数の法律が、企業の記録に関して _**データ保持**_ の義務を企業に課しています。これらの法律は、アイデンティティプロバイダとリライングパーティの両方に適用され、特定のアイデンティティデータを特定の期間保持することを要求する場合があります。

しかし最後に、 _**プライバシー**_ 法（GDPRなど）は個人データの保持に制限を課す場合があります。また、プライバシー法（GDPRやCCPAなど）は、データ主体に自分に関するデータの削除または消去を要求する権利を認めるようになってきています。

@row
> \-- Security of Identity Information and Processes

Many _**data security laws**_ and regulations impose obligations on companies with respect to the security of personal data and other information in their possession or under their control. To the extent that a participant in an identity system is collecting, using, storing, or transferring personal data, such data security laws may have a significant impact on its obligations and potential liability. This is particularly true for identity providers and relying parties.

Data security laws are sometimes incorporated into privacy laws, but regardless of form, they generally impose two key obligations: (1) a duty to _provide reasonable security_ for personal data, and (2) a duty to _disclose breaches_ of security of personal data to the persons affected and to regulators. Although not written specifically to address identity system activities, such laws will undoubtedly apply to the personal data used by identity systems as well.

@column
> \-- アイデンティティ情報およびプロセスのセキュリティ

多くの _**データセキュリティに関する法律**_ および規制は、企業が所有または管理する個人データおよびその他の情報のセキュリティに関して、企業に義務を課しています。アイデンティティシステムの参加者が個人データを収集、利用、保管または転送している範囲では、そのような データセキュリティ法は、その義務および潜在的責任に大きな影響を与える可能性があります。これは特にアイデンティティプロバイダおよびリライングパーティについて当てはまります。

データセキュリティ法は、プライバシー法に組み込まれることもありますが、形式に関係なく、 一般に2つの重要な義務、すなわち（1）個人データに妥当なセキュリティを提供する義務、 （2）個人データのセキュリティ侵害を影響を受ける人および規制当局に開示する義務を課します。アイデンティティシステム活動に特化して書かれているわけではないが、そのような法律は間違いなくアイデンティティシステムで使用される個人データにも適用されます。

@row
### Level 2 – Generic Identity System Law

The application of existing general law to identity systems is often not a good fit, frequently ambiguous, and in many cases leads to arguably inappropriate results. This is further complicated by the fact that the Level 1 laws applied to identity systems can vary considerably across jurisdictions. Thus, there have been several attempts to address these concerns.

Some jurisdictions have proposed, and some have enacted, legislation or regulations expressly governing all identity systems within their jurisdiction. However, there is not yet agreement on the desirability or goals of such generic legislation, much less on how to achieve them. Key questions yet to be resolved include whether such legislation should be designed to: (1) simply remove legal barriers (actual and perceived) to identity systems, (2) encourage and assist the development of identity systems, or otherwise help establish the “trust” and the “predictability” needed by parties engaged in online identity transactions, or (3) regulate and control identity systems, such as by protecting the privacy of personal information, ensuring the security and trustworthiness of identity transactions, or imposing or limiting the liability of identity providers.

At present, very little Level 2 law exists. Nevertheless, some noteworthy efforts to develop Level 2 law governing identity systems include the following:

Virginia . The state of Virginia became the first US state to adopt Level 2 identity legislation by enacting the Virginia Electronic Identity Management Act in 2015. That legislation is focused primarily on the issue of liability. To do that, it provides for the creation of a Virginia Identity Management Standards Advisory Council, which was tasked with developing Identity Management Standards. Identity providers and trust framework operators that comply with the requirements of those Identity Management Standards are then granted immunity from civil liability. In other words, the Virginia Act provides a safe harbor from liability for identity providers and trust framework operators.

UN Commission on International Trade Law (UNCITRAL) . In the Spring of 2015, both the American Bar Association Identity Management Legal Task Force, and a group of EU countries (Austria, Belgium, France, Italy, and Poland, with support from the EU Commission), submitted proposals to UN Commission on International Trade Law (UNCITRAL) regarding identity management legislation. Those proposals recommended that UNCITRAL undertake a project to develop “a basic legal framework covering identity management transactions, including appropriate provisions designed to facilitate international cross-border interoperability.” UNCITRAL has since agreed to move forward with such a project. [^14]

UNCITRAL provides an international forum capable of developing a harmonized set of globally accepted law governing identity management. Such law can be adapted domestically by individual countries to promote a universal approach to identity management law and can be extended globally (to facilitate cross-border identity transactions) through an international treaty or convention.

In September 2019, UNCITRAL produced the second version of its Draft Provisions on the Cross-border Recognition of IdM and Trust Services. Issues currently being considered include the:

*   Rights and responsibilities of various identity system roles
    
*   Determination of the reliability of identity systems
    
*   Liability of identity providers
    
*   Legal recognition of identity credentials.
    
*   Cross-border recognition of identity credentials.
    

@column
### レベル2 – 汎用アイデンティティシステム法

既存の一般法のアイデンティティシステムへの適用は、しばしばうまく適合せず、しばしば曖昧で、多くの場合、論外として不適切な結果をもたらします。これは、アイデンティティシステムに適用されるレベル1の法律が法域によってかなり異なる可能性があるという事実によってさらに複雑になっています。したがって、これらの懸念に対処するいくつかの試みがなされてきました。

一部の法域は、その法域のすべてのアイデンティティシステムを明示的に支配する法律または規制を提案し、一部は制定しています。しかし、そのような一般的な法律の望ましさや目標について、ましてやどのようにそれらを達成するのかについては、まだ合意が得られていません。まだ解決されていない主な疑問には、このような法律が次のような目的で制定されるべきであるかどうかなどが挙げられます：（1）アイデンティティシステムに対する（実際および認識された）法的課題を単に取り除く、（2）アイデンティティシステムの開発を奨励および支援する、またはオンラインアイデンティティトランザクションに従事する当事者が必要とする「信頼」および「予測可能性」の確立を支援する、（3）個人情報のプライバシー保護、アイデンティティトランザクションのセキュリティおよび信頼性の確保、アイデンティティプロバイダ責任の付与または制限などによるアイデンティティシステムの規制および管理などです。

現在のところ、レベル2の法律はほとんど存在しません。にもかかわらず、アイデンティティシステムを管理するレベル2の法律を作成する注目すべき取り組みには、次のものがあります：

ヴァージニア州。ヴァージニア州は、2015年にヴァージニア電子アイデンティ管理法を制定することでレベル2アイデンティ法に対応した最初のアメリカの州となりました。この法律は主に責任の問題に焦点を当てています。このために、アイデンティ管理標準の策定を目的としたヴァージニアアイデンティ管理標準諮問委員会を創設しています。これらのアイデンティ管理標準の要件に準拠したアイデンティプロバイダとトラストフレームワーク運用者は、民事責任を免除されます。言い換えれば、ヴァージニア法はアイデンティプロバイダとトラストフレームワーク運用者に避難港を提供します。

国連国際商取引法委員会（UNCITRAL）。2015年春、米国弁護士会アイデンティ管理リーガルタスクフォースおよびEU国家（EU委員会のサポートを受けたオーストリア、ベルギー、フランス、イタリア、ポーランド）のグループは、アイデンティ管理法に関連した提案を連国際商取引法委員会（UNCITRAL）に提出しました。これらの提案には、UNCITRALが「国際的な国境を超えた相互運用性を促進するために設計された適切な規定を含むアイデンティ管理トランザクションを対象とする基本的な法的な枠組み」を策定するプロジェクトに着手することを推奨しています。その後、UNCITRALはそのようなプロジェクトの推進に賛同しています。 [^14]

UNCITRALはアイデンティ管理を規定する国際的に認められた調和のとれた法律を作成できる国際フォーラムを提供します。このような法律は、アイデンティ管理法への普遍的なアプローチを推進するために個々の国々によって国内向けに適用することができ、国際条約または国際協定によって（国家を超えたアイデンティトランザクションを推進するために）グローバルに拡張することができます。

2019年9月、UNCITRALはIdMおよびトラストサービスの国家を超えた承認に関する規定ドラフトの2版を作成しました。現在検討されている課題には以下が含まれます：

*   複数のアイデンティティシステムロールの権利と責任
    
*   複数のアイデンティティシステムロールの権利と責任
    
*   アイデンティティプロバイダの責任
    
*   アイデンティティクレデンシャルの法的承認
    
*   アイデンティティクレデンシャルの国家間承認
    

@row
### Level 3 – Individual Identity System Rules

Both Level 1 and Level 2 law provides general rules applicable to all identity systems. But because each identity system is unique, it also requires its own tailored set of more detailed rules to govern its operations.

In fact, having predictable and enforceable rules designed to ensure that it functions properly and is trustworthy is key to any identity system. Unique system rules (e.g., a trust framework) will ideally provide such a structure to govern the operation of an identity system, much like the Visa or MasterCard rules rules (including the payment card industry data security standard or PCI-DCSS) that govern credit card systems. [^15] Such rules include the technical specifications and operational rules and requirements necessary to make the system functional and trustworthy and the legal rules that define the rights and legal obligations of the parties and facilitate enforcement where necessary.

These individual identity system rules are the Level 3 law that governs an identity system. For private sector identity systems, these rules typically take the form of a so-called trust framework and are made enforceable against the various system participants by contract. Accordingly, those rules must comply with any restrictions at Levels 1 and 2 law.

In the case of public sector identity systems (such as a national ID system), these rules usually take the form of legislation or regulations adopted by the government to govern the system. Many countries, including most notably Estonia and India, have adopted laws to govern their specific national ID systems. In some cases, a country may establish an identity system based on a set of rules that participants voluntarily agreed to by contract. The Australian Trusted Digital Identity Framework (TDIF), and the UK GOV. UK Verify program takes this approach.

Regardless of whether an identity system is public or private, the issues addressed by the Level 3 system rules/trust framework often include the following:

*   technical specifications that will govern the system
    
*   rights and obligations of participants in each system role
    
*   data subject registration and enrollment processes
    
*   identity verification process requirements
    
*   credential issuance requirements
    
*   authentication process requirements
    
*   rules governing reliance by relying parties
    
*   data security requirements (over and above requirements of applicable law)
    
*   privacy requirements (over and above requirements of applicable law)
    
*   audits, assessments, and certification requirements
    
*   allocation of liability risk among roles
    
*   termination rights and obligations
    
*   dispute resolution
    
*   enforcement of rights and obligations
    

Where such rules are embodied in laws or regulations issued by a government, they are of course binding on all system participants by force of law. But in the case of a trust framework (typically used in a private-sector system), the system rules are binding on the participants only to the extent they agree by contract to be bound to comply with the rules. In all cases, however, the Level 3 law is comprised of system rules written for a specific identity system, and thus its applicability is limited to that system.

@column
### レベル3 – 個別のアイデンティティ規則

レベル1とレベル2の両方の法律は、すべてのアイデンティティシステムに適用される一般的なルールを提供します。しかし、それぞれのアイデンティティシステムは固有であるため、その運用を管理するために、独自に調整されたより詳細なルールも必要です。

実際、適切に機能し、信頼できるものであることを保証するように設計された、予測可能で実施可能なルールを持つことは、アイデンティティシステムにとって重要です。独自のシステム ルール（トラストフレームなど）は、理想的には、クレジットカードシステムを管理するVisaまたはMasterCardのルール（Payment Card Industry Data Security StandardまたはPCI-DCSSを含む）と同様に、アイデンティティシステムの運用を管理する構成を提供します。 [^15] このような規則には、システムを機能的かつ信頼できるものにするために必要な技術仕様と運用規則と要件および当事者の権利と法的義務を定義し、必要に応じて執行を容易にする法的規則が含まれます。

これらの個別のアイデンティティシステムの規則は、アイデンティティシステムを管理するレベル3の法律です。民間企業のアイデンティティシステムの場合、これらのルールは通常、いわゆるトラストフレームワークの形をとり、契約によってさまざまなシステム参加者に対して施行可能になります。したがって、これらの規則は、レベル1およびレベル2の法律の制限に準拠する必要があります。

公的機関のアイデンティティシステム（国民アイデンティティシステムなど）の場合、これらの規則は通常、システムを管理するために政府によって採用された法律または規制の形をとります。特にエストニアとインドを含む多くの国では、特定の国民アイデンティティシステムを管理する法律を採用しています。場合によっては、参加者が契約によって自発的に同意した一連のルールに基づいて、アイデンティティシステムを国が確立することがあります。オーストラリアのTrusted Digital Identity Framework（TDIF）および英国のUK Verifyプログラムはこのアプローチを採用しています。

Regardless of whether an identity system is public or private, the issues addressed by the Level 3 system rules/trust framework often include the following:
アイデンティティシステムが公的または民間であるかにかかわらず、レベル3システムの規制／トラストフレームが対処する問題にはしばしば、以下のことを含みます

*   システムを統制する技術仕様
    
*   各システムロールにおける参加者の管理と義務
    
*   データ主体の申込みと登録のプロセス
    
*   身元確認プロセス要件
    
*   クレデンシャル発行要件
    
*   認証プロセス要件
    
*   リライングパーティの信頼を統制する規則
    
*   データセキュリティ要件（適用法の要件以上および要件外）
    
*   プライバシー要件（適用法の要件以上および要件外）
    
*   監査、保証および認定の要件
    
*   責任リスクの役割分担
    
*   解約の権利と義務
    
*   紛争解決
    
*   権利および義務の履行
    

Where such rules are embodied in laws or regulations issued by a government, they are of course binding on all system participants by force of law. But in the case of a trust framework (typically used in a private-sector system), the system rules are binding on the participants only to the extent they agree by contract to be bound to comply with the rules. In all cases, however, the Level 3 law is comprised of system rules written for a specific identity system, and thus its applicability is limited to that system.
このようなルールが政府によって発せられた法律や規則で具体化されている場合、当然ながら法律の力によってすべてのシステム参加者を拘束することになります。しかし、トラストフレームワーク（通常、民間のシステムで利用されます）の場合、システム規則は、参加者が規則に従うことに契約によって同意する程度まででしか、参加者を拘束しません。ただし、すべての場合において、レベル3の法律は特定のアイデンティティシステムのために書かれたシステム規則で構成されるため、その適用性はそのシステムに限定されます。

@row
## Author Bio

Thomas J. Smedinghoff is Of Counsel at Locke Lord, LLP, and Chair of the American Bar Association Identity Management Legal Task Force. He can be reached at [Tom.Smedinghoff@lockelord.com](mailto:Tom.Smedinghoff@lockelord.com)

@row
## Change Log

| Date | Change |
| --- | --- |
| 2021-06-30 | Editorial updates |

[^1]: Code of Virginia - Chapter 50. Electronic Identity Management Act. 2015. [https://law.lis.virginia.gov/vacode/title59.1/chapter50/](https://law.lis.virginia.gov/vacode/title59.1/chapter50/) .

[^2]: “Draft Provisions on the Cross-border Recognition of IdM and Trust Services,” revision A/CN.9/WG.IV/WP.160, United Nations Commission on International Trade Law, last revised 16 September 2019, [https://uncitral.un.org/sites/uncitral.un.org/files/media-documents/uncitral/en/wp-160-e.pdf](https://uncitral.un.org/sites/uncitral.un.org/files/media-documents/uncitral/en/wp-160-e.pdf) .

[^3]: “Greater Security via the SAFE Identity Trust Framework,” accessed 18 May 2021, SAFE Identity, [https://makeidentitysafe.com/trust-framework/](https://makeidentitysafe.com/trust-framework/) .

[^4]: “Sovrin Governance Framework,” accessed 18 May 2021, Sovrin, [https://sovrin.org/library/sovrin-governance-framework/](https://sovrin.org/library/sovrin-governance-framework/) .

[^5]: “SecureKey Concierge Trust Framework,” accessed October 10, 2019, SecureKey, [https://securekey.com/resources/trust-framework-securekey-concierge-in-canada/](https://securekey.com/resources/trust-framework-securekey-concierge-in-canada/) .

[^6]: eIDAS Regulation\[EU\]: [https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=uriserv:OJ.L\_.2014.257.01.0073.01.ENG](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=uriserv:OJ.L_.2014.257.01.0073.01.ENG)

[^7]: Identity Documents Act \[Estonia\]: [http://www.unhcr.org/refworld/docid/4728ab1b2.html](http://www.unhcr.org/refworld/docid/4728ab1b2.html)

[^8]: Aadhaar Act [https://uidai.gov.in/images/targeted\_delivery\_of\_financial\_and\_other\_subsidies\_benefits\_and\_services\_13072016.pdf](https://uidai.gov.in/images/targeted_delivery_of_financial_and_other_subsidies_benefits_and_services_13072016.pdf) .

[^9]: “Trusted Digital Identity Framework,” accessed 18 May 2021, Australian Government Digital Transformation Agency, [https://www.dta.gov.au/our-projects/digital-identity/trusted-digital-identity-framework](https://www.dta.gov.au/our-projects/digital-identity/trusted-digital-identity-framework) .

[^10]: “Mastercard Rules,” accessed 18 May 2021, Mastercard, [https://www.mastercard.us/en-us/about-mastercard/what-we-do/rules.html](https://www.mastercard.us/en-us/about-mastercard/what-we-do/rules.html) .

[^11]: “Visa Core Rules and Visa Product and Service Rules,” 15 October 2013, accessed 18 May 2021, Visa, [https://usa.visa.com/dam/VCOM/download/merchants/visa-international-operating-regulations-main.pdf](https://usa.visa.com/dam/VCOM/download/merchants/visa-international-operating-regulations-main.pdf) .

[^12]: “§ 1026.1 Authority, purpose, coverage, organization, enforcement, and liability,” 12 CFR Prt 1026 (Regulation Z), Consumer Financial Protection Bureau, accessed 18 May 2021 [https://www.consumerfinance.gov/rules-policy/regulations/1026/](https://www.consumerfinance.gov/rules-policy/regulations/1026/) .

[^13]: “California Consumer Privacy Act of 2018,” Title 1.81.5, Section 1798.100, Part 4 of Division 3, State of California, accessed 18 May 2021, [https://leginfo.legislature.ca.gov/faces/codes](https://leginfo.legislature.ca.gov/faces/codes) \_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5.

[^14]: UNCITRAL, “Colloquium on Identity Management and Trust Services,” 21-22 April 2016, accessed 18 May 2021, [https://uncitral.un.org/en/colloquia/electronic\_commerce/2016](https://uncitral.un.org/en/colloquia/electronic_commerce/2016) .

[^15]: PCI Security Standards Council, Standards Overview, website, [https://www.pcisecuritystandards.org/standards/](https://www.pcisecuritystandards.org/standards/).
