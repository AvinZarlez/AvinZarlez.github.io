---
id: 26081
title: When should you think about multiplatform?
date: 2014-06-16T11:00:59+00:00
author: Tobiah
excerpt: |
  I want to experiment with a new blog post series. People send me questions all the time, so instead of just responding to them via email, I will answer some here on my blog!
  
  Sound fun? Let's get into the first question:
  
  Hey Tobiah. When you were developing your first app, did you target a specific platform? Or did you develop simultaneously for multiple platforms? Thanks for any advice!
  -Scott Christian
  
  Great question, Scott.
  
  The short answer is yes, when making a new app I definitely keep all target platforms in mind...
layout: post
guid: http://www.tobiahmarks.com/?p=26081
permalink: /2014/06/16/think-multiplatform/
categories:
  - Ask Tobiah
tags:
  - Multiplatform
---
I want to experiment with a new blog post series. People send me questions all the time, so instead of just responding to them via email, I will answer some here on my blog!

Sound fun? Let''s get into the first question:

> Hey Tobiah. When you were developing your first app, did you target a specific platform? Or did you develop simultaneously for multiple platforms? Thanks for any advice!
> 
> -**Scott Christian**

Great question, Scott.

The short answer is yes, when making a new app I definitely keep all target platforms in mind. <!--more-->

Specifically, you asked about my _first_ app. In full honesty, it was iOS only. But don''t read too much into that, this was early 2009. The mobile market was kinda completely different back then, this whole "app store" idea was new. Since late 2010, when I make games I think about all target platforms during development.

For instance, most of the art in Blast Monkeys is in vector. Even though we then convert it to a raster format to include in-game, this made so we can easily rescale the art to any size screen.

You make your life easier when you keep multiplatform in mind in your development and testing. You may find a weird bug that only appears on iOS devices, or realize a feature you added has to have some addition code for UI scaling system for Android, or forget to code support for a unique platform feature like Snapview in Windows.

If you just pick one platforms, you''ll have a much harder time trying to track down bugs if your app doesn''t automagically work when you port. Hell, if that one platform you pick is Android, good luck getting your app to work at all. Hardware on Android varies so much, you really ought to follow multiplatform best practices just to get it to work on the most kinds of devices.

When I say multiplatform, I don''t just mean use a technical backend like <a href="http://coronalabs.com/products/corona-sdk/" target="_blank">Corona</a>, <a href="http://unity3d.com" target="_blank">Unity</a>, or <a href="https://xamarin.com/" target="_blank">Xamarin</a>. You have to think about things like screen size, device size, physical button location (if any), compression/memory size, etc. In addition, your monetization strategy may/should vary from platform to platform.

That is a lot to think about if you''re a small developer. There is a good argument on why you may want to release on one platform first. For instance, you could release on Windows first to test market in a smaller audience size and address bugs/issues. That said, you still need to keep multiplatform in mind during development. In the long run, it is faster and easier than focusing on only one platform then dealing with porting issues later.

It''s just bad business to not to do a multiplatform release. No matter which platform you pick, if you’re only picking one you are losing out on millions of potential users.

I hope that answers your question Scott! For everyone else out there, if you have a question you''d like me to answer on the blog please [send me an email](http://www.tobiahmarks.com/contact/ "Contact") and ask away! Your question could be featured on an upcoming blog post.

-Tobiah