---
id: 1381
title: How can I reduce file size?
date: 2013-10-25T22:50:38+00:00
author: Tobiah
layout: post
guid: http://tobiahmarks.com/?p=1381
permalink: /2013/10/25/reduce-file-size/
categories:
  - Tips and tricks
tags:
  - App Rank Optimization
  - Download limits
  - File Size
  - Friction Points
  - PNGCrush
  - Prevent Uninstalls
---
As I talked about [earlier this week](http://www.tobiahmarks.com/2013/10/file-size/ "File Size, an important factor often overlooked"), to maximize your success you want to reduce your apps file size by as much as possible.

Apps with a smaller file are easier and faster for users to download, especially over 3g connections, and are much less likely to be uninstalled.

The question is, how can you do that? With the constant drive for new updates in the [Apps as a Service](http://www.tobiahmarks.com/2013/10/apps-service-product/ "Apps are a service, not a product") business model, it''s easy to get carried away adding new assets and SDKs.

Here are some ideas to help reduce the size of your app.

### Design your assets with file size in mind

When you design elements of your app, keep in mind what needs a unique asset, what could be generated on the fly, and what doesn''t need to be there at all.

Sure, that fancy menu border might look cool in the concept drawing, but would a simple beveled edge look almost as nice, and take up less texture files?

Small, repeatable textures can replace larger background image file. When you have a large asset, ask yourself, can you break it up into smaller elements? If so, perhaps you should use repeating textures instead.<figure id="attachment_1431" style="width: 300px" class="wp-caption alignright">

[<img class="size-medium wp-image-1431" alt="Using multiple background images has other advantages, such as parallax scrolling to create perception of depth." src="/assets/2013/10/parallax_scrolling_sample_1-300x140.jpg?resize=300%2C140" width="300" height="140" data-recalc-dims="1" />](https://i0.wp.com/en.wikipedia.org/wiki/File:TWW_parallax_scrolling_sample_1.jpg)<figcaption class="wp-caption-text">Using multiple background images has other advantages, such as <a title="Wikipedia Parallax Scrolling" href="http://en.wikipedia.org/wiki/Parallax_scrolling" target="_blank">parallax scrolling</a> to create perception of depth.</figcaption></figure> 

If your game has a huge image of a grassy plain, mountains, and a one little house on one of the mountains. Try instead making a repeatable texture for each element. The grass, the mountains, and then a tiny image for the house. If you break up the image into smaller pieces, then assemble them in code, you can make them look like a larger more detailed background without using any large asset files.

You can even recycle elements when creating new areas. For example, the desert zone can use the same mountain textures as the grassy plains. Not only will you use less file space, but you''ll also be able to create new content faster and cheaper!

### Generate assets dynamically

It makes sense an important button would be highlighted/look different from others. But does each kind of button need a unique image? Could you have a grey "template" button and in the code recolor it to create differentiation instead?

Background music for games can also be a huge hog of disk space. Yet, you don''t want the same 30 second loop to repeat over and over and drive players crazy. Try layering your music. Have various 30 to 60 second "base" loops (Ex. base/drums) and then randomly layer on 15 to 90 second "tunes" (Ex. guitar/sax/whatever melody) on top. That way, the player will hear a randomly generated "song" each time they play. It may have repeating elements, but the unique way it''s continuous streamed together will (hopefully) be good enough to keep the player''s interest and make them think the music tracks are longer than they actually are.

### Use sprite sheets where applicable<figure id="attachment_1421" style="width: 256px" class="wp-caption alignright">

[<img class="size-full wp-image-1421" alt="An example sprite sheet" src="/assets/2013/10/spritesheet.png?resize=256%2C192" width="256" height="192" data-recalc-dims="1" />](http://opengameart.org/content/bomb-party-expansion)<figcaption class="wp-caption-text">An example of a sprite sheet</figcaption></figure> 

A sprite sheet is a collection of sprites (aka, image assets) placed together into one larger image.

Why is this useful? A couple of reasons, but for our purposes, it''s because of powers of two.

Computers are binary, and file storage is all based on <a title="Wikipedia Power of Two" href="http://en.wikipedia.org/wiki/Power_of_two" target="_blank">powers of two</a>. 16, 32, 64, 128, 256, 512, 1024, etc. If an image is larger than a power of two, it uses up the same amount of space in memory as the next power of two. Try looking at an images properties, you''ll see two values. "Size" and "Size on Disk". An image that''s 130&#215;300 uses up the same amount of memory/size on disk as a 256&#215;512 image.

If you take your image assets and combine them into large sprite sheet, you will likely save on overall disk space. One 512&#215;512 or 1024&#215;1024 sprite sheet is big by itself, but could potentially be much smaller than the sum of its parts. This method does need more work on your part. You will have to write some extra code to render the sprite sheet, only using the appropriate region of the image for each asset/texture.

The rewards don''t just end with file size however. When done correctly, this will also save on the number of draw calls being made to render the scene, giving you better performance as well.

### Compress assets

Use the compression format that makes the most sense. JPGs are great for heavy compression, although they are notorious for <a title="Wikipedia Artifacting" href="http://en.wikipedia.org/wiki/Compression_artifact" target="_blank">artifacting</a>. PNGs are great for sprites, as they allow transparency, however make note if you''re using PNG-8 or PNG-24. PNG-8 allows for up to 256 different colors, and PNG-24 supports up to 16 million.

The question is, do you need all 16 million colors, or can you make your asset look nice using only 256? It isn''t wrong to use PNG-24 (or even PNG-32 if you need per pixel alpha transparency), just make sure you aren''t using them when a more compressed version would look just as nice.

Also, remember to <a title="PNGCrush" href="http://pmt.sourceforge.net/pngcrush/" target="_blank">crush them</a>.

### Remove junk code

It seems like every advertiser out there wants you to integrate their SDK. "Get set up in five minutes!" they''ll claim. Well, that''s right, but often you aren''t using 100% of the features they offer in their platforms. Most of the time in my experience, you just end up using one aspect of their framework.

Consider using ad mediation to reduce the number of SDKs you need to import.

Take the time to go through their SDK and look at what you really need. Can this be simplified? Can whole files and assets be removed if you''re not using them? Some times, some frameworks will bundle in whole SDKs you aren''t even using at all, can you remove them completely and still have your app run fine?

### Download new assets from web

I like to call this "Cheating"!

Sometimes I''ve downloaded a game under 25mb, then when I open it up it wants to download "Extra content" at each new area. Suddenly, it becomes a 100mb+ game on my device!

Don''t get me wrong, cheating is a good thing! Well, at least, it isn''t a horrible idea. Allow players to download and do something with a small download, then if you can''t live without those extra assets, make the player download them before going to new areas. If the player hasn''t unlocked or doesn''t want to visit the Jungle world, don''t download those assets. This allows the player to get going faster, and the app size to scale with the content they''re actually using rather that every potential place they could go to.

However, there is a major problem to this. It requires an internet connection to unlock new content. This could cause horrible player experiences if they don''t want to use up their 3g bandwidth bill, or don''t have access to WiFi. When a players forced to download something and they can''t or won''t, they may rate the game poorly due to "Lack of content".

I would only recommend doing this if it''s completely optional game content, or if your game already requires an internet connection (like a multiplayer only title, or only download during an in app purchase).

### Remove temporary files

Speaking of downloading extra content from the web&#8230; When you''re done, clean up after yourself.

If you app is ever generating or downloading files (Save games, internal images/screenshots, extra data, etc), keep close track of them. Likely, your users will never notice or care until one day your apps ballooned to such a huge size it ends up first on the chopping block when they go to uninstall.

Pay attention to what files are necessary, and which can safely be removed. Have code to clean up temporary files, even if the app crashes/was suddenly closed last time it was used. While testing you may constantly install, uninstall, and reinstall your app again, but in the wild a user will likely only install your app once per device they use. You don''t want to accidentally bloat over time.

### What did I miss?

I hope this advice was helpful to some of you! I''m sure there are lots more tips and tricks out there for reducing file size. If you know one that I neglected to mention, please [send me a message](http://www.tobiahmarks.com/contact/ "Contact") or leave a comment here!

-Tobiah