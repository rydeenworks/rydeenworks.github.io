---
layout: post
title:  "AWS-Amplifyのクイックスタート続き(認証周り実装見直し)"
date:   2024-07-15
categories: dev
---

# AWS-Amplifyのクイックスタートで残った課題

## 問題の事象
- Sign in した直後に表示されるTODOタスクが、前回ログインしていたユーザのものになる
- 再現率100%

## 問題の回避策
- Webページをリロードすると当該ユーザのTODOタスクが表示される

## 課題

- クイックスタートのソースコードが正しくて、自身の実装がクイックスタート通りに実装できてないのか確認する
  - 確認した結果クイックスタート通りに実装できていた
  - つまりクイックスタートのソースコードはユーザごとにデータを保持する機能仕様に対応できてない模様
- クイックスタートの実装内容を見直して修正する
- アプリが利用しているライブラリやフレームワークの機能仕様・機能設計の理解があいまいで何が問題なのか特定できてないのが課題
  - useEffect処理(subscribeとsetTodos)について内容を理解する
  - Authenticator処理について内容を理解する

## ライブラリ・フレームワークの調査
- React
  - userEffect
    - [useEffectのAPIリファレンス](https://react.dev/reference/react/useEffect)
    - 「コンポーネントが DOM に追加されると、React はセットアップ関数を実行します。」とのこと
    - クリーンアップ関数が未実装だったので、unsubscribeする関数を返すようにする
    - console.log()を仕込んで実際の挙動を確認したところ、１度Webページを更新するとセットアップ→クリーンアップ→セットアップと呼び出されていることがわかった
    - React18でStrictModeの場合は意図的に二重にコンポーネントをレンダリングしているからセットアップが２回呼ばれるらしい
  - useState
    - todoデータを状態として保持する役割
    - 初期値は空っぽの配列
    - setTodos関数でデータを更新する
    - データを更新すると再レンダリングする
    - subscribeでTodoデータの更新を検知するとsetTodos関数を実行する設計
- Amplify
  - [Amplify Data](https://docs.amplify.aws/react/build-a-backend/data/)
    - 「TypeScript を使用してデータモデルを定義すると、Amplify がリアルタイム API をデプロイします。この API は AWS AppSync によって実行され、Amazon DynamoDB データベースに接続されます。」とのこと。
    - [AWS AppSyncページ](https://aws.amazon.com/jp/appsync/)を見ると、「GraphQL と Pub/Sub API を使用して、アプリをデータやイベントに接続」とのこと
    - [Amazon DynamoDB](https://aws.amazon.com/jp/dynamodb/)は「サーバーレス NoSQL フルマネージドデータベース」とのこと
    - Amplify Data 公式Docの[Subscribe to real-time updates](https://docs.amplify.aws/react/build-a-backend/data/set-up-data/#subscribe-to-real-time-updates) ではuseEffectでsubscribe/unsubscribeするソースコード例が載っていた
    - バックエンドからTodoタスクを読み出すソースコード例も公式Docにあった -> [Read data from your backend](https://docs.amplify.aws/react/build-a-backend/data/set-up-data/#read-data-from-your-backend)
    - ユーザごとにTodoタスクを保持するデータ設計なので、ユーザがサインインに成功したら該当ユーザのTodoタスクを表示する機能仕様になるはず
    - Todoタスクを読み出す実装を追加する必要がありそう
  - Authentication
    - [Amplify Auth 公式Doc](https://docs.amplify.aws/react/build-a-backend/auth/)
    - 「Amplify Auth は[Amazon Cognito](https://aws.amazon.com/jp/cognito/)を利用しています。」とのことなので認証機能の詳細はCognitoを理解するのが良さそう
    - Amplify Dev Center > UILibrary > Authenticator > [Advanced Usega](https://ui.docs.amplify.aws/react/connected-components/authenticator/advanced) にuseAuthenticator Hookというのがある
    - 今回の課題は認証時の実装作法についてなのでuseAuthenticatorを理解すれば良さそう

# クイックスタートの実装内容の調査
- todoデータはsubscribe時にしか更新されないのが課題なので、ユーザ認証されたタイミングでsetTodosする設計に見直す
- useAuthenticatorに以下のログを仕込んでroute/authStatus/usernameの認証時の値の振る舞いを明らかにした
``` javascript
  const { user, signOut } = useAuthenticator(
    (context) => {
      console.log("useAuthenticator onChanged. route=" + context.route + " authStatus=" + context.authStatus + " user:" + context.username);
      return [context.user];
    }
  );
```
- useAuthenticatorを調査した結果、userが有効な値の時にTodoタスクを読み出す設計にした
- useEffectのdependenciesとしてuserを設定し、user更新時にuseEffect時の処理を実行する設計とした
- useEffectのクリーンアップ関数でunsubscribeした
- useEffectのクリーンアップ関数でTodoタスクを空配列にした
  - 空配列にしないと別のユーザのTodoタスクが一瞬表示されたため
  - unsubscribeするということはデータ更新しないということなので、空配列にする設計は妥当だと思う
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

## 結果

- 課題は無事解決できた
- ライブラリやフレームワークの理解が深まった
- 3日間くらいログやDocで調査しつつフレームワークの動作モデルを正しく理解するのに費やした

## 感想

- AWS Amplifyでシステム構築した上で理解を深めるという作戦は狙い通りにうまく行った
- 引き続きアプリ機能を拡張しつつ理解を深めたい

## 参考
- [GitHub > rydeenworks > amplify-vite-react-template](https://github.com/rydeenworks/amplify-vite-react-template)
- [AWS Amplify > Build & connect backend](https://docs.amplify.aws/react/build-a-backend/)
- [AWS Amplify Quick Start for React](https://docs.amplify.aws/react/start/quickstart/)
- [useAuthenticatorフック](https://ui.docs.amplify.aws/react/connected-components/authenticator/advanced)
