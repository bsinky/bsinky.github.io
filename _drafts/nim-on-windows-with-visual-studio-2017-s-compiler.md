---
layout: post
title: Nim on Windows with Visual Studio 2017's Compiler
date: 2017-07-18 12:11
categories: ["programming"]
tags: ["programming", "nim", "windows"]
excerpt: A new blog post
comments: true
pinned: false
---

nim.cgf, set cc=vcc

Use VsDevCmd.bat with -arch=x64 CLI argument to build 64-bit binaries - this is the only way it worked on my work machine.  This gets the compiler, linker, etc., automatically put into the PATH so that the nim compiler can use them

On my work machine the bat was at C:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\Common7\Tools\VsDevCmd.bat, your mileage may vary.

So, with using that from Cmder, my final command to get a Cmder terminal capable of compiling Nim programs was:

%comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\Common7\Tools\VsDevCmd.bat" -arch=x64

Again, the -arch=x64 was *vital* to this working.  I'm not exactly sure *why*, but I received Linker errors (obj file not found) without this part.

Nim Compiler Version 0.17.0 (2017-05-18) [Windows: amd64]

As a fun side affect, this also remedied the issues I had been having compiling [Rust](https://www.rust-lang.org/) code on Windows!
