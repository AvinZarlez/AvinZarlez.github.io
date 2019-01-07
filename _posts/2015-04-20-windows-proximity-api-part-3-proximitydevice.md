---
id: 102011
title: 'Windows Proximity API Part 3: ProximityDevice'
date: 2015-04-20T12:35:36+00:00
author: Tobiah
excerpt: |
  Let's dive into the first part of the Proximity API we'll learn, the PeerDevice class.
  
  Read on for full instructions!
layout: post
guid: http://www.tobiahmarks.com/?p=102011
permalink: /2015/04/20/windows-proximity-api-part-3-proximitydevice/
categories:
  - Tips and tricks
tags:
  - Bluetooth
  - NFC
  - Proximity API
  - Wifi Direct
---
Let''s dive into the first part of the Proximity API we''ll learn, the PeerDevice class.

## Proximity API series overview

  * [Part 1 – What is the Proximity API?](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-1-what-is-the-proximity-api/ "Part 1")
  * [Part 2 – Demo project setup](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-2-demo-project-setup/ "Part 2")
  * Part 3 – ProximityDevice
  * [Part 4 – Expand demo project](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-4-expand-demo-project/ "Part 4 - Expand Demo Project")
  * [Part 5 – PeerFinder](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-5-peerfinder/ "Part 5")
  * [Part 6 – FindAllPeersAsync](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-6-findallpeersasync/ "Part 6")
  * [Part 7 – Final touches](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-7-final-touches/ "Part 7")
  * [Part 8 – Bonus: Proximity with the CoronaSDK](http://www.tobiahmarks.com/2015/06/windows-proximity-api-proximity-coronasdk-coronacards/ "Part 8 – Bonus: Proximity with the CoronaSDK")

# Part Three: ProximityDevice

<!--more-->

## Step One: Variables

We will need to keep track of three variables.

Add these to your MainPage class in **MainPage.xaml.cs**

<pre class="brush:csharp; toolbar: false">// Proximity Device
private ProximityDevice _proximityDevice;
// Published Message ID
private long _publishedMessageID = -1;
// Subscribed Message ID
private long _subscribedMessageID = -1;
</pre>

_proximityDevice
:   A reference to the ProximityDevice

_publishedMessageID
:   The ID of the message currently being published

_subscribedMessageID
:   The ID of the message currently being subscribed to

## Step Two: ProximityDevice Initialization

Now that we have _proximityDevice defined, we need to initialize it. Inside your MainPage constructor, add the following:

<pre class="brush:csharp; toolbar: false">//For sending and receiving messages
_proximityDevice = ProximityDevice.GetDefault();
if (_proximityDevice == null)
{
    WriteMessageText("Failed to initialized proximity device.\n" +
    "Your device may not have proximity hardware.");
}
</pre>

If the Proximity capability is enabled and the device supports it, the default ProximityDevice will be assigned. Otherwise, it will be null, and we will report an error to the user.

Remember, WriteMessageText is a function we made in Part 2.

## Step Three: Publish Button

Time to make some of those nice buttons from Part 2 actually do something!

Still in our MainPage class in **MainPage.xaml.cs**, add the following function:

<pre class="brush:csharp; toolbar: false">private void PublishButtonPressed(object sender, RoutedEventArgs e)
{

    //Stop Publishing the current message.
    if (_publishedMessageID != -1)
        _proximityDevice.StopPublishingMessage(_publishedMessageID);

    string msg = TapMessageTextBox.Text;
    if (msg.Length &gt; 0)
    {
        _publishedMessageID = _proximityDevice.PublishMessage("Windows.ExampleMessage", msg);
        WriteMessageText("Publishing your message. Tap devices to send!");
    }
    else
    {
        WriteMessageText("Error: Write something first, silly!");
    }
}
</pre>

The function name "PublishButtonPressed" was specifically called out in our eariler XAML code to execute on click.

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 4">//Stop Publishing the current message.
if (_publishedMessageID != -1)
    _proximityDevice.StopPublishingMessage(_publishedMessageID);
</pre>

If we have already published a message, the \_publishedMessageID won''t be -1. If that is the case, we ask the \_proximityDevice to stop publishing the old message before giving it a new one.

<pre class="brush:csharp; toolbar: false; first-line: 8">string msg = TapMessageTextBox.Text;
if (msg.Length &gt; 0)
{
    // ...
}
else
{
    WriteMessageText("Error: Write something first, silly!");
}
</pre>

Now we grab the message we''re going to publish. The user enters it into the TextBox called TapMessageTextBox we defined in our XAML.

If the Length is <= 0 though, that means we don''t have any message! Rather than publish nothing, we give the user a nice error message.

<pre class="brush:csharp; toolbar: false; first-line: 11">_publishedMessageID = _proximityDevice.PublishMessage("Windows.ExampleMessage", msg);
WriteMessageText("Publishing your message. Tap devices to send!");
</pre>

If everything is ready to go, we call our _proximityDevice to publish the message "msg". The first parameter is the message type.

The type is a case sensitive string that has two parts. The protocol is first, followed by a dot (.) and then the subtype.

For the PublishMessage method, the protocol must always be "Windows.", but the sub type is totally up to you. It just has to be a string of alphanumeric characters (or the following additional characters: . ( ) + , - : = @ ; $ _ ! * ’ ) and can''t exceed 250 characters in length.

You could use your app name, or a specific command. Remember, whatever you use, the device will look for whatever messages are being broadcast with that sub type. So if two apps use "Windows.BusinessCard", you may happen to read the published message from an app you didn''t intend to! Although since this is NFC, the odds of that are unlikely. Still, it''s good to remember to check the input.

This function returns an ID number (long), which we save to _publishedMessageID.

## Step Four: Subscribe Button

We''re publishing ok, but nobody is listening! Let''s change that.

Add the following under the above functions in our MainPage class in **MainPage.xaml.cs**:

<pre class="brush:csharp; toolbar: false">private void SubscribeButtonPressed(object sender, RoutedEventArgs e)
{
    if (_subscribedMessageID == -1)
    {
        _subscribedMessageID = _proximityDevice.SubscribeForMessage("Windows.ExampleMessage", messageReceived);
        WriteMessageText("Subscribing for messages! Tap devices to receive.");
    }
    else
    {
        WriteMessageText("Already subscribing!");
    }
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 3">if (_subscribedMessageID == -1)
{
    // ...
}
else
{
    WriteMessageText("Already subscribing!");
}
</pre>

If you are already subscribed to a message, let the user know. If not, start subscribing.

<pre class="brush:csharp; toolbar: false; first-line: 5">_subscribedMessageID = _proximityDevice.SubscribeForMessage("Windows.ExampleMessage", messageReceived);
WriteMessageText("Subscribing for messages! Tap devices to receive.");
</pre>

SubscribeForMessage takes two parameters. The message type as defined in step three, and a function to run when a message is received.

## Step Five: When a message is received&#8230;

Add the following messageReceived function we just referenced in step five.

<pre class="brush:csharp; toolbar: false">private void messageReceived(ProximityDevice device, ProximityMessage message)
{
    WriteMessageText("Message received: " + message.DataAsString);
}
</pre>

Simple enough! The function needs a ProximityDevice and ProximityMessage parameter. We don''t need to do anything, since we just want to display the text. We turn the input into a string with the DataAsString function and throw it into our WriteMessageText function.

## Step Six: Stop Buttons

Our app doesn''t strictly need a stop buttons, it could be handled automatically in the background. For this example, we''ll make buttons.

<pre class="brush:csharp; toolbar: false">private void StopPublishingButtonPressed(object sender, RoutedEventArgs e)
{
    if (_publishedMessageID != -1)
    {
        _proximityDevice.StopPublishingMessage(_publishedMessageID);
        _publishedMessageID = -1;
        WriteMessageText("Stopped publishing");
    }
}

private void StopSubscribingButtonPressed(object sender, RoutedEventArgs e)
{
    if (_subscribedMessageID != -1)
    {
        _proximityDevice.StopSubscribingForMessage(_subscribedMessageID);
        _subscribedMessageID = -1;
        WriteMessageText("Stopped subscribing");
    }
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 3">if (_publishedMessageID != -1)
{
    // ...
}
</pre>

<pre class="brush:csharp; toolbar: false; first-line: 13">if (_subscribedMessageID != -1)
{
    // ...
}
</pre>

If we are publishing/subscribing, the \_publishedMessageID or \_subscribedMessageID has a value other than -1&#8230;

<pre class="brush:csharp; toolbar: false; first-line: 5">_proximityDevice.StopPublishingMessage(_publishedMessageID);
_publishedMessageID = -1;
WriteMessageText("Stopped publishing");
</pre>

<pre class="brush:csharp; toolbar: false; first-line: 15">_proximityDevice.StopSubscribingForMessage(_subscribedMessageID);
_subscribedMessageID = -1;
WriteMessageText("Stopped subscribing");
</pre>

Similar to ProximityDevice.PublishMessage and ProximityDevice.SubscribeForMessage, we have ProximityDevice.StopPublishingMessage and ProximityDevice.StopSubscribingForMessage. Simply pass the ID as a parameter and it will stop!

Afterwards, we reset the ID to -1 so we know we''ve stopped.

# Test build!

We are now at the point to build the project and run it on a device!

Assuming all went well, you should be able to do the following error free:

  1. On one device, write a message and hit Publish.
  2. On the other device, hit subscribe.
  3. Touch the devices together, and on device two you will see the message from device one!

You can simultaneously subscribe and publish, both sending and receiving a message in one tap!

If this doesn''t work, go back through parts 1-3 and make sure you copied all the code correctly.

# Up next:

In part four, we''ll expand our demo project in order to add a second example for PeerFinder.

-Tobiah