---
layout: post
title:  "GitHub issueによる個人開発プログラミングの高速化"
date:   2019-12-30
categories: dev
---

# 個人開発のスピードを上げるためにすべき事

**個人開発していて開発スピードが上がらないことはありませんか？**

開発したい内容をタスクとして整理したり、タスク粒度を適度に小さくする事で開発スピードを上げられる場合があります。

前提条件
- プログラミング経験はある
- 技術的な事はネットを検索して自分で解決できる




本記事では、この疑問を解決します。

**本記事の内容**

- 開発内容をタスクとして整理する方法がわかる
- GitHub issueを使った開発ワークフローがわかる

![github-octocat]({{site.baseurl}}/assets/github-octocat.jpg)
photo credit: ben_nuttall <a href="http://www.flickr.com/photos/101462707@N03/26056639835">Octocat @ GitHub's Oval Office</a> via <a href="http://photopin.com">photopin</a> <a href="https://creativecommons.org/licenses/by-sa/2.0/">(license)</a>



**著者について**

この記事を書いている私はプログラミング歴15年です。
個人開発歴は3年で、会社員をしながら２つのアプリをGooglePlayにリリースした実績があります。





![office-taking-note.jpg]({{site.baseurl}}/assets/office-taking-note.jpg)


# 1 GitHub issueを使った開発タスク整理

## 1.1 開発タスクを箇条書きで書き出す

まず最初にGitHub issueに登録するために、開発タスクを箇条書きで書き出します。

以下の理由があります。

* 頭の中にある開発内容を書き出すことで整理できる
* 開発タスクを並べることで優先順位をつけられる
* 開発の全体ボリュームがなんとなくわかる

紙に書き出しても良いですし、PCにテキストで書いても良いです。

## 1.2 開発タスクの粒度を半日程度の規模に分割する

個人開発は時間との勝負です。
そして開発することが目的ではなく、リリースして初めて意味があります。
そのためにも開発タスクの粒度は半日程度にしてください。

以下の理由があります。
- 開発に着手するときのハードルが低い
- タスクが小さいので開発の中断と再開がしやすい
- タスクをcloseするまでの時間が短くて達成感を得やすい

## 1.3 開発タスクをGitHub issueに登録する


私が個人開発している「図書さがし」を例に issue を登録します。

[https://github.com/rydeenworks/MyBookSearch/issues](https://github.com/rydeenworks/MyBookSearch/issues)

**初期状態**

![github-issue]({{site.baseurl}}/assets/github-issue.png)

`[New issue]`ボタンを押します。

issue作成画面が表示されるので、issueのタイトルを記入します。
詳細な情報はコメント欄に記入できます。
記入が終わったら`[Submit new issue]`ボタンを押します。

![github-issue-new]({{site.baseurl}}/assets/github-issue-new.png)

ボタンを押すと issue が登録されました。

**issue 登録後**

![github-issues-added]({{site.baseurl}}/assets/github-issues-added.png)


## 1.4 issueに優先順位をつける

**その機能は本当に必要ですか？**

個人開発は時間との勝負です。

- あなたが開発に投入可能な時間
- issueの開発に必要な時間

上記の２つの時間のバランスを考えて、リリースに最低限必要な機能を選んで開発しましょう。




![octocat]({{site.baseurl}}/assets/octcat.png)



# まとめ：開発スピードアップのためにはGitHub issueでタスク化！

記事のポイントを以下にまとめます。

* 開発内容をGitHub issueでタスク化する
* タスクは半日程度で終わる粒度にする
* リリースに必要なタスクを優先度決めて片付ける

こんな感じです。


<a href="https://px.a8.net/svt/ejp?a8mat=35UQJU+AZXA2A+4B5K+5Z6WX" rel="nofollow">
<img border="0" width="468" height="60" alt="" src="https://www23.a8.net/svt/bgt?aid=191230698665&wid=001&eno=01&mid=s00000020108001004000&mc=1"></a>
<img border="0" width="1" height="1" src="https://www16.a8.net/0.gif?a8mat=35UQJU+AZXA2A+4B5K+5Z6WX" alt="">






# 参考

<div class="kattene">
    <div class="kattene__imgpart"><a target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/477416366X/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=477416366X&linkCode=as2&tag=dynamitecruis-22&linkId=0a59c69f70038c34694fbc085c51dd2f"><img src="https://ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=477416366X&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=dynamitecruis-22"></a></div>
    <div class="kattene__infopart">
      <div class="kattene__title"><a target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/477416366X/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=477416366X&linkCode=as2&tag=dynamitecruis-22&linkId=0a59c69f70038c34694fbc085c51dd2f">GitHub実践入門 ~Pull Requestによる開発の変革 (WEB+DB PRESS plus)</a></div>
      <div class="kattene__description">GitHubの実践的な使い方を、実際に手を動かす形で解説する書籍です。初学者の方にもわかりやすいよう、基本的なGitやGitHubの使い方から、「ソーシャルコーディング」の目玉機能であるPull Requestの送り方・受け方まで解説します。また、外部ツールとの連携、GitHub FlowやGit Flowなど、GitHubを中心とした開発手法についてもしっかり解説しているので、中・上級者の方にも参考になるはずです。</div>
      <div class="kattene__btns __five">
        <div><a class="kattene__btn __orange" target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/477416366X/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=477416366X&linkCode=as2&tag=dynamitecruis-22&linkId=0a59c69f70038c34694fbc085c51dd2f">Amazon</a></div>
      </div>
    </div>
</div>

- [未経験がWeb系転職成功したいならgithubでissue管理して開発しよう(Qiita)](https://qiita.com/fukubaka0825/items/c7710b4e87d478c8ba3b)

