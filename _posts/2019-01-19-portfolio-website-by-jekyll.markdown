---
layout: post
title:  "Jekyllによるウェブサイト構築方法"
date:   2019-01-19
categories: dev
---

個人開発や技術メモを整理するためウェブサイトを構築する事にした。[GitHub Pages](https://pages.github.com/)を利用して静的サイトジェネレータを使う方針とし、[StaticGen](https://www.staticgen.com/)などで調査して[Jekyll](https://jekyllrb.com/)を使う事にした。
選定理由は以下の通り。

* `Ruby`のエコシステムに習熟したい
* `Jekyll`は利用者数が多くてだいぶ枯れていて情報が多そう
* `GitHub Pages`が`Jekyll`に公式に対応しているので困る事が少なそう

# 参考

ウェブサイト構築にあたっては以下を特に参考にした。

* [Jekyll 公式サイト](https://jekyllrb.com/)
* [Jekyll 公式サイトの日本語訳ページ](https://jekyllrb-ja.github.io/)
* [Jekyll themeをCentrariumに変更する - Memotaro](https://haltaro.github.io/2018/02/11/theme-change)
* [Centrarium のGitHubリポジトリのREADME.md](https://github.com/bencentra/centrarium)

# 環境

* `macOS`
* `Ruby`環境は[HomeBrew](https://brew.sh/index_ja)で[rbenv](https://github.com/rbenv/rbenv)をインストールしてバージョン管理している
* [Bundler](https://bundler.io/)はインストール済み
* [GitHubアカウント](https://github.com/rydeenworks)は取得済みのものを利用
* [github.ioリポジトリ](https://github.com/rydeenworks/rydeenworks.github.io)は作成済みのものを利用

# 手順 - 入門編

入門編では公式サイトのチュートリアル通りの手順で環境構築とウェブサイト生成と動作確認を実施する。本番に向けた練習段階です。

## Jekyllインストールとウェブサイトテンプレート生成

`Jekyll`は`RubyGem`として提供されているので`Bundler`で管理したいため、公式サイトの[Using Jekyll with Bundler](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/)の手順で`Jekyll`インストールを行う。

```console
mkdir my-website
cd my-website
bundle init
bundle add jekyll
bundle exec jekyll new --force --skip-bundle .
bundle install
```

ここまでで`Jekyll`インストールとウェブサイトテンプレートの生成が完了する。[Configure BundlerPermalink](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/#configure-bundler)の章の`./vendor/bundle/`の設定はオプションと書いてあるので実行しなかった。

## ウェブサイト動作確認

```console
bundle exec jekyll serve
```

を実行して`http://127.0.0.1:4000/`にウェブブラウザでアクセスするとウェブサイトが表示された。

# 手順 - 本番

本番では`Jekyll`テーマを利用してウェブサイトを構築する。`Jekyll`テーマとは`Jekyll`で生成したウェブサイトテンプレートをベースにデザインや機能を拡張したものと理解している。

## Jekyllテーマ選定

[Jekyll themeをCentrariumに変更する - Memotaro](https://haltaro.github.io/2018/02/11/theme-change)が素敵なので[Centrarium](https://github.com/bencentra/centrarium)というテーマを採用する。導入の手順も基本的にこのサイトを参考にした。`Centrarium`の`GitHub`リポジトリの[README.md](https://github.com/bencentra/centrarium#centrarium-)に詳細な情報が載っているので、こちらも参考にした。

## Centrariumのダウンロード

`README.md`の[Installation](https://github.com/bencentra/centrarium#installation)に`download this project`と書いてあるのでダウンロードして任意のディレクトリに配置する。

## BundlerでJekyll環境のインストール

ダウンロードしたディレクトリに移動して`Bundler`で`gem`一式をインストールする。

```console
cd centrarium-master
bundle install
```

実行するとエラーが出た。

```console
-> % bundle install
rbenv: version `2.2.2' is not installed
```

`centrarium-master`ディレクトリ直下の`.ruby-version`というファイルに`2.2.2`と記述があるので、実行する`Ruby`バージョンが指定されているようだ。今の`Ruby`バージョンを確認する。

```console
-> % rbenv versions
rbenv: version `2.2.2' is not installed (set by /Users/username/Document/centrarium-master/.ruby-version)
  system
  2.5.1
```

`rbenv`でインストール可能な`Ruby`バージョンを確認する。

```console
rbenv install --list
```

`2.2.2`があったのでインストールする。

```console
rbenv install 2.2.2
```

インストールするとコンソール上に`WARNING: ruby-2.2.2 is past its end of life and is now unsupported.`と表示されたが`Ruby`バージョンでハマると嫌なので気にしない。
`bundle install`を再度実行するとエラー。

```console
-> % bundle install
rbenv: bundle: command not found

The `bundle' command exists in these Ruby versions:
  2.5.1
```

`gem`は`Ruby`環境にインストールされるので、`rbenv`で`2.2.2`をインストールした後は`gem`もインストールし直す必要があった。

```console
gem install bundler
```

成功したので関連する`gem`ライブラリをインストールする。

```console
bundle install
```

今度こそ成功した。次にウェブサイトの動作確認をする。

```console
bundle exec jekyll serve
```

無事に[Centrariumのデモページ](http://bencentra.com/centrarium/)と同じ表示が確認できた。

## カスタマイズ

基本的に[Jekyll themeをCentrariumに変更する - Memotaro](https://haltaro.github.io/2018/02/11/theme-change)を参考にカスタマイズした。

### `_config.yml`の設定変更

`External gems`の`jekyll-archives`をコメントアウトする。`GitHub Pages`ではきちんと動作しないようである。合わせて`Archive settings`と`Category descriptions`のセクションもコメントアウトする。
```yml
# External gems
gems:
  # - jekyll-archives # Sorry, not GitHub pages friendly!

# # Archive settings (see https://github.com/jekyll/jekyll-archives/)
# jekyll-archives:
#   enabled:
#     - categories
#     - tags
#   layout: 'archive'
#   permalinks:
#     category: '/category/:name/'
#     tag: '/tag/:name/'

# Category descriptions (for archive pages)
# descriptions:
#   - cat: dummy
#     desc: "Just some placeholder posts, lorem ipsum and the rest."
```

ウェブサイトの情報に合わせて`Site settings`を変更する。`subtitle`は不要なのでコメントアウトした。`index.html`でしか使ってないので問題ない。また、`URL`にカテゴリを含まない方が良さそうに思うので[パーマリンク](http://jekyllrb-ja.github.io/docs/permalinks/
)の設定を追記した。

```yml
# Site settings
title: RydeenWorks Dev Note
# subtitle: "A simple yet classy theme for your Jekyll website or blog"
email: rydeenworks[at]gmail.com
name: rydeenworks
description: >
  RydeenWorks is my development site.
baseurl: ""
url: "https://rydeenworks.github.io"
cover: "/assets/header_image.jpg"
logo: "/assets/logo.png"
permalink: "/:year/:month/:day/:title"
```

`Build settings`では[paginate](http://jekyllrb-ja.github.io/docs/pagination/)で表示する記事数を5 →10に増やした。また[highlightjs_theme](https://highlightjs.org/static/demo/)を`zenburn`にする。

```yml
# Build settings
paginate: 10
highlightjs_theme: "zenburn"
```

`Social icons and sharing options`は`GitHub`以外は全てコメントアウトした。

```yml
# Social icons and sharing options
social:
  - name: GitHub
    icon: github
    username: rydeenworks
    url: https://github.com/rydeenworks
    desc: Fork me on GitHub
    share: false
```

`Social sharing protocols`の設定は全てコメントアウトした。

### ウェブサイトのロゴ画像

[ICOOON MONOから雷のフリーアイコン](http://icooon-mono.com/11232-%E9%9B%B7%E3%81%AE%E3%83%95%E3%83%AA%E3%83%BC%E3%82%A2%E3%82%A4%E3%82%B3%E3%83%B3/)をダウンロードして`/assets/logo.png`に配置する。`rgb(142,70,169)`がちょうどいい感じ。また[http://www.favicon-generator.org/](http://www.favicon-generator.org/) というサイトを使うとicon一式を生成してくれたので`/assets/icons/`以下に一式配置した。(2MB以上の画像を使ってFaviconを作りたい場合は、こちらのサイトを使うと良い。[https://www.websiteplanet.com/webtools/favicon-generator/](https://www.websiteplanet.com/webtools/favicon-generator/))

### ウェブサイトのカバー画像

[ココ](https://pixabay.com/ja/%E9%9B%B7-%E7%85%A7%E6%98%8E-%E7%A8%B2%E5%A6%BB-%E3%82%AF%E3%83%A9%E3%82%A6%E3%83%89-%E3%83%9C%E3%83%AB%E3%83%88-%E9%9B%B7%E9%9B%A8-%E9%9B%B7%E3%81%AE%E5%B5%90-%E6%9A%B4%E9%A2%A8%E9%9B%A8-%E5%B8%82-1368797/)からダウンロードして`/assets/header_image.jpg`に配置した。

### Projectsページ追加

[フロントマター](http://jekyllrb-ja.github.io/docs/frontmatter/)に以下の記述をした`projects.md`を作成し`index.html`と同じ階層に配置する。すると、ウェブサイトのトップメニューに`Project`という項目が表示される。リンクをクリックするとページが表示される。

```html
---
layout: post
title: Projects
permalink: /projects/
public: true
---
```

### Aboutページの修正

以前`https://rydeenworks.github.io`で公開していた内容をこちらに転記した。またプロフィール画像として猫画像を置いた。

### Typographyページの非表示

`typography.html`の[フロントマター](http://jekyllrb-ja.github.io/docs/frontmatter/)に`published: false`を追記すると表示されない。

### _layouts/post.htmlを変更

著者名表示は不要なのでコメントアウトする。SNS共有も不要なのでコメントアウトする。[参考サイト](https://haltaro.github.io/2018/02/11/theme-change)参照。

### フォントサイズの微調整

`_sass/_layout.scss`と`_sass/base/_typography.scss`を調整した。
[参考サイト](https://haltaro.github.io/2018/02/11/theme-change)参照。

### index.htmlのサマリ表示を変更

「日本語で記事を書くと，index.htmlのサマリ部分に全文表示されてしまう．おそらく`<ul class="post-list">`部分の`truncatewords: 50`が英語以外で動作しないせいだと考えられる．」と[参考サイト](https://haltaro.github.io/2018/02/11/theme-change)にあったので、同様の対策を行う。

## GitHubへアップロードする

`git push`してから`https://rydeenworks.github.io/`へアクセスすると、無事ウェブサイトが表示された。

## GitHubのSecurity Alert対応

`GitHub`のリポジトリのページで`jekyllとffiのバージョンが古い`という`Security Alert`が表示された。`GemFile.lock`をみて指摘してくれているのではないかと思う。`Bundler`で`gem`を管理しているのでアップデートする。

```console
bundle update
```

アップデート後に`bundle exec jekyll serve`でローカルで動作確認すると以下の警告が出た。

```console
Configuration file: /Users/username/Documents/centrarium-master/_config.yml
Deprecation: The 'gems' configuration option has been renamed to 'plugins'. Please update your config file accordingly.
```

`_config.yml`の`gems`を`plugins`にリネームして、再び動作確認すると警告が消えた。

```yml
# External gems
plugins:
  # - jekyll-archives # Sorry, not GitHub pages friendly!
```

# 感想

`Ruby`や`Bundler`はだいぶ慣れていたのと、ネットに情報が多かったので特に困らずに環境構築ができたのは狙い通りだった。今後は記事をスラスラと書けるようになりたい。