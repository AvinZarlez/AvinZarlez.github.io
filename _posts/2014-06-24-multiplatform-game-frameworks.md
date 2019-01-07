---
id: 26443
title: Multiplatform game frameworks
date: 2014-06-24T10:30:11+00:00
author: Tobiah
excerpt: |
  Welcome to part two of a new blog series I've started, "Ask Tobiah"!
  
  You can read last Monday's question about multiplatform development. In response to it, I got today's question:
  
  What are your feelings on the different frameworks for creating cross platform games (such as unity, xamarin etc)? Are they any good? What would make you choose one / not choose one?
  -Matt Whetton
  
  I love them! I'd highly encourage game developers to use frameworks.
  
  It doesn't make sense to me why you would want to reinvent the wheel and deal with all the time and hassle of building your own engine...
layout: post
guid: http://www.tobiahmarks.com/?p=26443
permalink: /2014/06/24/multiplatform-game-frameworks/
categories:
  - Ask Tobiah
tags:
  - CoronaSDK
  - GameMaker
  - Multiplatform
  - Unity
---
Welcome to part two of a new blog series I''ve started, "Ask Tobiah"!

You can read [last Monday''s question](http://www.tobiahmarks.com/2014/06/think-multiplatform/) about multiplatform development. In [response](http://www.tobiahmarks.com/2014/06/think-multiplatform/#comments) to it, I got today''s question:

> What are your feelings on the different frameworks for creating cross platform games (such as unity, xamarin etc)? Are they any good? What would make you choose one / not choose one?
  
> -<b class="fn"><a class="url" href="http://www.codenutz.com" rel="external nofollow">Matt Whetton</a></b>

I love them! I''d highly encourage game developers to use frameworks.

It doesn''t make sense to me why you would want to reinvent the wheel and deal with all the time and hassle of building your own engine&#8230;<!--more--> There is this weird notion that using someone else''s engine is somehow less superior to making your own.

If you''re making a 3d game, you have to make a really convincing argument to me on why you wouldn’t want to use Unity.

Engine programming is a complicated skill and time-consuming process, not everyone can do it, nor should everybody.

For some people, not being in charge of 100% of your own code base is a big deal. But that fear I feel is irrational. Trying to build everything yourself is just not good business. Let me give you fictional example of what I mean:

We''ll say there are two developers working on the exact same game. Developer A will make their own engine, Deverloper B uses Unity.

Developer A has a boss of a programmer that can whip a custom 3D engine that does everything they''d use from Unity, is highly optimized for their game, and best of all they''re able to make it in under 3 months. Not realistic I think, but using that as just as an example. They then spend the next 2 months working on their game. Games aren''t just "finished" when the engine works after all, that''s only the beginning. Making levels, adding new features, polishing up the UI, etc.

Developer B uses a framework like Unity. Their game would be running almost right away. They have 2D/3D graphics, audio, porting to all major platforms, etc. They still have to learn Unity, which means they have to spend a month fixing weird quirks. I hear complaints from people often who say they hate having to figure out workarounds for doing what they need to do with their specific game in a specific engine. I''ll even give you the worst case scenario, and say after that extra month of work they will only be running at 80% optimization compared to what they could get if they made their own engine.

As a side note, 99.99% of the time, this isn''t the case. Developer A doesn''t have a crack team of optimization experts. Developer A is not spending 100% of their time improving their engine, like the team of developers for any game framework would be. Developer A doesn''t have the resources to constantly test every build on [every device/target platform](http://www.tobiahmarks.com/2014/06/think-multiplatform/ "When should you think about multiplatform?"). But again, let''s just go with it for my straw man argument example.

After 5 months of development, Developer A has a game that is fully working, with a basic set of features. Developer B, however, has had almost twice as long to focus on the things that matter. They have had twice the amount of time to add awesome features, play test with users, work on their designs, and simply make the game better.

On the store, if you see game A with half the content and polish as game B, even if game A runs "20% faster!" end users will buy and enjoy game B much more.

An even bigger factor is updates. Developer B was able to get to market faster, and will be able to deliver future updates will be much quickly than Developer A. As we know, we live in an [Apps as a Service](http://www.tobiahmarks.com/2013/10/apps-service-product/ "Apps are a service, not a product") world, and the more often you can update a game the better chance it will have.

Suddenly, a year later, say there is a major operation system update that requires all developers to change their engines. This breaks Developer B''s code, and they are helpless until their framework updates. Yet, Developer A would have to go through the process all over again of working on their engine and debugging code that they haven''t touched in months. Developer B just waits and then updates to the latest version of their framework. Maybe that update takes a month or so to come out&#8230; Well, that is still faster than Developer A might take if they have to do major changes or relearn their own code. Meanwhile, Deverloper B can spend their time working on the game to make it even better than it was when the fix finally does come out.

It''s true that sometimes, an engine does a lot more than you need it to. Some of that bloat could slow things down. Even if that is the case, I argue that it is still faster, cheaper, and worth your time to use whatever tools possible to speed up your development and utilize the work of others.

That''s my argument for using a framework vs. making your own engine. As for which frameworks I recommend using, there isn''t a one-size-fits all framework for game development, although Unity is getting close. A tool like <a href="https://www.scirra.com/construct2" target="_blank">Construct 2</a> might be amazing and fast if you''re making a 2d platforming game, maybe not your massive JRPG. That doesn''t make one tool "worse" than the other, just that you need to use the right one for the right job.

I sang the praises of <a title="Unity3D" href="http://unity3d.com/" target="_blank">Unity</a> in this post because it is my no-brainer recommendation for any game that uses 3D, and has an extremely solid 2D pipeline. I am also a fan of the <a title="Corona SDK" href="http://coronalabs.com/products/corona-sdk/" target="_blank">Corona SDK</a>, which is great for rapid development, and I am a huge advocate of working in Lua. <a title="GameMaker" href="https://www.yoyogames.com/studio" target="_blank">GameMaker </a>is also great for simple prototypes, especially for developers just starting out and learning.

All of those I mentioned have free versions, so there is not reason not to check them out and figure out which is the best tool for you.

Thanks to everybody so far so has sent me questions! I would love to hear from you and answer more. If you''d like to see your post on a future Ask Tobiah [send me an email](http://www.tobiahmarks.com/contact/ "Contact") and ask away!

-Tobiah