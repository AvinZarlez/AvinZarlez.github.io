---
id: 35251
title: 'Intro to Git and GitHub Part 3: Branching'
date: 2014-09-01T06:30:05+00:00
author: DEADNAME
excerpt: |
  This is a continuation of a tutorial blog series to learn the basics of Git, using GitHub and the GitHub client.
  
  To start from the beginning, go here: http://www.OLDURL/2014/08/intro-git-github-0/
  
  In this part, you will learn:
  What is branching?
  Create a branch
  Switch between branches
  Deleting branch
layout: post
guid: http://www.OLDURL/?p=35251
permalink: /2014/09/01/intro-git-github-3/
categories:
  - Tips and tricks
tags:
  - Branching
  - Git
---
This is a continuation of a tutorial blog series to learn the basics of Git, using GitHub and the GitHub client.

To start from the beginning, [go here](http://wp.me/p3X06x-8ZB).

Now we start to touch on stuff that is a bit more complicated. There is a lot more you can do with branches, this tutorial will serve as an introduction to the concept.

### What is branching?

When you make commits on git, you end up with a series of snapshots of the code in various states. What if you wanted keep the code in different states, without having to copy/paste into two different repositories?

For instance, you might have your 1.0 release version, and another 1.1 version for your in-progress new feature update.

What if while you are developing your 1.1 code, somebody finds a major bug that you need to fix from your 1.0 version right away? The new feature you are working on isn''t finished yet, but you don''t need to discard and revert all your hard work to get access to the 1.0 code. Instead, set up a new branch for your release and in-progress code.

What if you have a master version of your code, and you just want to mess around and change things just for testing? You want to be able to commit your work and save what you''ve been doing, but don''t want to mess up your master. You should not afraid to commit test changes because you would then have to revert them back later. Just make a new test branch instead that will not effect your master branch.

Branching allows you to organize your commits and keep track of multiple versions of your code.

This may sound weird at first, but it gets simpler once you see it in action.

### Create a branch

By default, all git projects have a "master" branch. There is a drop down box that says "master" on top of your commit log. Click it to expand the drop down menu to view all your current branches.

[<img class="aligncenter size-full wp-image-35261" src="/assets/2014/08/Branching01.png?resize=660%2C396" alt="Branching01" width="660" height="396" srcset="/assets/2014/08/Branching01.png?w=1000 1000w, /assets/2014/08/Branching01.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Branching01.png)To see more options, click the manage button on the right of the branches drop down.

[<img class="aligncenter size-full wp-image-35271" src="/assets/2014/08/Branching02.png?resize=660%2C396" alt="Branching02" width="660" height="396" srcset="/assets/2014/08/Branching02.png?w=1000 1000w, /assets/2014/08/Branching02.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Branching02.png)Since we only have one branch, not much is going on in this screen right now.

To make a new branch, go back to your main project screen. The text box should say "Filter or create new". Type the name of the new branch you want.

[<img class="aligncenter size-full wp-image-35281" src="/assets/2014/08/Branching03.png?resize=320%2C158" alt="Branching03" width="320" height="158" srcset="/assets/2014/08/Branching03.png?w=320 320w, /assets/2014/08/Branching03.png?resize=300%2C148 300w" sizes="(max-width: 320px) 100vw, 320px" data-recalc-dims="1" />](/assets/2014/08/Branching03.png)Now you have two branches. "master", and "feature1"!

### Switch between branches

To switch between, click on the drop down menu again.

[<img class="aligncenter size-full wp-image-35301" src="/assets/2014/08/Branching04.png?resize=320%2C180" alt="Branching04" width="320" height="180" srcset="/assets/2014/08/Branching04.png?w=320 320w, /assets/2014/08/Branching04.png?resize=300%2C169 300w" sizes="(max-width: 320px) 100vw, 320px" data-recalc-dims="1" />](/assets/2014/08/Branching04.png)Try selecting "feature1" and make a new commit.

[<img class="aligncenter size-full wp-image-35321" src="/assets/2014/08/Branching05.png?resize=660%2C396" alt="Branching05" width="660" height="396" srcset="/assets/2014/08/Branching05.png?w=1000 1000w, /assets/2014/08/Branching05.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Branching05.png)Now switch back to "master" branch. You''ll see that your new commit disappears. If you check your folder, the files are automatically changed. When you''re ready to work on your new feature again, select the branch again and you can continue working.

### Deleting branch

To delete a branch, you''ll need to go to your branch manager again. To get there, click the branches drop down menu again and hit the manage button on the top right.

[<img class="aligncenter size-full wp-image-35331" src="/assets/2014/08/Branching06.png?resize=660%2C396" alt="Branching06" width="660" height="396" srcset="/assets/2014/08/Branching06.png?w=1000 1000w, /assets/2014/08/Branching06.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Branching06.png)You can''t delete the current branch you have "checked out" (the one you have open). Other branches appear below, simply click the trash can to delete them.

## End of Part 3

[Click here](http://wp.me/p3X06x-8ZB) to return to the main blog post. [Part 4 will be posted on Friday](http://www.OLDURL/2014/09/intro-git-github-4/).

-DEADNAME