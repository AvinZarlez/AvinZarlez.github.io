---
id: 35091
title: 'Intro to Git and GitHub Part 2: Publishing, cloning, and forking.'
date: 2014-08-29T06:00:07+00:00
author: Tobiah
excerpt: |
  This is a continuation of a tutorial blog series to learn the basics of Git, using GitHub and the GitHub client.
  
  To start from the beginning, go here: http://www.tobiahmarks.com/2014/08/intro-git-github-0/
  
  In this part, you will learn:
  Publish a new repository
  Push changes
  Clone an existing repository
  Fork an existing repository
  Pull requests
layout: post
guid: http://www.tobiahmarks.com/?p=35091
permalink: /2014/08/29/intro-git-github-2/
categories:
  - Tips and tricks
tags:
  - Git
---
This is a continuation of a tutorial blog series to learn the basics of Git, using GitHub and the GitHub client.

To start from the beginning, [go here](http://wp.me/p3X06x-8ZB).

### Publish a new repository

Time to put your project online!

GitHub makes it easy to share your code with others online!

To publish your local repository, click the "Publish Repository" button in the upper right hand corner.

[<img class="aligncenter size-full wp-image-35121" src="/assets/2014/08/Publish01.png?resize=660%2C396" alt="Publish01" width="660" height="396" srcset="/assets/2014/08/Publish01.png?w=1000 1000w, /assets/2014/08/Publish01.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Publish01.png)GitHub will give you some choices. If you want to release your source code for everyone to see, it''s free.

[<img class="aligncenter size-full wp-image-35161" src="/assets/2014/08/Publish02.png?resize=526%2C370" alt="Publish02" width="526" height="370" srcset="/assets/2014/08/Publish02.png?w=526 526w, /assets/2014/08/Publish02.png?resize=300%2C211 300w" sizes="(max-width: 526px) 100vw, 526px" data-recalc-dims="1" />](/assets/2014/08/Publish02.png)Click publish and in a moment your code will be online!

Once your project is linked to an online repository, the publish button will change to a "Sync" button.

[<img class="aligncenter size-full wp-image-35171" src="/assets/2014/08/Publish03.png?resize=64%2C28" alt="Publish03" width="64" height="28" data-recalc-dims="1" />](/assets/2014/08/Publish03.png)If you want to make sure you have the latest code from the web, click the button to see if you need to download any changes.

### Push changes

After you''ve made a new commit, the Sync button will show that your local repository is ahead of the current online one.

[<img class="aligncenter size-full wp-image-35181" src="/assets/2014/08/Publish04.png?resize=660%2C396" alt="Publish04" width="660" height="396" srcset="/assets/2014/08/Publish04.png?w=1000 1000w, /assets/2014/08/Publish04.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Publish04.png)To "Push" these changes to the server, just click the sync button!

Now you can reach the latest code for your projects from any computer with an internet connection.

### Clone an existing repository

To download an existing repository to your computer, you have to "Clone" it.

GitHub''s client makes it easy to clone any repository tied to your GitHub account. Click the new repository button, and hit the "Clone" tab.

[<img class="aligncenter size-full wp-image-35183" src="/assets/2014/08/Publish05.png?resize=566%2C570" alt="Publish05" width="566" height="570" srcset="/assets/2014/08/Publish05.png?w=566 566w, /assets/2014/08/Publish05.png?resize=150%2C150 150w, /assets/2014/08/Publish05.png?resize=298%2C300 298w" sizes="(max-width: 566px) 100vw, 566px" data-recalc-dims="1" />](/assets/2014/08/Publish05.png)Here you''ll see a list of all the repositories tied to my GitHub account. Highlighted is the MyFirstRepo repository I just uploaded.

You can get to other repositories by going to [GitHub.com](http://www.github.com/ "GitHub"). On the side of every public project page on GitHub, you''ll see these two buttons:

[<img class="aligncenter size-full wp-image-35201" src="/assets/2014/08/Publish06.png?resize=200%2C90" alt="Publish06" width="200" height="90" data-recalc-dims="1" />](/assets/2014/08/Publish06.png)If you just want to download the files, you can go for the zip. But if you would like to be able to look at past commits, and commit your own changes, click the "Clone in Desktop" button and GitHub will automatically request to open your GitHub client.

Choice a place to save the files in, and now you have your own copy of that repository on your local machine!

### Fork an existing repository

"Forking" is similar to cloning, but GitHub automatically links your new cloned repository to the original repository from which it came from.

Using your web browser on [GitHub](http://www.github.com/ "GitHub")&#8216;s website, there is a "Fork" button on the top right of project pages.

[<img class="aligncenter size-full wp-image-35211" src="/assets/2014/08/Publish07.png?resize=660%2C158" alt="Publish07" width="660" height="158" srcset="/assets/2014/08/Publish07.png?w=1089 1089w, /assets/2014/08/Publish07.png?resize=300%2C72 300w, /assets/2014/08/Publish07.png?resize=1024%2C245 1024w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Publish07.png)Forking a project adds a new repo to your account, which you can then clone to your local machine in GitHub''s client. You can make whatever changes you would like to your version of the repository, and it won''t affect the original.

Why would you want to do this? Because now you work on your own code and modifications without worrying about messing up someone else''s code (or their code messing with yours). Then when you''re ready, you can make a pull request to merge those changes back in.

### Pull requests

Let''s say you want to work on an open source project. You decide to add a new feature to make the project even better.

You could clone it and work on your own new repo, which you may or may not share with others. Instead, you should work on a fork of the original project.

Then when you''ve finished making your changes and want to push them back into the original project for others to use, you can make a new "Pull" request. GitHub has a system for this built right into the website.

You can add documentation of exactly what you added and why, and the repository owner can check all the changes before making them officially part of the original repository.

That''s how you can contribute to the projects of others, and that is one of the basis of how open sourced software is built! Now you too can be an open source developer.

## End of Part 2

[Click here](http://wp.me/p3X06x-8ZB) to return to the main blog post. [Part 3 will be posted on Monday](http://www.tobiahmarks.com/2014/09/intro-git-github-3/).

-Tobiah