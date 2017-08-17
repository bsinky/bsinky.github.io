---
layout: post
title: hx8 - My First Foray into Emulation
date: 2017-08-17 00:00
categories: ["programming"]
tags: ["programming", "haxe", "emulation"]
excerpt: I am pleased to share that my first emulator project, hx8, is complete!
comments: true
pinned: false
---

I am pleased to share that my first emulator project, **hx8**, is complete!

Not to say there isn't room for improvement, or that I won't add more features, but I am happy with where the project is at now.

Now, onto the details!

### hx8 - a Chip-8 Emulator

hx8 is an emulator/interpreter for the [Chip-8](https://en.wikipedia.org/wiki/CHIP-8), written in [Haxe](http://haxe.org/).

I like to think of the Chip-8 as a fake computer system, but that's probably not entirely accurate.  The Wikipedia article gives a much better explanation and background.  Whatever technical name you give Chip-8, the important thing here is that hx8 can run programs written for Chip-8.

This is a project I began *years* ago[^1], but I set it aside very early on and forgot about it.  For a **long** time.  

hx8 stagnated for over *2 years*, until I found my repo again and checked in a few changes in September and October of 2016.

Then, a little under a month ago, I re-discovered the repo, and *really* dove in.  Luckily, getting back up to speed on the project was simple.  There wasn't a ton of code written when I got started on the project again.  Chip-8 is pretty simple, so there's not a ton of logic to implement anyway.  It had been a while since I had written any Haxe, and getting my feet wet in the language was again was great!

I'd like to mention a few truly *invaluable* resources that helped me through this project:

* [This article](http://www.multigesture.net/articles/how-to-write-an-emulator-chip-8-interpreter/) was the first resource I used, and it was simply *instrumental* in getting off the ground.
* [This Javascript Chip-8 emulator](https://github.com/alexanderdickson/Chip-8-Emulator) was also used occasionally for inspiration.
* [Octo](http://johnearnest.github.io/Octo/) is something I found very late in the game, but it was also very useful! Being able to download some of the Chip-8 games that people have created using Octo, then run them on hx8 and see them work was incredible.
* Last but certainly not least, my fianc&eacute;e, Shannon, for her support and help in writing this very post!


### The Struggles

I'm happy with how hx8 turned out.  There were a few challenges along the way.  Some of the biggest hurdles I faced:

#### *Tiny* errors in my code that had **HUGE** game-breaking ramifications in emulation.

These probably took the most time for me to solve.  For instance, the Chip-8 opcode FX29, I had implemented for the longest time like so:

```haxe
I += V[x] * 5;
```

FX29 is supposed to "Set I equal to location of sprite for digit Vx."  For the longest time, I stared at this implementation and though, "yeah, this looks right."  I load the digit sprites into memory starting at 0, hexadecimal digits 0 through F, and they're each 5 bytes long, so assuming V[x] is between 0 and F, this works.

But it didn't work, and I ended up with horribly garbled graphics whenever a game needed to render a digit! Below, you can see what PONG looked like at this point in hx8's history.

![image]({{ site.url }}/images/hx8/hx8-fx29-1.png)

Notice the glitchy-looking nonsense at the top? That's supposed to be each player's score.  That's the result of reading from the incorrect memory location to grab the digit sprite.  I took a long look at my implementation, and then at a few other implementations, and I *finally* saw my mistake.  I was *adding* to the value of I, not simply setting it.  The proper implementation for this opcode after I realized my idiocy:

```haxe
I = V[x] * 5;
```

*One* **single** character difference.  Look again if you didn't see the difference - I know I didn't, for a very long time! Below, observe PONG after the fix:

![image]({{ site.url }}/images/hx8/hx8-1.png)

#### Creating a file dialog

This was an issue I didn't expect to have, but I had a lot of difficulties getting a "Select file..." type dialog to open.

Initially, I was using the HaxeFlixel game engine.  At this point, I tried to also add the haxelib [systools](https://lib.haxe.org/p/systools/) library, for its file dialog capabilities.  All the builds I created during that time crashed at runtime, so I gave up.

Then, I tried using [lime's](https://lib.haxe.org/p/lime/) file dialog, since HaxeFlixel is built on top of OpenFL and lime, so I already had that dependency.  This didn't work for me either, though I don't recall the exact error.

Finally, I decided to drop the HaxeFlixel dependency, and just use lime for graphics/input/windowing.  This meant I could use the latest version of lime (HaxeFlixel is locked to an older version).  Dropping the HaxeFlixel dependency is something I wanted to do anyway[^2], and a quick test before commiting to the lime rewrite told me that yes, lime 5.3.0's file dialog *did* work!

One thing I still haven't figured out how to do is add a "File" menu to the lime window, and include an "Open..." option there.  This is an enhancement I would like to make at some point, but I don't know of an idiomatic Haxe/lime way to do it.  If anyone has done this in lime, please let me know, point me to the code if possible, and I would be very grateful!

### Closing Thoughts

Creating hx8 was a wild ride.  You can view the MIT licensed source code [on GitHub](https://github.com/bsinky/hx8).

It's my first step into further emulation projects, but it's not a step I thought I'd ever finish.  Up until this point I still saw emulators as black magic sorcery.  They appear less like sorcery to me now, and I believe Haxe and lime are a solid platform upon which to write an emulator.  I hope to start another emulator in Haxe in the near future.

I'll leave you with a few screenshots of hx8 running various Chip-8 games.  In a few, you can see one of hx8's features, changeable Chip-8 "screen" colors.  It's a basic feature, but one I am proud to have implemented nonetheless.

![image]({{ site.url }}/images/hx8/hx8-2.png)

![image]({{ site.url }}/images/hx8/hx8-3.png)

![image]({{ site.url }}/images/hx8/hx8-4.png)

![image]({{ site.url }}/images/hx8/hx8-6.png)

---

[^1]: My first commit was on May 18th, 2014!

[^2]: This is not an attack on HaxeFlixel at all - it's a fantastic library! It was just overkill for what I needed to accomplish, which is why dropping it in favor of only lime so much sense.
