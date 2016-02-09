---
layout: page
title: Ruby library Reference for v3.1.0 and over
---
* [Two modes](#descript)
* [Reference of module functions](#ref-module-functions)


{% include h_section.html name="Two modes" id="descript" %}
`CE` module will be read by `require 'color_echo'` or `require 'color_echo/get'`.
You might not generate instance because `CE` is not a class, `CE` is a module.
All of function of `color_echo` are module funtion.

For exmaple, when you loaded `require 'color_echo'` and you called `CE.fg(:cyan)`,
standard out of Kernel module functions followings `puts`,`p`,`print`,`printf`,`putc` are colored with `cyan`.

Hint: `printf`,`putc` were added  in `version 3.1.0`.

{% include ref/small_header.html name="for example " %}
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
{% include ref/small_header.html name="result " %}
![screen shot](/images/ref_ruby/ss01.png)

If you would not like to be overwritten `Kernel.#puts`,`Kernel.#p`,`Kernel.#print`,`Kernel.#printf`,`Kernel.#putc`, you might load `require 'color_echo/get'` instead of `require 'color_echo'`.

When you load by `require 'color_echo/get'`, `Kernel.#puts`,`Kernel.#p`,`Kernel.#print`,`Kernel.#printf`,`Kernel.#putc` will not be overrwritten.
You would like to get String that be decorated, you might use `CE.get("foo")`.

{% include ref/small_header.html name="for example " %}
{% highlight ruby %}
require "color_echo/get"

hello  = CE.fg(:yellow).get("Hello")
world  = CE.fg(:index199).bg(:gray).tx(:bold).get("World")
exclam = CE.rainbow.get("!!!!!!!!!!!!!!!!")

puts hello + " " +  world + " " + exclam

puts CE.fg(:blue).pickup(/color$/, :index199).pickup(/^color/, :h_green).get("color color color")
{% endhighlight %}
{% include ref/small_header.html name="result " %}
![screen shot](/images/ref_ruby/get01.png)

{% include h_section.html name="Reference of module functions" id="ref-module-functions" %}

{% include ref/method.html name="CE.pickup(pattern, foreground=:cyan, backgruond=nil, *text_attribute)" %}
<ul class="param">
{% include ref/param.html name="pattern" type="string or regexp or array of them" %}
{% include ref/param.html name="foreground" type="symbol or nil" explain="foreground color of string that matches pattern" %}
{% include ref/param.html name="background" type="symbol or nil" explain="background color of string that matches pattern" %}
{% include ref/param.html name="text_attribute" type="symbol or array of them" explain="text attribute of string that matches pattern" %}
{% include ref/return.html type="self" %}
</ul>

Decorates String that matches pattern with `foreground_color` and `background_color` and `text_attribute`.
You can see the list of value of `foreground_color`, `background_color`, `text_attribute` by `colorecho -s` and also `colorecho -l`.

When to be called `CE.rainbow`, this module function will be ignored.

{% include ref/small_header.html name="for example " %}
{% highlight ruby %}
CE.pickup(/^foo/, :index100, nil, :bold)
{% endhighlight %}

You can highlight specific string by `CE.pickup`.

{% include ref/small_header.html name="for example " %}
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
{% include ref/small_header.html name="result " %}
![screen shot](/images/ref_ruby/pickup01.png)


{% include ref/method.html name="CE.highlight(foreground=nil, background=nil, *text_attribute)" %}
<ul class="param">
{% include ref/param.html name="foreground" type="symbol or nil" explain="foreground color of line that matches pattern" %}
{% include ref/param.html name="background" type="symbol or nil" explain="background color of line that matches pattern" %}
{% include ref/param.html name="text_attribute" type="symbol or array of them" explain="text attribute of line that matches pattern" %}
{% include ref/return.html type="self" %}
</ul>
Decorates line that matches pattern with `foreground_color` and `background_color` and `text_attribute`.
You can see the list of values of `foreground_color`, `background_color`, `text_attribute` by `colorecho -s` and also `colorecho -l`.


{% include ref/method.html name="CE.ch_fg(foreground_color)" %}
<ul class="param">
{% include ref/param.html name="foreground_color" type="symbol" explain="foreground color" %}
{% include ref/return.html type="self" %}
</ul>
Changes foreground color to specified value by `foreground`.

Alias of this module function is `fg`.

* symbol list that can to specify in `foreground`
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

{% include ref/small_header.html name="for example " %}
{% highlight ruby %}
# foreground color turn to red
CE.ch_fg :red
{% endhighlight %}


{% include ref/method.html name="CE.ch_bg(background_color)" %}
<ul class="param">
{% include ref/param.html name="background" type="symbol" explain="background color" %}
{% include ref/return.html type="self" %}
</ul>
Changes background color to specified value by `background_color`.

Alias of this module function is `bg`.

* symbol list that can to specify in `background_color`
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

{% include ref/method.html name="CE.ch_tx(*text_attribute)" %}
<ul class="param">
{% include ref/param.html name="text_attribute" type="symbol or array of them" %}
{% include ref/return.html type="self" %}
</ul>
Changes text attribute to specified value by `text_attribute`.
You can see the list of value of text_attribute by colorecho -s.

Alias of this module function is `tx`.

* symbol list that can to specify in `text_attribute`
    * :bold ... Bold or increased intensity
    * :underline ... Underline: Single
    * :blink ... Blink: Slow
    * :reverse_video ... reverse video
    * :concealed ... Conceal; Not widely supported

{% include ref/small_header.html name="for example " %}
{% highlight ruby %}
# You can specify values at the same time by array
CE.ch_tx [:bold, :underline]
{% endhighlight %}


{% include ref/method.html name="CE.ch(foreground, background=nil, *text_attribute)" %}
<ul class="param">
{% include ref/param.html name="foreground" type="symbol or nil" explain="foreground color; accept `nil`" %}
{% include ref/param.html name="background" type="symbol or nil" explain="background color; accept `nil`" %}
{% include ref/param.html name="text_attribute" type="symbol or array of them" explain="text attribute" %}
{% include ref/return.html type="self" %}
</ul>
Changes foreground color and background color and text attribute to specified values.

{% include ref/small_header.html name="for example " %}
{% highlight ruby %}
# When you would like to specify only foreground color and text attribute,
# you might specify `nil` to background color.
CE.ch :red, nil, :bold
{% endhighlight %}


{% include ref/method.html name="CE.reset(scope=:all)" %}
<ul class="param">
{% include ref/param.html name="scope" type="symbol or array of them" explain="scope of target to reset" %}
{% include ref/return.html type="self" %}
</ul>
resets specified values. scopre of target to reset will be decided parameter of `scope`.
Default is `:all`, So all of values will be reset.

Alias of this module function are `off`, `disable`.

* symbol list that can to specify in `scope`
    * :all ... resets all of values
    * :fg ... resets value of foregroud color by `CE.ch_fg`
    * :bg ... resets value of background color by `CE.ch_bg`
    * :tx ... resets value of text attribute by `CE.ch_tx`
    * :pickup ... reset values of pattern by `CE.pickup`
    * :highlight ... reset values of decoration by `CE.highlight`
    * :rainbow ... reset rainbow foreground color by `CE.rainbow`

{% include ref/small_header.html name="for example " %}
{% highlight ruby %}
# You can specify values at the same time by array
CE.reset [:fg. :tx]
{% endhighlight %}


{% include ref/method.html name="CE.once" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
Decorates just once. It's the same as `CE.times(1)`.

{% include ref/method.html name="CE.times(cnt)" %}
<ul class="param">
{% include ref/param.html name="cnt" type="integer" %}
{% include ref/return.html type="self" %}
</ul>
Decorates number of times that is specified with `cnt`.

{% include ref/small_header.html name="for example " %}
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
{% include ref/small_header.html name="result " %}
![screen shot](/images/ref_ruby/times01.png)


{% include ref/method.html name="CE.enable_refresh(scope=:all)" %}
<ul class="param">
{% include ref/param.html name="scope" type="symbol" %}
{% include ref/return.html type="self" %}
</ul>
Tries to delete sequence code of given input.

* symbol list that can to specify in `scope`
    * :all ... always tries to delete sequence code
    * :prematch ... tries to delete sequence code when matches -p option’s patern


{% include ref/method.html name="CE.disable_refresh" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
Dosen't try to delete sequence code that is given form input. This is default.


{% include ref/method.html name="CE.unuse" %}
<ul class="param">
{% include ref/return.html type="void" %}
</ul>
Turns to disable `color_echo`.


{% include ref/method.html name="CE.rainbow" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
Changes foreground color to like rainbow.


{% include ref/method.html name="CE.get(string)" %}
<ul class="param">
{% include ref/param.html name="string" type="string" explain="string of target" %}
{% include ref/return.html type="string" %}
</ul>
Returns `string` with decoration.
This module function can to call when be loaded not `require 'color_echo'` but `require 'color_echo/get'`.

After this module function was called, all of specification for decoration will be reset.
If you would not that, you might call `CE.stateful` before this module function.


{% include ref/method.html name="CE.stateful" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
Keeps specification for decoration after `CE.get` was called.

When you don't call `CE.get`, this module function is meaningless.


{% include ref/method.html name="CE.stateless" %}
<ul class="param">
{% include ref/return.html type="self" %}
</ul>
All of specification for decoration will be reset after `CE.get` was called.

When you don't call `CE.get`, this module function is meaningless.


{% include ref/method.html name="CE.withdraw(target [,...])" %}
<ul class="param">
{% include ref/param.html name="target" type="symbol" %}
{% include ref/return.html type="array" %}
</ul>
Dose not assign preference of decaration toward the module functions that be specified in argument.
For example executed `CE.withdraw(:printf)`, output of `printf` won't be decorated.
You can specify values at the same time by comma.
The return value is array of symbol that succeeded to withdraw them.

This module function was added in `version 3.1.0`.

* symbol list that can to specify in `target`
    * :puts ... withdraw `Kernel.#puts` decoration
    * :p ... withdraw `Kernel.#p` decoration
    * :print ... withdraw `Kernel.#print` decoration
    * :printf ... withdraw `Kernel.#printf` decoration
    * :putc ... withdraw `Kernel.#putc` decoration


{% include ref/method.html name="CE.get_assigned" %}
<ul class="param">
{% include ref/return.html type="array" %}
</ul>
Returns array of symbol of module functions that assigned preference of decoration.
It will returns `[:puts, :p, :print, :printf, :putc]` When you didn't call `CE.withdraw`.

This module function was added in `version 3.1.0`.
