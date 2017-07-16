---
layout: post
title: Nim First Impressions
date: 2017-07-16 07:31
categories: ["programming"]
tags: ["programming", "nim"]
excerpt: Lately, a language called Nim has caught my attention.  Though I'm not very well versed in it at all yet, here are my experiences with it so far, installing, learning, and writing my first lines of Nim.
comments: true
pinned: false
---

Lately, a language called Nim has caught my attention.  Though I'm not very well versed in it *at all* yet, here are my experiences with it so far, installing, learning, and writing my first lines of Nim.

[Nim](https://nim-lang.org/) is a very interesting language.  The official site gives a good overview of it:

> Nim is a systems and applications programming language. Statically typed and compiled, it provides unparalleled performance in an elegant package.
> * High-performance garbage-collected language
> * Compiles to C, C++ or JavaScript
> * Produces dependency-free binaries
> * Runs on Windows, macOS, Linux, and more

That describes it better than I can, new as I am to the language.

I first got the idea to start writing Nim after I saw [this Reddit post](https://www.reddit.com/r/nim/comments/6llwdx/do_people_use_nim_as_a_general_purpose_scripting/?st=j56rm9vl&sh=b427deb0), from the [Nim subreddit](https://www.reddit.com/r/nim/).  Learning Nim by writing small programs for small tasks was really appealing to me, so I set out to learn it.

#### Learning Nim

I've been using a few different sources to learn Nim, [Nim By Example](http://nim-by-example.github.io/) has been a good reference so far.  It provides small examples of many Nim concepts, which has been helpful just to get a feel for how things in Nim are done.  I've been mostly copying the examples given and making a few simple changes, small extensions to the examples, and so on.

[This guide](http://howistart.org/posts/nim/1/) is what I used to set up my Nim environment.  The post goes on cover Nim programming as well, by building up a [Brainfuck](https://en.wikipedia.org/wiki/Brainfuck) interpreter.  The examples are good, it's nice that a real program, a Brainfuck interpreter, is created step by step, instead of using a bunch of contrived toy program examples.  They certainly seem to cover a *lot* of Nim's features, but around when the Brainfuck interpreter is converted to a Brainfuck to Nim compiler, the language features began to go over my head.  Revisiting the advanced topics in this resource after I have a bit more Nim experience under my belt is probably a good idea.

So far, those two recources are all I've used.  There's a lot of resources on the official Nim site [here](https://nim-lang.org/documentation.html) that should also prove useful.

#### My Thoughts

I really like Nim's `case` expressions.  The compiler forces you to handle *every* case, and will give an error if you don't handle a case.  For example, this modified code I took from Nim by Example:

```nim
case "charlie":
  of "alfa":
    echo "A"
  of "bravo":
    echo "B"
  of "charlie":
    echo "C"
```

This would not compile,
