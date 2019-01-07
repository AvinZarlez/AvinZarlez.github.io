---
id: 80451
title: CoronaCards for Windows Phone 8 now available!
date: 2014-10-24T08:34:16+00:00
author: Tobiah
excerpt: |
  As you may know, I am a big fan of Lua and Corona. As of this Tuesday, CoronaCards now supports Windows Phone 8!
  
  Corona is a Lua based game engine to make games for iOS and Android. They are coming out with a new product, CoronaCards, that enables developers to run Corona code everywhere. In native iOS and Android apps, in other engines like Unity and Appcelerator, and now within a Windows Phone 8 Silverlight project.
  
  Want to know what is supported and how you get started? Answers and links are located in the full post through the link below.
layout: post
guid: http://www.tobiahmarks.com/?p=80451
permalink: /2014/10/24/coronacards-windows-phone-8-now-available/
categories:
  - Tools
tags:
  - CoronaSDK
  - Windows Phone
---
[<img class="alignright size-full wp-image-80491" src="/assets/2014/10/CoronaLabs-Flatlogo-URL.png?resize=300%2C64" alt="Corona Labs Logo, creators of CoronaCards" width="300" height="64" data-recalc-dims="1" />](/assets/2014/10/CoronaLabs-Flatlogo-URL.png)As you may know, I am a big fan of Lua and Corona. As of [this Tuesday](http://coronalabs.com/blog/2014/10/21/introducing-corona-support-for-windows-phone-8/), CoronaCards now supports Windows Phone 8!

I look forward to seeing a lot more Lua/Corona based apps on the Windows Phone store!

## What is Corona and CoronaCards?

Corona is a Lua based game engine to make games for iOS and Android. They are coming out with a new product, CoronaCards, that enables developers to run Corona code everywhere. In native iOS and Android apps, in other engines like Unity and Appcelerator, and now within a Windows Phone 8 Silverlight project.<!--more-->

## So is it the full Corona?

Sadly, no. However, there are a good amount of the Corona APIs in CoronaCards. The exact list of supported APIs is here: <http://docs.coronalabs.com/daily/coronacards/wp8/support.html>

## What will I need to get started?

  * A Windows 8.1 machine (or Mac running Windows 8.1 in emulation).
  
    For Emulator support, you will need the 64 bit Pro version.
  * A copy of Visual Studio.
  
    Express works, but you can always get a free version of Ultimate through BizSpark if you happen to run a business that is less than 5 years old, makes less than 1 million dollars, and is privately held/purpose is to make software. For more information about BizSpark, you can [check out the website](http://www.microsoft.com/bizspark/) and/or [send me an email](mailto:Tobiah.Marks@Microsoft.com)!
  
    (If you contact me directly, I can likely help you get through the approval process faster)
  * A Windows Phone, of course!
  
    It has to run Windows Phone 8 or 8.1

## I have those things, how do I get started?

First, you should check out the great documentation on the Corona labs website, it did a really good job with answering all my initial questions: <http://docs.coronalabs.com/daily/coronacards/wp8/index.html>

Next you''ll want to install the CoronaCards Visual Studio extension. A guide can be found here: <http://docs.coronalabs.com/daily/coronacards/wp8/install.html> 

Reading not your thing? Prefer videos? Corona has taken the time to make some as well! <http://coronalabs.com/resources/tutorials/coronacards-enterprise/>

Now you are ready to make a new CoronaCards app! To port an existing app, you first create a new Visual Studio project using the CoronaCards template, and can copy in your Lua code into the Corona folder. Corona has also set up a guide for that: <http://docs.coronalabs.com/daily/coronacards/wp8/portapp.html>

If your app only uses the [supported APIs](http://docs.coronalabs.com/daily/coronacards/wp8/support.html), then you should be up and running in no time!

## What if I want to do something that isn''t supported?

Since CoronaCards runs on top of a Windows Phone 8 Silverlight project, you are actually able to do anything a Windows Phone app can normally do. However, some C# code will have to be involved.

Luckily, CoronaCards has a system to communicate between C# functions and Lua code. Though, if you haven''t done any C# before it might be a little tricky at first. Again, I reference the excellent documentation on Corona''s website: <http://docs.coronalabs.com/daily/coronacards/wp8/communication.html>

As an example, since there is no Store API for CoronaCards, you have to implement your In App Purchases using C# and link the functions to your Lua project. An example of this can be found here: <https://github.com/olomorolo/CoronaCardsWP8_IAPguide>

## What if I have a problem?

In addition to the forum Corona has set up just for Windows Phone development (<http://forums.coronalabs.com/forum/642-coronacards-for-wp8/>), let me know what problems or issues you run into when making your apps/games. You can either reply to this blog post or send me [an email](mailto:Tobiah.Marks@microsoft.com).

I am messing around with it too, and I am very interested in learning what problems/issues/questions/confusions you might be facing!

## What''s next?

I would love it if developers who have created solutions (such as that [IAP example on GitHub](https://github.com/olomorolo/CoronaCardsWP8_IAPguide)) started to share their code with others. If you have such code to share, or interested in writing some, please talk to me! Together we can help make everybody''s CoronaCards for Windows Phone development better and faster.

Either way, let me know what cool apps you make! I want to try them out! If you''re interested, I am also always looking for future guests for my [Be Indie Now](http://www.BeIndieNow.com) podcast.

If you have any other questions/comments/issues, such as what to do once you''re ready to release, let me know! I''m here to help.

-Tobiah