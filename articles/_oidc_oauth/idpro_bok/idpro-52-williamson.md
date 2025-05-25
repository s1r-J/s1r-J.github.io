---
layout: columns
title: Non-Human Account Management (v4)
permalink: /docs/oidc_oauth/idpro_bok/52
date: 2024-09-09
aside:
  toc: true
tags: ["IDPro", "IDPro BoK", "システムアカウント", "IoT", "ボット", "非人間", "サーバーアカウント", "サービスアカウント"]
---

IDPro Body of Knowledgeの翻訳メモです。

元記事：[https://bok.idpro.org/article/id/52/](https://bok.idpro.org/article/id/52/)

[IDPro Body of Knowledgeの翻訳メモのトップページ](/docs/oidc_oauth/idpro_bok)

@row
## Abstract

Non-human accounts are often the “Achilles’ heel” of a robust IAM environment. While IAM professionals concern themselves with managing identities, authentication, RBAC, ABAC, governance, and auditing of user accounts, other IT staff are deploying devices and services that are given access to protected resources via hard-wired accounts, exposed services, and APIs.

The management of non-human account control should be consistent with user-based account management, and controls placed on user account access to high-assurance applications should also be applied to non-human accounts.

There is no single solution for dealing with non-human accounts. Some IAM professionals suggest all accounts should be managed via the same processes and same infrastructure to ensure consistent policy deployment. This consistency, they argue, should ensure that non-human accounts are not ‘left-out’ when IAM deployments occur. Others consider this impractical and recommend that purpose-specific processes be deployed for non-human accounts. But regardless of the mechanism(s) used to manage non-human accounts, ensuring that they are managed is paramount. Otherwise, non-human accounts will continue to be a cybersecurity attack vector favored by hackers for gaining access to corporate facilities.

Keywords: System accounts, IoT, Bots, Non-Human, server accounts, service accounts

@column
## 概要

非人間アカウントはしばしば堅牢なIAM環境の「アキレス腱」となります。IAMの専門家はアイデンティティ、認証、RBAC、ABAC、ガバナンス、およびユーザーアカウントの監査の管理に注意していますが、他のITスタッフはハードに紐づいたアカウント、公開されたサービスおよびAPIを介して保護されたリソースへのアクセスを許可するデバイスとサービスをデプロイしています。

非人間アカウント制御を管理することはユーザーベースのアカウント管理と一貫性があるべきであり、高保証アプリケーションにアクセスするユーザーアカウントに対する制御は非人間アカウントにも適用すべきです。

非人間アカウントを扱う単一のソリューションはありません。一部のIAMの専門家は、ポリシーの一貫したデプロイを保証するため、すべてのアカウントが同じプロセスおよび同じインフラストラクチャを介して管理されるべきと提案しています。彼らの主張しているのは、この一貫性はIAMデプロイが発生したとき非人間アカウントが「取り残される」ことがないはずだということです。他の人たちはこれが非現実的と考え、非人間アカウントのために目的に応じたプロセスをデプロイすることを推奨しています。しかし、非人間アカウントの管理に使うメカニズムに関わらず、それらが確実に管理されることが重要です。そうでなければ、非人間アカウントは企業の設備にアクセスするためにハッカーが好んで利用するサイバーセキュリティ攻撃ベクトルであり続けるでしょう。

Keywords: システムアカウント、IoT、ボット、非人間、サーバーアカウント、サービスアカウント

@row
By Graham Williamson, André Koot, Gloria Lee

© 2023 IDPro, Graham Williamson, André Koot, Gloria Lee

@row
## Introduction

A non-human account is usually associated with a service or device rather than a human user. An example is a machine-to-machine service, such as a backup routine that runs during non-business hours to create an offline copy of production data. In this instance, the account permissions should be restricted, i.e., they should not have standard user access nor general Administrator privileges.

Devices such as sensors that provide data to be monitored are sometimes deployed with access to an account so that they can write to a database. Again, such an account should have limited privileges.

Fortunately, the use of such accounts is diminishing as the use of APIs becomes more sophisticated, providing better security and eliminating the practice of hardcoding usernames and passwords in connection routines.

While IAM professionals typically focus on user accounts, these non-human accounts represent a potential attack vector for organizations. These accounts should be considered when formulating policies for access to computer systems.

A comparison between the characteristics of these accounts is shown below:

|     | Person Identity | Non-human Identity |
| --- | --- | --- |
| Usage | Multi-faceted, must accommodate multiple access requirements to many applications or protected resources | Purpose-specific, with a single requirement for each deployment |
| Lifecycle | Created during the ‘joiner’ process, modified when ‘moves’ occur, continually monitored for compliance, disabled, and then deleted according to the ‘leaver’ process. [^1] | Created on deployment of the device/service, deleted on termination. |
| Access control | Dynamic – continual risk-assessed authentication matched to the assurance level requirements of the requested application or protected resource. MFA is used for authentication elevation. | Static – determined at the time of account creation. No MFA requirement. |
| Access  <br>endpoints | Users typically access computer services from smartphones, PCs, and laptops on an interactive basis. | Endpoints are typically devices or device controllers. They can also be computer applications, service routines, or Internet bots. |

_Table 1 - Account type characteristics_

There are two broad categories of non-human accounts that IAM practitioners should differentiate:

*   Machine-to-machine accounts used by devices or services to perform a specific function; these ‘server’ accounts should be monitored and alarm on any incident that is an anomaly to the expected operation.
    
*   Accounts that have access to system functions but are not assigned to a specific individual; these ‘system’ accounts include administrator accounts with elevated privileges.
    

@column
## イントロダクション

非人間アカウントは通常、人間のユーザーではなく、サービスまたはデバイスに関連付けられます。例としては、プロダクションデータのオフラインコピーを作成するために業務時間外に実行するバックアップルーティーンのようなマシンツーマシンサービスです。この例では、アカウントのパーミッションは制限されるべきです、つまり標準的なユーザーアクセスや一般的な管理者権限は付与すべきではありません。

監視用のデータを提供するセンサーのようなデバイスは、データベースへの書き込みができるアカウントへのアクセス権を付与してデプロイされることがあります。また、このようなアカウントは権限を制限すべきです。

幸いなことに、APIの利用がより洗練され、良いセキュリティが提供され、接続ルーティーンでユーザー名とパスワードをハードコーディングする習慣がなくなることで、このようなアカウントの利用は減っています。

IAM専門家は通常ユーザーアカウントに焦点を当てますが、これらの非人間アカウントが組織に対して潜在的な攻撃ベクトルを示します。コンピューターシステムへのアクセスポリシーを策定するとき、これらのアカウントを考慮すべきです。

これらのアカウントの特性の比較を以下に示します：

|     | 人間アイデンティティ | 非人間アイデンティティ |
| --- | --- | --- |
| 用途 | 多面的であり、多くのアプリケーションまたは保護されたリソースに対する複数のアクセス要件に対応しなくてはならない | 目的に特化し、各デプロイごとに単一の要件がある |
| ライフサイクル | 「Joiner」プロセスで作成され、「Mover」が発生すると変更され、コンプライアンスが継続的に監視され、無効化され、「Leaver」プロセスに従って削除される。[^1] | デバイス／サービスのデプロイで作成され、終了時に削除される。 |
| アクセス制御 | 動的 - 要求されたアプリケーションまたは保護されたリソースの保証レベル要件にあったリスク評価に基づく継続的な認証。認証の昇格にMFAが利用される。 | 静的 – アカウント作成時に決定される。MFAの要件はない。 |
| アクセス<br>エンドポイント | 一般的に、ユーザーはスマートフォン、PCおよびラップトップからインタラクティブにコンピューターサービスにアクセスする。 | 一般的に、エンドポイントはデバイスまたはデバイスコントローラーである。またはコンピュータアプリケーション、サービスルーティーン、またはインターネットボットもなりうる。 |

_表1 - アカウント種別ごとに特性_

IAM実務者が区別すべき2つの大きな非人間アカウントのカテゴリがあります：

*   特定の機能を実行するためのデバイスまたはサービスによって使用されるマシンツーマシンアカウント；これら「サーバー」アカウントは監視し、期待される操作と比べて移譲なインシデントが発生したときにアラームを発生させるべきです。
    
*   システム機能にアクセスでき、特定の個人に割当されていないアカウント；これらの「システム」アカウントは、昇格された権限を持つ管理者アカウントを含みます。
    

@row
### Terminology

*   Bot – sometimes called an Internet bot, short for ‘robot’ but referring to a software routine that performs automated tasks over the Internet, a web robot referring to an autonomous network application, or simply a ‘bot’ referring to an automated, typically repetitive, task used for a specific purpose.
    
*   Identity – defining attributes for a human user that may vary across domains, e.g., a user’s digital identity will have a different definition in a work environment as opposed to the user’s bank. A device identifier is sometimes referred to as its identity.
    
*   CIA Triad - the fundamental Information security concepts of risk classification of resources from the perspectives of Confidentiality, Integrity, and Availability.
    
*   Non-human/person account – any account not used by a person, including accounts used for devices, services, and servers.
    
*   Server account – an account established with access rights to a specific server operation; this includes service accounts used by a computer application to access another application or service or an account used for a device connection. Note: these accounts are username accounts typically secure via a password.
    
*   System account – a generic term for a privileged account that has extensive permissions that enable system configuration changes.
    

@column
### 用語解説

*   ボット - インターネットボットと呼ばれることもあり、「ロボット」の省略ですが、インターネット上で自動タスクをを実行するソフトウェアルーティーンを指し、ウェブロボットは自律ネットワークアプリケーションを指し、または単に「ボット」は特定の目的のために自動化された、一般的には反復的なタスクを指します。
    
*   アイデンティティ - 人間のユーザーの属性を定義しているものであり、ドメインごとに変化している可能性があり、例えば職場環境とユーザーの銀行ではユーザーのデジタルアイデンティティは定義が異なるでしょう。デバイス識別子はアイデンティティと呼ばれることがあります。
    
*   CIAトライアド - 機密性、完全性および可用性の観点からリソースのリスクを分類する基本的な情報セキュリティ概念。
    
*   非人間／非人物アカウント - 人間によって利用されるアカウントではなく、デバイス、サービス、およびサーバーのために利用されるアカウントを含みます。
    
*   サーバーアカウント - 特定のサーバー運用にアクセス権を付与されて確立されたアカウント；これには、コンピューターアプリケーションによって使用され、他のアプリケーションやサービスにアクセスするサービスアカウントや、デバイス接続のために使用され得るアカウントを含みます。注意：通常、これらのアカウントはパスワードによって保護されたユーザー名アカウントです。
    
*   システムアカウント - システム設定変更を可能にする広範なパーミッションを持つ特権アカウントの総称。
    

@row
## Non-human Access Control

A significant concern for the IAM practitioner is how to manage access control to and from devices, particularly with services not used interactively by humans. This includes bots that are increasingly being used for automated processes.

@column
## 非人間アクセス制御

IAM実務者にとって重要な懸念点は、デバイス間のアクセス制御、特に人間が対話的に使用しないサービスにおいてをどのように管理するか、です。これには、自動化プロセスで利用が増えているボットを含みます。

@row
### IoT Devices

IoT devices can be either a sensor or an actuator. In some cases, sensors provide a continuous stream of data that is displayed in real-time or discrete readings that are written to a database for periodic analysis. Actuators are devices typically used to control a process, turning something on or off. They may be used to open or close a valve by pulsing a servo motor a sufficient number of times until the desired aperture is reached. In many cases, devices are remotely located and connected via a controller to the supervisory system located in a central location. It is noted that IoT devices are becoming increasingly sophisticated with control capabilities and communication facilities built-in. This eliminates the need for a username/password account as IoT devices typically communicate to an API with encryption and digital signing functionality.

In a typical IoT configuration, there are three zones:

1.  IoT devices (sensors & actuators). Managing access to and from devices should be governed by a policy that imposes requirements for encryption of the communications channel, such as DNP3, MQTT, and/or digital signature technology (e.g., PKI), to suit the required security level. In low-security environments, static passwords might be used that remain in service until the equipment is decommissioned. In higher-sensitive applications, the security credentials (passwords, certificates, etc.) will be periodically rotated. The selected security requirement must match the capability of the devices, but technical limitations often constrain IoT devices. “Terminology for Constrained-Node Networks" (RFC 7228) nominates three classes of devices: [^2]
    
    1.  Class 0 – no capacity to support configurable authentication.
        
    2.  Class 1 – limited capacity for key management, token support, etc.
        
    3.  Class 2 – fully configurable and able to support dynamic authentication mechanisms.
        
2.  The Controller (to which the devices are connected). If sensor device data is aggregated by a device controller that maps each sensor or actuator to its control logic, providing access control to actuators and protection on writing collected data to a database is required (see Service Accounts, below).
    
3.  Human-Machine interface application (HMI) such as a controller app or a SCADA app monitoring or controlling the IoT devices. In some cases, sensors will write data directly to a database that is read by another application, such as a SCADA app or similar human-machine interface (HMI). Access to these applications will be by humans and should be managed via the IDM environment.
    

Historically IoT environments have been managed by a team responsible for operational technology (OT) and have had little to do with the information technology (IT) environment within an organization. The specialist nature of IoT technology has justified this organizational structure, and it is often corporate policy to isolate OT from potential compromise via the IT environment. But the requirement for isolation is diminishing as security technology improves. Integrating IoT systems with the IAM environment will improve access control capabilities and provide better corporate governance over operational technology deployments for most industrial applications.

If allowed by regulatory controls, best practice is to integrate the OT environment with the IT IAM environment. This enables the OT to set system entitlements via the IAM system and for OT staff to use their corporate credentials for authorization, potentially via a Privileged Access Management system.

There is increasing concern regarding the provenance of IoT devices and tracking devices throughout the supply chain to ensure no modifications have been made that could potentially deploy ‘back-door’ access. [^3] The IAM practitioner may wish to ensure corporate policy defines the certification processes to be employed for IoT devices and ensure that compliance with software supply chain policy is in place. This is increasingly important in regulated industries.

Just as important as securing the device itself is protecting the IoT device data. In many cases, databases with IoT devices are not adequately secured. A risk management approach should be employed to determine the adequacy of protection; building environment device data might be low risk but plant production data that is not adequately protected from industrial espionage might be considered critical. The IAM professional should ensure appropriate access controls are placed on industrial data stores. It is good practice to assign a data controller role to an industrial database.

Vulnerability Mitigation

There is no ‘correct answer’ when it comes to deciding the involvement of IAM practitioners in the management of IoT devices. At one end of the spectrum is the use case whereby all IoT deployments and management are the domain of OT personnel. In this case, the IAM involvement will be restricted to the human accounts that access the OT systems. Group management of entitlements to accounts that can configure IoT systems will heighten the level of security.

At the midpoint of the spectrum, components of the IoT configuration and operation will fall under IAM services. The IAM provisioning workflow will route configuration requests and potentially password rotation requests, to the responsible person. The IoT devices will participate in both attestation reporting to the responsible manager and compliance management with integration to the Security Operations Center (SOC) and possibly the Security Information and Event Management (SIEM) system.

At the other end of the spectrum, the provisioning of devices is included in the identity management infrastructure. IoT devices are treated the same way as individuals, applying a ‘digital identity’ to devices. Their entitlements can be set via the normal account provisioning workflows, and their access control can use the same protocols. Most modern API systems, including gateways, use OAuth 2.0 for machine-to-machine communications, while Open ID Connect can be appropriate for IoT device controller authentication. [^4]

@column
### IoTデバイス

IoTデバイスは、センサーまたはアクチュエーターのいずれかになります。場合によっては、センサーはリアルタイムで表示される連続的なデータストリームを提供したり、定期的な分析のためにデータベースに書き込まれる個別の読み取り値を提供したりします。アクチュエーターは、通常、プロセスの制御、つまり何かのオン／オフを切り替えるために使用されるデバイスです。目的の開度に達するまでサーボモーターを十分な回数パルス駆動することで、バルブを開閉するために使用できます。多くの場合、デバイスは遠隔地に配置され、コントローラーを介して中央にある監視システムに接続されます。IoTデバイスは、制御機能と通信機能が組み込まれ、ますます洗練されていることで注目されています。IoTデバイスは通常、暗号化とデジタル署名機能を備えたAPIと通信するため、ユーザー名／パスワードアカウントは必要ありません。

一般的なIoT構成には、以下のゾーンがあります：

1.  IoTデバイス（センサーおよびアクチュエーター）。デバイス間のアクセス管理は、DNP3、MQTT、および／またはデジタル署名テクノロジー（例、PKI）のようなコミュニケーションチャンネルの暗号化要件を課すポリシーによって統治されるべきです。低セキュリティ環境において、機器が破棄されるまで有効な静的なパスワードが利用されることがあります。機密性が高いアプリケーションでは、セキュリティクレデンシャル（パスワード、証明書など）は定期的にローテーションされます。選択されたセキュリティ要件はデバイスの機能と一致する必要がありますが、多くの場合に技術的な制限がIoTデバイスを制限することがあります。「Terminology for Constrained-Node Networks」（RFC 7228）は3つのデバイスクラスが水曜されています： [^2]
    
    1.  クラス0 – 設定可能な認証サポートする機能がない。
        
    2.  クラス1 – 鍵管理、トークンサポートなどの容量が制限されている。
        
    3.  クラス2 – 動的な認証メカニズムを完全に設定可能で、サポートしている。
        
2.  コントローラー（デバイスが接続されているコントローラー）。各センサーやアクチュエーターを制御ロジックにマッピングするデバイスコントローラーによってセンサーデバイスデータが集約される場合、アクチュエーターへのアクセス制御とデータベースへの収集されたデータの書き込みに対する保護を提供することが必要です（以下のサービスアカウントを参照）。
    
3.  IoTデバイスを監視または制御するコントローラーアプリやSCADAアプリのようなヒューマンマシンインタフェースアプリケーション（HMI）。場合によっては、センサーはSCADAアプリや同様のヒューマンマシンインタフェース（HMI）のような他のアプリケーションによって読み取られるデータベースに直接データを書き込みます。これらのアプリケーションへのアクセスは人間によっておこなわれ、IDM環境を介して管理されるべきです。
    

これまで、IoT環境は運用技術（OT）を担当するチームによって管理されており、組織内の情報技術（IT）環境とはほとんど関係がありませんでした。IoT技術の専門性はこの組織構造を正当化し、IT環境を介した潜在的な侵害からOTを隔離することが企業方針となっている場合が多くあります。しかし、セキュリティ技術の進歩とともに、隔離の必要性は減少しています。IoTシステムをIAM環境と統合することで、アクセス制御機能が向上し、ほとんどの産業用アプリケーションにおいて運用技術のデプロイに対するより良い企業ガバナンスを提供します。

規制当局により許可されている場合、ベストプラクティスはOT環境とIT IAM環境を統合することです。これにより、OTはIAMシステムを介してシステム権限を設定でき、OTスタッフは特権アクセス管理システムを介して企業の資格情報を利用して認可できるようになります。

「バックドア」アクセスのデプロイが潜在的に可能な改変がされていないことを確認するため、サプライチェーン全体を通じてIoTデバイスや追跡デバイスの出所についての懸念が増加しています。[^3] IAM実務者は、IoTデバイスに適用する認証プロセスを企業ポリシーで明確に定義し、ソフトウェアサプライチェーンポリシーへの準拠を確保することが望ましいでしょう。これは、規制の厳しい業界ではますます重要です。

デバイス自体のセキュリティ保護と同様に重要なのは、IoTデバイスデータの保護です。多くの場合、IoTデバイスが持つデータベースは適切に保護されていません。保護の適切性を判断するには、リスク管理アプローチを採用すべきです；建造環境のデバイスデータはリスクが低いかもしれませんが、産業スパイから適切に保護されていない工場の生産データは致命的かもしれません。IAM実務者は、産業用データストアに適切なアクセス制御が適用されていることを確認すべきです。産業用データベースにはデータ管理者の役割を割り当てることがグッドプラクティスです。

脆弱性の軽減

IoTデバイスの管理におけるIAM実務者の関与を決める場合、「正解」はありません。一方には、すべてのIoTの導入と管理をOT担当者の領域とするユースケースが挙げられます。この場合、IAMの関与はOTシステムにアクセスする人間のアカウントに限定されます。IoTシステムを構成できるアカウントのエンタイトルメントをグループ管理することで、セキュリティレベルを高めることができます。

中間として、IoTの構成と運用のコンポーネントがIAMサービスに該当させることがあります。IAMプロビジョニングワークフローは、構成リクエストと、場合によってはパスワードローテーションリクエストを担当者にルーティングします。IoTデバイスは、セキュリティオペレーションセンター（SOC）や、場合によってはセキュリティ情報イベント管理（SIEM）システムとの統合により、担当マネージャーへの認証レポートとコンプライアンス管理の両方に関与します。

対極として、デバイスのプロビジョニングはアイデンティティ管理インフラストラクチャに組み込むことがあります。IoTデバイスは個人と同様に扱われ、デバイスに「デジタルアイデンティティ」が適用されます。エンタイトルメントは通常のアカウントプロビジョニングワークフローを介して設定でき、アクセス制御にも同じプロトコルを使用できます。ゲートウェイを含むほとんどのモダンなAPIシステムは、マシン間通信にOAuth 2.0を使用していますが、IoTデバイスコントローラーの認証にはOpen ID Connectが適している場合があります。 [^4]

@row
### Service Accounts

There is a wide variety of service accounts. They are typically used in processes that are periodically run on an automated basis, e.g., via a UNIX cron job or Windows Task Scheduler. Auditors often overlook the accounts used by these processes because they are not accessed by users interactively. Since users do not log into them, they are typically basic, single-purpose accounts with restricted privileges.

Examples include:

*   An account used to perform a nightly backup of data
    
*   An account providing access to the HVAC system for monitoring purposes
    
*   An account used for replication of data between directory instances.
    

The term ‘batch account’ is sometimes used for a service account. These often refer to one or more utility operations that run periodically during non-production hours to perform a system function. Multiple batch processes may use a single batch account.

Vulnerability Mitigation

Service accounts are a significant source of concern for many organizations because they are often established with a static password that, if not encrypted, can be read by any system administrator. If their access rights are not tightly scoped, these accounts can then be used interactively by a malicious actor and possibly used for lateral movement to other servers in the organization’s network. If corporate data loss protection extends to service accounts, tools such as authentication monitoring for anomalies can guard against such vulnerabilities. User behavior analysis tools baseline the normal activity on an account; any deviation from this will generate an alert to the event monitoring system. Alternatively, static service accounts can be migrated to APIs that typically impose a strict security and monitoring regime.

Note: the term ‘service account’ is sometimes used to describe an account accessed periodically by a service person, e.g., an HVAC technician. Such accounts are user accounts and should be addressed in a company’s IAM strategy. They are not addressed in this document.

@column
### サービスアカウント

サービスアカウントには様々な種類があります。これらは通常、UNIXのcronジョブやWindowsのタスクスケジューラなど、自動化基盤で定期的に実行されるプロセスで使用されます。これらのプロセスで使用されるアカウントは、ユーザーがインタラクティブにアクセスしないため、監査者が見落としてしまうことがよくあります。ユーザーはこれらにログインしないため、これらは通常、権限が制限された、基本的な単一目的のアカウントです。

例：

*   夜間のデータバックアップの実行に利用されるアカウント
    
*   監視目的でHVACシステムにアクセスを提供するアカウント
    
*   ディレクトリシステム間のデータレプリケーションに利用されるアカウント。
    

時々、「バッチアカウント」という単語はサービスアカウントを指すために使われます。しばしば、これはシステム機能を実行するためにプロダクション稼働時間外に定期的に実行する1つ以上のユーティリティ操作を指します。複数のバッチプロセスが単一のバッチアカウントを使うこともあります。

脆弱性の軽減

サービスアカウントは静的なパスワードで設定されることが多く、暗号化されていない場合、システム管理者であれば誰でも読み取ることができるため、サービスアカウントは多くの組織にとって大きな懸念事項です。これらのアクセス権限が厳密に制限されていない場合、悪意のある攻撃者がこれらのアカウントをインタラクティブに利用し、組織ネットワーク内の他のサーバーへの水平方向の移動に利用される可能性があります。企業のデータ損失防止策がサービスアカウントに拡張する場合、異常に対する認証監視などのツールは、このような脆弱性を防ぎます。ユーザー行動分析ツールは、アカウントの正常なアクティビティを基準とします；この基準から逸脱すると、イベント監視システムにアラートを生成します。あるいは、静的なサービスアカウントを、通常は厳格なセキュリティと監視体制を課すAPIに移行することも可能です。

注意：「サービスアカウント」という単語は、時々、HVAC技術者のようなサービス担当者によって定期的にアクセスされるアカウントを指すために使われます。このようなアカウントはユーザーアカウントであり、企業のIAM戦略で対処すべきです。これは、本ドキュメントでは取り上げていません。

@row
### Bots

The term ‘bot’ has come from the Robotic Process Automation (RPA) sector that had its genesis in plant automation, where software routines are deployed for repetitive processes. [^5] Bots are now used for everything from website crawlers to retrieve usage information to denial-of-service malware. Increasingly they are being used by organizations to automate repetitive tasks such as retrieval of building information management data or consolidating customer transaction data. In these cases, access by bots will be restricted to a specific purpose.

Bots typically use the Internet to access remote services or resources. A publicly available website should apply mechanisms to limit bot activity and avoid malicious access. These mechanisms might include applying screen-scraper controls, human verification checks, and DDOS protection. A common form of malicious activity is ‘credential stuffing,’ whereby a hacker alters login credentials to take control of a session.

Organizations need to prepare for the external use of bots. Bots will exhibit different characteristics compared to ‘normal’ non-human access to a process or service. For the IAM practitioner, user behavior analysis can be used to identify access anomalies.

A process for reviewing the use of bots should be established, testing their functionality prior to deployment and analyzing their usage patterns. Monitoring is a continuous task since malicious corruption of bots is a constant concern.

Vulnerability Mitigation

For the corporate application of bot technology, the IAM practitioner’s task is to ensure that appropriate controls on credentials are observed and that PKI signatures and encryption are used as appropriate. Only sanctioned activities should be allowed.

For instance, a bot accessing website data will typically authenticate via HTTPS using an assigned session token. It is a good practice to expire session tokens periodically. The length of time a token should be valid should depend on the sensitivity of the service or resources being accessed.

@column
### ボット

「ボット」という単語は、工場の自動化から生まれたロボティックプロセスオートメーション（RPA）分野に由来しており、反復的なプロセスにソフトウェアルーティーンを導入しています。 [^5] 今やボットは利用状況情報の収集のためのWebサイトクローラーからサービス拒否攻撃をおこなうマルウェアまですべてに利用されています。組織によるボットの利用はますます増えており、建物情報管理データの収集や顧客取引データの統合というような反復的なタスクの自動化に利用しています。このような場合、ボットからのアクセスは特定の目的に制限されるでしょう。

通常、ボットはインターネットを使い、リモートサービスやリソースにアクセスします。公開されているWebサイトはボットの活動を制限し、悪意のあるアクセスを回避するメカニズムを採用すべきです。これらメカニズムはスクリーンスクレーパーの制御、人間の検証、およびDDOS攻撃からの保護を採用することを含みます。よくある悪意のあるアクティビティは、「クレデンシャルスタッフィング」であり、ハッカーがログインクレデンシャルを変更してセッションの制御をおこなうことです。

組織はボットの外部利用を準備する必要があります。ボットは、プロセスやサービスへの「一般的な」非人間アクセスと比べて異なる特徴を示します。IAM実務者としては、ユーザーの行動分析がアクセスの異常を特定するために利用できます。

ボットの利用をレビューし、デプロイ前に機能をテストし、利用パターンを分析するプロセスを確立すべきです。ボットによる悪意のある破壊は常に懸念されるため、監視は継続的なタスクになります。

脆弱性の軽減

ボット技術を企業に適用する場合、IAM実務者のタスクはクレデンシャルに対する適切な制御が観測され、PKI署名と暗号化が適切に利用されることを確実にすることです。承認されたアクティビティだけが許可されるべきです。

例えば、Webサイトのデータにアクセスするボットは通常、割り当てられたセッショントークンを使い、HTTPSを介して認証をおこないます。定期的にセッショントークンを有効期限切れにすることはグッドプラクティスです。トークンの有効期間は、アクセスするサービスまたはリソースの機密性に応じて適切にすべきです。

@row
### Client Devices

Traditionally identities are people; they have identifiers stored in an identity datastore and then used to authenticate users to protected resources. It is increasingly necessary to also track the endpoint devices that users employ to access corporate resources, such as laptops, tablets, or smartphones. To track those devices, an object is created in the organization’s directory or other data stores that record the detail for each device. This data allows us to grant access to a resource based on the device being used to access it.

There are several benefits to registering client devices:

*   It can provide a second factor during a human authentication event, thus reducing the risk score associated with the authentication.
    
*   It can be used to customize the presentation and improve the user experience by passing the details of a user’s device to an application.
    
*   It can enable unattended device authentication to support scheduled events such as device updates or data retrieval.
    
*   It can remove a vulnerability and improve governance options when client device objects from the data store are disabled or removed when the time period from the LastLogonTimestamp has been exceeded.
    

Whether your environment is on-premise, hybrid-cloud, or multi-cloud, managing the client device identity lifecycle is key to reducing the organization’s attack surface and maintaining compliance per corporate policy.

Vulnerability Mitigation

With the ubiquity of client devices these days, managing client devices can improve an organization’s cybersecurity profile. For instance, a smartphone can be a valuable device for multi-factor authentication (MFA). It can provide a ‘possession’ factor, e.g., the user is using their registered mobile phone. It can also be used to provide a biometric check for an ‘inherence’ factor.

Some organizations use a Mobile Device Management (MDM) tool to manage client devices. MDM facilitates the tracking and management of devices and will typically include a self-service module to allow users to register and deregister their devices as new devices are acquired or old devices are lost or retired.

Selecting and deploying the appropriate solution for managing client device ‘identities’ is a core capability in enabling non-human access control.

@column
### クライアントデバイス

従来、アイデンティティは人間です；人間はアイデンティティデータストアに保管され、保護されたリソースへのアクセスでユーザーを認証するために利用された識別子を有しています。ラップトップ、タブレットまたはスマートフォンのような企業のリソースにアクセスするさいにユーザーが用いるエンドポイントデバイスを追跡する必要性も増えています。これらのデバイスを追跡するため、組織のディレクトリや各デバイスの詳細を記録するその他のデータストアにオブジェクトを生成します。このデータによって、アクセスを使用されているデバイスに基づいてリソースへのアクセス権を付与できます。

クライアントデバイスを登録する利点はいくつかあります：

*   人間の認証イベントのにおいて第二要素を提供することができ、認証に関連するリスクスコアを低くできます。
    
*   ユーザーのデバイスの詳細情報をアプリケーションに提供することで、ユーザーエクスペリエンスを向上させ、プレゼンテーションをカスタマイズするために利用することができます。
    
*   無人デバイス認証を有効にし、デバイス更新やデータ収集のようなスケジュールされたイベントをサポートできます。
    
*   最終ログオン時刻からの時間が超過したとき、データストアからのクライアントデバイスオブジェクトが無効化されたり、削除されたりするとき、脆弱性が排除され、ガバナンスオプションを向上させることができます。
    

環境がオンプレミス、ハイブリッドクラウド、またはマルチクラウドなのかに関わらず、クライアントデバイスアイデンティティのライフサイクルを管理することは組織の攻撃領域を減らし、企業ポリシーに対してコンプライアンスを維持するための鍵となります。

脆弱性の軽減

これまでクライアントデバイスは普及しており、クライアントデバイスの管理は組織のサイバーセキュリティプロファイルを向上させます。例えば、スマートフォンは多要素認証（MFA）にとって価値の高いデバイスになります。スマートフォンは「所持」要素、例えばユーザーが登録されたモバイルフォンを利用していること、を提供します。また、「生得」要素のためのバイオメトリクス検証の提供に利用することもできます。

一部の組織はモバイルデバイス管理（MDM）ツールを利用し、クライアントデバイスを管理します。MDMはデバイスの追跡と管理を促進し、一般的に新しいデバイスを取得したり、古いデバイスを紛失したり、廃棄したりするとき、ユーザーはデバイスを登録したり、登録解除したりできるセルフサービスモジュールが含まれます。

クライントデバイス「識別子」を管理するための適切なソリューションを選択し、デプロイすることは非人間アクセス制御を有効するにあたってのコア機能です。

@row
## System Account Access Control

System accounts give humans access to physical or virtual systems or servers and grant entitlements to privileged system functionality. While not strictly non-human accounts, system accounts are included here because they have no single individual to which they are assigned. System accounts typically refer to administration accounts that are established when a system/server is commissioned. Since this type of account is not directly associated with a single person, they are generally not managed via an organization's joiner–mover-leaver HR processes. IAM practitioners must concern themselves with the management of these accounts.

@column
## システムアカウントアクセス制御

システムアカウントは、物理的または仮想的なシステムあるいはサーバーへのアクセス権を人間に与え、特権システム機能へのエンタイトルメントを付与します。厳密には非人間アカウントではないものの、システムアカウントは単一の個人に割り当てられないことから、これに含まれます。システムアカウントは通常、システム／サーバーが運用されるさいに作成される管理者アカウントを指します。この種のアカウントは直接単一の人間に関連付けられないため、一般的に組織のJoiner-Mover-LeaverというHRプロセスを介して管理されることはありません。IAM実務者は、これらのアカウントの管理に注意を払わなくてはなりません。

@row
### Admin or Root Account

The admin or root account of Windows and Linux or Unix servers is a highly privileged

account with access to system-level operations on the respective platform:

*   It is authorized at the highest level.
    
*   It has access to every file and process running on a platform.
    
*   It has permissions to configure the system operation and thereby influence the behavior of the platform.
    
*   Logs from a system will typically display commands that have been run and responses that have been viewed
    
*   Operational use of the account should be continuously monitored.
    

Note: virtualization and hypervisor platforms (VMware, Citrix, Xen) and container platforms (Docker, Openshift, DCOS, Kubernetes) have administrative accounts that provide an attack vector if not properly managed.

@column
### 管理者またはルートアカウント

WindowsおよびLinuxまたはUnixサーバーの管理者またはルートアカウントは、それぞれのプラットフォーム上のシステムレベルの操作にアクセスできる高い特権アカウントです：

*   最高レベルで認可されています。
    
*   プラットフォーム上で実行されているすべてのファイルとプロセスにアクセスできます。
    
*   システム操作を構成し、それによってプラットフォームの振る舞いに影響を与えるパーミッションを持っています。
    
*   通常、システムからのログは実行されたコマンドと表示されたレスポンスを表示します。
    
*   アカウントの運用での使用は、継続的に監視されるべきです。
    

注意：仮想化およびハイパーバイザープラットフォーム（VMWare、Citrix、Xen）とコンテナプラットフォーム（Docker、Openshift、DCOS、Kubernetes）は、適切に管理されていない場合に攻撃ベクトルを提供することになる管理者アカウントを有しています。

@row
### Superuser Account

The term Superuser applies to a business information system or application account that has elevated privileges over standard user accounts. It is generated as part of the system commissioning process when the system is deployed. The Superuser account has permission to modify a configuration, making it a mission-critical account in an information system.

@column
### スーパーユーザーアカウント

スーパーユーザーという単語は、標準ユーザーアカウントを超える高い権限を持つビジネス情報システムまたはアプリケーションアカウントを指します。これはシステムのデプロイ時にシステム委託プロセスの一部として生成されます。スーパーユーザーアカウントは構成を変更するパーミッションを持ち、情報システムにおいてミッションクリティカルなアカウントとなります。

@row
### Server Account

Accounts for middleware processes like DBMSs, ESBs, or other ICT components that run in the Windows or Linux operating system environments, are sometimes called server accounts. These are privileged accounts in an application such as a DBMS to give administrative access to a resource owner.

@column
### サーバーアカウント

WindowsまたはLinuxオペレーティングシステム環境で実行されるDBMS、ESB、またはICTコンポーネントのようなミドルウェアプロセスのアカウントは、サーバーアカウントと呼ばれることがあります。これらは、リソースオーナーに管理アクセスを付与するため、DBMSのようなアプリケーションにおける特権アカウントです。

@row
### Consumer Devices

There is increasing concern regarding the vulnerability of consumer devices that have connections to the Internet. Recent incidents include:

*   Privacy violations by devices that have audio or video capture capabilities and that are sending sensitive data back to a monitoring agency.
    
*   Security incidents such as DDoS attacks as common, published administrative passwords are used, giving hackers access to consumer devices that are then used to conduct Distributed Denial of Service (DDoS) attacks.
    

Most jurisdictions are now requiring products to adhere to an appropriate set of standards that typically include: [^6]

*   Ending the use of default passwords. All devices are shipped with a unique password that is not resettable to a common default setting.
    
*   Enabling support for software updates. Devices are shipped with firmware that can be readily updated in the event that a vulnerability is detected.
    
*   Supporting the secure storage of credentials. All credentials should be stored securely with encryption protection and/or a trusted storage mechanism.
    
*   Shipping with a more secure default configuration. Attack surfaces are minimized by closing unused ports, restricting exposed services to only the functionally necessary, and running software with the lowest level of privileges necessary for the system operation,
    
*   Restricting the storage of Personal Identifiable Information (PII). PII is never stored on the device, as per requirements of privacy regulation in the target geographies.
    

@column
### コンシューマーデバイス

インターネット二接続するコンシューマーデバイスの脆弱性に関する懸念が増加しています。直近のインシデントは以下のものがあります：

*   音声またはビデオのキャプチャ機能と機密データを監視機関に送信するデバイスによるプライバシー侵害。
    
*   DDoS攻撃のようなセキュリティインシデントでは、公開された管理パスワードが使用され、ハッカーがコンシューマーデバイスにアクセスして分散型サービス拒否（DDoS）攻撃を実行することができます。
    

ほとんどの法域では、今や製品が適切な標準に準拠することを要求しており、通常、これは以下を含みます： [^6]

*   デフォルトパスワードの利用を終了する。すべてのデバイスは、共通デフォルト設定にリセットできない固有のパスワードが設定された状態で出荷されます。
    
*   ソフトウェア更新のサポートを有効化する。デバイスは、脆弱性が検知された場合にはすぐにアップデートできるファームウェアが搭載されて出荷されます。
    
*   クレデンシャルのセキュアな保管をサポートする。すべてのクレデンシャルは、暗号化保護および／または信頼されたストレージメカニズムを用いて安全に保管するべきです。
    
*   よりセキュアなデフォルト構成で出荷する。使っていないポートを閉じ、機能的に必要な公開サービスだけに制限し、そしてシステム操作のために必要な最低限の権限でソフトウェアを実行することで、攻撃領域を最小化します。
    
*   個人を特定できる情報（PII）の保管を制限する。対象地域のプライバシー制限の要件に従い、PIIはデバイスに保管されません。
    

@row
### System Account Characteristics

Since system accounts are not assigned to a single identity, they cannot be wholly managed by an IAM solution, e.g., when the person with administrative privileges leaves an organization, it is not appropriate for such an account to be deleted. A common practice is to provide access to privileged accounts via a managed group so that all users in the group are granted access to the account. But management outside the IAM environment is still required. Good practices include:

*   Using a configuration management database in which the server/service is registered as an attribute of the identity it belongs to.
    
*   Assign an account owner to be accountable for the use of the account, typically the owner of the system/service that it belongs to. If no system owner has been defined, a responsible person in the IT department should be the accountable party.
    
*   Interactive accounts should only be used for infrastructural changes or calamities. Admin privileges should be granted via a user’s account, e.g., via membership in the appropriate Admin group.
    
*   Passwords for Admin/root accounts must be closely managed. They can be secured via a manual procedure, a password vault, or a Privileged Account Management system.
    

Vulnerability Mitigation

IAM practitioners should assist in the protection of access to all system accounts. In a UNIX environment, this might be via the removal of the ‘ [etc/passwd](https://www.google.com/search?sxsrf=ALeKk00EXgVcYJud1c2wvEi6kTkygI3HFQ:1588810082250&q=unix+root+access+sudo+etc+passwd&spell=1&sa=X&ved=2ahUKEwjKo8XkuqDpAhXPXisKHVrJBoIQBSgAegQIDRAn) ’ file and the use of SUDO for privilege escalation. In a Microsoft Windows environment, a privileged access management (PAM) system is a common solution. In this case, system passwords are made specifically complex and rotated as appropriate. Access to such an account is via a PAM system, which restricts access to specific individuals with the appropriate entitlements and logs all access events.

If a PAM is not used, Windows supports the time-limited elevation of account privileges, with notification to management. Manual intervention that ensures appropriate use and management of system and server accounts is also good practice, as is including server accounts in corporate audits. This level of management will require corporate policy to be established for server accounts which will heighten the visibility of account management practices.

Increasingly, applications are being deployed on cloud services requiring an access control environment that suits each deployment. This type of deployment might mean configuring a resource manager to protect master account privileges or setting policies that ensure applications do not use the master account for database access.

@column
### システムアカウントの特徴

システムアカウントは単一のアイデンティティに割り当てられないため、IAMソリューションで完全に管理することはできません。例えば、管理者権限を持つ人物が組織を退職したとき、そのようなアカウントを削除することは適切ではありません。よくあるプラクティスは管理グループを介して特権アカウントへのアクセスを提供し、グループ内のすべてのユーザーにアカウントへのアクセスを付与します。しかし、IAM環境外での管理は依然として必須です。グッドプラクティスには以下が含まれます：

*   サーバー／サービスが所属するアイデンティティの属性として登録されている構成管理データベースを利用する。
    
*   アカウントの使用に責任を負うアカウント所有者、通常はアカウントが所属するシステム／サービスの所有者をアサインする。システム所有者として定義されていない場合、IT部門の責任者が責任者となるべきです。
    
*   インタラクティブアカウントはインフラストラクチャの変更や障害のためだけに利用すべきです。管理者権限はユーザーのアカウントを介して、例えば適切な管理者グループのメンバーシップを介して付与されるべきです。
    
*   管理者／ルートアカウントのパスワードは厳重に管理しなければなりません。これは手動の手順、パスワード保管庫、または特権アカウント管理システムを通じて保護することができます。
    

脆弱性の軽減

IAM実務者は、すべてのシステムアカウントへのアクセスの保護を支援すべきです。UNIX環境では、「 [etc/passwd](https://www.google.com/search?sxsrf=ALeKk00EXgVcYJud1c2wvEi6kTkygI3HFQ:1588810082250&q=unix+root+access+sudo+etc+passwd&spell=1&sa=X&ved=2ahUKEwjKo8XkuqDpAhXPXisKHVrJBoIQBSgAegQIDRAn) 」ファイルの削除および権限昇格のためのSUDOの利用です。Microsoft Windows環境では、特権アクセス管理（PAM）システムが一般的なソリューションです。この場合、システムパスワードは特に複雑で必要に応じてローテーションされます。このようなアカウントへのアクセスはPAMシステムを通じておこない、適切なエンタイトルメントを持つ特定の個人にアクセスが制限され、すべてのアクセスイベントがログに残ります。

PAMを利用しない場合、Windowsは管理者への通知を伴う期間限定のアカウント権限の昇格をサポートします。システムとサーバーアカウントの適切な利用と管理を保証する手動介入もグッドプラクティスであり、企業の監査にサーバーアカウントを含めることも同様です。このレベルの管理は、アカウント管理作業の可視化を推進するためにサーバーアカウントを確立する企業ポリシーを必要とします。

アプリケーションがクラウドサービスにデプロイされることは増加しており、それぞれのデプロイメントに適したアクセス制御環境を必要としています。この種のデプロイメントはマスターアカウント権限を保護するためのリソースマネージャーの設定やアプリケーションがデータベースアクセスのためにマスターアカウントを利用しないことを保証するポリシーの設定を意味します。

@row
## The Future

The ubiquity of IoT devices will become more prevalent. Devices will span both the corporate and the consumer world, and integrating IoT devices and dataflows will be a new corporate risk. Automation will increasingly be deployed with Machine Learning and Artificial Intelligence, adding to the complexity of the access control environment. Integration with the IAM environment via the use of API gateways, database gateways, service meshes, and Policy-Based Access Control solutions should be considered.

Increasingly APIs are being used for machine-to-machine (M2M) communication. APIs provide the ability to apply consistent security controls on a communication channel and also to monitor it for management purposes. Companies adopting a gateway approach have the ability to provide consistency across M2M communications which is virtually impossible if each service instance is deployed individually.

As the adoption of cloud services continues to accelerate, the use of microservices and containerization will become prevalent. The IAM practitioner should ensure that the appropriate information security solutions are put in place to protect communications between services that communicate identity data.

The use of bots will also continue to accelerate; deployment of behavioral analytics and gateway technology should be considered. The US Department of Homeland Security [^7] advises the following:

*   Nefarious bot developers will target new IoT devices for vulnerabilities as they are released to the market and will compete with each other to deploy malware.
    
*   Bot code size will get smaller and more sophisticated to avoid detection and frustrate defenses.
    
*   Botnets will be extended and better monetized, likely through interfaces to social media platforms.
    
*   Botnet operators will operate increasingly globally, taking advantage of regional vulnerabilities. Attacks from foreign nation-state operators will increase.
    

Access control for non-human entities is a critical competence for risk-averse organizations. It is increasingly important to make sure devices and bots adequately identify themselves, move to APIs with consistent security and monitoring controls, and deploy data-loss prevention technologies such as behavioral analysis tools.

@column
## 展望

IoTデバイスの遍在性はますます高まるでしょう。デバイスは企業と消費者の両方に浸透し、IoTデバイスとデータフローの統合は新たな企業リスクになるでしょう。機械学習と人工知能による自動化の導入が増加し、アクセス制御環境に複雑さが増します。APIゲートウェイ、データベースゲートウェイ、サービスメッシュ、およびポリシーベースアクセス制御ソリューションの利用によるIAM環境との統合は検討されるべきです。

マシンツーマシン（M2M）コミュニケーションのためのAPI利用が増加します。APIはコミュニケーションチャンネルに一貫したセキュリティ制御を適用し、管理目的で監視する機能を提供します。ゲートウェイアプローチを採用している企業は、各サービスインスタンスが個別にデプロイされている場合には事実上不可能なM2Mコミュニケーションに関する一貫性を提供する機能を有しています。

クラウドサービスの採用が加速し続けるにつれて、マイクロサービスとコンテナライゼーションの利用は普及していくでしょう。IAM実務者は、アイデンティティデータを通信するサービス間の通信を保護するために適切な情報セキュリティソリューションを導入することを確実にすべきです。

ボットの利用も加速し続けるでしょう；行動分析およびゲートウェイテクノロジーの導入を検討すべきです。米国国土安全保障省 [^7] は以下の助言を与えています：

*   悪質なボット開発者は新しいIoTデバイスが市場にリリースされるとその脆弱性をターゲットにし、競い合ってマルウェアをデプロイするでしょう。
    
*   ボットのコード規模は検出を回避し、防御を妨害するためにより小さく、より洗練されるでしょう。
    
*   ボットネットは、ソーシャルメディアプラットフォームへのインタフェースを通じて拡張され、より収益化されるでしょう。
    
*   ボットネット運用者は、地域的な脆弱性の有利を利用してますますグローバルに運用するでしょう。外国・他の地域からの攻撃は増加するでしょう。
    

非人間エンティティに対するアクセス制御はリスク回避をしたい組織によって極めて重要な能力です。デバイスとボットを適切に特定、一貫したセキュリティと監視制御を備えたAPIへ移行、および行動分析ツールのようなデータ損失防止テクノロジーの導入を確実におこなうことがますます重要になります。

@row
## Conclusion

All too often, IAM practitioners are sequestered from non-human account management and only focus on the provisioning and access control associated with user accounts. This is unfortunate because it fragments the host organization’s risk management approach to cybersecurity and frustrates the governance task. At the very least, the IAM practitioner should ask the appropriate questions as to how IoT devices are being secured, how server accounts are being managed, and what defenses are in place to thwart malicious bots. It is preferable that the IAM and InfoSec teams within an organization work together to ensure the consistent application of cybersecurity controls that are aligned with corporate policy.

@column
## 結論

非常に多くの場合、IAM実務者は非人間アカウント管理から隔離され、ユーザーアカウントに関連するアクセス制御をプロビジョニングすることだけに集中します。これは、ホスト組織のサイバーセキュリティのためのリスク管理アプローチを断片化し、ガバナンスタスクを阻害するため、好ましくありません。少なくとも、IAM実務者はIoTデバイスのセキュリティ管理方法、サーバーアカウントの管理方法、および悪意のあるボットを阻止するための防御について適切な質問をすべきです。組織内のIAMと情報セキュリティチームが連携し、企業ポリシーに準拠したサイバーセキュリティ制御を一貫して適用することを保証することが望ましいです。

@row
### Author Bios

<!-- ![Author photo](/assets/images/idpro_bok/gwilliamson.jpg) --> Graham Williamson

Graham Williamson is an IAM consultant working with commercial and government organizations for over 20 years with expertise in identity management and access control, enterprise architecture and service-oriented architecture, electronic commerce, and public key infrastructure, as well as ICT strategy development and project management. Graham has undertaken major projects for commercial organizations such as Cathay Pacific in Hong Kong and Sensis in Melbourne, academic institutions in Australia such as Monash University and Griffith University, and government agencies such as Queensland Government CIO’s office and the Northern Territory Government in Australia and the Ministry of Home Affairs in Singapore.

Graham holds an electrical engineering degree from the University of Toronto and a Master of Business Administration from Bond University. As a member of the IDPro Body of Knowledge Committee, he looks forward to helping create the definitive body of knowledge for the IAM sector.

<!-- ![Author photo](/assets/images/idpro_bok/akoot.jpg) --> André Koot

André Koot is IAM Strategist and Chief Customer Success Officer at Sonic Bee. His IAM experience comes from a financial accounting and auditing background. This background in anti-fraud detection and prevention business processes led to research in the area of authorization principles.

<!-- ![Author photo](/assets/images/idpro_bok/glee.jpg) --> Gloria Lee

Gloria Lee is a Senior Program Manager in the Azure AD Engineering team at Microsoft. As part of the customer experience team for Identity and Network Access, her role is driving customer success in the Azure Identity division. Gloria is focused on helping customers increase security posture with the deployment of Azure Active Directory, Azure hybrid cloud-based solutions to provide identity management.

Prior to joining Microsoft, Gloria was a seasoned engineer/architect with 18+ years of experience in the areas of Identity, security, deployment of Microsoft O365 services as well as messaging and collaboration. She had previously spoken at various events such as Microsoft Identity Driven Airlift Conference for partners, GrayHat 2020, and Texas Security Summit. Outside of technology, she enjoys spending time with her kids/family and travel bargain hunting.

@row
## Change Log

| Date | Change |
| --- | --- |
| 2020-10-30 | V1 published |
| 2021-04-19 | Author affiliation change |
| 2022-02-28 | Added a section on client devices; added Gloria Lee as an author |
| 2023-03-31 | Various changes to improve the clarity of the article such as the addition of device vs. service information |

- - -

[^1]:  Cameron, Andrew and Olaf Grewe, “An Overview of the Digital Identity Lifecycle,” IDPro Body of Knowledge, 30 October 2020, [https://bok.idpro.org/article/id/31/](https://bok.idpro.org/article/id/31/) . 
    
[^2]:  Bormann, C., Ersue, M., and A. Keranen, "Terminology for Constrained-Node Networks", RFC 7228, DOI 10.17487/RFC7228, May 2014, < [https://www.rfc-editor.org/info/rfc7228](https://www.rfc-editor.org/info/rfc7228) \>. 
    
[^3]:  Hashemi, Soheil, and Mani Zarei. “Internet of Things Backdoors: Resource Management Issues, Security Challenges, and Detection Methods.” Transactions on Emerging Telecommunications Technologies. Wiley, October 12, 2020. [https://doi.org/10.1002/ett.4142](https://doi.org/10.1002/ett.4142) . 
    
[^4]:  See section ‘Mobile & API Innovation Gave Us OAuth & Delegated Authorization Frameworks’ in Dingle, Pamela, “Introduction to Identity - Part 2: Access Management,” IDPro Body of Knowledge, 17 June 2020, [https://bok.idpro.org/article/id/45/](https://bok.idpro.org/article/id/45/) . 
    
[^5]:  “What is a bot in RPA?,” n.d., [https://www.nice.com/guide/rpa/what-is-a-bot-in-rpa/](https://www.nice.com/guide/rpa/what-is-a-bot-in-rpa/) . 
    
[^6]:  For example, see Fernandez, Angel, "New IoT security regulations: what you need to know,” Allot blog, 30 January 2020, [https://www.allot.com/blog/new-iot-security-regulations-what-you-need-to-know/#](https://www.allot.com/blog/new-iot-security-regulations-what-you-need-to-know/) . 
    
[^7]:  Botnet Roadmap Status Update, Department of Commerce and Homeland Security, July 2020, [https://www.commerce.gov/sites/default/files/2020-07/Botnet%20Road%20Map%20Status%20Update.pdf](https://www.commerce.gov/sites/default/files/2020-07/Botnet%20Road%20Map%20Status%20Update.pdf) . 
