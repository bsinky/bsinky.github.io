---
layout: post
title: Skyrim Mods 101
date: 2017-06-19 20:36
categories: ["videogames"]
tags: ["video games", "skyrim"]
---

![image](http://cdn.akamai.steamstatic.com/steam/apps/72850/header.jpg?t=1493767797)

## Introduction

Skyrim is one of my all time favorite games, and today we're going to do a write up on getting started playing with mods!

Skyrim is good even in its un-modded, vanilla form.  But *with* mods, Skyrim is an *incredible* experience.

Mods for Skyrim can range from whimsical...

![image]({{ site.url }}/images/skyrim-mods-101/funnymods.jpg)

...to epic, DLC-sized addons - available entirely free of cost[^1], and made by passionate fans.  Pictured here is the map of the wholly new Falskaar area, from [the mod of the same name](http://www.nexusmods.com/skyrim/mods/37994/?).

![image]({{ site.url }}/images/skyrim-mods-101/falskaarmap.png)

So, how does one begin playing Skyrim with mods? Read on, and find out!

## Getting Started

The first decision to be made, which version of the game to play.  The remastered **Skyrim Special Edition** (hereafter known as **SSE**), or the **Original Skyrim**?

There are pros and cons to each.

**Original Skyrim** has a *huge* catalog of mods available.  There's a good chance that whatever you want your Skyrim experience to be, there's an Original Skyrim mod to do it.  Other pros for Original Skyrim, Skyrim Script Extender (SKSE) is available, and is required for some *very* nice mods, such as [SkyUI](http://www.nexusmods.com/skyrim/mods/3863/?), [RaceMenu](http://www.nexusmods.com/skyrim/mods/29624/?), and many others.  We'll get into SKSE and those mods in more detail later.  For now, just know that SKSE is available *only* for Original Skyrim at this time, and it allows modders to do things that they would otherwise be unable to.

The *downsides* of Original Skyrim are that while it is possible to install graphical mods like [RealVision ENB](http://www.nexusmods.com/skyrim/mods/30936/?)[^2] and mod the game where it looks potentially *better* than SSE, unless you have a very powerful gaming rig, be prepared to make huge performance sacrifices.

SSE is still new in the grand scheme of things.  Releasing on October 27th, 2016, as of this writing the game isn't yet a year old, so the modding community for SSE hasn't had time to catch up to Original Skyrim.  That said, many of the high-profile, essential mods for Original Skyrim *have* been converted to work with Skyrim Special Edition, such as [Immersive Armors](http://www.nexusmods.com/skyrimspecialedition/mods/3479/), [Alternate Start - Live Another Life](http://www.nexusmods.com/skyrimspecialedition/mods/272/?), and [Apocalypse - Magic of Skyrim](http://www.nexusmods.com/skyrimspecialedition/mods/1090/?).

The *downsides* of SSE are nearly opposite of Original Skyrim - the game should run smoother, even with quite a few mods, *but* the catalog of mods available is nowhere near the size of the Original Skyrim.

Once you've decided what version of the game you will be playing, it's time for the real work to begin - downloading mods!

## Downloading and Installing Mods

The biggest site for finding Skyrim mods is [Nexus Mods](http://www.nexusmods.com/games/?).  There's a section of the site for each supported game.  So, [the Skyrim Nexus](http://www.nexusmods.com/skyrim/?) is where you'll go for Original Skyrim, and [the SSE Nexus](http://www.nexusmods.com/skyrimspecialedition/?) for SSE.

At this point in time[^3], I highly recommend downloading [Nexus Mod Manager](http://www.nexusmods.com/skyrimspecialedition/mods/modmanager/?), known as NMM.  NMM makes it very easy to download mods from Nexus, and in addition supports the installation scripts that some mods[^4] use.  Once you install NMM, you should be able to downloads mods with one click by clicking "Download (NMM)" from the page of the mod or from its "Files" tab ("Download With Manager" there), if it supports the feature.  The following instructions will assume you are using NMM.

![image]({{ site.url}}/images/skyrim-mods-101/downloadnmm.png)

![image]({{ site.url}}/images/skyrim-mods-101/downloadwithmanager.png)

TODO: walkthrough of how to activate/install a mod, maybe with a screenshot?

## LOOT - sorting your load order

![image]({{ site.url }}/images/skyrim-mods-101/loot.png)

[LOOT](https://loot.github.io/) is an absolute *requirement* in my book, no matter how many mods you are using or intend to use.  You'll want to download and install the latest release from the linked site at this point.

As the LOOT site describes it, LOOT is able to sort your mod load order automatically in order to provide you a stable game that won't crash[^5], even when you load it full of hundreds of mods.

TODO: LOOT setup, walkthrough ,etc.

---

[^1]: Although, the "free of cost" aspect may only be due to the fact that modders cannot legally charge for their created content.  At least, not currently, but the upcoming [Creation Club](https://bethesda.net/en/article/3lO9zYi5QksEqwUoYowAMs/fallout-4-and-skyrim-special-edition-creation-club)  will presumably change that.  That's *not* a topic I'll be addressing here though. 

[^2]: There are many, many ENB presets out there.  I've always been happy with RealVision - the performance to prettiness ratio is right where I want it.  That said, though I've never used it myself, the screenshots for [Tetrachromatic ENB](http://www.nexusmods.com/skyrim/mods/73848/?) look ***great***!.

[^3]: Once upon a time, I would have whole-heartedly recommended [ModOrganizer](http://www.nexusmods.com/skyrim/mods/1334/?) instead, as it has the same features as NMM and more nice things on top of that.  The original developer has stopped worked on it though, and to be honest I haven't followed it since then.  Plus, it doesn't seem to support SSE well either (although it appears there's a [fork](https://github.com/LePresidente/modorganizer/releases) of the project on GitHub by a new developer working on SSE support).  The nice thing about NMM is that it works equally well for both Original and SSE.

[^4]: A lot of mods use these to let you turn various mod features on or off during installation, or to install compatibility patches based on other mods you're using.  They're very useful!

[^5]: To be fair, the game will still probably crash from time to time.  **But** without a properly sorted load order it would crash even more!
