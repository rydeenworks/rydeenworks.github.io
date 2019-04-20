---
layout: post
title: Projects
permalink: /projects/
public: true
---

# 1.図書館ほんだな

- 図書館に読みたい本があるかスマホから簡単に検索したい
- 読みたい本や既読の本を一覧したい

上記の動機で開発した。
既存のサービス([カーリル](https://calil.jp/)、図書館Webサイト、いくつかのスマホアプリ）を試したがしっくり来なかったため自分で作る事にした。
いくつかの技術のキャッチアップもできた。

## アプリケーション機能([GooglePlay](https://play.google.com/store/apps/details?id=com.rydeenworks.mybookreading))

1. Amazonサービスを利用して本を検索できる
1. 図書館で借りられるか表示する
1. 図書館に蔵書がある場合、貸出予約Webページを表示できる
1. Amazon商品Webページから本の評判を確認できる
1. 図書館は最大５件まで登録できる
1. ほんだなにたくさんの本を登録できる

## 利用技術

- VisualStudio/C#/Xamarin[^1]
- Android SDK
- WebAPI([Amazon-PAAPI](https://affiliate.amazon.co.jp/assoc_credentials/home)/[カーリル図書館API](https://calil.jp/doc/api.html))
- NoSQL([Realm Database](https://realm.io/jp/products/realm-database/))[^2]

[^1]: 過去にWindowsアプリを開発した経験があったが、.NET Framework/LINQ/XAML/C#の技術登場以降キャッチアップしてなかったので採用した。AndroidアプリとiPhoneアプリを同時に開発できる事に魅力を感じたが、結局ネイティブ部分は書き分ける必要があってAndroidのみ対応した。

[^2]: 基礎的なRDB/SQLの経験はあったがデータベースについて技術的なキャッチアップをしたかったのでNoSQLを採用した。

# 2.図書さがし

Amazonで書籍ページを閲覧している時に、その書籍が図書館にあるのか確認したいと`図書館ほんだな`を開発して思ったので開発した。

## アプリケーション機能([GooglePlay](https://play.google.com/store/apps/details?id=com.rydeenworks.mybooksearch))

- 上の画面でネットサーフィンすると下の画面で図書館で借りられるか表示する
- Android標準Chromeブラウザの共有機能で連携する事で図書館で借りられるか簡単に確認できる

## 利用技術

技術的に特筆することは無し。
書籍「[リーン・スタートアップ](https://www.amazon.co.jp/%E3%83%AA%E3%83%BC%E3%83%B3%E3%83%BB%E3%82%B9%E3%82%BF%E3%83%BC%E3%83%88%E3%82%A2%E3%83%83%E3%83%97-%E3%82%A8%E3%83%AA%E3%83%83%E3%82%AF%E3%83%BB%E3%83%AA%E3%83%BC%E3%82%B9/dp/4822248976/)」の影響を受けてまずは必要最低限の機能を実装して、それが目的を達成するアプリなのかユーザビリティ観点に着目して開発した。

---
