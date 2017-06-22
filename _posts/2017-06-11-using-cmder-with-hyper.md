---
layout: post
title: Using Cmder with Hyper
date: 2017-06-11 08:33
excerpt: Today I'm writing about Hyper, a program that essentially wraps a terminal instance in a pretty UI.
categories: ["programming", "tools"]
comments: true
---
Today I'm writing about [Hyper](https://hyper.is/), a program that essentially wraps a terminal instance in a pretty UI.  It might sound underwhelming, but it looks *really* good, and besides that has a number of plugins available to add features that you might not be able to get in a standard terminal.

![Hyper with Cmder terminal running on Windows]({{ site.url }}/images/hypercmder/hypercmder1.png)

This is especially true on Windows.  Terminal users are limited to either `cmd` or `powershell`, the latter of which is without a doubt more modern and useable, and yet for some reason I never find myself using `powershell` on Windows, and instead open up `cmd` without a thought when I need a terminal.

That brings us to [Cmder](http://cmder.net/).  Cmder is self-described as a "terminal emulator for Windows," so it is along the same vein as Hyper.  Cmder has some really nice features, like tab-autocomplete commands, which is something Windows `cmd` didn't have for a very long time, as far as I know[^1].  It has numerous other features, including tabs, there's a version that comes bundled with nice utilites like `ls` and `grep`, and so on.  I highly recommend Cmder to anyone who uses the terminal frequently on Windows.  You won't regret it! 

So Cmder offers a lot of nice features, and Hyper looks really cool...but what if I wanted to use a Cmder-style terminal within Hyper?

As I found out earlier this week, it is indeed possible.

So, first off, it appears that Cmder accomplishes much of the magic is does by running a command like this:

{% highlight bat %}
cmd /k "%ConEmuDir%\..\init.bat"  -new_console:d:%USERPROFILE%
{% endhighlight %}

The interesting bit to me was the argument passed with the `/k` switch.  Whatever that `bat` file does could be easily called when launching Hyper as well, since Hyper's `.hyper.js` config file exposes startup arguments for the terminal it launches.

With that in mind, getting a Cmder-like terminal running within Hyper is basically just a few simple steps:

 1. Figure out what your %ConEmuDir% directory is by runnning `echo %ConEmuDir%` **within Cmder** (I don't think that environment variable is set otherwise)
 2. In `.hyper.js`, inside the value for `env`, add a key `ConEmuDir: 'Your/ConEmuDir/Path/Here'` 
 3. Again in `.hyper.js`, add to the `shellArgs` array 2 values - the `/k` switch, and `%ConEmuDir%\..\init.bat` as the second

You should end up with something that looks similar to this[^2]:

{% highlight javascript %}
shellArgs: ['--login', '/k', '%ConEmuDir%\..\init.bat'],

env: {
    'ConEmuDir': 'C:\Path\To\Your\ConEmuDir'
},
{% endhighlight %}

And that's it! If you launch Hyper, you should be greeted with a Cmderesque terminal experience, with the current working directory text colored, and (depending on if you installed this Cmder version) Unix commands like `ls` available.

You may notice that I ommitted the `-new_console:` argument that Cmder uses.  I never attempted to use it in my own testing - it may or may not work/play nicely within Hyper, I do not know.  Try it if you dare!

The question you may be asking is, "If Cmder on Windows is so good, why would I ever use Hyper?"

I think the answer there is: try them both!

---

[^1]: I'm really not sure *when* `cmd` got tab completion, but it as only writing this post that I fired up `cmd` and noticed that is would autocomplete something like `expl` to `explorer` when I pressed tab.

[^2]: Your `.hyper.js` config may not have the `--login` argument in shellArgs, mine did by default so I left it there.  I am unsure if `--login` has any meaning in `cmd` or `powershell`...
