---
layout: article
title: 認証器の認定レベルまとめ
permalink: /docs/fido/fido_authenticator_level
date: 2022-07-18
aside:
  toc: true
tags: ["FIDO", "FIDO2", "認定", "認証器"]
---

## 認証器の認定状況について

MDSのEntryの`statusReports`の`status`の値は認証器の認定状況を示す文字列となる。
これらの文字列が何を意味するのかを調べた。

MDSのEntryについては[こちら](/docs/fido/fido_mds_entry)。

AuthenticatorStatusは大きく分けて3つに分けられる

- 認定に関するステータス
- セキュリティ通知ステータス
- 情報ステータス

### 認定に関するステータス

FIDO認定を受けているのか受けていないのか、取り消されているのかを示すステータスコード。また、認定を受けている場合、どのレベルの認定を受けているのかを示す。

まずステータスコードについて示し、あとから[認定レベル](#認定レベル)について詳細に記載する。

- `NOT_FIDO_CERTIFIED`：FIDO認定を受けていない
  - 使わないほうがよさそう。
- `SELF_ASSERTION_SUBMITTED`：認証器ベンダーが自己診断チェックリストを完了し、FIDOアライアンスに提出している
  - 認証機ベンダーは、FIDO認定を受ける前に認証器が必要な要件を満たしていることを確認する自己診断チェックをおこなう必要があるようだ。
  - 自己診断チェックリストが公開されている場合、`url`にアクセスするためのURLを入れることができる。
  - 使わないほうがよさそう。
- `FIDO_CERTIFIED`：FIDO認定を受けている
  - 現在このステータスの認定制度は終了しており、`FIDO_CERTIFIED_L1`に置換される予定。
  - YubiKey Bio Seriesでもこの値の入っている要素と`FIDO_CERTIFIED_L1`の入っている要素がある。
- `FIDO_CERTIFIED_L1`：FIDO Authenticator cerificationレベル1認定
  - FIDO UAF、FIDO U2F、FIDO2の認定には最低限レベル1の認定を受けなければならない。
  - [Authenticator Level 1 - FIDO Alliance](https://fidoalliance.org/certification/authenticator-certification-levels/authenticator-level-1/)
- `FIDO_CERTIFIED_L1plus`：FIDO Authenticator cerificationレベル1+認定
- `FIDO_CERTIFIED_L2`：FIDO Authenticator cerificationレベル2認定
- `FIDO_CERTIFIED_L2plus`：FIDO Authenticator cerificationレベル2+認定
- `FIDO_CERTIFIED_L3`：FIDO Authenticator cerificationレベル3認定
- `FIDO_CERTIFIED_L3plus`：FIDO Authenticator cerificationレベル3+認定
- `REVOKED`：何らかの理由で認証器が信頼できないとFIDOアライアンスが判断
  - リライングパーティはこの認証器モデルの将来的な登録を拒否しなければならない。
  - 信頼できないと判断した理由を示すニュースや記事のURLが`url`に入る。

### 認定レベル

参考：
- [Certified Authenticator Levels - FIDO Alliance](https://fidoalliance.org/certification/authenticator-certification-levels/)
- [FIDO認証の技術と応用展開の最新状況](https://www.nii.ac.jp/openforum/upload/20190529AM_Auth_01_Gomi.pdf)

まず認定レベルの厳しさは以下の通り。数値が大きいほうがセキュリティが高くなっている。：

```
FIDO_CERTIFIED = FIDO_CERTIFIED_L1 < FIDO_CERTIFIED_L1plus <  FIDO_CERTIFIED_L2 < FIDO_CERTIFIED_L2plus < FIDO_CERTIFIED_L3 < FIDO_CERTIFIED_L3plus
```

認定レベルに対する要件の概要

![](https://i1.wp.com/fidoalliance.org/wp-content/uploads/2021/07/CHART-2.png?resize=768%2C201&ssl=1)

とりあえず、ざっくりした翻訳

| レベル | ハードウェアおよびソフトウェア要件 | 防御対象 | 実装例 |
|:--:|:--|:--|:--|
| レベル1 | ハードウェア、ソフトウェアともに制限なし | ソフトウェアおよびベストプラクティスによってフィッシング攻撃および大部分のスケーラブル攻撃を防ぐ | レベル1は全ての認定に必須となるセキュリティレベル |
| レベル2 | デバイスは機密動作環境（TEE、セキュリティエレメントなど）のサポートが必要 | 機密動作環境によってリモートソフトウェア攻撃を防ぐ | 機密動作環境（セキュリティキーやTEE等）の実装 |
| レベル3 | 機密動作環境をサポートし、認証器への物理的な攻撃に対するセキュリティ耐性を持つデバイス | 機密動作環境によってリモートソフトウェア攻撃およびローカルハードウェア攻撃を防ぐ | [GlobalPlatform](https://globalplatform.org/technical-committees/trusted-execution-environment-tee-%E5%A7%94%E5%93%A1%E4%BC%9A/?lang=ja)に認定されたTEE、[Common Criteria](https://www.commoncriteriaportal.org/)に認定されたセキュアなエレメント |

- 機密動作環境（Restricted Operating Environments, ROE）：認証器アプリケーションのようなセキュリティを高くしたいアプリを実行できるような環境（[FIDO Authenticator Allowed Restricted Operating Environments List](https://fidoalliance.org/specs/fido-security-requirements/fido-authenticator-allowed-restricted-operating-environments-list-v1.2-fd-20201102.html)）
- 許可された機密動作環境（Allowed Restricted Operating Environments, AROE）：FIDOアライアンスに認められた機密動作環境

#### レベル1

[Authenticator Level 1 - FIDO Alliance](https://fidoalliance.org/certification/authenticator-certification-levels/authenticator-level-1/)

以下の4つのどれかに属する認証器はレベル1に該当する。

1. 同じ環境で実行されている他の多くのアプリケーションに対し、認証器セキュリティパラメータを効果的に防御できないハイレベル・オペレーティング・システム（HLOS）上で実行されている認証器アプリケーション
2. 同じ環境で実行されている他の多くのアプリケーションに対し、HLOSを攻撃することを除いて認証器セキュリティパラメータを効果的に防御できるHLOS上で実行されている認証器アプリケーション
3. 項2と同様だが、許可された機密動作環境（AROE）に保持したシークレット認証器セキュリティパラメータを保持する
4. AROE内で全て実装されている認証器（この認証器は、通常レベル2プラスを満たす）

ここだけを読むと「公開鍵・秘密鍵の作成ができれば何でもよい」と書かれているように見えるが、もっと詳しく仕様には書かれているのだろうか。

また、ハイレベル・オペレーティング・システム（HLOS）は何なのかよくわからなかった。AndroidはHLOSと書かれているような記事もあったので一般的なOSはHLOSなのだろうか。

#### レベル1プラス

[Authenticator Level 1+ - FIDO Alliance](https://fidoalliance.org/authenticator-level-1/)

レベル1プラスはレベル1とほぼ同じだが、ホワイトボックス暗号方式を実装している。

ホワイトボックス暗号方式：内部アルゴリズムが公開されている暗号方式。従来のブラックボックス方式の暗号方式では、攻撃者に内部アルゴリズムを推測されたり、信頼できない環境で実行されたりすると脆弱になる。（[ホワイトボックス暗号方式とは何か](http://support.safenet-inc.jp/srm/tech_note/wp/Web_WP_Whitebox_Cryptography.pdf)）

レベル1プラスには、大規模なソフトウェア攻撃に対する防御が必要。また、デバイスのOSが攻撃されても認証器アプリケーションを保護する。保護方法はAROEではなく、ホワイトボックス暗号方式およびその他のソフトウェア保護技術が用いられる。

暗号方式がホワイトボックス暗号方式となることで、デバイス自体を攻撃されてもある程度防御できるということだろう。

レベル1プラスの時点で認証器の実装が難しいそう。一般的な利用にはレベル1でも充分かもしれない。

#### レベル2

[Authenticator Level 2 - FIDO Alliance](https://fidoalliance.org/certification/authenticator-certification-levels/authenticator-level-2/)

レベル2は一般的なスケーラブルな攻撃に対抗できる認証器であることが求められる。
AROEおよび認証器セキュリティ要件にリスト化されている認可された暗号方式を実装している必要がある。ROEを持たない認証器やアテステーションをサポートしていない認証器はレベル2とは認定されない。

スケーラブルな攻撃：FIDOでは攻撃対象を追加するときにかかる労力・コストがほぼゼロ（=拡張性が高い（スケーラブル）？）となるような攻撃を指す。攻撃者が攻撃準備に手間をかけずに住むようなレベルとしては低い攻撃。

ROEの実装というのがレベル1との違いのようだ。

#### レベル2プラス

レベル2プラスは現在定義されていないらしく、要件を見つけることができなかった。

#### レベル3

[Authenticator Level 3 - FIDO Alliance](https://fidoalliance.org/certification/authenticator-certification-levels/authenticator-level-3/)

レベル3は強化された一般的なレベルでのソフトウェア攻撃およびハードウェア攻撃に対する防御を持つ認証器であることが求められる。
AROEおよび認証器セキュリティ要件にリスト化されている認可された暗号方式を実装している必要がある。CPUやメモリ、認証器自体の物理的なケースも攻撃に対抗できるものであることが必要らしい。

レベル3になると認証器を物理的にも守る必要があるようだ。

##### レベル3プラス

[Authenticator Level 3+ - FIDO Alliance](https://fidoalliance.org/certification/authenticator-certification-levels/authenticator-level-3-plus/)

レベル3プラスは（レベル3では一般的レベルだったのに対して）中程度または高いレベルでのソフトウェア攻撃およびハードウェア攻撃に対する防御を持つ認証器であることが求められる。

中程度または高いレベルでの攻撃：数週間から数ヶ月かけて高度に専門的な電子実験機器を用いたチップレベルへの攻撃

AROEおよび認証器セキュリティ要件にリスト化されている認可された暗号方式を実装している必要がある。

### セキュリティ通知ステータス

認証器にセキュリティに関する脆弱性が存在する場合、これらのステータスコードが利用される。
基本的にはリライングパーティでは公開鍵の登録を拒否するべきと思われる。

- `USER_VERIFICATION_BYPASS`：マルウェアがユーザ認証をバイパスできる
  - ユーザの同意なしに、潜在的にはユーザの知識（パスワードやPINコード）なしに認証器が利用されうる。
- `ATTESTATION_KEY_COMPROMISE`：認証器のアテステーション・キーの信頼が損なわれている
  - リライングパーティは`certificate`フィールドを確認して侵害されたアテステーション・キーを特定するべきである。`certificate`がセットされていない場合、この認証器による登録は全て拒否するべきである。
  - `url`にはインシデントに関するニュースや記事のURLが入る。
- `USER_KEY_REMOTE_COMPROMISE`：登録されたキーの信頼性が損なわれるような脆弱性が認証器に見つかっており、この認証器は信頼すべきではない
  - キーが推測できたり、偽造できたり、盗み出せたりする脆弱性も含む。
  - `url`にはインシデントに関するニュースや記事のURLが入る。
- `USER_KEY_PHYSICAL_COMPROMISE`：認証器のキー防御機構に脆弱性が見つかり、デバイスを物理的に所有している攻撃者によってユーザのキーが盗み出せる
  - `url`にはインシデントに関するニュースや記事のURLが入る。

### 情報ステータス

上記以外の何らかの情報を示すステータスコード。現状は1種類しか定義されていない。
一応、認証器を利用できるが、何らかの情報を提供したいときに使うものらしい。

- `UPDATE_AVAILABLE`：認証器のソフトウェアまたはファームウェアのアップデートが利用可能
  - `url`にはアップデートを入手できるURLをセットする。
  - `authenticatorVersion`には認証器の新しいバージョンを設定する。また、metadata statement内の`authenticatorVersion`と一致しなければならない。
  - 重大なセキュリティ脆弱性に対する修正アップデートの場合、このステータスコードではなく、セキュリティ通知ステータスのステータスまたはREVOKEDを利用しなければならない。
