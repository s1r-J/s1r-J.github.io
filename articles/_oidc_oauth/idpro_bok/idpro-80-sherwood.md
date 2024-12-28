---
layout: columns
title: Practical Implications of Public Key Infrastructure for Identity Professionals (v2)
permalink: /docs/oidc_oauth/idpro_bok/80
date: 2024-09-09
modify_date: 2024-12-28
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "PKI", "公開鍵基盤", "暗号化"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/80/](https://bok.idpro.org/article/id/80/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

Public Key Infrastructure, or “PKI,” is a technology that enables authentication via asymmetric cryptography. It is widely deployed for some vital security use cases on the Internet, especially for the authentication of servers via Transport Layer Security (TLS).

Despite its wide use in some scenarios, there are significant challenges in deploying PKI for more widespread use among smaller organizations or consumers.

Identity Professionals who need to deploy a PKI or have inherited a deployed PKI from someone else have several important considerations, including lifecycle management of keys and certificates, choosing the appropriate way to encode user identifiers, and understanding cross-PKI trust.


Keywords: PKI, Public Key Infrastructure, Encryption

@column
## 概要

公開鍵基盤、または「PKI」とは、非対称暗号を利用して認証を可能にする技術です。一部のインターネット上の重要なセキュリティユースケースとして広く採用されており、特にトランスポート層セキュリティ（TLS）によるサーバー認証において採用されています。
  
一部のシナリオでの幅広い利用にもかかわらず、より規模の小さな組織や消費者にとってより幅広く利用するためにPKIをデプロイすることは非常に困難です。
  
PKIをデプロイしたり、誰かからデプロイ済のPKIを引き継いだりする必要のあるアイデンティティ専門家には、鍵と証明書のライフサイクル管理、ユーザー識別子をエンコードする適切な方法の選定、クロスPKIトラストの理解などいくつかの重要な検討事項があります。


Keywords: PKI, 公開鍵基盤, 暗号化

@row
By Robert Sherwood

© 2022 Robert Sherwood and IDPro

_To comment on this article, please visit our [GitHub repository](https://github.com/IDPros/bok) and [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/opening-an-issue-from-code) ._

@row
## Introduction

In high-risk environments containing extremely sensitive data, every participant must have high confidence in the identity of every other participant. Public Key Infrastructure (PKI) is one of the most long-lived and widely deployed authentication technologies in these high-security environments. Despite the difficulty in deploying PKI for end users, which we discuss below, PKI was the only high-assurance credential available in the commercial market for many years. [^1] It is still considered the gold standard of credential assurance by many experts. Military and government environments have used PKI to provide secure authentication in sensitive environments since the late 90s.

Despite the widespread adoption of PKI in government environments, PKI has yet to see the same success in commercial settings. Later in this article, we will discuss some of the reasons for the lack of widespread adoption.

Despite the difficulties, PKI can be a feasible alternative to passwords for some enterprises, thanks to the implementation of smartcard-based authentication in many operating systems and browsers. Enterprises have renewed interest in smartcard login to eliminate passwords for privileged users in high-risk environments and scenarios.

This article includes analysis and guidance for the deployment of PKI for both human users and machines.

@column
## イントロダクション

非常に機密性の高い情報を扱うようなハイリスク環境において、全ての参加者は他の全ての参加者のアイデンティティに高い信頼がなければなりません。公開鍵基盤（PKI）は、このような高セキュリティ環境において最も長期にわたって広く採用されている認証技術の1つです。後述しますが、エンドユーザーにとってPKIの採用は困難がありますが、PKIだけが長年にわたって商業市場において高い保証度のあるクレデンシャルでした。 [^1] 依然として、PKIはクレデンシャル保証のゴールドスタンダードであると多くの専門家から見なされています。軍事および政府の環境では、90年代後半から機密性の高い環境における安全な認証を提供するためにPKIが利用されてきました。

政府環境でのPKIの採用が広がっている一方で、商業環境ではPKIは同じように成功しているわけではありません。この記事の後半に、幅広い採用がされていないいくつかの理由について議論します。

困難があるものの、多くのオペレーティングシステムとブラウザでのスマートカードによる認証の実装のおかげで、PKIは一部の企業にとってパスワードの有効な代替手段です。企業は、高リスク環境や高リスクシナリオにおける特権ユーザーのためのパスワードを排除するため、スマートカードログインに再び関心を寄せています。

本稿には、人間のユーザーおよびマシンの両方のためのPKIのデプロイに関する分析とガイダンスが書かれています。

@row
### Terminology

*   Asymmetric Cryptography: Any cryptographic algorithm which depends on pairs of keys for encryption and decryption. The entity that generates the keys shares one (see Public Key) and holds and protects the other (see Private Key). They are referred to as asymmetric because one key encrypts, and the other decrypts.
    
*   Automatic Certificate Management Environment (ACME): A communication protocol for automating lifecycle management of PKI certificates. Significant providers like Let's Encrypt leverage ACME to support issuing TLS certificates for web servers.
    
*   Certificate Authority Trust List (CTL): A client maintains a list of trusted Certificate Authorities created and managed by the software provider or local administrators. The client will only trust certificates issued under one of the CAs in the CTL, so the CTL serves as a "safe list."
    
*   Certificate Management System (CMS): A system that provides management and reporting layers for certificate issuance and revocation. A CMS integrates CA products with Identity Governance and Administration (IGA) systems as well as Service Desk systems.
    
*   Certificate Policy (CP): A document that defines the high-level policy requirement for a PKI. RFC 3647 identifies a PKI's policy framework and describes a CP's contents and outline. An enterprise operating a CA will often publish its certificate policy to external parties so they can determine whether to trust certificates issued by the CA.
    
*   Certification Practices Statement (CPS): A CP identifies the requirements for managing a CA and issuing PKI certificates. A CPS describes how a CA implements those requirements. The CPS uses the same outline as the CP, defined in RFC 3647. Unlike the CP, enterprises rarely publish their CPS in unredacted form.
    
*   Certificate Revocation List (CRL): A certificate authority will publish a list of revoked certificates, called a CRL so that clients can verify that a certificate is still good.
    
*   Certificate Signing Request (CSR): When requesting a certificate, the requesting entity provides a copy of the public key, their identifiers, and other information in a specially formatted binary object called a CSR.
    
*   Classical Computer: A computer that uses binary encoding and Boolean logic to make calculations in a deterministic way. We use the term Classical Computers in contrast with Quantum Computers.
    
*   Cryptographic Module: A hardware or software component that securely performs cryptographic operations within a logical boundary. Cryptographic Modules store private keys within this boundary and use them for cryptographic functions at the request of an authorized user or process.
    
*   Cryptographic Module Validation Program (CMVP): A program allowing cryptographic module developers to test their modules against the requirements defined in FIPS-140. The computer security resource center under the United States National Institute of Standards and Technology (NIST) maintains a publicly available list of validated modules.
    
*   Electronic Identification, Authentication, and Trust Services (eIDAS): European legislation gives legal standing to electronic signatures under eIDAS. This legislation also documents providing legally binding digital signatures with X.509 certificates to comply with Qualified Signature requirements.
    
*   Elliptic Curve Cryptography (ECC): An asymmetric cryptosystem based on calculating points along elliptic curves.
    
*   Encryption: Processing data using a cryptographic algorithm to provide confidentiality assurance.
    
*   Federal Agency Smart Credential Number (FASC-N): A unique identifier associated with a smart card. FASC-N is used in the US Federal Government PIV standard to support Physical Access.
    
*   Federal Information Processing Standard (FIPS) 140: A NIST standard defining "Security Requirements for Cryptographic Modules."
    
*   Groups: A set of identities with defined permissions. In this specific context, a group contains many individuals, but the group identity is opaque, and no information is available regarding which group member took an individual action.
    
*   Hardware Security Modules (HSMs): A hardware cryptographic module that generates and protects cryptographic keys.
    
*   Identifier: The way a system refers to digital identity. PKI Certificates support both internal and external identifiers. See Ian Glazer's article, "Identifiers and Usernames.” [^2]
    
*   Internet Key Exchange (IKE): A subordinate standard under IPsec specifying how to use X.509 certificates to establish symmetric keys for an IPsec tunnel.
    
*   Internet Protocol Security (IPsec): A standard for communication between two machines providing confidentiality and integrity over the Internet Protocol.
    
*   Key: In a cryptosystem, a Key is a piece of information used to encrypt or decrypt data in a cryptographic algorithm.
    
*   National Institute of Standards and Technology (NIST): A US Government agency that defines and publishes various standards. One department within NIST, the Computer Security Resource Center (CSRC), publishes the Federal Information Processing Standards (FIPS) series. While these standards are only mandatory for US Government Agencies, many countries recognize them as de-facto global standards.
    
*   Non-person entities (NPE): Any unique combination of hardware and software firmware (e.g., device) that utilizes the capabilities of other programs, devices, or services to perform a function. Non-person entities may act independently or on behalf of an authenticated individual or another NPE. [^3]
    
*   Online Certificate Status Protocol (OCSP): A protocol that allows a client to query the Certificate Authority or a Validation Authority for the status of an individual certificate rather than downloading a CRL.
    
*   Path Discovery and Validation (PDVal): The process to determine whether a certificate is valid and trusted by the validator.
    
*   Personal Identification Number (PIN): A numeric secret commonly used to unlock a private key container in software or hardware.
    
*   Personal Identity Verification (PIV): A US Government program designed to enable strong authentication for all government employees and contractors, based on Public Key Infrastructure.
    
*   Private key: A key that a single entity exclusively and privately controls. It corresponds to a public key that the entity may share for data encryption or signature verification.
    
*   Public key: A key that an entity publicly distributes. It corresponds to a private key that the entity exclusively and privately controls.
    
*   Public Key Certificate: A certificate containing a public key, one or more identifiers for the private key holder, an identifier for the Certificate Authority, and additional metadata to support security requirements.
    
*   Public Key Infrastructure: A set of tools, standards, and related policies designed to manage trust based on public/private key pairs and certificates.
    
*   Registration Authority (RA): An individual, system, or business function which provides registration and identity proofing for entities receiving certificates and manages the certificate issuance and renewal process. The most important responsibilities of an RA include identity proofing and binding the private key to the identity.
    
*   Revoke: Revocation is the announcement that clients should no longer trust an individual certificate.
    
*   Roles: A set of permissions. A role must be associated with an individual user, and the user gains the associated authorization when they are associated with the role.
    
*   RSA: An asymmetric cryptosystem based on large prime numbers. The acronym RSA stands for the three principal inventors, Ron Rivest, Adi Shamir, and Len Adleman.
    
*   S/MIME: A standard for constructing and sending digitally signed or encrypted messages using asymmetric cryptography.
    
*   Secure Socket Layer (SSL): A deprecated standard for encrypting data in transit; TLS has superseded it.
    
*   Server-based Certificate Validation Protocol (SCVP): A protocol that allows a client to query a server to determine whether a certificate is valid and trusted. The server does not need to be associated with the issuing CA. SCVP does two things; (1) it determines the path between the end entity and the trusted root, whereby the client doesn't need to trust any intermediate CAs. (2) it also performs delegated path validation according to policy.
    
*   Signature: Processing data using a cryptographic algorithm to provide integrity assurance.
    
*   Subject Alternative Name: One or more identifiers for a certificate subject that certificate issuers can use to carry application-specific identifiers such as email address or User Principal Name (UPN).
    
*   Subject Distinguished Name (Subject DN): A unique identifier for the subject within the scope of the Certificate Authority. Issuers structure the subject DN like an LDAP entry name.
    
*   Transport Layer Security (TLS): A cryptographic protocol designed to provide confidentiality and integrity of communications between two endpoints.
    
*   X.509: An ISO standard from the X.500 series that defines the basic rules for encoding public key certificates.
    
*   Validator: An entity that verifies a certificate and confirms that the other party controls the private key in the transaction.
    

@column
### 用語解説

*   非対称暗号：暗号化と復号のための一対の鍵に依存した暗号アルゴリズム。鍵を作成したエンティティは、1つ（「公開鍵」を参照）を共有し、もう1つ（「秘密鍵」を参照）を保持・保護します。これらの鍵は、一方は暗号化をおこない、他方は復号をおこなうため、非対称と呼ばれます。
    
*   Automatic Certificate Management Environment（ACME）：PKI証明書の自動ライフサイクル管理のための通信プロトコル。Let's Encryptのような規模の大きなプロバイダーはACMEを利用し、WebサーバーのためのTLS証明書発行をサポートしています。
    
*   認証局トラストリスト（CTL）：クライアントは、ソフトウェアプロバイダーまたはローカルの管理者が作成、管理している信頼できる認証局のリストをメンテナンスします。クライアントは、CTLに含まれるCAのうちの1つの元で発行された証明書のみを信頼するため、CTLは「安全なリスト」として振舞います。
    
*   証明書管理システム（CMS）：証明書の発行および失効を管理・報告するレイヤーを提供するシステム。CMSはCA製品をアイデンティティガバナンスと管理（IGA）システムおよびサービスデスクシステムと統合します。
    
*   証明書ポリシー（CP）：PKIの高レベルポリシー要件を定義したドキュメント。RFC 3647はPKIのポリシーフレームワークを特定し、CPの内容と概要を記述しています。CAを運用数r企業は多くの場合、その証明書ポリシーを外部の当事者に公開しており、それによって外部当事者はそのCAが発行した証明書を信頼するかどうかを決定します。
    
*   認証局運用規程（CPS）：CPはCAの管理およびPKI証明書の発行の要件を特定します。CPSは、CAがこれらの要件をどのように実装しているかを記述します。CPSは、RFC 3647で定義されているCPと同じ概要を使います。CPと異なり、稀に企業は無編集の形式でCPSを公開します。
    
*   証明書失効リスト（CRL）：認証局は、CRLと呼ばれる失効した証明書のリストを公開し、クライアントは証明書がまだ有効であることを検証します。
    
*   証明書署名リクエスト（CSR）：証明書を要求する際、リクエストをおこなうエンティティは公開鍵のコピー、識別子およびその他の情報をCSRと呼ばれる特別なバイナリオブジェクトの形式で提供します。
    
*   古典的コンピューター：バイナリエンコーディングとBoolean論理を用いて決定論的に計算を実行するコンピューター。量子コンピューターとの対象として古典的コンピューターという用語を用いています。
    
*   暗号モジュール：論理的境界内で暗号処理を安全に実行するハードウェアまたはソフトウェア。暗号モジュールは、その境界内に秘密鍵を保管し、認可されたユーザーまたはプロセスの要求時に暗号機能のために利用します。
    
*   暗号モジュール認証制度（CMVP）：暗号モジュールの開発者がFIPS-140で定義されている要件に照らし合わせてそのモジュールをテストすることを可能にする制度。米国国立標準技術研究所（NIST）傘下のコンピューターセキュリティリソースセンターが検証済モジュールの公開リストをメンテナンスしています。
    
*   Electronic Identification, Authentication, and Trust Services（eIDAS）：EU法は、eIDASによる電子署名に法的地位を与えています。この法律はQualified Signature要件に準拠するため、X.509証明書による法的拘束力のあるデジタル署名を提供することも文書化しています。
    
*   楕円曲線暗号（ECC）：楕円曲線に沿った点の計算に基づく非対称暗号システム。
    
*   暗号化：暗号アルゴリズムを使ってデータを処理し、機密性を保証すること。
    
*   連邦機関スマート認証情報番号（FASC-N）：スマートカードによるユニークな識別子。FASC-Nは米国連邦政府PIV標準において物理アクセスをサポートするために利用されます。
    
*   連邦情報処理規格（FIPS） 140：NIST標準が定義する「暗号モジュールのためのセキュリティ要件」。
    
*   グループ：定義された権限を持っているアイデンティティのセット。この特定のコンテキストｄえは、グループは多くの個人を含んでいますが、グループのアイデンティティは曖昧で、どのグループメンバーが個々のアクションを起こしたのかについての情報は入手できません。
    
*   ハードウェアセキュリティモジュール（HSM）：暗号鍵を生成および保護するハードウェア暗号モジュール。
    
*   識別子：システムがデジタルアイデンティティを参照する方法。PXI証明書は、内部および外部の両方の識別子をサポートしています。Ian Glazerの記事「Identifiers and Usernames」の参照。 [^2]
    
*   インターネット鍵交換（IKE）：IPSec下の規格で、IPSecトンネルのための共通鍵を確立するためのX.509証明書の使用方法を特定しています。
    
*   Internet Protocol Security（IPSec）：インターネットプロトコル上で機密性と完全性を提供する2つのマシン間の通信規格。
    
*   鍵：暗号システムにおいて、鍵とは暗号アルゴリズムでデータを暗号化または復号するために使用される情報の一部です。
    
*   国立標準技術研究所（NIST）：様々な標準仕様を定義し、公開する米国政府機関。NISTの一部書である、コンピューターセキュリティリソースセンター（CSRC）は一連の連邦情報処理規格（FIPS）を公開しています。これらの標準規格は米国政府機関のみに義務付けられていますが、多くの国がデファクトのグローバルスタンダードと認識しています。
    
*   非人間エンティティ（NPE）：機能を実行するため、他のプログラム、デバイスまたはサービスの能力を利用するハードウェアとソフトウェアファームウェア（例、デバイス）の1位となる組合せ。非人間エンティティは、独立してまたは認証された個人や他のNPEに代わって行動することができます。 [^3]
    
*   Online Certificate Status Protocol（OCSP）：クライアントが、CRLをダウンロードするのではなく、個別の証明書のすてーたうを認証局や検証局に問い合わせることを可能にするプロトコル。
    
*   Path Discovery and Validation（PDVal）：証明書が有効であり、検証者から信頼されているかを決定するプロセス。
    
*   暗証番号（PIN）：一般的にソフトウェアまたはハードウェア内の秘密鍵コンテナを解錠するために利用される数値シークレット。
    
*   個人特定証明（PIV）：公開鍵基盤に基づいて全ての政府職員および契約業者に強力な認証を可能にするように設計された米国政府制度。
    
*   秘密鍵：単一のエンティティが排他的、プライベートに管理する鍵。秘密鍵は、エンティティがデータの暗号化または署名検証のために共有している公開鍵に対応しています。
    
*   公開鍵：エンティティが公開して配布している鍵。公開鍵は、エンティティが排他的、プライベートに管理している秘密鍵に対応しています。
    
*   公開鍵証明書：公開鍵、秘密鍵保持者の1つ以上の識別子、認証局の識別子およびセキュリティ要件をサポートする追加のメタデータを含む証明書。
    
*   公開鍵基盤：公開鍵と秘密鍵のペアおよび証明書に基づくトラストを管理するために設計されたツール、標準仕様および関連するポリシーのセット。
    
*   登録局（RA）：登録および身元確認を、証明書を受け取るエンティティに提供し、証明書の発行と更新のプロセスを管理する個人、システムまたはビジネス機能。RAの最も重要な責任は身元確認と秘密鍵のアイデンティティへのバインディングです。
    
*   失効：失効とは、クライアントがとある個別の証明書をこれ以上信頼すべきではないと通知することです。
    
*   ロール：権限のセット。ロールは個々のユーザーに紐づけられなければならず、そしてユーザーはロールに紐づけられたときに紐づいている認可を取得します。
    
*   RSA：巨大な素数に基づく非対称暗号。略称であるRSAは、3人の主要な開発者であるRon Rivest、Adi ShamirおよびLen Adlemanを指します。
    
*   S/MIME：非対称暗号を利用したデジタル署名されたまたは暗号化されたメッセージの構築と送信のための標準仕様。
    
*   Secure Socket Layer（SSL）：通信中のデータの暗号化に関する非推奨の標準仕様；TLSはこれにとって代わりました。
    
*   Server-based Certificate Validation Protocol（SCVP）：クライアントが証明書が有効で信頼できるかを決定するためにサーバーへ問い合わせを可能にするプロトコル。サーバーは発行をおこなったCAと紐づく必要はありません。SCVPは以下の2つを実施します；(1) SCVPは末端エンティティと信頼できるルートの間のパスを決定しますが、クライアントは中間CAをイン来する必要はありません。 (2) SCVPはポリシーに基づいてパスの検証の委譲も実行します。
    
*   署名：完全性を保証するため、暗号アルゴリズムを用いてデータを処理すること。
    
*   サブジェクトの別名：EメールアドレスまたはUser Principal Name（UPN）のようにアプリケーション固有の識別子を伝達するために証明書発行者が利用する証明書サブジェクトのための1つ以上の識別子。
    
*   Subject Distinguished Name（サブジェクトDN）：認証局の範囲内でのサブジェクトの一意の識別子。発行者は、サブジェクトDNをLDAPエントリ名のように構造化します。
    
*   Transport Layer Security（TLS）：2つのエンドポイント間の通信の機密性と完全性を提供するために設計された暗号プロトコル。
    
*   X.509：公開鍵証明書のエンコーディングのための基本的なルールを定義するX.500シリーズのISO標準規格。
    
*   検証者：証明書を検証し、やり取りの中で他の当事者が秘密鍵を管理することを確認するエンティティ。
    

@row
## Basics of PKI for Identity Practitioners

@column
## アイデンティティ実務者のためのPKIの基礎

@row
### What is PKI

_PKI_ stands for " _Public Key Infrastructure,_ " a set of interlocking standards and technologies that support the secure exchange of public keys for _asymmetric cryptography_ use cases.

Originally developed as part of the X.500 series of specifications for electronic directory services, the _X.509_ standard proposed a way to link a public key into a universal, hierarchical directory designed to support OSI networks.

The OSI protocol is, for all intents and purposes, dead. However, the X.500 specification lives on in simplified form as LDAP, and X.509 has found a second life in the modern Internet.

PKI is woven deeply into the fabric of the Internet, and it supports the following critical Internet capabilities:

*   _TLS_ as a general encryption layer for application protocols
    
*   _S/MIME_ as a standard for secure email
    
*   _IPsec_ as a standard for virtual private networking (VPN), which depends upon PKI via the Internet Key Exchange (IKE) extension
    
*   Some commercial software or services, such as Adobe Acrobat, Microsoft Word, or DocuSign, support digital signatures for non-repudiation or integrity protection. In Europe, qualified signatures and time stamps have official legal standing, recognized in the Electronic Identification, Authentication, and Trust Services (eIDAS) framework.
    

This article is not a general primer on PKI; it provides a minimal overview of PKI as it relates to identity Management and identifies critical issues relevant to identity Practitioners. Interested readers are referred to the references section at the end for more detail.

Here are some excellent resources to learn more about PKI in general:

Books:

*   [_Applied Cryptography, by Bruce Schneier,_](https://www.schneier.com/books/applied-cryptography/) is a classic guide to the cryptographic technology underlying PKI and its applications. For those who want to know everything about this subject, this is the place to start.
    

Online Resources

*   The US Federal government has deployed PKI widely for both logical and physical access. IDManagement.gov maintains information about the Federal PKI here: [_https://playbooks.idmanagement.gov/fpki/_](https://playbooks.idmanagement.gov/fpki/)
    
*   Bruce Schneier, the author of Applied Cryptography, maintains a fascinating and helpful blog here: https://www.schneier.com/
    

Standards:

*   [_X.509_](https://www.itu.int/rec/T-REC-X.509-201910-I/en) : The original specification for PKI certificates. This document must be purchased.
    
*   [_RFC 5280_](https://datatracker.ietf.org/doc/html/rfc5280) : The Internet X.509 Public Key Infrastructure Certificate and Certificate Revocation List (CRL) Profile standard specifies a subset of the X.509 standard for use on the Internet.
    

@column
### PKIとは何か

_PKI_ は「 _Public Key Infrastructure_ 」を表し、 _非対称暗号_ ユースケースのための公開鍵の安全な交換をサポートする関連した標準仕様と技術のセットです。

元々は電子ディレクトリサービスのためのX.500仕様シリーズの一部として開発された _X.509_ 標準仕様はOSIネットワークをサポートするように設計されたユニバーサルな階層ディレクトリに公開鍵を紐づける方法を提案しました。

OSIプロトコルはどう考えても死にました。しかし、X.500標準仕様はLDAPのような単純な形式として生き残っており、X.509は現代のインターネットにおいて第二の人生を見つけました。

PKIはインターネットの構造に深く組み込まれおり、以下の重要なインターネットの機能をサポートしています：

*   _TLS_ はアプリケーションプロトコルのための一般的な暗号化レイヤーです
    
*   _S/MIME_ はセキュアなEメールの標準仕様です
    
*   _IPsec_ はVirtual Private Networking（VPN）のための標準仕様で、Internet Key Exchange（IKE）拡張を通じてPKIに依存しています
    
*   Adobe Acrobat、Microsoft WordやDocuSignのような一部の商用ソフトウェアやサービスは、否認防止または完全性の保護のためにデジタル署名をサポートしています。欧州では、適切な署名やタイムスタンプが、Electronic Identification, Authentication, and Trust Services（eIDAS）フレームワークにおいて正式な法的地位を有しています。
    

この記事は、PKIの一般的な入門書ではありません；本記事は、アイデンティティ管理に関連するPKIの最小限の概要を提供し、アイデンティティ実務者が関わる極めて重大な問題を特定します。興味のある読者は、さらに詳しい内容のために本記事末尾の参考セクションを参照してください。

一般的にPKIについてさらに学ぶ素晴らしいリソースがここにあります：

書籍：

*   [_Applied Cryptography, by Bruce Schneier,_](https://www.schneier.com/books/applied-cryptography/) is a classic guide to the cryptographic technology underlying PKI and its applications. For those who want to know everything about this subject, this is the place to start.
    

オンラインリソース：

*   The US Federal government has deployed PKI widely for both logical and physical access. IDManagement.gov maintains information about the Federal PKI here: [_https://playbooks.idmanagement.gov/fpki/_](https://playbooks.idmanagement.gov/fpki/)
    
*   Bruce Schneier, the author of Applied Cryptography, maintains a fascinating and helpful blog here: https://www.schneier.com/
    

標準仕様：

*   [_X.509_](https://www.itu.int/rec/T-REC-X.509-201910-I/en) : The original specification for PKI certificates. This document must be purchased.
    
*   [_RFC 5280_](https://datatracker.ietf.org/doc/html/rfc5280) : The Internet X.509 Public Key Infrastructure Certificate and Certificate Revocation List (CRL) Profile standard specifies a subset of the X.509 standard for use on the Internet.
    

@row
### How do a 'Private Key' and a 'Public Key Certificate' Provide Authentication Assurance

@column
### 「秘密鍵」と「公開鍵証明書」が認証の保証をどのように提供するのか

@row
#### Public and Private Keys

Private and _public keys_ are random numbers, but not just any random

number.

- In the _RSA_ specification, keys are derived from a large prime number.

- In _ECC,_ keys are related to points along a particular elliptical curve.

By taking some data, such as text or an image, and plugging the data

into a specific equation with one of the numbers (keys), you create a

scrambled version of the data that only the other number (key) can

unscramble. This concept is the basis of asymmetric cryptography.

The _private key's_ owner must retain and closely guard it since a foundational assumption in PKI is that only the authorized user controls the private key. The public key, by contrast, can be widely shared.

A sender can scramble a message using the public key to send a message only the private key's owner can read. Because the private key is the only key that can unscramble and read the message, the sender knows that the message can only be read by the private key owner. [^4]

The owner of a private key can use it to scramble a message, and a recipient can only unscramble the message with the public key. The recipient can be sure that the private key owner sent the message and that it has not been modified in transit. [^5]

In asymmetric cryptography, “ _encryption”_ refers to scrambling data with the public key, and “ _signature”_ refers to scrambling data with the private key.

In practice, signature and encryption are much more complicated, involving cryptographic hashes or intermediate symmetric keys. For our purposes, it is sufficient to understand that private keys sign and public keys encrypt.

![Illustration of Encryption and Signature path for a document](PKI.jpg)

Despite the widespread use of PKI for highly secure credentials, asymmetric cryptography does not directly provide authentication! Authentication protocols that leverage PKI credentials depend on signature or encryption.

In public-key authentication schemes, the user is whoever has control of the private key. When a system wishes to authenticate a private key owner, it requires them to use the private key they own. The user can sign something with the private key that the system can verify with the public key or decrypt something with the private key that the system encrypts with the public key.

The user can provide a signed message for the authenticating system to verify, or the authenticating system can generate and encrypt data that the user can only decrypt with their private key. In both scenarios, possession of the private key, demonstrated by the ability to use the private key to decrypt or sign data, proves the user's identity.

@column
#### 公開鍵と秘密鍵

秘密鍵と _公開鍵_ はランダムな数値ですが、単なるランダムな数値ではありません。

- _RSA_ 仕様では、鍵は巨大な素数に由来します。

- _ECC_では、鍵は特別な楕円曲線に沿った点に関係します。

テキストや画像のようなあるデータを取り出し、そのデータを数字（鍵）のひとつと特定の方程式に差し込むことで、もう一方の数字（鍵）だけがスクランブルを解除できるスクランブル化されたデータを作成します。このコンセプトが非対称暗号の基礎となっています。

PKIの基礎となる前提は、認可されたユーザーだけが秘密鍵を制御するということであるため、 _秘密鍵の_ 所有者は秘密鍵を保持し、厳重に守らなければなりません。対照的に、公開鍵は広く共有できます。

送信者は公開鍵を使ってメッセージをスクランブル化することで、秘密鍵の所有者だけが送信されたメッセージを読むことができます。秘密鍵がメッセージのスクランブル化を解除し、読むことができる唯一の鍵であるため、送信者はメッセージを読むことができるのは秘密鍵の所有者だけであることを知っています。 [^4]

秘密鍵の所有者は秘密鍵をメッセージのスクランブル化に使うことができ、受信者は公開鍵によってのみスクランブル化の解除ができます。この受信者は、秘密鍵所有者がこのメッセージを送ったこととメッセージが通信途中で変更されていないことを確認することができます。 [^5]

非対称暗号では、「 _暗号化_ 」は公開鍵によるデータのすくらんぶるかを指し、「 _署名_ 」は秘密鍵によるデータのスクランブル化を指します。

実際には、署名と暗号化はもっと複雑で、暗号ハッシュまたは中間共有鍵を含みます。本書の目的では、秘密鍵が署名をおこない、公開鍵が暗号化をおこなうという理解で充分です。

![Illustration of Encryption and Signature path for a document](PKI.jpg)

高セキュリティクレデンシャルのためのPKIが幅広く利用されているにも関わらず、非対称暗号は直接的に認証を提供することはありません。PKIクレデンシャルを活用する認証プロトコルは、署名または暗号化に依存しています。

公開鍵認証スキームにおいて、ユーザーはだれでも秘密鍵の制御をおこないます。システムが秘密鍵所有者を認証したい場合、所有者自身が持っている秘密鍵の利用を要求します。ユーザーは秘密鍵によって何かに署名し、システムは公開鍵によって検証またはシステムが公開鍵によって暗号化した未必鍵によって何かを復号します。

ユーザーは認証システムが検証するために署名されたメッセージを提供し、もしくは認証システムはユーザーがその秘密鍵によってのみ複合できるデータを生成および暗号化します。両方のシナリオで、データの復号または署名のために秘密鍵を利用する能力があることを示ことで、秘密鍵の所持がユーザーのアイデンティティを証明します。

@row
#### Public Key Certificates

So far, we have seen how to authenticate a user if you have their public key. The challenge that remains is finding a reliable way to exchange public keys.

We have solved this problem in several ways with different protocols and systems. Many modern authentication protocols, including FIDO, Verifiable Credentials, and passkeys, leverage public/private keys and asymmetric cryptography. Every protocol requires an out-of-band process that links the public key with a public identifier. In some contexts, notably in the SSH public-key authentication protocol or "Web of Trust" based systems like PGP, pre-existing relationships or pre-provisioned authorizations are sufficient.

In the context of complex modern business processes where you are unlikely ever to meet the majority of people you interact with, users cannot simply exchange keys directly. After all, in the absence of some way to verify the identity of the individual providing you with a public key, you have no way to distinguish between your intended counterparty and an imposter.

PKI solves this issue by relying on the concept of a "trusted third party." In a PKI, a central trusted authority vouches for identities according to a documented process. This centralized authority introduces scalable trust by allowing users to verify the identity of previously unknown users or systems. The users rely on the centralized authority to enforce an identity registration and lifecycle management process. The mechanism used in PKI to convey this assurance is the public-key certificate.

For every participant to have confidence in distributed business transactions, each participant must have confidence in the identity of every other participant. For asymmetric encryption to support business applications, the public key must be connected, or "bound," to the participant's identifier. In PKI, public key certificates are the artifacts that connect a public key and an identifier.

A _public key certificate_ contains several critical pieces of

information. For authentication purposes, the following three fields are the most important:

- The public key

- One or more identifiers associated with a user

- Information about the “trusted third party” that vouches for the association

between the key and the identifier.

![Left, key components of a PKI certificate that support Identity. ](/assets/images/idpro_bok/80-image1.png) ![Right, a detailed listing of several possible elements of a PKI certificate.](/assets/images/idpro_bok/80-image2.png)

Figures 1 and 2: Key components of a PKI certificate that support identity including Name, key, metadata, signature algorithm, and signature. Additionally, a detailed listing of several possible elements of a PKI certificate.

A public key certificate is a file with a prescribed structure defined by the X.509 v3 standard and refined by RFC 5280. It contains the user's public key, their identifiers, and important metadata about the certificate itself. [^6] The file is digitally signed using the private key of a trusted third party, called a "Certificate Authority."

@column
#### 公開鍵証明書

ここまで、ユーザーの公開鍵を所有しているときのユーザーを認証する方法について見てきました。残っている課題は、公開鍵を交換する信頼できる方法を見つけることです。

様々なプロトコルとシステムで、いくつかの方法によってこの問題を解決しました。FIDO、検証可能なクレデンシャルおよびパスキーを含む多くの現代の認証プロトコルでは、公開鍵/秘密鍵および非対称暗号を活用します。全てのプロトコルが、公開鍵と公開識別子を紐づける帯域外のプロトコルを要求します。一部のコンテキストでは、特にSSH公開鍵認証プロトコルまたはPGPのような「Web of Trust」をベースにしたシステムでは、既存の信頼関係または事前にプロビジョニングされた認可で充分です。

やり取りをおこなう人々の大多数に会ったことがないような、複雑な現代のビジネスプロセスのコンテキストでは、ユーザーは単純に直接鍵の交換をすることはできません。結局、公開鍵を提供する個人のアイデンティティの検証方法がないことには、意図した相手と偽物を区別する方法もありません。

PKIは「信頼できる第三者」の概念によってこの問題を解決します。PKIにおいて、中央の信頼される機関が文書化されたプロセスによってアイデンティティを保証します。この中央集権された機関は、以前は未知であったユーザーまたはシステムのアイデンティティをユーザーが検証できるようにすることでスケーラブルなトラストを導入します。ユーザーは、アイデンティティ登録とライフサイクル管理のプロセスを実行する中央集権された機関に依存します。この保証を伝達するためにPKIで利用されるメカニズムが、公開鍵証明書です。

全ての参加者が分散ビジネストランザクションにおいて信頼を有するためには、全ての参加者が他の全ての参加者のアイデンティティに信頼を持たなければなりません。ビジネスアプリケーションを支える非対称暗号のため、公開鍵は参加者の識別子に紐づけされる、つまり「バインド」される必要があります。PKIでは、公開鍵証明書は、公開鍵とアイデンティティが紐づける成果物です。

_公開鍵証明書_ はいくつかの重要な情報の断片が含まれます。認証のためには、以下の3つのフィールドが最も重要でです：

- 公開鍵

- ユーザーに紐づく1つ以上の識別子

- 鍵と識別子の紐付けを保証する「信頼された第三者」に関する情報

![Left, key components of a PKI certificate that support Identity. ](image1.png) ![Right, a detailed listing of several possible elements of a PKI certificate.](image2.png)

Figures 1 and 2: Key components of a PKI certificate that support identity including Name, key, metadata, signature algorithm, and signature. Additionally, a detailed listing of several possible elements of a PKI certificate.

公開鍵証明書は、X.509 v3標準仕様によって定義され、RFC 5280によって洗練された所定の構造を持つファイルです。公開鍵証明書はユーザーの公開鍵、その識別子および証明書自体の重要なメタデータを含みます。 [^6] このファイルは「認証局」と呼ばれる信頼された第三者の秘密鍵を使ってデジタル署名されています。

@row
### Who Can Get a Certificate

Any business process participant who can generate and store a private

key and associated public key may receive a certificate. The most common recipients of certificates are listed here:

- Humans: A human being can receive a public key certificate that names them individually.

- _Non-person entities:_ Examples of non-person entities include devices like routers, software services like web or email servers, IoT devices, and other non-human entities like software providers who digitally sign software packages.

- _Roles:_ Sometimes, a person may act in a role, such as "Software Release Manager" or "Doctor on call." A certificate authority can issue a certificate that identifies the user's role, allowing them to authenticate in the persona of that role. Role certificates are issued to individuals and contain a personal identifier for the person holding the private key to maintain individual accountability. Everyone with a role certificate has a unique private key.

- _Groups:_ In some exceptional cases, several people share a private key. In this case, a certificate authority can issue a certificate to a group. The certificate will identify the group, and the group members will take additional security precautions to ensure that only authorized members use the private key.

@column
### 誰が証明書を取得できるのか

秘密鍵および対応する公開鍵を生成、保管できるビジネスプロセス参加者はだれでも証明書を受け取ることができるでしょう。最も一般的な証明書の受信者は以下にリスト化します：

- 人間：人類は自分の名前が個別に記載された公開鍵証明書を受け取ることができます。

- _非人間エンティティ_：非人間エンティティの例には、ルーターのようなデバイス、WebやEメールサービスのようなソフトウェアサービス、IoTデバイスまたはソフトウェアパッケージにデジタル署名をおこなうソフトウェアプロバイダーのような非人間エンティティが含まれます。

- _ロール_：時折、人間は「Software Release Manager」や「Doctor on call」のようなロールを果たすことがあります。認証局は証明書を発行し、ユーザーのロールを特定し、ユーザーがそのロールのペルソナで認証することを許可します。ロールの証明書は個人に発行され、個人の説明責任を維持するために秘密鍵を持つその人の個人識別子を含みます。ロールの証明書を持つ全ての人はユニークな秘密鍵を有しています。

- _グループ_：一部の例外ケースでは、何人かが1つの秘密鍵を共有します。このケースでは、認証局はグループに証明書を発行します。証明書はグループを特定し、グループメンバーは認可されたメンバーだけが秘密鍵を利用することを保証するため、追加セキュリティ予防措置を設けます。

@row
### How Are PKI Certificates Like Other Credentials, and How Are They Different?

Users can authenticate themselves with a private key and corresponding PKI Certificate, like other credentials.

*   The trustworthiness of the credential depends on the identity proofing and issuance process as much as it depends on cryptographic math. As with other credentials, the identity assurance level for authenticated users is low if the proofing or issuance processes are insecure or the user does not protect the private key.
    
*   Like other credentials, a private key and certificate are a single authentication factor that enterprises can supplement with additional factors. Typically, we consider a key and certificate "something you have" and often supplement it with a PIN, Password, or biometric.
    

PKI credentials have many unique properties not shared by most other authentication credentials.

**A public-key certificate file contains all the information necessary**

**to authenticate the subject:**

For most other credential types, each authentication challenge requires the involvement of the credential issuer. When a user enters a password, the authenticating system must check it against the directory or database where the user created their account. By contrast, PKI authentication can occur without directly interacting with the issuing Certificate Authority. The user generally activates the private key with a secret, such as a PIN or a password, but his secret is entered directly into the software or device containing the private key; the user does not provide it to the Certificate Authority.

**Public key certificates are long-life credentials:**

Certificates may be valid for a much longer-term than is typical for other credential types. It is common for a certificate authority to issue a public key certificate to a user with a three-year lifetime. This extended lifetime is acceptable because the private key credential is not user-selected and is too long to be easily memorized or copied by humans.

**Key protection affects the overall security of the PKI credential:**

Like any other authentication secret, the user must protect a private key from third parties to prevent the third party from impersonating the user. Recall that in public-key cryptography, the user is whoever controls the private key. For this reason, it is essential to ensure that private keys cannot be copied or taken without a user's awareness and permission. Because private keys are usually very long and appear random, they cannot be memorized and must be stored.

Several technologies are available to protect private keys, including _Hardware Security Modules (HSMs)_ or personal tokens such as the YubiKey Security Key or SafeNet eToken Smart Card. The United States _National Institute of Standards and Technology (NIST)_ has published a standard, _Federal Information Processing Standard (FIPS) 140,_ and has implemented the _Cryptographic Module Validation Program (CMVP)_ to ensure that HSMs implement proper cryptographic algorithms and key protections for private keys.

The security properties of PKI credentials mean they can provide a higher level of identity assurance than other kinds of credentials. Governments reserve the highest levels of assurance defined by governments for PKI certificates stored on smart cards. This security comes at a price in terms of direct costs and additional complexity.

**PKI credentials can support additional use cases beyond interactive**

**authentication:**

While passwords, OTP, and other credentials are limited to interactive authentication, PKI credentials are suitable for transactions that are not immediate and interactive. One example is a digital signature, where the recipient of a signed message must know the signer's identity, but the signer may not know who will verify the signature. Encryption is another case where the encryptor of the sensitive data must ensure that the intended recipient is the only one who will have access even when data is exchanged out-of-band and asynchronously. PKI can enable capabilities such as S/MIME, Qualified Signatures, and others that cannot be supported by credentials that only provide authentication.

@column
### 他のクレデンシャルとPKI証明書がどのように似ているか、そしてどのように異なっているか？

他のクレデンシャルどのように、ユーザーは秘密鍵と対応するPKI証明書を使って自身を認証することができます。

*   クレデンシャルの信頼性は、暗号数学に依存するのと同様に身元確認と発行プロセスに依存します。他のクレデンシャルと同じく、身元確認プロセスまたは発行プロセスが安全ではない場合またはユーザーが秘密鍵を保護しなかった場合、認証されたユーザーのアイデンティティ保証レベルは低くなります。
    
*   他のクレデンシャルと同様に、秘密鍵と証明書は企業が追加の認証要素で保管できる単一の認証要素です。通常、鍵と証明書を「所持しているもの」とみなし、しばしばPIN、パスワードや生体認証によって補完します。
    

PKIクレデンシャルは、他のほとんどの認証クレデンシャルとは異なる多くの独自の性質を持っています。

**公開鍵証明書ファイルは必要な全ての情報を有している**

**主体の認証のため：**

他のほとんどのクレデンシャルタイプにとって、認証チャレンジはそれぞれクレデンシャル発行者の関与を必要とします。ユーザーがパスワードを入力する場合、認証システムはユーザーがアカウントを作成したディレクトリまたはデータベースに対してパスワードをチェックしなくてはなりません。対照的に、PKI認証は発行をおこなった認証局に直接やり取りすることなく発生します。一般的にユーザーはPINやパスワードのようなシークレットを使って秘密鍵を有効化しますが、そのシークレットは秘密鍵を有しているソフトウェアやデバイスに直接入力されます；ユーザーは認証局にシークレットを提供することはありません。

**公開鍵証明書は長期間のクレデンシャル：**

証明書は他のクレデンシャルタイプの一般的な有効期限よりもはるかに長く有効かもしれません。一般的に、認証局がユーザーに3年の有効期間を持つ公開鍵証明書を発行します。秘密鍵クレデンシャルはユーザー選択ができず、人間が容易に記憶またはコピーするには長すぎるため、この長い有効期間は許容されます。

**鍵の保護はPKIクレデンシャルのセキュリティ全てに影響します：**

他の認証シークレットと同様に、第三者がユーザーになりすますことを避けるため、ユーザーは第三者から秘密鍵を保護しなければなりません。公開鍵暗号について思い返すと、ユーザーは秘密鍵を管理している人です。この理由から、ユーザーの認識および許可がない状態で、秘密鍵がコピーされたり、持ち出されたりができないように保証することが不可欠です。通常、秘密鍵は非常に長く、ランダムに見えるため、秘密鍵を記憶することはできず、保管しなければなりません。

秘密鍵の保護のため、いくつかのテクノロジーが利用でき、 _ハードウェアセキュリティモジュール（HSM）_ やYubiKey Security KeyまたはSafeNet eToken Smart Cardのようなパーソナルトークンなどが存在します。米国 _国立標準技術研究所（NIST）_ は、HSMが適切な暗号アルゴリズムおよび秘密鍵のための鍵の保護を実装していることを保証するため、標準仕様 _連邦情報処理規格（FIPS） 140_ を公開し、 _暗号モジュール認証制度（CMVP）_ を実装しました。

PKIクレデンシャルのセキュリティ特性は、PKIクレデンシャルが他の種類のクレデンシャルに比べてより高いレベルのアイデンティティ保証を提供できることを意味します。政府は、スマートカード上に保管されるPKIクレデンシャルのためのガバナンスによって定義された最高レベルの保証を確保しています。このセキュリティは、直接的なコストと複雑さの追加という点で代償をともないます。

**PKIクレデンシャルは対話型の認証を超えた追加のユースケースをサポートできます：**

パスワード、OTPやその他クレデンシャルは対話型の認証に制限される一方で、PKIクレデンシャルは即時および対話型ではないやり取りに適しています。一例としてデジタル署名の例を挙げると、署名されたメッセージの受信者は署名者のアイデンティティを知らなければなりませんが、署名者は誰が署名を検証するかを知らない可能性があります。他のケースとして暗号化では、機密データの暗号化の実行者はデータが帯域外および非同期に交換されたとしても意図した受信者だけがアクセスできることを保証しなければなりません。PKIはS/MIME、適格電子署名など、認証を提供するだけのクレデンシャルではサポートできないその他の機能を可能にします。

@row
### Factors and Problems Limiting PKI Adoption

The roots of PKI extend back to the 1970s, and the earliest versions of the Secure Sockets Layer (SSL) standard cemented its use as the basis for secure communication in the mid-1990s. However, despite its maturity and widespread use for some specific use cases, it has yet to see broad adoption for authentication of individuals, either for business-to-consumer or business-to-employee use cases. There are many reasons why PKI has yet to see widespread adoption outside these narrow use cases, though the technology and vendor support has improved. The following are some of the most significant challenges hindering adoption:

**Enterprise key management is challenging:**

For PKI to be a trustworthy and secure authentication approach, the private key must be controlled exclusively by the authentication subject. As we said earlier, the user is whoever controls the private key. There are two ways to ensure that the intended user is the only one with access to the private key. The authentication subject must generate the private key within a protected software environment, or the CA must generate the private key on the subject's behalf and then pass it to the subject using a secure transfer mechanism. Both processes are complex and challenging to automate without extensive tooling.

Internet software providers have focused on providing automation for critical technical use cases, such as TLS for Web Servers. Protocols like _Automatic Certificate Management Environment (ACME)_ and services like Let's Encrypt provide zero-touch key management and certificate rotation for web servers. These services do not support the management of certificates issued to humans.

Vendors, meanwhile, have implemented sophisticated, proprietary solutions for the automation of key management. Microsoft Active Directory Certificate Services can provide key management and certificate services for machines and human users in an Active Directory environment. The Entrust Certificate Authority provides a client-side tool to manage the lifecycle of keys and certificates for clients. However, these tools and others like them are tied to a specific product and are part of a closed, proprietary system.

Other providers, like KeyFactor or Venafi, can provide certificate lifecycle services for a mix of CA products. However, these tools are proprietary and may require significant integration efforts.

**PKI has poor usability:**

As discussed above, key management is a complex organizational and technical issue with its share of challenges. Unfortunately, many PKI implementations require end-users to manage much of that complexity. Notably, users must initiate the key generation and request process. Once a user generates a private key and the CA issues a certificate, the user must configure all of their tools (operating system, web browser, mail client, etc.) to use the private key generated by the user and manage the list of trusted certificate issuers. Sophisticated enterprises with dedicated engineering teams should be able to handle this complexity on behalf of the user community. Still, this complexity is difficult to manage even in highly controlled environments. This complexity is unmanageable for most small businesses and home users.

One way to address this user challenge is to have a designated administrator or security officer who assists users in generating their private keys and initializing their tokens. This approach is widespread in large enterprises and can also be feasible for smaller companies.

In high-security environments, users and administrators generate private keys on a hardware security module. This hardware requirement adds device driver installation and management issues to the other problems confronting users attempting to use PKI for authentication. Some platform vendors have implemented platform-level API (e.g., Microsoft CAPI). Still, support for this API is not universal, with some applications implementing proprietary or platform-neutral key storage systems that do not integrate with the host OS.

As with many IDM technologies, enterprises should observe the 80/20 rule. IDM professionals should ensure that critical or widespread user applications support your PKI implementation and accept alternative credentials for essential legacy applications.

**Public key enablement of applications is hard:**

We have discussed the difficulty of using PKI for authentication from the perspective of Authentication Subjects. Enabling applications to consume PKI credentials is even more challenging in some ways:

1.  The list of trusted certificate issuers must be maintained and synchronized across all applications where the user may need to authenticate.
    
2.  Applications must validate certificates, which requires the applications to access a public HTTP site or LDAP directory to obtain Certificate Revocation information.
    
3.  A local user profile must be created in the application based on an identifier present in the certificate or entered by the user during a manual registration process.
    

There is no concept of provisioning or de-provisioning built into PKI by default, so applications must implement this capability through a separate integration with the Registration Authority (RA). Since it is common for users to authenticate with a site directly, CAs rarely offer this capability. Identity professionals should leverage existing directory technologies, such as Active Directory, to support user profiles for multiple applications.

For internally-facing enterprise applications, an IGA system may manage these aspects. Across enterprise boundaries or in a B2C context, this additional complexity makes PKI credentials difficult and expensive compared to other authentication technologies.

**Certificate trust path discovery and validation are complex and existing**

**implementations have inconsistent behavior:**

In the previous section, we discussed applications needing to validate the certificates. This validation is complicated, even when administrators configure applications to use a static Trust List of known good issuers. [^7] To complicate things further, PKI supports a form of federation through cross-certification, discussed below in more detail. In this section, we will note that determining whether a trusted partner issued a certificate in a federated or cross-certified environment is very challenging.

_Path Discovery and Validation (PDVal)_ is complex. Different vendors

implement it inconsistently. One application may treat a certificate as valid, while another application may reject the same certificate, depending on the underlying certificate validation library. Some third-party solutions support consistent PDVal across products, but they must be implemented and integrated with each endpoint. This burden has made enterprises leery of implementing PKI on the server side.

@column
### PKI採用を制限する要素と問題

PKIのルーツは1970年代までさかのぼり、Secure Sockets Layer（SSL）の初期バージョンが1990年代半ばまでに安全な通信の基礎としてPKIの利用を定着させました。しかし、PKIの成熟と一部の特定のユースケースでのその利用の広がりにも関わらず、PKIは企業-消費者や企業-従業員のユースケースにおける個人の認証として未だに広く採用されてはいません。技術やベンダーサポートが向上しているにも関わらず、PKIが狭い範囲のユースケース以外では未だに広く採用されていない理由は多くあります。採用を妨げている最も重要な課題は以下です：

**企業の鍵管理が困難である：**

PKIが信頼でき、安全な認証アプローチであるためには、秘密鍵は認証主体によって排他的に制御されなければなりません。前述のとおり、ユーザーは誰であれ秘密鍵を制御します。意図したユーザーだけが秘密鍵にアクセスすることを保証するための方法が2つあります。認証主体は保護されたソフトウェア環境内で秘密鍵を生成しなければならず、またはCAが主体に代わって秘密鍵を生成して安全な転送メカニズムを使って秘密鍵を主体に渡さなければなりません。これらプロセス両方が項かなツールなしに自動化することは複雑で困難です。

インターネットソフトウェアプロバイダーは、WebサーバーのためのTLSのような重要な技術ユースケースのための自動化を提供することに注目していました。 _Automatic Certificate Management Environment（ACME）_ のようなプロトコルやLet's Encryptのようなサービスは、鍵管理に全く関与せず、Webサーバーのための証明書ローテーションを提供します。これらのサービスは人間に発行された証明書の管理をサポートしていません。

一方、ベンダーは鍵管理の自動化のために洗練されたプロプライエタリなソリューションを実装しています。Microsoft Active Directory Certificate ServicesはActive Directory環境にあるマシンと人間のユーザーのための鍵管理と証明書サービスを提供できます。Entrust Certificate Authorityは、クライアントのための鍵と証明書のライフサイクルを管理するためのクライアントサイドツールを提供します。しかし、これらのツールやこれらに似た他のツールは特定の製品に紐づいていたり、クローズドなプロプライエタリシステムの一部です。

KeyFactorやVenafiのような他のプロバイダーは、CA製品の組み合わせる証明書ライフサイクルサービスを提供できます。しかし、これらのツールはプロプライエタリであり、統合に多大な労力を必要とするかもしれません。

**PKIはユーザビリティが悪い：**

上で議論したように、鍵管理は複雑な組織的および技術的な問題があり、課題があります。残念ながら、多くのPKI実装はエンドユーザーにその大きな複雑さを管理することを要求します。特筆すべきことは、ユーザーは鍵の生成とリクエストの処理を開始しなければなりません。ユーザーは秘密鍵を生成し、CAが証明書を発行したとき、ユーザーはユーザーが生成した秘密鍵を利用し、信頼された証明書発行者のリストを管理するためにすべてのツール（オペレーティングシステム、Webサーバー、メールクライアントなど）を設定しなければなりません。専門のエンジニアリングチームを持つ洗練された企業は、ユーザーコミュニティに代わってこの複雑さを処理することができるはずです。それでも、高度に制御された環境においてでもこの複雑さの管理は困難です。この複雑さはほとんどの小規模な企業とホームユーザーにとっては管理不可能です。

このユーザーの課題に対処する1つの方法は、秘密鍵の生成とトークンの初期化においてユーザーを助ける指名された管理者またはセキュリティオフィサーを用意することです。このアプローチは大企業では広まっており、小規模な会社でも実現可能です。

高セキュリティ環境では、ユーザーと管理者はハードウェアセキュリティモジュール上で秘密鍵を生成します。このハードウェア要件は、認証のためにPKIを使おうとするユーザーが直面する問題に、デバイスドライバーのインストールと管理の問題を追加します。一部のプラットフォームベンダーは、プラットフォームレベルのAPI（例、Microsoft CAPI）を実装しています。それでも、このAPIのサポートはユニバーサルではなく、一部のアプリケーションによってはホストOSと統合しないプロプライエタリまたはプラットフォームニュートラルな鍵保管システムを実装しています。

多くのIDM技術と同様に、企業は80/20の法則を守るべきです。IDM専門家は重要なまたは広く普及しているユーザーアプリケーションがPKI実装をサポートしていることを確認し、重要なレガシーアプリケーションのために代替となるクレデンシャルを受け入れるようにすべきです。

**アプリケーションの公開鍵有効化は困難である：**

認証主体の観点から、認証のためにPKIを利用することの難しさについて議論してきました。アプリケーションがPKIクレデンシャルを有効にすることは、ある意味でさらに困難です：

1.  信頼された証明書発行者のリストはメンテナンスされ、ユーザーが認証する必要があるであろうすべてのアプリケーション間で同期されていなければなりません。
    
2.  アプリケーションは、証明書失効情報を取得するためにアプリケーションが公開されたHTTPサイトまたはLDAPディレクトリにアクセスすることを要求する証明書を検証しなければなりません。
    
3.  ローカルユーザープロファイルは、証明書に提示されている識別子または手動登録プロセス中にユーザーによって入力された識別子に基づいて、アプリケーションで生成されなければなりません。
    

デフォルトでは、PKIが組み込まれたプロビジョニングまたはデプロビジョニングの概念は存在しないため、アプリケーションは登録局（RA）による個別の統合を通じてその機能を実装しなければなりません。ユーザーがサイトで直接認証することが一般的であるため、CAがこの機能を提供することは稀です。アイデンティティの専門家はActive Directoryのような既存のディレクトリ技術を活用し、複数アプリケーションのためのユーザープロファイルをサポートするべきです。

内部向けの企業アプリケーションためえ、IGAシステムはこれらの側面を管理することがあるかもしれません。企業の境界を超える場合やB2Cの場合、この追加の複雑さが他の認証技術と比べてPKIクレデンシャルを難しく、高価なものにします。

**証明書トラストパスディスカバリーと検証は複雑であり、既存の実装は一貫性のない動作をする：**

前のセクションで、証明書を検証する必要のあるアプリケーションについて議論しました。この検証は複雑であり、管理者が既知の正当な発行者の静的な信頼リスト [^7] を使うようにアプリケーションを設定したとしてもです。これをさらに複雑にするのは、PKIが後述のクロス証明書を通じてフェデレーションされる形式をサポートしています。このセクションでは、フェデレーションされたまたはクロス証明された環境において信頼されたパートナーが証明書を発行したかどうかを決めることが非常に困難であることに注意してください。

_Path Discovery and Validation（PDVal）_ は複雑です。ベンダーごとにその実装は一貫していません。あるアプリケーションは証明書を正当と判定するかもしれない一方で、有している証明書検証ライブラリに依存して別のアプリケーションは同じ証明書を拒否するかもしれません。一部のサードパーティーソリューションは製品間で一貫したPDValをサポートしますが、各エンドポイントでそれらを実装および統合しなければなりません。この負荷は企業がサーバーサイドにPKIを実装することを慎重にさせます。

@row
## Unique Considerations for Identity Practitioners

@column
## アイデンティティ実務者のための独自の考慮事項

@row
### Ensure that PKI is the Right Fit for Your Requirements

Deployment of PKI involves several complexities and difficulties outlined in this document. However, PKI is a powerful tool that can offer strong authentication and support other use cases, such as email signing/encryption, that are impossible with other strong authentication credentials. When considering the deployment of PKI, ensure that the use cases you can support justify the added complexity for your environment and your users.

For TLS and link encryption, PKI may be the best or only choice, but

that does not necessarily mean that you should implement your own local

PKI. A third-party PKI service provider is an excellent alternative for most organizations.

@column
### PKIが要件に正しく適合していることを確認する

PKIの導入はこの文書で概説したいくつかの複雑さと困難が含まれています。しかし、PKIは強い認証を提供し、Eメールの署名/暗号化のような他の強力な認証クレデンシャルでは実現できない認証以外のユースケースをサポートするパワフルなツールです。PKIの導入を検討するとき、サポートできるユースケースが環境とユーザーにとって複雑さが増されることを正当化できることを確認してください。

TLSとリンク暗号化について、PKIは最も良いそして唯一の選択肢かもしれませんが、必ずしも独自ののローカルPKIを実装する必要はありません。サードパーティーPKIサービスプロバイダーはほとんどの組織にとって優れた代替手段です。

@row
### The Importance of Planning

If you determine that an internally managed PKI is the correct choice for your organization, planning is critical for a successful PKI deployment. While the need for planning is not unique to PKI, the complexity of a PKI environment can make retroactive cleanup much more complex than careful up-front planning and deployment. As with any Identity Management technology, planning is critical to success.

@column
### 計画の重要性

内部管理されているPKIが組織にとってただしい選択であることを決定した場合、計画はPKI導入の成功に重要です。計画の必要性はPKIに固有ではありませんが、PKI環境の複雑性は、入念な事前の計画と導入よりも後始末のほうがはるかに複雑になりえます。アイデンティティ管理テクノロジーと同様に、計画は成功に不可欠です。

@row
### IGA and PKI

Enterprises that leverage Identity Governance and Administration tools may need to expand their toolkit to accommodate PKI credentials. Existing IGA tools can manage accounts and privileges but may not track the PKI credentials associated with the managed accounts. It is important to recall that a PKI certificate and private key represent self-contained credentials that are still valid even if the underlying account has been deactivated or deleted. Unless the certificate is revoked or has expired, external applications may still accept a PKI credential as valid.

The challenges of managing non-human accounts such as machines, IoT devices, Bots, or other entities also apply to certificates issued to non-person entities. Refer to “Non-human Account Management (v3)” by Graham Williamson, André Koot, and Gloria Lee for information about unique issues related to these entities. [^8] The section below, ‘Machine Identities and Certificate Management Systems,’ discusses machine identities in more detail.

Many CAs include management capabilities to address these challenges. Some third-party (Certificate Management System) CMS products interact with multiple CA products to provide a single pane of glass for certificate management in a multi-vendor multi-CA environment. A later section discusses these products in more detail.

@column
### IGAとPKI

アイデンティティガバナンスと管理ツールを活用する企業は、PKIクレデンシャルに対応するようにツールキットを拡張する必要があるかもしれません。既存のIGAツールはアカウントと特権を管理しますが、管理しているアカウントに紐づくOKIクレデンシャルを追跡できない可能性があります。PKIクレデンシャルと秘密鍵は自己完結型のクレデンシャルを表し、これは対象のアカウントが非活性化または削除されたときでも有効であることを思い出すことが重要です。証明書が失効しなかったり、有効期限が切れなかったりするかぎり、外部のアプリケーションは依然としてPKIクレデンシャルが有効であるとして受け入れます。

マシン、IoTデバイス、ぼっとやその他エンティティのような非人間アカウントを管理するという課題は、非人間エンティティに発行された証明書にも適用されます。これらのエンティティに関係する固有の問題に関する情報のため、Graham Williamson、André KootとGloria Leeによる「Non-human Account Management (v3)」を参考にしてください。 [^8] 以下のセクション、「マシンアイデンティティと証明書管理システム」ではマシンアイデンティティについてより詳細に議論しています。

多くのCAはこれらの課題に対処する管理能力を有しています。一部のサードパーティー（証明書管理システム）CMSは、マルチベンダー・マルチCA環境において証明書管理のためのシングルペイン・オブ・グラスを提供するために、複数のCA製品と相互連携しています。後続のセクションでこれらの製品についてさらに詳しく議論しています。

@row
### Lifecycle Management of PKI Certificates Compared to Other Credentials

Modern cryptographic algorithms ensure that private keys cannot be easily guessed. For example, a _classical (non-quantum) computer_ would need about 300 trillion years to break a 2048-bit RSA key, while the same computer would require an average of five sextillion seven hundred eighty-three quintillion + years to guess a 128-bit ECC key.

However, the security of an overall system rarely depends exclusively on math.

The overall security of a PKI system includes several variables, including unreliable humans. CAs issue end entity certificates for a relatively short time, such as 90 days for public SSL certs or up to years for human subscriber certificates. CA certificates may be valid for as long as 20 years. This lifetime is much longer than a typical password or other credentials because the private key is never directly presented during authentication. The CA must store its private keys in a Hardware Security Module to ensure that an attacker cannot copy them.

Because CAs issue certificates with a fixed lifetime, key management can become a significant challenge. Enterprises should deploy a Certificate Management System (CMS) to monitor certificates and automate the renewal process or provide notification when a renewal is required. Most CA products include a rudimentary management console, but CMS products can offer a single pane of glass to manage multiple CAs from different vendors. CMS systems can also provide Service Desk support tools for assisting in smartcard registration and forgotten/locked PIN issues.

As with any other type of credential, a certificate may become invalid before it expires for various reasons. A user may leave the organization, change roles, or lose access to the private key. PKI provides for the revocation of public-key certificates in this case. The list of "no longer trusted" certificates is called the Certificate Revocation List (CRL). In every certificate, the CA publishes a URL where the CRL can be found. Alternative protocols, such as the Online Certificate Status Protocol (OCSP), offer other means of checking the validity of a certificate. Most web browsers have implemented proprietary revocation-checking techniques.

A third technology, called Server-based Certificate Validation Protocol (SCVP), has been developed and documented in a standard but has not been widely implemented. It is mentioned here for completeness, but most enterprises can disregard SCVP.

Because a certificate passes between the subject and a third party without involving the original issuer of the certificate, it is imperative that applications correctly validate certificates and check the revocation information.

@column
### 他のクレデンシャルと比較したPKI証明書のライフサイクル管理

現代の暗号アルゴリズムは秘密鍵が簡単に推測できないことを保証します。例えば、 _古典的（非量子）コンピューター_ は2048ビットRSA鍵を破るのに約300兆年必要とされている一方で、同じコンピューターで128ビットECC鍵を推測するために平均で 57垓8300京年以上必要とされています。

しかし、システム全体のセキュリティが数学だけに依存することは稀です。

PKIシステム全体のセキュリティには、信頼できない人間のようないくつかの変数が含まれます。CAは、公開SSL証明書では90日間、人間のサブスクライバー証明書には最長で数年の比較的短期間のエンドエンティティ証明書を発行します。CA証明書は有効期間は20年にもなることがあります。秘密鍵は認証中に直接提示されることはないため、この有効期間は一般的なパスワードや他のクレデンシャルよりも非常に長いです。CAは、攻撃者が秘密鍵をコピーできないことを保証するため、ハードウェアセキュリティモジュールに秘密鍵を保管しなければなりません。

CAが固定の有効期間を持つ証明書を発行するため、鍵管理は大きな課題になります。企業は、証明書の監視、更新プロセスの自動化または更新が必要なときに通知を送るため、証明書管理システム（CMS）を採用すべきです。ほとんどのCA製品は、基本的な管理コンソールが含まれていますが、CMS製品は異なるベンダーからの複数のCAを管理するためのシングルペイン・オブ・グラスを提供できます。CMSシステムは、スマートカード登録とPINを忘れた/ロックされたという問題を支援するサービスデスクサポートツールも提供できます。

他の種類のクレデンシャルと同じく、証明書は様々な理由によって有効期限の前に無効になる可能性があります。ユーザーが組織を離れたり、ロールを変えたり、秘密鍵へのアクセス権を失ったりするかもしれません。このケースでは、PKIは公開鍵証明書を失効させます。「もはや信頼できない」証明書のリストは証明書失効リスト（CRL）と呼ばれます。全ての証明書では、CAがCRLを発見できるURLを公開しています。Online Certificate Status Protocol（OCSP）のような代替プロトコルをは、証明書の正当性を確認する別の方法を提供しています。ほとんどのWebブラウザはプロプライエタリな失効確認技術を実装しています。

第三の技術、Server-based Certificate Validation Protocol（SCVP）と呼ばれます、は開発され、標準仕様として文書化されていますが、広く実装されてはいません。念のため述べておきますが、ほとんどの企業はSCVPは無視できます。

証明書の元の発行者なしに主体とサードパーティーの間で証明書を受け渡すので、アプリケーションは証明書を正しく検証し、失効情報を確認することが不可欠です。

@row
### Options for Identifiers in Public Key Certificates

The primary purpose of the certificate, as described above, is to link a public key with a user identifier. Of course, a user may have several identifiers for different use cases. Rather than issuing separate certificates for each user identifier, the PKI specification supports including multiple identifiers in a single certificate.

The primary user identifier in a certificate is the Subject Distinguished Name (Subject DN). The Subject DN must be structured like an LDAP Distinguished Name. Typically, there will be a "Base DN" shared by all certificates issued from a Certificate Authority and one or more "Relative DNs" which differentiate certificate subjects. Common relative DNs include "Organization" and "Organizational Unit." Finally, the certificate lists a subject's unique identifier. This identifier can take several forms, such as "Common Name," usually a user's Legal Name. In large PKI deployments, users with frequently seen names may have other

identifiers embedded or appended to their names to distinguish between

users with the same legal name. The common name is not the only possible identifier for a user in a Subject DN. Certificates can also use UID or email address to identify a certificate subject.

Because the Subject DN must mimic an LDAP Distinguished Name, it is very restrictive. For this reason, certificates often use an additional field instead. The “ _Subject Alternative Name”_ field is a much more flexible option to encode different user identifiers. It allows multiple names to be encoded and does not mandate a particular structure. Common uses for the subject alternative name field include:

*   Email address to support S/MIME digital signature and encryption
    
*   UPN to support smartcard login on the Windows platform
    
*   Hostname to support TLS connections
    

The Subject Alternative Name does not impose any constraints on the type of identifiers that can be encoded. So, in addition to all of the previously listed identifiers, private communities of interest may insert identifiers that have strictly local meaning into this field. An example is the _Federal Agency Smart Credential Number (FASC-N),_ which is part of the US Federal Government's Personal Identity Verification (PIV) standard.

Generally, Enterprises should use the subject alternative name for the user or machine identifiers. The Subject DN must be unique but should not contain multiple identifiers or non-standard ID types.

@column
### 公開鍵証明書における識別子の選択肢

上述のように、証明書の主な目的はユーザーの識別子と公開鍵を紐づけます。当然、ユーザーは異なるユースケースにとっていくつかの識別子を有することがあります。各ユーザー識別子に対して別の証明書を発行するのではなく、PKI仕様は単一の証明書に複数の識別子を含むことに対応しています。

証明書の主なユーザー識別子はSubject Distinguished Name（Subject DN）です。Subject DNはLDAP Distinguished Nameのように構造化されていなければなりません。通常認証局から発行される全ての証明書で共通の「Base DN」と、証明書主体を区別する1つ以上の「Relative DNs」があります。一般的なRelative DNsは「Organization」と「Organizational Unit」を含みます。最終的に、証明書は主体のユニーク識別子をリスト化しています。この識別子は「Common Name」、通常ユーザーの法的な名前のようないくつかの形式をとることができます。大規模なPKI導入において、よくある名前のユーザーは、同じ法的な名前を持っているユーザーと区別するためにその名前に他の識別子を埋め込んだり、付加したりすることがあります。「Common Name」はSubject DNにおいてユーザーのための唯一の識別子ではありません。証明書はUIDまたはEメールを使って証明書主体を識別することもできます。

Subject DNはLDAP Distinguished Nameを模倣しなければならないため、非常に制限されています。この理由により、証明書はしばしば代わりに追加のフィールドを利用します。「 _Subject Alternative Name_ 」フィールドは異なるユーザー識別子をエンコードするためのはるかに柔軟なオプションです。これは複数の名前をエンコードすることができ、特定の構造を義務付けるものではありません。Subject Alternative Nameフィールドの一般的な使い方は以下の通りです：

*   S/MIMEデジタル署名および暗号化をサポートするEメールアドレス
    
*   Windowsプラットフォーム上でスマートカードログインをサポートするUPN
    
*   TLS接続をサポートするホスト名
    

Subject Alternative Nameは、エンコードできる識別子の種類に制約を課すことはありません。そのため、先に挙げた識別子の全てに加え、利害関係のある民間コミュニティは、厳密にローカルな意味のある識別子をこのフィールドに追加できます。米国連邦政府個人特定証（PIV）標準の一部である _Federal Agency Smart Credential Number（FASC-N）_ がその例です。

一般的に、企業はユーザーまたはマシンの識別子のためにSubject Alternative Nameを使うべきです。Subject DNはユニークでなければならず、複数の識別子や非標準の種類のIDを含むべきではありません。

@row
### Machine Identities and Certificate Management Systems

While PKI has not seen widespread adoption as a credential for people,

it is dominant as a credential for machines, thanks to its use in TLS. TLS is not only used to provide secure access to web servers in end-user browsers; it is also widely used as a tunneling technology in machine-to-machine or site-to-site communication.

Virtualization and containerization technologies and the use of cloud providers have exploded in recent years. For this reason, the number of PKI-based machine identities is increasing exponentially. Managing and tracking the keys and associated certificates is becoming a significant challenge.

A Certificate Management System is an increasingly critical tool for enterprises to deploy to avoid service outages due to expired certificates, especially for enterprises with hybrid-cloud-based infrastructure or multi-vendor server environments.

@column
### マシンアイデンティティと証明書管理システム

PKIは人々にクレデンシャルとして広く採用されているわけではない一方で、TLSでの利用のおかげで、マシンのクレデンシャルとして支配的です。TLSはエンドユーザーブラウザにWebサーバーへの安全にアクセスを提供するためだけに使われているわけではありません；マシン間またはサイト間の通信におけるトンネル技術としても広く使われています。

仮想化およびコンテナ化技術とクラウドプロバイダーの利用は、近年爆発的に広がっています。このため、PKIに基づくマシンアイデンティティの数は指数関数的に増加しています。鍵と関連する証明書を管理し、追跡することは大きな課題になります。

証明書管理システムは、特にハイブリッドクラウドベースのインフラストラクチャまたはマルチベンダーサーバー環境において、証明書の有効期限が切れることによるサービス停止を避けるため、導入することが企業にとって重要になってきているツールです。

@row
### Federated Authentication and PKI

We have already seen a critical difference between PKI and other credentials - a user can authenticate to an external application without involving the issuing authority in every transaction. This property can simplify authentication flows but places a greater burden on external applications since they validate the certificate themselves.

For an external application to consume certificates issued by your certificate authority, the application must trust your certificate authority. There are two basic ways for an application to trust an external certificate authority: explicit trust using certificate trust lists or implicit trust based on cross-certification.

Explicit trust is the most commonly used approach. In this model, applications explicitly managed trusted issuers within static Certificate Authority Trust Lists (CTL). The location of the trust lists will vary from product to product and system to system. A Java virtual machine, the Windows Operating System, and most web server software all maintain individual trust lists. Synchronizing them all in an Enterprise environment can be a very complex challenge. If you leverage an internal PKI, a CMS product can automate much of the management of disparate trust stores. Vendors typically configure standard software packages to trust the more prominent commercial Certificate Authorities. This is another good reason to acquire certificates from these sources.

Implicit trust relies on a technique known as cross-certification. In cross-certification, a CA will issue a certificate to another CA, typically operated by a different organization. From the perspective of an application validating certificates, the external CA appears to be another internal CA connected to the CA issuing the cross-certificate. The promise of cross-certification is that it dynamically allows applications to discover trust relationships between independently operated certificate authorities. In practice, however, the inconsistent behavior of PDVal implementations in software validating trust relationships between CA has prevented the promise of cross-certification from being fully realized. For most enterprises, cross-certification is not a helpful tool for federated authentication.

Finally, Identity Federation technologies can simplify the implementation of cross-domain trust by providing assertions across enterprise boundaries rather than relying directly on crossPDVal. The certificate can be validated within enterprise boundaries using relatively straightforward reliance on trust lists and local revocation publication. An SSO product can provide a federated token to external applications. This will address the interactive authentication use case but will not solve the challenges associated with other use cases that PKI can support, such as secure email encryption and signature or digital signatures for documents.

@column
### フェデレーションされた認証とPKI

全てのトランザクションにおいて発行機関が関与することなく、ユーザーが外部のアプリケーションに認証することができる、PKIと他のクレデンシャルとの大きな違いをこれまで見てきました。この性質は認証フローをシンプルにすることができますが、外部アプリケーション自体が証明書を検証するため、外部アプリケーションに大きな負担をかけます。

あなたの認証局によって発行された証明書を利用する外部アプリケーションにとって、アプリケーションはあなたの認証局を信頼しなければなりません。アプリケーションが外部の認証局を信頼するためには2つの基本的な方法があります：証明書トラストリストを使う明示的な信頼またはクロス認証による暗黙的な信頼です。

明示的な信頼は最も一般的に使われるアプローチです。このモデルでは、アプリケーションが静的な認証局トラストリスト（CTL）内で信頼された発行者を明示的に管理します。トラストリストの位置は、プロダクトおよびシステムによって異なります。Java仮想マシン、WindowsオペレーティングシステムおよびほとんどのWebサーバーソフトウェアはすべて個別のトラストリストを管理しています。企業環境においてそれらすべてを同期することは非常に複雑な課題です。内部PKIを利用する場合、CMS製品は異なるトラストストアの管理の多くを自動化します。ベンダーは通常、より有名な商用の認証局を信頼するように標準ソフトウェアパッケージを設定します。これは、これらのソースから証明書を取得するもう一つの良い理由です。

暗黙的な信頼は、クロス認証と知られる技術に依存します。クロス認証において、CAは通常、他の組織によって運用されている他のCAに証明書を発行します。アプリケーションが証明書を検証する観点から、外部CAはクロス証明書を発行しているCAに接続された他の内部CAに見えます。クロス証明の約束は、独立して運用される認証局間の信頼関係をアプリケーションに動的に発見させることです。しかし、実際には、CA間の信頼関係を検証するソフトウェアのPDVal実装の動作の一貫性のなさは、クロス認証の約束が完全に実現されることを妨げます。ほとんどの企業にとって、クロス認証はフェデレーションされた認証にっても役立つツールではありません。

最終的に、アイデンティティフェデレーション技術は、クロスPDValに直接依存するよりも企業の境界を超える証明を提供することによって、クロスドメイントラストの実装を単純化できます。証明書を、トラストリストとローカル失効公開に比較的単純に依存することで、企業の境界内で検証できます。SSO製品は、外部認証にフェデレーションされたトークンを提供できあmす。これは、対話型の認証ユースケースに対処しますが、安全なEメール暗号化および署名、またはドキュメントのデジタル署名のようなPKIがサポートできる他のユースケースに紐づく課題を解決はしません。

@row
## Conclusion

PKI is a powerful but complex tool for highly-secure authentication. It is likely already used within your environment for NPE or machine identities. Identity professionals should investigate the tools and processes used by individual programs to minimize redundancy of effort and cost.

Carefully weigh the benefits of the use cases within your environment before committing to deploying the technology to end users. If you choose to deploy PKI, avoid the temptation to introduce local or proprietary extensions, and stick to widely supported standards.

If an enterprise identity management environment is needlessly complex, it significantly complicates PKI deployment. Before deploying PKI, or any other complex authentication technology, ensure that identity management tools and practices are rationalized and streamlined within the enterprise environment.

If you introduce PKI for end-users, consider deploying a Certificate Management System to track the lifecycle of keys and certificates across your entire domain.

@column
## 結論

PKIは安全性の高い認証にとって、強力ですが複雑なツールです。環境内でNPEまたはマシンアイデンティティに既に利用されている可能性があります。アイデンティティ専門家は、労力とコストの重複を最小限にするため、個別のプログラムによって使われるツールとプロセスを調査すべきです。

エンドユーザーにテクノロジーを展開する前に、環境内のユースケースでの利益を慎重に検討しましょう。PKIを導入することｗ選択した場合、ローカルまたはプロプライエタリな拡張を導入する誘惑を避け、広くサポートされている標準にこだわりましょう。

企業のアイデンティティ管理環境が皮膚つように複雑な場合、PKIの導入が非常に複雑になります。PKIまたはほかの複雑な認証技術を導入する前に、アイデンティティ管理ツールとプラクティスが企業環境内で筋が通っており、合理的であることを確認しましょう。

エンドユーザーにPKIを導入する場合、ドメイン全体で鍵と証明書の有効期間を追跡するために証明書管理システムを導入することを検討してください。

@row
## Author Bio

Robert Sherwood is the Principal Consultant at Credentive Security, a boutique consulting firm focused on Identity Strategy and Architecture.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2021-09-30 | V1 published |
| 2022-12-15 | V2 published; content significantly updated |

- - -

[^1]:  Note that credential assurance is distinct from identity assurance. Identity assurance measures how well you verified the identity of the account holder and how securely you connected the identity to the credential at the time of issuance. Credential assurance measures how confident you can be that the credential subject has maintained control over the credential, and that the credential has not been compromised. 
    
[^2]:  Glazer, I., (2020) “Identifiers and Usernames”, _IDPro Body of Knowledge_ 1(1). doi: [https://doi.org/10.55621/idpro.16](https://doi.org/10.55621/idpro.16) . 
    
[^3]:  Williamson, G. & Koot, A. & Lee, G., (2022) “Non-human Account Management (v3)”, _IDPro Body of Knowledge_ 1(7). doi: [https://doi.org/10.55621/idpro.52](https://doi.org/10.55621/idpro.52) 
    
[^4]:  Technically, the sender generates a symmetric key, encrypts the message with the symmetric key, and then encrypts the symmetric key with the intended recipient’s public key. 
    
[^5]:  Technically, digital signing appends a 'hash' to the document that can be deciphered by the sender's public key - ensuring the sender's identity. 
    
[^6]:  International Telecommunications Union – Technology (ITU-T), _X.509 : Information technology - Open Systems Interconnection - The Directory: Public-key and attribute certificate frameworks_ , October 2019, [https://www.itu.int/rec/T-REC-X.509](https://www.itu.int/rec/T-REC-X.509) . 
    
[^7]:  For example, see this article on how browsers handle revocation checks: [https://www.ssl.com/blogs/how-do-browsers-handle-revoked-ssl-tls-certificates/](https://www.ssl.com/blogs/how-do-browsers-handle-revoked-ssl-tls-certificates/) . 
    
[^8]:  Williamson, Koot, and Lee, “Non-Human Account Management (v3).” 
