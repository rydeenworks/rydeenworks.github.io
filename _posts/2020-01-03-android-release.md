---
layout: post
title:  "AndroidアプリをGooglePlayストアに公開する手順[APK版]"
date:   2020-01-03
categories: dev
---

AndroidアプリをGooglePlayストアに公開するまでの手順についてまとめました。大まかな流れは以下の通りです。

* アプリのバージョンを上げる
* AndroidStudioでリリース向けのapkを作成をする
* GooglePlayConsoleで新しいリリースを作成する

私が個人開発したAndroid向けアプリ「図書さがし」を例に手順を説明します。
<a href='https://play.google.com/store/apps/details?id=com.rydeenworks.mybooksearch&pcampaignid=pcampaignidMKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1'><img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png'/></a>

**(注意事項)** GoogleではBundle版でのリリースを推奨しているようですが、本記事ではAPKによるリリースの手順となっています。


**(著者について)** この記事を書いている私は個人開発歴は3年、今までに２つのアプリをリリースしています。

# 1 アプリのバージョンを上げる

GooglePlayストアではアプリのバージョン情報を管理しているため、リリース済みのバージョンのままリリースする事はできません。バージョンを上げてリリースします。

# 1.1 build.gradleの表示

AndroidStudioのProjectツールウィンドウからbuild.gradleを表示しましょう。

![app-version.png]({{site.baseurl}}/assets/android_release/app-version.png)


# 1.2 バージョンを上げる

上の画像の `versionCode`と`versionName` の部分がバージョンの記述です。この部分を書き換えればOKです。私は1ずつ上げてます。

```
        versionCode 5
        versionName "5.0"
```

# 2 AndroidStudioでリリース向けのapkを作成をする

AndroidStudioの Buildメニュー > Generate Signed Bundle / APK... を選択する。

![release_build_menu]({{site.baseurl}}/assets/android_release/release_build_menu.png)

APKを選択して[Next]ボタンを押す。

![release_by_apk]({{site.baseurl}}/assets/android_release/release_by_apk.png)

key情報を設定して[Next]ボタンを押す。

![release_key_info]({{site.baseurl}}/assets/android_release/release_key_info.png)

releaseを選択する。Signatureは V1 と V2 両方をチェックする。[Finish]ボタンを押す。

![release_signature_info]({{site.baseurl}}/assets/android_release/release_signature_info.png)

ビルドが終わるとAndroidStudio上に通知が出る。

![release_build_notify]({{site.baseurl}}/assets/android_release/release_build_notify.png)

作成したapkはきちんとバージョンがわかるようにして管理しましょう。以上でapk作成は完了です。

![release_apk_version]({{site.baseurl}}/assets/android_release/release_apk_version.png)


# 3 GooglePlayConsoleで新しいリリースを作成する

今回は過去にGooglePlayConsoleでリリースしたことがあると前提とします。

"アプリのリリース"の製品版の"管理"をクリックする。

![console_product_manage]({{site.baseurl}}/assets/android_release/console_product_manage.png)

[リリースを作成]ボタンを押す。

![console_new_release]({{site.baseurl}}/assets/android_release/console_new_release.png)

[ファイルを選択]ボタンを押して、作成したapkを選択する。

![console_select_apk]({{site.baseurl}}/assets/android_release/console_select_apk.png)

リリースノートを書いて保存ボタンを押す。

![console_release_note]({{site.baseurl}}/assets/android_release/console_release_note.png)

APKでリリースすると警告が出ますが、今回は無視します。

![console_release_warning]({{site.baseurl}}/assets/android_release/console_release_warning.png)

[製品版として公開を開始]ボタンを押すとGooglePlayストアで公開されます。1時間〜半日くらいでストアに反映されると思います。お疲れ様でした。

![console_product_release]({{site.baseurl}}/assets/android_release/console_product_release.png)

<a href="//ck.jp.ap.valuecommerce.com/servlet/referral?sid=3495347&pid=886287729" rel="nofollow"><img src="//ad.jp.ap.valuecommerce.com/servlet/gifbanner?sid=3495347&pid=886287729" border="0"></a>

