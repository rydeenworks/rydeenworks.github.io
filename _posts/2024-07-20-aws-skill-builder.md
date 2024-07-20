---
layout: post
title:  "AWS BUILDERS ONLINE SERIESセッションを視聴した感想"
date:   2024-07-20
categories: dev
---

# 概要

[AWS BUILDERS ONLINE SERIESのアジェンダ](https://pages.awscloud.com/rs/112-TZM-766/images/AWS-Builders-Online-Series_2024-Q3_Agenda.pdf)

[視聴ページ](https://buildersonline.awslivestream.com/?trk=21aceb35-5bb1-40a9-aa1c-94db6b7ca4dc&trkcampaign=builders-online-seri)

ちょうどAWSを使ったモダンなアプリケーション開発をAmplifyを通じて学習中だったので、参加を申し込みました。以下のセッションをリアルタイムで視聴しました。自分のレベルにちょうど合っていて大変ためになりました。
- BOS-08: はじめてのコンテナワークロード - AWS でのコンテナ活⽤の第⼀歩
- BOS-09: はじめてのサーバーレス - AWS Lambda でサーバーレスアプリケーション開発
- BOS-10: AWS ではじめるオブザーバビリティ - システムのどこで・何が・なぜ起こってるのかを理解する 
- BOS-11: AWS Amplify ではじめる Webアプリケーション開発

# 感想

## BOS-08: はじめてのコンテナワークロード

- 業務でコンテナ使ったことなかったので、概要が掴みやすい内容で良かった
- コンテナ利用の目的や背景の説明が丁寧だった点が良かった
- コンテナサービスを個別に取り上げて説明してくれて良かった
  - オーケストレーション
    - Amazon ECS
    - Amazon EKS
  - レジストリ
    - Amazon ECR
  - コンピューティング
    - AWS Fargate(コンテナをサーバーレスで動作させるコンテナ実行環境)
  - フルマネージド
    - AWS App Runner
- コンテナ実行の基本的なフローの説明によりサービス構成がイメージしやすくて良かった
- AWS App Runnerはちょっと難しかった
- 「構築済みのインフラにすぐにデプロイ」するのがApp Runnerの役割と理解した
- AWS Amplifyもすぐにデプロイできるが、Amplifyの場合はコンテナを使ってない(バックエンドサービスにコンテナサービスは見当たらないので)
- [AppRnnerの開発者ガイド](https://docs.aws.amazon.com/apprunner/latest/dg/what-is-apprunner.html)を見ると「AWS App Runner は、ソースコードまたはコンテナイメージから AWS クラウド内のスケーラブルで安全な Web アプリケーションに直接デプロイする」と書いてある。
- ソースコードからデプロイするならAmplifyと同じだろうか？

## BOS-09: はじめてのサーバーレス

- サーバレスとは？から説明してくれて良かった
- 従来のWeb３層アーキテクチャとの対比の説明があって良かった
- Amazon API Gateway/DynamoDB/S3は使ったことがなかったので説明があって良かった
- AWS Lambda/DynamoDBの実装デモで具体的なイメージが理解できた
- Lambda関数にDynamoDBへのアクセス権限を付与する操作が見れて良かった
- Lambda関数がHttpリクエストを受け付けるための実装が見れて良かった
- POST/GETコマンドに対する処理をLambda関数内部に実装していた
- Lambda Function URLsの設定操作を見れて良かった
- S3コンソール画面で設定の一例として紹介があったのも良かった
- ハンズオンが色々あるようなので、そこから始めたい

## BOS-10: AWS ではじめるオブザーバビリティ

- 基本的なところからオブザーバビリティについて説明してくれて良かった
- 従来の監視と現代の監視の違いがイメージできた
- メトリクス・ログ・トレースという考え方はなかったので知れて良かった
- Amazon CloudWatch / AWS X-Rayの役割がイメージができた
- デモがあることで具体的な使い方がイメージできた

## BOS-11: AWS Amplify ではじめる Webアプリケーション開発

- Webアプリケーションとその開発方法から説明してくれてありがたい
- 「制限のない拡張性 - CDKで任意のAWSサービスを追加」という部分について自分で試せるようになりたい
- Amplifyプロジェクトのディレクトリ構成規約があるの気づいてなかったので知れて良かった
- [公式Doc](https://docs.amplify.aws/react/reference/project-structure/)にProject Structureの説明があったの気づいてなかった
- testブランチで開発してmainブランチにプルリクしてマージする時のAmlifyの挙動をデモで見れたのが良かった
- [Amplify Gen 2 Workshop](https://catalog.workshops.aws/amplify-core/en-US)というのがあるので、試すと良さそう

## まとめ

- 参加して良かった
- アンケートに回答してセッション資料をもらえた
- 資料を見返してブログ記事を書くのにとても役に立った
- 各セッションのアーカイブ動画も公開中なのでデモでの操作画面とか見返せて良い
- チュートリアルやハンズオンがたくさんあることがわかったので試したい

## 参考

[AWS ハンズオン資料](https://aws.amazon.com/jp/events/aws-event-resource/hands-on/)
