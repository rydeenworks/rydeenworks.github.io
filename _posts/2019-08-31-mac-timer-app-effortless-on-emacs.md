---
layout: post
title:  "Mac Effortless App on Emacs"
date:   2019-08-31
categories: orgmode
---
仕事にプライベートに毎日Emacsのorgmodeを愛用していて、だんだんとパワフルな環境になってきました。先日、[Rebuild.fm](https://rebuild.fm/) を聞いていて [Effortless](https://www.effortless.app/) というポモドーロテクニック的なタイマーアプリが紹介されて調べてみたのですが、これは・・・Emacs なら自分で作れそうだと思いました。そしてこのタイマーは私のorgmodeシステムのplan.orgにピッタリだと思いました。

# 機能仕様案

## タイマースタート

矢印 `->` を書いたらスタートする。タスク名とタイマーをmode line部に表示しカウントダウンする。

![plan-task-timer-start]({{site.baseurl}}/assets/plan-task-timer-start.png)



## タイマーストップ

時間が経過したらストップする。またはチェックをつけたらストップする。矢印の右側には個人的に実績値を書けるようにしたい。

![plan-task-timer-stop]({{site.baseurl}}/assets/plan-task-timer-stop.png)



# 車輪の再発明はしない

上記のような内容なら既にありそうな気がしました。ネットで検索しましたがズバリそのものは見つかりませんでした。無いならEmacs Lispを覚えながら作ってみたいです。GitHubで見つけた [chronos](https://github.com/dxknight/chronos) は近そうに思いました。`ReadMe.md`を 読むとやはりタイマーアプリはたくさん存在するようです。

> There are a number of Emacs packages that provide timer functionality, such as job tracking, alarms or a countdown timer in the mode line. 

ただ、`chronos` 作者は自分が欲しいものとは違ったため作ったそうです。私も無いなら作ってみようと思いました。

