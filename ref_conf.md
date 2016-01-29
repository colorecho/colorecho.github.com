---
layout: page
title: How to read options from file?
---
When you generate files under directories that `$HOME/.colorecho` or value of environment variable `$COLORECHO` (I'll call this as colorecho options directory),
you don't need any more to input many options.   
You can choose files that are written some options by `-c` option.

When you specified colorecho options deirectory in environment variable `$COLORECHO`, `colorecho` won't try to find files under `.colorecho` directory.

{% include h_section.html name="1. About default options" id="default" %}
When found colorecho options directory, `colorecho` will try to find  a file named `default` under colorecho options directory, even when didn't specify `-c default`.
When found a file that named `default`, `colorecho` read options from it.

{% include ref/small_header.html name="Sets default foreground color(-f option's value) to 'magenta'" %}
{% highlight bash %}
$ vim ~/.colorecho/default
{% endhighlight %}
{% highlight bash %}
f=magenta
{% endhighlight %}

{% include h_section.html name="2. Selectable options files" %}
This is tutorial that to generate and use selectable options files by `-c` option.

* 1 Generates a file that named `foo` in colorecho options directory.

* 2 writes some options and value of it to `$HOME/.colorecho/foo`.
The syntax of that is [Check Syntax of options file](#syntax).

* 3 When you want to use options that were written to `$HOME/.colorecho/foo`,
You might choose them by `-c foo`. In short, `-c` options value meaning a file name in colorecho option’s directory.

{% include h_section.html name="3. Multiple reading options file" %}
You can choose options files by comma as `-c foo,bar`.
When chose options files by `-c` option, files that are chosen must exist.

{% include h_section.html name="4. Priority of options" %}
For example, when be specified as `-c foo,bar`, `default` will be read at first when it was found.
And then `foo` will be read and then `bar` will be read. In short, options file will be read as `default -> foo -> bar`.
Finally, options that are input from command line will be read.

Options to be read later override previous options.

{% include h_section.html name="5. Syntax of options file" id="syntax" %}
* You must write as `option_name=option_value`.
* requires a line break between option and next option.
* Beginning of `#` to end of line is comment.
* You might not surround option's value with `""`.
* You might not escape `"` or `\` with back slash.
* You can't specify here as below options `-l`,`-s`,`-c`,`-h`,`-v`.

{% include ref/small_header.html name="for exmaple " %}
{% highlight bash %}
-f=gray
-b=black
--pickup=/^foo/,h_cyan,nil,bold,underline
-H=blue
{% endhighlight %}

You can omit prefix of `-, --`. So in other syntax as below.
{% highlight bash %}
f=gray
b=black
pickup=/^foo/,h_cyan,nil,bold,underline
H=blue
{% endhighlight %}
