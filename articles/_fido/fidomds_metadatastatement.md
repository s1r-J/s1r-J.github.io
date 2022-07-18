---
layout: article
title: FIDO MDSのMetadata Statementまとめ
permalink: /docs/fido/fido_mds_metadatastatement
date: 2022-07-18
aside:
  toc: true
tags: ["FIDO", "MDS", "メタデータサービス", "FIDO2", "FIDO U2F", "UAF"]
---

ブログに書いた記事と同じ内容を並び替えた。
MetadataのMetadataStatementプロパティ内の各プロパティについて、このサイトにメモしておきたかったので転記して残しておく。

Metadata Entryは[こちら](/docs/fido/fido_mds_entry)。

- [FIDO Metadata serviceのMetadata Statementのプロパティを勉強する - s1r-Jの技術ブログ](https://s1r-j.hatenablog.com/entry/2022/07/15/004701)

## おさらい

以前の記事で飛ばした部分、Metadata Entryの`metadataStatement`プロパティの中身についてまとめていく。

おさらいとして、前の記事では`metadataStatement`プロパティについて以下のように記載した。

----

- `metadataStatement`：非必須。認証器に関する情報。
	- 認証器に関する細かい情報が入っているようだ。後述の`statusReports`よりも細かい情報が欲しければこちらを使うのだろうか。非必須であるが、現時点で提供されている認証器データにはすべて含まれていた。
	- この項目は長いので、次回以降まとめる。
	- 参考：[Metadata Statement - FIDO Metadata Statement](https://fidoalliance.org/specs/mds/fido-metadata-statement-v3.0-ps-20210518.html#metadata-keys)

----

前回の振り返りおわり。

 `metadataStatement`はMDS バージョン2のEntryにはなかった項目であり、バージョン3からより詳細な認証器情報が提供されるようになった。
参考として記載した定義を和訳しつつ、実データなどを交えて勉強していく。

### Metadata Entryについて

MetadataEntryについての公式情報は以下のリンク先を参照されたし。

- [Entryの定義 - FIDO Metadata Service](https://fidoalliance.org/specs/mds/fido-metadata-service-v3.0-ps-20210518.html#metadata-blob-payload-entry-dictionary)

## Metadata Statement

`metadataStatement`に含まれるプロパティを一気に紹介していく。

- `legalHeader`：MDSを利用するための法的な合意事項。
	- 例として`https://fidoalliance.org/metadata/metadata-statement-legal-header/`というURLが記載されているように、ここに文言を入れる必要はないようだ。下記の実際のFIDO2認証器のメタデータでもURLが入っている。
- `aaguid`, `aaid`, `attestationCertificateKeyIdentifiers`：認証器のモデルを特定するための識別子。Entryにも存在する。
	- FIDO2の認証器は `aaguid`を持つ、FIDO UAFの認証器は`aaid`を持つ、FIDO U2Fの認証器は`attestationCertificateKeyIdentifiers`を持つ。なので、上記のいずれかのプロパティに値が入っている
- `description`：必須。人間が読むことができる認証器の端的な説明。英語で記載する。
- `alternativeDescription`： `description`プロパティと似た内容だが、英語以外の言語で記載する。
	- `{"ru-RU": "Пример UAF аутентификатора от FIDO Alliance", "fr-FR": "Exemple UAF authenticator de FIDO Alliance"}`のように言語コードをキー、認証器の説明をバリューとする。
- `authenticatorVersion`：必須。認証器のバージョン。符号なしの整数。
	- メタデータで指定された要件を満たす、最も古い（すなわち最も低い）信頼できるバージョン番号が入る。認証器のステータス（Entryの`statusReports`プロパティ参照）で認証器が信頼できない状態になってから修正されたらバージョンを変更する。
	- ここに記載されているバージョン番号のほうが利用している認証器のバージョン番号よりも大きい場合、リスクが高くなっていると考えられるので注意。
- `protocolFamily`：必須。認証器がサポートしているFIDOプロトコル。 
	- `uaf`、`u2f`、`fido2`のいずれか。
- `schema`：必須。現在のMetadata Statementがどのメタデータスキーマのバージョンのものかを示す。MDSバージョン3なので値は`3`になる。
- `upv`：必須。`upv`とはFIDOユニファイドプロトコルバージョン（おそらく認証器とクライアントの接続プロトコル）の略称。認証器がどのバージョンをサポートしているか示す配列。FIDO UAF、FIDO U2F、FIDO2で取る値が若干異なる。
	- FIDO UAFの場合、[FIDO UAF Protocol Specification](https://fidoalliance.org/specs/fido-uaf-v1.2-ps-20201020/fido-uaf-protocol-v1.2-ps-20201020.html#operationheader-dictionary)のOperationHeaderの`upv`に準拠するようにと書かれている。つまり、`major`が1で`minor`は2ということだが、[FIDO UAFの例](#fido-uaf認証器のmetadata-entry)とは異なっている。
	- FIDO U2Fの場合、`major`が1で`minor`が0ならU2F v1.0を示す。同様にv1.1、v1.2（=CTAP1）が取りうる値。
	- FIDO2の場合、`major`が2で`minor`が0ならCTAP2.0を示し、`major`が2で`minor`が1ならCTAP2.1を示す。
- `authenticaionAlgorithms`：必須（空配列も禁止）。認証器がサポートしている認証器アルゴリズムのリスト。
	- [FIDO Registry](https://fidoalliance.org/specs/common-specs/fido-registry-v2.1-ps-20191217.html#authentication-algorithms)のAuthenticator Algorithmsで定義されているアルゴリズム名で記載する。
- `publicKeyAlgAndEncodings`：必須（空配列も禁止）。認証器登録処理において認証器がサポートする公開鍵フォーマットのリスト。複数の値を取る場合には好ましいものをより先頭に並べる。
	- [FIDO Registry](https://fidoalliance.org/specs/common-specs/fido-registry-v2.1-ps-20191217.html#public-key-representation-formats)のPublic Key Representation Formatsで定義されているフォーマット名で記載する。
	- FIDO2ならば値としては`cose`が基本的に入っているはず？
- `attestationTypes`：必須。認証器がどのアテステーションタイプに対応したアテステーションを生成するのかを示したリスト。
	- [FIDO Registry](https://fidoalliance.org/specs/common-specs/fido-registry-v2.1-ps-20191217.html#authenticator-attestation-types)のAuthenticator Attestation Typesに定義された名称で記載する。
	- FIDO2のセルフコンフォーマンステストでもテスト項目になっている。このリストに無いアテステーションタイプのアテステーションだった場合には認証器登録を拒否しなければならない。
- `userVerificationDetails`：必須。ユーザ認証（User Verification）方式を示す2重の配列。
	- 外側の配列の要素同士はOR関係で、内側の配列の要素同士はAND関係になっている。
	- 下の例だと、(1) 指紋認証 または(2) パスコード認証 または(3) 顔認証かつ声帯認証 が利用できるユーザ認証方式となる
```
[
    [
      { "userVerificationMethod": "fingerprint_internal" }
    ],
    [
      { "userVerificationMethod": "passcode_internal" }
    ],
    [
      { "userVerificationMethod": "faceprint_internal"},
      { "userVerificationMethod": "voiceprint_internal"}
    ]
  ]
```
- `keyProtection`：必須（空配列も禁止）。認証器がサポートしているキープロテクションタイプ（作成した秘密鍵の保管、守り方）のリスト。
	- [FIDO Registry](https://fidoalliance.org/specs/common-specs/fido-registry-v2.1-ps-20191217.html#key-protection-types)のKey Protection Typesで定義されている名称で記載する。
	- 定義にかかれている`tee`とかはFIDO認証器の認定レベル（[Certified Authenticator Levels - FIDO Alliance](https://fidoalliance.org/certification/authenticator-certification-levels/)）にも出てきた。
- `isKeyRestricted`：秘密鍵の利用用途が認証器によってFIDOのアサーションへの証明だけに制限されているかを示す。
- 	`true`の場合またはこの項目が存在しない場合、FIDOのアサーションへの証明だけに制限。`false`の場合は制限されておらず、アプリケーションからFIDO以外での用途に利用される可能性がある。
- `isFreshUserVerificationRequired`：秘密鍵を利用する場合、必ず新鮮なユーザ認証（過去に実施されてキャッシュされているユーザ認証ではなく）を必要とするかを示す。
	- `true`の場合またはこの項目が存在しない場合、必ず新鮮なユーザ認証が必要。`false`の場合はキャッシュしたユーザ認証を利用する。
	- `false`の場合、ユーザの関与がなくなるため、ユーザ同意の実施は呼び出し元のアプリの責任となる。
- `matcherProtection`：空配列は禁止。認証器がサポートしているユーザ認証方式（matcher）の保護方式のリスト。
- [FIDO Registry](https://fidoalliance.org/specs/fido-v2.0-id-20180227/fido-registry-v2.0-id-20180227.html#matcher-protection-types)のMatcher Protection Typesで定義されている名称で記載する。
- `cryptoStrength`：認証器の暗号強度の値。値が存在しない場合、暗号強度が不明ということを示す。
- `attachmentHint`：空配列は禁止。認証器がサポートしている認証器とクライアントとの接続方法のヒントのリスト。
	- [FIDO Registry](https://fidoalliance.org/specs/common-specs/fido-registry-v2.1-ps-20191217.html#authenticator-attachment-hints)のAuthenticator Attachment Hintsで定義されている名称で記載する。
- `tcDisplay`：認証器がサポートしているトランザクションコンファーメーション表示のリスト。認証器がトランザクションコンファーメーションをサポートしていない場合、空配列にしなければならない。
	- [FIDO Registry](https://fidoalliance.org/specs/common-specs/fido-registry-v2.1-ps-20191217.html#transaction-confirmation-display-types)のTransaction Confirmation Display Typesで定義されている名称で記載する。
	- トランザクションコンファーメーション（transaction confirmation）とは、FIDO認証のさいに取引内容（transaction、ネットバンキングにおける振込指示やECストアにおける商品購入情報など）も改竄されておらず、ユーザが確認（confirmation）したと検証できる仕組みのこと。
		- 参考：[次世代認証技術を金融機関が導入する際の留意点：FIDOを中心に](https://www.imes.boj.or.jp/research/papers/japanese/kk35-4-2.pdf)
	- このプロパティでは、トランザクションコンファーメーションを実施するための保護方法を記載する。
- `tcDisplayContentType`：トランザクションコンファーメーション表示に利用されるMIMEタイプ。
	- 認証器がトランザクションコンファーメーションをサポートしている場合（前述の `tcDisplay`プロパティの配列が空ではない場合）、このプロパティは存在しなければならない。
- `tcDisplayPNGCharacteristics`：トランザクションコンファーメーション表示に利用するPNG画像の特徴（縦横の長さ、色など）のリスト。配列に複数要素がある場合は、代替となる画像の特徴となっている。
	- 認証器がトランザクションコンファーメーションをサポートしており（前述の `tcDisplay`プロパティの配列が空ではない場合）、かつ前述の`tcDisplayContentType`の値が`image/png`の場合、このプロパティは存在しなければならない。
- `attestationRootCertificates`：アテステーションのルート証明書（X509形式、Base64エンコーディング）、つまりトラストアンカー。複数存在する場合はルート証明書が複数存在しており、同じモデルの認証器でも異なるルート証明書に基づいてることがあるということ。証明書チェーンではない。
	- FIDO2のセルフコンフォーマンステストで利用したことがある。利用しなくてもテストは通過する。
- `ecdaaTrustAnchors`：ECDAAアテステーションに対して利用されるトラストアンカーのリスト。
	- このプロパティはUAF認証器だけが利用する。FIDO2だとECDAAは使っていない。
- `icon`：認証器のアイコン画像。
- `supportedExtensions`：サポートしている認証器拡張機能のリスト。
	- このプロパティはUAF認証器だけが利用する。FIDO2なら次の`authenticatorGetInfo`を参照する。
- `authenticatorGetInfo`：サポートしているバージョン（U2F、FIDO2、FIDO2.1Pre？）、拡張機能、AAGUIDやその機能（対応アルゴリズム等）のデータが入っている。認証器の外見なども含まれており、metadata statementと同じような内容が含まれている。
	- CTAPの`authenticatorGetInfo`メソッドが呼び出された際に認証器が返す情報になっている。
	- 参考：[Client to Authenticator Protocol (CTAP)](https://fidoalliance.org/specs/fido-v2.0-ps-20190130/fido-client-to-authenticator-protocol-v2.0-ps-20190130.html#authenticatorGetInfo)
	- 参考：[CTAP超ざっくりまとめ＆WindowsにFIDOキーでサインインする試み - Qiita](https://qiita.com/gebo/items/84ed5ec93aef843032c6)
	- 参考：[Web Authentication: An API for accessing Public Key Credentials - Level 2 | 9. WebAuthn Extensions](https://www.w3.org/TR/webauthn-2/#webauthn-extensions)

以上。
FIDOの認定試験の最初のステップであるセルフコンフォーマンステストで使った `attestationTypes`、一応利用した`attestationRootCertificates`あたりがWebでFIDO認証を行なう上では最も重要だと思う。

それ以外の項目については、一定レベルのセキュリティや機能が存在する認証器以外は利用させないなどの用途に用いるのだろうか。

## おわりに

[前回](https://s1r-j.hatenablog.com/entry/2021/11/30/020043)から半年以上あけてしまい、もはや何のための記事なのかわからないが勉強してよかった。

この半年の間には、FIDO2サーバのためのNode.jsのモジュールを作成してセルフコンフォーマンステストが通ることを確認したりと勉強はしてきた。モジュールはnpmで公開している。

- [@s1r-j/fido2server-lib - npm](https://www.npmjs.com/package/@s1r-j/fido2server-lib)

拡張機能の実装がまだまだできてなかったり、穴が多いモジュールなので今後も勉強して改善していきたい。

## Appendix

### FIDO2認証器のMetadata Entry

Yubico Bio Series

```json
		{
			"aaguid": "d8522d9f-575b-4866-88a9-ba99fa02f35b",
			"metadataStatement": {
				"legalHeader": "https://fidoalliance.org/metadata/metadata-statement-legal-header/",
				"aaguid": "d8522d9f-575b-4866-88a9-ba99fa02f35b",
				"description": "YubiKey Bio Series",
				"authenticatorVersion": 328965,
				"protocolFamily": "fido2",
				"schema": 3,
				"upv": [
					{
						"major": 1,
						"minor": 0
					},
					{
						"major": 1,
						"minor": 1
					}
				],
				"authenticationAlgorithms": [
					"secp256r1_ecdsa_sha256_raw",
					"ed25519_eddsa_sha512_raw"
				],
				"publicKeyAlgAndEncodings": [
					"cose"
				],
				"attestationTypes": [
					"basic_full"
				],
				"userVerificationDetails": [
					[
						{
							"userVerificationMethod": "none"
						}
					],
					[
						{
							"userVerificationMethod": "presence_internal"
						},
						{
							"userVerificationMethod": "fingerprint_internal",
							"baDesc": {
								"selfAttestedFRR": 0,
								"selfAttestedFAR": 0,
								"maxTemplates": 5,
								"maxRetries": 5,
								"blockSlowdown": 0
							}
						}
					],
					[
						{
							"userVerificationMethod": "passcode_external",
							"caDesc": {
								"base": 64,
								"minLength": 4,
								"maxRetries": 8,
								"blockSlowdown": 0
							}
						},
						{
							"userVerificationMethod": "presence_internal"
						}
					],
					[
						{
							"userVerificationMethod": "presence_internal"
						}
					],
					[
						{
							"userVerificationMethod": "passcode_external",
							"caDesc": {
								"base": 64,
								"minLength": 4,
								"maxRetries": 8,
								"blockSlowdown": 0
							}
						}
					],
					[
						{
							"userVerificationMethod": "fingerprint_internal",
							"baDesc": {
								"selfAttestedFRR": 0,
								"selfAttestedFAR": 0,
								"maxTemplates": 5,
								"maxRetries": 5,
								"blockSlowdown": 0
							}
						}
					]
				],
				"keyProtection": [
					"hardware",
					"secure_element"
				],
				"matcherProtection": [
					"on_chip"
				],
				"cryptoStrength": 128,
				"attachmentHint": [
					"external",
					"wired"
				],
				"tcDisplay": [],
				"attestationRootCertificates": [
					"MIIDHjCCAgagAwIBAgIEG0BT9zANBgkqhkiG9w0BAQsFADAuMSwwKgYDVQQDEyNZdWJpY28gVTJGIFJvb3QgQ0EgU2VyaWFsIDQ1NzIwMDYzMTAgFw0xNDA4MDEwMDAwMDBaGA8yMDUwMDkwNDAwMDAwMFowLjEsMCoGA1UEAxMjWXViaWNvIFUyRiBSb290IENBIFNlcmlhbCA0NTcyMDA2MzEwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC/jwYuhBVlqaiYWEMsrWFisgJ+PtM91eSrpI4TK7U53mwCIawSDHy8vUmk5N2KAj9abvT9NP5SMS1hQi3usxoYGonXQgfO6ZXyUA9a+KAkqdFnBnlyugSeCOep8EdZFfsaRFtMjkwz5Gcz2Py4vIYvCdMHPtwaz0bVuzneueIEz6TnQjE63Rdt2zbwnebwTG5ZybeWSwbzy+BJ34ZHcUhPAY89yJQXuE0IzMZFcEBbPNRbWECRKgjq//qT9nmDOFVlSRCt2wiqPSzluwn+v+suQEBsUjTGMEd25tKXXTkNW21wIWbxeSyUoTXwLvGS6xlwQSgNpk2qXYwf8iXg7VWZAgMBAAGjQjBAMB0GA1UdDgQWBBQgIvz0bNGJhjgpToksyKpP9xv9oDAPBgNVHRMECDAGAQH/AgEAMA4GA1UdDwEB/wQEAwIBBjANBgkqhkiG9w0BAQsFAAOCAQEAjvjuOMDSa+JXFCLyBKsycXtBVZsJ4Ue3LbaEsPY4MYN/hIQ5ZM5p7EjfcnMG4CtYkNsfNHc0AhBLdq45rnT87q/6O3vUEtNMafbhU6kthX7Y+9XFN9NpmYxr+ekVY5xOxi8h9JDIgoMP4VB1uS0aunL1IGqrNooL9mmFnL2kLVVee6/VR6C5+KSTCMCWppMuJIZII2v9o4dkoZ8Y7QRjQlLfYzd3qGtKbw7xaF1UsG/5xUb/Btwb2X2g4InpiB/yt/3CpQXpiWX/K4mBvUKiGn05ZsqeY1gx4g0xLBqcU9psmyPzK+Vsgw2jeRQ5JlKDyqE0hebfC1tvFu0CCrJFcw=="
				],
				"icon": "data:image/png;base64,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",
				"authenticatorGetInfo": {
					"versions": [
						"FIDO_2_0",
						"FIDO_2_1_PRE",
						"FIDO_2_1"
					],
					"extensions": [
						"credProtect",
						"hmac-secret",
						"largeBlobKey",
						"credBlob",
						"minPinLength"
					],
					"aaguid": "d8522d9f575b486688a9ba99fa02f35b",
					"options": {
						"plat": false,
						"rk": true,
						"clientPin": false,
						"up": true,
						"uv": false,
						"pinUvAuthToken": true,
						"largeBlobs": true,
						"bioEnroll": false,
						"userVerificationMgmtPreview": false,
						"authnrCfg": true,
						"credMgmt": true,
						"credentialMgmtPreview": true,
						"setMinPINLength": true,
						"makeCredUvNotRqd": false,
						"alwaysUv": true
					},
					"maxMsgSize": 1200,
					"pinUvAuthProtocols": [
						2,
						1
					],
					"maxCredentialCountInList": 8,
					"maxCredentialIdLength": 128,
					"transports": [
						"usb"
					],
					"algorithms": [
						{
							"type": "public-key",
							"alg": -7
						},
						{
							"type": "public-key",
							"alg": -8
						}
					],
					"maxSerializedLargeBlobArray": 1024,
					"minPINLength": 4,
					"firmwareVersion": 328965,
					"maxCredBlobLength": 32,
					"maxRPIDsForSetMinPINLength": 1,
					"preferredPlatformUvAttempts": 3,
					"uvModality": 2,
					"remainingDiscoverableCredentials": 25
				}
			},
			"statusReports": [
				{
					"status": "FIDO_CERTIFIED",
					"effectiveDate": "2021-08-06"
				},
				{
					"status": "FIDO_CERTIFIED_L1",
					"effectiveDate": "2021-08-06",
					"url": "www.yubico.com",
					"certificationDescriptor": "YubiKey Bio",
					"certificateNumber": "FIDO20020210806001",
					"certificationPolicyVersion": "1.3",
					"certificationRequirementsVersion": "1.4"
				}
			],
			"timeOfLastStatusChange": "2021-08-10"
		},
```


### FIDO UAF認証器のMetadata Entry


```json
		{
			"aaid": "4e4e#4005",
			"metadataStatement": {
				"legalHeader": "https://fidoalliance.org/metadata/metadata-statement-legal-header/",
				"aaid": "4e4e#4005",
				"description": "Touch ID, Face ID, or Passcode",
				"authenticatorVersion": 256,
				"protocolFamily": "uaf",
				"schema": 3,
				"upv": [
					{
						"major": 1,
						"minor": 0
					},
					{
						"major": 1,
						"minor": 1
					}
				],
				"authenticationAlgorithms": [
					"rsa_emsa_pkcs1_sha256_raw"
				],
				"publicKeyAlgAndEncodings": [
					"rsa_2048_raw"
				],
				"attestationTypes": [
					"basic_surrogate"
				],
				"userVerificationDetails": [
					[
						{
							"userVerificationMethod": "passcode_internal",
							"caDesc": {
								"base": 10,
								"minLength": 4,
								"maxRetries": 5,
								"blockSlowdown": 60
							}
						}
					],
					[
						{
							"userVerificationMethod": "fingerprint_internal",
							"baDesc": {
								"selfAttestedFRR": 0,
								"selfAttestedFAR": 0,
								"maxTemplates": 0,
								"maxRetries": 5,
								"blockSlowdown": 0
							}
						}
					]
				],
				"keyProtection": [
					"hardware",
					"tee"
				],
				"matcherProtection": [
					"tee"
				],
				"attachmentHint": [
					"internal"
				],
				"tcDisplay": [
					"any"
				],
				"tcDisplayContentType": "text/plain",
				"attestationRootCertificates": [],
				"icon": "data:image/png;base64,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"
			},
			"statusReports": [
				{
					"status": "NOT_FIDO_CERTIFIED",
					"effectiveDate": "2018-05-19"
				}
			],
			"timeOfLastStatusChange": "2018-05-19"
		},
```

### FIDO U2F認証器のMetadata Entry


```json
		{
			"attestationCertificateKeyIdentifiers": [
				"1434d2f277fe479c35ddf6aa4d08a07cbce99dd7"
			],
			"metadataStatement": {
				"legalHeader": "https://fidoalliance.org/metadata/metadata-statement-legal-header/",
				"attestationCertificateKeyIdentifiers": [
					"1434d2f277fe479c35ddf6aa4d08a07cbce99dd7"
				],
				"description": "NEOWAVE Winkeo FIDO2",
				"authenticatorVersion": 2,
				"protocolFamily": "u2f",
				"schema": 3,
				"upv": [
					{
						"major": 1,
						"minor": 1
					}
				],
				"authenticationAlgorithms": [
					"secp256r1_ecdsa_sha256_raw"
				],
				"publicKeyAlgAndEncodings": [
					"ecc_x962_raw"
				],
				"attestationTypes": [
					"basic_full"
				],
				"userVerificationDetails": [
					[
						{
							"userVerificationMethod": "presence_internal"
						}
					]
				],
				"keyProtection": [
					"hardware",
					"secure_element"
				],
				"matcherProtection": [
					"on_chip"
				],
				"cryptoStrength": 128,
				"attachmentHint": [
					"external",
					"wired"
				],
				"tcDisplay": [],
				"attestationRootCertificates": [
					"\n\n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"
				],
				"icon": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAIAAAD8GO2jAAACqUlEQVRIx2P8//8/Ay0BEwONwagFpFlw8cKFirIyR3t7S1Oz0KDgBfPm//z5k3izvn39lp+Ta2tltWTRIoTofxhYtXKllpq6srwCAikoRIVHvH379j9x4NSpU0AtQI1W5hZwQagPzp87V11ZiXAvIxj9Zzh54kRNZRWRPvj96xcDOM0zMTKiB9G8uXP//fsHNFRASLC+sXHm7Nlubu4Qm3bt3Llu7VpiLGCEmcuIacGZU6fB4cWQX1AQGx/n7OIyaeoUbV0diIvamluePXtGUST/+g32HSODhoYGRISFhaWppYWVlRUo+OHjh6b6BoosgHvqz58/cDl9ff3M7CwIe8+e3atXrqQgmeIokDKzs/X19EGy/xk6OzofP3pEWUbDsAYYRC3tbRwcHED2h/fv62pqCReOjCTmZE0trZy8XAj78KFDy5YuJd50VAsYcepKTU83NjWBqOnu7Hxw/wE+O/7jsgC315mZmRubm9nZ2YFqvnz+0lBfhzOg/qO7lQm/B+EAmHwLioogCo4cOrxk0WIiPUEgkpFBUnKymZk5hN3T1XX3zh1iYoKJcDTBA4qFubmtlYubC8j++vVrTVU1qHQhzQeMBHyhrKxcWFwMUXn61Kn5c+dSv8JJSEy0trGGsCf099+6dQsuxcLCCrH7P5IrSYgDeKFS39TEx8sHZH//9r2uGhFQN65fh2VPNoqqTCUlpeKyUmgxfPpMSWERMAMuX7asv7cXIqilrYXwFrxeg/qOuGZSdEzM3t17Dh06CPT0pk0bN23cCI9FYKZJz8hE98Hff38hDDY2diL90dHdpaurixawrCysre3tunq6iLTX0NAAToIsTx4/tndwiIyOAtYExFjAzc3t4+sLJL99/QosE0VFRe3s7RtbmoGVFUqcjTYdh78FAIhBLlNd7ju1AAAAAElFTkSuQmCC"
			},
			"statusReports": [
				{
					"status": "NOT_FIDO_CERTIFIED",
					"effectiveDate": "2021-09-21"
				}
			],
			"timeOfLastStatusChange": "2021-09-21"
		},
```
