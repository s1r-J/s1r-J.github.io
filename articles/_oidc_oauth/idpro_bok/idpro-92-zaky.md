---
layout: columns
title: Multi-factor Authentication
permalink: /docs/oidc_oauth/idpro_bok/92
date: 2024-09-09
modify_date: 2024-11-29
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "FIDO", "MFA", "多要素認証", "TOTP", "FIDO U2F", "WebAuthn", "フィッシング"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/92/](https://bok.idpro.org/article/id/92/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

Multi-factor authentication (MFA) is critical in securing account access and guarding against account takeover. In this article, we explain the core concepts that define MFA, explore the characteristics of different MFA types, and discuss the various threats mitigated by using MFA.

Keywords: credentials, FIDO, Google Authenticator, IAM, MFA, multi-factor authentication, Security, Security Blog, totp, u2f, WebAuthn, YubiKey, Identity and Access Management, TOTP, U2F, passwords, phishing, authentication

@column
## 概要

多要素認証（MFA）は、アカウントアクセスを保護し、アカウント乗っ取りを防ぐために重要です。本記事では、MFAを定義するコアコンセプトについて説明し、様々な種類のMFAの特徴について探り、MFAを利用することで軽減できる様々な脅威について議論します。

Keywords: クレデンシャル, FIDO, Google Authenticator, IAM, MFA, 多要素認証, セキュリティ, セキュリティブログ, totp, u2f, WebAuthn, YubiKey, アイデンティティとアクセス管理, TOTP, U2F, パスワード, フィッシング, 認証

@row
By Dean H. Saxe (Amazon) and Khaled Zaky (Amazon)

© 2022 IDPro, Dean H. Saxe, Khaled Zaky

@row
## Introduction

This article describes multi-factor authentication (MFA), a key component in securing account access and guarding against account takeover. Organizations and individuals typically have multiple types of MFA and several strategies for implementing its use. Not all MFA offers the same level of security, and some types of MFA are generally not recommended.

@column
## イントロダクション

この記事では、アカウントへのアクセスを保護し、アカウントの乗っ取りを防ぐために重要なコンポーネントである多要素認証（MFA）について説明しています。一般的に、組織および個人には複数の種類のMFAおよびその利用を実装するためのいくつかの方法が存在しています。すべてのMFAが同じセキュリティレベルを有しているわけではなく、一般的に推奨されないMFAもあります。

@row
### Terminology

_Many of these terms have been sourced from “Terminology in the IDPro Body of Knowledge.”_ [^1]

| Term | Definition |
| --- | --- |
| Authentication | Authentication is the process of proving that the user with a digital identity who is requesting access is the rightful owner of that identity. Depending on the use case, an ‘identity’ may represent a human or a non-human entity; may be either individual or organizational; and may be verified in the real world to varying degrees, including not at all. |
| Authorization | Determining a user’s rights to access functionality with a computer application and the level at which that access should be granted. In most cases, an ‘authority’ defines and grants access, but in some cases, access is granted because of inherent rights (like patient access to their own medical data). Authorization is evaluating what access or rights an identity should have in an environment. |
| Identity and Access Management | Identity and Access Management (IAM) is the discipline used to ensure the correct access is defined for the correct users to the correct resources for the correct reasons. |
| Identity Provider | An Identity Provider (IdP) performs a service that sends information about a user to an application. This information is typically held in a user store, so an identity provider will often take that information and transform it to be able to be passed to the service providers, AKA apps. The OASIS organization, responsible for the SAML specifications, defines an IdP as “A kind of SP that creates, maintains, and manages identity information for principals and provides principal authentication to other SPs within a federation, such as with web browser profiles.” |
| Multi-Factor Authentication (MFA) | An approach whereby a user’s identity is validated to the trust level required according to a security policy for a resource being accessed using more than one factor (something you know (e.g., password), something you have (e.g., smartphone), something you are (e.g., fingerprint). |
| MFA Prompt Bombing | Also known as MFA fatigue, MFA prompt bombing is a cyber-attack technique that describes when an attacker bombards a user with mobile-based push notifications, which sometimes leads to the user to approve the request out of annoyance which might lead to an account takeover. |

@column
### 用語解説

_以下の用語の多くは「Terminology in the IDPro Body of Knowledge」をソースとしています。_ [^1]

| 用語 | 定義 |
| --- | --- |
| 認証 | 認証は、アクセスを要求しているデジタルアイデンティティを持つユーザーがそのアイデンティティの正当な所有者であることを証明するプロセスです。ユースケースに依存しますが、「アイデンティティ」は人間もしくは非人間のエンティティを表す場合があります；個人や組織のいずれかの場合もあります；また、現実世界で様々な程度の検証をされることや全く検証されない場合もあります。 |
| 認可 | コンピュータアプリケーションの機能にアクセスするユーザーの権利と、付与されるべきアクセス権のレベルを決定すること。ほとんどのケースでは、「権威あるもの」が決定をおこない、アクセス権を付与しますが、一部のケースでは生得権によってアクセス権が付与されます（患者が自身の医療で0他にアクセスするようなケース）。認可は、ある環境でどのようなアクセスや権利をアイデンティティが有するべきかを評価することです。 |
| アイデンティティとアクセス管理 | アイデンティティとアクセス管理（IAM）は、適切なユーザーが適切な理由によって適切なリソースへ適切にアクセスできるようにするための規律です。 |
| アイデンティティプロバイダー | アイデンティティプロバイダー（IdP）はアプリケーションにユーザーについての情報を送信するサービスを実行します。この情報は一般的にユーザーストアに保持されるため、アイデンティティプロバイダーは多くの場合、その情報を取得し、サービスプロバイダー（別名としてはアプリ）に提供できるように変換します。SAML標準仕様を管轄するOASISはIdPを、「SPの一種であり、プリンシパルのアイデンティティ情報の作成、メンテナンス、管理をおこない、プリンシパルの認証をWebブラウザのプロファイルなどを利用したフェデレーションによって他のSPに提供するもの」と定義しています。 |
| 多要素認証（MFA） | 1つ以上の要素（知っているもの（例、パスワード）、持っているもの（例、スマートフォン）、その人であるもの（例、指紋））を使うことで、アクセスされるリソースのセキュリティポリシーが要求する信頼レベルでユーザーのアイデンティティを検証するアプローチ。 |
| MFAプロンプト爆弾 | MFA消耗としても知られるMFAプロンプト爆弾は、攻撃者がユーザーにモバイルベースのプッシュ通知を浴びせかけるサイバー攻撃技術であり、時折ユーザーが煩わしさを回避するためにリクエスをを承認してしまい、アカウントの乗っ取りにつながることもあります。 |

@row
## What is Multi-factor Authentication?

MFA is an authentication mechanism that requires a user logging into an application or an online account to present two or more factors to sign in and complete their authentication flow. Traditionally this would have been just a username and a password combination or another form of single-factor authentication, such as fingerprint biometrics. Adding multiple factors reduces the likelihood of bad actors gaining unauthorized access in case any of the factors are compromised. For example, single factors, such as passwords (which are subject to reuse and compromise), are one of the most common ways malicious actors can gain unauthorized access to your accounts, data, and online assets. Adding additional factors reduces the risk of account compromise and raises authentication assurance. Check out the [NIST](https://pages.nist.gov/800-63-3/sp800-63b.html) 800-63-B, which provides recommendations on types of authentication processes, authenticator types, and various assurance levels. [^2]

There are three types of MFA factors:

*   The _knowledge_ factor is _something you know_ . This factor could be something like a password or a PIN code.
    
*   The _possession_ factor is _something you have_ . This factor could be something like a USB key, a smartphone, or an access card.
    

@column
## 多要素認証とは？

MFAは、アプリケーションまたはオンライン・アカウントにログインするユーザがサインインをおこない、認証フローを完了するために。2つ以上の要素を提示することを要求する認証メカニズムです。従来はユーザー名とパスワードの組み合わせや指紋生体認証のような単要素認証が利用されてきました。多要素を追加することは、いずれかの要素が侵害されたとき、攻撃者が認可されていないアクセス権を取得する可能性を低下させます。例えば、パスワード（再利用していたり、侵害されていたりする可能性がある）のように単要素は、悪意のある攻撃者がアカウント、データおよびオンライン資産への認可されていないアクセス権を取得する最も一般的な方法のひとつです。要素を追加することは、アカウント侵害のリスクを低減し、認証保証を向上させます。[NIST](https://pages.nist.gov/800-63-3/sp800-63b.html) 800-63-Bでは、認証プロセスの種類、認証器の種類および様々な保証レベルについて推奨情報を提供しています。 [^2]

MFAの要素は3種類あります：

*   _知識_ 要素は、 _知っているもの_ です。この要素はパスワードやPINコードのようなものを指します。
    
*   _所持_ 要素は _持っているもの_ です。この要素はUSBキー、スマートフォンやアクセスカードなどを指します。
    

@row
![](/assets/images/idpro_bok/92-image1.png)

@row
*   The _inherence_ factor is _something you are_ . This factor could be a biometric, like facial recognition, fingerprint, or voice recognition.
    

What is the Difference between MFA and 2FA?  
Two-factor authentication, or 2FA, is an identity and access management authentication method that requires exactly two factors of identification to gain access.  It is worth mentioning that 2FA is sometimes referred to as two-step verification or 2SV in some online services. 2FA is usually used interchangeably with MFA. However, in the case of MFA, more than two factors can be required,  such as a combination of password + one-time password (OTP) + on a device with mobile device management (MDM). Therefore, 2FA is a subset of MFA.

@column
*   _生体_ 要素は、 _本人であること_ です。この要素は顔識別、指紋や声紋識別のような生体情報を指します。
    

MFAと2FAの違いは何でしょうか？
二要素認証、つまり2FAはアクセス権を取得するために正確に2つの識別の要素を必要するアイデンティティとアクセス管理の認証方法です。一部のオンラインサービスでは、時々2FAのことを二段階認証もしくは2SVと呼ばれることがあります。大抵の場合、2FAはMFAと言い換えることができます。しかし、MFAの場合、2要素よりも多くの要素が要求されことがあります。例えばパスワード、ワンタイムパスワード（OTP）とデバイス上のモバイルデバイス管理（MDM）が要求されることがあります。つまり、2FAはMFAのサブセットということです。

@row
### History of Multi-factor Authentication

How did the industry come to embrace MFA?  Although the original ideas and patents are up for debate, we can say that the concept of MFA was first commonly used with automated teller machines (ATMs, cash machines).  First introduced in [Europe in 1967](https://www.theatlantic.com/technology/archive/2015/03/a-brief-history-of-the-atm/388547/) , ATMs required a physical card containing information encoded on the magnetic stripe as the possession factor (something I have) and a PIN (something I know) to conduct bank transactions. [^3]

> The breakthrough in security was the idea that a public number (PAN) was to be combined with a private identification number (PIN). The PAN was printed in punched holes on the card and of course, could be forged. It would be secured through the use of a PIN that would correspond to the PAN through a complex coding system. The key was that such system should be of sufficient strength to prevent anyone getting to the PIN from the PAN. Chubb tested the system by printing off 1001 cards and attempting to break this system. They failed and Goodfellow’s system became the basis of the security system in the ‘Chubb MD2’ cash dispenser. Goodfellow’s patent was filed on May 2, 1966 (GB1197183). [^4]

In 1987, RSA introduced the first hardware key fob, enabling the use of one-time passwords (OTPs) as an authentication factor.  These hardware key fobs are still in use today and sold by numerous vendors using both Time-based One Time Passwords (TOTP, see [RFC6238](https://www.rfc-editor.org/rfc/rfc6238) ) [^5] and HMAC-Based One Time Passwords (HOTP, see [RFC4226](https://www.rfc-editor.org/rfc/rfc4226) ). [^6]

By the early 2000s, MFA solutions began to see a broad rollout in enterprise, government, and consumer use cases.  In 2004 the [United States Homeland Security Program Directive 12 (HSPD-12)](https://www.dhs.gov/homeland-security-presidential-directive-12) was signed by President George W. Bush.

> “US policy is to enhance security, increase Government efficiency, reduce identity fraud, and protect personal privacy by establishing a mandatory, Government-wide standard for secure and reliable forms of identification issued by the Federal Government to its employees and contractors (including contractor employees). This directive mandates a federal standard for secure and reliable forms of identification.” [^7]

In response to HSPD-12, the US Federal Government, through the National Institute of Standards and Technology (NIST), released [FIPS-201-1](https://csrc.nist.gov/CSRC/media/Publications/fips/201/1/archive/2006-06-23/documents/FIPS-201-1-chng1.pdf) , specifying the requirements for Personal Identity Verification (PIV) for US Federal Government employees and contractors. [^8] [NIST Special Publication 800-73-1](https://csrc.nist.gov/publications/detail/sp/800-73/1/archive/2006-03-15) \[xi\] , released in March 2006, “specifies the PIV data model, Application Programming Interface (API), and card interface requirements necessary \[...\] for interoperability across deployments or agencies. Interoperability is defined as the use of PIV identity credentials such that client-application programs, compliant card applications, and compliant integrated circuit cards (ICC) can be used interchangeably by all information processing systems across Federal agencies.” [^9]

In December 2004, the US Federal Deposit Insurance Corporation (FDIC) released the paper “ [Putting an End to Account-Hijacking Identity Theft,](https://www.ojp.gov/ncjrs/virtual-library/abstracts/putting-end-account-hijacking-identity-theft) ” which concluded with the recommendation for “upgrading existing password-based single-factor customer authentication systems to two-factor authentication.” [^10] Shortly after that, in 2005, the Federal Financial Institutions Examination Council released guidance for the US banking industry entitled “ [Authentication in an Internet Banking Environment,](https://www.ffiec.gov/pdf/authentication_guidance.pdf) ” which stated, “The agencies consider single-factor authentication, as the only control mechanism, to be inadequate for high-risk transactions involving access to customer information or the movement of funds to other parties. Financial institutions offering Internet-based products and services to their customers should use effective methods to authenticate the identity of customers using those products and services.” [^11] The requirements were not compulsory.  In 2011, the RAND Corporation noted:

> The financial sector is potentially the most varied in its implementation practices. Despite regulations (more like “guidelines”) that require financial institutions to protect certain data to a certain minimum level and indicate that MFA meets these criteria, organizations in this sector make network access decisions internally. [^12]

These changes did not arrive without debates about their value and consumer concerns about using MFA. [^13] First deployed in Nigeria in 2005 by Neticash, SMS OTP was broadly adopted in the 2010s.  At the same time, consumer use of OTPs became more common with readily available authenticator apps, such as Google Authenticator, becoming available for various smartphone devices.

The FIDO Alliance was [founded](https://fidoalliance.org/overview/history/) in 2012 to develop a password-less authentication protocol and later, an open, second-factor protocol. [^14] The World Wide Web Consortium (W3C) released the first WebAuthn specification in conjunction with FIDO Alliance Client to Authenticator Protocol (CTAP) in March 2019, enabling FIDO2 as a phishing-resistant authentication protocol across platforms, browsers, and devices. [^15] With the public release of passkeys by the FIDO Alliance, W3C, and commercial partners in 2022, the tools for strong, highly phishing-resistant authentication already exist in many consumer and enterprise devices such as laptops, tablets, and phones. [^16]

Bruce Schneier wrote in 2005, “Two-factor authentication isn’t our savior. It won’t defend against phishing. It’s not going to prevent identity theft. It’s not going to secure online accounts from fraudulent transactions. It solves the security problems we had ten years ago, not the security problems we have today.” [^17] Schneier’s blog post was prescient.  Even after the broad rollout of MFA mechanisms starting in 2005, we are still fighting against phishing, fraud, and identity theft in the 2020s.  As the industry has adapted to these ills, malicious actors have also adapted their mechanisms.  As we close the front door with better technology, what new paths will actors take to achieve their nefarious goals?

@column
### 多要素認証の歴史

業界がどのようにMFAを取り入れるようになったのでしょうか？オリジナルのアイデアと特許は議論の余地がありますが、MFAの概念が最初に一般的に使われるようになったのは現金自動預払機（ATM、キャッシュマシーン）と言うことができるでしょう。ATMは最初に[1967年にヨーロッパ](https://www.theatlantic.com/technology/archive/2015/03/a-brief-history-of-the-atm/388547/)で導入され、磁気ストライプにエンコードされた情報を持つ物理的なカードを所持要素（持ってるもの）と銀行取引を実行するためのPIN（知っているもの）を要求します。 [^3]

> セキュリティにおけるブレークスルーは、公開番号（PAN）をプライベート識別番号（PIN）と組み合わせるというアイデアでした。PANはカードにパンチホールとして印刷され、もちろん偽造される可能性がありました。複雑なコーディング体系を利用したPANに対応したPINを使うことでセキュアにすることができました。PANからPINを取得することを避けるため、そのような体系が充分な強度を持つことが重要でした。Chubbは体系をテストするため、1001枚のカードを印刷し、解読を試みました。解読には失敗し、Goodfellowの体系は「Chubb MD2」現金自動引出機のセキュリティシステムの基礎となりました（GB1197183）。 [^4]

1987年、RSAはワンタイムパスワード（OTP）の利用を可能にする最初のハードウェア・キーフォブを売り出しました。これらハードウェア・キーフォブは今日でも使われており、多彩なベンダーから販売されており、時間ベースワンタイムパスワード（TOTP、[RFC6238](https://www.rfc-editor.org/rfc/rfc6238)参照） [^5] とHMACベースワンタイムパスワード（HOTP、[RFC4226](https://www.rfc-editor.org/rfc/rfc4226)参照）の両方を利用することができます。 [^6]

2000年代初頭、MFAが企業、政府そして消費の様々なユースケースで幅広く使われるようになりました。2004年には、George W. Bush大統領によって[United States Homeland Security Program Directive 12 (HSPD-12)](https://www.dhs.gov/homeland-security-presidential-directive-12)が署名されました。

> 「米国の方針は、連邦政府がその職員や業務委託者（業務委託職員を含む）に発行するセキュアで信頼できる身分証明の形式に対して強制的な政府全体の基準を確立することで、セキュリティを強化し、政府の効率性を高め、アイデンティティ詐欺を減らして個人のプライバシーを保護することです。この指令はセキュアで信頼できる身分証明の形式の連邦基準を義務付けるものです。」 [^7]

HSPD-12に対応して、米国連邦政府は、米国国立標準技術研究所（NIST）を通じて、連邦職員および契約業者の個人特定証明（PIV）の要件を定める[FIPS-201-1](https://csrc.nist.gov/CSRC/media/Publications/fips/201/1/archive/2006-06-23/documents/FIPS-201-1-chng1.pdf)を発表しました。 [^8] 2006年3月に発表された[NIST Special Publication 800-73-1](https://csrc.nist.gov/publications/detail/sp/800-73/1/archive/2006-03-15) \[xi\] では、「デプロイまたは機関をまたいだ相互運用性のため、 \[...\] PIVデータモデル、アプリケーションプログラミングインタフェース（API）および券面インタフェース要件を規定します。相互運用性は、クライアントアプリケーションプログラム、準拠カードアプリケーションおよび準拠集積回路カード（ICC）が連邦機関間の全ての情報処理システムによって相互に利用できるのようなPIVアイデンティティクレデンシャルの利用と定義されています。」 [^9]

2004年12月、米国連邦預金保険公社（FDIC）は「[Putting an End to Account-Hijacking Identity Theft](https://www.ojp.gov/ncjrs/virtual-library/abstracts/putting-end-account-hijacking-identity-theft)」という論文を発表し、「既存のパスワードベースの単一要素の顧客認証システムから2要素認証にアップグレードすること」を推奨するという結論を出した。 [^10] その直後である2005年、連邦金融機関検査協議会は、「[Authentication in an Internet Banking Environment](https://www.ffiec.gov/pdf/authentication_guidance.pdf)」という米国の銀行業界向けのガイドラインを公開し、「当局は、単一の制御メカニズムとして、単要素認証は顧客情報へのアクセスや他の当事者への資金移動のような高リスクな取引には不十分であると考えています。インターネットベースの製品やサービスを顧客に提供する金融機関は、それら製品およびサービスを利用する顧客のアイデンティティを認証するために効果的な手法を用いるべきです。」と述べました。 [^11] この要件は強制ではありませんでした。2011年、ランド研究所は以下のように指摘しました：

> 金融セクターはその実施方法において最も多様である可能性があります。規制（というよりも「ガイドライン」に近い）は、金融機関に対し、特定のデータを一定の最低レベルで保護し、MFAがその基準を満たしていることを示すこと要求していますが、このセクターの組織は内部でネットワークアクセスに関する決定をしている。 [^12]

これらの変化は、その価値についての議論やMFAの使用について消費者の懸念をなしにもたらされたわけではありませんでした。 [^13] 2005年、ナイジェリアでNeticash車によって初めてデプロイされたSMS OTPは2010年代に広く受け入れられました。同時に、消費者のOTP利用は、様々なスマートフォンデバイスで利用できるようになったGoogle Authenticatorなどの容易に利用できる認証アプリによって、より一般的になりました。

FIDOアライアンスは、パスワードレス認証プロトコルを開発するために2012年に[設立](https://fidoalliance.org/overview/history/)され、その後、オープンな2要素プロトコルを開発しました。 [^14] World Wide Web Consortium（W3C）は、2019年3月FIDOアライアンスのClient to Authenticator Protocol（CTAP）と連携した最初のWebAuthn仕様書をリリースし、FIDO2をプラットフォーム、ブラウザとデバイスを横断するフィッシング耐性のある認証プロトコルにしました。 [^15] 2022年、FIDOアライアンス、W3Cおよび商業パートナーによってパスキーが一般公開されると、強力でフィッシング耐性の高い認証のためのツールが、ノートパソコンやタブレット、携帯電話など消費者および企業のデバイスに既に存在しています。 [^16]

2005年Bruce Schneier氏は、「2要素認証は救世主ではありません。2FAはフィッシングを防ぐことができません。アイデンティティ窃盗を防ぐことができません。オンラインアカウントを不正取引から守ることもできません。10年前のセキュリティ問題を解決しますが、今日のセキュリティ問題を解決するものではありません。」と書きました。 [^17] Schneier氏のブログ記事は先見の明がありました。2005年に始まったMFAメカニズムが広く展開された後でさえ、2020年代においてもまだフィッシング、詐欺そしてアイデンティティ窃盗と戦っています。業界はこれらの悪に適応するにつれて、悪意のあるアクターもこれらのメカニズムに対応してきました。より優れたテクノロジーによって玄関を閉じるとき、悪意のあるアクターはどのような新しい経路によって悪意のある目標を達成するのでしょうか？

@row
### Why Choose Multi-factor Authentication?

The key benefit of adopting MFA is that it improves individuals' and enterprises' security posture and delivers a higher level of assurance to guard against unauthorized account access. With MFA enforced, users are required to authenticate by presenting multiple factors, for example, a username, password, and fingerprint from their device. These additional factors reduce the risk of unauthorized access when one of the authentication factors is compromised, such as a leaked password through a third-party data breach or a phishing attack. You can think of every factor added as an additional lock as an access security layer to prevent unauthorized users from breaking in.

@column
### なぜ多要素認証を選ぶのでしょうか？

MFAを採用する重要な利益は、それが個人および企業のセキュリティ姿勢を改善し、認可されていないアカウントアクセスから保護するために高い保証レベルを提供することです。MFAが採用されると、ユーザーは複数の要素、例えばユーザー名、パスワードおよびデバイスからの指紋、を提示することによる認証が必須となります。これらの追加要素は、サードパーティーのデータ流出やフィッシング攻撃を通じてパスワードがリークしたような認証要素の1つが侵害されたとき、認可されていないアクセスのリスクを減らします。追加のロックとして追加される全ての要素は、認可されていないユーザーの侵入を防ぐアクセスセキュリティレイヤーとして考えることができます。

@row
### The Problem with Single-Factor Authentication

Single-factor authentication is when access is provided when a user presents one factor. This presentation could be in the form of a password, access card, or fingerprint biometric. The most common single-factor authentication mechanism is the password. Password-less mechanisms, such as passkeys, designed to replace passwords as an authentication factor, are expected to see broad consumer rollout after their introduction in 2022.

However, passwords are still the most widely used mechanism to authenticate to various online services. Passwords are vulnerable to various attack techniques commonly used by attackers to gain access to online accounts. Here are some examples of those techniques:

*   **Identity Theft:** This is when an attacker illegally acquires personal information such as date of birth, credit card details, or even answers to security questions that could be used for password guessing or resets.
    
*   **Phishing:** This is when an attacker falsely presents themselves as a trusted party through fraudulent emails, websites, or pop-ups, hoping that they collect someone’s personal information, such as username/password.
    
*   **Brute force:** This involves an attacker guessing username and password combinations in hopes that they would eventually gain unauthorized access to an account
    
*   **Credential Stuffing:** This is when an attacker uses a list of known compromised passwords to take over someone’s account.
    
*   **Key-logging:** This requires an attacker to compromise the end-point like a public computer where they would have installed a key-logger to monitor and record actual keystrokes for personal information such as login information and credit cards.
    
*   **Man in the middle:** An attacker could use URLs that closely resemble the intended website. This deceptive URL is then used to direct the user to a reverse proxy server used by the attacker to intercept the communication between the user and the intended website in order to steal sensitive data, such as a user’s password.
    

The introduction of passkeys presents an interesting dilemma: Are passkeys an MFA mechanism when they are syncable across cloud services? What about when they are resident on a single device? If passkeys are primarily designed as a single authentication factor to replace passwords, will we see passkeys deployed with additional factors? With varying security models depending on where the passkeys are generated and how they are stored, synced, and shared, we believe it is likely that some passkey implementations will require additional authentication factors. For additional passkey considerations, see the FIDO section below.

@column
### 単要素認証の問題

単要素認証は、ユーザーが1つの要素を提示したとき、アクセスが提供される方式です。この提示は、パスワード、アクセスカードまたは指紋のような形式です。最も一般的な単要素認証のメカニズムはパスワードです。パスキーのような、認証要素としてパスワードに取って代わるために設計されたパスワードレスメカニズムは、2022年の導入後に消費者に広く展開されると予想されています。

しかし、パスワードは様々なオンラインサービスへの認証において未だに最も広く利用されているメカニズムです。パスワードは、オンラインアカウントへのアクセス権を得るために攻撃者によって一般的に利用される様々な攻撃手法に対して脆弱です。ここではそれらの手法の一部を示します：

*   **アイデンティティ窃盗**：攻撃者が違法に誕生日、クレジットカード情報や、パスワード推測やリセットのために利用されるセキュリティ質問への回答のような個人情報を取得する手法。
    
*   **フィッシング**：攻撃者が、詐欺メール、ウェブサイトやポップアップを通じて信頼できる当事者として不正な表示をおこない、ユーザー／パスワードのような誰かの個人情報を収集する手法。
    
*   **ブルートフォース**：攻撃者がユーザー名とパスワードの組み合わせを推測し、最終的にアカウントへの認可されていないアクセスを取得します。
    
*   **クレデンシャルスタッフィング**：攻撃者が、アカウントを乗っ取るために既知の侵害されたパスワードのリストを使用する手法。
    
*   **キーロギング**：この手法では、攻撃者が公共のコンピューターなどのエンドポイントを侵害し、キーロガーをインストールして、ログイン情報やクレジットカードなどの個人情報の実際のキー入力を監視および記録することを必要とします。
    
*   **マン・イン・ザ・ミドル**：攻撃者は、意図したウェブサイトに酷似したURLを使用することができます。この欺瞞的なURLは、ユーザーのパスワードなどの機密データを盗むため、ユーザーと意図したウェブサイトとの間の通信を傍受するように攻撃者が使用するリバースプロキシサーバーにユーザーを誘導するために使用されます。
    
パスキーの導入は、興味深いジレンマを提供します：パスキーは、クラウドサービスを介して同期できる場合にMFAメカニズムでしょうか？単一デバイスに閉じ込めている場合はどうでしょうか？パスキーがパスワードを置換する単一認証要素として主に設計されている場合、パスキーが追加要素とともにデプロイされることはあるでしょうか？パスキーが生成された場所や保管、同期、共有される方法に依存して様々なセキュリティモデルがあり、一部のパスキー実装が追加認証要素を必要になる可能性が高いと考えています。パスキーに関する追加の考慮事項については、以下のFIDOのセクションを参照してください。

@row
## Multi-factor Authentication Mechanisms

@column
## 多要素認証メカニズム

@row
### Grid Cards & Grid-Based Mechanism

_**Possession Factor:**_ Card

_**Knowledge Factor:**_ Password

_**Inherence Factor:**_ None

_**Phishing Resistance:**_ None

A form of a challenge-response protocol, a unique grid with named columns and rows is printed on card stock, a plastic card (e.g., student ID), etc. [^18] At each set of coordinates is a cell containing an alphanumeric value.  Upon first factor authentication with a password, the user is presented with a dynamic challenge requiring entry of the values at multiple coordinates on the grid as a second factor.

@column
### グリッドカードとグリッドベースメカニズム

_**所有要素**_ ：カード

_**知識要素**_ ：パスワード

_**生体要素**_ ：なし

_**フィッシング耐性**_ ：なし

チャレンジレスポンスプロトコルの一種であり、名前がつけられた列と行をもつユニークなグリッドがカード用紙やプラスチックカード（学生証など）などに印刷されています。 [^18] 各座標は英数字の値を持つセルです。パスワードによって最初の要素による認証をおこない、ユーザーは2つ目の要素として、グリッド上の複数の座標の値の入力を要求されるダイナミックチャレンジが提示されます。

@row
### Credential Calculators Hardware Token

_**Possession Factor:**_ Credential Calculator

_**Knowledge Factor:**_ Password

_**Inherence Factor:**_ None

_**Phishing Resistance:**_ None

In another form of challenge-response protocol, users authenticate to a service with a password and receive a numeric challenge.  This challenge is entered into the device using a keyboard, and the response is calculated.  The user enters the output into the service to complete the authentication process.

@column
### クレデンシャル計算機ハードウェアトークン

_**所有要素**_ ：クレデンシャル計算機

_**知識要素**_ ：パスワード

_**生体要素**_ ：なし

_**フィッシング耐性**_ ：なし

チャレンジレスポンスプロトコルの別形式では、ユーザーはパスワードによってサービスに対して認証をおこない、数字のチャンレジを受け取ります。このチャンレンジはキーボードを使ってデバイスに入力され、レスポンスが計算されます。ユーザーはその出力をサービスに入力し、認証処理が完了します。

@row
### One-Time Passwords - HOTP

_**Possession Factor:**_ HOTP Generator

_**Knowledge Factor:**_ PIN or Password

_**Inherence Factor:**_ None

_**Phishing Resistance:**_ None

Described by [RFC 4226](https://www.rfc-editor.org/rfc/rfc4226) as “An HMAC-based One Time Password Algorithm,” HOTP is a commonly used second factor.  Successive HOTP values are generated through the application of the HMAC-SHA1 algorithm, whose inputs are a static seed value, unique per device and shared with the server, and the counter, a numeric value that increments on each iteration.  The output is truncated to a set of human-readable numbers, often 4-8 bytes in length.

Generally found on hardware devices with small display screens showing a set of numbers after pressing a button, the HOTP output is entered into a form field by the user to complete authentication.  Of note with HOTP generation is that the codes are generated dynamically in response to a user action, such as a button press.  This can lead to devices becoming out of sync with the server state when multiple HOTPs are generated by the client and unused.  Desynchronization must be addressed through a re-synchronization process that is undefined by RFC.

@column
### ワンタイムパスワード - HOTP

_**所有要素**_ ：HOTP生成器

_**知識要素**_ ：PINまたはパスワード

_**生体要素**_ ：なし

_**フィッシング耐性**_ ：なし

[RFC 4226](https://www.rfc-editor.org/rfc/rfc4226)で「An HMAC-based One Time Password Algorithm」として定義されている、HOTPは一般的に2つ目の要素として利用されます。連続するHOTPの値は、HMAC-SHA1アルゴリズムのアプリケーションを通じて生成されます。アルゴリズムの入力値はデバイスごとに一意でサーバーと共有される静的なシード値と、反復ごとに増加する数値であるカウンターです。出力は人間が読むことができる、通常は4～8バイトの長さに切り捨てられます。

一般的に、ボタンを押した後に一連の数字が表示される小さな表示画面を持つハードウェアデバイスであり、HOTPの出力はユーザーによってフォームフィールドに入力され、認証を完了します。HOTP生成で注意すべき点は、ボタン押下のようなユーザー操作に応じてダイナミックにコードが生成されることです。これにより、クライアントによって複数のHOTPが生成されたり、利用されなかったとき、デバイスがサーバーの状態と同期しなくなる可能性があります。非同期化はRFCで定義されていない再同期化プロセスによって対処しなければなりません。

@row
### One-Time Passwords - TOTP

_**Possession Factor:**_ TOTP Generator

_**Knowledge Factor:**_ PIN or Password

_**Inherence Factor:**_ None

Similar to a HOTP, a TOTP is defined by [RFC 6238](https://www.rfc-editor.org/rfc/rfc6238) as a time-based one-time password algorithm.  The RFC describes TOTPs as a “variant of the HOTP algorithm \[that\] specifies the calculation of a one-time password value, based on a representation of the counter as a time factor.”  Since the successive values are not generated in response to a user action, desynchronization is less of an issue with TOTPs vs. HOTPs, assuming the services are not subject to excessive clock-skew.

Similar to HOTP, TOTP is often implemented in hardware devices with a small display screen that is constantly refreshed over time, displaying 4 to 8 digits.  Additionally, TOTPs are often implemented by software such as password managers, Authy, etc., as a convenient mechanism for users with smartphones to carry multiple TOTP generators for different services on a device they already possess.  In this case, the user will scan a QR code with their TOTP software application, instantiating the TOTP in the software.  The user then enters the current TOTP into the relying party’s service to validate the TOTP has been instantiated correctly.  These TOTPs may exist on multiple devices, either through a cloud-based sync or re-scanning the QR code on multiple devices as a backup of the TOTP generator.

TOTP, like HOTP, was developed by the Initiative for Open Authentication, an industry group that developed the open specifications, which later became IETF RFCs. The standards developed by OATH enabled the creation of an ecosystem of hardware devices and software implementations, eliminating the need for context-specific second factors.

@column
### ワンタイムパスワード - TOTP

_**所有要素**_ ：TOTP生成器

_**知識要素**_ ：PINまたはパスワード

_**生体要素**_ ：なし

HOTPと同様に、TOTPは[RFC 6238](https://www.rfc-editor.org/rfc/rfc6238)によって時間ベースのワンタイムパスワードアルゴリズムとして定義されています。RFCはTOTPを「時間を要素としたカウンターの表現に基づくワンタイムパスワードの値を計算を指示するHOTPアルゴリズムの変形」と記述しています。連続する値はユーザー操作とは関係なく生成されているため、サービスは過度なクロックスキューの影響を受けなければ、HOTPと比べてTOTPは非同期化の問題は少ないです。

HOTPと同様に、TOTPは4～8桁の数字が表示される、時間とともに常に更新される小さな表示画面を持つハードウェアデバイスにしばしば実装されます。加えて、TOTPはAuthyなどパスワードマネージャーのようなソフトウェアによって実装されることが多くあり、これはスマートフォンを持つユーザーにとって、既に所持しているデバイス上で異なるサービスのための複数のTOTP生成器を持ち運ぶために便利な仕組みとなっています。この場合、ユーザーはTOTPソフトウェアアプリケーションでQRコードをスキャンし、ソフトウェア内でTOTPをインスタンス化します。そして、ユーザーは現在のTOTPをリライングパーティのサービスに入力し、TOTPが正しくインスタンス化されたかを検証します。これらのTOTPは、クラウドによる同期やTOTP生成器のバックアップとして複数のデバイスでQRコードを再スキャンすることによって、複数のデバイスに存在するかもしれません。

HOTPのように、TOTPはInitiative for Open Authentication、オープンな仕様を開発した業界団体、によって開発され、後年IETF RFCになりました。OAUTHによって開発された標準仕様はハードウェアデバイスとソフトウェア実装のエコシステムの構築を可能にし、コンテキスト固有の2つ目の要素の必要性を排除します。

@row
### One-Time Passwords - SMS (Short Messaging Service)

_**Possession Factor:**_ Access to SMS on a mobile device

_**Knowledge Factor:**_ PIN or Password

_**Inherence Factor:**_ None

SMS OTP allows a user to authenticate using a one-time password sent over to the user’s mobile number using SMS.  The user configures their phone number with a relying party to receive OTPs during authentication. As noted above, NIST-800-63rev3 identifies [SMS OTP](https://pages.nist.gov/800-63-3/sp800-63b.html#pstnOOB) as a “ [restricted](https://pages.nist.gov/800-63-3/sp800-63b.html#restricted) ” authenticator.

> “The use of a RESTRICTED authenticator requires that the implementing organization assess, understand, and accept the risks associated with that RESTRICTED authenticator and acknowledge that risk will likely increase over time. It is the responsibility of the organization to determine the level of acceptable risk for their system(s) and associated data and to define any methods for mitigating excessive risks. If at any time the organization determines that the risk to any party is unacceptable, then that authenticator SHALL NOT be used. [^19]
> 
> Verifiers SHOULD consider risk indicators such as device swap, SIM change, number porting, or other abnormal behavior before using the PSTN to deliver an out-of-band authentication secret.” [^20]

@column
### ワンタイムパスワード - SMS（ショートメッセージサービス）

_**所有要素**_ ：モバイルデバイスでSMSにアクセスする

_**知識要素**_ ：PINまたはパスワード

_**生体要素**_ ：なし

SMS OTPは、SMSを使ってユーザーの携帯電話番号に対して送られたワンタイムパスワードを使ってユーザーが認証できるようにします。ユーザーは認証時にOTPを受信するために、電話番号をリライングパーティに設定します。上述のように、NIST-800-63rev3では[SMS OTP](https://pages.nist.gov/800-63-3/sp800-63b.html#pstnOOB)を「[制限された](https://pages.nist.gov/800-63-3/sp800-63b.html#restricted)」認証器としています。

> 「 **制限された** 認証器の利用には、導入する組織は **制限された** 認証器に関連するリスクを評価、理解および受容することと、そのリスクが時間とともに増大していく傾向があることを知っておくことが必要です。組織のシステムと関連データに対して受容できるリスクのレベルを決定することと、過度なリスクを軽減する方法を定義することは、組織の責任です。組織がいかなる当事者に対するリスクも許容できないと判断した場合、その認証器は使用するべきではない（SHALL NOT）。 [^19]
> 
> 検証者は、帯域外認証シークレットを配信するためにPSTNを利用する前に、デバイススワップやSIMスワップ、ナンバーポーティング、その他の異常動作のようなリスク指標を考慮すべきです（SHOULD）。」 [^20]

@row
### One-Time Passwords - Email

_**Possession Factor:**_ Email address (no physical possession)

_**Knowledge Factor:**_ PIN or Password

_**Inherence Factor:**_ None

Email OTP allows a user to user to authenticate using a one-time password sent over to a registered email address registered to the user’s account. The user must provide the OTP value during the authentication ceremony.  The security of email OTP is dependent upon the security of the user’s email service.

@column
### ワンタイムパスワード - Eメール

_**所有要素**_ ：Eメールアドレス（物理的所有はない）

_**知識要素**_ ：PINまたはパスワード

_**生体要素**_ ：なし

EメールOTPは、ユーザーアカウントに登録されたEメールアドレスに対して送られたワンタイムパスワードを使ってユーザーが認証できるようにします。ユーザーは認証セレモニー中にOTPの値を提供しなければなりません。EメールOTPのセキュリティはユーザーのEメールサービスのセキュリティに依存します。

@row
### One-Time Passwords – Magic Links

_**Possession Factor:**_ Indeterminate

_**Knowledge Factor:**_ Indeterminate

_**Inherence Factor:**_ Indeterminate

Magic links provide a fast and easy sign-in user experience. Users are authenticated by providing their email address only; they are then sent an email with a link for the user to click and complete their sign-in. This link is an embedded token that can only be used once. This provides a password-less login experience, which has many user experience advantages. However, it is worth mentioning that magic links are only as secure as a user’s email address. For example, if someone gets access to a user’s inbox, they can now access the magic links as they get sent to the user, which might lead to an authorized access event. Therefore, we classify the possession, knowledge, and inherence factors are indeterminate – the security is dependent upon the authentication credentials to the email service and any devices which have persistent access to the same.

@column
### ワンタイムパスワード – マジックリンク

_**所有要素**_ ：不確定

_**知識要素**_ ：不確定

_**生体要素**_ ：不確定

マジックリンクは、素早く簡単なサインインユーザー体験を提供します。ユーザーはEメールアドレスだけで認証されます；ユーザーがクリックするとサインインが完了するリンク付きのEメールが送られます。このリンクは1度だけ利用できるトークンが埋め込まれています。これはパスワードレスログイン体験を提供し、ユーザー体験で大きな利点があります。しかし、マジックリンクはユーザーのEメールアドレスと同じ安全性でしかないことは言及しておく価値があります。例えば、何者かがユーザーの受信箱にアクセスできる場合、今やユーザーに送られたマジックリンクにアクセスすることができ、認可されたアクセスイベントとなります。よって、所有要素、知識要素および生体要素を不確定と分類し、セキュリティはEメールサービスおよび同じEメールサービスに永続的にアクセスできるデバイスの認証クレデンシャルに依存します。

@row
### FIDO U2F / FIDO2

_**Possession Factor:** Devices such as a phone, tablet, laptop, or a FIDO hardware security key_

_**Knowledge Factor:**_ PIN code (optional, may be used in place of an inherence factor)

_**Inherence Factor:** fingerprint, iris, or faceprint (optional, may be used in place of a PIN code)_

The FIDO protocols (U2F/CTAP1, CTAP2.x) and WebAuthn use asymmetric cryptography to authenticate users on external hardware devices (e.g., security keys) and platform authenticators built into laptops, tablets, and phones.  Authentication credentials are [scoped](https://www.w3.org/TR/webauthn-2/#scope) to origins controlled by the relying party; relying parties cannot discover credentials for unrelated origins to protect privacy. [^21] The credentials may be bound to a single device, as with hardware keys and some platform authenticators, or synchronized across a cloud fabric, ensuring availability across the user’s devices. FIDO credentials are considered to be highly phishing resistant.

Some FIDO credentials are attestable.  At registration, the authenticator emits a signed attestation statement identifying the provenance of the authenticator.  Relying parties can validate the signature on the attestation and collect additional authenticator metadata through the FIDO Metadata Service (MDS). [^22] This data may include information about the authenticator’s [certification level](https://fidoalliance.org/certification/authenticator-certification-levels/) and conformance to standards such as FIPS140-1. [^23]

Implementers should note that not all FIDO credentials are created equally. FIDO credentials may be created and managed entirely in software, within TPMs, Secure Enclaves, or other hardware embedded in general-purpose computers, phones, and tablets, or on hardware security keys. While all of these credentials use the same cryptographic primitives and protocols, relying parties should have an understanding of the differences between FIDO authentication mechanisms to help them make effective choices when implementing FIDO solutions.

*   Passkeys are discoverable credentials that reside on the system that created them.
    
*   Passkeys may be used as a highly phishing-resistant, single-factor credential, replacing passwords.
    
*   The number of passkeys that can be configured on a single hardware security key is limited by the properties of the hardware and credentials.
    
*   Passkeys created on hardware security keys do not leave the device.
    
*   Passkeys may be synchronized across a fabric provided by platforms (Apple, Google, Microsoft) or password managers (1Password, Dashlane). Synchronization fabrics are provider-specific. Synchronized keys are sometimes called “multi-device credentials”. Non-synchronized keys are “single-device credentials”.
    
*   Passkeys cannot be synchronized across providers.
    
*   Synchronized credentials create an alternative credential recovery pathway. Credential recovery mechanisms are provider-specific.
    
*   Passkeys may be shared by exporting them to nearby contacts through the AirDrop protocol on Apple platform devices.
    
*   Passkeys, like all FIDO credentials, may not carry an attestation during registration. Relying parties may request attestation during credential registration. Authenticators and browsers may restrict whether an attestation is returned.
    
*   In the event that a credential does not meet the relying party’s requirements, the RP must reject credential registration after the credential is created on the authenticator.
    
*   Relying parties cannot be assured of the origin or security properties of unattested credentials. High-assurance use cases should require and validate all attestations.
    

The breadth of the FIDO2/WebAuthn ecosystem is too broad for this article.  Look for a future BoK article on the FIDO protocols to address these protocols in more depth.

@column
### FIDO U2F / FIDO2

_**所有要素**_ ： _携帯電話、タブレット、ノートパソコンもしくはFIDOハードウェアセキュリティキーのようなデバイス_

_**知識要素**_ ：PINコード（オプション、生体要素の代わりに利用される可能性があります）

_**生体要素**_ ： _指紋、虹彩や顔認証（オプション、PINコードの代わりに利用される可能性があります）_

FIDOプロトコル（U2F/CTAP1、CTAP2.x）とWebAuthnは、外部ハードウェア（セキュリティキーなど）およびノートパソコン、タブレットや携帯電話に組み込まれたプラットフォーム認証器条でユーザーを認証するために非対称鍵暗号を利用します。認証クレデンシャルはリライングパーティが管理しているオリジンに[限定](https://www.w3.org/TR/webauthn-2/#scope)されます；リライングパーティはプライバシー保護のため、無関係なオリジン向けのクレデンシャルを発見することはできません。 [^21] クレデンシャルは、ハードウェアキーや一部のプラットフォーム認証器のように単一デバイスにバインドされていたり、クラウドファブリックを介して同期されてユーザーのデバイス間で利用可能になっていたりする可能性があります。FIDOクレデンシャルは高いフィッシング耐性があると考えられています。

一部のFIDOクレデンシャルは証明可能です。登録時、認証器は認証器の由来を特定する署名付きアテステーションステートメントを発行します。リライングパーティはアテステーションの署名を検証することができ、FIDOメタデータサービス（MDS） [^22] を介して追加の認証器メタデータを収集できます。このメタデータは認証器の[認定レベル](https://fidoalliance.org/certification/authenticator-certification-levels/)およびFIPS140-1のような標準仕様への準拠についての情報が含まれているかもしれません。 [^23]

実装者は、全てのFIDOクレデンシャルを同じように生成されるわけではないことに注意すべきです。FIDOクレデンシャルは、TPM、セキュアエンクレーブや汎用的なコンピュータ、携帯電話やタブレットに組み込まれたその他のハードウェア、あるいはハードウェアセキュリティキーで、完全にソフトウェアで生成され、管理される可能性があります。これらクレデンシャルの全てが同じ暗号プリミティブとプロトコルを利用しますが、リライングパーティはFIDOソリューションを実装するときに効果的な選択をおこなうために役立つようにFIDO認証メカニズムの違いを理解しておくべきです。

*   パスキーは、作成したシステムに存在する、発見可能なクレデンシャルです。
    
*   パスキーはフィッシング耐性が高く、単一要素のクレデンシャルであり、パスワードを置き換えるものとして利用されることがあります。
    
*   単一のハードウェアセキュリティキー上に設定できるパスキーの数は、ハードウェアとクレデンシャルのプロパティによって制限されます。
    
*   ハードウェアセキュリティキー上に作成されたパスキーはデバイスから離れることはありません。
    
*   パスキーは、プラットフォーム（Apple、Google、Microsoft）やパスワードマネージャー（1Password、Dashlane）によって提供されるファブリックを介して同期されることがあります。同期ファブリックはプロバイダーによって異なります。同期されたキーは「マルチデバイスクレデンシャル」と呼ばれることもあります。非同期キーは「単一デバイスクレデンシャル」と呼ばれることもあります。
    
*   パスキーはプロバイダー間で同期することはできません。
    
*   同期クレデンシャルは、代替のクレデンシャルリカバリー手順を作成します。クレデンシャルリカバリーメカニズムはプロバイダーによって異なります。
    
*   パスキーは、Appleプラットフォームデバイス上のAirDropプロトコルを介した近接接続にパスキーをエクスポートすることで、共有することがあります。
    
*   全てのFIDOクレデンシャルのようにパスキーは登録時にアテステーションを持っていないかもしれません。リライングパーティは、クレデンシャル登録時にアテステーションを要求する可能性があります。認証器およびブラウザはアテステーションが返却されるかを制限するかもしれません。
    
*   クレデンシャルがリライングパーティの要件に一致しない場合、クレデンシャルが認証器で作成された後、RPはクレデンシャルの登録を拒否しなくてはなりません。
    
*   リライングパーティは、証明されていないクレデンシャルの出所やセキュリティ特性を保証できません。高い保証を要求するユースケースは、全てのアテステーションを要求し、検証するべきです。
    

FIDO2/WebAuthnエコシステムの範囲は、この記事にとって非常に広いです。これらのプロトコルについて詳しい、FIDOプロトコルについての将来のBoKの記事を参照してください。

@row
### Push-Based Authentication

_**Possession Factor:** Access to the mobile device where the push notification is sent_

_**Knowledge Factor:**_ PIN or Password (optional)

_**Inherence Factor:** Biometric on the device (optional)_

Push-based authentication is primarily a mobile-based experience. At authentication time, the service sends a push notification to the user’s registered device(s) or applications.  The user receives the notification and may approve or decline the request.  As with most technologies, this has been abused by malicious actors who use social engineering or prompt bombing attacks to obtain the user's help to complete the authentication process. [^24] These attacks can be mitigated by providing additional context data to the user, such as the location of the authentication session or device identity, or requiring the user to copy a number from the push notification to the device attempting authentication. [^25]

@column
### プッシュ型認証

_**所有要素**_ ： _プッシュ通知が送られたモバイルデバイスへのアクセス_

_**知識要素**_ ：PINまたはパスワード（オプション）

_**生体要素**_ ： _デバイス上のバイオメトリクス（オプション）_

プッシュ型認証は主にモバイルベースの体験です。認証時、サービスはユーザーの登録済デバイスまたはアプリケーションにプッシュ通知を送ります。ユーザーは通知を受け取り、リクエストを承認するか拒否するかします。ほとんどのテクノロジーと同様に、認証プロセスを完了させるためにユーザーの助けを得るために、ソールシャルエンジニアリングやプロンプト爆弾攻撃を使う悪意のあるアクターによって悪用されてきました。 [^24] これらの攻撃は、ユーザーに認証セッションの位置やデバイスアイデンティティのような追加のコンテキストデータを提供することや、ユーザーにプッシュ通知から番号を認証を試みているデバイスにコピーすることを要求することによって軽減できます。 [^25]

@row
### Smart Cards

_**Possession Factor:**_ Smart Card

_**Knowledge Factor:**_ PIN (optional, may use inherence factors)

_**Inherence Factor:**_ Fingerprint (optional, may use PIN)

Smart Cards are physical devices of varying sizes (e.g., nano-SIM, SIM, credit card form factors) used to store a credential, often in the form of a cryptographic certificate, which can be unlocked by the user presenting a PIN or inherence factor to facilitate authentication.  The card may be presented by insertion into a physical reader or via a contactless protocol, such as NFC.

Smart cards exist in a wide variety of formats with different use cases depending on the industry in which they are used.  A common deployment is the use of a Common Access Card (CAC) by the US Federal Government.  After identity proofing, the federal government issues a CAC to an individual as both a physical identity document used to access government property, as well as a multi-factor authenticator.  Upon inserting the CAC into a reader, the user enters a PIN to unlock the device.  Once unlocked, the CAC authenticates the user against a directory service via the public key certificate embedded in the hardware.

@column
### スマートカード

_**所有要素**_ ：スマートカード

_**知識要素**_ ：PIN（オプション、生体要素を利用する可能性があります）

_**生体要素**_ ：指紋（オプション、PINを利用する可能性があります）

スマートカードとは、認証を容易にするための様々なサイズ（例、nano-SIM、SIM、クレジットカードなどの規格）の物理デバイスであり、多くの場合に暗号化証明書の形式でクレデンシャルを保管するために利用され、ユーザーによって提示されたPINまたは生体要素によって復号されます。スマートカードは物理的なリーダーへの挿入やNFCのようなコンタクトレスプロトコルによって提示されます。

スマートカードは、利用される業界によって異なるユースケースに応じて幅広い種類の形式が存在しています。一般的な導入例は、米国連邦政府による共通アクセスカード（CAC）の利用です。身元確認後、連邦政府は政府資産へのアクセスに利用される物理的な身分証明書として、多要素認証器としてCACを発行します。CACをリーダーに挿入するとき、ユーザーはPINを入力してデバイスを解錠します。解錠されると、CACはハードウェアに埋め込まれた公開鍵証明書を介してディレクトリサービスに対してユーザーを認証します。

@row
## Threat Mitigation by MFA Mechanism

The [NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html) is a recommended read as it provides an informative section on the various threat and security considerations and how to mitigate them. In this section, we highlight a subset of threats against MFA mechanisms and whether the mechanism is susceptible to the threat (❌), partially mitigates the threat (～), or completely mitigates the threat (✅).

The threats considered below are:

*   Credential duplication - Can the credential be duplicated and used in a manner undetectable to the owner?  For example, a grid card could be photographed and used illicitly if the password was known, but the attack is not scalable.
    
*   Eavesdropping / Man in the Middle - Active or passive eavesdropping of communications can compromise flows that depend on secrets, either by sniffing the secret off the wire as they are being delivered to the recipient (e.g., attacks on mobile SMS networks or SIM swapping), or by replaying secrets obtained through phishing.
    
*   Replay - Some MFA mechanisms are designed for one-time use.  Implementations may fail to enforce one-time use of these secrets, allowing sniffed secrets to be replayed.
    
*   Social Engineering - Manipulating a target through psychological means such as authority, intimidation, urgency, and other mechanisms to force a victim to take actions that may not be in their own best interests.  In the realm of MFA, this may be seen through attacks such as prompt bombing.
    
*   Phishing - A form of social engineering where the victim is enticed into entering their credentials into a fraudulent site designed to look like a legitimate service.  Phishers will collect credentials, including passwords and second factors, and use them immediately to authenticate to the legitimate site to further their schemes.  In 2020, phishing was the most frequent crime reported to the FBI Internet Crime Complaint Center (IC3), representing almost one-third of all complaints (241,343 of 791,790). [^26]
    

@column
## MFAメカニズムによる脅威軽減

[NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)では様々な脅威およびセキュリティ考慮事項およびそれらをどのように軽減するのかに関する有益なセクションが提供されているため、読むことを推奨します。本セクションでは、MFAメカニズムに対する脅威の部分集合と、MFAメカニズムが脅威に対して無防備である（❌）か、部分的に脅威を軽減できる（～）か、完全に脅威を軽減できる（✅）かを示します。

以下の脅威について検討します：

*   クレデンシャルの複製 - クレデンシャルを複製し、所有者に検知できない方法で利用できるか？例えば、パスワードを知っている場合、グリッドカードを撮影して不正に利用することはできますが、この攻撃は規模を大きくすることはできません。
    
*   盗聴 / マン・イン・ザ・ミドル - 通信の能動的または受動的な盗聴、受信者に配信されるときに経路でシークレットをスニッフィング（例えば、モバイルSMSネットワークへの攻撃やSIMスワッピング）することや、フィッシングによって取得したシークレットをリプレイすること、によってシークレットに依存したフローを侵害できます。

*   リプレイ - 一部のMFAメカニズムは1回だけの利用を想定した設計をしています。実装がこれらのシークレットの1回限りの利用を強制しない可能性があり、これはスニッフィングされたシークレットをリプレイすることが可能になります。
    
*   ソーシャルエンジニアリング - 権威、威嚇、緊急性およびその他のメカニズムなどの心理的な手法を使って対象者を操作し、被害者自身にとっての最善の利益にならない可能性のあることを取らせること。MFAの領域ではプロンプト爆弾のような攻撃を通じて見られます。

*   フィッシング - ソーシャルエンジニアリングの一種で、被害者が正規サービスに似ているように作成された詐欺サイトにクレデンシャルを入力するように誘うこと。フィッシング攻撃者は、パスワードおよび第二要素を含むクレデンシャルを収集し、正規サイトでの認証のためにすぐにそれらを利用し、自分たちの計画を進めます。2020年、フィッシングはFBIインターネット犯罪苦情センター（IC3）に報告された最も多い犯罪であり、苦情全体の約3分の1を締めています（791,798件中241,343件）。 [^26]
    

@row

| **脅威（--->）** | **クレデンシャルの複製** | **盗聴 / マン・イン・ザ・ミドル / リプレイ** | **フィッシング** | **Sソーシャルエンジニアリング** |
| --- | --- | --- | --- | --- |
| **メカニズム（↓）** |     |     |     |     |
|     |     |     |     |     |
| グリッドカードとグリッドベースメカニズム | ❌   | ～   | ❌   | ❌   |
| クレデンシャル計算機ハードウェアトークン | ❌   | ～   | ❌   | ❌   |
| ワンタイムパスワード - HOTP | ～   | ～   | ❌   | ❌   |
| ワンタイムパスワード - TOTP | ❌   | ～   | ❌   | ❌   |
| ワンタイムパスワード - SMS | N/A | ～   | ❌   | ❌   |
| ワンタイムパスワード - Eメール | N/A | ～   | ❌   | ❌   |
| FIDO U2F / FIDO2 | ～   | ✅   | ✅   | ✅   |
| プッシュ型認証 | N/A | ✅   | ✅   | ～   |
| スマートカード | ✅   | ✅   | ✅   | ✅   |

@row
## Conclusion

Using MFA is now considered an essential security best practice. It protects against many cyber threats, and the user experience has significantly improved since the early days of heavy hardware tokens. There is more to learn when it comes to deploying MFA in an environment; we suggest further exploring this space by reading Nishant Kaushik’s [“Designing MFA for Humans”](https://doi.org/10.55621/idpro.49) . [^27]

@column
## まとめ

MFAの利用は、今や不可欠なセキュリティベストプラクティスと考えられています。MFAは多くのサイバー脅威から保護し、ユーザー体験は初期の重いハードウェアトークンに比べて非常に改善されています。環境にMFAを導入することに関して、まだまだ学ぶべきことがあります；Nishant Kaushikの[“Designing MFA for Humans”](https://doi.org/10.55621/idpro.49) [^27] を読み、この分野をさらに探求することを推奨します。

- - -

[^1]:  References
    
    “Terminology in the IDPro Body of Knowledge,” IDPro Body of Knowledge, updated 30 September 2021, [https://bok.idpro.org/article/id/41/](https://bok.idpro.org/article/id/41/) . 
    
[^2]:  Grassi, Paul A., James L. Fenton, Elaine M. Newton, Ray A. Perlner, Andrew R. Regenscheid, William E. Burr, and Justin P. Richer, "NIST Special Publication 800-63B: Digital Identity Guidelines: Authentication and Lifecycle Management," National Institute of Standards and Technology, U.S. Department of Commerce, updated 2 March 2022, [https://doi.org/10.6028/NIST.SP.800-63b](https://doi.org/10.6028/NIST.SP.800-63b) . 
    
[^3]:  Bátiz-Lazo, Bernardo, "A Brief History of the ATM: How automation changed retail banking, an Object Lesson," The Atlantic, 26 March 2015, [https://www.theatlantic.com/technology/archive/2015/03/a-brief-history-of-the-atm/388547/](https://www.theatlantic.com/technology/archive/2015/03/a-brief-history-of-the-atm/388547/) (accessed 14 December 2022). 
    
[^4]:  Batiz-Lazo, Bernardo and Reid, Robert J. K., "Evidence from the Patent Record on the Development of Cash Dispensing Technology," MPRA: Munich Personal RePEc Archive, University of Leicester, University of Leicester and University of Glasgow, 30 June 2008, [https://mpra.ub.uni-muenchen.de/9461/1/MPRA\_paper\_9461.pdf](https://mpra.ub.uni-muenchen.de/9461/1/MPRA_paper_9461.pdf) (accessed 14 December 2022). 
    
[^5]:  M'Raihi, D., Machani, S., Pei, M., and J. Rydell, "TOTP: Time-Based One-Time Password Algorithm", RFC 6238, DOI 10.17487/RFC6238, May 2011, < [https://www.rfc-editor.org/info/rfc6238](https://www.rfc-editor.org/info/rfc6238) \>. 
    
[^6]:  M'Raihi, D., Bellare, M., Hoornaert, F., Naccache, D., and O. Ranen, "HOTP: An HMAC-Based One-Time Password Algorithm", RFC 4226, DOI 10.17487/RFC4226, December 2005, < [https://www.rfc-editor.org/info/rfc4226](https://www.rfc-editor.org/info/rfc4226) \>. 
    
[^7]:  U.S. Department of Homeland Security,"Homeland Security Presidential Directive 12: Policy for a Common Identification Standard for Federal Employees and Contractors," last updated 27 January 2022, [https://www.dhs.gov/homeland-security-presidential-directive-12](https://www.dhs.gov/homeland-security-presidential-directive-12) (accessed 14 December 2022). 
    
[^8]:  National Institute of Standards and Technology, "Personal Identity Verification (PIV) of Federal Employees and Contractors," Federal Information Processing Standard (FIPS) 201-1, March 2006, [https://csrc.nist.gov/CSRC/media/Publications/fips/201/1/archive/2006-06-23/documents/FIPS-201-1-chng1.pdf](https://csrc.nist.gov/CSRC/media/Publications/fips/201/1/archive/2006-06-23/documents/FIPS-201-1-chng1.pdf) . Please note version is for historical reference only; the current version of this publication is FIPS 201-3, published January 2022 and available at [https://doi.org/10.6028/NIST.FIPS.201-3](https://doi.org/10.6028/NIST.FIPS.201-3) . 
    
[^9]:  Dray, James, Scott Guthery, and Teresa Schwarzhoff, "NIST Special Publication 800-73-1: Interfaces for Personal Identity Verification," Computer Security Resource Center, National Institute of Standards and Technology, U.S. Department of Commerce, March 2006, [https://csrc.nist.gov/publications/detail/sp/800-73/1/archive/2006-03-15](https://csrc.nist.gov/publications/detail/sp/800-73/1/archive/2006-03-15) . Please note version is for historical reference only; the current version of this publication is NIST 800-73-4, published May 2015 and available at https://doi.org/10.6028/NIST.SP.800-73-4. 
    
[^10]:  U.S. Department of Justice, Office of Justice Programs, "Putting an End to Account-Hijacking Identity Theft," NCJ Number: 210758, December 2004, [https://www.ojp.gov/ncjrs/virtual-library/abstracts/putting-end-account-hijacking-identity-theft](https://www.ojp.gov/ncjrs/virtual-library/abstracts/putting-end-account-hijacking-identity-theft) (accessed 14 December 2022). 
    
[^11]:  Federal Financial Institutions Examination Council, "Authentication in an Internet Banking Environment," 2005, [https://www.ffiec.gov/pdf/authentication\_guidance.pdf](https://www.ffiec.gov/pdf/authentication_guidance.pdf) (accessed 14 December 2022) 
    
[^12]:  Libicki, Martin C., Edward Balkovich, Brian A. Jackson, Rena Rudavsky, Katharine Watkins Webb, "Influences on the Adoption of Multifactor Authentication," technical report, RAND Homeland Security and Defense Center, 2011, [https://www.rand.org/content/dam/rand/pubs/technical\_reports/2011/RAND\_TR937.pdf](https://www.rand.org/content/dam/rand/pubs/technical_reports/2011/RAND_TR937.pdf) (accessed 14 December 2022). 
    
[^13]:  “ [Banks to Use 2-factor Authentication by End of 2006](https://it.slashdot.org/story/05/10/19/2340245/banks-to-use-2-factor-authentication-by-end-of-2006) ,” Slashdot forum discussion, 2005, [https://it.slashdot.org/comments.pl?sid=165833&cid=13832042](https://it.slashdot.org/comments.pl?sid=165833&cid=13832042) (accessed 14 December 2022). 
    
[^14]:  FIDO Alliance, “History of FIDO Alliance,” n.d., [https://fidoalliance.org/overview/history/](https://fidoalliance.org/overview/history/) (accessed 14 December 2022). 
    
[^15]:  "Web Authentication: An API for accessing Public Key Credentials Level 1," W3C Recommendation, 4 March 2019, and “Client to Authenticator Protocol (CTAP),” FIDO Alliance, 21 June 2022, [https://fidoalliance.org/specifications/download/](https://fidoalliance.org/specifications/download/) . 
    
[^16]:  Passkey.dev website, [W3C WebAuthn Community Adoption Group](https://www.w3.org/community/webauthn-adoption/) and the [FIDO Alliance](https://fidoalliance.org/) , [https://passkeys.dev/](https://passkeys.dev/) (accessed 14 December 2022). 
    
[^17]:  Schneier, Bruce, "The Failure of Two-Factor Authentication," Schneier on Security blog, March 2005, [https://www.schneier.com/blog/archives/2005/03/the\_failure\_of.html](https://www.schneier.com/blog/archives/2005/03/the_failure_of.html) (accessed 14 December 2022). 
    
[^18]:  Williams, Andy, "Grid-based two-factor authentication comes to campus cards," SecureIDNews, 25 September 2006, [https://www.secureidnews.com/news-item/grid-based-two-factor-authentication-comes-to-campus-cards/](https://www.secureidnews.com/news-item/grid-based-two-factor-authentication-comes-to-campus-cards/) \# (accessed 14 December 2022). 
    
[^19]:  NIST 800-63B Section 5.2.10 Restricted Authenticators. 
    
[^20]:  NIST 800-63B Section 5.1.3.3 Authentication using the Public Switched Telephone Network. 
    
[^21]:  "Web Authentication: An API for accessing Public Key Credentials Level 2," W3C Recommendation, 8 April 2021, section 3. Dependencies, [https://www.w3.org/TR/webauthn-2/#scope](https://www.w3.org/TR/webauthn-2/#scope) . 
    
[^22]:  FIDO Alliance Metadata Service, website, [https://fidoalliance.org/metadata/](https://fidoalliance.org/metadata/) (accessed 14 December 2022). 
    
[^23]:  FIDO Alliance Certified Authenticator Levels, website, [https://fidoalliance.org/certification/authenticator-certification-levels/](https://fidoalliance.org/certification/authenticator-certification-levels/) (accessed 14 December 2022). 
    
[^24]:  Goodin, Dan, "A Sinister Way to Beat Multifactor Authentication Is on the Rise," Ars Technica, 30 March 2022, [https://www.wired.com/story/multifactor-authentication-prompt-bombing-on-the-rise/](https://www.wired.com/story/multifactor-authentication-prompt-bombing-on-the-rise/) . 
    
[^25]:  Cybersecurity & Infrastructure Security Agency, "Implementing Number Matching in MFA Applications," October 2022, [https://www.cisa.gov/sites/default/files/publications/fact-sheet-implement-number-matching-in-mfa-applications-508c.pdf](https://www.cisa.gov/sites/default/files/publications/fact-sheet-implement-number-matching-in-mfa-applications-508c.pdf) . 
    
[^26]:  "Internet Crime Report 2020," Internet Crime Compliant Center, Federal Bureau of Investigation, 2021, [https://www.ic3.gov/Media/PDF/AnnualReport/2020\_IC3Report.pdf](https://www.ic3.gov/Media/PDF/AnnualReport/2020_IC3Report.pdf) . 
    
[^27]:  Kaushik, N., (2020) “Designing MFA for Humans”, IDPro Body of Knowledge 1(3). doi: [https://doi.org/10.55621/idpro.49](https://doi.org/10.55621/idpro.49) . 
