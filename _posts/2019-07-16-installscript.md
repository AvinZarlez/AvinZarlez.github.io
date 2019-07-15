---
layout: post
title: "Automatic App Install Script"
date: 2019-07-16 12:00
category: 
author: Tobiah
tags: [chocolatey]
summary: ""
---

I like to reset my PC fairly frequently. My primary work machine I'll wipe every other month, though I'm usually a bit slower with personal machines I do less development on.

Either way, whenever my PC is feeling slow and/or I have the time, I like to reset things. This gives me a lot of advantages, such as:

### 1. Faster speed / load times

Removes all the junk!

As a developer, sometimes files can get a little untidy. Extra programs in the system PATH, various temp files that never got cleaned up, or just software I no longer need.

### 2. Forces good backup practices

I make sure nothing I care about is not stored in a way that is automatically backed up. If my systems are wiped suddenly, I will lose no data.

This is easier said than done, but if you wipe your system frequent it motivates you to be much stricter in your file storage practices. I hate having to repeat manual work, so my backups need to also be automatic and continous.

### 3. Updates software

Resetting my PC is a great time to make sure i'm using the latest versions of my drivers and favorite software.

### 4. Encourages automation!

As I mentioned in point 2, a lot of the reason people ***don't*** backup as often as they should is the manual work involved.

Luckily, technology can change that!

Installing software often took the most amount of time for me whenever I wiped my system. In part because all the clicking involved. When I reset windows, I can walk away for an hour or so and it's done. But when I want to install 10+ programs that don't happen to be on [ninite](https://ninite.com/)? That takes some time.

So, I decided to make myself a script!

## Tobiah's Automatic Install Script

<script src="https://gist.github.com/TobiahZ/b3c6a4acdb8f8a694ee3299439c492f3.js"></script>

Feel free to try it out for yourself next time you need to install a bunch of apps!

All you have to do is tweak the `$TobiahsPackages` list with the packages you want to install.
You can find a list of available chocolatey packages on https://chocolatey.org/packages

If you use the script, or if you have any comments/questions/feature requests, let me know!
-Tobiah
