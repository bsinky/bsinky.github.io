---
layout: post
title: Pok&eacute;mon Site/Blog Generator
date: 2017-06-27 21:31
categories: ["programming"]
tags: ["programming", "pokemon", "video games"]
excerpt: In writing the Pok&eacute;mon blog posts that I've been frequently posting, I wrote a small program, currently called pk-site.  It ocurred to me today that I hadn't written about the inner workings of my here - until now! 
comments: true
pinned: false
---

In writing the Pok&eacute;mon blog posts that I've been frequently posting, I wrote a small program, currently called [pk-site](https://github.com/bsinky/pk-site).  It ocurred to me today that I hadn't written about the inner workings of my process here - until now!

One thing to note, pk-site does not yet have a LICENSE file, as I'm not entirely sure how to license it due to the various dependencies it has, but that is something I intend to figure out.

### Why program this?

One might wonder, what is the motivation behind this small program? The answer...is not particularly inspiring, truth be told.  I had started playing Pok&eacute;mon Heart Gold (randomized) prior to thinking of writing this program.  Once I'd started, it ocurred to me one day that I'd like a way to track or record my progress over time.  Actually, at first the idea wasn't even "over time," it was simply that I wanted to create a single webpage to display my *current* progress in whatever version I was playing.  It was a friend of mine who suggested I track my progress over time, and the most natural answer to this in my mind was generating blog posts.

So, I set off to write this program.  The first question to answer was this: how do I take the game's record of my progress, the save file, and use the information stored within to create a webpage? Searching on GitHub for "pokemon save," I found that *yes*, parsing the file format of Pok&eacute;mon save files was a problem that several people had already worked on! When choosing which of these solutions I would base my own off of, I first looked at [pksav](https://github.com/ncorgan/pksav), a library written in C.  What deterred me there is that the README file for pksav makes it seem like support isn't entirely there for Generation 4 and up[^1], which was bad news for me since I was looking for Heart Gold support.  The library I settled on for save parsing is [PKHeX](https://github.com/kwsch/PKHeX), which is really a Pok&eacute;mon Save Editor written in C#.

 

---

[^1]: If anyone knows otherwise, please correct me!
