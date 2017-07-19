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

Lately, a language called [Nim](https://nim-lang.org/) has caught my attention.  Though I'm not very well versed in it *at all* yet, here are my experiences with it so far, installing, learning, and writing my first lines of Nim.

The official Nim site provides a nice overview:

> Nim is a systems and applications programming language. Statically typed and compiled, it provides unparalleled performance in an elegant package.
> * High-performance garbage-collected language
> * Compiles to C, C++ or JavaScript
> * Produces dependency-free binaries
> * Runs on Windows, macOS, Linux, and more

That describes it better than I can, new as I am to the language.

I first got the idea to start writing Nim after I saw [this Reddit post](https://www.reddit.com/r/nim/comments/6llwdx/do_people_use_nim_as_a_general_purpose_scripting/?st=j56rm9vl&sh=b427deb0), from the [Nim subreddit](https://www.reddit.com/r/nim/).  Learning Nim by writing small programs for small tasks was really appealing to me, so I set out to learn it.

#### Learning Nim

I've been using a few different sources to learn Nim, [Nim By Example](http://nim-by-example.github.io/) has been a good reference so far.  It provides small examples of many Nim concepts, which has been helpful just to get a feel for how things in Nim are done.  I've been mostly copying the examples given and making a few simple changes, small extensions to the examples, and so on.

[This guide](http://howistart.org/posts/nim/1/) is what I used to set up my Nim environment.  The post goes on cover Nim programming as well, by building up a [Brainfuck](https://en.wikipedia.org/wiki/Brainfuck) interpreter.  The examples are good.  It's nice that a real program, a Brainfuck interpreter, is created step by step, instead of using a bunch of contrived toy program examples.  They certainly seem to cover a *lot* of Nim's features, but around when the Brainfuck interpreter is converted to a Brainfuck to Nim compiler, the language features began to go over my head.  Revisiting the advanced topics in this resource after I have a bit more Nim experience under my belt is probably a good idea.

So far, those two resources are all I've used.  There's a lot of resources on the official Nim site [here](https://nim-lang.org/documentation.html) that should also prove useful.

#### My Thoughts

I really like Nim's `case` expressions.  The compiler forces you to handle *every* case, and will give an error if you don't handle a case.  For example, this code taken from [this page](https://nim-lang.org/docs/tut1.html#control-flow-statements-case-statement) on the official Nim site:

```nim
from strutils import parseInt

echo "A number please: "
let n = parseInt(readLine(stdin))
case n
  of 0..2, 4..7: echo "The number is in the set: {0, 1, 2, 4, 5, 6, 7}"
  of 3, 8: echo "The number is 3 or 8"
```

This would not compile, providing the following error:

`Error: not all cases are covered`

Nim's `case` seems a lot like pattern matching in many functional languages.  The exhaustive matching done by the compiler is wonderful.

Another point I like about Nim is that it is garbage-collected, which makes it an easy transition from other garbage-collected languages, and produces executables with zero dependencies.  Compile your Nim code, and just distribute the binary - *simple*! No need to verify that a minimum version of Python/.NET/etc. is installed.  This is very refreshing to me, and I feel it's a path that many modern languages have strayed from[^1].

The *downsides* of Nim I've run into so far are mostly related to its (relatively) young nature.  According to the [Wikipedia page](https://en.wikipedia.org/wiki/Nim_(programming_language)), Nim first appeared 9 years ago, originally called Nimrod.  9 years old for a programming language is very, very young.  Nim seems to have a passionate community though, so Googling for documentation/examples/etc. has gone relatively well so far, though there's simply not the amount of resources an old, widespread language like Java would have.

That about covers my initial thoughts on Nim.  If it wasn't painfully obvious, I've barely even scratched the surface of the language.  There are still a number of basic language constructs I haven't encountered.

I'm planning on writing about it again soon - probably in the form of a short tutorial in setting up Nim on Windows to use the Visual Studio 2017 C/C++ compiler.  Look out for that!

---

[^1]: Not all, of course.  I know there are other languages that work similarly to Nim.  [Rust](https://www.rust-lang.org/) comes to mind.
