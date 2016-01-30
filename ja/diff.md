---
layout: page
title: color_echo version 3.0.0 の変更点  
---

{% include h_section.html name="Ruby版 color_echo の変更点" %}

{% include ref/method.html name="新しいモジュール関数を追加しました" %}

* CE.stateful   
`CE.get` を呼び出してもリセットされません。それまでに定義された `CE.ch`, `CE.pickup` などの装飾に関するすべての指定を保持し続けます。   

* CE.stateless    
`CE.get` を呼び出すとそれまで設定した装飾に関する指定がすべてクリアされます。
デフォルトはこの挙動で `CE.stateful` が実装されていない `version 2.0.x` までの `CE.get` は常にこの挙動です。   


{% include ref/method.html name="メソッド名を変更しました" %}
`CE.hitline`を`CE.highlight`に変更しました。
`CE.reset`のスコープであるシンボル`:hitline`も`:highlight`と指定する必要があります。


{% include ref/method.html name="CE.once, CE.times の影響範囲を変更しました" %}
`CE.pickup`,`CE.highlight`で指定された値は影響を受けず保持し続けていましたが、指定回数を超えるとすべての装飾の指定をリセットするように修正しました。


{% include ref/method.html name="CE.pickup のパラメータのデフォルト値を変更しました" %}
`foreground_color`のデフォルト値は`:red`でしたが`colorecho`コマンドの`-p`オプションに合わせて`:cyan`に変更しました。


{% include ref/method.html name="軽微なバグを修正しました" %}
`color_echo`が無効な状態で`CE.get`に与えた引数が常に配列で返ってくるバグを修正しました。



{% include h_section.html name="コマンド版 color_echo の変更点" %}


{% include ref/method.html name="文字色のデフォルト値を変更しました" %}
`color_echo` のデフォルトの文字色を変更しました。`version 3.0.0` からは文字色、つまり、`-f`オプションのデフォルト値は `nil` となります。ただし例外的に `-p`オプション、または `--stripe`オプションを指定したとき文字色が `nil` のときは `cyan` を文字色に使用します。  

文字色のデフォルト値を変更したいときは[「デフォルト値の設定について」](ref_conf.html#default)をご覧ください。  


{% include ref/method.html name="-p オプションのパラメータを変更しました" %}
以前は`-p pattern`でパターンを指定しマッチした部分には`-f`,`-b`,`-t`オプションで指定した装飾が適用されました。
`version 3.0.0`からは`-p`オプションがとるパラメータが増え各パターンと一致した部分を個別に装飾できるようになり`-p pattern,foreground,background,text_attribute`で指定します。

これにより`-p`オプションを複数指定した場合に各パターン別々の装飾を指定することができるようになりました。
`-f`,`-b`,`t`オプションはパターンとマッチする部分以外に対して適用されます。

詳しくは[コマンド版 color_echo](ref_cli.html)をご覧ください。


{% include ref/method.html name="-H オプションは複数指定できるようになりました" %}
`-p`オプションが各パターン別々の装飾を指定できるようになったのでそれに対応するパターンとマッチした行の装飾もそれぞれ指定できるようにする必要がありました。
`version 3.0.0`からは`-H`オプションは`-p`オプションの数だけ複数指定できます。

詳しくは[コマンド版 color_echo](ref_cli.html)をご覧ください。


{% include ref/method.html name="オプションファイルからオプションを読み込めるようになりました" %}
よく指定するオプションを登録して簡単にコマンドラインから呼び出すことが可能となりました。もう長いオプションをいちいち指定する必要はありません。

詳しくは[オプション読み込み機能について](ref_conf.html)をご覧ください。


{% include ref/method.html name="ロングオプション名を変更しました" %}
`--refresh-pre-match`オプションは`version 3.0.0`からは`--refresh-match`に名前を変更しました。メジャーバージョンのアップデートなので互換性は持たせないので下位のバージョンを使用している方は注意してください。
ショートオプション名に変更はありません。

また、互換性のために存在していた`--symbol_list`,`--index_list`オプションも`version 3.0.0`で削除しています。


{% include ref/method.html name="color_echoコマンドを削除しました" %}
互換性のために`color_echo`コマンドを残していましたが今後は`colorecho`コマンドのみに統一されます。


{% include ref/method.html name="軽微なバグを修正しました" %}
改行コードを含めたテキストを評価するとき`-e`, `--stripe`オプションがテキストより後の改行コードを無視するバグを修正しました。


{% include h_section.html name="共通の変更" %}

{% include ref/method.html name="シンボル :underscore を :underline に変更しました" %}
`CE.tx` や `-t`オプションの値である`underscore`は`underline`に変更されました。
