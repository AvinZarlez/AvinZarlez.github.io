---
id: 34571
title: Intro to Git and GitHub
date: 2014-08-25T12:00:35+00:00
author: Tobiah
excerpt: |
  This tutorial will teach you the basics of Git, using GitHub and the GitHub client.
  
  Experience required: None.
  This is written for people who have never used any kind of version control system before.
  
  What will you learn:
  
  Part 0: Introduction/Setup
  What is Git
  Why use version control?
  What is GitHub?
  Setting up the GitHub client
  
  Part 1: Your first repository
  Creating a new local repository
  Committing changes
  Discarding changes
  Renaming an deleting files
  Reverting changes
  Ignoring files
  
  Part 2: Publishing, cloning, and forking using the GitHub client.
  Publish a new repository
  Push changes
  Clone an existing repository
  Fork an existing repository
  Pull requests
  
  Part 3: Introduction to Branching.
  What is branching?
  Create a branch
  Switch between branches
  Deleting branch
  
  Part 4: Merging and Rebasing overview.
  Merging branches
  Resolving conflicts
  Undoing a merge
  Rebasing
  When should you merge and when should you rebase?
  
  Each part will be a different post. For now, let's dive into part 0.
layout: post
guid: http://www.tobiahmarks.com/?p=34571
permalink: /2014/08/25/intro-git-github-0/
categories:
  - Tips and tricks
tags:
  - Git
---
This tutorial will teach you the basics of Git, using <a href="https://github.com/" target="_blank">GitHub </a>and the <a href="https://windows.github.com/" target="_blank">GitHub client</a>.

### Experience required:

None. This is written for people who have never used any kind of version control system before.

### What will you learn:

[<img class="alignright size-medium wp-image-34871" src="/assets/2014/08/Octocat-300x249.png?resize=300%2C249" alt="Octocat" width="300" height="249" srcset="/assets/2014/08/Octocat.png?resize=300%2C249 300w, /assets/2014/08/Octocat.png?w=800 800w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />](https://github.com/)
  
**Part 0: Introduction and Setup
  
** 

  * What is Git
  * Why use version control?
  * What is GitHub?
  * Setting up the GitHub client

**Part 1: Your first repository**

  * Creating a new local repository
  * Committing changes
  * Discarding changes
  * Renaming an deleting files
  * Reverting changes
  * Ignoring files

**Part 2: Publishing, cloning, and forking using the GitHub client.**

  * Publish a new repository
  * Push changes
  * Clone an existing repository
  * Fork an existing repository
  * Pull requests

**Part 3: Introduction to Branching.**

  * What is branching?
  * Create a branch
  * Switch between branches
  * Deleting branch

**Part 4: Merging and Rebasing overview.**

  * Merging branches
  * Resolving conflicts
  * Undoing a merge
  * Rebasing
  * When should you merge and when should you rebase?

Each part will be a different post. For now, let''s dive into part 0.

# Part 0: **Introduction and Setup**

## What is Git?

Git is a distributed revision control system created by Linus Torvalds.

Since its creation in 2005, Git has quickly become one of the most widely used version control and source code management systems.

## Why use version control?

Have you ever accidentally deleted an important file? Had a computer crash and lost work?

Do you manually zip and/or copy/paste your important files to keep backups?

Have you ever tried changing something in your code, only to accidentally mess everything up and not remember what you did to break it?

With version control, you can not only have a back up, but have a detailed history of all the important milestones of your project. You can also share your work with others, and have multiple coders work on the same project at the same time.

## How much does it cost?

Git itself is free! There are various hosting services out there that have different pricing models. For this lesson, we''ll be using GitHub.

## What is GitHub?

<a href="https://github.com/" target="_blank">GitHub </a>is a hosting service for Git repositories. Don''t be confused by the similar name, Git and GitHub are completely different things. You can use Git with a variety of software packages and services. GitHub is just one of the most popular sites for open source projects.

GitHub (the website) is free for an unlimited number of users, and an unlimited number of open sourced repositories. However, they charge a monthly fee for private (not viewable by the public) repositories.

## What is open source?

Open source means everyone can see, and download the code for your projects. This allows others to check out, learn from or even contribute to your work. There are a lot of open source software projects that are created and maintained by various members of the community, including Git itself!

## Where else can I host git repos?

There are a lot of different git hosts out there. I would recommend checking out the following:

#### Visual Studio Online

Website: <a href="http://www.visualstudio.com/products/visual-studio-online-user-plans-vs" target="_blank">http://www.visualstudio.com/products/visual-studio-online-user-plans-vs</a>
  
Cost: Unlimited projects and private repositories for up to 5 users. Charge for additional users.

#### BitBucket

Website: <a href="https://bitbucket.org/" target="_blank">https://bitbucket.org/</a>
  
Cost: Unlimited projects and private repositories for up to 5 users.

## Do I have to use the GitHub client to use GitHub!

No you do not!

You can use any Git client to connect to GitHub. Many people control Git through text base commands, but I think it''s a lot easier to use a GUI tool.

There are other, more advanced clients you can use like <a title="Git Extensions" href="http://sourceforge.net/projects/gitextensions/" target="_blank">Git Extensions</a> or <a title="SourceTree" href="http://www.sourcetreeapp.com/" target="_blank">SourceTree</a>. GitHub''s client very simple and bare bones, which I think is nice when you''re first learning, and why I chose it for this tutorial.

## Setting up the GitHub Client:

### Download GitHub Client

You can download the GitHub for Windows client by going to <a href="http://windows.github.com/" target="_blank">http://windows.github.com/</a>

### Create Account

To create an account for GitHub, go to <a href="https://github.com/join" target="_blank">https://github.com/join</a>

Once you get your account set up, you can start the GitHub client on your computer and log in.

### Configure settings

You will be given the option to set the name and email address you would like to have tied to your commits. Use an email address you don''t mind others seeing, as this information will be public!

If you are worried about spam, or simply don''t want your email address to be publicly listed, GitHub provides a private email address. Simply set your email address to "_username@users.noreply.github.com_" where _username_ is your GitHub username.

For more information, follow the instructions here: <a href="https://help.github.com/articles/keeping-your-email-address-private" target="_blank">https://help.github.com/articles/keeping-your-email-address-private</a>

## To be continued

On Wednesday, look for [Part 1: Your first repository](http://www.tobiahmarks.com/2014/08/intro-git-github-1/)!

-Tobiah