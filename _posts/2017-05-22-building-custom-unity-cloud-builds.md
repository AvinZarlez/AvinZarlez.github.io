---
id: 685271
title: Building your own custom Unity Cloud Builds
date: 2017-05-22T14:45:33+00:00
author: DEADNAME
excerpt: |
  Are you manually making builds for your Unity project? It may not seem like a lot of time, but those minutes add up. Especially if you’re working with others, or have to deploy to many different test machines. A non-standardized process can lead to confusion from the rest of the team when determining which build is the latest, and almost impossible to find the latest previous known good build.
  
  Did you know you can create an automated build and release pipeline using Azure? This article will show you how!
layout: post
guid: http://www.DEADNAMEz.com/?p=685271
permalink: /2017/05/22/building-custom-unity-cloud-builds/
image: /assets/2014/01/Unity_Logo.png
categories:
  - Resources
tags:
  - Azure
  - Unity
---
Are you manually making builds for your Unity project? It may not seem like a lot of time, but those minutes add up. Especially if you’re working with others, or have to deploy to many different test machines. A non-standardized process can lead to confusion from the rest of the team when determining which build is the latest, and almost impossible to find the latest previous known good build.

Did you know you can create an automated build and release pipeline using Azure? This article will show you how!

<!--more-->

## Step One: Requirements

There are some requirements before you start. Some of these aren’t strictly required, but it’s a good idea to have handy to make sure everything works correctly the first and 50<sup>th</sup> time.

Make sure you do these two things:

  1. Project should be buildable on Windows (or Linux) via the command line 
      * Watch for random error “gotchas” like spaces in file names.
      * You’ll need a build script, see below.
  2. Write down required software and version numbers.

  * What version of Unity do you use? Git? Any other software you use for your project.
  * You’ll be able to update these later, but if you don’t track it now you’ll be frustrated 6 months from now when the build breaks because some random piece of software updated and changed something.

### What’s a Build Script?

In order to build from command line, we need to define the parameters of the build in a file instead of the Unity GUI interface.

In Assets/Editor, create a “Build” class. (Example: "Builder.cs" which derives from type ScriptableObject)

Then in this new class, make a new public static function to build for each platform.

For an example, check out this file: <https://github.com/DEADNAMEZ/DumbGame/blob/master/Assets/Editor/Builder.cs>

(Feel free to copy/paste that file into your own project)

## Step Two: Azure Account

You’ll need an Azure account, of course. Sign up by going to <http://portal.azure.com> !

## Step Three: Spin up a VM

For this example we have created a virtual machine running Windows Server 2012 R2 with Visual Studio Community already installed. You can use the [JSON template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) to deploy the required virtual network and ports supporting Jenkins, the required storage accounts, and virtual machine. The template includes a DSC extension to configure some additional operating system features and to install [Chocolatey](https://chocolatey.org/), which was then used to install community-maintained packages for Jenkins, Unity, and Git.

If you are not using our template, you’ll need to do the following:

  * Deploy a VM
  * Deploy to a Security Group
  * Open port 8080
  * Open RDP port 3388
  * Install Git, Unity and Jenkins

## Step Four: Configure server

After you’ve deployed yourself or with our template, you’ll need to make sure you:

  * Configure Git
  * Open Unity and log in
  * Possible configure Unity for certain platform builds 
      * Example: Installing and telling Unity where the Android SDK is.

If you plan to do UWP/Windows Store builds, you’ll also need to:

  * Set up Visual Studio
  * Log in with developer ID
  * Install Windows Store SDK

You can possible automate this process as well using a deployment template, [Chocolatey](https://chocolatey.org/), and [Unity’s command line arguments](https://docs.unity3d.com/Manual/CommandLineArguments.html).

## Step Five: Configure Jenkins

First, connect Jenkins to your git repo using the Git plugin:

<https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin>

Make sure the plugin is installed and follow the documentation there. The only way I got it to work for Private repos was to configure the server to log into git using SSH.

If you are using GitHub with a private repo, I would go into Jenkins->Config, GitHub->Advanced, log in to your GitHub account and let it automatically configure it as needed.

From there, you can follow the instructions with Jenkin’s plugin system to link to Slack, HockeyApp, or any other service you use for your builds.

When it comes time to making the Unity build, configure the Unity Jenkins plugin by setting the path to where you installed Unity. Then in your build configuration, execute the following command line argument:

> -quit -batchmode -executeMethod Builder.PerformWSABuild
> 
> -quit -batchmode -executeMethod Builder.PerformAndroidBuild

(Where “Builder.PerformWSABuild” is from the build script you created earlier)

&nbsp;

After the build, make sure to archive the artifact and upload it to somewhere safe like an Azure Blob Storage account.

If you told your build script to put the files in a “Builds/” folder, you can tell Jenkins to archive all the files in “Builds/*\*/\*”

## Step Six: Test a build!

Once you have it all set up, try making a build and see what happens! Jenkins gives you pretty detailed console logs, so it should tell you exactly what’s wrong if anything bad happens.

I would work with a dummy project that you are 100% sure builds on remote machines fine before attempting your actual project.

I have set one up you can use here: <https://github.com/DEADNAMEZ/DumbGame/>

## Links

Here are some other useful links:

<https://github.com/DEADNAMEZ/JenkinsUnityBuildPipeline>

<https://wiki.jenkins-ci.org/display/JENKINS/HockeyApp+Plugin>

<https://wiki.jenkins-ci.org/display/JENKINS/Unity3dBuilder+Plugin>

<https://wiki.jenkins-ci.org/display/JENKINS/Windows+Azure+Storage+Plugin>

<https://github.com/jenkinsci/tfs-plugin/blob/master/README.md>

&nbsp;

Now you have your own private Unity cloud build! If you have any more questions or run into issues, comment below.

-DEADNAME