---
layout: post
title:  "Androidアプリ 図書さがし の使い方"
date:   2019-08-23
categories: dev
---
私はよく図書館で本を借ります。ネットサーフィンしてて気になる本を見かけたら、Amazonでレビューを見て読むか判断します。PC環境のGoogleChromeブラウザでは、Amazonページで表示中の本が図書館で借りられるか表示するプラグインがあるので便利です。AndroidのWebブラウザで同様の事を実現するのが、**図書さがし** アプリです。



# 使い方

## Amazonページで表示中の本が図書館にあるか調べる

(1)Webブラウザで読みたい本のAmazon書籍ページを表示する

(2)Chromeブラウザの右上のメニューボタンをタップしてメニューを表示する

(3)メニューの「共有...」をタップする

![1_chrome_browser_share.png]({{site.baseurl}}/assets/mybooksearch/1_chrome_browser_share.png)

(4)共有の選択画面が表示されるので、「図書さがし」をタップする

![2_share_mybooksearch.png]({{site.baseurl}}/assets/mybooksearch/2_share_mybooksearch.png)

(5)アプリが起動されて自動で **カーリル** の書籍ページを開く

![3_mybooksearch_search_from_calil.png]({{site.baseurl}}/assets/mybooksearch/3_mybooksearch_search_from_calil.png)

### (注意事項)カーリルの図書館設定

カーリルのページでは探したい図書館を設定してください。最初に一度設定すれば大丈夫です。

![4_calil_setting.png]({{site.baseurl}}/assets/mybooksearch/4_calil_setting.png)



## アプリの履歴から本が図書館にあるか調べる

(1)ホーム画面から「図書さがし」アプリを起動する

(2)履歴一覧から調べたい本のリンクをタップする

![0_book_history.png]({{site.baseurl}}/assets/mybooksearch/0_book_history.png)

(3)Amazonで本の検索結果ページを表示されるので、「Amazonページで表示中の本が図書館にあるか調べる」の方法で調べてください

# 詳細仕様
- Amazonページの解析内容
  - `<title>` `</title>`タグで本のタイトルを取得する
  - `ISBN-13`タグでISBN文字列を取得する
  - 上記の理由によりKindle版の本には対応してない
  - 本のタイトル、ISBNを取得できない場合は"このページは検索できませんでした"と表示する

- Amazonページの解析に成功したら`https://calil.jp/book/` URLに ISBN文字列をつけて外部ブラウザを起動する。
- カーリルが対応してない本は図書館にあるか調べられない
- 本の履歴は100件
- 履歴ページのリンクは、Amazonの検索クエリURLに本のタイトル付与して生成する

# ソースコード
GitHubで公開している。
https://github.com/rydeenworks/MyBookSearch

# 参照
- [カーリルの図書館設定のページ](https://calil.jp/settings)
- [Google Play 図書さがしアプリ](https://play.google.com/store/apps/details?id=com.rydeenworks.mybooksearch)