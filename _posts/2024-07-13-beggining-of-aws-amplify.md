---
layout: post
title:  "AWS-Amplify入門"
date:   2024-07-13
categories: dev
---

# 入門の動機

- ASW Amplifyというものがあることを知った
- フロントエンド開発者に対してバックエンドやインフラ構築を半自動的に提供する体験をできそうなので試したくなった
  - [AWS Amplify コンセプト抜粋](https://docs.amplify.aws/react/how-amplify-works/concepts/)「AWS Amplify Gen 2 は、バックエンドの定義に TypeScript ベースのコードファースト開発者エクスペリエンス (DX) を使用します。Gen 2 DX は、ホスティング、バックエンド、UI 構築機能とコードファーストのアプローチを備えた統合された Amplify 開発者エクスペリエンスを提供します。Amplify を使用すると、フロントエンド開発者は、アプリのデータモデル、ビジネスロジック、認証、承認ルールを完全に TypeScript で表現するだけで、クラウドインフラストラクチャをデプロイできます。Amplify は適切なクラウドリソースを自動的に構成し、基盤となる AWS サービスをつなぎ合わせる必要がなくなります。」

# 入門の仕方

- [Front-End Web & Mobile on AWS](https://aws.amazon.com/jp/products/frontend-web-mobile/) みて概要把握
- [AWS Amplify Quick Start for React](https://docs.amplify.aws/react/start/quickstart/) を試す

# クイックスタートの実行結果の調査

- 特に問題なくデプロイまでできた
- [Amplifyコンソール画面](https://us-east-1.console.aws.amazon.com/amplify/apps)の当該アプリの「デプロイされたバックエンドリソース」から78個のバックエンドリソースが自動的に構築されたことが確認できた
- バックエンドリソースを整理することでシステムイメージが深まりそう
- amplify_outputs.jsonはgitignoreにコミット対象外ファイルとして定義済みだった
- TODO削除機能を追加してlocalhostで動作確認したら デプロイ環境で追加したTODOが表示された
- mainブランチ用バックエンドがローカル開発でも使われる(amplify_outputs.jsonが同じなので)
- TODO削除機能をmainブランチにpushしたら自動的にデプロイされて削除機能が使えた
- [アカウントセットアップ](https://docs.amplify.aws/react/start/account-setup/)は少し手こずったができた
- サンドボックスも作れた
- ユーザごとにTODOアイテムを持つように修正するとサンドボックスに自動的に反映されてデプロイされるようだ
- チュートリアル通りだとユーザごとのデータ取得のタイミングがおかしい気がする
- サインインした直後は以前のユーザのタスクが表示されるのがおかしい
- useEffectのタイミングでsetTodosするのが設計としておかしい気がする
- [useAuthenticatorフック](https://ui.docs.amplify.aws/react/connected-components/authenticator/advanced) を使えば良いのでは？
- Authenticator周りは追加で調査する

## 感想

- AWS Amplifyを使うことで、AWS::AppSync、AWS::CDK、AWS::Cognito、AWS::IAM、AWS::Lambda、AWS::S3、AWS::SSM、AWS::StepFunctionsがバックエンドリソースとして動いた
- これらのシステム動作イメージをつかみたい
- これをベースに独自アプリ作れそうな気がする
- コード修正してGitHubにpushするとビルド・デプロイまでされる体験はとても良い
- 知識なしにアプリ開発に集中できる体験が特に良い
- アプリ開発しながら必要な知識をつければ良さそうな点も良い
- この体験のためだけに課金する価値ある

## 参考

特になし
