---
id: 103811
title: Visual Studio Code Ultimate Starter Guide (UPDATED 9/11/2015)
date: 2015-05-18T08:30:11+00:00
author: Tobiah
excerpt: |
  During Build, Microsoft released a brand new code editor called "Visual Studio Code"!
  
  In this post I will go over what it is, what it isn't, and how you can use it with your Unity and/or Corona projects.
  
  What is Visual Studio Code?
  
  Visual Studio Code (or "VSCode") is a new, cross platform lightweight coding editor.
  It is not a stripped down version of Visual Studio, nor is it comparable to "Visual Studio Express". This is a wholly new editor designed from the ground up to give a focused streamlined experience.
  Sometimes, you don't need a full featured IDE. A lot of the time all you need is something to edit files with IntelliSense/Syntax highlighting and maybe some debugging.
  I would often use Sublime side by side with Visual Studio. Sublime is a great solution, but Visual Studio Code is a new competitor on the block. It have many of the features and characteristics I like most from Sublime (plus a couple more), and it's $70 cheaper (a.k.a. FREE!)
  
  What to learn more? Click on the link below!
layout: post
guid: http://www.tobiahmarks.com/?p=103811
permalink: /2015/05/18/visual-studio-code/
image: /assets/2015/05/VisualStudioCodeCrossPlatform-825x510.png
categories:
  - Tools
tags:
  - CoronaSDK
  - Unity
  - Visual Studio Code
---
Microsoft has a brand new code editor called " Visual Studio Code "!

In this post I will go over what it is, what it isn''t, and how you can use it with your Unity and/or Corona projects.

## Updated 9/11/2015

Added new features from 0.8.0

You can read the full feature changes of 0.8.0, as well as all previous versions of Visual Studio Code, from the [update page](https://code.visualstudio.com/updates).

# What is Visual Studio Code?

Visual Studio Code (or "VSCode") is a new, cross platform lightweight coding editor launched during Microsoft''s Build 2015 conference.

It is not a stripped down version of Visual Studio, nor is it comparable to "Visual Studio Express". This is a new editor designed from the ground up to give a focused streamlined experience.

Sometimes, you don''t need a full featured IDE. A lot of the time all you need is something to edit files with IntelliSense/Syntax highlighting and maybe some debugging.

I would often use [Sublime](http://www.sublimetext.com/ "Sublime") side by side with Visual Studio. Sublime is a great solution, but Visual Studio Code is a new competitor on the block. It have many of the features and characteristics I like most from Sublime (plus a couple more), and it''s **$70 cheaper** (a.k.a. **_FREE_**!)

# How do I install Visual Studio Code?

Installing Visual Studio Code is an arduous process that requires at least 6 hours and a dedicated high speed internet connection.

&#8230;

**Just kidding!** It''s extremely simple and easy.
  
<!--more-->


  
All you have to do is go to [http://code.visualstudio.com/](http://code.visualstudio.com/ "Visual Studio Code") and download the app for your platform of choice!

[<img class="aligncenter size-full wp-image-103801" src="/assets/2015/05/VisualStudioCodeInstall.png?resize=330%2C370" alt="Installing Visual Studio Code" width="330" height="370" srcset="/assets/2015/05/VisualStudioCodeInstall.png?w=330 330w, /assets/2015/05/VisualStudioCodeInstall.png?resize=268%2C300 268w" sizes="(max-width: 330px) 100vw, 330px" data-recalc-dims="1" />](http://code.visualstudio.com/)

### Windows Set Up

Simply run the installation file and wait a few moments.

You can start Visual Studio Code from the created shortcuts, or simply type `code .` in the console/command prompt to open it to that folder.

### Mac OS Set Up

Open the zip, and drag Visual Studio Code.app to the Applications folder.

From there, you can open it from the launchpad. Or, if you''d like to be able to open VSCode from the terminal, append the following to your `~/.bash_profile` file:

<pre class="toolbar: false">code () {
    code () { VSCODE_CWD="$PWD" open -n -b "com.microsoft.VSCode" --args $* ;}
}
</pre>

### Linux Set Up

Yes, VSCode works on Linux as well! Just extract the zip into the folder you''d like and double-click on `Code` to run.

If you''d like to be able to open VSCode from the terminal, create the following link substituting `/path/to/vscode/Code` with the absolute path to the Code executable:

<pre class="toolbar: false">sudo ln -s /path/to/vscode/Code /usr/local/bin/code
</pre>

## Wait, that''s it?

That''s all you need to do. Seriously!

Depending on what you want to do though, you may also want to consider checking out the following Microsoft recommended tools:

  * [ASP.NET 5](https://github.com/aspnet/home) - a lean and composable framework for building web and cloud applications, fully open source and available on GitHub
  * [Node.js (incudes NPM)](http://nodejs.org/) - a platform for easily building fast, scalable network applications
  * [git](http://git-scm.com/download) - VS Code has built in support for source code control using git
  * [Yeoman](http://yeoman.io/) - an application scaffolding tool, you can think of this as File | New Project for VS Code
  * [generator-aspnet](https://www.npmjs.com/package/generator-aspnet) - a yeoman generator for scaffolding ASP.NET 5 applications, run npm install -g generator-aspnet to install
  * [hottowel](https://github.com/johnpapa/generator-hottowel) - a yeoman generator for quickly creating AngularJS applications, run npm install -g generator-hottowel to install
  * [Express](http://expressjs.com/) - an application framework for Node.js applications, uses the Jade template engine
  * [gulp](http://gulpjs.com/) - a streaming task runner system, integrates with VS Code tasks
  * [mocha](http://mochajs.org/) - a JavaScript test framework that runs on Node.js
  * [bower](http://bower.io/) - a client side package manager
  * [TypeScript](http://typescriptlang.org/) - brings structure and strong typing to your JavaScript code, without compromising the good parts
  * [TypeScript definition manager](http://definitelytyped.org/tsd/) - search and download 100''s of TypeScript definition files for popular JavaScript frameworks, providing great IntelliSense in VS Code

# How do I use Visual Studio Code?

When you open Visual Studio Code, you immediately get an editor window. There are no project files to open, no "File->New->(List of options here)", just straight up ready to type and get to work.

<img class="aligncenter size-full wp-image-103831" src="/assets/2015/05/VisualStudioCode.png?resize=660%2C458" alt="Visual Studio Code when you first open it" width="660" height="458" srcset="/assets/2015/05/VisualStudioCode.png?w=960 960w, /assets/2015/05/VisualStudioCode.png?resize=300%2C208 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />

The Visual Studio Code UI is divided up into four areas:

  1. **Editor** - Where you write code
  2. **Sidebar** - Gives you info about what you''re working on, such as a file explorer
  3. **Statusbar** - This also has more information about your project, such as which language you''re writing.
  4. **Viewbar** - Icons on the far left that lets your change views

Instead of "Tabs", VSCode allows up to three visible editors at a time in one instance/window. Press `Ctrl + \` to split your editor, `Ctrl + (1/2/3)` to switch between them easily, and close them by pressing `Ctrl + W`.

For more information on the basics of Visual Studio Code, you can [read the official documentation](https://code.visualstudio.com/Docs/codebasics "Visual Studio Code Basics"). There they also have a [guide of the more advanced editing features](https://code.visualstudio.com/Docs/editingevolved "Visual Studio Code Editing Evolved"), using [Git version control](https://code.visualstudio.com/Docs/versioncontrol "Visual Studio Code version control") within the program, and [debugging](https://code.visualstudio.com/Docs/debugging "Visual Studio Code Debugging").

Currently debugging only supports Node.js (JavaScript and TypeScript), with experimental support for Mono (C# and F#) on OS X and Linux.

# I''m coming from Sublime, are the keyboard shortcuts different?

You can see [all the keyboard shortcuts](https://code.visualstudio.com/Docs/customization "Visual Studio Code Keyboard Shortcuts") from the official documentation.

So far in my experience they are very similar. However, here are some notable differences:

  * **Move Line Down**: `Ctrl + Shift + Down` replaced with `Alt + Down`
  * **Move Line Up**: `Ctrl + Shift + Up` replaced with `Alt + Down`
  * **Split Editor**: `Alt + Shift + #` replaced with `Ctrl + #`, or `Ctrl + \`
  * **Jump parentheses**: `Ctrl + M` replaced with `Ctrl+Alt+J`
  * **Focus into next editor**: `Ctrl + PgUp` and `Ctrl + PgDn` replaced with `Ctrl + Alt + Left` and `Ctrl + Alt + Right`.
  * **Go to Symbol**: `Ctrl + R` replaced with `Ctrl + Shift + O`
  * **Toggle Block Comment**: `Ctrl + Shift + /` replaced with `Alt + Shift + A`
  * **Duplicate line(s)**: `Ctrl + Shift + D` replaced with `Alt + Shift + Down` - Also note, you can duplicate up by using `Alt + Shift + Up`!

Close matches:

  * **Select word**: You can replace `Ctrl + D` with `Ctrl + F2` (Selects all occurrences of selected word) OR `Ctrl + Shift + L` (Select all occurrences of current selection)
  * **Goto word in current file**: You can replace `Ctrl + ;` with `Ctrl + F` (Find)
  * **Quick-open files by name**: You can replace `Ctrl + P` with `Ctrl + Alt + O` (Open File)

Sadly not everything has a replacement. As of this writing these shortcuts have no equivalent I could find:
  
(Let me know if I''m wrong or things change in the future!)

  * **Select line**: `Ctrl + L`
  * **Select all contents of the current parentheses**: `Ctrl + Shift + M`
  * **Join line below to the end of the current line**: `Ctrl + J`
  * **Paste and indent**: `Ctrl + Shift + V`
  * **Soft Undo (jump to last change before undoing)**: `Ctrl + U`
  * **Wrap Selection in html tag**: `Alt + Shift + W`
  * **Transform to Uppercase**: `Ctrl + KU`
  * **Transform to Lowercase**: `Ctrl + KL`

# What about custom settings?

You can change your default settings file, or you can do so on a per-workspace basis.

For example, for my Unity projects I may include the following `settings.json` file in a `.vscode` folder:

<pre class="toolbar: false">// This setting files is for Unity projects.
// Place in your settings in this file to overwrite default and user settings.
{
    
    //-------- Search configuration --------

    // The folders to exclude when doing a full text search in the workspace.
    "search.excludeFolders": [
        ".git",
        "*.dll",
        "*.meta"
    ],
}
</pre>

That way .dll and .meta files will be excluded during my searches, but I didn''t have to change my overall settings if I wanted to be able to search dll''s in other projects.

> **Note**: The folder used to be \`.settings\`, but was changed to \`.vscode\` in 0.8.0 in order to not conflict with other editors that may use a folder called \`.settings\`. Don''t worry, once you update Visual Studio Code it will also automatically update your old folders to match.

# Can I use VSCode with Unity?

Absolutely!

There are two ways to work with Visual Studio Code and Unity, depending on which version you are using.

## Unity 5.2 and above and Visual Studio Code 0.8.0 and above

Unity development with Visual Studio Code has become even easier!

The quickest way to get started is by checking out [this awesome Unity plug-in](https://github.com/dotBunny/VSCode/) maintained by [@Reapazor](https://twitter.com/reapazor).

The plugin streamlines the following tasks:
  
- Sets VS Code as the default editor - opening a script now opens it in VS Code
  
- Configures Unity to pass file and line numbers and reuse the existing window - so VS Code opens in the correct context
  
- Scrubs the Unity project file to ensure that OmniSharp can work with it - to get the best editing experience
  
- Configures VS Code to ignore certain Unity file types - removing clutter from the VS Code file explorer
  
- Configures a launch.json file with the correct debug port - to enable debugging

> **NOTE**: Debugging is currently only supported for OS X. Windows does not support Mono debugging, and Microsoft has not tested the plug-in with Linux.

### Step One: Download the plugin

Open up a console and do a clone of the repo to get the plug-in source code.

&#8216;git clone https://github.com/dotBunny/VSCode.git''

### Step Two: Add the plug-in to your project

Go to the folder where you downloaded the plug-in source code and copy the &#8216;Plugins\Editor\dotBunny'' folder to your Unity project.

> **NOTE**: You may need to create a &#8216;Plugins'' folder under &#8216;Assets''

Next time you load your project in Unity, you will see a new set of options under the "Assets->VS Code" menu.

[<img src="/assets/2015/05/unity_plugin.png?resize=660%2C179" alt="Visual Studio Code Unity Plugin" width="660" height="179" class="aligncenter size-full wp-image-105911" srcset="/assets/2015/05/unity_plugin.png?w=986 986w, /assets/2015/05/unity_plugin.png?resize=300%2C82 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2015/05/unity_plugin.png)

Make sure to click "Enable Integration"!

### Step Three: Unity Intellisense

Then just open the root folder of your project in VS Code and you''re good to go!

From there, it should automatically detect your Unity project solution file. You can double-check this by looking for the flame icon in your status bar.

If it detects more than one project file, make sure you chose the **-csharp** solution (.sln) file.

If you want more instructions or options, check out the [Visual Studio Code with Unity documentation](https://code.visualstudio.com/Docs/runtimes/unity).

## Unity 5.1 and below or Visual Studio Code 0.7.x and below

These are the old instructions if you are using Visual Studio Code before version 0.8.0, and Unity before 5.2 (before Visual Studio Community became the default editor).

For reference, I''ve left these instructions here. However, I would not recommend following them. You really ought to update and use the later versions! Both Visual Studio Code and Unity are much better. If for some reason you can''t, or won''t, read on:

### Step One: Sync MonoDevelopProject

<img class="aligncenter size-full wp-image-103841" src="/assets/2015/05/SyncMonoDevelopProject.png?resize=473%2C419" alt="Sync MonoDevelop Project Unity" width="473" height="419" srcset="/assets/2015/05/SyncMonoDevelopProject.png?w=473 473w, /assets/2015/05/SyncMonoDevelopProject.png?resize=300%2C266 300w" sizes="(max-width: 473px) 100vw, 473px" data-recalc-dims="1" />

First, make sure you click "Sync MonoDevelop Project" to update your project file. This _should_ be done automatically, but sometimes is not so it''s always good to force a sync.

### Step Two: Set External Script Editor

Now we need to tell Unity to open Visual Studio Code (as opposed to MonoDevelop, Visual Studio, Sublime, or some other editor)

Here is how to do so with Windows.

First, go to Preferences:

<img class="aligncenter size-full wp-image-103851" src="/assets/2015/05/UnityPreferences.png?resize=465%2C587" alt="Unity Preferences" width="465" height="587" srcset="/assets/2015/05/UnityPreferences.png?w=465 465w, /assets/2015/05/UnityPreferences.png?resize=238%2C300 238w" sizes="(max-width: 465px) 100vw, 465px" data-recalc-dims="1" />

Then go to `External Tools` and click the `External Script Editor` dropdown:

<img class="aligncenter size-full wp-image-103881" src="/assets/2015/05/UnityPreferencesExternalToolBrowse.png?resize=516%2C439" alt="Unity Preferences External Script Editor" width="516" height="439" srcset="/assets/2015/05/UnityPreferencesExternalToolBrowse.png?w=516 516w, /assets/2015/05/UnityPreferencesExternalToolBrowse.png?resize=300%2C255 300w" sizes="(max-width: 516px) 100vw, 516px" data-recalc-dims="1" />

Click browse, and make your way to the following folder:

> C:\Users\ <your profile> \AppData\Local\Code\Bin

In there, VS Code automatically made a file called `code.cmd` that opens the editor. Select it!

<img class="aligncenter size-full wp-image-103891" src="/assets/2015/05/UnityPreferencesExternalToolVisualStudioCode.png?resize=516%2C439" alt="Unity Preferences External Script Editor Visual Studio Code" width="516" height="439" srcset="/assets/2015/05/UnityPreferencesExternalToolVisualStudioCode.png?w=516 516w, /assets/2015/05/UnityPreferencesExternalToolVisualStudioCode.png?resize=300%2C255 300w" sizes="(max-width: 516px) 100vw, 516px" data-recalc-dims="1" />

### Step Three: Unity Intellisense

Within Visual Studio Code, all you have to do is hit "Open Folder" and chose the root folder of your Unity project.

From there, it should automatically detect your Unity project solution file. You can double-check this by looking for the flame icon in your status bar.

If it detects more than one project file, make sure you chose the **-csharp** solution (.sln) file.

# Can I use VSCode with CoronaSDK or CoronaCards?

Even fewer steps than working with Unity!

Unlike Visual Studio, VS Code has Lua syntax coloring and bracket matching right out of the box.

<img class="aligncenter size-full wp-image-103901" src="/assets/2015/05/VisualStudioCodeLua.png?resize=660%2C308" alt="Visual Studio Code Lua" width="660" height="308" srcset="/assets/2015/05/VisualStudioCodeLua.png?w=1107 1107w, /assets/2015/05/VisualStudioCodeLua.png?resize=300%2C140 300w, /assets/2015/05/VisualStudioCodeLua.png?resize=1024%2C478 1024w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />

To work with a CoronaSDK project, simply open up the folder as your workspace!

[<img class="aligncenter size-full wp-image-103911" src="/assets/2015/05/VisualStudioCodeCoronaSDK.png?resize=660%2C418" alt="Visual Studio Code Corona with simulator" width="660" height="418" srcset="/assets/2015/05/VisualStudioCodeCoronaSDK.png?w=1574 1574w, /assets/2015/05/VisualStudioCodeCoronaSDK.png?resize=300%2C190 300w, /assets/2015/05/VisualStudioCodeCoronaSDK.png?resize=1024%2C649 1024w, /assets/2015/05/VisualStudioCodeCoronaSDK.png?w=1320 1320w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](https://twitter.com/TobiahMarks/status/598929572449517568)

This works really well with CoronaCards, since CoronaCards is a Visual Studio project with a CoronaSDK project within.

<img class="aligncenter size-full wp-image-103921" src="/assets/2015/05/VisualStudioCodeCorona.png?resize=660%2C292" alt="Visual Studio Code CoronaCards" width="660" height="292" srcset="/assets/2015/05/VisualStudioCodeCorona.png?w=1365 1365w, /assets/2015/05/VisualStudioCodeCorona.png?resize=300%2C133 300w, /assets/2015/05/VisualStudioCodeCorona.png?resize=1024%2C452 1024w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />

You can work with your Lua and C# code side by side, all nicely syntax colored!

# What about (insert language here)?

VSCode supports a bunch of different languages, and more coming soon!

For full details, read the [official documentation](https://code.visualstudio.com/Docs/languages "VSCode Languages").

# Wait, you didn''t cover (insert feature here) yet!

There is only so much I can talk about in one post! I hadn''t even began to touch on using [version control](https://code.visualstudio.com/Docs/versioncontrol "version control"), [debugging](https://code.visualstudio.com/Docs/debugging "debugging"), or [task automation](https://code.visualstudio.com/Docs/tasks "task automation").

I will have to save that for future blog posts.

For now, the best place to get more details would be&#8230; You guessed it, the official documentation!

[http://code.visualstudio.com/Docs/](http://code.visualstudio.com/Docs/ "http://code.visualstudio.com/Docs/")

(I am going for a record of most times linking to the same site in one blog post - Did I win?)

# Next Steps

If you have not already, I hope this posts encourages you to download VS Code and play with it yourself.

As always, I want to hear from you! How do you think it compares to other editors like Sublime? What''s your favorite feature? Are you having any problems? If you are, let me know!

-Tobiah