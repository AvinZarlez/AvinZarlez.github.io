---
id: 35391
title: 'Intro to Git and GitHub Part 4: Merging and Rebasing overview'
date: 2014-09-05T00:20:45+00:00
author: Tobiah
excerpt: |
  This is a continuation of a tutorial blog series to learn the basics of Git, using GitHub and the GitHub client.
  
  To start from the beginning, go here: http://www.tobiahmarks.com/2014/08/intro-git-github-0/
  
  In this part, you will learn:
  Merging branches
  Resolving conflicts
  Undoing a merge
  Rebasing
  When should you merge and when should you rebase?
layout: post
guid: http://www.tobiahmarks.com/?p=35391
permalink: /2014/09/05/intro-git-github-4/
categories:
  - Tips and tricks
tags:
  - Git
---
This is a continuation of a tutorial blog series to learn the basics of Git, using GitHub and the GitHub client.

To start from the beginning, [go here](http://wp.me/p3X06x-8ZB).

Now that you''ve made multiple branches, it''s time to learn how to put them back together!

### Merging branches

To merge our "feature1" branch from [part 3](http://www.tobiahmarks.com/2014/09/intro-git-github-3/) back into our master branch, go back to your branch manager. To get there, click the branches drop down and hit manage.

[<img class="aligncenter size-full wp-image-35461" src="/assets/2014/08/Merging01.png?resize=660%2C396" alt="Merging01" width="660" height="396" srcset="/assets/2014/08/Merging01.png?w=1000 1000w, /assets/2014/08/Merging01.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Merging01.png)Drag the "feature1" into the blank box on the left under "Merge", and "master" onto the blank box on the right.

That will tell the GitHub client to merge the commits from "feature1" into the branch of "master". You can confirm that you''ve done this right (as opposed to the other way around) if the blue box on the far right also says "master".

Click the merge button, and because there were no conflicts "master" now matches "feature1".

### Viewing branch graph

For this tutorial, I''ve been trying to stay away from doing shell commands. But, when it comes to merging, it eventually becomes unavoidable to use some text based commands.

To open the shell, click Settings->Open in Git Shell.

[<img class="aligncenter size-full wp-image-35471" src="/assets/2014/08/Merging02.png?resize=220%2C256" alt="Merging02" width="220" height="256" data-recalc-dims="1" />](/assets/2014/08/Merging02.png)I won''t go over all the basic commands here, but in the shell you can do everything we''ve done so far in the GitHub client and more, with more options.

Specifically when dealing with multiple branches, viewing a graph may be useful. Try typing in this line:

<p style="padding-left: 30px;">
  <code>git log --graph --oneline --all --decorate</code>
</p>

As an example, I made another new branch called "feature2". In both "feature1" and "feature2" branches I made new commits.

When I open the Shell and run the above command, I get this useful graph:

[<img class="aligncenter size-full wp-image-35481" src="/assets/2014/08/Merging03.png?resize=534%2C264" alt="Merging03" width="534" height="264" srcset="/assets/2014/08/Merging03.png?w=534 534w, /assets/2014/08/Merging03.png?resize=300%2C148 300w" sizes="(max-width: 534px) 100vw, 534px" data-recalc-dims="1" />](/assets/2014/08/Merging03.png)It may be ASCII art, but you can see the relationship between on the branches.

"HEAD" is the current branch. "origin/master" and "origin/HEAD" are the remote (aka "origin") branches on GitHub. If we published the "feature1" or "feature2" branches, another "origin/feature1" or "origin/feature2" tag would also appear for the remote versions of those branches.

### Resolving conflicts

As amazing and useful as Git is, sometimes things don''t always go as planned.

Let''s take our current project. We''ve been working on two different branches, one improving feature 1 and another creating a feature 2. However, they both have been working on `Features.txt`

First, let''s merge "feature1" with "master".

[<img class="aligncenter size-full wp-image-35491" src="/assets/2014/08/Merging04.png?resize=660%2C396" alt="Merging04" width="660" height="396" srcset="/assets/2014/08/Merging04.png?w=1000 1000w, /assets/2014/08/Merging04.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Merging04.png)So far so good. But, what happens when we try to then merge "feature2" with "master"?

[<img class="aligncenter size-full wp-image-35501" src="/assets/2014/08/Merging05.png?resize=660%2C396" alt="Merging05" width="660" height="396" srcset="/assets/2014/08/Merging05.png?w=1000 1000w, /assets/2014/08/Merging05.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Merging05.png)Things don''t go quite as smoothly&#8230;

[<img class="aligncenter size-full wp-image-35511" src="/assets/2014/08/Merging06.png?resize=660%2C396" alt="Merging06" width="660" height="396" srcset="/assets/2014/08/Merging06.png?w=1000 1000w, /assets/2014/08/Merging06.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Merging06.png)It''s time to break out the Git Shell again.

Our project now exists in a semi limbo state mid-merge.

If we wanted to give up and abort this merge, we can stop it by typing:

<p style="padding-left: 30px;">
  <code>git merge --abort</code>
</p>

We don''t need to abort it though, let''s try to fix it instead. Use the diff command to see where the conflict is.

<p style="padding-left: 30px;">
  <code>git diff</code>
</p>

[<img class="aligncenter size-full wp-image-35521" src="/assets/2014/08/Merging07.png?resize=534%2C312" alt="Merging07" width="534" height="312" srcset="/assets/2014/08/Merging07.png?w=534 534w, /assets/2014/08/Merging07.png?resize=300%2C175 300w" sizes="(max-width: 534px) 100vw, 534px" data-recalc-dims="1" />](/assets/2014/08/Merging07.png)Yep, we know the exact problem. You can see the "feature1" and "feature2" versions are at odds at each other.

It''s here you could use something like `git mergetool` to help resolve these conflicts and chose which lines from branch A and which from branch B to use. But since this is simple, we will go in manually and fix it.

Let''s open up `Features.txt`.

[<img class="aligncenter size-full wp-image-35531" src="/assets/2014/08/Merging08.png?resize=340%2C172" alt="Merging08" width="340" height="172" srcset="/assets/2014/08/Merging08.png?w=340 340w, /assets/2014/08/Merging08.png?resize=300%2C152 300w" sizes="(max-width: 340px) 100vw, 340px" data-recalc-dims="1" />](/assets/2014/08/Merging08.png)Git has added at each conflict, the <<<<<<<, =======, and >>>>>>>. The first part represents the "HEAD"/"master" branch, and the second part after the equals signs represents the "feature2" branch.

We want to manually mix the two files together.

[<img class="aligncenter size-full wp-image-35541" src="/assets/2014/08/Merging09.png?resize=340%2C172" alt="Merging09" width="340" height="172" srcset="/assets/2014/08/Merging09.png?w=340 340w, /assets/2014/08/Merging09.png?resize=300%2C152 300w" sizes="(max-width: 340px) 100vw, 340px" data-recalc-dims="1" />](/assets/2014/08/Merging09.png)Now let''s go back to git. We now have to add all the conflicted files again to the project and commit. To see which files are or are not part of a current commit, we can use `git status`

[<img class="aligncenter size-full wp-image-35561" src="/assets/2014/08/Merging10.png?resize=534%2C300" alt="Merging10" width="534" height="300" srcset="/assets/2014/08/Merging10.png?w=534 534w, /assets/2014/08/Merging10.png?resize=300%2C169 300w" sizes="(max-width: 534px) 100vw, 534px" data-recalc-dims="1" />](/assets/2014/08/Merging10.png)We see that Features.txt is not resolved. We fixed it already, now we need to tell git. As the message says, we just need to type `git add Features.txt` and then `git commit` to finalize the merge.

[<img class="aligncenter size-full wp-image-35571" src="/assets/2014/08/Merging11.png?resize=569%2C120" alt="Merging11" width="569" height="120" srcset="/assets/2014/08/Merging11.png?w=569 569w, /assets/2014/08/Merging11.png?resize=300%2C63 300w" sizes="(max-width: 569px) 100vw, 569px" data-recalc-dims="1" />](/assets/2014/08/Merging11.png)Now if we look in the GitHub client, we see our merge has gone through.

[<img class="aligncenter size-full wp-image-35581" src="/assets/2014/08/Merging12.png?resize=660%2C396" alt="Merging12" width="660" height="396" srcset="/assets/2014/08/Merging12.png?w=1000 1000w, /assets/2014/08/Merging12.png?resize=300%2C180 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2014/08/Merging12.png)

### Undoing an merge

If we aren''t happy with this merge, we can always revert as we learned in part 1. You can also revert by going back to the git shell and typing:

`git reset --soft HEAD~1`

The `git reset` reverts us back to an earlier commit. The "`--soft`" option means that instead of discarding the changes, it puts them back into our workspace for us to edit. `HEAD~1` means we are reverting to the last commit (The current one being `HEAD`, so the one right before `HEAD` is `HEAD~1`)

That would undo the merge, or whatever the last commit just did. Since our "feature2" branch hasn''t changed, we can always merge again if desired.

### Rebasing

Instead of merging, git also has "rebasing".

Rebasing takes a branch and integrates all its commits into another branch.

Functionally, it acts very similar to merging. You have to use it from the git shell. Instead of `git merge <branch>`, you do `git rebase` 

### When should you merge and when should you rebase?

At first merging and rebasing might seem to give you the same result. The code gets all mashed together! But, there is a key difference between the two.

Merging takes all the changes in one branch, then in one commit applies those differences into another branch.

Rebasing says I want to take all the commits in my current branch, and change the "base" at when the branch initially started at.

So when would you want to use one vs. the other?

#### You might want to merge when&#8230;

You made a branch for a new feature. After you''ve coded it and bug tested the feature and ready to bring it into your main code, you probably want to merge.

In this case, you don''t care about maintaining all the interim commits, but simply want the final product of that branch.

#### You might want to rebase when&#8230;

You were developing in branch A, and another developer working from branch B wants to integrate their work with yours.

In this case, you want to preserve all the interim commit steps and documentation they have been working on. By rebasing, you get not just the final code but all the steps that the developer took as if they had also been working on branch A the whole time.

## End of Part 4

[Click here](http://wp.me/p3X06x-8ZB) to return to the main blog post.

# Summary

You now know how to use Git and GitHub to create and maintain repositories!

You should try making Git repos for all your software projects. Remember to commit changes early and often, and write good descriptions! This small extra step will eventually save you hours of headache when something eventually goes wrong. In addition to allowing you to more collaborate and share your work with others.

For further learning, here is a fun interactive Git lesson that teaches you a lot of different more advanced git concepts: <http://pcottle.github.io/learnGitBranching/>

I hope you enjoyed this intro to Git and GitHub blog series! If you have trouble understanding anything, or think I left something out, [please let me know](http://www.tobiahmarks.com/contact/ "Contact").

Thanks for reading!

-Tobiah