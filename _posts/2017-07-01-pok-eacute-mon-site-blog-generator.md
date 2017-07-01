---
layout: post
title: Pok&eacute;mon Site/Blog Generator
date: 2017-07-01 08:28
categories: ["programming"]
tags: ["programming", "pokemon", "video games"]
excerpt: In writing the Pok&eacute;mon blog posts that I've been frequently posting, I wrote a small program, currently called pk-site.  It occurred to me today that I hadn't written about the inner workings of my here - until now! 
comments: true
pinned: false
---

In writing the Pok&eacute;mon blog posts that I've been frequently posting, I wrote a small program, currently called [pk-site](https://github.com/bsinky/pk-site).  It occurred to me today that I hadn't written about the inner workings of my process here - until now!

One thing to note, pk-site does not yet have a LICENSE file, as I'm not entirely sure how to license it due to the various dependencies it has, but that is something I intend to figure out.

### Why program this?

What is the motivation behind this small program? The answer is not particularly inspiring, truth be told.  I had started playing Pok&eacute;mon Heart Gold (randomized) prior to thinking of writing this program.  Once I'd started, it occurred to me one day that I'd like a way to track or record my progress over time.

Actually, at first the idea wasn't even "over time," it was simply that I wanted to create a single webpage to display my *current* progress in whatever version I was playing.  It was a friend of mine who later suggested I track my progress over time and the most natural answer to this, in my mind, was generating blog posts.

So, I set off to write this program.  The first question to answer was this: how do I take the game's record of my progress, the save file, and use the information stored within to create a webpage?

Searching on GitHub for "pokemon save," I found that *yes*, parsing the file format of Pok&eacute;mon save files was a problem that several people had already worked on! When choosing which of these solutions I would base my own off of, I first looked at [pksav](https://github.com/ncorgan/pksav), a library written in C.  What deterred me there is that the README file for pksav makes it seem like support isn't entirely there for Generation 4 and up[^1], which was bad news for me since I was looking for Heart Gold support.

The library I settled on for save parsing is [PKHeX](https://github.com/kwsch/PKHeX), which is actually *not* a library, but a full Pok&eacute;mon Save Editor written in C#.  Even though PKHeX is written as a standalone save-editing program, I am able to reference it as a dependency in pk-site, and reuse as much of its logic as I needed.

### Writing the Code

Choosing a C# library had an added benefit for me; I'm very familiar with the C# ecosystem and tooling.  It didn't take long for me to get something up and running with PKHeX.  The API for PKHeX was straightforward enough, and very fully featured.  Parsing the save is a single method call, regardless of which game or generation the save file is from.  It was very convenient! The GUI for the PKHeX Save Editor, its primary purpose, includes tiny thumbnail images of every Pok&eacute;mon.  Retrieving those images to use in pk-site was also very simple.  One method call, and I had an `Image` instance that I could save and include in the generation website/blog post!

One of the downsides of my reuse of PKHeX's Pok&eacute;mon Image code is that pk-site has a dependency on more than just `PKHeX.Core`, the project that contains the base save parsing code.  I also need to reference the GUI project `PKHeX.WinForms`, which means that when I compile I end up compiling not just my pk-site binary, but I also need to compile *all* of PKHeX, and wind up having the entire PKHeX Save Editor binary in my output directory.

I'm not sure of the best way around this, without restructuring PKHeX's code.  I *could* write my own code to retrieve Pok&eacute;mon images, but PKHeX's is *really* convenient and also renders images of whatever Item a Pok&eacute;mon is holding as part of the Pok&eacute;mon sprite.  Which is really cool! So, at the moment, I'm not planning on refactoring to get rid of the `PKHeX.WinForms` dependency, but I have thought about it.  If I did, I would probably approach it the same way PKHeX does, and make it as simple as this (real PKHeX call to get an image of a Pok&eacute;mon):

```cs
Image pokemonImage = pokemon.Sprite();
```
It doesn't get easier than that.

By [this commit](https://github.com/bsinky/pk-site/commit/88b53d0eff75e9c6c9a3ac61489a4b81f9c989bd), I seemingly had single page generation working, including images of party Pok&eacute;mon.  Afterward, I focused on improving the style of the generated page, switching from some very basic CSS I had written, to the [Bulma](http://bulma.io/) CSS framework.  Bulma is a framework I've used before.  I really like the aesthetics of it, and how easy to use it is.

The single webpage generation of pk-site uses [RazorEngine](https://github.com/Antaris/RazorEngine) to generate the outputted HTML.  I had a few issues initially with getting RazorEngine to work.  RazorEngine is a [templating engine](https://en.wikipedia.org/wiki/Template_processor).  My plan was to use RazorEngine for its text replacement and loops, even though it is capable of far more and I could basically use it to write whatever C# code I wanted within a template, and it would just work.  I *did* end up getting RazorEngine to work how I wanted, but only after at least an hour of confused debugging and wondering why my template was compiling, but failing when I fed it data and tried to generate HTML.

### Adding Blog Postability

After my friend helped me with the blog post idea, it seemed like a simple matter to add blog post generation to pk-site.  I had thought that RazorEngine only supported HTML generation, and would fail to generate non-HTML output.  I wanted to generate Markdown, since that's what Jekyll blog posts are written in, so I began looking for another templating engine, since I (wrongly[^2]) believed RazorEngine could not do this for me. 

Not long after starting my search, I found [Handlebars.Net](https://github.com/rexm/Handlebars.Net).  The README describes it well: 

> [Handlebars.js](http://handlebarsjs.com/) is an extension to the Mustache templating language created by Chris Wanstrath. Handlebars.js and [Mustache](https://mustache.github.io/) are both logicless templating languages that keep the view and the code separated like we all know they should be.

Handlebars.Net was *extremely* simple to use.  The issues I had experienced with RazorEngine were nowhere to be found with Handlebars.Net.  Of course, I imagine the trade-off is that Handlebars.Net might not be as powerful as RazorEngine, but I don't have enough experience with either to really compare their features.  In any case, Handlebars.Net gave me the features I needed (simple text replacement and loops), in a very straightforward way.  I've used Handlebar.js in previous projects, so it was also somewhat familiar to me.

For what I needed, Handlebars was a dream come true.  For instance, creating the loop to go through the Party Pok&eacute;mon is this simple:

```handlebars
{% raw %}
<div class="columns is-multiline is-mobile">
  {{#Model.PartyMembers}}
     {{> party}}
  {{/Model.PartyMembers}}
</div>
{% endraw %}
```

Then, there's simply another template file, `party.hb`, that contains the template to render for each and every party member.  In no time at all, I was generating Markdown posts with pk-site!

### What's Next?

Handlebars.Net worked so well that I've been thinking of switching the original website generation of pk-site to use it instead of RazorEngine.  I don't need any of the advanced code-in-the-template RazorEngine features.  In the near future, I probably *will* make this change, but it should be completely transparent and not affect the output in any noticeable way.

Other future plans include:

  1. Cleaning up the code
  2. Redesigning the code with proven design patterns in mind
  3. Allow options to be passed in with a configuration file instead of requiring them to be passed from the command line
  4. Add more features??

The 1st and 2nd items are what I feel most strongly about.  I really want to use pk-site as an opportunity to learn more about design patterns, and see where I can make things in pk-site's codebase more robust and flexible without compromising current features.  Along that same line, writing a few unit tests is also something I would like to do, to gain some experience there.

pk-site isn't, and perhaps never will be, large enough where unit tests are *needed*.  The codebase is small enough that if I break something, tracking it down would be a very simple process.  *But*, if I could write unit tests to automatically tell me when I made a change that breaks something, that would be very nice indeed.

---

[^1]: If anyone knows otherwise, please correct me!

[^2]: Turns out, RazorEngine can easily be configured to generate any kind of raw text output, including Markdown, by using setting `config.EncodedStringFactory` to an instance of `RawStringFactory`, so it *definitely* would have been an option for me, had I investigated it further.
