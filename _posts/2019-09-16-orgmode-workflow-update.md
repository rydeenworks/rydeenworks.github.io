---
layout: post
title:  "最近のorgmodeの使い方"
date:   2019-09-16
categories: orgmode
---
私はSpacemacsでorg-modeを愛用しています。平日は会社、週末は自宅というように毎日使っています。Emacs使用歴は2-3年と浅いので知らないことが多いです。最近知ったEmacsとorg-modeのTipsをまとめます。

# Tips

## アウトラインにIDをつける

このTipsとコードは[Rainer氏のブログ](https://koenig-haunstetten.de/2018/02/17/improving-my-orgmode-workflow/) と[動画](https://www.youtube.com/watch?v=be8TC-i-NpE)を見つけて取り込みました。

``` lisp
(defun my/copy-idlink-to-clipboard() 
  "Copy an ID link with the headline to killring, if no ID is there then create a new unique ID.  This function works only in org-mode or org-agenda buffers.  The purpose of this function is to easily construct id:-links to org-mode items. If its assigned to a key it saves you marking the text and copying to the killring."
       (interactive)
       (when (eq major-mode 'org-agenda-mode) ;switch to orgmode
         (org-agenda-show)
         (org-agenda-goto))       
       (when (eq major-mode 'org-mode) ; do this only in org-mode buffers
         (setq mytmphead (nth 4 (org-heading-components)))
         (setq mytmpid (funcall 'org-id-get-create))
         (setq mytmplink (format "[[id:%s][%s]]" mytmpid mytmphead))
         (kill-new mytmplink)
         (message "Copied %s to killring (clipboard)" mytmplink)
         ))
```

私はこのコードを`org-global.el`に入れて使ってます([6/30の記事参照](https://rydeenworks.github.io/2019/06/30/how-to-use-orgmode))。Rainer氏はF5キーを割り当ててますが、私はキー割り当て無しで試用中です。



使い方は、IDをつけたいアウトラインにカーソルを当ててから `my/copy-idlink-to-clipboard`関数を実行します。

![copy-idlink-to-clipboard_1.png]({{site.baseurl}}/assets/copy-idlink-to-clipboard_1.png)

実行するとプロパティとしてIDが設定されます。それと同時にkillringにリンク文字列が格納されます。

![copy-idlink-to-clipboard_2.png]({{site.baseurl}}/assets/copy-idlink-to-clipboard_2.png)

リンク文字列をyankすると、TODOへのリンクが貼れました。

![copy-idlink-to-clipboard_3.png]({{site.baseurl}}/assets/copy-idlink-to-clipboard_3.png)



目標管理である`goal.org` `todo.org` `proj_xxxx.org`と時系列管理である`plan.org` `journal.org` を関連づけてorgmodeを運用したいと思っていたところだったので、とても良いTipsに出会えたと思います。



## モードライン部の表示On/Off

[Spacemacsのドキュメント](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#mode-line)に表示制御について記載がありました。

- バッテリー充電状態
- org-clockのタスク名
- 時刻

を表示するようにしました。

![orgmode-modeline-display.png]({{site.baseurl}}/assets/orgmode-modeline-display.png)

`org-deadline` `org-schedule` `org-set-effort` `org-pomodoro` は以前から知ってましたが、やりすぎると面倒なので使いどころを探っていきたいです。



# 参照
- [orgmodeの記事(2019/06/30)](https://rydeenworks.github.io/2019/06/30/how-to-use-orgmode)
- 私が勝手にorgmodeの師匠と思っている [Rainer氏のブログ](https://koenig-haunstetten.de/2018/02/17/improving-my-orgmode-workflow/) と[動画](https://www.youtube.com/watch?v=be8TC-i-NpE)
