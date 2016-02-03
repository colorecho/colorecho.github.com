---
layout: page
title: Release Note
---

* version 3.1.0, 2016-02-04
    * Preference of decoration will be work in Kernel.printf, Kernel.putc.
    * Added new module functions -> CE.withdraw, CE.get_assigned. Please take a look at the reference.
    * [Fixed the problem](https://github.com/khotta/color_echo/issues/3)

* version 3.0.0, 2016-01-29
    * [The difference bitween version 3 and 2](diff.html)

---

* v2.0.4, 2016-01-06
    * [Fixed the problem](https://github.com/khotta/color_echo/issues/2)

* v2.0.3, 2016-01-06
    * rebuild by old gem, because latest gem can't use symbolic link in bin/.

* v2.0.2, 2016-01-06
    * [Fixed the problem](https://github.com/khotta/color_echo/issues/1)
    * This version has problem of fail to execute colorecho command, Please use v2.0.3 and over.

* v2.0.1, 2015-08-21
    * Fixed bug that highlight of line is incorrect in commandline interface.

* v2.0.0, 2015-05-20
    * Added new module functions -> CE::hitline, CE.enable_refresh, CE.disable_refresh. Please check the reference.
    * Can to select new parameter ':hitline' in CE.reset.
    * Flushes any buffered data when output data to STDOUT.
    * Fixed bug, When the input was included invalid encoding.
    * Fixed not to be output the interruptted message, When you pressed ctl + C.
    * Fixed default foreground color to yellow in command line interface.

---

* version 1.3.0, 2015-02-06
    * Change some options help messages.
    * You can call 'colorecho' as 'color_echo' in command line interface.

* version 1.2.0, 2015-01-28
    * Add -e option.

* version 1.1.0, 2015-01-27
    * Modified to output the argument when the standard input is hit.
    * Add --stripe option in the command line interface.
    * Change the delimiter of long option with a hyphen -> --symbol-list,--index-list; Can to specify also underline as before.

* version 1.0.0, 2015-01-23
    * Add command line interface.

---

* version 0.9.0, 2015-01-19
    * Add a mode to receive as the words with ANSI escape sequence; without output to display.

* version 0.8.0, 2015-01-14
    * Change for the specified arguments of reset method.
    * Fix small bugs.

* version 0.7.0, 2015-01-08
    * Add new method -> pickup
    * Add new symbol that can to specify in reset method of first parameter -> CE.reset(:pickup)

* version 0.6.0, 2015-01-05
    * Add command line tool.

* version 0.5.0, 2014-12-16
    * Add a new method -> \#once, \#times

* version 0.4.0, 2014-12-11
    * Add 256 colors.

* version 0.3.0, 2014-12-08
    * Add high colors.
    * Can to select multi value in ch_tx method.
    * Add parameter to the #reset method.

* version 0.2.4, 2014-12-04
    * Can to specify a non-string when rainbow mode.
    * Cab take over the setting of other types of sequence when rainbow mode.

* version 0.2.3, 2014-12-02
    * Fix small bugs.

* version 0.2.0
    * Added new method -> rainbow
    * Added some method alias.

* version 0.1.0
    * Added new method -> ch, unuse
    * Added some method alias.
