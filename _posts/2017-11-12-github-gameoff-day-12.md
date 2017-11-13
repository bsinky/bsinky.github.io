---
layout: post
title: GitHub GameOff Day 12
date: 2017-11-12
categories: ["gamedev"]
tags: ["gamedev", "godot", "programming", "githubgameoff"]
summary: Wrapping up Day 12 of GitHub GameOff 2017
comments: true
pinned: false
---

Nearly 10 days have passed since the last update on GitHub GameOff 2017.

That's a scary thought, because quite honestly I've been sitting around idly during that time! Actually, I have been very busy playing a certain JRPG[^1], which I enjoyed very much, but for gamedev things I have been slacking.  Since the last write-up, I haven't done much of anything with Godot, besides read documentation pages here and there.  The most involved thing I have done with it remains the toy demo seen in my Day 3 write-up.

Not to say efriedman3 and I haven't been *thinking* about the GameOff.  We've spent quite a bit of time discussing ideas for games that would fit the "throwback" theme of the jam.  Our focus has centered primarily on 2 ideas:

 - Take a retro game and modernize it
 - Create an original game that feels retro

Other ideas were also considered, but those are the 2 that I remember most clearly and those that we've brainstormed about most.  Currently, the potential games we would make for each category are, respectively:

 - "Super Pong 2K18", a modern take on the classic game "Pong"
   - Specific gameplay changes and enhancements aren't exactly nailed down
 - An adventure game similar to the original NES "The Legend of Zelda"
   - Maybe with unique, single button combo/pattern combat

We've actually started with the initial steps of creating a few iterations of the first idea, "Super Pong 2K18."  Nothing particularly of note yet, but ideally in the next week we'll have figured out for sure what the gameplay should be like.  The area we've struggled with most is, "how do we make this game *fun*?" It's a simple question, but we haven't come up with a simple answer of what will draw people in to play our game.  We have high hopes that once we start delving in more deeply testing iterations of different gameplay styles the answer will be become clear.

For now, here's a very, very, extremely early screenshot of what my current branch looks like when running.

![image]({{ site.url }}/images/gameoff/gameoff-day-12-3.jpg)

Aside from that, I played around *very* briefly with some of Godot's animation features, namely [AnimatedSprite](http://docs.godotengine.org/en/stable/classes/class_animatedsprite.html) and [Animations](http://docs.godotengine.org/en/stable/learning/step_by_step/animations.html) themselves.  I'm a little blown away by how quickly I was able to get things animated onscreen.  AnimatedSprite in particular is very easy to grok, and it's easy so see how they could be used to create game characters that animate differently depending on whether they are walking, attacking, etc..

Here are some very stimulating visuals from my animation tests.  First, what the setup looks in Godot's editor.  One thing I want to mention, I do enjoy Godot's editor interface.  Everything seems to work pretty well, nothing really gets in your way, and so on.

![image]({{ site.url }}/images/gameoff/gameoff-day-12-1.jpg)

Which, when running, produces the following "game":

<div style='position:relative;padding-bottom:59%'><iframe src='https://gfycat.com/ifr/SizzlingOnlyEwe' frameborder='0' scrolling='no' width='100%' height='100%' style='position:absolute;top:0;left:0;' allowfullscreen></iframe></div>

Quick shout out to [OpenGameArt.org](https://opengameart.org), which is where the [goblin](https://opengameart.org/content/2d-goblin-chibi) and [background](https://opengameart.org/content/forest-background-art-2) graphics from the above demo came from.  These assets are provided courtesy of users [ramtam](https://opengameart.org/users/ramtam) and [Segel](https://opengameart.org/users/segel), respectively.

That's it for now.  No matter what happens with our GameOff entry in the coming weeks, this has been an enjoyable experience.  As before, working with Godot has been very refreshing - a lot to learn, to be sure, but the lessons are rewarding since the end result is something interactive or visual, and the workflow in Godot (modifying a scene and then running the updated scene) allows for instant gratification.

Thanks for reading, we'll catch you in the next update!


---

[^1]: It was [Shin Megami Tensei Persona 3 FES](http://megamitensei.wikia.com/wiki/Persona_3_FES) by the way.  I enjoyed it so much that you may see a post solely about it in the future.  Even if said post is just 20 paragraphs of raving fanboyism.
