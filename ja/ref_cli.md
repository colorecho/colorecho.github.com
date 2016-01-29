---
layout: page
title: コマンド版 color_echo for v3.0.0 and over
---

{% include h_section.html name="使用方法" id="usage" %}
{% highlight bash %}
colorecho [options] message
colorecho [options] < /path/to/file
echo "message" | colorecho [options]
colorecho -v
colorecho -s
colorecho -l
colorecho -h
{% endhighlight %}

{% include h_section.html name="オプション一覧" id="op" %}

{% include ref/method.html name="-s, --symbol-list" %}
文字色、背景色、テキスト属性で指定できるシンボルの一覧を表示します。

{% include ref/method.html name="-l, --index-list" %}
文字色、背景色で指定が可能なカラーインデックスの一覧を表示します。例えば60番の色を指定する場合には`index60`とします。

{% include ref/small_header.html name="例" %}
{% highlight bash %}
$ colorecho Hello -f index220 -b index90
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_cli/index01.png)

[カラーインデックスの一覧をチェックする](ref_colors.html)

{% include ref/method.html name='-p, --pickup "pattern[,foreground_color[,background_color[,text_attribute]]]"' %}
指定したパターンとマッチしたテキストに対してここで指定した文字色、背景色、テキスト属性を適用します。
バージョン2まではマッチしたパターンに適用する装飾は`-f`,`-b`,`-t`オプションで指定でしたが`version 3.0.0`からはここで指定した装飾を適用するようになりました。

このオプションは複数書けます。マッチしたパターンが含まれる行を装飾したい場合は`-H`オプションを使用してください。   

`foreground_color`を指定しなかったとき、パターンとマッチしたテキストに適用するデフォルトの文字色は cyan です。
`/^foo/i`のようにパターンを指定した場合は`pattern`を正規表現リテラルとして扱います。

{% include ref/small_header.html name="例" %}
{% highlight bash %}
$ echo "FooFoOfOO" | colorecho -p "/foo$/i,magenta" -p "/^foo/i,green"
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_cli/pickup01.png)

{% include ref/method.html name='-H, --hightlight "foreground_color[,background_color[,text_attribute]]"' %}
`-p`オプションでマッチした行に対してマッチしたパターン以外の部分に指定した装飾を適用します。  

ひとつ目の`-p`オプションにはひとつ目の`-H`オプションが対応します。
従ってこのオプションは`-p`オプションの数を超えて指定することはできません。
もし`-p`オプションを超える数のオプションが指定された場合、超過分の`-p`オプションとマッチした行には最初に指定した`-H`オプションの装飾が適用されます。   

ひとつの行に`-p`オプションで指定した`pattern`がふたつ以上マッチしたとき最初に指定した`-H`オプションの装飾が適用されます。   


{% include ref/small_header.html name="例" %}
{% highlight bash %}
$ colorecho -e "xxxfooxxx\nxxxxxxfoo\nfooxxxxxx" -p "/foo$/,green" -H index85
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_cli/highlight01.png)

{% include ref/method.html name="-f, --fg color_name" %}
文字色を指定します。使用できる色のリストは`colorecho -s`または`colorecho -l`で確認できます。

{% include ref/method.html name="-b, --bg color_name" %}
背景色を指定します。使用できる色のリストは`colorecho -s`または`colorecho -l`で確認できます。

{% include ref/method.html name="-t, --tx text_attribute[,...]" %}
テキスト属性を指定します。使用できるテキスト属性のリストは`colorecho -s`で確認できます。
このオプションは`-t underline,bold,blink`のように複数書くことができます。

{% include ref/method.html name="-w, --watch" %}
待機モードです。標準入力を待つ場合に使用します。`exit`,`quit`,`bye`もしくは`Ctl + c`でこのモードを抜けることができます。
例えば`tail -f`など、標準入力を受け取りたいときに使用します。

{% include ref/small_header.html name="例" %}
{% highlight bash %}
$ tail -f /tmp/foo.log | colorecho -w -f gray -p foo.html,h_red,nil,bold,underline -H h_cyan
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_cli/watch01.png)

* `-w`と`-p`オプションを使えばこのように特定のパターンを含む行をハイライトするように待機することができます。

{% include ref/method.html name="--stripe" %}
一行間隔を空けて装飾を適用します。このオプションは`-p`オプションとは同時に使用できません。
このオプションを指定したときに`-p`オプションが指定されていても無視されます。   

`-f`,`-b`,`-t`オプションに何も装飾を指定していなかったときは文字色に`cyan`を使用します。

{% include ref/small_header.html name="例" %}
{% highlight bash %}
$ tail -f /tmp/foo.log | colorecho -w --stripe
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_cli/stripe01.png)

{% include ref/method.html name="-r, --refresh-match" %}
入力に対し`-p`オプションで指定したパターンとマッチする場合のみ可能な限りシーケンスコードを取り除きます。

{% include ref/method.html name="-R, --refresh" %}
入力に対し常に可能な限りシーケンスコードを取り除きます。
ただし`f`,`-b`,`-t`,`-p`オプションなど、なんらかの装飾の指定を行っている場合にしか機能しません。

{% include ref/small_header.html name="例" %}
{% highlight bash %}
$ tail -f /tmp/foo.log | colorecho -f index205 -w | colorecho -w --stripe -f index156 -R
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_cli/refresh01.png)

* この例では一度全体の文字色に`index205`で色をつけ、次に`--stripe`で一行飛ばしに`index156`で色をつけています。
すでに`index205`で色づけされているため、それを取り除くために`-R`オプションを指定しています。

{% include ref/method.html name="-c file_name,..." %}
指定したオプション用ファイルからオプションを読み込みます。
カンマ区切りで複数指定でき、オプションが重複するものは後のほうが優先されます。
また、`default`が作成されている場合はこのオプションを指定されなくても常に`default`からオプションを読み込みます。

詳しいリファレンスマニュアルは[オプション読み込み機能について](ref_conf.html)をご覧ください。

{% include ref/method.html name="-n" %}
最後に改行コードを出力しません。

{% include ref/method.html name="-e" %}
改行コードを検出したとき改行コードとして評価します。

{% include ref/method.html name="-v" %}
`color_echo`のバージョンを表示します。

{% include ref/method.html name="-h, --help" %}
ヘルプを表示します。

{% include h_section.html name="使用例" id="eg" %}

あなたはアクセスログからステータスコードが4xx, 5xx番台のログを探していたとします。
![screen shot](/images/ref_cli/eg01.png)

4xxに黄色、5xxに赤色をつけて、さらに文字色を灰色にして目立たせてみましょう。
{% include ref/small_header.html name="例" %}
{% highlight bash %}
$ sed -n 1,1000p /var/log/httpd/access.log | colorecho -f gray -p "/\\s4..\\s/,h_yellow,nil,bold,underline" -H index156 -p "/\\s5..\\s/,h_red,nil,bold,underline" -H index197 | less -R
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_cli/eg02.png)

いかがでしょうか。こんなにも見つけやすくなりました。
しかし少しオプションが長いので外部のファイルに移して好きなときに呼び出せるようにしましょう。

{% include ref/small_header.html name="~/.colorecho/status_code" %}
{% highlight bash %}
f=gray
p=/\s4..\s/,h_yellow,nil,bold,underline
H=index156
p=/\s5..\s/,h_red,nil,bold,underline
H=index197
{% endhighlight %}
ファイルからオプションを指定するときには `\` や `"` を `\\` や `\"` のようにバックスラッシュでエスケープする必要はありません。
これを`~/.colorecho/status_code`で保存したらここに記述した長いオプションを`-c status_code`で呼び出すことができます。

下記のように`tail`と`colorecho`を組み合わせてアクセスログをリアルタイムで監視することもできます。

{% include ref/small_header.html name="例" %}
{% highlight bash %}
$ tail -f /var/log/httpd/access.log | colorecho -w -c status_code
{% endhighlight %}

コマンド版の`colorecho`の使い方で一番便利なのがこのように`tail`などと組み合わせて特定のパターンとそのパターンの含まれる行を強調できることです。
`colorecho`は標準入力を受け付けることも待機することもできるのでいろいろなコマンドと組み合わることができます。

{% include ref/method.html name="組み合わせ例" %}
{% include ref/small_header.html name="vmstat と組み合わせてストライプ状に色をつけて見やすくします" %}
{% highlight bash %}
$ vmstat -n 1 | colorecho -w --stripe
{% endhighlight %}

{% include ref/small_header.html name="netstat と組み合わせて特定のポートを目立たせます" %}
{% highlight bash %}
$ netstat -nat | colorecho -f gray -p :8080,red,nil,bold -H index52 -w
{% endhighlight %}

{% include ref/small_header.html name="top と組み合わせて特定のユーザのプロセスを目立たせます" %}
{% highlight bash %}
$ top | colorecho -p khotta,red,nil,bold,underline -H cyan -w
{% endhighlight %}

{% include ref/small_header.html name="less と組み合わせて特定のパターンを目立たせます" %}
{% highlight bash %}
$ colorecho -p foo < foo.txt | less -R
{% endhighlight %}

{% include ref/small_header.html name="ps と組み合わせて特定のプロセスを目立たせます" %}
{% highlight bash %}
$ ps aux | colorecho -p apache,red,nil,bold,underline -H cyan -w | less -R
{% endhighlight %}
