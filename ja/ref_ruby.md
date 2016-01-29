---
layout: page
title: Ruby版 color_echo for v3.0.0 and over
---
* [2つのモード](#descript)
* [モジュール関数リファレンス](#ref-module-functions)

{% include h_section.html name="2つのモード" id="descript" %}

`require 'color_echo'`もしくは`require 'color_echo/get'`で`color_echo`を読み込むと`CE`というモジュールが組み込まれます。ruby から`color_echo`を使用する場合はオブジェクトを作る必要はありません。`color_echo`の機能はすべてモジュール関数で実装されています。   

例えば`CE.fg(:cyan)`をコールすると組み込みの Kernel module の以下の3つモジュール関数`Kernel.p, Kernel.puts, Kernel.print`のコマンドライン出力が`cyan`に変わります。    

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
require 'color_echo'
puts "Hello World !!"

CE.fg(:cyan)
puts "Hello World !!"

CE.bg(:gray)
puts "Hello World !!"

CE.tx(:bold,:underline)
puts "Hello World !!"
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_ruby/ss01.png)

Kernel module のモジュール関数がオーバライドされ自動で装飾されることを望まない場合は`require 'color_echo'`ではなく、`require 'color_echo/get'`で読み込んでください。   

`require "color_echo/get"`で読み込むと`color_echo`は`Kernel.p, Kernel.puts, Kernel.print`の出力を装飾しません。装飾したテキストを取得するには`CE.get("some message")`を使います。   

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
require "color_echo/get"

hello  = CE.fg(:yellow).get("Hello")
world  = CE.fg(:index199).bg(:gray).tx(:bold).get("World")
exclam = CE.rainbow.get("!!!!!!!!!!!!!!!!")

puts hello + " " +  world + " " + exclam

puts CE.fg(:blue).pickup(/color$/, :index199).pickup(/^color/, :h_green).get("color color color")
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_ruby/get01.png)

{% include h_section.html name="モジュール関数リファレンス" id="ref-module-functions" %}

{% include ref/method.html name="CE.pickup(pattern, foreground=:cyan, backgruond=nil, *text_attribute)" %}
<ul class="param">
{% include ref/param.html name="pattern" type="string or regexp or array of them" explain="パターン。" %}
{% include ref/param.html name="foreground" type="symbol or nil" explain="パターンとマッチしたワードの文字色。" %}
{% include ref/param.html name="background" type="symbol or nil" explain="パターンとマッチしたワードの背景色。" %}
{% include ref/param.html name="text_attribute" type="symbol or array of them" explain="パターンとマッチしたワードの装飾。" %}
{% include ref/return.html type="self" %}
</ul>
パラメータ`pattern`とマッチする文字列を指定した文字色、背景色、テキスト属性で色づけします。使用できる文字色等は、`colorecho -s` または `colorecho -l` で確認できます。`CE.rainbow` がコールされている場合はこの機能は無視されます。   

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
CE.pickup(/^foo/, :index100, nil, :bold)
{% endhighlight %}

`CE.pickup`を使えば特定のワードだけを色づけすることができます。

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
CE.fg(:h_cyan).pickup("color_echo", :h_white, :red, :underline).pickup("COLOR_ECHO", :h_yellow)

puts <<EOS
xxxxxxxxxxxxxxxxxcolor_echoxxxxxxxxxxxxxxxxxxxxxxxx
xxxxcolor_echoxxxxxxxCOLOR_ECHOxxxxxxxxxxxxxxxxxxxx
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
xxxxxxxxxxxxxxxxxcolor_echoxxxxxxxxxxcolor_echoxxxx
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
EOS
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_ruby/pickup01.png)


{% include ref/method.html name="CE.highlight(foreground=nil, background=nil, *text_attribute)" %}
<ul class="param">
{% include ref/param.html name="foreground" type="symbol or nil" explain="パターンとマッチした行の文字色。" %}
{% include ref/param.html name="background" type="symbol or nil" explain="パターンとマッチした行の背景色。" %}
{% include ref/param.html name="text_attribute" type="symbol or array of them" explain="パターンとマッチした行の装飾。" %}
{% include ref/return.html type="self" %}
</ul>
`CE.pickup`でマッチした行に対して、指定した文字色、背景色、テキスト属性で色づけします。


{% include ref/method.html name="CE.ch_fg(foreground)" %}
<ul class="param">
{% include ref/param.html name="foreground" type="symbol" %}
{% include ref/return.html type="self" %}
</ul>
文字色を指定した色に変更します。エイリアス`fg`でも呼び出し可能です。

* パラメータ`foreground`で指定できるシンボルの一覧
    * :black
    * :red
    * :green
    * :yellow
    * :blue
    * :magenta
    * :cyan
    * :white
    * :gray
    * :h_red
    * :h_green
    * :h_yellow
    * :h_blue
    * :h_magenta
    * :h_cyan
    * :h_white
    * :index[1-256]

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
# 文字色が赤になります。
CE.ch_fg :red
{% endhighlight %}




{% include ref/method.html name="CE.ch_bg(background)" %}
<ul class="param">
{% include ref/param.html name="background" type="symbol" explain="指定できるシンボルの一覧は foreground と同様。" %}
{% include ref/return.html type="self" %}
</ul>
背景色を指定した色に変更します。エイリアス`bg`でも呼び出し可能です。




{% include ref/method.html name="CE.ch_tx(*text_attribute)" %}
<ul class="param">
{% include ref/param.html name="text_attribute" type="symbol or array of them" %}
{% include ref/return.html type="self" %}
</ul>
テキスト属性を指定した色に変更します。エイリアス`tx`でも呼び出し可能です。`colorecho -s`でそれぞれどのような装飾になるかチェックすることができます。

* パラメータ`text_attribute`で指定できるシンボル一覧
    * :bold ... 文字を太字にします。
    * :underline ... 文字に下線をつけます。
    * :blink ... 文字を点滅させます。
    * :reverse_video ... 文字色と背景色を反転させます。
    * :concealed ... サポートされている環境が少ないため削除予定です。

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
# テキスト属性は同時に複数の指定が可能です。
CE.ch_tx [:bold, :underline]
{% endhighlight %}


{% include ref/method.html name="CE.ch(foreground, background=nil, *text_attribute)" %}
<ul class="param">
{% include ref/param.html name="foreground" type="symbol or nil" explain="文字色。nil を許可。" %}
{% include ref/param.html name="background" type="symbol or nil" explain="背景色。nil を許可。" %}
{% include ref/param.html name="text_attribute" type="symbol or array of them" explain="テキスト属性。" %}
{% include ref/return.html type="self" %}
</ul>
文字色、背景色、テキスト属性を指定したものに変更します。

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
# 文字色、テキスト属性の指定のみ行いたい場合は背景色に nil を指定します。
CE.ch :red, nil, :bold
{% endhighlight %}


{% include ref/method.html name="CE.reset(scope=:all)" %}
<ul class="param">
{% include ref/param.html name="scope" type="symbol or array of them" explain="リセット対象のスコープ。下記参照。" %}
{% include ref/return.html type="self" %}
</ul>

指定した色やテキスト属性をリセットします。リセットする範囲はスコープで決まります。
デフォルトは :all ですのですべての設定がリセットされます。エイリアス`off`, `disable`でも呼び出し可能です。

* パラメータ`scope`で指定できるシンボル一覧
    * :all ... すべての指定をリセットします。
    * :fg ... 文字色に関する指定をリセットします。
    * :bg ... 背景色に関する指定をリセットします。
    * :tx ... テキスト属性に関する指定をリセットします。
    * :pickup ... `CE.pickup`で指定したパターンに関する指定をリセットします。
    * :highlight ... `CE.highlight`で指定したパターンとマッチした行に関する装飾の指定をリセットします。
    * :rainbow ... `CE.rainbow`を呼び出したことによる装飾をリセットします。

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
# このように配列で複数のシンボルを同時に指定することも可能です。
CE.reset [:fg. :tx]
{% endhighlight %}


{% include ref/method.html name="CE.once" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
一度だけ設定した装飾を適用します。これは`CE.times(1)`と同様です。


{% include ref/method.html name="CE.times(cnt)" %}
<ul class="param">
{% include ref/param.html name="cnt" type="integer" %}
{% include ref/return.html type="self" %}
</ul>
`cnt`で指定した回数だけ設定した装飾を適用します。標準出力（もしくは`CE.get`）するたびに回数がインクリメントされます。

{% include ref/small_header.html name="例" %}
{% highlight ruby %}
CE.once.ch :h_yellow, :h_red, :underline
puts "first"
puts "second"

puts "\n"

CE.times(3).rainbow
puts "first"
puts "second"
puts "third"
puts "fourth"
{% endhighlight %}
{% include ref/small_header.html name="結果" %}
![screen shot](/images/ref_ruby/times01.png)


{% include ref/method.html name="CE.enable_refresh(scope=:all)" %}
<ul class="param">
{% include ref/param.html name="scope" type="symbol" %}
{% include ref/return.html type="self" %}
</ul>
与えられた入力に対して可能な限りシーケンスコードを取り除きます。

* パラメータ`scope`で指定できるシンボル一覧
    * :all ... いかなる時もシーケンスコードを取り除きます。
    * :prematch ... `CE.pickup`で指定したパターンにマッチした時だけシーケンスコードを取り除きます。


{% include ref/method.html name="CE.disable_refresh" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
与えられた入力に対してシーケンスコードを取り除きません。デフォルトはこの挙動です。


{% include ref/method.html name="CE.unuse" %}
<ul class="param">
{% include ref/return.html type="void" %}
</ul>
このメソッドがコールされた時点で`color_echo`の機能を無効にします。


{% include ref/method.html name="CE.rainbow" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
出力をレインボーにします。


{% include ref/method.html name="CE.get(string)" %}
<ul class="param">
{% include ref/param.html name="string" type="string" explain="装飾したい文字列。" %}
{% include ref/return.html type="string" %}
</ul>
`string`を装飾して返します。`require 'color_echo/get'`を読み込んだ時だけ使えるメソッドです。

このメソッドが呼び出されたあとは装飾に関するこれまでの指定はリセットされます。
この機能を望まない場合は`version 3.0.0`で新しく追加された`CE.stateful`をこのメソッドの前で一度だけコールしてください。


{% include ref/method.html name="CE.stateful" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
`CE.get` を呼び出したあともそれまでに定義された `CE.ch`, `CE.pickup` などの装飾に関するすべての指定を保持し続けます。
`CE.get` を使用しない場合は意味のないメソッドです。


{% include ref/method.html name="CE.stateless" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
`CE.get` を呼び出すとそれまで設定した装飾に関する指定がすべてクリアされます。デフォルトはこの挙動です。
`CE.get` を使用しない場合は意味のないメソッドです。
