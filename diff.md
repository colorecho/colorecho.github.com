---
layout: page
title: The difference bitween version 3 and 2
---

{% include h_section.html name="The change of for ruby library" %}

{% include ref/method.html name="Added new method functions" %}

* CE.stateful   
Preference for decorations that is specified by user won't be reset when you called `CE.get`.   
Preference for decorations is specified by `CE.ch`,`CE.pickup` or something will be retained.

* CE.stateless    
All of Preference for decorations will be reset when you call `CE.get`. version 2 and under version are always this behavior.


{% include ref/method.html name="Changed module funtion's name" %}
`CE.hitline` is renamed to `CE.highlight`.
And also, you couldn't call `CE.reset :hitline` on `version 3.0.0` and over, you must call like `CE.reset :highlight`
when you would like to be off highlights.


{% include ref/method.html name="Changed scope of CE.once, CE.times" %}
Changed that when you call `CE.times(n)` and then after over n times, Preference of decorations will be reset as scope :all.


{% include ref/method.html name="Changed CE.pickup's default value of foreground_color" %}
Changed `:red` to `:cyan` in order to match as `-p`option's default value of `colorecho` command.


{% include ref/method.html name="Fixed small bug" %}
When `color_echo` was disabled, `CE.get` always returns array even if given string. Fixed it on this version.



{% include h_section.html name="The change of for CLI" %}

{% include ref/method.html name="Changed default value of foreground" %}
Changed default value of foreground color `yellow` to `nil`. It means `-f` option's default value is `nil`.   
As an exception, It will be used `cyan` for foreground color when you sepecified `-p` option or `--stripe` option.  
When you would like to change default color, please take a look at [About default options](ref_conf.html#default).


{% include ref/method.html name="Changed parameters of -p option" %}
In `version 2` and under, `-p` option accept one argument like `-p pattern` and string that matches the pattern will be decorated by `-f`,`-b`,`-t` options. It has been chenged.  
`-p` option accept four arguments as below `-p pattern,foreground,background,text_attribute`.  

More information is [Check Reference for CLI](ref_cli.html).


{% include ref/method.html name="You can specify -H option more than one" %}
You can specify as many `-H` options, as many `-p` options.

More information is [Check Reference for CLI](ref_cli.html).


{% include ref/method.html name="You can specify some options from file" %}
You can specify options that often use, and you can call them easily. Do not need to specify many options each time any more.

More information is [Check About option reading from file](ref_conf.html).


{% include ref/method.html name="Changed log option name" %}
`--refresh-pre-match` option has been renamed `--refresh-match` option. There is no change in the short option name.   

`--symbol_list`,`--index_list` options that existed for compatibility were deleted in `version 3.0.0` and over.


{% include ref/method.html name="Deleted 'color_echo' command" %}
`color_echo` command was remained for compatibility. It be unified only in `colorecho` command in `version 3.0.0` and over.

{% include ref/method.html name="Fixed small bug" %}
Fixed the bug as below, If string is included some line break, `-e` option or `--stripe` option ignore them after string.



{% include h_section.html name="Common changes" %}

{% include ref/method.html name="Changed symbol :underscore to :underline" %}
Changed value of `CE.tx` and `-t`option. You must use `underline` instead of `underscore`.
