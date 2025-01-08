---
layout: columns
title: The Business Case for IAM
permalink: /docs/oidc_oauth/idpro_bok/97
date: 2024-09-09
modify_date: 2024-12-30
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "プロジェクト管理"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/97/](https://bok.idpro.org/article/id/97/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

Businesses are under enormous pressure to deliver their products and services in ways that profit the company. Areas that do not directly bring in funding are often moved lower in priority, resulting in a competition for resources that can see internal projects in areas such as IAM struggle to succeed. Projects that move to the top of the priority pile in this competition are ones that provide a compelling business case. This article focuses on how to develop a positive business case for your IAM programs.

Keywords: Business case, Investments, ROI, IAM, Program management, Project management

@column
## 概要

企業は、会社に利益をもたらす方法で製品やサービスを提供しなければならないという大きなプレッシャーにさらされています。直接資金をもたらさない分野は、優先順位が下がることが多く、その結果リソースの奪い合いになり、IAMのような分野の社内プロジェクトの成功にはもがくことになります。このような競争の中で優先順位の高いプロジェクトは、説得力のあるビジネスケースを提供するものです。この記事では、IAMプログラムの実用的なビジネスケースをどのように作成するかに焦点をあてています。

Keywords: ビジネスケース, 投資, ROI, IAM, プログラム管理, プロジェクト管理

@row
By André Koot

© 2023 IDPro, André Koot

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

**Please note: this article has large, complex tables viewable only in the [PDF](https://bok.idpro.org/article/97/galley/222/view).**

@row
## Introduction

Identity and Access Management (IAM) is often seen as one of many expenses that must be controlled within an organization. Businesses need to see the benefits of an IAM program before they are willing to invest in IAM programs. This circular demand can leave IAM improvements stuck in a never-ending game of catch-up. Businesses fail to see the strategic value in a solid IAM program until they see tactical improvements directly attributed to IAM services.

A solid business case helps break this deadlock by providing different perspectives on the overall Return On Investment (ROI) that IAM can bring to an organization. The best business cases include:

*   the concept of the quantitative versus the qualitative components of the business case for IAM;
    
*   the perspective from different IAM domains (e.g., internally facing IAM requirements from the enterprise, externally facing IAM requirements from the customers, cybersecurity requirements); and
    
*   the recognition of the different strategic and operational requirements for both IT and the business.
    

Of course, different companies will respond better to different types of business cases. Some will be driven purely by the finances, while others will respond better by putting IAM in context with other services in an organization. Some may instead be primarily driven by the regulatory requirements governing their specific business operations (e.g., finance industry regulations).

@column
## 導入

アイデンティティとアクセス管理（IAM）は、しばしば組織内で管理しなければならない多くの費用の1つと見らえています。企業は、IAMプログラムに投資する前に、IAMプログラムのメリットを確認する必要があります。このような循環的な要求によって、IAMの改善は終わりのないキャッチアップゲームから抜け出せなくなる可能性があります。企業は、IAMサービスに直接起因する戦術的な改善を確認できるまで、堅実なIAMプログラムの戦略的価値を見出すことができません。

堅実なビジネスケースは、IAMが組織にもたらす全体的な投資利益率（ROI）に関する様々な視点を提供することで、このデッドロックを打破します。最良のビジネスケースには以下が含まれます：

*   IAMのビジネスケースの定量的要素と定性的要素の概念；
    
*   異なるIAM領域（例えば、企業から見た内部的なIAM要件、消費者から見た外部的なIAM要件、サイバーセキュリティ要件）からの観点；
    
*   ITとビジネスの両方にとっての異なる戦略および運用の要件の認識
    

もちろん、企業によって対応できるビジネスケースは異なります。純粋に財務的な要因で動く企業もあれば、IAMを組織内の他のサービスと関連付けることでうまく対応できる企業もあります。または、特定の事業運用を管理する規制要件（例えば、金融業界の規制）が主な原動力になる企業もあるでしょう。

@row
### Terminology

| Term | Definition |
| --- | --- |
| Attribute-Based Access Control (ABAC) | Attribute-Based Access Control is a pattern of access control involving dynamic definitions of permissions based on information (“attributes” or “claims”), such as job code, department, or group membership. |
| Business to Business (B2B) | Business to Business processes in the field of IAM involve business partner access to company resources using some form of remote access (e.g., federated access). |
| Business to Consumer (B2C) | Business to Consumer processes in the field of IAM are customer or consumer access to company resources. In B2C, consumers manage their own identity in a CIAM. The company still manages access to the resources, using ABAC or PBAC methods for access control |
| Business to Employee (B2E) | Business to Employee, also called workforce IAM, includes managing identities and accounts for employees and contractors following an identity lifecycle. |
| Consumer Identity and Access Management (CIAM) | Consumer Identity and Access Management, or Customer Identity and Access Management, involves providing access to company resources through a digital identity managed by the customer. |
| Identity Governance and Administration (IGA) | Identity Governance and Administration is a discipline focusing on identity life cycle management and access control from an administrative perspective. |
| Joiner, Mover, and Leaver (JML) | The joiner/mover/leaver lifecycle of an employee identity considers three stages in the life cycle: joining the organization, moving within the organization, and leaving the organization. |
| Policy-Based Access Control (PBAC) | Policy-Based Access Control is a pattern of access control involving dynamic definitions of access permissions based on attributes (as in ABAC) and context for authorized access. |
| Privileged Access Management (PAM) | Privileged Access Management is a mechanism for managing temporary access for accounts with high-risk permissions. PAM often involves check-out and check-in of a credential generated for a single use. |
| Role-Based Access Control (RBAC) | Role-Based Access Control involves using roles at run-time to govern control access. It is a pattern of access control involving sets of static, manual definitions of permissions assigned to “roles,” which can be consistently and repeatedly associated with users with common access needs. |
| Return on Investment (ROI) | Return on Investment is the economic measure of value of an investment, using costs, revenues, interest rates, and lifecycle as parameters. |
| Sunk cost | Expenses that have already been made in the past and that are unrecoverable. |

@column
### 用語解説

| Term | Definition |
| --- | --- |
| Attribute-Based Access Control (ABAC) | Attribute-Based Access Control is a pattern of access control involving dynamic definitions of permissions based on information (“attributes” or “claims”), such as job code, department, or group membership. |
| Business to Business (B2B) | Business to Business processes in the field of IAM involve business partner access to company resources using some form of remote access (e.g., federated access). |
| Business to Consumer (B2C) | Business to Consumer processes in the field of IAM are customer or consumer access to company resources. In B2C, consumers manage their own identity in a CIAM. The company still manages access to the resources, using ABAC or PBAC methods for access control |
| Business to Employee (B2E) | Business to Employee, also called workforce IAM, includes managing identities and accounts for employees and contractors following an identity lifecycle. |
| Consumer Identity and Access Management (CIAM) | Consumer Identity and Access Management, or Customer Identity and Access Management, involves providing access to company resources through a digital identity managed by the customer. |
| Identity Governance and Administration (IGA) | Identity Governance and Administration is a discipline focusing on identity life cycle management and access control from an administrative perspective. |
| Joiner, Mover, and Leaver (JML) | The joiner/mover/leaver lifecycle of an employee identity considers three stages in the life cycle: joining the organization, moving within the organization, and leaving the organization. |
| Policy-Based Access Control (PBAC) | Policy-Based Access Control is a pattern of access control involving dynamic definitions of access permissions based on attributes (as in ABAC) and context for authorized access. |
| Privileged Access Management (PAM) | Privileged Access Management is a mechanism for managing temporary access for accounts with high-risk permissions. PAM often involves check-out and check-in of a credential generated for a single use. |
| Role-Based Access Control (RBAC) | Role-Based Access Control involves using roles at run-time to govern control access. It is a pattern of access control involving sets of static, manual definitions of permissions assigned to “roles,” which can be consistently and repeatedly associated with users with common access needs. |
| Return on Investment (ROI) | Return on Investment is the economic measure of value of an investment, using costs, revenues, interest rates, and lifecycle as parameters. |
| Sunk cost | Expenses that have already been made in the past and that are unrecoverable. |

@row
### Acronyms

C-level Chief Executive Level, including Chief Executive Officer, Chief Financial Officer, Chief Information Officer, etc.

BC/DR Business Continuity/Disaster Recovery

CI/CD Continuous Integration/Continuous Deployment

GDPR General Data Protection Regulation

HIPAA Health Insurance Portability and Accountability Act

HR Human Resources

IAM Identity and Access Management

IT Information Technology

ROI Return on Investment

SSO Single Sign-On

Y2K Year 2000

ZTA Zero Trust Authorization

@column
### 略語解説

Cレベル 最高経営責任者、最高財務責任者、最高情報責任者などを含む最高経営責任者レベル

BC/DR 事業継続/災害復旧

CI/CD 継続的インテグレーション/継続的デプロイメント

GDPR 一般データ保護規則

HIPAA 医療保険の携行性と責任に関する法律

HR 人事

IAM アイデンティティとアクセス管理

IT 情報テクノロジー

ROI 投資利益率

SSO シングルサインオン

Y2K 2000念

ZTA ゼロトラスト認可

@row
## Starting an IAM program

When working in IAM, the question often arises as to whether the costs and investments of an IAM program are worthwhile. Organizations generally ask for a financial business case since that is a traditional way to argue for an investment decision. It takes significant effort to convince decision-makers to look beyond the financial viewpoint.

Most IAM programs are started to solve one of three enterprise problems:

*   Operations management (HR, IT)
    
    *   for increasing employee efficiency, enhancing data quality, and cost-effectiveness [^1]
        
*   Enterprise, IT, or security architecture
    
    *   for aligning with current best practices such as new controls for API access, support for Zero Trust, and supporting multi-factor authentication along with resolving issues of technology debt
        
    *   for realizing newly defined strategic business initiatives, such as implementing a Consumer IAM (CIAM) strategy for revenue generation, improving customer services, and easing digital transformation [^2]
        
*   Chief Executive Level (C-level)
    
    *   for responding to audit findings in a management letter or directives from a supervisory agency or as the result of a security incident or data breach [^3]
        

Regardless of where the IAM program starts, a lot of money will be required from multiple cost centers before the program is complete. It often takes several budget cycles and significant organizational commitment to realize an effective IAM initiative. The program's sponsors must be prepared to make a business case to justify the organizational effort and the financial costs. Even if the C-level initiates the IAM efforts, a business case must often remind all stakeholders why this initiative is critical to the organization.

So, what elements of IAM investments can be identified that make an investment worthwhile?

This article looks at the business case for IAM from different perspectives.

*   The first viewpoint is based on the difference between a business case's quantitative and qualitative components.
    
    *   Quantitative means an objective calculation of the financial costs and benefits of an investment
        
    *   Qualitative means that the costs and benefits of an investment cannot be calculated objectively, but the components have value for the business or bring additional trouble.
        
*   A second viewpoint looks at IAM from different domains: B2E (i.e., Workforce IAM, Identity Governance and Administration (IGA)), B2C and B2B (i.e., CIAM), and Privileged Access Management (PAM).
    
*   The third viewpoint is the organizational viewpoint: strategic, tactical, and operational reasons for implementing IAM.
    

There is no easy, complete formula for calculating the ROI of an investment in IAM. But at least these views can help to convince the stakeholders to look beyond the purely financial impact of IAM.

@column
## IAMプログラムを開始する

IAMの仕事に携わっていると、IAMプログラムのコストや投資が割に合うかどうかという疑問がしばしば生じます。一般的に、それが投資決定を主張する伝統的な方法であるため、組織は財務的なビジネスケースを要求します。意思決定者に、財務的な視点を超えて見てもらうためには、多大な努力が必要です。

ほとんどのIAMプログラムは、3つの企業の問題のいずれかを解決するために開始されます：

*   運用管理（HR, IT）
    
    *   従業員の効率を高め、データの質とコスト効率を向上させる [^1]
        
*   企業、ITまたはセキュリティアーキテクチャ
    
    *   APIアクセスの新たな制御、ゼロトラストへの対応および多要素認証のサポートなど現代のベストプラクティスに沿うことで技術的負債を解決する
        
    *   収益創出、カスタマーサービスの向上およびデジタル・トランスフォーメーションの促進のためのコンシューマーIAM（CIAM）戦略の導入のような新しい戦略的なビジネスへの取り組みの実現 [^2]
        
*   最高経営責任者レベル（Cレベル）
    
    *   マネジメントレターでの監査指摘事項や、監査機関やセキュリティインシデントやデータ漏洩の結果による指示への対応 [^3]
        

IAMプログラムがどこから始まるかにかかわらず、プログラムが完了するまでには、複数のコストセンターから多額の資金が要求されます。効果的なIAMへの取り組みを実現するためには、数回の予算サイクルと組織の多大なコミットメントが必要になることが多いです。プログラムのスポンサーは、組織の努力と財務的コストを正当化するためのビジネスケースを準備しなければなりません。たとえCレベルがIAMの取り組みを始めたとしても、多くの場合、ビジネスケースは、なぜこの取り組みが組織にとって重要なのかをすべての利害関係者に思い出させなければなりません。

では、IAM投資のどのような要素を特定すれば、投資に値するのだろうか？

この記事では複数の異なる観点からのIAMのビジネスケースについてみていきます。


*   最初の観点は、ビジネスケースの定量的要素と定性的要素の違いに基づいています。
    
    *   定量的とは、投資の財務的なコストと利益の客観的な算定を意味します
        
    *   定性的とは、投資のコストと利益は客観的に算定できませんが、その要素がビジネスにとって価値があるかほかの問題を引き起こすことを意味します
        
*   第二の観点は、異なる領域からIAMを見ることです：B2E（例えば、従業員IAMやアイデンティティのガバナンスと管理（IGA））、B2CとB2B（つまり、CIAM）、そして特権アクセス管理（PAM）。
    
*   第三の観点は組織的な観点です：戦略的、戦術的および運用的な理由でのIAM導入。
    

IAMの投資のROIを算定する簡便で完璧な公式はありません。しかし、少なくといくつかの観点は、単純なIAMの財務的な影響以外を見ることをステークホルダーに納得させる助けになるでしょう。

@row
## The Added Value of IAM

@column
## IAMの付加価値

@row
### Preventing Negative Impacts

IAM strengthens businesses in many ways, from supporting business continuity to protecting business resources and reputation. For example, there are many reasons to consider IAM as a method for Business Continuity and Disaster Recovery (BC/DR). As organizations grow, access to resources becomes a liability: access to resources becomes more challenging overall, and delegating tasks and responsibilities becomes a bigger problem. If an organization is not in control of its data, including information on who may access that data, its ability to function in the case of significant business interruption is at risk. Even in a disaster, maintaining a record of who has in the past and can in the future access systems and data is critical.

Possibly the most famous example of a disaster directly related to a poorly managed and enforced IAM program is that of the Enron scandal in the late 1990s. [^4] In IAM terms, the scandal was partly a result of executives circumventing management controls, possibly because of the lack of fitting access controls. The best practice of Segregation of Duties was circumvented by greed, organizational culture, and practices.

At the same time, investments in IAM suffer from the prevention paradox. Investing in IAM rarely brings immediate, visible improvements. Finding the benefits (in terms of concrete cost savings) may be hard to achieve. Would the effects be the same with fewer costs and efforts of the IAM investment? It may seem like the Y2K crisis all over again. [^5]

@column
### 悪性業を防ぐ

IAMは、事業継続の支援からビジネス・リソースや評判の保護まで、さまざまな方法でビジネスを強化します。例えば、事業継続と災害復旧（BC/DR）の手法としてIAMを検討する理由は多くあります。組織が成長するにつれ、リソースへのアクセスは義務となります：リソースへのアクセスは全体的に難しくなり、タスクや責任の委譲はより大きな問題となります。組織は、誰がそのデータにアクセスできるかという情報を含め、データを管理できなければ、事業が大幅に中断した場合に機能する能力が危険にさらされます。災害時であっても、誰が過去にシステムやデータにアクセスしたか、また将来アクセスできるかを記録しておくことは非常に重要です。

不十分な管理および実行がされていたIAMプログラムに直接関係する災害の例として最も有名なのは、1990年代後半のエンロン事件でしょう。 [^4] IAMの用語で言えば、この事件は経営幹部が管理統制を迂回した結果の一部であり、おそらく適切なアクセス制御が欠如していたためでした。職務分掌というベストプラクティスが、強欲、組織文化および慣行によって回避されました。

同時に、IAMへの投資は予防のパラドックスに苦しんでいます。IAMへの投資がすぐに目に見える改善をもたらすことはほとんどありません。（具体的なコスト削減という）効果を見出すのは難しいかもしれません。IAMへの投資のコストや努力が少なくても、効果は同じでしょうか？Y2K問題の再来のように思えるかもしれません。 [^5]

@row
### Supporting Positive Impacts

Of course, not every organization suffers from the same malicious drivers as Enron did. Still, that case highlights the need for access control from the perspectives of business continuity, governance, and compliance. To be in control, the need for managing identities and especially the management of authorizations is demonstrated by this case and many others.

But there are more reasons for investing in IAM. In many organizations, the need for IAM comes from the need for efficiency and high data quality. Manually creating identities for personnel and adding and revoking authorizations is inefficient, while the manual execution of these tasks can result in a lack of data quality. Automating the process can provide higher quality with less expensive results.

Organizations will also find benefits in improving their user experience. Developing single sign-on (SSO) services and self-service access requests improves not just the efficiency of the process but also the user’s satisfaction. The continuing development of external access and the move toward API access led to the need for IAM-related programs.

These lines of reasoning, while valid, may be too far away from daily operations and immediate, visible improvements in efficiency. Businesses and boards experience the need for short-term insight as well as long-term improvements before they make further investments. In other words, companies need a specific and complete business case for IAM.

@column
### 良影響を支援する

もちろん、すべての組織がエンロンのような悪意のある操縦者に悩まされているわけではありません。それでも、このケースは事業継続、ガバナンスおよびコンプライアンスの観点からアクセス制御の必要性をハイライトしています。コントロールするためには、アイデンティティの管理、特に認可管理が必要であることは、このケースやその他多くのケースで実証されています。

しかし、IAMに投資する理由は他にもあります。多くの組織では、IAMの必要性は効率性と高いデータ品質の必要性に由来しています。手作業で担当者のアイデンティティを作成し、認可を追加したり失効させたりすることは非効率的であり、これらのタスクを手作業で実行することはデータ品質の低下となる可能性があります。プロセスを自動化することで、より低コストでより高い品質を提供することができます。

組織は、ユーザーエクスペリエンスの向上にもメリットを見出すでしょう。シングルサインオン（SSO）サービスやセルフサービス・アクセス・リクエストの開発は、プロセスの効率だけでなく、ユーザーの満足度も向上させます。外部アクセスの継続的な発展とAPIアクセスへの移行は、IAM関連プログラムの必要性につながりました。

これらの理屈は妥当ではあるが、日常業務やすぐに目に見える効率改善からは遠すぎるかもしれません。企業や取締役会は、さらなる投資をおこなう前に、短期的な洞察と長期的な改善の必要性を経験しています。言い換えれば、企業はIAMに対する具体的かつ完全なビジネスケースを必要とします。

@row
## Different Dimensions of IAM Business Case

@column
## IAMビジネスケースの異なる面

@row
### Quantitative versus Qualitative Business Case

A simple formula for calculating the ROI looks thus:

  
$$ ROI = \frac{NetReturnonInvestment}{CostofInvestment} \ast 100{\%}  $$  

(see [_Guide to calculating ROI_](https://www.investopedia.com/articles/basics/10/guide-to-calculating-roi.asp) )

The simple formula can be used to calculate if an investment is anything good, financially speaking. Suppose you want to invest 1 million and later sell the investment for 1.1 million, resulting in a profit of 100,000; the ROI would then be

(1,100000 – 1,000,000) / 1,000,000 \* 100% = 10%

Of course, the calculation would be a little more complex for projects. It is unlikely that you would invest 1 million in IAM and later sell the investment, making a profit. This simple formula also hides the fact that indirect returns are both critical for the overall measure of ROI and extremely hard to quantify.

First, let’s look at the distinction between the quantitative business case and the qualitative business case.

*   The _Quantitative Business_ _Case_ is all about money. It is about calculating the costs and benefits objectively, at least as much as possible. This enumeration is relevant for managers to calculate all investments in an organization to prioritize investments. To a lesser degree, the business case can be input for a cash flow analysis. In this article, we classify topics as objectively quantifiable, but just like in risk management, some entries cannot be calculated objectively. For example, the risk of penalties does not result in an absolute value. It is an approximation of the cost of the risk. The cost of the risk could be calculated as the chance of discovery of the non-compliance times the potential maximal amount of a fine. That means that, just like any approximation, it has to be taken with a grain of salt.
    
*   For most governance, risk, and compliance managers, the _Qualitative Business Case_ will be the preferred justification for investments in IAM solutions. The entries in the overview below may not be objectively quantifiable, but that does not mean that they should not be considered when prioritizing investments.
    
*   An interesting example of a financial business case is the situation of banks and insurance companies who have to undergo a stress test to find if they can survive a financial crisis. The capital requirements are higher or lower depending on the risk level. High capital requirements impact the money-making capabilities; a high reserve is a lot of unused capital. These rules and regulations have been defined in the EU Basel IV and Solvency 2 regulations, which have also been adopted by the Federal Reserve in the US. [^6]
    

> If a bank has sufficient assurance about authorizations because of adequate access control, then data quality will be better, and risk (uncertainty about access) and capital requirements will be lower, resulting in a significant impact on revenue creation capabilities.

@column
### 定量的ビジネスケースと定性的ビジネスケース

ROIを算出する単純な計算式は以下の通りです：

  
$$ ROI = \frac{NetReturnonInvestment}{CostofInvestment} \ast 100{\%}  $$  

（[_Guide to calculating ROI_](https://www.investopedia.com/articles/basics/10/guide-to-calculating-roi.asp)参照）

この単純な計算式は、ある投資が財務的に良いものかどうかを計算するのに利用できます。100万ドルを投資し、後に110万ドルで売却して10万ドルの利益を得たとします；ROIは以下のようになります

(1,100000 – 1,000,000) / 1,000,000 \* 100% = 10%

もちろん、プロジェクトの場合はもう少し複雑な計算になります。IAMに100万ドルを投資し、後でその投資を売却して利益を上げるということはまずありません。また、この単純な計算式は、間接的なリターンがROIの全体的な尺度にとって重要であることと、定量化するのが極めて難しいという事実を隠しています。

まず、定量的ビジネスケースと定性的ビジネスケースの区別を見てみましょう。

*   _定量的ビジネスケース_ とは、すべてお金に関するものです。少なくとも可能な限り、コストと利益を客観的に計算することです。この目録はマネジャーが投資の優先順位をつけるために組織内のすべての投資を計算することに関連します。また、少ないながらもビジネスケースはキャッシュフロー分析のインプットにもなります。本稿では、トピックを客観的に定量化可能なものとして分類していますが、リスクマネジメントと同様に、客観的に計算できない項目もあります。例えば、罰則金のリスクは絶対値にはなりません。リスクのコストの近似値です。リスクのコストは、コンプライアンス違反が発覚する可能性に潜在的な罰則金の最大額をかけることで算出できます。つまり、どのような近似値であっても、それは大目に見る必要があります。
    
*   ほとんどのガバナンス、リスクおよびコンプライアンスマネージャーにとって、 _定性的ビジネスケース_ はIAMソリューションへの投資を正当化するために好まれます。以下の概略のエントリーは客観的で定量的ではないかもしれませんが、投資の優先順位を決定するさいに考慮すべきでないということではありません。
    
*   金融ビジネスケースの興味深い例として、銀行や保険会社が金融危機を乗り切れるかどうかを調べる負荷試験を受けなければならない状況があります。必要資本はリスクレベルに応じて高くなったり低くなったりします。自己資本規制が高ければ高いほど、金儲けの能力に影響を与えます；高い準備金とは、未使用の資本が多いことです。これらのルールや規制は、EUのバーゼルIV規制やソルベンシー2規制で定義されており、米国の連邦準備制度理事会（FRB）でも採用されています。 [^6]
    

> 適切なアクセス制御により、銀行が認可について充分な保証を得ることができれば、データの質は向上し、リスク（アクセスに関する不確実性）や必要資本は低下し、結果として収益創出能力に大きな影響を与えることになります。

@row
### The Business Case for Different IAM domains: IGA, PAM, and CIAM

Another view is that the business case for different types of IAM-related programs may have different focal points because they focus on different things. For example:

*   Identity Governance & Administration (IGA), which focuses on the internal account and authorization management for employees and contractors with enterprise access, has a root cause in automation, efficiency of performing JML processes, and assigning and revoking roles. While IGA investment decisions will benefit from a quantitative approach to the business case, a purely quantitative approach will not be enough to make the case. Costs and benefits will probably lie in different cost centers that measure success in different ways (e.g., in improved efficiency, in lower risk to security, in regulatory compliance). So, unless the business case is calculated companywide, the business case will be negative.
    
*   Privileged Access Management (PAM) is all about managing risks of critical authorizations and remote access for internal accounts with broad access to sensitive resources. Its focus lies in governance and compliance. In this case, the business case is more likely to start off with a qualitative focus and miss out on some of the critical quantitative aspects that will strengthen the argument. The business case will be qualitative at first sight, but a secondary point of view may be limiting the risk of penalties and fines from laws and regulations.
    
*   CIAM (used for B2C and B2B connections and also applicable for IoT and OT access) focuses on self-service identity management of consumers or customers. That moves convenience and consumer appreciation into a competitive advantage. The quantitative approach may not be sufficient; business continuity may be at risk for lack of investment.
    

This means that the business drivers for these domains are different and that the business case will contain other components.

@column
### 異なるIAM領域にとってのビジネスケース：IGA、PAMおよびCIAM

他の観点は、異なる種別のIAM関連プログラムのビジネスケースは、それらが商店を合わせていることが異なるため、異なる注目点をもっているというものです。例えば：

*   アイデンティティのガバナンスと管理は、企業アクセスをおこなう従業員と請負業者の企業内のアカウントおよび認可管理に注目しており、自動化、JMLプロセス実行の効率化およびロールの割り当てと取り消しの根源です。IGA投資の決定は定量的なアプローチからビジネスケースに利益をもたらしますが、純粋な定量的アプローチはケースの作成に充分ではないでしょう。コストと利益は、成功を異なる方法（例えば、効率の改善、セキュリティに関するリスクの低下、規制遵守）で測定する異なるコストセンターに存在しているでしょう。
    
*   特権アクセス管理（PAM）は、機密リソースに広くアクセスできる内部アカウントの重要な認可とリモートアクセスのリスクを管理するためのものです。その焦点はガバナンスとコンプライアンスにあります。この場合、ビジネスケースは定性的な焦点から出発し、議論を強化する重要な定量的側面のいくつかを見逃してしまう可能性が高いです。ビジネスケースは一見すると定性的なものですが、二次的な観点として、法律や規制による罰則や罰則金のリスクを抑えることが考えられます。
    
*   CIAM（B2CおよびB2BコネクションまたはIoTとOTアクセスにも利用される）は消費者もしくは顧客のセルフサービス・アイデンティティ管理に注目しています。これは利便性と消費者の評価を競争優位な状況にします。定量的なアプローチでは充分ではないでしょう；投資不足は事業継続をリスクにさらすでしょう。
    

つまり、これらのドメインのビジネスドライバーは異なり、ビジネスケースが他のコンポーネントを含むことがあります。

@row
### Strategic, Tactical, and Operational Viewpoints

The third way of looking at the concept of the business case is the organization's viewpoint. In traditional organizational theory models (e.g., the Anthony triangle [^7] ), we can identify the strategic, tactical, and operational layers. And if we follow up on these separate layers, there are also strategic, tactical, and operational considerations for implementing IAM:

@column
### 戦略的、戦術的、運用的な観点

ビジネスケースの概念での3つ目の観点は組織の観点です。伝統的な組織の理論モデル（例、アンソニーの三角形 [^7] ）において、私たちは戦略的、戦術的、運用的なレイヤーを特定することができます。そして、これら別々のレイヤーをフォローアップしていくと、IAM導入における戦略的、戦術的、運用的な懸念点があります：

@row
#### Strategic

This topic is all about implementing business governance of Access, putting the business in control of IAM, and taking IAM out of the realm of IT. The underlying principles are:

*   Governance Risk and Compliance: to be able to show that the organization is in control, to be compliant with laws and regulations, and to prevent ‘Enron’ issues.
    
*   Competitor initiatives, competitive advantage: either to follow industry best practices (for example, a competitor implemented IGA) or to lead the market (for example, by implementing a leading CIAM platform).
    

These issues can also be seen as qualitative components in the business case.

@column
#### 戦略的

このトピックは、アクセスに関するビジネス・ガバナンスを導入し、ビジネスがIAMの制御をできるようにし、IAMをITの領域から解放することを目的としています。基本原則は以下の通りです：

*   ガバナンス・リスクとコンプライアンス：組織が管理していることを示すことができ、法律や規制を遵守し、「エンロン」問題を防ぐ。
    
*   競合他社の取り組み、競争優位性：業界のベストプラクティスに従うか（例えば、競合他社がIGAを導入した）、市場をリードするか（例えば、優れたCIAMプラットフォームを導入する）。 
    

これらの問題は、ビジネスケースの質的要素として捉えることもできます。

@row
#### Tactical

The tactical drivers may include enhancing business processes and information flows, structuring the organization to be more agile, and supporting merger and acquisition processes. But another driver could be to reduce technical debt that prevents innovation and agility. Older identity management solutions that are end-of-support or do not scale well to the cloud should be replaced.

The tactical components can be both quantitative and qualitative.

@column
#### 戦術的

戦術的な推進要因としては、ビジネスプロセスと情報フローの強化、よりアジャイルな組織構造の構築、合併・買収プロセスの支援などが考えられます。しかし、もう１つの原動力は、革新と俊敏性を妨げる技術的負債を削減することです。サポートが終了したまたはクラウドにうまく拡張できない古いアイデンティティ管理ソリューションは、リプレースする必要があります。

戦術的要素には、定量的なものと定性的なものの両方があります。

@row
#### Operational

Operational considerations are related to the effectiveness and efficiency of people, processes, and technology. The automation of manual processes, increasing efficiency through self-service activities, and improving user experience are relevant topics for the business case.

These manual processes can be automated:

*   User account management - In the JML processes, the workflow and the lifecycle can be automated based on transactions in the source system for identities (HR, student management, customer relationship management (CRM), etc.). For example, when Role-Based Access Control (RBAC) is implemented, granting and revoking of roles can also be automated. So, user and account management, as well as role management, can be automated, resulting in less manual work, faster processing, better data quality, and cost savings.
    
*   Password reset – establishing a self-service mechanism for password resets increases user satisfaction and customer service efficiency.
    
*   Reporting, certification, and attestation processes - these can be automated, resulting in more transparency.
    
*   Data processing disclosure - Informing customers about the processing of their data can be automated in CIAM portals.
    
*   Single Sign-on (SSO) – SSO enhances user convenience and reduces all kinds of service desk-related calls.
    
*   Automated logging and auditing – Automated logging will facilitate security operations and forensic readiness.
    

Many of the operational issues can be regarded and calculated as quantitative components in the business case.

@column
#### 運用的

運用での考慮点は、人、プロセス、テクノロジーの有効性と効率性に関係します。手作業によるプロセスの自動化、セルフサービス活動による効率の向上、ユーザーエクスペリエンスの向上は、ビジネスケースに関連するテーマです。

以下のの手動プロセスは自動化できるでしょう：

*   ユーザーアカウント管理 - JMLプロセスにおいて、アイデンティティのソースシステム（人事、学生管理、顧客関係管理（CRM）など）における取引に基づいて、ワークフローとライフサイクルを自動化することができます。例えば、ロールベースアクセス制御（RBAC）が実装されている場合、役割の付与と取り消しも自動化できます。したがって、ユーザーとアカウントの管理およびロール管理を自動化することができ、その結果、手作業が減り、処理が速くなり、データ品質が向上し、コストが削減されます。
    
*   パスワードリセット – パスワードリセットのセルフサービス・メカニズムを確立するk遠出ユーザー満足度および顧客サービスの効率を向上させます。
    
*   報告、認定、証明プロセス - これらは自動化することができ、透明性がより高くなります。
    
*   データ処理の開示 - 顧客情報の処理について顧客に知らせることはCIAMポータルで自動化できます。
    
*   シングルサインオン（SSO） – SSOはユーザーの利便性を向上させ、あらゆる種類のサービスデスクに関連した電話呼び出し減少させます。
    
*   自動化されたロギングと監査 – 自動化されたロギングはセキュリティ運用とフォレンジックへの縦鼻を容易にします。
    

運用上の問題の多くは、ビジネスケースを定量的な要素として考え、計算することができます。

@row
### One Invalid View

One argument for not investing in IAM is the notion that an organization may have already invested heavily in IAM solutions, resulting in capital expenses that have not yet been written off.

This is not how an organization should react to an identified need for change. Costs based on decisions in the past should not be used in future decision processes; past decisions would lead to lock-in or in-agility for keeping up with the old choices. This kind of reasoning is referred to as the ‘sunk cost fallacy’ where people as well as organizations often continue with an action even as the costs outweigh the benefits. [^8] A useful counterargument to combat this fallacy is that, in hindsight, individuals would make different decisions for their organization.

@column
### 誤った観点の1つ

IAMに投資しない論拠の一つは、組織がすでにIAMソリューションに多額の投資をおこなっており、その結果、まだ償却されていない資本費用が発生している可能性があるという考え方であす。

これは、変革の必要性が明らかになったときに、組織がとるべき対応ではありません。過去の意思決定に基づくコストは、将来の意思決定プロセスで使うべきではありません；過去の意思決定は、古い選択肢を維持するためのロックインやアジリティ不足につながでしょう。このような理論は「サンクコストの誤謬」と呼ばれ、組織だけでなく人々もコストが利益を上回っているにもかかわらず、行動を継続することが多いことを指します。 [^8] この誤謬に対抗するための有効な反論は、後知恵を働かせれば、個人は組織のために異なる決定を下すというものです。

@row
## Overview of Business Case Topics

This section offers an overview of the different components of the business case for IAM. It is by no means a complete overview, but it gives an indication of arguments for convincing anyone of the positive effects of investing in an IAM program. The tables suggest both the quantitative and the qualitative components of the business case for each of the three example domains: IGA, CIAM, and PAM. These examples can act as templates for other domains; practitioners will need to adapt the specifics to suit their own organizations and use cases. The strategic, tactical, and operational components can be recognized as components in the qualitative and quantitative columns of the tables.

The first table shows the components of the business case for Identity Governance and Administration (automating JML and implementing RBAC). In this table, both positive (green background) and negative (red background) components of both the quantitative aspects (left column) and qualitative aspects (right column) of the business case are explained.

The consecutive tables show comparable topics for both CIAM programs and PAM programs.

The negative financial components (investments, licenses, costs) are comparable for all three domains.

A basic cost savings formula is shown for some of the financial and quantitative components as guidance. It will, however, be meaningless without a good explanation of the benefits.

_**Please view the [PDF](https://bok.idpro.org/article/97/galley/222/view) to see the tables.**_

@column
## ビジネスケースに関するトピックの概説

このセクションでは、IAMのビジネスケースのさまざまな構成要素について概説します。決して完全ではないが、IAMプログラムに投資することのポジティブな効果を誰にでも納得してもらうための論拠を示しています。この表は、3つの事例の領域（IGA、CIAM、PAM）それぞれについて、ビジネスケースの定量的要素と定性的要素の両方を示唆しています。これらの例は、他の領域に対するテンプレートとして機能します；実務者は、自組織やユースケースに合わせて具体的な内容を調整する必要があるでしょう。戦略的、戦術的、運用的な構成要素は、表の質的・量的な列の構成要素として認識することができます。

最初の表は、アイデンティティ・ガバナンスと管理（JMLの自動化とRBACの実装）のビジネスケースの構成要素を示しています。この表では、ビジネスケースの量的側面（左の列）と質的側面（右の列）の両方について、肯定的な構成要素（緑の背景）と否定的な構成要素（赤の背景）の両方を説明しています。

連続した表は、CIAMプログラムとPAMプログラムの両方で同等のトピックを示しています。

ネガティブな財務的要素（投資、ライセンス、コスト）は、3つの領域すべてで同等です。

基本的なコスト削減の方程式は、ガイダンスとして財務的・定量的要素のいくつかについて示されています。しかし、この方程式は利益に関する適切な説明がなければ意味をなしません。

_**表を確認するために[PDF](https://bok.idpro.org/article/97/galley/222/view)を閲覧してください。**_

@row
## Closing Thoughts About the Business Case

As explained before, a short-term positive real quantifiable business case can hardly ever be achieved. For instance, the real benefits of automating the JML flow with RBAC will only be apparent after several years, after adding multiple target systems across multiple lines of business, thus generating more business value. When looking through one-year project glasses, the outcome will not be financially interesting enough. IAM cannot just be seen from a financial perspective; there are many more considerations to be taken into account.

Pay attention to the following:

The issue of just focusing on the financial business case is too restrictive, more so when the investing stakeholder Is not the stakeholder who benefits from the investment—as is often the case. In many cases, the IT department is the cost center funding the investment. But, as can be seen in the business case examples, other departments profit from the investment in IAM. It is therefore essential to identify all stakeholders and the advantages they gain from the investment in IAM solutions, even if these benefits are not financial.

A second topic that should not be ignored in the financial savings area. Many manual activities are ‘hidden’ costs, including when users request access, and managers review existing authorizations, approve new requests, create accounts, and grant permissions or roles. These activities disappear in the ‘normal’, daily tasks of employees and so often go unaccounted for. By automating these tasks, employees can focus on more valuable activities. In the financial business case, quantifying this element may be an unwanted eye-opener.

Considering a multi-faceted business case for IAM is essential for every IAM program. A business case that goes beyond financial considerations will build awareness and commitment for starting a multi-year program that adds value to long-term business continuity. Approval is nice, but do not make it depend on a financial business case only.

@column
## ビジネスケースについてのまとめ

先に説明したように、短期的にポジティブな実際の定量化可能なビジネスケースが達成されることはほとんどありません。例えば、JMLフローをRBACで自動化することの本当のメリットは、数年後、複数のビジネスラインにまたがる複数の対象システムを追加し、より多くのビジネス価値を生み出して初めて明らかになります。1年間のプロジェクト成果を場合、それは財務的に充分に興味深いものではないでしょう。IAMは財務的な観点からだけ見ることはできません。

以下のことに注意してください：

財務的なビジネスケースだけに焦点を当てるという問題は、投資を決定する利害関係者が投資から利益を得る利害関係者ではない場合（よくあるケース）には、制限が大きすぎます。多くの場合、IT部門は投資資金を調達するコストセンターです。しかし、ビジネスケースの例でわかるように、他の部門もIAMへの投資から利益を得ています。したがって、すべての利害関係者を特定し、たとえこれらの利益が財務的なものではないとしてもIAM ソリューションへの投資から彼らが得る利益を特定することが重要です。

財務的節約の分野で無視できない2つ目のトピックがあります。多くの手作業は「隠れた」コストであり、ユーザーがアクセスを要求するとき、管理者が既存の認可を確認し、新しいリクエストを承認し、アカウントを作成し、権限やロールを付与するときなどが含まれます。このような活動は、従業員の「通常の」日常業務に紛れているため、計上されないことが多いです。これらの作業を自動化することによって、従業員はより価値のある活動に集中することができます。財務的なビジネスケースにおいて、この要素を定量化することは、目を見張るものがあるかもしれません。

IAMの多面的なビジネスケースを検討することは、すべてのIAMプログラムにとって不可欠です。財務的な検討を超えたビジネスケースは、長期的な事業継続に付加価値を与える複数年に渡るプログラムを開始するための意識とコミットメントを構築します。承認は素晴らしいですが、それを財務的なビジネスケースだけに依存させてはなりません。

@row
## Acknowledgments

The author wishes to thank Robert Sherwood and IDPro Principal Editor Heather Flanagan for their reviews and assistance in writing this article, turning thoughts into words.

@row
## Additional Reading

Beattie, Andrew. 2022. “How to Calculate Return on Investment (ROI).” _Investopedia_ , August. https://www.investopedia.com/articles/basics/10/guide-to-calculating-roi.asp.

Azmi, A. M. (2007). [_Business cases for information technology projects_](https://www.pmi.org/learning/library/business-cases-information-technology-projects-7365) . Paper presented at PMI® Global Congress 2007—EMEA, Budapest, Hungary. Newtown Square, PA: Project Management Institute.

James Cook University (14th February 2020). [_How to Write a Business Case_](https://online.jcu.edu.au/blog/how-to-write-business-case) : Tips, Resources and Examples.

Wikipedia contributors, "Business case," _Wikipedia, The Free Encyclopedia,_ [https://en.wikipedia.org/w/index.php?title=Business\_case&oldid=1164376316](https://en.wikipedia.org/w/index.php?title=Business_case&oldid=1164376316) (accessed October 17, 2023).

@row
## Author Bio

André Koot is principal consultant at and co-founder of SonicBee, a Dutch IAM consultancy company (IDPro partner), focused on business consultancy and giving IAM training courses. He is also a member of the IDPro BoK committee and (co-)authored several articles in the BoK.

- - -

[^1]:  Schueler, Chris. 2022. “Neglecting The IAM Process Is Fighting A Losing Battle To Achieve Operational Excellence.” Forbes, April 8, 2022. [https://www.forbes.com/sites/forbestechcouncil/2022/04/08/neglecting-the-iam-process-is-fighting-a-losing-battle-to-achieve-operational-excellence/?sh=2a6b16147977](https://www.forbes.com/sites/forbestechcouncil/2022/04/08/neglecting-the-iam-process-is-fighting-a-losing-battle-to-achieve-operational-excellence/?sh=2a6b16147977) . 
    
[^2]:  “Manage Technology Debt to Create Technology Wealth.” Gartner. August 17, 2020. [https://www.gartner.com/en/documents/3989188](https://www.gartner.com/en/documents/3989188) . 
    
[^3]:  ​​ Shea, Sharon. “How IAM Systems Support Compliance.” _Security_ , July 2020. [https://www.techtarget.com/searchsecurity/tip/Identity-management-compliance-How-IAM-systems-support-compliance](https://www.techtarget.com/searchsecurity/tip/Identity-management-compliance-How-IAM-systems-support-compliance) . 
    
[^4]:  Hayes, Adam. “What Was Enron? What Happened and Who Was Responsible.” Investopedia, March 2023. [https://www.investopedia.com/terms/e/enron.asp](https://www.investopedia.com/terms/e/enron.asp) . 
    
[^5]:  Allen, Frederick E. 2019. “Apocalypse Then: When Y2K Didn’t Lead To The End Of Civilization.” _Forbes_ , December 29, 2019. [https://www.forbes.com/sites/frederickallen/2020/12/29/apocalypse-then-when-y2k-didnt-lead-to-the-end-of-civilization/?sh=6c4625dc475c](https://www.forbes.com/sites/frederickallen/2020/12/29/apocalypse-then-when-y2k-didnt-lead-to-the-end-of-civilization/?sh=6c4625dc475c) . 
    
[^6]:  “Basel IV Implementation in the EU: What Does the New Banking Package Mean for Banks?” 2022. Oxford Law Blogs. February 3, 2022. [https://blogs.law.ox.ac.uk/business-law-blog/blog/2022/02/basel-iv-implementation-eu-what-does-new-banking-package-mean-banks](https://blogs.law.ox.ac.uk/business-law-blog/blog/2022/02/basel-iv-implementation-eu-what-does-new-banking-package-mean-banks) and “Solvency II.” n.d. European Insurance and Occupational Pensions Authority. [https://www.eiopa.europa.eu/browse/regulation-and-policy/solvency-ii\_en](https://www.eiopa.europa.eu/browse/regulation-and-policy/solvency-ii_en) . 
    
[^7]:  Larson, Theodore, and Daniel Friesen. n.d. “The Anthony Triangle and an Analytics Framework: Developing a Business Analytics Curriculum Conceptual Model.” _CERN European Organization for Nuclear Research_ . December 2020. [https://doi.org/10.5281/zenodo.3996830](https://doi.org/10.5281/zenodo.3996830) . 
    
[^8]:  “The Sunk Cost Fallacy - The Decision Lab.” n.d. The Decision Lab. [https://thedecisionlab.com/biases/the-sunk-cost-fallacy](https://thedecisionlab.com/biases/the-sunk-cost-fallacy) . 
