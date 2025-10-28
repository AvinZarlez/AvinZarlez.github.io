---
id: 102151
title: Which platform should you release on first?
date: 2015-05-28T14:00:15+00:00
author: DEADNAME
excerpt: |
  Today’s Ask DEADNAME comes from Samuel Schumacher:
  
  “My team and I are just wondering how many (and which) platforms we should support on launch. We are deep into development of a new endless runner/platformer game built mainly for touch screens (we are using Unity 5 for development). We are aiming to support as many platforms as possible, but are unsure as to which ones are the best to launch with (or if we should launch on all at the same time).”
  -Samuel Schumacher
  
  In an ideal world, the answer is clear: Release everywhere simultaneously.
  
  There are probably hundreds if not thousands of blog posts that debate the merits of releasing on one platform vs. another first. You can judge one as “better” than the other by all sorts of metrics:
  
  Which device do you own/like more?
  What percentage of users pay for apps?
  How many devices were activated last month?
  How many devices have been activated ever?
  How many similar apps were released last month?
  How long does it take for updates to appear on the store?
  
  The problem with all of these is that they start from a false premise… That one platform is better than others to release on first.
  
  Read on to see my full answer!
layout: post
guid: http://www.OLDURL/?p=102151
permalink: /2015/05/28/which-platform-should-you-release-on-first/
categories:
  - Ask DEADNAME
---
Today’s Ask DEADNAME comes from Samuel Schumacher:

> “My team and I are just wondering how many (and which) platforms we should support on launch. We are deep into development of a new endless runner/platformer game built mainly for touch screens (we are using Unity 5 for development). We are aiming to support as many platforms as possible, but are unsure as to which ones are the best to launch with (or if we should launch on all at the same time).”
  
> -Samuel Schumacher

In an ideal world, the answer is clear: Release everywhere simultaneously.<!--more-->

## There is no one “winner”

There are probably hundreds if not thousands of blog posts that debate the merits of releasing on one platform vs. another first. You can judge one as “better” than the other by all sorts of metrics:

  * Which device do you own/like more?
  * What percentage of users pay for apps?
  * How many devices were activated last month?
  * How many devices have been activated ever?
  * How many similar apps were released last month?
  * How long does it take for updates to appear on the store?

The problem with all of these is that they start from a false premise… That one platform is better than others to release on first.

There are millions of potential paying users on Android, iOS, and yes even Windows Phone. If you exclude yourself from any of them, you’re losing out.

I use a Windows Phone, but I have many friends who use Android or iOS. If I tell them about a cool game, but they can’t play it, you’re losing out on virality/”K-Factor”. The more markets your game appears in, the higher chance you’ll get noticed and start rising up the charts.

## Develop with cross platform in mind

If you’re already using a tool like Unity 5, the effort needed to port could be next to nothing.

There is no good reason not to keep all platforms in mind when you’re developing your game.

Make sure you game works on:

  * Different resolution screens
  * Screens of a different physical sizes
  * Low end hardware and older devices
  * High end hardware and newer devices
  * Older OS versions
  * Newer recent OS updates

This may sound like extra work, but honestly: It’s kind of steps you have to do anyway in order to run on Android devices alone.

By being mindful of such things, it will make your game a great experience on Android phones and tablets, iOS phones and tablets, Windows Phones, and even Windows touch desktops and tablets.

## Common problems

All that said, we don’t live in an ideal world. There are some extra factors to consider, and they may limit your ability to release on other devices. Such as:

  * Game relies on certain plugins or services that aren’t available on all platforms.
  * Hardware requirements (Such as a Fingerprint scanner, or NFC)
  * Developer registration fees ($99 per year for Apple, $25 one-time fee Google Play, $19 one-time fee for Windows store both desktops and tablets)
  * Exclusive deals or external licensing rights

You’re using Unity, but if you used other engines such as GameMaker you’d also have to [weigh in the extra cost for those modules](http://www.OLDURL/2015/04/gamemaker-html5-module-worth-the-cost/).

These problems can be dealt with. It doesn’t sound like your game has any special plugin or hardware requirements. There are many choices for basic things like ad services, analytics, etc. including some that work on all three platforms.

Even if you’re using a plugin or service that only works on certain platforms, you can wrap the code around [platform dependent compilation #if statements](http://docs.unity3d.com/Manual/PlatformDependentCompilation.html), so you won’t have to worry about multiple codebases.

Developer fees are fairly cheap, and even iOS’s expensive $99/yr is probably worth it if your game has half way decent monetization.

Exclusive deals can be nice if you get them, but they usually have to be pretty good to overcome the lost revenue of releasing on multiple platforms. If you’re exclusive to a platform, there is a higher chance of being featured. But, being tri-platform doesn’t mean you won’t be featured. Usually you’ll only be featured if your game is popular anyway, and it’s easier to get more popular if you can get yourself out there in more places and in front of more people.

## Release simultaneously? What’s “close enough”?

For the launch, it may be worth it to hold back the Windows/Android release a few days until the iOS build is approved. But you should hold back your launch anyway. After you’re ready to go on all platforms, you ought to give yourself time to hype your (confirmed) launch date, connect with press, and test/bug fix.

For updates, unless the game has cross platform multiplayer it’s not as big of concern. Just make sure one platform doesn’t fall behind another.

## Bottom line

In my experience, the extra effort required is worth it for being on all platforms, even if those platformers are “smaller”.

For your case specifically, it sounds like your endless runner/platform game should work well on a variety of types of devices, and using Unity enables you to still only need one codebase to maintain.

I would definitely create your game with a cross platform release in mind.

* * *

Thanks for the great question Samuel, let me know when your game comes out! Good luck.

-DEADNAME