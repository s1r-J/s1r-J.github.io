---
layout: columns
title: Ethics for Digital Identity and Identity-Driven Algorithms
permalink: /docs/oidc_oauth/idpro_bok/105
date: 2024-09-09
modify_date: 2025-04-20
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "倫理", "デジタルアイデンティティ"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/105/](https://bok.idpro.org/article/id/105/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

Recent work by multiple organizations has helped to solidify a practical approach to ensuring the ethical use of digital identity technologies, including identity-driven algorithms. This article seeks to elucidate one approach that can improve internal ethical posture and foment comparisons between existing implementations across various industries. It establishes five ethical axes to evaluate and communicate relative strengths and weaknesses between implementations. The five key axes asserted herein include (1) well-being, (2) accountability, (3) transparency, (4) fairness, and (5) user data rights. Finally, the article explores a methodology for applying those axes within an organization.

Keywords: Ethics, Algorithms, Digital Identity

@column
## 概要

複数の組織によって近年の取り組みは、アイデンティティドリブンアルゴリズムを含むデジタルアイデンティティテクノロジーの倫理的な利用を確保する実践的なアプローチを固めるために役立ってきました。本稿では、組織内の倫理的な姿勢を改善し、様々な産業間の既存の実装の比較を誘導する1つのアプローチを解明しようとするものです。実装間の相対的な強みと弱みを評価して伝達するために5つの倫理的な軸を設定します。ここで主張する5つの重要な軸は、(1)幸福、(2)説明責任、(3)透明性、(4)公平性、(5)ユーザーデータの権利です。最後に、本記事ではこれらの軸を組織に適用するための方法論について探求します。

**Keywords:** 倫理, アルゴリズム, デジタルアイデンティティ

@row
By Mike Kiser (Sailpoint)

© 2024 IDPro, Mike Kiser

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code)._

@row
## Introduction

Algorithms that rely on digital identity and other data from the past to predict the future have long been commonplace: they predict what we will watch next,[^1] how financially stable we will be,[^2] or how likely we are to commit a crime.[^3] The assumption is that with enough data, anything is predictable. Over the last several years, however, headlines have repeatedly illustrated the influence of algorithms on human well-being and highlighted many inherent algorithmic biases.[^4] Before we embrace a digital identity solution or an associated algorithm, how can we ensure that they promote justice and fairness rather than reinforcing existing inequalities? How do we prevent new and unforeseen harms?

To answer the questions above, it is not enough to merely espouse ethical principles: “Do no harm” is only helpful if it comes with the tools for everyday use. The industry needs a _practical and measurable standard for digital identity and identity-driven algorithms_: this may enable improved ethical posture and the comparison between existing implementations of algorithms across various industries. This article looks to recent work by IBM,[^5] the IEEE,[^6] and the High-Level Expert Group on Artificial Intelligence (AI HLEG)[^7] , which have helped to solidify an ethical approach to the use of identity-driven algorithms. While these efforts focus on algorithms, their principles can provide the foundation for an ethical approach to digital identity more generally.

This paper proposes five ethical axes that build off of the work cited above and enable comparisons between digital identity solutions:

1.  Well-being
    
2.  Accountability
    
3.  Transparency
    
4.  Fairness
    
5.  User data rights.s
    

All three of the initiatives mentioned above share these five axes as core to an ethical approach to artificial intelligence are shared by, with varying emphasis on each of them. For example, the IEEE calls out the impact of effectiveness misuse and competence of a solution and provides a list of resources for further investigation. The AI HLEG provides a tiered model that describes how ethical principles translate into more practical activities. IBM’s design emphasizes the importance of establishing ethics as an underpinning part of a solution’s design rather than an afterthought.

The five axes chosen in this paper reflect common elements of these approaches; together, they form a proposed framework and basis for further ethical exploration by identity practitioners.

Note that IDPro is concurrently releasing another article, _Ethics and Digital Identity_, which adopts some of these values and adapts others. That article explores the theoretical underpinnings of ethics – including the importance of having conversations and developing a shared understanding of ethical values within the communities served. As such, we strongly urge you to consider the values herein as inputs to a conversation rather than the end of one.[^8]

@column
## はじめに

デジタルアイデンティティおよびそのほか将来を予測するための過去からのデータに依存するアルゴリズムは、長きにわたり一般的になっています：私たちが次に何を見るのかを予測し [^1]、経済的にどれほど安定するのか [^2]、またはどれくらいの可能性で犯罪を犯すのか [^3]。前提として、充分なデータがあればどのようなことでも予測できるというものがあります。しかし、ここ数年で、見出しは繰り返し人間の幸福におけるアルゴリズムの影響を説明し、アルゴリズムに内在する多くのバイアスを浮き彫りにしてきました。 [^4] デジタルアイデンティティソリューションまたは関連するアルゴリズムを受け入れる前に、既存の不平等を強化するよりも正義と公平性を促進することをどの程度確認できるでしょうか？新たな、そして不測の損害をどの程度防ぐことができるでしょうか？

上述の疑問に回答するためには、単に倫理的な原則をとなるだけでは充分ではありません：「危害を加えないこと」は、日常利用するツールだけ役立ちます。産業は、 _デジタルアイデンティティおよびアイデンティティドリブンアルゴリズムのための実践的で、測定可能な基準_ を必要とします：この基準は、リンrにて来な姿勢と様々な産業間で既存のアルゴリズム実装の比較を改善できるかもしれません。この記事では、IBMによる最近の取り組み [^5]、IEEEの取り組み [^6]、そしてHigh-Level Expert Group on Artificial Intelligence（AI HLEG）の取り組み [^7]について見ていきます。これらはアイデンティティドリブンアルゴリズムの利用に対する倫理的なアプローチを強固にするために役立ちます。これらの努力はアルゴリズムに着目していますが、これらの原則はより一般的なデジタルアイデンティティに対する倫理的なアプローチに基礎を提供することができます。

本稿では、前述で引用した取り組みに基づき、デジタルアイデンティティソリューション間の比較を可能にする5つの倫理的な軸を提案します：

1.  幸福
    
2.  説明責任
    
3.  透明性
    
4.  公平性
    
5.  ユーザーデータの権利
    

前述の3つの取り組みはすべて、人工知能に対する倫理的なアプローチの核としてこれら5つの軸を共有していますが、それぞれで重点の置き方が異なっています。例えば、IEEEは有効性の誤用とソリューションの適性の影響について言及し、さらなる調査のためのリソース一覧を提供しています。AI HLEGは、倫理的な原則がより実践的な活動にどの程度変換されるのかについて説明する階層モデルを提供しています。IBMの設計は、後付けではなくソリューションの設計の基礎部分として倫理を確立することの重要性について協調しています。

本稿で取り上げる5軸は、これらのアプローチの共通する要素を反映します；同時に、これらはアイデンティティ実務者による倫理的な探求をさらにおこなうための提案されたフレームワークおよび基礎を形成します。

IDProは、別の記事として _Ethics and Digital Identity_ を同時にリリースしており、一部の価値観の採用とその他の適応をおこなっています。この記事では、倫理の理論的な基盤を探求しており、サービスを提供するコミュニティ内で対話を実施することおよび倫理的な価値観の共有理解を発展させることの重要性を述べています。このように、私たちはここに書かれている価値観を、対話の終わりではなく、インプットと考えてもらうことを強く推奨しています。
 [^8]

@row
## A Proposed Ethical Maturity Graph

This article proposes a standard approach bolstered by easily accessible tools that create a practical ethical evaluation and comparison method. Any analysis or evaluation is only useful if its intended audience understands it. To that end, a radar chart is recommended to communicate the evaluation of any particular use of digital identity, artificial intelligence, and associated algorithms. This visual representation creates a means for evaluating past ethical progress and an implementation’s relative strengths or weaknesses.

@column
## 倫理的成熟度グラフの提案

この記事では、実用的な倫理的な評価と比較方法を作成するための簡単に利用できるツールによって強化された標準的なアプローチを提案します。いかなる分析や評価も、想定される聴衆がそれを理解しているときにしか意味を成しません。つまり、デジタルアイデンティティ、人工知能そして関連するアルゴリズムの特定の利用に関する評価についてコミュニケーションをとるためには、レーダーチャートがおすすめです。この視覚表現は、過去の倫理的な進歩と実装の相対的な強みまたは弱みを評価する方法となります。

@row
![A diagram of a person's performance Description automatically generated with medium confidence](/assets/images/idpro_bok/105-image1.png)

Figure 1 - A Proposed Framework for Ethical Evaluation

@row
Each of the five axes in Figure 1 is assessed and then plotted on a radar chart for quick visual comprehension (the center of the graph connotes complete ethical immaturity for that axis).

Since every organization seeking to utilize technology ethically has unique requirements or needs, creating this graph involves self-evaluation. At the same time, it is important to note that practitioners may find common processes and tools helpful for evaluating each axis.

The following section examines each axis in Figure 1, highlighting key processes and best practices that will increase ethical maturity. Where possible, it offers open-source tools or readily available techniques and provides a concise guide for self-evaluation along that particular axis.

@column
Figure 1の5軸のそれぞれが評価され、視覚的に理解しやすいようにレーダーチャートにプロットされます（グラフの中心はその軸が倫理的に完全に未熟であることを意味します）。

テクノロジーの倫理的な活用を模索するすべての組織は固有の要件やニーズを有しているため、このグラフを作成するには自己評価が含まれます。同時に、実務者が各軸の評価に役立つ一般的なプロセスとツールを見つけることが重要です。

以下のセクションでは、Figure 1の各軸について検証し、重要なプロセスおよび倫理的な成熟度を高めるであろうベストプラクティスを強調します。可能であれば、オープンソースなツールや簡単に利用できるテクニックを示し、特定の軸に沿った自己評価についての簡潔なガイドを提供します。

@row
### Well-Being

The first tenet of a practical ethical approach is that an identity practitioner must put human well-being first. This is not normally a controversial assertion. The question, then, is what the term “well-being” signifies. Certainly, there is an established, widely accepted truth that grounds well-being and is expressed in the Hippocratic oath: “Do no harm,” but the concept must involve more than a mere defensive approach.

As explored in _Ethics and Digital Identity,_ the question remains: whose well-being should be prioritized?[^9] Practitioners often make difficult choices: to protect one group or class may negatively impact another. Determining well-being is not simple when wielding the power of identity since well-being is nuanced and often culturally dependent. This context-dependence means exploring and documenting the interplay of interests for all parties. There may not be clear-cut answers for complex issues, but a methodological approach is essential for understanding the impact of decisions made in the development of new solutions.

Using a tool known as an “ethics canvas,” these choices and outcomes may be explored and centrally documented.[^10] Identifying the affected individuals, their relationships, and worldviews helps to give concrete insight into whose interests might be in conflict and what trade-offs underlie each decision or implementation choice.

@column
### 幸福

実践的な倫理的アプローチの第一の信条は、アイデンティティ実務者が人間の幸福を第一に考えなければならないということです。これは通常、議論の余地がない主張です。問題は、「幸福」という単語が何を意味するのかということです。幸福の根拠となり、ヒポクラテスの誓いで表現されている、確立され、広く受け入れられている真理が間違いなくあります：「害をなしてはならない」は、単なる防御的なアプローチ以上のものが含まれていなければならない概念です。

_Ethics and Digital Identity_　で探求されているように、疑問は残ります：誰の幸福が優先されるべきでしょうか？ [^9] 実務者はしばしば難しい選択を迫られます：あるグループや階層を守るために、別のグループや階層にネガティブな影響を及ぼすかもしれません。幸福は微妙な差異があり、多くの場合には文化に依存するため、アイデンティティの力を行使する場合に幸福の定義は単純ではありません。このコンテキスト依存性は、すべての関係者にとって利益の相互関係を探り、文書化することを意味します。複雑な問題に対する明快な回答はありませんが、新たなソリューションの開発における決定の影響を理解するには、方法論的なアプローチが不可欠です。

「倫理キャンバス」として知られるツールを使うことで、これらの選択および結果について探求し、一元的に文書化することができます。 [^10] 影響を受ける個人、関係性、世界観を特定することは、誰の利益が対立関係にあり、それぞれの決定や実装の選択にどのようなトレードオフが存在しているのかについて具体的な洞察をおこなうのに役立ちます。

@row
![A screenshot of a computer screen Description automatically generated](/assets/images/idpro_bok/105-image2.png)

Figure 2: Example of an Ethics Canvas

@row
This process helps all participants — from designers to implementers — to contemplate the ramifications of their decisions and to embed a mindset that seeks to underscore the morality of their actions more clearly. This central document establishes the ethical standard that all participants agree to abide by; it is a guiding force throughout the rest of the process.

@column
このプロセスはすべての参加者、設計者から実装者まで、が自分たちの決定の影響について熟考し、自分たちの行動の道徳性をより明確しようとする考えを根付かせることができます。この中心的な文書は、すべての参加者が遵守することに同意する倫理基準を確立するものであり、プロセスの残りの部分を通して指針となるものです。 

@row
![A black text on a white background Description automatically generated](/assets/images/idpro_bok/105-image3.png)

Figure 3: Human Impact in the Ethical Maturity Framework

@row
This documentation increases ethical maturity by ensuring that the organization has, at minimum, explored and documented its human impact and, at best, regularly reviews whether its impact matches its intent.

@column
この文書化は、組織が少なくともその人的影響について調査し、文書化をおこなった、最も良い場合には定期的にその影響が意図に合致していることをみなすことを保証することで、倫理的成熟度を高めます。

@row
### Accountability

Once the ethical choices have been laid out using the ethics canvas above, organizations seeking ethical maturity must ensure that they are accountable for meeting the newly documented ethical standard. There are two primary ways to achieve accountability. First, all ethical decisions must be tracked as solutions that are designed and architected. Documentation encourages designers, architects, and implementers to make ethical choices and records a rationale for each choice. Second, a feedback loop must be built into the solution so that the end users (those directly impacted by the technology) have a method for holding the designers and creators of identity systems accountable.

Documenting past choices reinforces the notion of responsibility for those decisions – something people are far too willing to abdicate. Previous studies have found that as technology emerges, humans become more reliant on the technology rather than their own faculties. An easy illustration of this occurred as mobile devices became popular: before the rise of the mobile phone, most people had at least a score of numbers committed to memory so that they could call friends and family. Subsequently, they relied on their devices — technology — to provide that number recall function. Research has shown that this process is writ large across society: technology such as search engines and the internet have shifted recall from the actual content (phone numbers, key facts, dates, and navigation) to the location to find that content online.[^11] In short, we have delegated that memory function to technology. There is an inherent danger that using identity data (particularly in algorithms) will lead people, organizations, and ultimately large swathes of humanity to cede ethical choices. They will merely remember “whom to ask” (or what service to call) rather than feeling accountable for the decisions themselves. Documenting choices compels technologists to remember that the choice (and its consequences) lies with them.

@column
### 説明責任

前述の倫理キャンバスを用いて倫理的な選択肢が示された場合、倫理的成熟を追い求める組織は新たに文書化された倫理基準に適合するように説明責任を確実に果たすようにしなければなりません。説明責任を達成するには主に2つの方法があります。1つ目は、すべての倫理的決定は設計および構築されたソリューションとして追跡されなければなりません。ドキュメントは設計者、アーキテクトおよび実装者に倫理的決定をおこない、それぞれの選択における根拠を記録する助けとなります。2つ目は、フィードバックループは、エンドユーザー（テクノロジーによって直接影響を受ける人々）がアイデンティティシステムの設計者と作成者に説明責任を負わせる方法を持つように、ソリューションに組み込まれなければなりません。

過去の選択をドキュメント化することは、人々が喜んで捨ててしまう決定の責任の概念を強化します。過去の研究ではテクノロジーが生まれると、人類は自分たちの能力よりもテクノロジーへ依存するようになることがわかっています。これが発生していることが端的に示されているのが、モバイルデバイスが一般的になったときです：携帯電話が登場する以前、ほとんどの人々は、友人や家族に電話をかけるために少なくとも数個の番号を記憶していました。結果として人々は番号を記録する機能を提供しているデバイス、テクノロジーに依存するようになりました。研究では、このプロセスは社会全体に広がっていることを示しています：検索エンジンやインターネットのようなテクノロジーが、実際のコンテンツ（電話番号、重要な事実、日付や道案内）から、そのコンテンツをオンラインで探す場所へ記憶することを移行しています。 [^11] 簡単に言えば、記憶する機能をテクノロジーに委譲しているということです。アイデンティティデータ（特にアルゴリズム）を利用することで人々と組織および人類の大部分が倫理的な選択を捨ててしまうように導くようになる危険性が内しています。人々は決定自体の説明責任を感じるのではなく、単に「誰に聞けばよいか」（もしくはどのサービスに問い合わせればよいか）を記憶するようになります。選択を文書化することで、技術者は選択（とその結果）が自自分自身であることを思い出すように強制します。

@row
![A white paper with black text Description automatically generated](/assets/images/idpro_bok/105-image4.png)

Figure 4: The Feedback Loop of Ethically Mature Organizations

@row
Figure 4 shows that accountability is more than internal processing. Giving voice to those impacted by the use of identity data provides essential feedback, illuminating the actual effects of an implementation. Features that allow comments and complaints into our systems in ways that are easy to use are not optional for an ethically mature organization. Far from being an “add-on,” this is a requirement for accountability — if the goal is fairness, then those who feel that a particular use of identity data or that an identity-based decision is unfair must be able to register their complaint.

@column
Figure 4は、説明責任が内部プロセス以上であることを示しています。アイデンティティデータの利用によって影響を受ける人々に声を聞くことは、不可欠なフィードバックが提供されることになり、実装の実際の効果を明らかにします。使いやすい方法でコメントや苦情をシステムに投稿する機能は、倫理的に成熟した組織にとってオプションではありません。これは「アドオン」ではなく、説明責任には要件です。つまり、目標が公平性であるならば、アイデンティティデータの特定の利用またはアイデンティティに基づく決定が公平ではないと感じる人々にとっては、苦情を登録できるものでなければなりません。

@row
### Transparency

For users to hold practitioners accountable, the reasons for those decisions must be transparent. True transparency not only answers the question of why, but it breaks down the how in a simple way. When applying this to identity, it is critical to use language that is easily understandable to the end user, as technical jargon can quickly become complex.

@column
### 透明性

ユーザーは実務者に説明責任を求めるために、これらの決定の理由に透明性がなければなりません。真の透明性とはなぜという疑問に答えるだけでなく、どのようにという問いを簡単な方法に分解することです。このことをアイデンティティに適用する場合、技術的な専門用語をすぐに複雑になるため、エンドユーザーにとって簡単に理解できる言葉を使うことが必須です。

@row
![A close-up of a white background Description automatically generated](/assets/images/idpro_bok/105-image5.jpg)

Figure 5: Ethical Maturity in Relation to Transparency

@row
This transparency is more than just disclosure for disclosure’s sake — it builds trust in the power of identity itself. Mature identity systems that can explain themselves and invite feedback (for accountability) promote a “virtuous loop” that increases the likelihood of an ethical standard undergirding a particular identity implementation.

@column
この透明性は、単なる開示のための開示よりも意味があり、アイデンティティ自体の力に対する信頼を構築します。成熟したアイデンティティシステムはそれ自身を説明することができ、（説明責任のための）フィードバックを求めることができ、特定のアイデンティティ実装を支える倫理基準の可能性を高くする「好循環」を促進します。

@row
### Fairness (Bias)

For identity to promote fairness, it must expose its own biases. Detection is successful only when the full range of bias is understood: there are helpful tools out there, such as IBM’s taxonomy of bias,[^12] which ranges from “shortcut bias” (doing too much, too quickly) to “impartiality bias” (false assumptions of sound judgment) and more direct prejudices (like “self-interest bias”).

Identifying bias is sometimes straightforward, such as when a flawed identity-based algorithm is blatantly biased, even to outsiders with little knowledge of the system. It is easier to spot and address these issues rapidly.

In other instances, biased outcomes can be more insidious: they must be discovered through diligent examination of the identity data and the process by which a system assimilates and learns from that data set. Hiring or salary determination algorithms that use historical data, which tend to depress the value of women in the marketplace,[^13] provide a well-known example of this. These biased data sets reflect past sociocultural trends in which women earned less money due to institutional, structural, familial, and other drivers. This poor data becomes a self-fulfilling prophecy that locks women into the patterns of the past.

@column
### 公平性（バイアス）

アイデンティティが公平性を促進するには、それ自身のもつバイアスを明らかにしなければなりません。すべてのバイアスが理解されたときにのみ、検出に成功します：IBMのバイアス分類法 [^12] は「ショートカットバイアス」（あまりにも多くのことをあまりに早くおこなうこと）から「公平性バイアス」（健全な判断の誤った想定）や直接的な偏見（「利己的バイアス」など）まで範囲としており、役立つツールです。

時には、バイアスを特定することが簡単な、欠陥のあるアイデンティティに基づいたアルゴリズムは明らかに偏っており、システムについて知識の少ない外部者でもそれがわかります。このような問題を早急に発見し、対応することは容易です。

他の例として、偏った結果はより狡猾です：偏った結果は、アイデンティティデータとそのデータセットからシステムが知識を吸収して学習しているプロセスの注意深く調査することで発見しなければなりません。過去のデータを利用した雇用や給与決定のアルゴリズムは、市場における女性の価値を低下させる傾向にあり [^13] 、よく知られた例の1つです。この偏ったデータセットは過去の社会文化的な傾向、つまり女性は制度的、構造的、家庭的、その他の要因によって収入が少なかった、を反映しています。この残念なデータは女性を過去のパターンに閉じ込める自己成就的予言となります。

@row
![A black text on a white background Description automatically generated](/assets/images/idpro_bok/105-image6.png)

Figure 6: Ethical Maturity in Relation to Fairness

@row
There are many examples in which algorithms can perpetuate biased outcomes. To achieve a mature ethical posture, organizations that identify one of these issues at play in their model or proposed implementation should return to the well-being axis: with the new information in hand, a reevaluation of the use of technology (e.g., AI or other algorithms) is necessary to understand the impact on affected parties–and to discern whether or not the system can be refactored to address and correct for inequality.

@column
このアルゴリズムが偏った結果を永続化させうる例は数多くあります。成熟した倫理的姿勢を達成するには、組織のモデルや提案されている実装においてこれらの問題を特定した組織は幸福の軸に立ち返るべきです：新たな情報を手にして、テクノロジー（例、AIやほかのアルゴリズム）の利用を再評価することは、影響を与える関係者への影響を理解し、不平等に対処して是正するためのリファクタリングをシステムに実施できるかできないかを見極めるために必要になります。

@row
### User Data Rights

User data rights underpin other essential ethical considerations. Rather than a nice-to-have, privacy and control over the data that comprise identity is recognized as a fundamental human right. Article 12 of the Universal Declaration of Human Rights, adopted in 1948 by the General Assembly of the United Nations, states, “No one shall be subjected to arbitrary interference with his privacy, family, home or correspondence, nor to attacks upon his honor and reputation. Everyone has the right to the protection of the law against such interference or attacks.”[^14] While we may not have had a complete reckoning over what this means in the digital age,[^15] more than 160 countries have either enacted data privacy laws or are in the process of doing so – reinforcing that the right to control personal attributes and data is moving towards near-universal acceptance.[^16]

Assuming that ethical maturity is the goal, technology that supports user data rights should be an automatic inclusion for anyone seeking to use identity and personally identifiable data. These include standards that grant the user control over the use of their data, such as enabled by User Managed Access (UMA), consent management, and selective disclosure. Furthermore, organizations should apply techniques that ensure personal data cannot be associated with individuals and correlated (data anonymization, pseudonymization, and differential privacy).[^17] These techniques and tactics provide a firm grounding for realizing ethical standards.

@column
### ユーザーデータの権利

ユーザーデータの権利は、他の本質的な倫理的な考察を支えるものです。プライバシーとアイデンティティを含むデータの制御は、あればよいというものではなく、基本的人権として認識されています。1948年に国連総会で採択された世界人権宣言の12条では、「何人も、自己の私事、家族、家庭若しくは通信に対して、ほしいままに干渉され、又は名誉及び信用に対して攻撃を受けることはない。人はすべて、このような干渉又は攻撃に対して法の保護を受ける権利を有する。」 [^14] と記載されています。デジタル時代においてこれが意味することは完全には理解されていない [^15] と思われるが、160カ国以上がデータプライバシー法を制定しているか、制定している途中であり、個人の属性やデータを制御する権利はほぼ普遍的なものとして受け入れられつつあります。 [^16]

倫理的成熟が目標だと仮定すると、ユーザーデータの権利を支えるテクノロジーは、アイデンティティおよび個人の特定できるデータを利用しようとする人にとって自動的に組み込まれるべきです。これらには、データの利用に対する制御をユーザーに付与する標準仕様、ユーザー管理アクセス（UMA）や同意管理、選択的開示などが含まれます。さらに、組織は個人データが個人に紐づけられたり、関連付けられたりしないようにする技術（データ匿名化、仮名化や差分プライバシー） [^17] を適用すべきです。これらの技術や戦略は倫理的基準を実現するための確固たる基礎となります。

@row
![A close-up of a document Description automatically generated](/assets/images/idpro_bok/105-image7.png)

Figure 7: Ethical Maturity in Relation to User Data Rights

@row
Ethically mature organizations understand what data they are collecting, justify how and why it is being used with respect to their ethical position, and take sufficient steps to protect that data.

Note that “user data” can go beyond individuals’ private data. Even when users willingly consent to use their data – and even when data is collected anonymously – that data can be used to do unethical things. Elizabeth Renieris notes in her book _Beyond Data_ that an overreliance on “user control” can open the door to other harms without suitable controls.[^18] These harms might include data uses that the user misunderstood or did not foresee (after they clicked “consent” on a screen that lacked transparency). It may also include attempts to use mass amounts of anonymized data to manipulate (or, in UN parlance, “arbitrarily interfere with”) behavior. The Cambridge Analytica scandal provides a valuable example.[^19]

@column
倫理的に成熟した組織では、どのようあデータを収集しているかを理解しており、そのデータを倫理的立場においてどのように、なぜ利用するのかを正当化し、そのデータを保護するために充分な処置を実施しています。

「ユーザーデータ」は個人のプライバシーデータの範囲を超えていることに注意してください。ユーザーがそのデータを利用することにすすんで同意している場合でも、データが匿名化されて収集されている場合でも、非倫理的なものに使われる可能性があります。Elizabeth Renieris氏は、自身の著書 _Beyond Data_ で「ユーザー制御」に稼働に依存することは適切な制御がない限り、ほかの弊害をもたらすことになると指摘しています。 [^18] これらの弊害は、ユーザーが誤解していたり、予見していなかったり（透明性に欠けている画面の「同意」をクリックしたなど）するデータ利用が含まれるかもしれません。また、大量の匿名データを使って、行動を操作する（国連での「ほしいままに干渉」される）という試みも含まれるかもしれません。ケンブリッジ・アナリティカ問題は価値ある例の1つです。 [^19]

@row
## Evaluating Identity System Ethics

Once organizations carry out a self-audit on the axes above (or those they have selected after reflection and conversation), then the radial chart enables stakeholders to see the identity system ethics at a glance:

@column
## アイデンティティシステムの倫理の評価

上記の軸で組織が自己監査を実施すると（もしくは振り返りと対話を選択すると）、放射状のチャートによってステークホルダーがアイデンティティシステムの倫理について一目で確認できるようになります：

@row
![A diagram of a person's body Description automatically generated](/assets/images/idpro_bok/105-image8.png)

Figure 8: Example Ethics Analysis Radial Diagram

@row
Measures can then be taken to address areas of weakness. In the figure above, well-being is a well-founded goal of the organization. Still, there are issues with fairness and a near disregard for the principles of protecting user data rights, which are likely revealed by the transparent system that enables accountability (since both of these score highly).

The goal is continuous improvement, such that we are:

*   More aware of the impact of these systems on human well-being
    
*   Working for accountability internally and externally
    
*   Increasingly transparent in our decision-making
    
*   Seeking out other voices that might go unheard
    
*   Using standards that improve how user data rights are protected.
    

True ethical advancement requires, however, that the journey is not a solitary one. By comparing various algorithms, their data inputs and outputs, and how they are implemented, practitioners can begin to learn from one another. Lessons learned by one organization can spread rapidly throughout the community, advancing the cause of ethics and embedding an ethically-minded approach in the next wave of solutions.

Projecting several hypothetical analyses of comparable solutions on a single ethical maturity graph rapidly shows the relative strengths and weaknesses of each in an intuitive, visual way:

@column
弱点の領域に対処するための対策をとることができるようになります。上図では、幸福は組織にとってしっかりと達成しています。しかし、公平性についての門dナイトとユーザーデータの権利の原則をほとんど無視していることが、透明性があるシステムによる説明積んによって明らかになったと思われます（この軸のスコアは両者ともに高いため）。

継続的な改善の目標は、以下のようになります：

*   人間の幸福へのシステムの影響についてより認識する
    
*   内部および外部に対する説明責任が果たされている
    
*   意思決定の透明性を高める
    
*   聞かれていないかもしれない他の声を探し出す
    
*   ユーザーデータの権利を保護する方法を改善する標準仕様を利用する
    

しかし、真の倫理的進歩には、その旅が孤独でない必要があります。様々なアルゴリズム、データの入出力、それらをどのように実装するのかを比較することで、実務者は互いに学び始めることができます。ある組織が学んだ教訓は、コミュニティ全体に急速に広がり、倫理の主義を前進させ、倫理的アプローチをソリューションの次の波に組み込みます。

1つの倫理的成熟度グラフに、比較できるソリューションの複数の仮説的な分析を投影することで、それぞれの相対的な強みと弱みを直感的かつ視覚的な方法で素早く示すことができます：

@row
![A diagram of a diagram Description automatically generated](/assets/images/idpro_bok/105-image9.png)

Figure 9: Comparing Implementations on Ethical Axes

@row
Rather than abstract discussions that are often vague, a visual representation of the ethical status of an algorithm provides a framework to facilitate interaction and allow for productive learning between organizations and across an industry.

@column
しばしば曖昧な抽象的な議論よりも、アルゴリズムの倫理的な状態の視覚的な表現は、組織間および業界間での相互作用を促進し、生産的な学びを可能にするフレームワークを提供します。

@row
## Conclusion

Establishing and following an ethical standard for using digital identity — before developing the technology— is essential. As we race to embrace new technology, mine new data sources, and that anything is predictable with enough data, we would do well to pause. As identity systems and artificial intelligence converge, it is worth remembering what a Washington State Supreme Court case recently found:

_“We affirm this court’s long history of recognizing that one’s past does not dictate one’s future.”_ [^20]

Past patterns in aggregate can be helpful, but we must not lose sight of the individuals involved in the systems we build: to ensure that people are treated ethically creates ripples through society at large.

This article has sought to further the practice of ethics within the digital identity industry by delineating a pragmatic and measurable ethical approach for those involved in designing, directing, creating, and administering the next wave of technology. This five-pronged approach to ethics promotes discussions between those seeking to take an ethical approach to all phases of development and thus advances human well-being through innovation.

Done well, we build trust in the small, everyday tasks that, in turn, promote equitable outcomes and build systemic trust. Lest we be seduced by the power and potential of technology, we must not allow it to outpace our ethics. In short, we must strive to use digital identity with our humanity intact.

@column
## 結論

テクノロジーを開発する前にデジタルアイデンティティのための倫理的基準を確立し、従うことは非常に重要です。新しいテクノロジーを受け入れ、新しいデータソースを採掘し、十分なデータがあればすべてが予測可能であると競い合っているときに、一時的に立ち止まることは良いことです。アイデンティティシステムおよび人工知能が有効していくとき、ワシントン州最高裁判所の直近の判例を思い出すことには価値があります：

_「我々は、過去が未来を決定することはないことを認識している、この法廷の長い歴史を支持します」_ [^20]

収集された過去のパターンは助けになりますが、自身が構築したシステムにおいて個人から目を離してはなりません：人々を倫理的に扱うことを保証することは、社会全体に波紋を広げます。

この記事では、次のテクノロジーの波の設計、支持、作成および管理にかかわる人々のための計画可能で測定可能な倫理的アプローチを描くことで、デジタルアイデンティティ業界における倫理の実践を促進することを期待しています。倫理に対する5つの柱のアプローチは、すべての開発段階に倫理的アプローチをとろうとする人々でのディスカッションを促進し、イノベーションによって人間の幸福を進化させます。

うまくいくことは、小さな毎日のタスクにおいて信頼を気づき、最終的に公平な結果をもらたらし、組織的な信頼を築きます。テクノロジーの力と可能性によって誘惑されないように、倫理から逸脱しないようにしなければなりません。つまり、私たちは人間性を残したままデジタルアイデンティティを利用するように努めなければなりません。

@row
- - -

[^1]:  D. Jackson, “The Netflix Prize: How a $1 Million Contest Changed Binge-Watching Forver,” 7 7 2017. \[Online\]. Available: https://www.thrillist.com/entertainment/nation/the-netflix-prize.
    
[^2]:  K. Waddell, “The Atlantic,” 2 December 2016. \[Online\]. Available: https://www.theatlantic.com/technology/archive/2016/12/how-algorithms-can-bring-down-minorities-credit-scores/509333/. \[Accessed 12 July 2019\].
    
[^3]:  J. Angwin, J. Larson, S. Mattu and L. Kirchner, “Machine Bias,” 23 May 2016. \[Online\]. Available:  [^1] ProPublica, “Machine Bias,” ProPublica, 23-May-2016. \[Online\]. Available: https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing. \[Accessed: 01-Aug-2019\]. ‌. \[Accessed 12 7 2019\].
    
[^4]:  See 2 and 3 above.
    
[^5]:  A. Cutler, M. Pribić and L. Humphrey, “Everyday Ethics for Artifical Intelligence,” IBM Corp, New York City, 2019.
    
[^6]:  “The IEEE Global Initiative on Ethics of Autonomous and Intelligent Systems,” 2019. \[Online\]. Available: https://standards.ieee.org/content/dam/ieee-standards/standards/web/documents/other/ead1e.pdf. \[Accessed 15 July 2019\].
    
[^7]:  AI HLEG, “Ethics Guidelines for Trustworthy AI,” European Commission, Brussels, 2019.
    
[^8]:  Marsman, H. (2024) “Ethics and Digital Identity” IDPro Body of Knowledge 1(14) doi: https://doi.org/10.55621/idpro.104.
    
[^9]:  Ibid. Note, in particular, the discussion of Utilitarianism and the value of well-being.
    
[^10]:  “The Ethics Canvas,” 2017. \[Online\]. Available: https://ethicscanvas.org. \[Accessed 13 July 2019\].
    
[^11]:  B. Sparrow, J. Liu and D. M. Wegner, “Google Effects on Memory: Cognitive Consequences of Having Information at Our Fingertips,” Science, vol. 333, no. 6043, pp. 776-778, 2011.
    
[^12]:  A. Cutler, M. Pribić and L. Humphrey, “Everyday Ethics for Artificial Intelligence,” IBM Corp, New York City, 2019.
    
[^13]:  C. O'Neil, Weapons of Math Destruction, New York: Crown Publishers, 2016.
    
[^14]:  United Nations, “Universal Declaration of Human Rights,”10 December 1948, https://www.un.org/en/universal-declaration-human-rights/.
    
[^15]:  See, for example Renieris, Elizabeth M. _Beyond Data: Reclaiming Human Rights at the Dawn of the Metaverse_. MIT Press, 2023.
    
[^16]:  D. Banisar, “Banisar, David, National Comprehensive Data Protection/Privacy Laws and Bills 2018 (September 4, 2018). Available at SSRN: https://ssrn.com/abstract=1951416 or http://dx.doi.org/10.2139/ssrn.1951416,” 4 September 2018. \[Online\]. Available: https://ssrn.com/abstract=1951416. \[Accessed 12 July 2019\].
    
[^17]:  Kantara Initiative, “WG - User Managed Access,” site accessed 14 January 2020, https://kantarainitiative.org/confluence/display/uma/Home
    
[^18]:  Renieris, E. (2023) “Beyond Data”.
    
[^19]:  See, for example, Confessore, N. "[Cambridge Analytica and Facebook: The Scandal and the Fallout So Far](https://www.nytimes.com/2018/04/04/us/politics/cambridge-analytica-scandal-fallout.html)" New York Times: London (April 4, 2018)
    
[^20]:  https://www.courts.wa.gov/opinions/pdf/2016715.pdf \[Accessed 22 July 2024\].
