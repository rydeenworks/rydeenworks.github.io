---
layout: post
title:  "動的計画法の習得"
date:   2024-06-04
categories: dev
---

# 競技プログラミングについて

競技プログラミングが面白いです。始めのうちは簡単な問題はどんどん正解できて面白いのですが、進めていくうちにだんだんと難しめの問題が解けなくて悔しい思いをすることがありました。そのため、難しい問題も解けるようになりたいという欲が出てきました。最近では、競技プログラミングを学ぶのに良い書籍が色々と出ています。

- [問題解決のための「アルゴリズム×数学」が基礎からしっかり身につく本](https://amzn.to/3Kv6L9U)
- [競技プログラミングの鉄則 ~アルゴリズム力と思考力を高める77の技術~](https://amzn.to/4ea2beA)

書籍をざっと眺めみたところ、動的計画法というテクニックを習得することでクリアできる問題が増えそうです。そのため、動的計画法について習得することにしました。

# 問題解決のための「アルゴリズム×数学」が基礎からしっかり身につく本

書籍の3.7節で動的計画法について詳しく説明されています。本を読むことで動的計画法の概要は把握できて、いまは節末問題に取り組んでいます。問題についてはAtCoderで解答を提出できるようになっていて便利です。

## [009 - Brute Force 2](https://atcoder.jp/contests/math-and-algorithm/tasks/math_and_algorithm_i)

ナップサック問題の解法を応用して２次元配列で解けました。どうやったら解法を応用できるか試行錯誤してたら、うまく当てはめることができました。

## [031 - Taro's Vacation](https://atcoder.jp/contests/math-and-algorithm/tasks/math_and_algorithm_ac)

この問題が解けたことで、少しだけコツがつかめました。最初は場合分けや組み合わせ方を考えてたのですが、いまいち解ける気がしませんでした。一晩寝て起きて、あらためて問題を整理しながら考えると、きれいな漸化式で表現ができました。それをプログラムに落とし込んで動作確認して、AtCoderで提出するとクリアできました。

# 競技プログラミングの鉄則 ~アルゴリズム力と思考力を高める77の技術~

自分の理解度を試すために、4章の動的計画法の演習問題を解いてます。以下の問題はすんなり解くことができました。こちらもAtCoderで解答を提出できるようになっていて便利です。

- [B16 - Frog 1](https://atcoder.jp/contests/tessoku-book/tasks/dp_a)
- [B17 - Frog 1 with Restoration](https://atcoder.jp/contests/tessoku-book/tasks/tessoku_book_cp)
- [B18 - Subset Sum with Restoration](https://atcoder.jp/contests/tessoku-book/tasks/tessoku_book_cq)

