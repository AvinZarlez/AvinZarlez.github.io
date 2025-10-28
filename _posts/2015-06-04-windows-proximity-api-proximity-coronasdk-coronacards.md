---
id: 104181
title: 'Windows Proximity API Bonus: Proximity with the CoronaSDK'
date: 2015-06-04T12:30:06+00:00
author: DEADNAME
excerpt: |
  For those that use (or want to use) the CoronaSDK, I wanted to show you how you can integrate a native API like the Proximity API into CoronaCards. To do so, we'll need to create a bridge between Lua and C#.
  
  Read on for full instructions!
layout: post
guid: http://www.OLDURL/?p=104181
permalink: /2015/06/04/windows-proximity-api-proximity-coronasdk-coronacards/
categories:
  - Tips and tricks
tags:
  - Bluetooth
  - CoronaSDK
  - NFC
  - Proximity API
  - Wifi Direct
---
For those that use (or want to use) the [CoronaSDK](https://coronalabs.com/ "CoronaSDK"), I wanted to show you how you can integrate a native API like the Proximity API into [CoronaCards](http://coronacards.com/ "CoronaCards"). To do so, we''ll need to create a bridge between Lua and C#.

## Proximity API series overview

  * [Part 1 – What is the Proximity API?](http://www.OLDURL/2015/04/windows-proximity-api-part-1-what-is-the-proximity-api/ "Part 1 – What is the Proximity API?")
  * [Part 2 – Demo project setup](http://www.OLDURL/2015/04/windows-proximity-api-part-2-demo-project-setup/ "Part 2 - Demo project setup")
  * [Part 3 – ProximityDevice](http://www.OLDURL/2015/04/windows-proximity-api-part-3-proximitydevice/ "Part 3 – ProximityDevice")
  * [Part 4 – Expand demo project](http://www.OLDURL/2015/04/windows-proximity-api-part-4-expand-demo-project/ "Part 4 – Expand demo project")
  * [Part 5 – PeerFinder](http://www.OLDURL/2015/05/windows-proximity-api-part-5-peerfinder/ "Part 5 - PeerFinder")
  * [Part 6 – FindAllPeersAsync](http://www.OLDURL/2015/05/windows-proximity-api-part-6-findallpeersasync/ "Part 6- FindAllPeersAsync") 
  * [Part 7 – Final touches](http://www.OLDURL/2015/05/windows-proximity-api-part-7-final-touches/ "Part 7- Final touches") 
  * Part 8 – Bonus: Proximity with the CoronaSDK

# Part Eight: Bonus: Proximity with the CoronaSDK

<!--more-->

## Step One: Install CoronaCards

If you haven''t already, you''ll need CoronaCards installed in addition to Visual Studio. Not just the normal CoronaSDK!

After you [download CoronaCards for Windows Phone 8](http://developer.coronalabs.com/downloads/coronacards), unzip the file. Inside will be `CoronaLabs.Corona.Cards.WindowsPhone.vsix`. Double it click to install.

## Step Two: New CoronaCards Project

Open Visual Studio and hit File->New->Project.

Under Templates->Visual C#->Corona you should find CoronaCards (Windows Phone) app, select it.

<img src="/assets/2015/06/CoronaCardsProximityVisualStudioSelect.png?resize=660%2C402" alt="CoronaCards Proximity Visual Studio" width="660" height="402" class="aligncenter size-full wp-image-104281" srcset="/assets/2015/06/CoronaCardsProximityVisualStudioSelect.png?w=955 955w, /assets/2015/06/CoronaCardsProximityVisualStudioSelect.png?resize=300%2C183 300w" sizes="(max-width: 660px) 100vw, 660px" data-recalc-dims="1" />

## Step Three: Change Capabilities

Exactly like we did in our sample app, we''ll need to enable the Proximity Capability.

However, since this is a Windows 8.0 app, we''ll open the **WMAppManifest.xml** file this time.

Under "Capabilities", enable **ID\_CAP\_PROXIMITY**

<img src="/assets/2015/06/WindowsPhoneCapabilities.png?resize=512%2C512" alt="Windows Phone Capabilities" width="512" height="512" class="aligncenter size-full wp-image-104291" srcset="/assets/2015/06/WindowsPhoneCapabilities.png?w=512 512w, /assets/2015/06/WindowsPhoneCapabilities.png?resize=150%2C150 150w, /assets/2015/06/WindowsPhoneCapabilities.png?resize=300%2C300 300w" sizes="(max-width: 512px) 100vw, 512px" data-recalc-dims="1" />

It should be on by default, but still double check that **ID\_CAP\_NETWORKING** is enabled as well.

## Step Four: Main.lua

I won''t spend too much time going over how CoronaCards works, but it is basically a C# Application that runs a Lua CoronaCards application within it.

Under the Assets folder is a "Corona" folder. In that folder is your Corona project. You could actually run the `Main.lua` file within there in the Corona simulator if you''d like.

Open it up, and replace the contents with the following:

<pre class="brush:text; toolbar: false">local background = display.newImage( "world.jpg", display.contentCenterX, display.contentCenterY )

local myText = display.newText( "Tap me!", display.contentCenterX, display.contentWidth / 4, native.systemFont, 38 )
myText:setFillColor( 1.0, 0.4, 0.4 )

-- Called when a Corona event named "messageReceived" has been dispatched
local function onMessageReceived( event )
    -- Print event property "message" to the screen
    myText.text = "It works!\n" .. event.message

    return "Done"
end

-- Dispatch an event named "startSubscribeAndPublish" to be received by C#
local startSubscribeAndPublishEvent =
{
    name = "startSubscribeAndPublish",
    message = "Hello World!"
}

local result = Runtime:dispatchEvent( startSubscribeAndPublishEvent )

Runtime:addEventListener( "messageReceived", onMessageReceived )

-- In a real app, remember to remove when you're done!
--Runtime:removeEventListener( "messageReceived", onMessageReceived )
</pre>

#### Breakdown:

<pre class="brush:text; toolbar: false">local background = display.newImage( "world.jpg", display.contentCenterX, display.contentCenterY )

local myText = display.newText( "Tap me!", display.contentCenterX, display.contentWidth / 4, native.systemFont, 38 )
myText:setFillColor( 1.0, 0.4, 0.4 )
</pre>

Set up the background and text.

<pre class="brush:text; toolbar: false; first-line: 6">-- Called when a Corona event named "messageReceived" has been dispatched
local function onMessageReceived( event )
    -- Print event property "message" to the screen
    myText.text = "It works!\n" .. event.message

    return "Done"
end
</pre>

Lua function called when the Proximity API receives a message. Takes the text and replaces the myText display.newText object contents with it.

<pre class="brush:text; toolbar: false; first-line: 14">-- Dispatch an event named "startSubscribeAndPublish" to be received by C#
local startSubscribeAndPublishEvent =
{
    name = "startSubscribeAndPublish",
    message = "Hello World!"
}

local result = Runtime:dispatchEvent( startSubscribeAndPublishEvent )
</pre>

Call a C# function from Lua. We create a table with some values. First is the name of the event we would like to call. We will set up that event name later in C# later. Secondly we pass along any parameters we would like to include, such as "Message"

Then we dispatch the event. We get a value back from C#, but for this example we don''t care about that too much.

<pre class="brush:text; toolbar: false; first-line: 23">Runtime:addEventListener( "messageReceived", onMessageReceived )
</pre>

Add a listener so that when C# calls for a "messageReceived" event we go to the onMessageReceived we just created above.

<pre class="brush:text; toolbar: false; first-line: 25">-- In a real app, remember to remove when you're done!
--Runtime:removeEventListener( "messageReceived", onMessageReceived )
</pre>

Included for reference. Normally, want to remove listeners when we are done. But for this extremely simple example, we don''t need it.

That''s it for Lua! Now let''s go back to C# and **MainPage.xaml.cs**

## Step five: Include Proximity API

This step might seem important, but it really isn’t.

When using Proximity API functions, you could type Windows.Networking.Proximity over and over again. But who wants to do _that_?

Let''s make all of our lives easier by adding the following line on top of our **MainPage.xaml.cs** file, just after the other includes:

<pre class="brush:csharp; toolbar: false">// Add Proxmity API on top of defaults
using Windows.Networking.Proximity;
</pre>

(Wait, didn''t I [say all this before](http://www.OLDURL/2015/04/windows-proximity-api-part-2-demo-project-setup/ "Part 2 - Step 5")?)

## Step Six: Variables

We will need to keep track of three variables.

Add these to your MainPage class in **MainPage.xaml.cs**

<pre class="brush:csharp; toolbar: false">// Proximity Device
private ProximityDevice _proximityDevice;
// Published Message ID
private long _publishedMessageID = -1;
// Subscribed Message ID
private long _subscribedMessageID = -1;

CoronaLabs.Corona.WinRT.CoronaRuntimeEventArgs coronaEventArgs;
</pre>

Again, this should look really similar. This time we just needed to add the coronaEventArgs.

## Step Seven: ProximityDevice Initialization

Just like before, at the end of our MainPage constructor, add the following:

<pre class="brush:csharp; toolbar: false">//For sending and receiving messages
_proximityDevice = ProximityDevice.GetDefault();
if (_proximityDevice == null)
{
     // Device failed to load.
     // TO DO: Add error message
}
</pre>

I didn''t bother writing an error message, though I could have just put a native popup of some sort.

## Step Eight: Corona Functions

First replace/add the follow two Corona functions in our MainPage class:

<pre class="brush:csharp; toolbar: false">/// &lt;summary>Called when the Corona runtime has started and finished loaded the "main.lua" file.&lt;/summary>
/// 
/// 
private void OnCoronaRuntimeStarted(object sender, CoronaLabs.Corona.WinRT.CoronaRuntimeEventArgs e)
{

    coronaEventArgs = e;
}

/// &lt;summary>
///  Called when a new CoronaRuntimeEnvironment has been created/loaded,
///  but before the "main.lua" has been executed.
/// &lt;/summary>
/// 
/// 
private void OnCoronaRuntimeLoaded(object sender, CoronaLabs.Corona.WinRT.CoronaRuntimeEventArgs e)
{

    e.CoronaRuntimeEnvironment.AddEventListener("startSubscribeAndPublish", OnStartSubscribeAndPublish);

    e.CoronaRuntimeEnvironment.AddEventListener("stopSubscribeAndPublish", OnStopSubscribeAndPublish);

}
</pre>

When the Corona runtime loads, we added the event listeners for starting and stopping the Proximity API. Then when the Corona runtime starts, we store the CoronaRuntimeEventArgs in the variable we created earlier.

## Step Eight: Proximity Device Functions

Add the following functions in our MainPage class:

<pre class="brush:csharp; toolbar: false">/// &lt;summary>
/// When the app is started, start listening for other devices.
/// &lt;/summary>
/// 
/// 
private CoronaLabs.Corona.WinRT.ICoronaBoxedData OnStartSubscribeAndPublish(
    CoronaLabs.Corona.WinRT.CoronaRuntimeEnvironment sender,
    CoronaLabs.Corona.WinRT.CoronaLuaEventArgs e)
{
    string str = "";

    // Fetch the "event.message" property.
    var boxedMessage = e.Properties.Get("message") as CoronaLabs.Corona.WinRT.CoronaBoxedString;
    if (boxedMessage == null)
    {
        // A "message" property was not provided or it was not of type string.
        // Return an error message to Lua describing what went wrong.
        return CoronaLabs.Corona.WinRT.CoronaBoxedString.From("'event.message' is a required field.");
    }

    if (_subscribedMessageID == -1)
    {
        _subscribedMessageID = _proximityDevice.SubscribeForMessage("Windows.ProximityDemo", messageReceived);
        str += "Subscribed";
    }
    else
    {
        str += "Already Subscribed";
    }


    //Stop Publishing the current message.
    if (_publishedMessageID != -1)
    {
        _proximityDevice.StopPublishingMessage(_publishedMessageID);
    }

    string msg = boxedMessage.ToString();
    if (msg.Length > 0)
    {
        _publishedMessageID = _proximityDevice.PublishMessage("Windows.ProximityDemo", msg);
        str += " - Published";
    }
    else
    {
        str += " - Error Length 0";
    }


    // Return a success message to Lua.
    return CoronaLabs.Corona.WinRT.CoronaBoxedString.From("Started Proximity: " + str);
}

/// &lt;summary>
/// When the stop subscribing button is pressed, stop listening for other devices.
/// &lt;/summary>
/// 
/// 
private CoronaLabs.Corona.WinRT.ICoronaBoxedData OnStopSubscribeAndPublish(
    CoronaLabs.Corona.WinRT.CoronaRuntimeEnvironment sender,
    CoronaLabs.Corona.WinRT.CoronaLuaEventArgs e)
{

    if (_subscribedMessageID != -1)
    {
        _proximityDevice.StopSubscribingForMessage(_subscribedMessageID);
        _subscribedMessageID = -1;
    }

    if (_publishedMessageID != -1)
    {
        _proximityDevice.StopPublishingMessage(_publishedMessageID);
        _publishedMessageID = -1;
    }

    // Return a success message to Lua.
    return CoronaLabs.Corona.WinRT.CoronaBoxedString.From("Stopped subscribing and publishing");
}
</pre>

That''s a lot of code! But if you notice, most of it is exactly the same as our previous version. Really, the only difference is the parameters and returns.

This is because Lua types are very, very different than C# types. So we have to do a little conversion at the start and end.

Now we just need to add the messageReceived function that is called when we subscribe to the message.

## Step Eight: messageReceived Function

This one is a little different, as we have to call back into Lua.

<pre class="brush:csharp; toolbar: false">/// &lt;summary>
/// Invoked when a message is received
/// &lt;/summary>
/// 
/// 
private void messageReceived(ProximityDevice device, ProximityMessage message)
{
    // This will be converted into a Lua "event" table once dispatched by Corona.
    var eventProperties = CoronaLabs.Corona.WinRT.CoronaLuaEventProperties.CreateWithName("messageReceived");
    eventProperties.Set("message", message.DataAsString);

    // Dispatch the event to Lua.
    var eventArgs = new CoronaLabs.Corona.WinRT.CoronaLuaEventArgs(eventProperties);
    var result = coronaEventArgs.CoronaRuntimeEnvironment.DispatchEvent(eventArgs);
}
</pre>

We create a set of event properties with the variables we want to pass back into Lua, then send them off with the event name "messageReceived" we set up in Lua earlier.

# That''s it!

That is all you need to know to create an extreme basic Proximity API app using the Corona SDK. Mainly, I just wanted to show off the ability to bridge between Lua and C#.

Once you understand how to do that, nearly all native C# APIs become usable within your Corona/Lua programs.

If you want to learn more about how to use CoronaCards with Windows 8, you can read [the official documentation](https://docs.coronalabs.com/daily/coronacards/wp8/index.html "CoronaCards for Windows 8"). Specifically if you want to know more about this communication between Lua and C#, there are [more examples and explanation listed here](https://docs.coronalabs.com/daily/coronacards/wp8/communication.html "CoronaCards Lua/.NET Communication").

# Where can I find this code?

I have set up a separate GitHub repository for this CoronaCards project. You can get the latest completed code here: [https://github.com/DEADNAMEZ/CoronaCards-WP8-ProximityDemo](https://github.com/DEADNAMEZ/CoronaCards-WP8-ProximityDemo "CoronaCards GitHub")

# What''s next?:

I hope you have enjoyed this series. If you have a suggestion for other tutorials you''d like to see, let me know!

-DEADNAME