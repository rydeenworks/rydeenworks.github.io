---
layout: post
title:  "EmacsとorgmodeによるGTD実例【ビジネススキル】"
date:   2019-11-23
categories: orgmode
---

**Emacsでorgmodeを使いこなしたい人**

Emacsでorgmodeを使ってタスク管理しているんだけど、なんか使いこなせない。
あと、なんか便利なテンプレートや設定があれば知りたい。と考えていませんか？



本記事では、この疑問を解決します。

**本記事の内容**

- Emacsでorgmodeを使ってGTDする方法がわかる

- タスク管理と週次レビューはセットで実行すべき



![office-taking-note.jpg]({{site.baseurl}}/assets/office-taking-note.jpg)



**著者について**

この記事を書いている私はGTD歴10年、Emacsとorgmode歴が3年ほどです。仕事で毎日orgmodeを使ってタスク管理と振り返りを継続してます。







# 1 orgmodeを使ったGTDシステムの構築方法

## 1.1 org-capture-templatesを設定する

orgmodeを使ってGTDするためにはorg-capture-templatesの設定を行います。

以下の理由があります。

* キーボードショートカットでGTDの操作を身体で覚えられてストレスなく作業できる
* 記述内容のテンプレートが自動で挿入されて高速に作業できる

Emacsでのorgmodeの環境構築は過去記事を参考にしてください。記事の中でorg-capture-templatesの設定も説明しています。

[私生活向けorgmodeによるGTDの使い方](https://rydeenworks.github.io/2019/06/30/how-to-use-orgmode)



org-capture-templatesの設定内容を以下に抜粋しました。

``` lisp
  (setq org-capture-templates
        '(("t" "Todo entry" entry (file "~/Dropbox/org-for-cat/private/todo.org")
           "* TODO %?\n    :LOGBOOK:\n    - Added: %U\n    :END:" :empty-lines 1)
          ("p" "Plan entry" entry (file+datetree "~/Dropbox/org-for-cat/private/plan.org")
           "- [ ] %?")
          ("j" "Journal entry" entry (file+datetree "~/Dropbox/org-for-cat/private/journal.org")
           "* 週次レビュー\n- good:%?\n- bad:\n- try:\n")
          ("r" "Review entry" entry (file+datetree "~/Dropbox/org-for-cat/private/review.org") (file "~/Dropbox/org-for-cat/private/template-review.org"))
          )
        )

```

今回は`"p"(plan.org)` と `"j"(journal.org)`を使います。

 `"t"(todo.org)` と`"r"(review.org)` は使用しません。



## 1.2 毎日のタスク管理にplan.orgを使用する

毎日のタスク管理をするためにplan.orgだけを使います。
また、チェックボックス形式のリスト行で完了/未完了の状態だけを管理します。

以下の理由があります。

* 完了/未完了の管理だけでGTDでは十分
* plan.orgにタスクを集約すると決めた方が迷いなく高速にタスク処理できる
* 仕事の優先度は日々変わるためplan.orgで一覧した方が優先順位をつけやすい



それではplan.orgの使い方を説明します。

### 1.2.1 plan.orgを開く

初期状態が次の画面だとします。

![plan-org-first.png]({{site.baseurl}}/assets/plan-org-first.png)


### 1.2.2 org-captureを実行して今日の日付を追加する

キー操作 `C-c c` でorg-captureを実行します。
org-capture-templatesで設定したテンプレート設定が表示されます。
この画面で `p` を押します。

![org-capture-template]({{site.baseurl}}/assets/org-capture-template.png)

この画面では、`C-c C-c`を押して、plan.orgへの記述を確定します。
![capture-plan-orgmode.png]({{site.baseurl}}/assets/capture-plan-orgmode.png)

以上で、plan.orgに今日の日付が追加されました。
![org-capture-plan-finish.png]({{site.baseurl}}/assets/org-capture-plan-finish.png)

### 1.2.3 昨日の未完了タスクを今日の日付に移動する、そしてタスクの整理をする

タスク整理は以下のことを行います。
整理することで今日すべきことが明確になって集中力がアップします。

* 不要なタスクの削除
* 新規タスクの追加
* 既存タスクの内容の見直し
* タスク優先順位の見直し

以下の状態になりました。あとは今日すべきことをするだけです。

![plan-sort-today.png]({{site.baseurl}}/assets/plan-sort-today.png)



## 1.3 今週分のjournal.orgを用意する

週の始まりごとにjournal.orgにエントリーを追加しましょう。
そして日々のタスクを行う中で気づいた事をjournal.orgに記入していきましょう。

* 良かった事(good)
* 悪かった事(bad)
* 改善点(try)

なぜなら、単にタスクをこなすだけでは物事が改善しないからです。
タスクをこなす事で自身の気づきがあると思いますが、その気づきをjournal.orgに記録し振り返る事で改善につながるのです。


### 1.3.1 org-captureを実行して今週のエントリーを追加する

キー操作 `C-c c` でorg-captureを実行します。
org-capture-templatesで設定したテンプレート設定が表示されます。
この画面で `j` を押します。

![org-capture-template]({{site.baseurl}}/assets/org-capture-template.png)

この画面では、`C-c C-c`を押して、journal.orgへの記述を確定します。

![org-capture-journal.png]({{site.baseurl}}/assets/org-capture-journal.png)

### 1.3.2 journal.orgに自身の気づきを記入する

まずは気軽に自分の思ったことや気づいた事を書いてみましょう。
この記録は自分の行動を振り返ってみるときに役に立ちます。

![journal-entry.png]({{site.baseurl}}/assets/journal-entry.png)



# 2 タスク管理と合わせて週次レビューをすべき

タスク管理をするときには週次レビュー（一週間おきに振り返り）をセットで行うべきです。

## 2.1 週次レビューをしましょう

以下の理由があります。
* タスクを処理するだけでは単なるタスクマシーンになる恐れがある
* 自分の目標達成に向かって行動しているか確認するのが大事である
* 目標達成に向かってない場合の方向修正の機会になる
* タスク処理の効率性や効果改善につながる

自分の行動を客観的に見てみると、改善ポイントが見えてくるのです。



## 2.2 週次レビューのやり方

(1) 左画面にplan.org、右画面にjournal.orgを表示する
(2) plan.orgに今週完了したタスクを表示させる
(3) 完了タスクを眺めながら思ったこと気づいたことをjournal.orgに記入する

![weekly-review.png]({{site.baseurl}}/assets/weekly-review.png)

# 記事のポイント

ポイントを以下にまとめます。

* plan.orgで日々のタスクを管理する
* journal.orgで日々のタスクの気づきを記入する
* 一週間に一度はplan.orgとjournal.orgを見返して振り返りを行なう

こんな感じです。
orgmodeの操作を身体に覚えさせて、GTDと週次レビューのサイクルを回せるようになると圧倒的に成果が出るようになります。ぜひ試してください。


# オススメの本


GTDについて詳しく知りたい方は書籍がオススメです。

<div class="kattene">
    <div class="kattene__imgpart"><a target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/4576151878/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4576151878&linkCode=as2&tag=dynamitecruis-22&linkId=d3f73b1ede75906ca1b29dd0fd9f37ab"><img src="https://ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4576151878&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=dynamitecruis-22"></a></div>
    <div class="kattene__infopart">
      <div class="kattene__title"><a target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/4576151878/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4576151878&linkCode=as2&tag=dynamitecruis-22&linkId=d3f73b1ede75906ca1b29dd0fd9f37ab">全面改訂版 はじめてのGTD ストレスフリーの整理術</a></div>
      <div class="kattene__description">最強の仕事術=GTDのバイブルが時代に合わせてアップグレード!ゆるぎない仕事の基本原則がここにある。「本書を読めば、マルチタスクと情報過多の時代に必要とされる精神的なスキルを身につけることができる」――ウォール・ストリート・ジャーナル</div>
      <div class="kattene__btns __five">
        <div><a class="kattene__btn __orange" target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/4576151878/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4576151878&linkCode=as2&tag=dynamitecruis-22&linkId=d3f73b1ede75906ca1b29dd0fd9f37ab">Amazon</a></div>
      </div>
    </div>
</div>



こちらはチェックリストの効果について学べる本です。
チェックリストはシンプルですがとても強力です、私はこの本を読んで大変役に立っています。


<div class="kattene">
    <div class="kattene__imgpart"><a target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/4863912803/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4863912803&linkCode=as2&tag=dynamitecruis-22&linkId=19cc78bc2807d124f88288a2b7bbd386"><img src="https://ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=JP&ASIN=4863912803&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL250_&tag=dynamitecruis-22"></a></div>
    <div class="kattene__infopart">
      <div class="kattene__title"><a target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/4863912803/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4863912803&linkCode=as2&tag=dynamitecruis-22&linkId=19cc78bc2807d124f88288a2b7bbd386">アナタはなぜチェックリストを使わないのか？【ミスを最大限に減らしベストの決断力を持つ！】</a></div>
      <div class="kattene__description">単純な「チェックリスト」が日常に起きるミスを減らし、災害・事故に際しては人命を救う。絶対にミスの許されない医療現場で著者が辿り着いた真実。経営者、投資家、医師、パイロット、建築家、料理人…、あらゆるプロフェッショナルが信じる成功のエッセンスがここにある。米誌「TIME」の「世界で最も影響力ある100人」に選ばれた著者の提言。</div>
      <div class="kattene__btns __five">
        <div><a class="kattene__btn __orange" target="_blank" rel="noopener" href="https://www.amazon.co.jp/gp/product/4863912803/ref=as_li_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4863912803&linkCode=as2&tag=dynamitecruis-22&linkId=19cc78bc2807d124f88288a2b7bbd386">Amazon</a></div>
      </div>
    </div>
</div>



# 図書館の予約を便利にするアプリの紹介

私は図書館をよく利用するのですが、上記の本は図書館から借りました。本が図書館にあるかAndroidアプリ [図書さがし(Google Play)](https://play.google.com/store/apps/details?id=com.rydeenworks.mybooksearch)で簡単に調べることができて便利です。

![goole-play-mybooksearch]({{site.baseurl}}/assets/goole-play-mybooksearch.png)
