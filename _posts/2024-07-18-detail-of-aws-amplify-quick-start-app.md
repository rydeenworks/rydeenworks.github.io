---
layout: post
title:  "AWS-Amplifyのクイックスタートアプリの詳細調査(AppSync,CDK)"
date:   2024-07-19
categories: dev
---

# AWS-Amplifyのクイックスタートで開発したアプリのシステム構成

## バックエンドリソース一覧

- AWS::AppSync
- AWS::CDK
- AWS::Cognito
- AWS::IAM
- AWS::Lambda
- AWS::S3
- AWS::SSM
- AWS::StepFunctions

## [AWS::AppSync](https://aws.amazon.com/jp/appsync/)

### 概要

公式ページの説明は次のとおり。

> ウェブとモバイルのフロントエンド
> 
> 安全でサーバーレスで高性能な GraphQL と Pub/Sub API を使用して、アプリをデータやイベントに接続

> 1 つのネットワークリクエストで、1 つまたは複数のソースやマイクロサービスからデータにアクセスできますAPI を 1 つのマージ済み API に結合します。
>
> サーバーレスの WebSocket を通じて、任意のイベントソースからサブスクライブしたクライアントにデータを公開することで、魅力的なリアルタイムエクスペリエンスを実現します。
>
> セキュリティ、監視、ロギング、トレースが組み込まれています。低レイテンシーを実現するオプションのキャッシュ。
>
> API へのリクエストと、接続されたクライアントに配信されたリアルタイムのメッセージに対してのみお支払いいただけます。

> 仕組み
>
> AWS AppSync は、サーバーレスの GraphQL および Pub/Sub API を作成し、単一のエンドポイントを通じて安全にデータの照会、更新、公開を行うことで、アプリケーションの開発を簡素化します。 

AppSync - GraphQLシステム構成図

![2024-07-18_appsync_graphql.png]({{site.baseurl}}/assets/2024-07-18_appsync_graphql.png)

AppSync - Pub/Sub APIシステム構成図

![2024-07-18_pubsub_api.png]({{site.baseurl}}/assets/2024-07-18_pubsub_api.png)

### クイックスタートアプリの実装(AppSync GraphQL API)

[コンセプト説明ページのDataセクション](https://docs.amplify.aws/react/how-amplify-works/concepts/#data)に次の説明がある。

「The @aws-amplify/backend library offers a TypeScript-first Data library for setting up fully typed real-time APIs (powered by AWS AppSync GraphQL APIs) and NoSQL databases (powered by Amazon DynamoDB tables). After you generate an Amplify backend, you will have an amplify/data/resource.ts file, which will contain your app's data schema. The defineData function turns the schema into a fully functioning data backend with all the boilerplate handled automatically.」

つまり、@aws-amplify/backendを使うことで、resource.tsのスキーマ定義に応じたGraphQL APIが自動的に用意される。


resource.tsでTodoというスキーマを定義している。
``` javascript
const schema = a.schema({
  Todo: a
    .model({
      content: a.string(),
    })
    .authorization((allow) => [allow.owner()]),
});
```

App.tsxでcreateTodo/deleteTodo/fetchTodoなどTODOタスク操作を実現している。
``` javascript
  function deleteTodo(id: string) {
    client.models.Todo.delete({id});
  }
```

clientはApp.tsxで以下のように実装している。
``` javascript
const client = generateClient<Schema>();
```

generateClientはAmplifyライブラリ側の実装となるが、ソースコードを見ると次のようになっている。
node_modules/@aws-amplify/api/dist/esm/API.d.ts
``` javascript
import { CommonPublicClientOptions, V6Client } from '@aws-amplify/api-graphql';
/**
 * Generates an API client that can work with models or raw GraphQL
 */
export declare function generateClient<T extends Record<any, any> = never>(options?: CommonPublicClientOptions): V6Client<T>;
```

コメントに書いてあるとおりclientを使うことで、GraphQLのAPIを隠蔽してモデルを操作できるという事。

前掲のConceptページには以下の記載がある。
「On your app's frontend, you can use the generateClient function, which provides a typed client instance, making it easy to integrate CRUD (create, read, update, delete) operations for your models in your application code.」
つまりCRUD


### クイックスタートアプリの実装(AppSync Pub/Sub API)

以下ソースコードのsubscribe/unsubscribeがPub/Sub API呼び出しに該当する。
subscribeしておくと、1つ目のWebページでTodoタスクを追加すると、
2つ目のWebページにもリアルタイムでTodoタスクが追加される挙動にできる。

``` javascript
  useEffect(() => {
    console.log("useEffect::user=" + user);
    if (user) {
      fetchTodos();
    }
    const subscribe = client.models.Todo.observeQuery().subscribe({
      next: (data) => {
        console.log("useEffect::Todo.observeQuery()>>>setTodos");
        setTodos([...data.items]);
      },
    });
    return () => {
      console.log("useEffect::unsubscribe()");
      subscribe.unsubscribe();
      setTodos([]);
    }
  }, [user]);
```

[Build & connect backend > Data > Subscribe to real-time events](https://docs.amplify.aws/react/build-a-backend/data/subscribe-data/)ページに詳しい説明が載っている。


## [AWS::CDK](https://aws.amazon.com/jp/cdk/)

### 概要

> デベロッパーツール
>
> AWS クラウド開発キット
>
> 使い慣れたプログラミング言語を使用したクラウドアプリケーションリソースの定義
>
> 仕組み
> AWS Cloud Development Kit (CDK) は、一般的なプログラミング言語を使用してアプリケーションをモデル化し、クラウド開発を加速します。

上記の文章だけだとイメージがつかめませんでした。

[開発者ガイドページ - AWS CDK とは何ですか?](https://docs.aws.amazon.com/cdk/v2/guide/home.html)によると、「AWS Cloud Development Kit (AWS CDK) は、 AWS CloudFormationクラウドインフラストラクチャをコードで定義し、それをプロビジョニングするためのオープンソースのソフトウェア開発フレームワークです。」とのこと。

[AWS CloudFormation](https://aws.amazon.com/jp/cloudformation/)はリンク先に以下の説明がありました。

> 管理ツール
> AWS CloudFormation
> Infrastructure as Code でクラウドプロビジョニングを高速化する
> 仕組み
> AWS CloudFormation は、インフラストラクチャをコードとして扱うことで、AWS およびサードパーティーのリソースをモデル化、プロビジョニング、管理することができます。

管理ツールとしてのAWS CloudFormationをAWS CDKでラッパーして開発者でも使いやすくしたのだと理解しました。

AWS CDKの開発者ガイドページに以下の文章と図があったので、引用します。
「AWS CDK は、TypeScript、JavaScript、Python、Java、C#/.Net、Go をサポートしています。これらのサポートされているプログラミング言語のいずれかを使用して、コンストラクトと呼ばれる再利用可能なクラウドコンポーネントを定義できます。これらを組み合わせてスタックとアプリを作成します。次に、CDK アプリケーションを AWS CloudFormation にデプロイして、リソースをプロビジョニングまたは更新します。」

![2024-07-19_aws_cd_app_stack_construct.png]({{site.baseurl}}/assets/2024-07-19_aws_cd_app_stack_construct.png)

[CDKアプリケーション](https://docs.aws.amazon.com/cdk/v2/guide/apps.html)の説明ページに以下の文章と図がありました。
「CDK アプリをデプロイすると、次のフェーズが実行されます。これはアプリライフサイクルと呼ばれます。」

![2024-07-19_aws_cdk_app.png]({{site.baseurl}}/assets/2024-07-19_aws_cdk_app.png)

以上の内容から、おおまかなイメージは理解しました。

### AWS AmplifyでのCDKの使い方コンセプト

[Connecting to AWS beyond Amplify](https://docs.amplify.aws/react/how-amplify-works/concepts/#connecting-to-aws-beyond-amplify)にコンセプトが書いてあります。

「Gen 2 is layered on top of AWS Cloud Development Kit (CDK)—the Data and Auth capabilities in @aws-amplify/backend wrap L3 AWS CDK constructs. As a result, extending the resources generated by Amplify does not require any special configuration. The following example adds Amazon Location Services by adding a file: amplify/custom/maps/resource.ts.」とのことで、resource.tsを追加して記述するとAmazon Location Servicesがアプリに追加できるようです。
つまり、CDKを意識せずにアプリにサービス機能を拡張できるようです。

## 感想

AppSyncとCDKはイメージつかめました。
他のサービスも調査することでシステム全体構成を描けそうです。

## 参考

特になし