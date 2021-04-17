---
layout: article
title: Jenkinsに関するリンクまとめ
permalink: /docs/java/jenkins_links
date: 2021-04-18
aside:
  toc: true
tags: ["Java", "Jenkins", "Gradle"]
---

Jenkinsの勉強中なのでそのリンク一覧

## Jenkins

まずは公式ドキュメント

- [Jenkins](https://www.jenkins.io/)

Jenkinsで実行する内容（実行するコマンド等）をファイルに書き出すことができ、Jenkinsfileと呼称する。Gitなどでソースコード管理できるのでGood。  
その書き方についてのリンク。

- [Jenkinsの設定を最小限でJenkinsfile(Pipeline)を使う - Qiita](https://qiita.com/comefigo/items/fc7aad310235caf89fcd)
- [Jenkinsfileの書き方 (Jenkins Pipeline) - Qiita](https://qiita.com/dublog/items/38831adf42e3cfeed66a)
- [Jenkinsfileの書き方 - Qiita](https://qiita.com/lufia/items/18cdb01f86a6d5040c60)
- [Jenkinsfileの書き方 - Plan 9とGo言語のブログ](https://blog.lufia.org/entry/2018/01/19/000000)
- [Declarative PipelineでJenkinsfileを書いてみた(Checkstyle,Findbugs,PMD,CPDとか) - Qiita](https://qiita.com/Takumon/items/e266146c225d07b82c13)

Javaプロジェクトでの注意点。

- [gradle - gradlew: Permission Denied - Stack Overflow](https://stackoverflow.com/questions/17668265/gradlew-permission-denied)
- [HTML Publisher \| Jenkins plugin](https://plugins.jenkins.io/htmlpublisher/)


複数のジョブを設定し始めると、各Jenkinsfileで共通で使っている内容が出てくる。DRYを避けるには共有ライブラリという機能を使う。

- [Extending with Shared Libraries](https://www.jenkins.io/doc/book/pipeline/shared-libraries/)
- [Jenkins Shared Libraryで快適 Jenkins 生活？ - Qiita](https://qiita.com/bols_blue/items/50b024cf423439e8e99a)
- [Jenkinsで共有ライブラリを作成してみる - ヒトリ歩き](https://kotapontan.hatenablog.com/entry/2019/08/27/235603)
