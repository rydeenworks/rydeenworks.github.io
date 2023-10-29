---
layout: post
title:  "JekyllによるWebサイト構築(2023年度版)"
date:   2023-10-29
categories: dev
---

# Webサイトを構築しなおす背景

ブログではなくカテゴライズされた資料置き場として整備したくなったので、ウェブサイトを見直したい。[GitHub Pages](https://pages.github.com/)は以前と変わらず[Jekyll](https://jekyllrb.com/)に対応しているので、サイドバーに対応したJekyllのテンプレートを探したところ、[jekyll-libdoc](https://jamstackthemes.dev/theme/jekyll-libdoc/)というテンプレートが良さそうなので、これをベースに資料置き場を構築する。

2019年当時はRubyやJekyllへのモチベーションがあったが、2023年はPCローカルには環境構築せずに全てWebブラウザ上で完結させる方針とする。[jekyll-libdocのGitHub](https://github.com/olivier3lanc/Jekyll-LibDoc#online---no-installation-copy-or-clone)に詳細の手順が紹介されているが、基本的にテンプレートをForkしてオンライのVSCodeで編集してコミットすることでWebページが更新できることがわかった。GitHubのリポジトリのページでピリオドキーを押すだけでVSCodeを使ってオンライン上で編集できる体験はとても感動した。

# Codespacesについて

オンラインのVSCodeで編集する機能はGitHubが提供するCodespacesというサービスによるもの。個人ユーザはベータ版を無料で使えるようだ。

[GitHub codespaces](https://github.co.jp/features/codespaces)

> 個人向けFreeプランのユーザーには、Codespacesベータ版を継続して提供しています。ベータ版の利用に関して変更がある場合は別途お知らせします。

> 個人でCodespacesの使用が可能になる状況についての詳細は、今後お伝えする予定です。現在ベータ版を使用している個人のユーザーは、引き続きCodespacesにアクセスすることができ、料金を請求されることはありません。

# Markdownをプレビューする方法

オンラインのVSCode上でMarkdownファイルを編集した時にプレビューする必要がある。VSCode上でファイルを右クリック>"プレビューを開く"で確認することができる

# 参考

* 2019年に当サイトを構築したときの記録 ![Jekyllによるウェブサイト構築方法]({{site.url}}/2019/01/19/portfolio-website-by-jekyll.markdown)

