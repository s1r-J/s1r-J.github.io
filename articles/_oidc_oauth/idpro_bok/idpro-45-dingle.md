---
layout: columns
title: "Introduction to Identity - Part 2: Access Management"
permalink: /docs/oidc_oauth/idpro_bok/45
date: 2024-09-09
modify_date: 2024-09-16
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "アクセス管理"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/45/](https://bok.idpro.org/article/id/45/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

Who are you, and what are you allowed to do? In digital systems, these questions are the domain of “Identity and Access Management (IAM).” Access management systems provide the mechanisms for deciding who is who, and evaluate and enforce decisions about who should get access to what. Part 2 of the introduction explores the big picture of access management through a historical perspective. You can expect a little advice, a lot of context, and an experience-based overview of what we do in access management and why our contributions matter.

Keywords: Access Management, SSO, LDAP, Federation, WAM, MFA

@column
## 概要

あなたは誰で、あなたは何を許可されていますか？デジタルシステムにおいて。これらの質問は「アイデンティティとアクセス管理（IAM）」の領域です。アクセス管理システムは、誰が誰であるかを判断するのと、誰を何にアクセスさせるべきかという決定を評価して強制させるためのメカニズムを提供します。イントロダクションのパート2では歴史的な観点からアクセス管理を大きく見ていきます。少しの助言、多くのコンテキストそしてアクセス管理で何をするのか、なぜ貢献が重要なのかについて経験をもとにした概要を説明します。

Keywords: アクセス管理, SSO, LDAP, フェデレーション, WAM, MFA

@row
By Pamela Dingle

© 2020 IDPro, Pamela Dingle

@row
### Terminology

*   Ceremonies - predictable interactions that users can infrequently navigate in a well-watched place
    
*   Delegated authorization framework - an access control framework that decouples authentication from authorization, allowing the password to stay local and protected. [^1]
    
*   Federated Identity - the means of linking a person’s electronic identity and attributes, stored across multiple distinct identity management systems. [^2]
    
*   Least privilege - also known as the Principle of Least Privilege; a resource, such as a user, must only be able to access the resources (e.g., applications, data) that are necessary for it to function. [^3]
    
*   Trust federation - a trust framework between multiple entities with the purpose of leveraging identity and access management information in a controlled fashion.
    
*   Zero trust - From NIST Draft Special Publication 800-207, “Zero trust assumes there is no implicit trust granted to assets or user accounts based solely on their physical or network location (i.e., local area networks versus the internet)” [^4]
    
@column
### 用語解説

*   セレモニー - よく監視された場所で、稀にユーザが予測可能なやり取りを実行すること
    
*   委譲型認可フレームワーク - 認証と認可を切り離し、パスワードがローカルに留まり保護されるようなアクセス制御フレームワーク。 [^1]
    
*   フェデレーション・アイデンティティ - 複数の異なるアイデンティティ管理システムに保存されている個人の電子的アイデンティティと属性を紐づける手段。 [^2]
    
*   最小権限 - 最小権限の原則とも呼ばれる；ユーザーのようなリソースは、機能に必要な最低限のリソース（例、アプリケーションやデータ）だけにアクセスできるようにしなくてはならない。 [^3]
    
*   トラスト・フェデレーション - 複数のエンティティ間で、管理された方法でアイデンティティとアクセス管理情報を活用すること目的にしたトラスト・フレームワーク。
    
*   ゼロトラスト - NIST Draft Special Publication 800-207より、「ゼロトラストとは、物理またはネットワーク上(例えば、ローカルエリアネットワークとインターネットとの間)だけにおいて、資産またはユーザーアカウントに暗黙のトラストが付与されないということを前提とすること」 [^4]
    
@row
## Introduction

What is access management, and why is it so exciting? There is something thrilling and urgent about the moment a decision is made, a gate is lifted, and a precious resource is made available to a stranger. Did we make the right person productive, or did we make a risky mistake? Good access management depends on good identity data; it also requires policies that represent corporate rules, an accurate understanding of current environmental and contextual factors, and tools that can enforce according to a defined risk tolerance. A lot of preparation and consideration goes into the run-time decisions that are made every day and that operate with all kinds of granularity at infrastructure, middleware, and application layers.

If you are an experienced identity professional, you have watched our tools evolve - but if you are just starting, it can be valuable to hear some perspective on why things are the way they are. Hold on to your hats: this introduction is not even remotely objective, but it will give you one perspective on how we got here and how the concepts discussed in later chapters have evolved into our current access management landscape.

To kick off the ride, here are a few critical realities to keep in mind in the world of access management:

@column
## イントロダクション

アクセス管理とは何か、そしてなぜそんなにエキサイティングなのでしょうか？決断が下され、ゲートが開けられ、貴重な資源が見知らぬ人に利用できるようになる瞬間はスリリングで切迫したものがあります。適切な人を生産的にしたのでしょうか、それとも危険なミスを犯したのでしょうか？優れたアクセス管理は、優れたアイデンティティデータに依存しています。また、企業規則を表すポリシー、現在の環境とコンテキスト要素の正確な理解、定義されたリスク許容度に従って実施できるツールも必要です。インフラストラクチャ、ミドルウェア、およびアプリケーションの各レイヤーで、あらゆる種類の粒度で毎日おこなわれるランタイムでの決定には、多くの準備と考慮が必要です。

あなたが経験豊富なアイデンティティの専門家であれば、ツールの進化を見てきたでしょう。しかし、もしこれから始めるのであれば、なぜ現状がそのようになっているのかについての見解を聞くことは価値があるかもしれません。驚かずに聞いてください：このイントロダクションは客観的ではありませんが、どのようにしてここに至ったのか、後の章で議論する概念がどのように進化して現在のアクセス管理の状況になったのかについて、ひとつの視点を提供できるでしょう。

始める前に、アクセス管理の世界で覚えておくべきいくつかの重要な現実を紹介します：

@row
### Resources need stability

Company secrets, financial transactions, and personal communications are just a few examples of the precious resources that identity professionals are tasked with protecting. Resources may be exposed through application programming interfaces (APIs), web interfaces, or native mobile applications. Adding externalized access management capabilities to a single resource is relatively easy, but adding to a hundred or a thousand is exhausting. Owners of these applications rarely want to make frequent changes. After the first time, you as an identity professional try to schedule an application access management update within the change management windows of a hundred different applications, you will feel the same way.

@column
### リソースは安定を必要とする

企業機密、金融取引、個人的な通信などは、アイデンティティの専門家が保護を任されている貴重なリソースのほんの一例です。リソースは、アプリケーション・プログラミング・インターフェース（API）、Web インターフェース、またはネイティブ・モバイル・アプリケーションを通じて公開されていることがあります。単一のリソースに外部化アクセス管理機能を追加するのは比較的簡単ですが、100や1000のリソースに追加するのは大変な作業です。これらアプリケーションの所有者が頻繁に変更を加えたいと思うことはほとんどありません。アイデンティティの専門家として初めて、100種類のアプリケーションの変更管理ウィンドウ内でアプリケーション・アクセス管理の更新をスケジュールしようとしたら、同じように感じることでしょう。

@row
### Resources should not perform local identity management

If every resource you deploy performs its own login functions, it is nearly impossible to ensure that they follow the kinds of best practices detailed in places such as NIST 800-63B or adhere to unified corporate policies. [^5] Hundreds of applications each separately attempting to store credentials, protect a login page, and secure an account recovery process present an immense attack surface and make it likely that users will reuse passwords across applications. This pattern means an attacker who guesses the password to one application has a credential that can be replayed to gain access to other applications, and you have no way to know which applications are at risk.

@column
### リソースはローカルなアイデンティティ管理を実行すべきではない

デプロイする全てのリソースが独自のログイン機能を実行する場合、NIST 800-63Bなどで詳解されているベストプラクティスに従っているか、統一された企業ポリシーに従っているかを確認することはほぼ不可能です。 [^5] 何百ものアプリケーションがそれぞれ個別に認証情報の保存、ログインページの保護、アカウント回復プロセスの防御を試みているため、膨大な攻撃対象が存在し、ユーザーがアプリケーション間でパスワードを再利用する可能性が高くなります。このパターンは、1つのアプリケーションのパスワードを推測した攻撃者が、他のアプリケーションにアクセスするために再利用できるクレデンシャルを持つことを意味します。

@row
### Humans need challenges, but not obstacles

While resources need stability and consistency, humans need empathy. We require users to interact with computer systems to show they are the proper operator of the digital account they claim to have a right to; this process should be easy for a good user and tough for an impostor. The best practice is to create “ceremonies” - predictable interactions that users can infrequently navigate in a well-watched place. While authentication is the best-known ceremony, there are many other ways in which humans are asked to interact, such as self-service registration or account recovery, notifications, or transactional approval. We want users to notice when an unusual ceremony takes place because it may alert them that fraud is happening. Ceremonies are guaranteed to change as new attacks force administrators to try additional techniques, including changes in user experience (UX), authentication factors, and risk detection. While it is important to keep the attackers out, the experience of the good users is critically important. Faced with a tough problem, humans often behave predictably, and that predictability is an attack vector in itself. If you as the administrator make your users’ lives too hard, you become the problem: Users will circumvent the controls you put in place to try to protect them.

@column
### 人は課題を必要とするが、困難であってはならない

リソースは安定性と一貫性を必要とする一方で、人間は共感を必要とします。私たちは、ユーザーが主張するデジタルアカウントの正当な利用者であることを証明するためにコンピューターシステムとやりとりすることを要求します；このプロセスは善良なユーザーにとっては簡単で、詐欺師にとっては厳しいものであるべきです。ベストプラクティスは「セレモニー」、つまりよく監視された場所でユーザーが稀に予測可能なやりとりを実行すること、を作成することです。認証は最もよく知られたセレモニーですが、セルフサービスの登録、アカウント回復、通知や取引承認など人がやり取りを求められる方法は他にも多く存在します。一般的ではないセレモニーがおこなわれた場合、不正行為が起きた可能性を警告するため、ユーザーに気がついて欲しいのです。新しい攻撃手法がユーザーエクスペリエンス（UX）、認証要素およびリスク検知の変化を含む新しい技術を試すことを管理者に強制するため、セレモニーは必ず変更されます。攻撃者を排除し続けることは重要である一方、善良なユーザーのエクスペリエンスも非常に重要です。困難な問題に直面すると、しばしば人は予測可能な振る舞いをし、その予測可能性が攻撃の糸口になります。あなたが管理者としてユーザーの生活を厳しくしすぎると、あなたが問題になります：ユーザーは、ユーザーを守ろうとするあなたの管理を回避しようとするでしょう。

@row
### Garbage In, Garbage Out

The most visible parts of access management are decisions made in the moment, but those decisions do not exist in a vacuum. Before any access management decision is made, someone has to set up digital rules and policies that closely approximate the business goals of the organization (see “Introduction to Project Management for IAM Projects” for more on managing an IAM project). [^6] User, group, and role context must exist, and some combination of device, network, and risk context as well. By the time a user attempts to access a given resource, all of the data that might go into an access choice should be available. Never forget: It doesn’t matter how good your access management infrastructure is if decisions are based on bad input.

@column
### ゴミを入れたら、ゴミが出てくる

アクセス管理の最も目に見える部分は、その瞬間におこなわれる意思決定ですが、それらの意思決定はなにもない環境に存在するわけではありません。アクセス管理の意思決定がおこなわれる前に、誰かが組織のビジネスゴールに近いデジタルルールとポリシーを設定する必要があります（IAMプロジェクトの管理については「Introduction to Project Management for IAM Projects」を参照）。 [^6] ユーザー、グループ、ロールのコンテキストが存在し、デバイス、ネットワーク、リスクのコンテキストも何らかの組み合わせで存在しなければなりません。ユーザが特定のリソースにアクセスしようとする時点までに、アクセスの判断に必要なすべてのデータが利用できなければなりません。決して忘れてはならないのは、アクセス管理インフラがいかに優れていても、誤ったインプットに基づいて意思決定がおこなわれるのであれば、意味がないということです。

@row
### Now, on to the Fun Part

Identity professionals end up at the forefront of an age-old problem. We have resources to protect, users who want access, and attackers who want access as well and are really hard to distinguish from users. We need a system that is accurate, but no system will be 100% accurate, so the system must also follow the principles of zero trust, starting with least privilege. We must strongly authenticate users and leverage the environmental context to detect fraud. We must apply a single consistent policy view across a disparate landscape of resources. And we have to verify all the time that our systems are working the way we think they are.

@column
### さて、楽しいパートに移りましょう

アイデンティティの専門家は、古くからある問題の最前線に立たされています。保護すべきリソースがあり、アクセスを望むユーザーがいて、そして同様にアクセスを望む攻撃者がいて、それはユーザーと区別するのが本当に難しいです。正確なシステムが必要ですが、100％正確なシステムなど存在しえないため、システムは最小権限から始まるゼロトラストの原則にも従わなければなりません。ユーザーを強力に認証し、不正を検知するために環境コンテキストを活用しなければなりません。私たちは、リソースのバラバラな活動に単一の一貫したポリシー・ビューを適用しなければなりません。そして、私たちのシステムが私たちが考えているとおりに動いていることを常に検証する必要があります。

@row
## Access Management as an Evolution

This body of knowledge will give you all sorts of data about the basic concepts that are deployed in an access management regime - but why do those mechanisms exist? They evolved in response to both business requirements and security threats. Administrators found themselves lacking in control and created best practices that made administration at scale easier and attacks at scale more difficult.

@column
## 進化するアクセス管理

このBody of Knowledgeでは、アクセス管理メカニズムで展開される基本概念に関するあらゆるデータを紹介しますが、どうしてこのようなメカニズムが存在するのでしょう？アクセス管理は、ビジネス上の要求とセキュリティ上の脅威の両方に対応するなかで進化してきました。管理者は、自分たちではコントロールしきれないことに気が付き、規模に応じた管理を容易にし、規模に応じた攻撃を困難にするベストプラクティスを生み出しました。

@row
### Password Proliferation Gave Us Directories

When businesses first began accumulating business programs within their private network, every new program required that user accounts be created and deleted. Every program asked each user to set a password. As businesses grew to have hundreds and thousands of programs, users hit the limit of how many usernames and passwords they could remember. Some programs let users choose their own usernames, and as a result, usernames varied wildly across programs. Many programs had wildly varying password policies. It was the wild west and from that wild west came the concept of “directories”. Instead of a hundred programs separately storing usernames and passwords, applications began to call out to an external directory of users, often using LDAP (Lightweight Directory Access Protocol). [^7] , [^8] Suddenly, users could use one password everywhere, and administrators didn’t have to maintain thousands of applications individually. All was well... for a while.

@column
### パスワードの急増がディレクトリを生み出した

企業がプライベートネットワーク内にビジネスプログラムを蓄積し始めた頃、新しいプログラムには必ずユーザーアカウントの作成と削除が必要でした。どのプログラムも、各ユーザーにパスワードの設定を要求しました。企業が何百、何千ものプログラムを持つように成長するとともに、ユーザーは数多のユーザー名とパスワードを覚えておける限界に達しました。一部のプログラムはユーザーが自身でユーザー名を選べるものもあり、その結果、ユーザー名はプログラムによって千差万別となりました。多くのプログラムでは、パスワードポリシーも千差万別でした。それは西部開拓時代とも言える状態であり、その時代から「ディレクトリ」という概念が生じました。100のプログラムが個別にユーザー名とパスワードを保存する代わりに、アプリケーションは、多くの場合ではLDAP（Lightweight Directory Access Protocol）を利用して、ユーザーの外部ディレクトリを呼び出すようになりました。 [^7] , [^8] 突然、ユーザーはどこでも1つのパスワードを使えるようになり、管理者は何千ものアプリケーションを個別に管理する必要がなくなりました。すべてが順調でした...しばらくの間は。

@row
### Password Fatigue Gave Us Web Access Management

The upside to user directories and LDAP was that users only had to remember one password. The downside was that even if all applications at the time were within the same network perimeter and were all LDAP-integrated, the user was still prompted for their password every time they used a new application - over the course of a day, that was a lot of typing. The resulting innovation was a new access management technique called “Web Access Management” (WAM). [^9] With web access management, users would authenticate once with their password, and then a (usually encrypted) domain-wide session cookie would be generated that could be read by multiple applications. Instead of performing an LDAP “bind,” the application could check that the user had a valid cookie. Around the same time, other technologies to address password fatigue developed, including Kerberos. [^10] These technologies finally give users some relief; a user could log in one time and access multiple applications. The concept of logging in once to access multiple apps has come to be known as ‘single sign-on’ (SSO).

@column
### パスワード入力疲れがウェブアクセス管理を生み出した

ユーザーディレクトリとLDAPの長所は、ユーザーが1つのパスワードを覚えていればいいということでした。欠点は、たとえ当時のすべてのアプリケーションが同じネットワーク境界内にあり、すべてLDAPに統合されていたとしても、ユーザーは新しいアプリケーションを使うたびにパスワードを入力するよう促されることでした。つまり、1日にするとかなりの入力回数になります。その結果、「ウェブアクセス管理」（WAM）と呼ばれる新しいアクセス管理手法が考案されました。 [^9] ウェブアクセス管理では、ユーザはパスワードで一度認証され、それから（通常は暗号化された）ドメイン全体のセッションクッキーが生成され、複数のアプリケーションによって読み取られます。LDAPの「バインド」を実行する代わりに、アプリケーションはユーザが有効なクッキーを持っていることを確認できます。同じ頃、Kerberosを含むパスワード疲れに対処するための他の技術が開発されました。 [^10] これらの技術により、ユーザーは一度ログインすれば複数のアプリケーションにアクセスできるようになり、ようやく落ち着きを得られるようになりました。ユーザーが一度ログインすれば複数のアプリケーションにアクセスできるというコンセプトは、「シングルサインオン」（SSO）として知られるようになりました。

@row
### Perimeter Limitations Gave Us Federation

As long as businesses were operating within their network perimeters, access management functions like Kerberos and WAM provided both convenience and security. But the Internet was opening up, and many companies wanted to begin allowing not only their employees to access resources, but also partners and customers. Businesses wanted to create trust relationships with other businesses and enable their users to access each other’s applications. This desire was met through a standard called SAML (Security Assertion Markup Language). [^11] Businesses pre-establish a trust “federation” between two domains and then request a secure introduction whenever a user attempts to access a resource. SAML and other federated identity specifications allowed businesses to retain control over the activities of their own users both in their own domains and across domains. Federated identity remains a backbone of access management, and SAML is still the gold standard for cross-domain access management.

@column
### 境界の限界がフェデレーションを生み出した

企業がネットワーク境界の中で業務をおこなっているかぎり、KerberosやWAMのようなアクセス管理機能は利便性とセキュリティの両方を提供していました。しかし、インターネットが開放され、多くの企業が従業員だけでなく、パートナーや顧客もリソースにアクセスできるようにしたいと考えるようになりました。企業は、他の企業と信頼関係を構築し、ユーザーがお互いのアプリケーションにアクセスできるようにしたいと考えていました。この要望は、SAML（Security Assertion Markup Language）と呼ばれる標準仕様によって満たされました。 [^11] 企業は2つのドメイン間でトラスト・「フェデレーション」を事前に確立し、ユーザがリソースにアクセスしようとするときは常に、セキュアな紹介を要求しました。。SAMLおよびその他のフェデレーション・アイデンティティの仕様によって、企業は自身のドメインと他社のドメインの両方で、自社ユーザーの活動を制御できるようになりました。フェデレーション・アイデンティティはは現在もアクセス管理のバックボーンであり、SAMLは現在もドメインをまたがるアクセス管理の優秀な標準仕様です。

@row
### Mobile & API Innovation Gave Us OAuth & Delegated Authorization Frameworks

Federation and SSO are what we call in the industry “user-present” scenarios. We can tell that the user is present in a federation request because the activity occurs using a browser, and browsers don’t have brains - they are ‘passive’ clients, and somebody has to be there to push the buttons and click the links. Around 2007, most business application delivery was focused on the browser - but the release of the first “smartphone” changed the game. Mobile applications could be downloaded from an app store and render data accessed from cloud APIs, just as cloud platforms were becoming popular. Suddenly an ‘active’ software client became a desirable way to talk to users.

Even as users got excited about the power of mobile applications, identity professionals ran into a problem: applications were calling APIs when users were not present, and even worse, many mobile applications wanted to consume and display data from cloud platforms that they were not affiliated to. If a mobile app wanted to access an unaffiliated cloud platform, the only answer was to ask the user for their password and then replay the password within every single API fetch. The result was something called the **password anti-pattern** : users got used to giving away their cloud platform passwords to any client that asked for it, and those clients had to cache user credentials on mobile devices so they could execute API calls in users’ absence.

SAML was not a perfect fit in a mobile context. XML parsers were not built into mobile platforms, and cryptographic requirements were heavy. The resulting access management paradigm was OAuth 1.0, a “delegated authorization framework” that could layer with federated protocols. OAuth addresses the ‘user not present’ scenario: applications ask for and receive an “access token” that does not introduce the user; instead, access tokens represent the ability to access a tightly scoped set data and services on behalf of a user.

Maybe access tokens don’t sound like such a big deal, but when you consider that you can pass access tokens to APIs instead of primary credentials, the results are significant. You prevent API endpoints from ever collecting or validating primary user credentials, thus removing multiple attack vectors around data leakage, man-in-the-middle-attacks, and rogue administrators harvesting credentials. Because the mechanism for authorizing the API is decoupled from the mechanism for authenticating users, the door opens to a world where a user could authenticate with factors other than a password without causing work for applications. Access tokens act as a stable currency that can be centrally architected and scalably deployed.

@column
### モバイル・アプリケーションとAPI呼び出しがOAuthと委譲型認可フレームワークを生み出した

フェデレーションとSSOは、私たちが業界で「ユーザーが存在する」シナリオと呼ぶものです。フェデレーション・リクエストでユーザーが存在するとわかるのは、ブラウザを使ってアクティビティが発生するからであり、ブラウザには脳がないためです。ブラウザは「受動的な」クライアントであり、ボタンを押したり、リンクをクリックするためにそこに誰かがいる必要があります。2007年頃、ほとんどのビジネスアプリケーションの配信はブラウザに集中していましたが、最初の「スマートフォン」のリリースがゲームチェンジをおこしました。ちょうどクラウドプラットフォームが普及し始めた頃で、モバイルアプリケーションはアプリストアからダウンロードし、クラウドAPIから取得したデータをレンダリングすることができました。突然、「能動的な」ソフトウェアクライアントが、ユーザーと会話する望ましい方法となりました。

ユーザーがモバイル・アプリケーションのパワーに興奮したとき、アイデンティティ専門家は問題に直面しました：ユーザーが存在しないときにアプリケーションはAPIを呼び出し、更に悪いことに多くのモバイル・アプリケーションは提携していないクラウドプラットフォームからデータを取得し、表示しようとしていました。モバイルアプリが提携していないクラウドプラットフォームにアクセスしたい場合、唯一の答えはユーザーにパスワードを尋ね、API呼び出しのたびにパスワードを再利用することでした。その結果、 **パスワードのアンチパターン** と呼ばれるものが生じました：ユーザーはクラウドプラットフォームのクライアントにパスワードを教えることに慣れてしまい、それらのクライアントはユーザーの不在時にAPI呼び出しを実行できるように、ユーザーの認証情報をモバイルデバイスにキャッシュしなければならなくなりました。

SAMLは、モバイルアプリのコンテキストに完全には適合していませんでした。XMLパーサはモバイル・プラットフォームに組み込まれておらず、暗号化要件は重かったのです。その結果、アクセス管理のパラダイムはフェデレーション・プロトコルとレイヤー化できる「委任型認可フレームワーク」であるOAuth 1.0となりました。OAuthは、「ユーザが存在しない」シナリオに対処します：アプリケーションは、ユーザを誘導しない「アクセストークン」を要求し、受け取ります。その代わりに、アクセストークンは、ユーザの代わりに、厳密にスコープされた一連のデータやサービスにアクセスする能力を表す。

アクセストークンはそれほど重大なものに思えないかもしれないが、プライマリー・クレデンシャルの代わりにアクセストークンをAPIにアクセスできるようにしていると考えると非常に重大です。APIエンドポイントがプライマリー・ユーザークレデンシャルを収集したり、検証したりすることを防ぐことで、データ漏洩、中間者攻撃やクレデンシャルを収集する悪意のある管理者といった複数の攻撃の糸口を排除できます。APIの認可のメカニズムはユーザー認証のメカニズムから分離されているため、アプリケーションに負担を強いることなく、パスワード以外の要素でユーザーを認証できる世界への扉が開かれます。アクセストークンは、一元的に設計され、スケーラブルに展開できる安定した通貨のように動作します。

@row
### Multi-Factor Authentication (MFA) Is and Was and Will be Again

Through all of the above antics and shenanigans, password attacks were haunting identity administrators. All sorts of conventions evolved to try to keep attackers out of accounts they didn’t own: we forced people to change their passwords regularly; we forced them to set longer and more complex passwords; we designed our LDAP directories and login forms to stop responding if too many incorrect attempts were made. Despite all these attempts to mitigate the risk, almost any password a human could set and remember without help is trivially attackable. If you doubt this statement, read “ [_Your Pa$$word doesn’t matter_](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/your-pa-word-doesn-t-matter/ba-p/731984) “ by Alex Weinert (@alex\_t\_weinert). [^12] Be prepared to weep.

The revelation that passwords are fundamentally flawed is not new - dating back to at least the ’70s, there has been research on how to get around the need for a human brain in the authentication process. [^13] , [^14] We developed the simple idea that passwords are “something you know,” but also described other options for validating a human’s ownership of a digital account could also include “something you have” or “something you are”. The idea is not that validating the thing you have can replace the thing you know, but rather that a combination of things you have, are, and know would require an attacker to compromise both digital and physical information. Today, the state of the art in multi-factor authentication is very sophisticated. A growing number of users protect their phone with a biometric, navigate an SMS message to confirm a transaction, or use an OTP (one-time password) to improve security without any need to understand the underlying principles.

We all know that MFA must continue to improve in usability to become ubiquitous. Specifications like FIDO2 are industry-changing for access management, not because the problem is solved - but because the problem is _**decoupled**_ \- FIDO2 (W3C WebAuthn and FIDO CTAP2) has separated the problem of negotiating cryptographic keys from the problem of requiring user gestures. [^15] The cryptographic key exchange can now stay reliable, while we focus on innovation - and possibly even revolution - in user interactions.

@column
### 多要素認証（MFA）は今も昔も、そしてこれからも続く

上記のような悪ふざけやいたずらのすべてを通じて、パスワード攻撃はアイデンティティ管理者を悩ませていました。攻撃者を自身のものではないアカウントから締め出すために様々な慣例が生まれてきました；パスワードを定期的に変更させたり、パスワードをより長く複雑なものに設定させたり、不正な試行が多すぎるときにはLDAPディレクトリやログインフォームがレスポンスを返さないようにしたりしました。リスクを軽減させるためのこれらの試みは、何の助けもなく人間が設定したり、記憶したりすることができないパスワードのほとんどは攻撃可能でした。この言葉を疑うのであれば、Alex Weinert (@alex\_t\_weinert)による「[_Your Pa$$word doesn’t matter_](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/your-pa-word-doesn-t-matter/ba-p/731984)・を読んでください。 [^12] 泣く準備をしましょう。

Today, the state of the art in multi-factor authentication is very sophisticated. A growing number of users protect their phone with a biometric, navigate an SMS message to confirm a transaction, or use an OTP (one-time password) to improve security without any need to understand the underlying principles.
パスワードに根本的な欠陥があることは今に始まったことではなく、少なくとも70年代には、認証プロセスにおける人間の脳の必要性を回避する方法についての研究がおこなわれていました。 [^13] , [^14] 私たちは、パスワードは「あなたが知っているもの」であるという単純な考えを発展させたが、デジタル・アカウントの人間の所有権を検証するための他の選択肢には、「あなたが持っているもの」や「あなたがあなたであること」も含まれると説明した。このアイデアは、「あなたが持っているもの」を検証することが「あなたが知っているもの」に取って代わるというものではなく、「あなたが持っているもの」「あなたがあなたであること」「あなたが知っているもの」を組み合わせることで、攻撃者はデジタル情報と物理情報の両方を侵害しなければなりません。今日、多要素認証の技術は非常に洗練されている。携帯電話を生体情報で保護したり、取引確認のためにSMSメッセージを誘導したり、セキュリティ向上のためにOTP（ワンタイムパスワード）を使用したりと、基本原理を理解していないユーザーが増加しています。

MFAがユビキタスになるためには、ユーザビリティを向上させ続けなければならないことは誰もが知っています。FIDO2のような仕様はアクセス管理の業界を変革しますが、それは問題が解決されたからではありません、問題が _**切り離された**_ からです。FIDO2 (W3C WebAuthnおよびFIDO CTAP2) は、暗号鍵の交換の問題とユーザージェスチャの問題を切り分けました。 [^15] 暗号鍵の交換は信頼性を維持したまま、ユーザーインタラクションの革新、そしておそらくは革命に集中することができます。

@row
### The Best Security is Invisible Security

In addition to the visible ceremonies we put in front of those who attempt access to resources, a lot is happening beneath the surface. We increasingly rely on context to supplement active user challenges in calculating the risk of any given transaction. Adjacent areas to identity are now critical stakeholders in our attempts to prevent identity fraud - Cloud Access Security Brokers (CASBs), [^16] Unified Endpoint Management (for example, Mobile Device Management or MDM), [^17] and EUBA (Entity and User Behavioral Analysis) [^18] fortify our access management regimes. Attackers have learned to defeat static access management processes, so we have evolved our defenses beyond password complexity: if you are not checking passwords against a rapidly updated set of banned strings including lists of newly known-to-be-breached passwords and augmenting this with real-time threat intelligence you are in serious trouble.

@column
### ベストなセキュリティは見えないセキュリティ

リソースにアクセスしようとする人たちの前で実行される目に見えるセレモニーに加え、水面下では多くのことが実行されています。ある取引のリスクを算出するさいに、アクティブユーザーの課題を追加するためにコンテキストにますます依存しています。アイデンティティに適応した領域は今やアイデンティティ詐欺を防止するための取り組みにおける重要なステークホルダーです。Cloud Access Security Brokers（CASBs）、 [^16] Unified Endpoint Management（例えばMobile Device ManagementやMDM）、 [^17] そしてEUBA（Entity and User Behavioral Analysis） [^18]は我々のアクセス管理体制を強化しています。攻撃者は静的なアクセス管理プロセスを打ち負かすことを学んだため、私たちはパスワードの複雑さを超えて防御を進化させています。新たに侵害されたパスワードの一覧を含む、迅速に更新される禁止文字列のセットとパスワードを照合し、リアルタイムの脅威インテリジェンスでこれを補強していない場合、深刻な問題が発生します。

@row
## And the Moral of the story is...

That brings us to now. Identity professionals today still struggle with all of the anecdotal issues listed here, but we have tools at our disposal and conventions on how to best deploy them. The better we can get as a profession at working together to eliminate fraud, detect abuse, and guide our users towards successful interactions, the better off everyone is. Everyone before you leveraged the work of their contemporaries to take a step forward. Now you have the opportunity to take the next step.

@column
## そして、この物語の教訓は...

そして現在に至ります。今日でもアイデンティティの専門家は、ここに挙げた逸話的な問題のすべてと闘っていますが、自由に使えるツールとツールをデプロイするベストな方法に関する慣習を持っています。不正行為を排除し、不正使用を検出し、ユーザーとのやり取りを成功に導くために、専門職として協力し合うことができればできるほど、すべての人がより良くなります。あなたの前の誰もが、同時代の人たちの仕事を活用して一歩を踏み出しました。今、あなたには次の一歩を踏み出すチャンスがあります。

@row
### What Will Access Management look like in the Future?

When we look back on today’s world of access management, what stories will be our contribution? There will be an assessment of our success in helping users to adopt multiple factors - did we succeed? Did we miss opportunities? As long as we are timid, a huge chunk of our immediate future will be spent mitigating attacks that we already _know_ are mostly preventable. Dragging your feet on MFA as an access management professional today is like catching up on social media when you know you have a report due (a behavior common enough to have its own name: akrasia) [^19] . After the fact, we will ask ourselves why we got in our own way, and there will likely be no good answer.

At some point, when enough administrators adopt MFA and eliminate the easy jackpots that are single-factor passwords, our industry will win this amazing prize:

**A whole new wave of inventive attacks!**

That may not sound so great, but it really is. Today, attackers can spend almost no money or time and still make a living from doing nothing fancier than running free phishing scripts from the Internet. A strongly authenticated world does not eliminate jackpots, but it does make the pool of criminals able to win those prizes a much more distinguished group. Attackers will move to post-authentication attacks like token theft and consent abuse. And the whole time, identity professionals and others will be making new things! Inventing better ways! Introducing resources and content that businesses want! We will embrace wearables as security devices, perform secure transactions even in hostile places, make the measure of least privilege even tighter. We will get better at tracking the promises that products make to us and better at punishing those who mess with our data. We will find a way to share private things and have true confidence that those private things will never become public. We will weather quantum meltdowns and new social networks, and it will all be a fight worth fighting.

The identity management professional who has read this far is clearly dedicated - and that is a great thing. We need the next generation of professionals to pick up the torch, question all assumptions, and push us into a future where risk is low, productivity is high, and new challenges keep our lives interesting.

@column
### アクセス管理は将来どうなっているか？

今日のアクセス管理の世界を振り返ったとき、私たちはどのようなストーリーに貢献でしょうか？ユーザーの多要素認証の導入支援の成功が評価されるでしょう。私たちは成功したのでしょうか？私たちは機会を逸したのでしょうか？私たちが臆病であるかぎり、目の前の未来の大部分は、既にほとんど防げると _知っている_ 攻撃の軽減に費やされるでしょう。今日、アクセス管理の専門家としてMFA導入の決定を遅らせることは、レポートの提出期限が迫っていることがわかっていながらソーシャルメディアを見るようなものです（一般的に「アクラシア（akrasia）」と呼ばれる一般的な行動） [^19] 。あとからなぜ自分たちのやり方で上手くいかなかったのか自問することになりますが、良い答えはでないでしょう。

ある時点で、充分な数の管理者がMFAを採用し、単要素パスワードのような安易な大当たりがなくなれば、私たちの業界はこの素晴らしい賞を獲得することになるでしょう：

**独創的な攻撃の全く新しい波！**

あまり聞こえが良くありませんが、本当にそうなのです。今日、攻撃者はお金も時間もほとんどかけずに、インターネットから無料のフィッシングスクリプトを実行するだけで、生計を立てることができます。高強度の認証が使われている世界では大当たりはなくならないが、大当たりを勝ち取ることができる犯罪者の集団はより目立つものとなります。攻撃者は、トークンの窃盗や同意の乱用など、認証後の攻撃に移行するでしょう。そしてその間にも、アイデンティティの専門家やその他の人々は新しいものを作り続けています！より良い方法を発明します！企業が求めるリソースやコンテンツを紹介します！私たちはウェアラブル・でバイスをセキュリティ・デバイスとして採用し、敵対的な場所でも安全な取引をおこない、最小限の権限という原則をより厳格なものにします。私たちは、製品が約束していることを追跡することにもっとうまくなり、私たちのデータに手を出した人たちを罰することにもっとうまくなるでしょう。私たちは、プライベートなものを共有し、そのプライベートなものが決して公開されることがないという真の信頼を得る方法を見つけるでしょう。私たちは量子のメルトダウンや新しいソーシャル・ネットワークを乗り切ります。

ここまで読んでくれたアイデンティティ管理の専門家は、明らかに献身的です。そして、私たちは、次世代の専門家たちが聖火を手にし、あらゆる前提を疑い、リスクが低く、生産性が高く、新たな挑戦が生活を面白くしてくれる未来へと押し進める必要があります。

@row
### Author Bio

<!-- ![A person wearing glasses and smiling at the camera Description automatically generated](/assets/images/idpro_bok/45-image1.jpeg) --> Pamela Dingle is a long-time member of the identity management world, and is a Director, running the identity standards team at Microsoft. The identity standards team works with standards bodies like W3C, IETF, and the OpenID Foundation on specifications like OAuth 2.0, FIDO, SCIM, and OpenID Connect, and Pamela works to ensure that customers, product groups, and the industry all understand the value of standards and other identity best practice patterns. Pamela spent eight years as an identity architect and eight years in the office of the CTO at Ping Identity and is a founder of Women in Identity.

- - -

[^1]:  Raible, Matt, “What the Heck is OAuth?” DZone Security Zone, 28 April 2018, [https://dzone.com/articles/what-the-heck-is-oauth](https://dzone.com/articles/what-the-heck-is-oauth) . 
    
[^2]:  Wikipedia contributors, "Federated identity," Wikipedia, The Free Encyclopedia, [https://en.wikipedia.org/w/index.php?title=Federated\_identity&oldid=949399706](https://en.wikipedia.org/w/index.php?title=Federated_identity&oldid=949399706) (accessed June 6, 2020). 
    
[^3]:  Wikipedia contributors, "Principle of least privilege," Wikipedia, The Free Encyclopedia, [https://en.wikipedia.org/w/index.php?title=Principle\_of\_least\_privilege&oldid=950981064](https://en.wikipedia.org/w/index.php?title=Principle_of_least_privilege&oldid=950981064) (accessed June 6, 2020). 
    
[^4]:  Rose, Scott, and Oliver Borchert, Stu Mitchell, Sean Connelly, “Zero Trust Architecture (2 nd Draft),” SP 800-207 (Draft), National Institute of Standards and Technology, February 2020, [https://csrc.nist.gov/publications/detail/sp/800-207/draft](https://csrc.nist.gov/publications/detail/sp/800-207/draft) . 
    
[^5]:  Paul A. Grassi, James L. Fenton, Elaine M. Newton, Ray A. Perlner, Andrew R. Regenscheid, William E. Burr, and Justin P. Richer. 2017. Digital identity guidelines - Authentication and Lifecycle Management. Technical Report. NIST Special Publication 800-63B. 
    
[^6]:  Graham Williamson and Corey Scholefield. Introduction to IAM Project Management for IAM Projects. IDPro Body of Knowledge, volume 1, issue 1, 31 March 2020. [https://bok.idpro.org/article/id/25/](https://bok.idpro.org/article/id/25/) . 
    
[^7]:  Wikipedia contributors, "Lightweight Directory Access Protocol," Wikipedia, The Free Encyclopedia, [https://en.wikipedia.org/w/index.php?title=Lightweight\_Directory\_Access\_Protocol&oldid=960496535](https://en.wikipedia.org/w/index.php?title=Lightweight_Directory_Access_Protocol&oldid=960496535) (accessed June 6, 2020). 
    
[^8]:  “The Most Complete History of Directory Services You Will Ever Find,” blog, Easy Identity, 13 April 2020, [https://idmdude.com/2012/04/13/the-most-complete-history-of-directory-services-you-will-ever-find/](https://idmdude.com/2012/04/13/the-most-complete-history-of-directory-services-you-will-ever-find/) (accessed June 12, 2020). 
    
[^9]:  Wikipedia contributors, "Web access management," Wikipedia, The Free Encyclopedia, [https://en.wikipedia.org/w/index.php?title=Web\_access\_management&oldid=959341667](https://en.wikipedia.org/w/index.php?title=Web_access_management&oldid=959341667) (accessed June 6, 2020). 
    
[^10]:  Wikipedia contributors, "Kerberos (protocol)," Wikipedia, The Free Encyclopedia, [https://en.wikipedia.org/w/index.php?title=Kerberos\_(protocol)&oldid=960957884](https://en.wikipedia.org/w/index.php?title=Kerberos_(protocol)&oldid=960957884) (accessed June 6, 2020). 
    
[^11]:  Wikipedia contributors, "Security Assertion Markup Language," Wikipedia, The Free Encyclopedia, [https://en.wikipedia.org/w/index.php?title=Security\_Assertion\_Markup\_Language&oldid=956779073](https://en.wikipedia.org/w/index.php?title=Security_Assertion_Markup_Language&oldid=956779073) (accessed June 6, 2020). 
    
[^12]:  Weinert, Alex, “Your Pa$$word doesn’t matter,” Azure Active Directory Identity Blog, Microsoft Corporation, 9 July 2019, [https://techcommunity.microsoft.com/t5/azure-active-directory-identity/your-pa-word-doesn-t-matter/ba-p/731984](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/your-pa-word-doesn-t-matter/ba-p/731984) . 
    
[^13]:  Morris, Robert, and Ken Thompson. "Password security: A case history." Communications of the ACM 22.11 (1979): 594-597. 
    
[^14]:  Feldmeier D.C., Karn P.R. (1990) UNIX Password Security - Ten Years Later. In: Brassard G. (eds) Advances in Cryptology — CRYPTO’ 89 Proceedings. CRYPTO 1989. Lecture Notes in Computer Science, vol 435. Springer, New York, NY 
    
[^15]:  “FIDO2:WebAuthn & CTAP,” FIDO Alliance, [https://fidoalliance.org/fido2/](https://fidoalliance.org/fido2/) . 
    
[^16]:  Wikipedia contributors, "Cloud access security broker," Wikipedia, The Free Encyclopedia, [https://en.wikipedia.org/w/index.php?title=Cloud\_access\_security\_broker&oldid=949494699](https://en.wikipedia.org/w/index.php?title=Cloud_access_security_broker&oldid=949494699) (accessed June 6, 2020). 
    
[^17]:  Raam, Giridhara, “The What, Why, and How of Unified Endpoint Management,” Integration Zone, DZone, 8 July 2019, [https://dzone.com/articles/the-what-why-and-how-of-unified-endpoint-managemen](https://dzone.com/articles/the-what-why-and-how-of-unified-endpoint-managemen) . 
    
[^18]:  Petters, Jeff, “What is UEBA? Complete Guide to User and Entity Behavior Analytics,” Inside Out Security Blog, Varonis, 29 March 2020. https://www.varonis.com/blog/user-entity-behavior-analytics-ueba/ 
    
[^19]:  Clear, James, “The Akrasia Effect: Why We Don’t Follow Through on What We Set Out to Do and What to Do About It,” excerpt from [Atomic Habits](https://jamesclear.com/atomic-habits) , [https://jamesclear.com/akrasia](https://jamesclear.com/akrasia) (accessed June 6, 2020). 
