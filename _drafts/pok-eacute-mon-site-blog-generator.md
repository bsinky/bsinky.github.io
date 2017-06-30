---
layout: post
title: Pok&eacute;mon Site/Blog Generator
date: 2017-06-27 21:31
categories: ["programming"]
tags: ["programming", "pokemon", "video games"]
excerpt: In writing the Pok&eacute;mon blog posts that I've been frequently posting, I wrote a small program, currently called pk-site.  It occurred to me today that I hadn't written about the inner workings of my here - until now! 
comments: true
pinned: false
---

In writing the Pok&eacute;mon blog posts that I've been frequently posting, I wrote a small program, currently called [pk-site](https://github.com/bsinky/pk-site).  It occurred to me today that I hadn't written about the inner workings of my process here - until now!

One thing to note, pk-site does not yet have a LICENSE file, as I'm not entirely sure how to license it due to the various dependencies it has, but that is something I intend to figure out.

### Why program this?

What is the motivation behind this small program? The answer, is not particularly inspiring, truth be told.  I had started playing Pok&eacute;mon Heart Gold (randomized) prior to thinking of writing this program.  Once I'd started, it occurred to me one day that I'd like a way to track or record my progress over time.  Actually, at first the idea wasn't even "over time," it was simply that I wanted to create a single webpage to display my *current* progress in whatever version I was playing.  It was a friend of mine who suggested I track my progress over time, and the most natural answer to this in my mind was generating blog posts.

So, I set off to write this program.  The first question to answer was this: how do I take the game's record of my progress, the save file, and use the information stored within to create a webpage? Searching on GitHub for "pokemon save," I found that *yes*, parsing the file format of Pok&eacute;mon save files was a problem that several people had already worked on! When choosing which of these solutions I would base my own off of, I first looked at [pksav](https://github.com/ncorgan/pksav), a library written in C.  What deterred me there is that the README file for pksav makes it seem like support isn't entirely there for Generation 4 and up[^1], which was bad news for me since I was looking for Heart Gold support.  The library I settled on for save parsing is [PKHeX](https://github.com/kwsch/PKHeX), which is really a Pok&eacute;mon Save Editor written in C#.

### Writing the Code

Choosing a C# library had an added benefit for me; I'm very familiar with the C# ecosystem and tooling.  It didn't take long for me to get something up and running with PKHeX.  By [this commit](https://github.com/bsinky/pk-site/commit/88b53d0eff75e9c6c9a3ac61489a4b81f9c989bd), I seemingly had single page generation working, including images of party Pok&eacute;mon By [this commit](https://github.com/bsinky/pk-site/commit/88b53d0eff75e9c6c9a3ac61489a4b81f9c989bd), I seemingly had single page generation working, including images of party Pok&eacute;mon.  Afterward, I focused on improving the style of the generated page, switching from some very basic CSS I had written to the [Bulma](http://bulma.io/) CSS framework.  Bulma is a framework I've used before, and I really like the aesthetics of it, and how easy to use it is.

The single webpage generation of pk-site uses [RazorEngine](https://github.com/Antaris/RazorEngine) to generate the outputted HTML.  I had a few issues initially with getting RazorEngine to work.  RazorEngine is a [templating engine](https://en.wikipedia.org/wiki/Template_processor).  My plan was to use RazorEngine for its text replacement and loops, even though it is capable of far more, and I could basically use it to write whatever C# code I wanted within a template, and it would just work.  I *did* end up getting RazorEngine to work how I wanted, but only after at least an hour of confused debugging and wondering why my template was compiling, but failing when I ran it with my given data.

### Adding Blog Postability

After my friend helped me with the blog post idea, it seemed like a simple matter to add blog post generation to pk-site.  I had thought that RazorEngine only supported HTML generation, and would fail to generate non-HTML output.  I wanted to generate Markdown, so I began looking for another templating engine, since I (wrongly[^2]) believed RazorEngine could not do this for me. 

Not long after starting my search, I found [Handlebars.Net](https://github.com/rexm/Handlebars.Net).  The README describes it well: 

> [Handlebars.js](http://handlebarsjs.com/) is an extension to the Mustache templating language created by Chris Wanstrath. Handlebars.js and [Mustache](https://mustache.github.io/) are both logicless templating languages that keep the view and the code separated like we all know they should be.

Handlebars.Net was *extremely* simple to use.  The issues I had experienced with RazorEngine were nowhere to be found with Handlebars.Net.  Of course, I imagine the trade-off is that Handlebars.Net might not be as powerful as RazorEngine, but I don't have enough experience with either to really compare their features.  In any case, Handlebars.Net gave me the features I needed (simple text replacement and loops), in a very straightforward way.  I've used Handlebar.js in previous projects, so it was also somewhat familiar to me.

In no time at all, I was generating Markdown posts with pk-site! Handlebars.Net worked so well that I've been thinking of switching the original website generation of pk-site to use it instead of RazorEngine.

---

[^1]: If anyone knows otherwise, please correct me!

[^2]: Turns out, RazorEngine can easily be configured to generate any kind of raw text output, including Markdown, by using setting `config.EncodedStringFactory` to an instance of `RawStringFactory`, so it *definitely* would have been an option for me, had I investigated it further.
