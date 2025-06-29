---
layout: article
title: Agent2Agent仕様の認証と認可の翻訳
permalink: /docs/oidc_oauth/agent2agent_auth_translate
date: 2025-06-29
aside:
  toc: true
tags: ["Agent2Agent", "AI", "AIエージェント", "認証", "認証"]
---

Agent2Agentの仕様の認証と認可に関する章だけ翻訳したので、メモとして残しておく。

- v0.2.3
- [Specification - Agent2Agent (A2A) Protocol](https://a2aproject.github.io/A2A/latest/specification/#4-authentication-and-authorization) 4章


認証の方法はAgent2Agentでは定義されていません。OAuth 2.0で認可がおこなってそのトークンを使うか、APIキーを使うかなどの指定はありません。
AgentCardを使ってエージェントの能力や認証した方法など様々な情報がわかるようになっています。

## 翻訳

### 4. 認証と認可

A2Aは、エージェントを標準的なエンタープライズアプリケーションとして扱い、確立されたWebセキュリティプラクティスに準拠します。アイデンティティ情報はA2A JSON-RPCペイロード内では送信 **されず** 、HTTPトランスポート層で処理されます。

エンタープライズセキュリティの側面に関する包括的なガイドについては、[エンタープライズ対応機能](https://a2aproject.github.io/A2A/latest/topics/enterprise-ready/)を参照してください。

#### 4.1. トランスポートセキュリティ

セクション3.1に記載されているように、本番環境ではHTTPSを使用しなければなりません（MUST）。実装では、強力な暗号スイートを備えた最新の[TLS](https://datatracker.ietf.org/doc/html/rfc8446)構成（TLS 1.2以上を推奨）を使用すべきです（SHOULD）。

#### 4.2. サーバーアイデンティティの検証

A2Aクライアントは、TLSハンドシェイク中に信頼できる証明機関（CA）に対してTLS証明書を検証することにより、A2Aサーバーのアイデンティティを確認すべきです（SHOULD）。

#### 4.3. クライアント/ユーザーのアイデンティティと認証プロセス

1. **要件の検出**：クライアントは、[AgentCard](https://a2aproject.github.io/A2A/latest/specification/#55-agentcard-object-structure)の `authentication` フィールドを介してサーバーが必要とする認証スキームを検出します。スキーム名は、多くの場合、[OpenAPI認証方法](https://swagger.io/docs/specification/authentication/)と一致します（例、OAuth 2.0トークンの場合は「Bearer」、Basic認証の場合は「Basic」、APIキーの場合は「ApiKey」）。
2. **資格情報の取得（帯域外）**：クライアントは、必要な認証スキームとアイデンティティプロバイダに固有の **帯域外プロセス** を通じて、必要な資格情報（例、APIキー、OAuthトークン、JWT）を取得します。このプロセスはA2Aプロトコル自体の範囲外です。
3. 資格情報の送信:クライアントは、サーバーに送信するすべてのA2Aリクエストの適切な[HTTPヘッダー](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)(例、 `Authorization: Bearer <token>` 、 `X-API-Key: <value>)` ）にこれらの資格情報を含めます。

#### 4.4. 認証におけるサーバーの責任

A2Aサーバーは：

- 提供されたHTTP資格情報とAgentCardで宣言された認証要件に基づいて、すべての受信リクエストを認証しなければなりません（MUST）。
- 認証チャレンジまたは拒否には、[`401 Unauthorized`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/401)または[`403 Forbidden`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403)のようなの標準のHTTPステータスコードを使用すべきです（SHOULD）。
- 必要な認証スキームを示してクライアントを誘導するため、 `401 Unauthorized` レスポンスに関連するHTTPヘッダー（例、[WWW-Authenticate](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/WWW-Authenticate)）を含めるべきです（SHOULD）。

#### 4.5. タスク内認証（二次資格情報）

エージェントがタスクの実行中に、 __別の__ システムまたはリソースに対する __追加__ の資格情報を必要とする場合（例、独自の認証を必要とするユーザーに代わって特定のツールにアクセスする場合）は：

1. A2Aタスクを `auth-required` 状態（[`TaskState`](https://a2aproject.github.io/A2A/latest/specification/#63-taskstate-enum)参照）に遷移させるべきです（SHOULD）。
2. 付随する `TaskStatus.message` （多くの場合[`DataPart`](https://a2aproject.github.io/A2A/latest/specification/#653-datapart-object)）は、[`PushNotificationAuthenticationInfo`](https://a2aproject.github.io/A2A/latest/specification/#69-pushnotificationauthenticationinfo-object)のような構造を利用して必要性を記述するなど、必要な二次認証に関する詳細を提供すべきです（SHOULD）。
3. A2Aクライアントは、これらの新しい認証情報を帯域外で取得し、後続の[`message/send`](https://a2aproject.github.io/A2A/latest/specification/#71-messagesend)または[`message/stream`](https://a2aproject.github.io/A2A/latest/specification/#72-messagestream)リクエストで提供します。これらの資格情報の使用方法（例、エージェントがプロキシ接続している場合はA2Aメッセージ内のデータとして渡されるか、クライアントが二時システムと直接やり取りするために使用されるか）は、具体的なシナリオによって異なります。

#### 4.6. 認可

クライアントが認証されると、A2Aサーバーは認証されたクライアント/ユーザーのアイデンティティと自身のポリシーに基づいてリクエストを認可する責任を負います。認可ロジックは実装依存であり、以下の基準に基づいて適用されることがあります（MAY）。

- 特定のスキルの要求（例、AgentCardの `AgentSkill.id` で識別される）。
- タスク内で試行されたアクション。
- エージェントが管理するリソースに関連するデータアクセスポリシー。
- 該当する場合、提示されたトークンに関連付けられたOAuthスコープ。

サーバーは最小権限の原則を実装すべきです。
