---
layout: page
title: CLI Reference for v3.0.0 and over
---

{% include h_section.html name="Usage" id="usage" %}
{% highlight bash %}
colorecho [options] message
colorecho [options] < /path/to/file
echo "message" | colorecho [options]
colorecho -v
colorecho -s
colorecho -l
colorecho -h
{% endhighlight %}

{% include h_section.html name="Available Options" id="op" %}

{% include ref/method.html name="-s, --symbol-list" %}
Shows symbol list that can to specify in foreground_color, background_color, text_attr.

{% include ref/method.html name="-l, --index-list" %}
Shows color index list that can to specify in foreground_color, background_color.

For example, When you would like to specify number 60, you must specify `index60`.

{% include ref/small_header.html name="For example" %}
{% highlight bash %}
$ colorecho Hello -f index220 -b index90
{% endhighlight %}
{% include ref/small_header.html name="Result" %}
![screen shot](/images/ref_cli/index01.png)

[See color index list](ref_colors.html)

{% include ref/method.html name='-p, --pickup "pattern[,foreground_color[,background_color[,text_attribute]]]"' %}
Decorates your specified pattern. You can use this option many times.  

If you don't specify foreground_color, will be used cyan as foreground_color for matches pattern.
You have to escape with backslash, when your pattern is included comma, double quote, backslash etc.

`-f`,`-b`,`t` options will be used with the exception of string that matches pattern.
`-p` option accept four arguments as below `-p pattern,foreground,background,text_attribute`.
String that matches pattern will be decorated by `-p` option arguments.
So `version 3.0.0` and over can to specify decoration each `-p` option.

When pattern is surrounded by backslash like `/pattern/`, It will be work as regular expression.

{% include ref/small_header.html name="For example" %}
{% highlight bash %}
$ echo "FooFoOfOO" | colorecho -p "/foo$/i,magenta" -p "/^foo/i,green"
{% endhighlight %}
{% include ref/small_header.html name="Result" %}
![screen shot](/images/ref_cli/pickup01.png)

{% include ref/method.html name='-H, --hightlight "foreground_color[,background_color[,text_attribute]]"' %}
Highlight lines that match pattern which is specified by `-p` option.

A first of `-p` option correspond to a first of `-H` option, also a second of `-p` option correspond to a second of `-H` option.
That's why you can specify this options only same number as `-p` options.   

If two and over patterns are matched in one line, `-H` option will be used that you specified at first.
In case you specfied -H options more than `-p` options, surplus of `-p` option correspond to a first of `-H` option.

{% include ref/small_header.html name="For example" %}
{% highlight bash %}
$ colorecho -e "xxxfooxxx\nxxxxxxfoo\nfooxxxxxx" -p "/foo$/,green" -H index85
{% endhighlight %}
{% include ref/small_header.html name="Result" %}
![screen shot](/images/ref_cli/highlight01.png)

{% include ref/method.html name="-f, --fg color_name" %}
Specifies foreground color. You can see the list of value by `colorecho -s` and also `colorecho -l`.

{% include ref/method.html name="-b, --bg color_name" %}
Specifies background color. You can see the list of value by `colorecho -s` and also `colorecho -l`.

{% include ref/method.html name="-t, --tx text_attribute[,...]" %}
Specifies background color. You can see the list of value by `colorecho -s`.
This option can to specify many values like that `-t underline,bold,blink`.

{% include ref/method.html name="-w, --watch" %}
Keeps wait for standard input.
You can exit this mode follows keywords `exit`,`quit`,`bye` or `Ctl + c`.

{% include ref/small_header.html name="For example" %}
{% highlight bash %}
$ tail -f /tmp/foo.log | colorecho -w -f gray -p foo.html,h_red,nil,bold,underline -H h_cyan
{% endhighlight %}
{% include ref/small_header.html name="Result" %}
![screen shot](/images/ref_cli/watch01.png)

{% include ref/method.html name="--stripe" %}
Decorates on every other line.

When you specified this option, -p option will be ignored. You can't use `--stripe` option and `-p` option at the same time.

When you don't specify any decoration by `-f`,`-b`,`-t`option, will be used cyan as value of `-f` option.

{% include ref/small_header.html name="For example" %}
{% highlight bash %}
$ tail -f /tmp/foo.log | colorecho -w --stripe
{% endhighlight %}
{% include ref/small_header.html name="Result" %}
![screen shot](/images/ref_cli/stripe01.png)

{% include ref/method.html name="-r, --refresh-match" %}
Tries to delete sequence code from input that matches -p option's pattern.

{% include ref/method.html name="-R, --refresh" %}
Tries to delete sequence code from input.
But It will works when you specified `-f`,`-b`,`-t`,`-p`options.

{% include ref/small_header.html name="For example" %}
{% highlight bash %}
$ tail -f /tmp/foo.log | colorecho -f index205 -w | colorecho -w --stripe -f index156 -R
{% endhighlight %}
{% include ref/small_header.html name="Result" %}
![screen shot](/images/ref_cli/refresh01.png)

* This example to add `index205` color to the whole foreground, And then add `index156` color to foreground on every other line.
The whole foreground has already colored with `index205`, That's why must to delete the sequence code before add `index156` color on every other line.

{% include ref/method.html name="-c file_name,..." %}
Reads options from your specify file.
You can specify many files as `-c foo,bar,baz`.
If you have duplicated option name, a previous file be given priority over a subsequent file.

When you have ~/.colorecho/default or $COLORECHO/default, You souldn't specify `-c default`
because a default file will be read automatically.

More information is [Check About option reading from file](ref_conf.html).

{% include ref/method.html name="-n" %}
Do not output the trailing newline.

{% include ref/method.html name="-e" %}
Enable interpretation of line feed.

{% include ref/method.html name="-v" %}
Shows version of color_echo.

{% include ref/method.html name="-h, --help" %}
Shows help message.

{% include h_section.html name="Example" id="eg" %}

You are looking for status code 4xx, 5xx.
![screen shot](/images/ref_cli/eg01.png)

Let's turn color of `4xx` yellow, turn color of `5xx` red, and turn foreground color gray to be emphasized.
{% include ref/small_header.html name="For example" %}
{% highlight bash %}
$ sed -n 1,1000p /var/log/httpd/access.log | colorecho -f gray -p "/\\s4..\\s/,h_yellow,nil,bold,underline" -H index156 -p "/\\s5..\\s/,h_red,nil,bold,underline" -H index197 | less -R
{% endhighlight %}
{% include ref/small_header.html name="Result" %}
![screen shot](/images/ref_cli/eg02.png)

Easy to find that now.

But options are rather long.
So let's move these to a file to call whenever you want.

{% include ref/small_header.html name="~/.colorecho/status_code" %}
{% highlight bash %}
f=gray
p=/\s4..\s/,h_yellow,nil,bold,underline
H=index156
p=/\s5..\s/,h_red,nil,bold,underline
H=index197
{% endhighlight %}
When you specify options from file, shouldn't escape `\` or `"` to `\\` or `\"` by backslash.

Let's save that as `~/.colorecho/status_code`, and then you can call that by `-c status_code`.  
You can watch access log as the file grows by combination of `tail`, `colorecho`.

{% include ref/small_header.html name="For example" %}
{% highlight bash %}
$ tail -f /var/log/httpd/access.log | colorecho -w -c status_code
{% endhighlight %}

You can use many kind of command with `colorecho` because `colorecho` can to receive standard input and also wait it.

{% include ref/method.html name="combination example" %}
{% include ref/small_header.html name="vmstat's output will be added color like stripe " %}
{% highlight bash %}
$ vmstat -n 1 | colorecho -w --stripe
{% endhighlight %}

{% include ref/small_header.html name="Highlights the specific port " %}
{% highlight bash %}
$ netstat -nat | colorecho -f gray -p :8080,red,nil,bold -H index52 -w
{% endhighlight %}

{% include ref/small_header.html name="Highlights the specific user's process " %}
{% highlight bash %}
$ top | colorecho -p khotta,red,nil,bold,underline -H cyan -w
{% endhighlight %}

{% include ref/small_header.html name="Highlights the specific pattern " %}
{% highlight bash %}
$ colorecho -p foo < foo.txt | less -R
{% endhighlight %}

{% include ref/small_header.html name="Highlights the specific process " %}
{% highlight bash %}
$ ps aux | colorecho -p apache,red,nil,bold,underline -H cyan -w | less -R
{% endhighlight %}
