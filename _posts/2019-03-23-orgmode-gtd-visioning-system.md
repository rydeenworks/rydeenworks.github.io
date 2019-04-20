---
layout: post
title:  "orgmodeとGTDによるVisioningシステム"
date:   2019-03-23
categories: orgmode
---

## システム構成

![orgmode-system]({{site.baseurl}}/assets/orgmode-system.jpg)

### 説明

- 紙のメモ帳(memopad)を持ち歩いて思いついた事をすぐ書きとめます
- OrgzlyはDropBox上のorgファイルと同期するアプリです(Androidではorgmodeの閲覧だけです)
- ブログ記事→Jekyllの_postsフォルダ、orgmode→orgフォルダ
- Macの方がストレスがないと思いますが、WindowsでもOK

## orgmodeファイル構成

![org-directory]({{site.baseurl}}/assets/org-directory.png)

### メイン

| ファイル名    | 内容                                                         |
| ------------- | ------------------------------------------------------------ |
| goal.org      | GTDにおける**望んでいる結果**。将来の夢やビジョンなど実現したい事を書く。 |
| todo.org      | GTDにおける**次の具体的行動**。TODO/MAYBE/WAIT/PROJは全部ここに入れる。 |
| logbook.org   | アイデアや感情などを記録する。私は紙のメモ帳を使うのでほとんど使わない。 |
| plan.org      | 日単位の記録。私はほとんど使わない。使い方は検討中。         |
| journal.org   | 週単位の記録、および週次レビューの振り返りを記録する。       |
| review.org    | 週次レビューチェックリスト。                                 |
| proj_xxxx.org | GTDにおけるプロジェクト。プロジェクト単位にファイルを作る。  |
| doc_xxxx.org  | GTDにおける資料。ファイルの分け方は任意。                    |

### Emacs設定関連

| ファイル名          | 内容                                                         |
| ------------------- | ------------------------------------------------------------ |
| org-global.el       | orgmodeの設定                                                |
| template-review.org | 週次レビューチェックリストのテンプレート                     |
| todo.org_archive    | 完了したタスクをアーカイブするファイル。Emacsが自動的に作る。 |

## 使い方

内容整理中。

## 感謝

- [https://orgmode.org](https://orgmode.org)

  Emacsとorgmodeはとても素晴らしいツールです。

- [Orgmode E07S02: Presenting my system](https://www.youtube.com/watch?v=-2RXhPV_zgc)a

  この動画に出会わなければ本システムは構築できなかったと思います。

- [The power of orgmode capture templates](https://koenig-haunstetten.de/2014/08/29/the-power-of-orgmode-capture-templates/)

  動画作者の投稿記事。org-captureを強化するための参考になりました。


- [http://spacemacs.org/](http://spacemacs.org/)

  spacemacsはEmacsのコマンド名が出てくるので愛用しています。

- [https://gettingthingsdone.com/](https://gettingthingsdone.com/)

  [Weekly Reviewのページ](https://gettingthingsdone.com/2018/08/episode-43-the-power-of-the-gtd-weekly-review/)と[Five Stepsのページ](https://gettingthingsdone.com/five-steps/)を参考にしました。<a target="_blank" href="https://www.amazon.co.jp/%E5%85%A8%E9%9D%A2%E6%94%B9%E8%A8%82%E7%89%88-%E3%81%AF%E3%81%98%E3%82%81%E3%81%A6%E3%81%AEGTD-%E3%82%B9%E3%83%88%E3%83%AC%E3%82%B9%E3%83%95%E3%83%AA%E3%83%BC%E3%81%AE%E6%95%B4%E7%90%86%E8%A1%93-%E3%83%87%E3%83%93%E3%83%83%E3%83%89%E3%83%BB%E3%82%A2%E3%83%AC%E3%83%B3/dp/4576151878?&_encoding=UTF8&tag=dynamitecruis-22&linkCode=ur2&linkId=9327cd4b2c7d8ad114597dbdb499647c&camp=247&creative=1211">GTDの本</a><img src="//ir-jp.amazon-adsystem.com/e/ir?t=dynamitecruis-22&l=ur2&o=9" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" /> は全面改訂版で再読しました。

- [https://typora.io/](https://typora.io/)

  Typoraは最近出会いましたが素晴らしいです。

