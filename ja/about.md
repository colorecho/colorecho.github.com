---
layout: page
title: color_echo について
---
`color_echo` は ANSIエスケープシーケンスを用いてコマンドライン出力に色をつけたり、装飾を加える gemライブラリです。   

コマンドラインで使用できる `colorecho` コマンドが付属するので Rubyを知らない人でもまったく問題ありません。
`colorecho` コマンドはとても便利なコマンドです。  

[使い方はこちらをご覧ください。](ref_cli.html)

[version 3.0.0 で color_echo がどれだけ変わったかはこちらをご覧ください。](diff.html)

[やる気が出るように color_echo にスターをつけてください =(^x^=]({{site.url-github}})

### 動索環境
* Linux or Mac
* Ruby-2.0.0 and over

### FAQ
* Q: なんで gemパッケージ名が`colorecho`じゃなくて`color_echo`なの？
* A: もともとコマンドラインで使える`colorecho`コマンドは存在しませんでした。
コマンドラインで`color_echo`が使えるようになったのが`version 1.0.0`ですが、コマンドラインから`color_echo`と打つと
アンダースコアの入力が邪魔で面倒なため`color_echo`のエイリアスとして`colorecho`コマンドが用意されました。
`version 3.0.0`からはコマンドラインからの実行は`colorecho`コマンドに統一されました。

### 256色の色の選択が可能です
![screen shot](/images/colorindex01.png)
![screen shot](/images/colorindex02.png)
