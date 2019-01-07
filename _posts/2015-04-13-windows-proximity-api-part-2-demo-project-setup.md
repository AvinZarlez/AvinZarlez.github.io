---
id: 101911
title: 'Windows Proximity API Part 2: Demo project setup'
date: 2015-04-13T12:00:32+00:00
author: Tobiah
excerpt: |
  Welcome to Part 2 of my Proximity API blog series!
  
  In this part we will set up our initial project, including all the XAML we’ll need for our demo application. This part isn’t specific to the Proximity API, but will give us the shell of a code base we’ll need to do the real stuff in the following parts.
  
  Part Two: Demo project setup
  For this demo application, we’ll start with a blank Windows Phone C# project. The Proximity API code would work on Windows 8 and Universal apps, but for the sack of simplicity we’ll focus on Windows Phone so we don’t have to deal with two different XAMLs/UIs.
  
  Read on for full instructions!
layout: post
guid: http://www.tobiahmarks.com/?p=101911
permalink: /2015/04/13/windows-proximity-api-part-2-demo-project-setup/
categories:
  - Tips and tricks
tags:
  - Bluetooth
  - NFC
  - Proximity API
  - Wifi Direct
---
Welcome to Part 2 of my Proximity API blog series!
  
In this part we will set up our initial project, including all the XAML we’ll need for our demo application. This part isn’t specific to the Proximity API, but will give us the shell of a code base we’ll need to do the real stuff in the following parts.
  
If you are already comfortable setting up a new Windows Phone project and UI in XAML, skip to [step four](#stepfour "Go to Step Four").

## Proximity API series overview

  * [Part 1 – What is the Proximity API?](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-1-what-is-the-proximity-api/ "Part 1")
  * Part 2 – Demo project setup
  * [Part 3 – ProximityDevice](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-3-proximitydevice/ "Part 3 - ProximityDevice")
  * [Part 4 – Expand demo project](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-4-expand-demo-project/ "Part 4 - Expand Demo Project")
  * [Part 5 – PeerFinder](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-5-peerfinder/ "Part 5")
  * [Part 6 – FindAllPeersAsync](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-6-findallpeersasync/ "Part 6")
  * [Part 7 – Final touches](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-7-final-touches/ "Part 7")
  * [Part 8 – Bonus: Proximity with the CoronaSDK](http://www.tobiahmarks.com/2015/06/windows-proximity-api-proximity-coronasdk-coronacards/ "Part 8 – Bonus: Proximity with the CoronaSDK")

# Part Two: Demo project setup

<!--more-->


  
For this demo application, we’ll start with a blank Windows Phone C# project. The Proximity API code would work on Windows 8 and Universal apps, but for the sack of simplicity we’ll focus on Windows Phone so we don’t have to deal with two different XAMLs/UIs.

## Step one: Make a new project

Open Visual Studio and hit File->New->Project.

Under Templates->Visual C#->Store Apps->Windows Phone Apps you should find Black App (Windows Phone), select it.

[<img class="aligncenter size-full wp-image-101951" src="/assets/2015/04/2-1.png?resize=660%2C364" alt="New Blank Windows App" width="660" height="364" srcset="/assets/2015/04/2-1.png?w=815 815w, /assets/2015/04/2-1.png?resize=300%2C166 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2015/04/2-1.png)

Set up a name and where you’ll save it, and hit ok!

## Step two: Create a UI in XAML

Let''s make a UI for the ProximityDevice sample we''ll make in Part 3.

First we want to make a Pivot view, so that we can Pivot between the ProximityDevice sample we''ll make in Part 3 and the PeerFinder sample we''ll make in part 5.

We will define one element in this Pivot, which will be for the "ProximityDevice" sample in Part 3.

Open up the **MainPage.xaml** file, and replace the " element with the following:

<pre class="brush:xml; toolbar: false">&lt;!-- Top part of grid is pivot view of controls, bottom is output text -->
&lt;Grid>  
    &lt;Grid.RowDefinitions>
        &lt;RowDefinition Height="Auto"/>
        &lt;RowDefinition Height="*"/>
    &lt;/Grid.RowDefinitions>
    &lt;Pivot Title="Proximity API Demos" Grid.Row="0" SelectionChanged="PivotChanged">
        &lt;PivotItem Header="ProximityDevice">
            &lt;StackPanel Orientation="Vertical">
                &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
                    &lt;TextBox x:Name="TapMessageTextBox" Text="Hello World!" Width="256"/>
                &lt;/StackPanel>
                &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
                    &lt;Button x:Name="PublishButton" Content="Publish" Margin="5,0,5,0"
                                Click="PublishButtonPressed" />
                    &lt;Button x:Name="StopPublishingButton" Content="Stop Publishing" Margin="5,0,5,0"
                                Click="StopPublishingButtonPressed" />
                &lt;/StackPanel>
                &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
                    &lt;Button x:Name="SubscribeButton" Content="Subscribe" Margin="5,0,5,0"
                                Click="SubscribeButtonPressed" />
                    &lt;Button x:Name="StopSubscribingButton" Content="Stop Subscribing" Margin="5,0,5,0"
                                Click="StopSubscribingButtonPressed" />
                &lt;/StackPanel>
            &lt;/StackPanel>
        &lt;/PivotItem>
    &lt;/Pivot>
    &lt;ScrollViewer Grid.Row="1">
        &lt;TextBlock x:Name="MessageBlock" FontSize="18" TextWrapping="WrapWholeWords"
                   Text="Welcome to Proximity API Demos!&#x0a;Swipe to switch between examples."
                   VerticalAlignment="Top" Margin="10,0,10,0" />
    &lt;/ScrollViewer>
&lt;/Grid>
</pre>

We will be going back to this XAML file to include more later, but for now this is just what we need to get started.

#### Breakdown:

<pre class="brush:xml; toolbar: false; first-line: 3">&lt;Grid.RowDefinitions>
    &lt;RowDefinition Height="Auto"/>
    &lt;RowDefinition Height="*"/>
&lt;/Grid.RowDefinitions>
</pre>

This defines two vertical elements in the grid, one of automatic height and the other the remaining screen real estate.

<pre class="brush:xml; toolbar: false; first-line: 7">&lt;Pivot Title="Proximity API Demos" Grid.Row="0" SelectionChanged="PivotChanged">
</pre>

Creates the Pivot table, sets it as the top element, and set the "SelectionChanged" function.

A function named "PivotChanged" will be called whenever the user swipes and changes the focus of the Pivot. We will define this function in part 5, when we''ll have more than one element in the Pivot.

<pre class="brush:xml; toolbar: false; first-line: 8">&lt;PivotItem Header="PeerDevice">
    &lt;StackPanel Orientation="Vertical">
        &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
            &lt;TextBox x:Name="TapMessageTextBox" Text="Hello World!" Width="256"/>
        &lt;/StackPanel>
        &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
            &lt;Button x:Name="PublishButton" Content="Publish" Margin="5,0,5,0"
                        Click="PublishButtonPressed" />
            &lt;Button x:Name="StopPublishingButton" Content="Stop Publishing" Margin="5,0,5,0"
                        Click="StopPublishingButtonPressed" />
        &lt;/StackPanel>
        &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
            &lt;Button x:Name="SubscribeButton" Content="Subscribe" Margin="5,0,5,0"
                        Click="SubscribeButtonPressed" />
            &lt;Button x:Name="StopSubscribingButton" Content="Stop Subscribing" Margin="5,0,5,0"
                        Click="StopSubscribingButtonPressed" />
        &lt;/StackPanel>
    &lt;/StackPanel>
&lt;/PivotItem>
</pre>

Here we define the PeerDevice example UI elements.

We have a TextBox for the user''s message, and buttons for "Publish", "Stop Publishing", "Subscribe", and "Stop Subscribing".

<pre class="brush:xml; toolbar: false; first-line: 28">&lt;ScrollViewer Grid.Row="1">
    &lt;TextBlock x:Name="MessageBlock" FontSize="18" TextWrapping="WrapWholeWords"
               Text="Welcome to Proximity API Demos!&#x0a;Swipe to switch between examples."
               VerticalAlignment="Top" Margin="10,0,10,0" />
&lt;/ScrollViewer>
</pre>

As the second, lower element of our grid, we define a Scroll View. Inside we put a single TextBlock for displaying "console style" status messages to communicate to the user.

We wrap it in a Scroll View because then we can look at past messages after there are more than fit on the screen.

## Step three: WriteMessageText Function – 6min

Time to dive into C#!

We need a function design to take a string and display it to the screen, using the new TextBlock element we just created in step two.

Open up **MainPage.xaml.cs**, and within the " class

<pre class="brush:csharp; toolbar: false">// Dispatcher for messages we display to the screen
private Windows.UI.Core.CoreDispatcher messageDispatcher = Window.Current.CoreWindow.Dispatcher;

async private void WriteMessageText(string message, bool overwrite = false)
{
    await messageDispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
        () =&gt;
        {
            message = DateTime.Now.ToString("[HH:mm:ss] ") + message + "\n";

            if (overwrite)
                MessageBlock.Text = message;
            else
                MessageBlock.Text = message + MessageBlock.Text;
        });
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 2">private Windows.UI.Core.CoreDispatcher messageDispatcher = Window.Current.CoreWindow.Dispatcher;
</pre>

Set the dispatcher to run the message function asynchronously.

<pre class="brush:csharp; toolbar: false; first-line: 6">async private void WriteMessageText(string message, bool overwrite = false)
{
    await messageDispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
        () =&gt;
        {
        });
}
</pre>

An async function that takes a string "message", and optional "overwrite" bool.

Inside the function, it runs through the dispatcher we just created another function:

<pre class="brush:csharp; toolbar: false; first-line: 9">message = DateTime.Now.ToString("[HH:mm:ss] ") + message + "\n";

if (overwrite)
    MessageBlock.Text = message;
else
    MessageBlock.Text = message + MessageBlock.Text;
</pre>

Add the time to the string, and then either add it to the existing MessageBlock.Text or overwrite the existing MessageBlock and replace it with the new string.

## Step four: Package.appxmanifest {#stepfour}

Now we need to tell our application we want to use the Proximity API. If the program doesn''t explictly ask for permission, it won''t be able to access it!

If you forget to do this step, you''ll all sorts of odd errors when you try to use the Proximity API.

Fortunately, all you have to do is open your **Package.appxmanifest** file, open the "Capabilities" tab, and enable **Proximity**.

[<img class="aligncenter size-full wp-image-101971" src="/assets/2015/04/2-2.png?resize=660%2C295" alt="Check internet and proximity" width="660" height="295" srcset="/assets/2015/04/2-2.png?w=859 859w, /assets/2015/04/2-2.png?resize=300%2C134 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />](/assets/2015/04/2-2.png)

It should be on by default, but you will also need to ensure **Networking** / **Internet** capability is enabled in order for everything to work.

While we are here, let’s also go to the "Application" tab and select **Portrait**. This makes it so the screen will be locked in the Portrait orientation no matter which way we hold our device.

[<img class="aligncenter size-full wp-image-101981" src="/assets/2015/04/2-3.png?resize=560%2C129" alt="Portrait mode" width="560" height="129" srcset="/assets/2015/04/2-3.png?w=560 560w, /assets/2015/04/2-3.png?resize=300%2C69 300w" sizes="(max-width: 560px) 100vw, 560px" data-recalc-dims="1" />](/assets/2015/04/2-3.png)

Since we''ll be asking people to rub devices together, I personally like sticking with one orientation to not disorient users.

## Step five: Include Proximity API

This step might seem important, but it really isn’t.

When using Proximity API functions, you could type Windows.Networking.Proximity over and over again. But who wants to do _that_?

Let''s make all of our lives easier by adding the following line on top of our **MainPage.xaml.cs** file, just after the other includes:

<pre class="brush:csharp; toolbar: false">// Add Proxmity API on top of defaults
using Windows.Networking.Proximity;
</pre>

# Up next:

In part three, we''ll make all these next buttons and UI we just added do something!
  
-Tobiah