---
layout: article
title: クラウド設計パターンのメモ
permalink: /docs/design/clouddesignpattern_azure
date: 2024-01-10
aside:
  toc: true
tags: ["クラウド", "デザインパターン", "設計", "Azure", "アーキテクチャ", "AWS"]
---

クラウドでのデザインパターン、設計についての記事があったので一通り確認した。

[クラウド設計パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/)

基本的にはパターンの概要を記事から引用している。
また、わかる範囲でAWSのサービスならどれを使うのかをメモした（Azureは勉強していないのでわからない）。

## アンバサダーパターン

[アンバサダー パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/ambassador)

> コンシューマー サービスまたはアプリケーションの代わりにネットワーク要求を送信するヘルパー サービスを作成します。 アンバサダー サービスは、クライアントに併置されているプロセス外のプロキシと考えることができます。

アプリケーションコードから、ネットワーク越しのリクエストを送る機能を分離してアンバサダーサービスとして構築する。

![ambassador.png](https://drive.google.com/uc?export=view&id=180Du8iPUcAnoO7vUmobmIiUfdFwfnNb4)

アプリケーションコードとは別に管理することで、セキュリティ、監視、認証などの機能といったものを更新・変更することが容易になる。
複数のことなる言語で実装されたアプリケーションから共通的に利用することができる。
アンバサダーサービスが間に入ることでオーバーヘッドが発生し、それを許容で着ない場合にはこのパターンは利用できない。
汎用的なネットワーク接続では対応できない場合にはこのパターンを採用できない。一部のアプリケーションでは冪等性が確保されておらず、ネットワーク接続の再試行が許容されないケースなど。

## 破損対策レイヤーパターン

[破損対策レイヤー パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/anti-corruption-layer)

> 同じセマンティクスを共有しない異なるサブシステム間にファサード、つまりアダプター レイヤーを実装します。 このレイヤーでは、一方のサブシステムがもう一方のサブシステムに行った要求が変換されます。 このパターンを使用することで、アプリケーションの設計が、外部サブシステムへの依存関係によって制限されないようにします。 

同じセマンティクスを共有しない＝同じ意味、内容のデータを使っていない
`name`が指すものが違う、とか？？？

> 新しいシステムとレガシ システムの間のアクセスを維持することによって、新しいシステムは、少なくともレガシ システムの API または他のセマンティクスの一部に強制的に従うことになります。 こうしたレガシ機能の品質に問題がある場合、その機能をサポートすることで、正常に設計された最新のアプリケーションが "破損" する場合があります。
> レガシ システムだけでなく、開発チームが制御できない外部システムでも似た問題が発生する可能性があります。

> 異なるサブシステムの間に破損対策レイヤーを配置し、これらを切り離します。 このレイヤーは、2 つのシステム間の通信を変換するもので、一方のシステムはそのままで、もう一方のシステムの設計と技術的アプローチも損なわれません。

アダプターパターンのことだと思う。

新システムとレガシシステムの統合する場合、サブシステム間で異なるセマンティクスを利用しているが通信する必要がある場合に使われる。

## 非同期要求-応答パターン

[非同期要求-応答パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/async-request-reply)

> フロントエンド ホストからバックエンド処理を分離します。その場合バックエンド処理を非同期にする必要がありますが、引き続きフロントエンドには明確な応答が必要です。

> この問題の 1 つの解決策は、HTTP ポーリングを使用することです。 コールバック エンドポイントを提供したり、長時間実行する接続を使用したりするのは困難な場合があるため、クライアント側コードにはポーリングが役立ちます。 

> 1. クライアントは要求を送信し、HTTP 202 (Accepted) 応答を受信します。
> 2. クライアントは、HTTP GET 要求を状態エンドポイントに送信します。 作業がまだ保留中のため、この呼び出しは HTTP 200 を返します。
> 3. ある時点で作業が完了すると、状態エンドポイントは、リソースにリダイレクトする 302 (Found) を返します。
> 4. クライアントは、指定された URL にあるリソースをフェッチします。

ざっくり、以下のような使い方だと思う。
API Gatewayで要求を受け取り、処理依頼をSQSにキューイングしてコンシューマとしてLambdaを用意しておく、Lambdaは処理結果をDynamoDBに入れる。
クライアントは定期的に処理結果をAPI Gatewayに要求し、別のLambdaがDynamoDBを確認して処理が完了していれば結果を返す。

## フロントエンド用バックエンドのパターン

[フロント エンド用バックエンドのパターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/backends-for-frontends)

> 特定のフロント エンド アプリケーションやインターフェイスによって使用される個別のバックエンド サービスを作成します。 このパターンは、複数のインターフェイスのために 1 つのバックエンドをカスタマイズすることが非効率な場合に役立ちます。

ユーザーインターフェイスごと（デスクトップPC、モバイルといったように）に 1つのバックエンドを作成する。

## バルクヘッドパターン

[バルクヘッド パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/bulkhead)

> 障害を許容するアプリケーション設計の一種です。 バルクヘッド アーキテクチャでは、アプリケーションの要素をプールに分離し、1 つの要素で障害が発生しても、他の要素は引き続き機能できるようにします。

> 船体の区分された区画 (bulkhead: 隔壁) になぞらえた命名

単一障害点をなくそう、ということだと思う。

## キャッシュアサイドパターン

[キャッシュ アサイド パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/cache-aside)

> オンデマンドでデータをデータ ストアからキャッシュに読み込みます。 これにより、パフォーマンスが向上するだけでなく、キャッシュに保持されているデータと基になるデータ ストアのデータの間で整合性が維持されます。

一般的なキャッシュシステムでは、リードスルーおよびライトスルー/ライトビハインド操作が実装されている。

> アプリケーションはキャッシュを参照してデータを取得します。 データがキャッシュにない場合は、データ ストアから取得され、キャッシュに追加されます。 キャッシュに保持されているデータに対する変更は、データ ストアにも自動的にライトバックされます。

キャッシュがこの機能を持っていない場合、アプリケーションがキャッシュアサイド戦略を実装することで機能をエミュレートする。

- オンデマンドでデータをキャッシュに読み込む
- 情報を更新したら、データストアに変更を加え、キャッシュ内の対応する項目を無効にする（ライトスルー戦略）
- 項目が次回必要になったときは、データ ストアから最新のデータが取得してキャッシュに再度追加する

> 多くのキャッシュで、指定された期間アクセスされなかったデータを、無効にしてキャッシュから削除する有効期限ポリシーが実装されています。 

AWSのサービスだとElastiCacheが存在する、またAurora PostgreSQLにはキャッシュ機能があるようだ。

[Aurora PostgreSQL のキャッシュ管理機能の紹介 \| Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/introduction-to-aurora-postgresql-cluster-cache-management/)

## コレオグラフィパターン

[コレオグラフィ パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/choreography)

> 中央の制御ポイントに依存するのではなく、システムの各コンポーネントが、ビジネス トランザクションのワークフローに関する意思決定プロセスに参加するようにします。

コレオグラフィ＝振り付け
[【図解】コレ１枚でわかるオーケストレーションとコレオグラフィ：ITソリューション塾：オルタナティブ・ブログ](https://blogs.itmedia.co.jp/itsolutionjuku/2019/08/post_729.html)

> 演劇や踊りで演技者に予め振り付けが行われるように、個々のサービスに予め動作条件や次にどのサービスを起動させるかといった設定が与えられており、それに従って、各サービスが自律的に動作する方式

オーケストレーション（オーケストレータ）

> 指揮者の指示に従って各演奏者が担当する楽器を演奏するように、全体の処理の流れを制御する指揮者にあたるプログラムが存在し、そこからのリクエストによってサービスを実行し、実行結果をレスポンスとして指揮者に返して次の処理に引き継ぐ方式です。これを「リクエスト・リプライ方式」と呼んでいます。

マイクロサービスアーキテクチャでは、小さいサービスが互いに通信してサービスを構築している。
オーケストレータパターンではオーケストレータがクライアントのリクエストを受け取り、それぞれのサービスの呼び出しをおこなう。オーケストレータと各サービスが密結合し、オーケストレータにドメイン知識が含まれる。

コレオグラフィパターンの一つである非同期メッセージングパターンでは、クライアントのリクエストがメッセージキューに入ると、各サービスにプッシュする。各サービスは処理の成功・失敗をメッセージキューに返し、後続のサービスが動作するように同じまたは別のキューにメッセージを送る。これを繰り返す。

> オーケストレーターはワークフローの回復性を集中的に管理し、単一障害点になる可能性があります。 これに対して、コレオグラフィの場合は、役割がすべてのサービス間で分散されるため、回復性の堅牢さが低下します。

オーケストラパターンはStep Functionsのはず。
コレオグラフィパターンは特定のサービスを指すものではない。

## サーキットブレーカーパターン

[サーキット ブレーカー パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/circuit-breaker)

> リモート サービスまたはリソースとの接続時に、復旧に要する時間が一定しないエラーを処理します。 これにより、アプリケーションの安定性と回復性を向上させることができます。

クラウドアプリケーションで発生する障害は、一時的なエラー（ネットワークの不調・タイムアウト、リソースの過剰な利用・一時的に使用できなくなる）による場合と回復にかなりの時間が要する場合がある。
回復にかなりの時間が要する場合、操作が失敗したことをすぐに受け入れて再試行せずにエラーを処理する必要がある。そうでない場合、CPUやコネクションの同時接続が解消されずにシステムリソースが枯渇する可能性がある。

> サーキット ブレーカーは、失敗する可能性のある操作のプロキシとして機能します。 プロキシは、最近発生した障害の数を監視し、その情報を使用して、操作を続行できるか、すぐに例外を返すだけにするかを決定します。

プロキシは以下の3つの状態をもつ

- クローズド：アプリケーションからの要求を操作にルーティングする。操作が失敗した場合、エラー数をカウントアップし、一定期間に閾値を超えたエラーが発生するとオープン状態に移行する。
- オープン：アプリケーションからの要求はすぐに失敗となり、アプリケーションに例外を返す。オープン状態にはタイムアウト時間が設定され、時間経過でハーフオープン状態に移行する。
- ハーフオープン：アプリケーションからの要求を限定的に操作にルーティングする。操作が成功した場合、障害からの回復とみなし、クローズド状態に移行する。操作が失敗した場合、再度オープン状態に移行する。


Step Functionsにサーキットブレーカーパターンを取り込んで実装する例が紹介されていた。
どのサービスで実現するとかではなく、アプリケーション実装に取り込むパターン。

[AWS Step Functionsにサーキットブレーカーパターンを組み込んでみた \| DevelopersIO](https://dev.classmethod.jp/articles/aws-step-functions-circuit-breaker-pattern/)

## クレームチェックパターン

[クレーム チェック パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/claim-check)

claim check：預り証
[預かり証って英語でなんて言うの？ - DMM英会話なんてuKnow?](https://eikaiwa.dmm.com/uknow/questions/139204/)

参照ベースのメッセージングとも呼ばれる。

> 大きいメッセージを要求チェックとペイロードに分割します。 要求チェックはメッセージング プラットフォームに送信し、ペイロードは外部サービスに格納します。 このパターンを使用して大きいメッセージを処理すると、メッセージ バスやクライアントで大きな負荷や速度の低下が発生するのを防ぐことができます。 

メッセージキューをつかったアプリケーションでは、メッセージに画像やテキストファイル、バイナリデータが含まれることがある。アプリケーションは、まず受け取ったメッセージのペイロード全体をデータベースなどの外部サービスに格納し、その格納先への参照をメッセージバス（キュー）に格納する。キューからメッセージを取り出したアプリケーションは参照をもとにデータベースを検索してペイロードを取得、処理をおこなう。このときの参照を荷物の預り証（クレームチェック）になぞらえている。

SQSのメッセージサイズは基本的に256KBに制限されている。
拡張クライアントライブラリを使うことでサイズが大きいメッセージオブジェクトをS3に保管することができるようになる。

[Amazon S3を使用した大量のAmazon SQSメッセージの管理 - Amazon Simple Queue Service](https://docs.aws.amazon.com/ja_jp/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-s3-messages.html)

## 補正トランザクションパターン

[補正トランザクション パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/compensating-transaction)

> 一連のステップで構成される最終的に整合性がある操作を使用するときは、補正トランザクション パターンが役立ちます。 具体的には、1 つ以上のステップが失敗した場合、補正トランザクション パターンを使用して、ステップで実行された作業を元に戻すことができます。 

クラウドアプリケーションでは、最終的整合性モデル（結果整合性モデル）が採用されていることがある（操作中のステップが実行されている間、システム状態を全体的に見ると整合性がないが、操作が完了し、すべてのステップが実行されると、システムは整合性のある状態になる）。
このとき、あるステップでエラーが発生したとき（単なる失敗ではなく、タイムアウトエラーの可能性もある）、前のステップで完了したすべての作業を元に戻す必要が生じる。データストアがひとつであるとは限らない、元に戻すものがデータストアにあるとは限らない（サービス志向アーキテクチャの場合など）。

補正トランザクションによって、元の操作のステップの影響を元に戻すが、このプロセスは同時実行される作業を考慮し、元の操作のステップの作業の質・特性（もしくはアプリケーション固有のビジネスルールなど）に依存したものになる。

> 2 つの重要点を次に示します。
> - 補正トランザクションでは、必ずしも元の操作の正反対の順序で作業を元に戻すとは限りません。
> - 元に戻すステップをいくつか並列で実行できることがあります。

> 補正トランザクションはそれ自体が最終的に整合性がある操作であるため、失敗することもあります。
> 場合によっては、手動介入のみが、失敗したステップから回復する方法であることがあります。 この場合、システムはアラートを発生させ、失敗の理由についてできるだけ多くの情報を提供する必要があります。

> 可能であれば、補正トランザクションを必要とする複雑さを持たないようにソリューションを設計します。

## 競合コンシューマーパターン

[競合コンシューマー パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/competing-consumers)

> 複数の同時実行コンシューマーが、同じメッセージング チャネルで受信したメッセージを処理できるようにします。 複数の同時実行コンシューマーがいる場合、システムは複数のメッセージを同時に処理して、スループットを最適化し、スケーラビリティと可用性を向上させ、ワークロードのバランスを取ることができます。

クライアントリクエストをSQSにキューイングしてLambdaで処理させる、という方式のこと。

## コンピューティングリソース統合パターン

[コンピューティング リソース統合パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/compute-resource-consolidation)

> 複数のタスクまたは操作を 1 つのコンピューティング単位に統合します。 これにより、コンピューティング リソースの使用率を高め、クラウドでホストされるアプリケーションでコンピューティング処理を実行することに関連するコストと管理オーバーヘッドを削減できます。

ソリューションでは個々のタスクに対して独立してホストし、それらには別個のコンピューティング（Lambda、EC2など）が割り当てられる（問題分離の設計原則）。

> コストの削減、使用率の向上、通信速度の向上、および管理の削減に役立つように、複数のタスクや操作を 1 つのコンピューティング単位に統合することが可能です。

統合してよいタスクなのかは同じようなスケーラビリティが求められるタスクなのかが基準になる。急激にリクエストが増加するタスクと低頻度でリクエスト数が少ないタスクを統合するのはリソースの無駄になる。

## CQRSパターン

[CQRS パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/cqrs)

CQRS=Command Query Responsibility Segregation

> CQRS はコマンド クエリ責務分離を表し、データ ストアの読み取りと更新の操作を分離するパターンです。 アプリケーション内に CQRS を実装すると、そのパフォーマンス、スケーラビリティ、セキュリティが最大化される場合があります。 CQRS への移行によって生まれる柔軟性により、システムは時間の経過と共にさらに進化し、更新コマンドでドメイン レベルのマージ競合が発生することを防ぐことができます。

コマンド=データの更新をおこなうためのもの、クエリ＝データを読み取るためのもの
データベースの更新とクエリに同じデータモデルを利用できないことがある。

> 読み取り側でさまざまなクエリが実行され、形式の異なる複数のデータ転送オブジェクト (DTO) が返される場合もあります。 これにより、オブジェクトのマッピングが複雑になる可能性があります。 また書き込み側のモデルでは、複雑な検証とビジネス ロジックが実装される可能性があります。 その結果、モデルが複雑になりすきる恐れがあります。

> データを更新するためのコマンドとデータを読み取るためのクエリを使用し、読み取りと書き込みを別々のモデルに分離します。

> - コマンドは、データ中心ではなく、タスクベースにします。 (「ReservationStatus を Reserved に設定する」などではなく、「ホテルの部屋を予約する」などの形式にします)。
> - コマンドは、同期的に処理するのではなく、非同期処理のキューに配置できます。
> - クエリでは、データベースは変更されません。 クエリでは、ドメイン ナレッジをカプセル化しない DTO が返されます。

## デプロイスタンプパターン

[デプロイ スタンプ パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/deployment-stamp)

> デプロイ スタンプ パターンには、複数のワークロードまたはテナントをホストおよび運用するための異種リソース グループのプロビジョニング、管理、監視が含まれます。 個々のコピーはスタンプと呼ばれ、サービス ユニット、スケール ユニット、またはセルと呼ばれる場合もあります。

> 複数のスタンプをデプロイして、ソリューションをほぼ直線的にスケーリングし、増加するテナントにサービスを提供できます。 このアプローチにより、ソリューションのスケーラビリティが向上し、インスタンスを複数のリージョンにデプロイすることが可能となり、顧客データを分離できます。

アプリケーションの動作に必要な一通りのリソース群をスタンプと呼び、スケーリングするときにそのスタンプ内のリソースのどれかを増強するのではなく、スタンプ自体を追加でデプロイするというパターン。

Azureには以下の例でデプロイスタンプを利用したパターンについて消化していた。

[デプロイ スタンプを使用して IoT ソリューションをスケーリングおよび管理する - Azure Example Scenarios \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/example-scenario/iot/application-stamps)

> デプロイ スタンプは、定義されたデバイス群をサポートする異種コンポーネントで構成されるユニットです。 デプロイ スタンプでは、ソリューションのさまざまな部分を個別にスケールアップするのではなく、スタンプをレプリケートすることで、接続されている IoT デバイスの数をスケールアップします。

AWSだとCloudWatchでスケーリングの必要性を検出し、CloudFormationで複数のリソースをデプロイするように設計するような感じか。

## エッジワークロード構成パターン

[Edge ワークロード構成パターン - Cloud Design Patterns \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/edge-workload-configuration)

作業現場（エッジロケーション）には様々なデバイスやシステムがあり、様々なプロトコル、ドライバー、データ形式をサポートするように構成されている。結果としてエッジロケーション内に様々な構成が存在したり、構成が1日に複数回更新される場合があったりとその構成管理は重要である。

エッジワークロードでの構成管理の特性

> - ソフトウェア ソース、CI/CD パイプライン、クラウド テナント、エッジの場所など、異なるレイヤーにグループ化できる構成ポイントがいくつかあります。
> - さまざまなレイヤーが異なる担当者によって更新される可能性があります。
> - 構成の更新方法に関係なく、慎重に追跡および監査する必要があります。
> - ビジネス継続性のためには、エッジで構成にオフラインでアクセスできる必要があります。
> - また、クラウドで利用できる、構成をグローバルに確認できるビューも必要です。

解決方法は存在するエッジワークロードによって変わる

- ワークロードの外部にある構成コントローラーを使う
- ワークロードの内部に存在する構成プロバイダーから構成をプルする内部構成プロバイダーを使う
- クラウド構成コントローラーとして機能するIoTハブを使う

## イベントソーシングパターン

[イベント ソーシング パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/event-sourcing)

> ドメインに、データの現在の状態だけを格納する代わりに、追加専用ストアを使用して、そのデータに対して実行された一連のすべてのアクションを記録します。 ストアは、レコードのシステムとして機能し、ドメイン オブジェクトを具体化するために使用できます。

> イベント ソーシング パターンは、一連のイベントによって制御されるデータへの操作の処理方法を定義し、各イベントが追加専用のストアに記録されます。 

Kinesis Data Streamsを利用してイベントを収集しつつ、イベントストアとして利用する。

## 外部構成ストアパターン

[外部構成ストア パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/external-configuration-store)

> アプリケーション展開パッケージから、一元管理される場所に構成情報を移動します。 

> 多くのアプリケーション ランタイム環境には、アプリケーションと共にデプロイされるファイルに保持される構成情報が含まれています。 場合によっては、これらのファイルを編集して、デプロイ後にアプリケーションの動作を変更することができます。

> ローカル構成ファイルでも構成は単一のアプリケーションに制限されていますが、複数のアプリケーションで構成設定を共有することが適している場合もあります。 たとえば、データベース接続文字列、UI テーマ情報、関連するアプリケーション セットに使用されるキューとストレージの URL があります。

> 外部ストレージに構成情報を格納し、構成設定の読み取りと更新をすばやく効率的に行うために使用できるインターフェイスを用意します。

> 多くの組み込み構成システムは、アプリケーションの起動時にデータを読み取り、データをメモリ内にキャッシュして高速なアクセスを提供し、アプリケーション参照に対する影響を最小限に抑えます。 

Systems ManagerパラメータストアおよびSecrets Managerで実現できる。

[よくある質問 - AWS Systems Manager \| AWS](https://aws.amazon.com/jp/systems-manager/faq/)

> Q: Parameter Store と Secrets Manager のどちらを使えば良いですか?
> 設定とシークレットにひとつのストアが欲しい場合、パラメータストアをお使いください。ライフサイクル管理を備えたシークレット専用のストアが欲しい場合、シークレットマネージャーをお使いください。

## フェデレーションIDパターン

[フェデレーション ID パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/federated-identity)

> 外部の ID プロバイダーに認証を委任します。 これにより、開発を簡略化し、ユーザー管理の要件を最小限に抑え、アプリケーションのユーザー エクスペリエンスを向上させることができます。

> フェデレーション ID を使用できる認証メカニズムを実装します。 アプリケーション コードからユーザー認証を分離し、信頼できる ID プロバイダーに認証を委任します。 これにより開発が簡略化され、管理オーバーヘッドを最小限に抑えながらより広い範囲の ID プロバイダー (IdP) を使用して認証できます。 承認から認証を明確に分離することもできます。

OIDCとかを使って外部IdPに認証を任せることができる。
あとは、Cognitoを使うことで認証機能自体をオフロードできる。

## ゲートキーパーパターン

[ゲートキーパー パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/gatekeeper)

> クライアントとアプリケーションまたはサービスとの間のブローカー要求に対する専用ホスト インスタンスを使用して、アプリケーションとサービスを保護します。 ブローカーは要求を検証してサニタイズし、セキュリティの追加の層を提供してシステムの攻撃面を制限できます。

AWS WAFがこれにあたるだろう。

## ゲートウェイ集約パターン

[ゲートウェイ集約パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/gateway-aggregation)

> ゲートウェイを使用して、複数の個々の要求を 1 つの要求に集約します。 このパターンは、クライアントが操作を実行するために、さまざまなバックエンド システムに複数の呼び出しを行う必要がある場合に便利です。

> タスクを実行するのに多くのサービスに依存するアプリケーションでは、要求ごとにリソースを展開する必要があります。 アプリケーションに新しい機能やサービスが追加されると、追加の要求が必要になり、リソース要件およびネットワーク呼び出しが増加します。 このクライアントとバックエンド間の頻繁な通信が、アプリケーションのパフォーマンスとスケールに悪影響を及ぼす可能性があります。

> 一般的に待機時間の長い携帯ネットワークでは、この方法で個々の要求を使用することは効率が悪く、接続が切断されたり、要求が不完全になったりする可能性があります。 要求は並列で実行できますが、アプリケーションは各要求のデータをすべて個別の接続で送信、待機、および処理する必要があるため、エラーが発生する可能性が高くなります。

> ゲートウェイはクライアント要求を受信し、さまざまなバックエンド システムに要求をディスパッチして結果を集計し、それらを要求元のクライアントに送り返します。

## ゲートウェイオフロードパターン

[ゲートウェイ オフロード パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/gateway-offloading)

> 共有または専用のサービス機能の負荷をゲートウェイ プロキシにオフロードします。 このパターンは、SSL 証明書の使用などの共有サービス機能を、アプリケーションの他の部分からゲートウェイに移動することで、アプリケーション開発をシンプルにします。

> 一部の機能、特に証明書の管理、認証、SSL 終了、監視、プロトコル変換、調整など、分野横断的な懸念事項を、ゲートウェイにオフロードします。

調整=Throttling

CloudFrontであっているはず。

## ゲートウェイルーティングパターン

[ゲートウェイ ルーティング パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/gateway-routing)

> 単一のエンドポイントを使用して複数のサービスまたは複数のサービス インスタンスに要求をルーティングします。 このパターンは次の場合に役立ちます。
> 
> - 単一のエンドポイントで複数のサービスを公開し、要求に基づいて適切なサービスにルーティングする
> - 負荷分散または可用性を目的として、1 つのエンドポイントで同じサービスの複数のインスタンスを公開する
> - 1 つのエンドポイントで同じサービスの異なるバージョンを公開し、異なるバージョン間でトラフィックをルーティングする

> 一連のアプリケーション、サービス、またはデプロイの前にゲートウェイを配置します。 

API Gatewayを使う。

## ジオードパターン

[Geode パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/geodes)

> Geode パターンでは、バックエンド サービスを一連の **Ge**ographical n**ode** (地理的ノード) にデプロイする必要があり、それぞれによって任意のリージョンで任意のクライアントの任意の要求を処理できます。 このパターンにより、"アクティブ/アクティブ" スタイルで要求を処理できるようになり、要求処理が世界中に分散されることで可用性が向上し、待機時間が短縮されます。

> 世界各地の Geode と呼ばれる数多くのサテライト拠点にサービスにデプロイしてください。

CLoudFrontでのLambda@EdgeとかRoute53によってユーザに地理的に一番近いリージョンのアプリケーションにルーティングするといったパターン。

## 正常性エンドポイントの監視パターン

[正常性エンドポイントの監視パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/health-endpoint-monitoring)

> アプリケーションとサービスが正常に実行されていることを確認するには、正常性エンドポイント監視パターンを使います。 このパターンには、アプリケーションの機能チェックの使用を指定します。 外部ツールは、公開されたエンドポイントを介して、定期的にこれらのチェックにアクセスできます。

## インデックステーブルパターン

[インデックス テーブル パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/index-table)

> クエリによって頻繁に参照されるデータ ストア内のフィールドにインデックスを作成します。 このパターンによって、アプリケーションがデータ ストアから目的のデータを取得するまでの時間が短縮されるため、クエリのパフォーマンスが向上します。

> データ ストアでセカンダリ インデックスがサポートされていない場合は、独自のインデックス テーブルを作成することにより、それらを手動でエミュレートすることができます。 インデックス テーブルでは、指定されたキーでデータが整理されます。 

## リーダー選定パターン

[リーダー選定パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/leader-election)

> 他のインスタンスを管理する役割を担うリーダーとして 1 つのインスタンスを選択することで、分散アプリケーション内で連携するインスタンスのコレクションによって実行されるアクションを調整します。 これにより、インスタンスが互いに競合して、共有リソースとの競合を引き起こしたり、他のインスタンスが実行されている作業に誤って干渉したりしないようにできます。

## 具体化されたビューパターン

[具体化されたビュー パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/materialized-view)

> データの形式が必要なクエリ操作に適していない場合に、1 つ以上のデータ ストアのデータの事前設定されたビューを生成します。 これにより、効率的なクエリとデータ抽出をサポートできるようになり、アプリケーションのパフォーマンスが向上します。

> データを保存するときに、開発者とデータ管理者は、多くの場合、データを読み取る方法ではなく、保存する方法を優先します。

> クエリで一部のエンティティのデータのサブセットだけが必要な場合 (注文の詳細がまったく含まれていない、複数の顧客の注文の概要など)、必要な情報を取得するために、関連するエンティティのすべてのデータを抽出する必要があります。

> 効率的なクエリをサポートするには、一般的な解決策として、必要な結果セットに適した形式でデータを具体化するビューを事前に生成します。 具体化されたビュー パターンでは、ソース データがクエリに適した形式ではない環境、適切なクエリの生成が難しい環境、またはデータやデータ ストアの性質に起因してクエリのパフォーマンスが低い環境で、データの事前設定されたビューを生成します。

## メッセージングブリッジパターン

[メッセージング ブリッジ パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/messaging-bridge)

複数のシステムがそれぞれにメッセージングインフラストラクチャ（RabbitMQ、Azure Service Bus、Amazon SQS など）に有しており、それらを統合するためのパターン。

> 2 つ以上のメッセージング インフラストラクチャに同時に接続するブリッジ コンポーネントを導入します。 ブリッジは一方からメッセージをプルし、ペイロードを変更することなくそれを他方にプッシュします。

> 統合されているシステムが、他のシステムやブリッジを認識する必要はありません。 送信側システムは、ネイティブ メッセージング インフラストラクチャ上の指定されたキューに特定のメッセージを送信するように構成されています。 ブリッジでメッセージが取得され、異なるメッセージング インフラストラクチャ内の別のキューに転送されると、受信側システムによってそこからメッセージが取得されます。

## パイプとフィルターのパターン

[パイプとフィルターのパターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/pipes-and-filters)

> 複雑な処理を実行するタスクを、再利用できる一連の独立した要素に分解します。 これを行うと、処理を実行する複数のタスク要素を別々にデプロイおよびスケーリングすることで、パフォーマンス、スケーラビリティ、再利用性を向上できます。

例えば2種類のソースからデータを受け取って処理するアプリケーションがあった場合、実行するタスクはモノリシックなモジュール内でそれぞれ処理します。
アプリケーションで実行されるタスクは重複していても別個にデプロイされます。

![pipes-and-filters-modules.png](https://drive.google.com/uc?export=view&id=1cQu9o8sgRXnTWFXOhmCcgqS_pQbpOal_)

タスクを分解して個々のコンポーネント（フィルター）とする。
データの処理全体はパイプラインと呼ばれ、データ処理に合わせてフィルターを組み合わせて定義される。フィルター間はメッセージキューで繋げられる。

![pipes-and-filters-solution.png](https://drive.google.com/uc?export=view&id=13w_xJH2NxJA9Mu13Yj_7MEWDhWRlZS89)

## Priority Queueパターン

[Priority Queue パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/priority-queue)

> サービスに送信される要求に優先順位を設定し、優先順位の高い要求から順番に受信および処理されるようにします。 このパターンは、個々のクライアントにそれぞれ異なるサービス レベルを保証するアプリケーションにおいて有用です。

> 一部のメッセージ キューでは、優先順位メッセージングをサポートします。 メッセージをポストするアプリケーションは、優先順位を割り当てることができます。 キュー内のメッセージは自動的に並べ替えられ、優先順位の高いものが優先順位の低いメッセージより先に受信されます。

> 優先順位に基づくメッセージ キューをサポートしないシステムでは、代替ソリューションとして、優先順位ごとに個別のキューを維持します。 メッセージを適切なキューに送信するのはアプリケーションの役割です。

AWSの場合、優先順位ごとに個別のSQSを容易することになる。

## パブリッシャーとサブスクライバーのパターン

[パブリッシャーとサブスクライバーのパターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/publisher-subscriber)

> 送信側と受信側を結合せずに、アプリケーションから関心を持っている複数のコンシューマーに対して非同期的にイベントを通知できるようにします。
> 別名:パブリッシュ/サブスクライブ メッセージング

> 以下を含む非同期メッセージング サブシステムを導入します。
> - 送信者によって使用される入力メッセージング チャネル。 送信者は、既知のメッセージ形式を使用して、メッセージ内にイベントをパッケージ化し、入力チャネルを介してこれらのメッセージを送信します。 このパターンの送信者は、パブリッシャーとも呼ばれます。
> - コンシューマーごとに 1 つの出力メッセージング チャネル。 コンシューマーはサブスクライバーとも呼ばれます。
> - そのメッセージに関心があるすべてのサブスクライバーのために、入力チャネルから出力チャネルに各メッセージをコピーするためのメカニズム。 この操作は通常、メッセージ ブローカーやイベント バスなどの仲介機能によって処理されます。

![publish-subscribe.png](https://drive.google.com/uc?export=view&id=1GziGmDU3UGhZQnmpbWiV3-roY91brwcH)

AWSではSNSでファンアウトできる。
Lambda関数からEventBridgeを呼び出し、EventBridgeがルールによって後続の配信先サブスクライバーを決定する方法もある。

## キュー ベースの負荷平準化パターン

[キュー ベースの負荷平準化パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/queue-based-load-leveling)

> タスクとそれによって呼び出されるサービスとの間のバッファーとして機能するキューを使用して、サービスの失敗やタスクのタイムアウトの原因となり得る断続的な高負荷を平準化します。これは、需要のピークによってタスクとサービスの両方の使用可能性と応答性が受ける影響を最小限に抑えるうえで役立つ場合があります。

> ソリューションをリファクタリングし、タスクとサービス間でキューを導入します。 タスクとサービスを非同期に実行します。 タスクは、キューにサービスで必要なデータを含むメッセージを投稿します。 キューは、サービスが取得するまでメッセージを格納するバッファーとして機能します。 サービスはキューからメッセージを取得して処理します。

## レート制限パターン

[レート制限パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/rate-limiting-pattern)

> 多くのサービスでは調整パターンを使用して自らが消費するリソースを制御し、他のアプリケーションやサービスからアクセスできるレートに制限を課します。 レート制限パターンを使用すると、これらの調整制限に関連する調整エラーを回避または最小化したり、スループットをより正確に予測したりするのに役立ちます。

調整パターン=スロットリングパターン

> レート制限パターンは多くのシナリオに適していますが、バッチ処理などの大規模な反復的自動化タスクで特にその効果を発揮します。

> 調整に使用されるメトリックに関係なく、レート制限の実装には、特定の期間にサービスに送信される操作の数とサイズ、またはその一方を制御することや、調整の容量を超えないようにしながらサービスの使用を最適化することが含まれます。


> - 調整で制限されているサービスによって発生する調整エラーを削減する。
> - エラーが発生したら再試行するという素朴なアプローチよりもトラフィックを削減する。
> - レコードを処理する容量がある場合にだけそれをデキューすることで、メモリ消費量を削減する。

スロットリングが設定されているサービスへのアクセス・リクエストによるエラー発生を減らすため、そのサービスへのアクセス・リクエスト前にレート制限を加える、といった感じだろうか。

## 再試行パターン

[再試行パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/retry)

> 一時的な障害をアプリケーションが処理できるようにします。アプリケーションがサービスまたはネットワーク リソースに接続しようとしたときに失敗した操作を透過的に再試行します。 これにより、アプリケーションの安定性を向上させることができます。

> 障害とは、たとえば、コンポーネントやサービスとのネットワーク接続が一瞬失われたり、サービスを一時的に利用できなくなったり、サービスがビジー状態となってタイムアウトしたりすることが該当します。

> クラウドでは、一時的な障害は珍しいことではないため、それらを適切かつ透過的に処理するようにアプリケーションを設計する必要があります。 これにより、アプリケーションによって実行されているビジネス タスクに与える可能性がある障害の影響を最小限に抑えることができます。

障害の処理方法は以下の通り

> - キャンセルする。 障害が一時的でないか、操作を繰り返しても成功する可能性が低い場合、アプリケーションは、操作をキャンセルして例外を報告する必要があります。 たとえば、無効な資格情報を提供することで発生した認証の失敗は、何回試しても成功する見込みはありません。
> - 再試行する。 報告された特定の障害が異常であるか、めったに発生しないものである場合は、ネットワーク パケットが転送中に破損しているといった普通でない状況が原因である可能性があります。 この場合、アプリケーションは、失敗した要求をすぐに再試行できます。これは、同じ障害が繰り返される可能性は低く、要求はおそらく成功するためです。
> - 時間をおいて再試行する。 障害の原因が、一般的な接続エラーまたはビジー エラーのいずれかである場合、ネットワークまたはサービスは、接続の問題が修正されるか作業のバックログがクリアされるための時間を必要とします。 アプリケーションは、要求を再試行する前に、適切な時間、待機する必要があります。

AWS SDKには再試行動作の設定が存在しており、再試行について考慮されている。
そのまま使っていれば問題ないとは思うが、エクスポネンシャルバックオフやジッターなどは目を通しておきたい。

[再試行動作 - AWSSDK とツール](https://docs.aws.amazon.com/ja_jp/sdkref/latest/guide/feature-retry-behavior.html)
[AWS SDKのエクスポネンシャルバックオフを確認してみた \| DevelopersIO](https://dev.classmethod.jp/articles/aws-sdk-exponential-backoff/)

## saga分散トランザクションパターン

[saga パターン - Azure Design Patterns \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/reference-architectures/saga/saga)

> saga 設計パターンは、分散トランザクション シナリオでマイクロサービス間のデータの一貫性を管理する方法です。 saga はトランザクションのシーケンスです。この saga によって各サービスが更新され、次のトランザクション ステップをトリガーするメッセージまたはイベントが発行されます。 また、ステップが失敗すると、その前のトランザクションを無効にする補正トランザクションを実行されます。


トランザクション：ロジックまたは作業の 1 つのユニットで、複数の操作で構成されることもあります。
イベント：トランザクション内でのエンティティに対して発生する状態変更
コマンド：アクションの実行や後のイベントのトリガーに必要な情報をカプセル化したもの

sagaパターンでのトランザクションは、ローカルトランザクションのシーケンスによって構成されている。ローカルトランザクションはsagaに参加する要素（各サービス）での作業工数である。各ローカルトランザクションによってデータベースが更新され、次のローカル トランザクションをトリガーするメッセージまたはイベントが発行される。ローカルトランザクションが失敗した場合、補正トランザクションが実行される。

補正可能なトランザクション：逆の効果を持つ別のトランザクションを処理することによって元に戻される可能性があるトランザクション
ピボットトランザクション：sagaの続行/中止ポイント。saga の補正も再試行もできないトランザクション、補正可能な最後のトランザクション、または再試行可能な最初のトランザクション
再試行可能なトランザクション：ピボットトランザクションに続くトランザクションで、成功が保証されている

> saga の実装アプローチとして一般的なのは、"コレオグラフィ" と "オーケストレーション" の 2 つです。 

## Scheduler Agent Supervisorパターン

[Scheduler Agent Supervisor パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/scheduler-agent-supervisor)

> 分散された一連のアクションを 1 つの操作として調整します。 いずれかのアクションが失敗した場合は、全体の操作が全体として成功または失敗するように、その失敗を透過的に処理しようとするか、または実行された作業を元に戻します。 これにより、一時的な例外、長期間続く障害、プロセスのエラーなどのために失敗したアクションを復旧して再試行することが可能になるため、分散システムに回復性が追加される場合があります。

このパターンで登場するアクター

- Scheduler：実行されるタスクを構成する手順を準備し、ワークフロー内の手順が正しい順序で実行されるようにすることに責任を負い、ワークフローの状態を記録する。状態情報には手順時間の上限（＝タイムアウト）の監理も含む。ある手順にリモート サービスまたはリソースへのアクセスが必要な場合、Scheduler は適切な Agent を呼び出す。Schedulerは非同期の要求/応答メッセージングやキューを使用して実装する。
- Agent：リモート サービスの呼び出し、またはタスク内の手順によって参照されるリモート リソースへのアクセスをカプセル化するロジックを含む。 各 Agent は通常、1 つのサービスまたはリソースの呼び出しをラップし、適切なエラー処理と再試行ロジックを実装する。
- Supervisor：Scheduler によって実行されているタスク内の手順の状態を監視する。定期的に実行され (頻度はシステムに固有です)、Scheduler によって保持されている手順の状態を調べる。タイムアウトまたは失敗したことを検出した場合は、その手順を復旧するか、または適切な是正アクションを実行する適切な Agent を準備します。 復旧または是正アクションはSupervisorが実行を要求し、実際にはScheduler と Agent によって実装される。

![scheduler-agent-supervisor-pattern.png](https://drive.google.com/uc?export=view&id=1ongqowNLyBKpqV_Z8ntML1RHqzHUijSR)

## シーケンシャルなコンボイパターン

[シーケンシャルなコンボイ パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/sequential-convoy)

> 他のメッセージ グループの処理をブロックせずに、関連する一連のメッセージを定義された順序で処理します。

異なるカテゴリのタスクを1つのFIFOキューにプッシュし、カテゴリごとのコンシューマが1度に1つずつロックしてプルして処理をおこなう。
カテゴリごとにプルできるので、インターリーブされてた結果として異なるカテゴリのタスクによって特定のコンシューマが空くようなことはない。

![sequential-convoy-overall.png](https://drive.google.com/uc?export=view&id=1DXlgByBu6_Thaqj0tzqPiwzwkSzReL1b)

[インターリーブとは - 意味をわかりやすく - IT用語辞典 e-Words](https://e-words.jp/w/%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%AA%E3%83%BC%E3%83%96.html)

> インターリーブ（interleaving）とは、データ入出力や通信において連続的に信号やデータを扱う際、時間や空間などの何らかの物理的な広がりに対してわざと不連続にデータを配置する手法。転送速度の向上や誤り訂正などのために行われる。

![sequential-convoy-queuemessages.png](https://drive.google.com/uc?export=view&id=1nXELd-URyNT01kVuXrMIlkmlo0mg07Vq)

FIFOを有効にしたSQSだとは思うが、カテゴリごとに別個にメッセージを取得することはできなかったと思う。カテゴリごとに個別のキューを用意することになる。

## シャーディングパターン

[シャーディング パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/sharding)

> データ ストアを水平方向のパーティションまたはシャードのセットに分割します。 これにより、データを大量に保存したり、膨大なデータにアクセスするときのスケーラビリティを改善できます。

ディスク容量、処理能力、メモリ、ネットワーク接続を垂直にスケールすることは、一時的な解決策にしかならない可能性がある。

> データ ストアを水平方向のパーティションやシャードに分割します。 各シャードにはスキーマがありますが、それぞれ特定のデータのサブセットを保持しています。 シャードは、自身の権限を持つデータ ストア (異なる種類の多数のエンティティのデータを格納できます) で、ストレージ ノードとして機能するサーバー上で動作します。

AWSのこのサービスと言うことはできないが、Kinesis Data StreamやElastiCache for Redis、Dynamo DBはシャーディングによって水平スケールすることで負荷に対処している。

[Amazon Kinesis Data Streams の用語と概念 - Amazon Kinesis Data Streams](https://docs.aws.amazon.com/ja_jp/streams/latest/dev/key-concepts.html)


## サイドカーパターン

[サイドカー パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/sidecar)

> アプリケーションのコンポーネントを別のプロセスまたはコンテナーにデプロイして、分離性とカプセル化を実現します。 このパターンは、種類が異なるコンポーネントとテクノロジでアプリケーションを構成することも可能にします。

> このパターンでは、サイドカーは親アプリケーションに接続され、アプリケーションにサポート機能を提供します。 また、サイドカーは、親アプリケーションと同じライフ サイクルを共有し、親アプリケーションと共に作成され、終了します。 サイドカー パターンは、サイドキック パターンと呼ばれることもある分解パターンです。

> 多くの場合、アプリケーションとサービスは、監視、ログ記録、構成、ネットワーク サービスなどの関連する機能を必要とします。 これらの周辺タスクを、独立したコンポーネントまたはサービスとして実装できます。

## 静的コンテンツ ホスティング パターン

[静的コンテンツ ホスティング パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/static-content-hosting)

> 静的コンテンツを、クライアントに直接配信できるクラウド ベースのストレージ サービスにデプロイします。 これにより、高額なコンピューティング インスタンスの必要性を低減できる可能性があります。

> ほとんどのクラウド ホスティング環境では、いくつかのアプリケーションのリソースと静的なページをストレージ サービスに配置することができます。 ストレージ サービスではこれらのリソースの要求を処理することができ、他の Web 要求を処理するコンピューティング リソースの負荷が軽減されます。 クラウドでホストされるストレージのコストは、通常、多くのコンピューティング インスタンスのコストよりも安価です。

S3には静的ウェブサイトをホスティングする機能がある。  
また、CloudFrontとS3を使って静的コンテンツを公開する方法もある。

[Amazon S3 を使用して静的ウェブサイトをホスティングする - Amazon Simple Storage Service](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/WebsiteHosting.html)

## ストラングラーフィグパターン

[ストラングラー フィグ パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/strangler-fig)

> 機能の特定の部分を新しいアプリケーションやサービスに徐々に置き換えることで、レガシ システムを段階的に移行します。 レガシ システムからの機能が置き換えられていくと、新しいシステムは最終的に古いシステムの機能すべてを置き換え、古いシステムを抑圧して使用停止できるようにします。

> 段階的に、機能の特定の部分を新しいアプリケーションやサービスに置き換えます。 バックエンド レガシ システムに送信される要求をインターセプトするファサードを作成します。 ファサードは、これらの要求をレガシ アプリケーションまたは新しいサービスにルーティングします。 既存の機能は段階的に新しいシステムに移行でき、コンシューマーは、移行が行われていることに気付くことなく、同じインターフェイスを引き続き使用できます。

![strangler.png](https://drive.google.com/uc?export=view&id=1wYC6zaL6YiTQItwASwiSN-zdLsODdGho)

[システム移行戦略「レガシーミミックパターン」＆「ストラングラーフィグパターン」とは？ #アーキテクチャ - Qiita](https://qiita.com/minorun365/items/6eeea65f6ddfbe3fb909#%E3%82%B9%E3%83%88%E3%83%A9%E3%83%B3%E3%82%B0%E3%83%A9%E3%83%BC%E3%83%95%E3%82%A3%E3%82%B0%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3%E3%81%A8%E3%81%AF)

> ストラングラーフィグというのは熱帯植物の名前で、他の樹木に寄生するように育ち最終的に包み込んでしまうそうです。（日本でも屋久島などで見られる模様）
この移行戦略も、まさに古いシステムをすこしずつ置き換えて廃止するプロセスをとります。

AWSのこのサービスと言うことはできないが、オンプレからクラウドへの移行とすればApplication Migration Service（MGN）は、継続的な移行をサポートするサービスのようだ。

マイクロサービスへの移行にはAWS Migration Hub Refactor Spacesがあるようだ（2024年1月時点でプレビューリリース）。

> リファクタリングスペースは、インクリメンタルリファクタリングのためにStrangler Fig パターンをモデル化するアプリケーションを提供します。リファクタリングスペースアプリケーションは、Amazon API Gateway、Network Load Balancer、およびリソースベースのオーケストレーションを行います。

[AWS Migration Hub ファクタリングスペースとは何ですか? - AWS Migration Hub リファクタリング](https://docs.aws.amazon.com/ja_jp/migrationhub-refactor-spaces/latest/userguide/what-is-mhub-refactor-spaces.html)


## 調整（Throttling）パターン

[調整パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/throttling)

> アプリケーションのインスタンス、個々のテナント、またはサービス全体によって使用されるリソースの使用量を制御します。 これによりシステムは、需要の増加に伴ってリソースに過度な負荷がかけられた場合でも正常な動作を継続し、サービス レベル アグリーメントに準拠することができます。

> 自動スケールに代わる戦略として、アプリケーションに上限までのリソースの使用を許可し、この上限に達したときに調整を行う方法があります。 使用量がしきい値を超えたときに 1 人または複数のユーザーの要求を制限できるよう、システムがリソースの使用状況を監視します。 これにより、システムは正常な動作を継続し、適用されるすべてのサービス レベル アグリーメント (SLA) に準拠することができます。

スロットリングパターンは以下のとおり。

- ユーザごとに一定時間ごとのアクセス回数の制限をおこなう
- 重要ではないサービスの機能を無効にする、サービスの品質を下げる（動画の低解像度モードへの切り替え）
- 負荷平準化をおこなう（優先順位の高い処理を優先して実行し、低い処理は中止する）
- 優先度が低い処理は操作を一時停止・制限する
- サードパーティサービスの正常復旧を待って再試行する（サーキット ブレーカーパターンみたいなこと）



## バレット キーパターン

[バレット キー パターン - Azure Architecture Center \| Microsoft Learn](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/valet-key)

> アプリケーションからのデータ転送をオフロードするため、クライアントに特定リソースへの限定的な直接アクセスを提供するトークンを使用します。 これは特に、クラウドでホストされるストレージ システムやキューを使用するアプリケーションで役に立ち、コストを最小限にしてスケーラビリティとパフォーマンスを最大化できます。

認可のパターンのこと。

アクセスを要求するクライアントにバレットキー（多くの場合、トークン）を提供し、このトークンによって特定のリソースへの時間制限付きアクセスを提供し、ストレージやキューに対する読み取りと書き込み、Web ブラウザーでのアップロードとダウンロードなど、定義済みの操作のみを許可します。

![valet-key-pattern.png](https://drive.google.com/uc?export=view&id=15cFfXviWHyG9D90pAc7AP2z2miXM8aoi)

S3には署名付きURLを使ってオブジェクトを共有できる機能がある。それと同じ。

[署名付き URL を使用したオブジェクトの共有 - Amazon Simple Storage Service](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html)
