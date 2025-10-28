---
id: 102541
title: 'Windows Proximity API Part 5: PeerFinder'
date: 2015-05-04T13:00:28+00:00
author: DEADNAME
excerpt: |
  Now that we've added the final part of our UI, let's make it functional. In this part we'll enable our app to establish a connection via PeerFinder.
  
  Read on for full instructions!
layout: post
guid: http://www.OLDURL/?p=102541
permalink: /2015/05/04/windows-proximity-api-part-5-peerfinder/
categories:
  - Tips and tricks
tags:
  - Bluetooth
  - NFC
  - Proximity API
  - Wifi Direct
---
Now that we''ve added the final part of our UI, let''s make it functional. In this part we''ll enable our app to establish a connection via PeerFinder.

## Proximity API series overview

  * [Part 1 – What is the Proximity API?](http://www.OLDURL/2015/04/windows-proximity-api-part-1-what-is-the-proximity-api/ "Part 1 – What is the Proximity API?")
  * [Part 2 – Demo project setup](http://www.OLDURL/2015/04/windows-proximity-api-part-2-demo-project-setup/ "Part 2 - Demo project setup")
  * [Part 3 – ProximityDevice](http://www.OLDURL/2015/04/windows-proximity-api-part-3-proximitydevice/ "Part 3 – ProximityDevice")
  * [Part 4 – Expand demo project](http://www.OLDURL/2015/04/windows-proximity-api-part-4-expand-demo-project/ "Part 4 – Expand demo project")
  * Part 5 – PeerFinder
  * [Part 6 – FindAllPeersAsync](http://www.OLDURL/2015/05/windows-proximity-api-part-6-findallpeersasync/ "Part 6 – FindAllPeersAsync")
  * [Part 7 – Final touches](http://www.OLDURL/2015/05/windows-proximity-api-part-7-final-touches/ "Part 7- Final touches") 
  * [Part 8 – Bonus: Proximity with the CoronaSDK](http://www.OLDURL/2015/06/windows-proximity-api-proximity-coronasdk-coronacards/)

# Part Five: PeerFinder

<!--more-->

## Step One: PeerFinder Variables

We''ll need some more variables!

<pre class="brush:csharp; toolbar: false">// Handle external connection requests.
PeerInformation requestingPeer;
// Current peer socket and datawriter
Windows.Networking.Sockets.StreamSocket proximitySocket;
Windows.Storage.Streams.DataWriter dataWriter;
// Are we currently advertising?
bool _advertising = false;
</pre>

requestingPeer
:   The current Peer requesting to connect

proximitySocket
:   The network socket from the proximity connection.

dataWriter
:   The DataWriter for writing messages to peers.

_advertising
:   Are we currently advertising for other peers?

## Step Two: Handlers

We need to run a handler when the connection state changes, and when we get a request.

Add the following to the `MainPage` class in **MainPage.xaml.cs**:

<pre class="brush:csharp; toolbar: false">private void TriggeredConnectionStateChanged(object sender, TriggeredConnectionStateChangedEventArgs e)
{
    if (e.State == TriggeredConnectState.PeerFound)
    {
        WriteMessageText("Peer found. You may now pull your devices out of proximity.");
    }
    if (e.State == TriggeredConnectState.Completed)
    {
        WriteMessageText("You are now connected and may exchange messages! ");
        EnableMessaging(e.Socket);
    }
}

private void ConnectionRequested(object sender, ConnectionRequestedEventArgs e)
{
    requestingPeer = e.PeerInformation;
    WriteMessageText("Connection requested by " + requestingPeer.DisplayName + ". " +
        "Click 'Accept Connection' to connect.");
}
</pre>

We''ll implement the EnableMessaging function later on in this post.

## Step Three: Initialize the handlers

Whenever we pivot onto the PeerFinder, we have to initialize our handlers.

In the PivotChanged class we added in Part 4, replace the `if (current_pivot_index == 1) {}` with the following:

<pre class="brush:csharp; toolbar: false">if (current_pivot_index == 1) // Initialize PeerFinder.
{
    // If supported, add handler
    if ((PeerFinder.SupportedDiscoveryTypes & PeerDiscoveryTypes.Triggered) == PeerDiscoveryTypes.Triggered)
    {
        PeerFinder.TriggeredConnectionStateChanged += TriggeredConnectionStateChanged;
    }
    PeerFinder.ConnectionRequested += ConnectionRequested;
    WriteMessageText("Starting PeerFinder");
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 4">if ((PeerFinder.SupportedDiscoveryTypes & PeerDiscoveryTypes.Triggered) == PeerDiscoveryTypes.Triggered)
{
    PeerFinder.TriggeredConnectionStateChanged += TriggeredConnectionStateChanged;
}
</pre>

If the device supports triggered peer discovery (also known as NFC), add the connection state changed handler. If not, don''t bother.

<pre class="brush:csharp; toolbar: false; first-line: 8">PeerFinder.ConnectionRequested += ConnectionRequested;
WriteMessageText("Starting PeerFinder");
</pre>

Either way, initialize the connection requested handler.

## Step Four: Clean up

Always remember to clean up after you initialize stuff!

Once again in the same PivotChanged class from Part 4, replace the `case 1: //Leaving Proximity Device demo` with the following:

<pre class="brush:csharp; toolbar: false">case 1: //Leaving Proximity Device demo
    // Detach the callback handler (there can only be one PeerConnectProgress handler).
    PeerFinder.TriggeredConnectionStateChanged -= TriggeredConnectionStateChanged;
    // Detach the incoming connection request event handler.
    PeerFinder.ConnectionRequested -= ConnectionRequested;

    //TO DO: Finish cleanup code.

    WriteMessageText("Stopping PeerFinder");
    break;
</pre>

We will replace that `//TO DO: Finish cleanup code.` comment later as well.

## Step Five: Advertise

When we press the Advertise button, we want to show the world (or at least, the current area) that we''re here!

At the bottom of our `MainPage` class, add the following:

<pre class="brush:csharp; toolbar: false">private void AdvertiseButtonPressed(object sender, RoutedEventArgs e)
{
    if (_advertising)
    {
        WriteMessageText("You are already advertising for a connection.");
        return;
    }

    PeerFinder.DisplayName = DisplayNameTextBox.Text;

    if ((PeerFinder.SupportedDiscoveryTypes &
         PeerDiscoveryTypes.Triggered) ==
         PeerDiscoveryTypes.Triggered)
    {
        WriteMessageText("You can tap to connect a peer device that is " +
                         "also advertising for a connection.");
    }
    else
    {
        WriteMessageText("Tap to connect is not supported.");
    }

    if ((PeerFinder.SupportedDiscoveryTypes &
         PeerDiscoveryTypes.Browse) !=
         PeerDiscoveryTypes.Browse)
    {
        WriteMessageText("Peer discovery using Wi-Fi Direct is not supported.");
    }

    PeerFinder.Start();
    _advertising = true;
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 3">if (_advertising)
{
    WriteMessageText("You are already advertising for a connection.");
    return;
}
</pre>

If we are already advertising, give a message and return out of this function.

<pre class="brush:csharp; toolbar: false; first-line: 9">PeerFinder.DisplayName = DisplayNameTextBox.Text;
</pre>

Set our DisplayName to whatever happened to be in the DisplayNameTextBox (which was initialized to `PeerFinder.DisplayName` back in Part 4)

<pre class="brush:csharp; toolbar: false; first-line: 11">if ((PeerFinder.SupportedDiscoveryTypes &
    PeerDiscoveryTypes.Triggered) ==
    PeerDiscoveryTypes.Triggered)
{
    WriteMessageText("You can tap to connect a peer device that is " +
                     "also advertising for a connection.");
}
else
{
    WriteMessageText("Tap to connect is not supported.");
}
</pre>

Again, check if triggered discover is supported. Either way, let the user know.

<pre class="brush:csharp; toolbar: false; first-line: 23">if ((PeerFinder.SupportedDiscoveryTypes &
    PeerDiscoveryTypes.Browse) !=
    PeerDiscoveryTypes.Browse)
{
    WriteMessageText("Peer discovery using Wi-Fi Direct is not supported.");
}
</pre>

Check if Wi-Fi discovery is supported, let the user know if so.

<pre class="brush:csharp; toolbar: false; first-line: 30">PeerFinder.Start();
_advertising = true;
</pre>

Start the PeerFinder class. Simple, right? Also set our _advertising variable as we are now advertising.

## Step Six: Cleanup for PeerFinder

Every time we start something, have to remember to clean it up! Back in case 1 of PivotChanged class, replace that `//TO DO: Finish cleanup code.` we just wrote with the following:

<pre class="brush:csharp; toolbar: false">if (_advertising)
{
    PeerFinder.Stop();
    CloseSocket();
    _advertising = false;
}
</pre>

We''ll end this part with writing the `CloseSocket()` function.

## Step Seven: EnableMessaging

Now that we have a connection, we need to be able to write messages back and forth.

Add the following function to the `MainPage` class:

<pre class="brush:csharp; toolbar: false">private void EnableMessaging(Windows.Networking.Sockets.StreamSocket socket)
{
    // If PeerFinder has not been started, quit.
    if (!_advertising)
    {
        CloseSocket();
        return;
    }

    // Get the network socket from the proximity connection.
    proximitySocket = socket;

    // Create DataWriter for writing messages to peers.
    dataWriter = new Windows.Storage.Streams.DataWriter(proximitySocket.OutputStream);

    // Listen for messages from peers.
    Windows.Storage.Streams.DataReader dataReader =
            new Windows.Storage.Streams.DataReader(proximitySocket.InputStream);
    StartReader(dataReader);
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 3">// If PeerFinder has not been started, quit.
if (!_advertising)
{
    CloseSocket();
    return;
}
</pre>

If we haven''t started advertising yet, we can''t exchange messages. Close any sockets.

<pre class="brush:csharp; toolbar: false; first-line: 10">// Get the network socket from the proximity connection.
proximitySocket = socket;
</pre>

Save the socket from the successful connection.

<pre class="brush:csharp; toolbar: false; first-line: 13">// Create DataWriter for writing messages to peers.
dataWriter = new Windows.Storage.Streams.DataWriter(proximitySocket.OutputStream);
</pre>

Create a DataWriter from said socket.

<pre class="brush:csharp; toolbar: false; first-line: 16">// Listen for messages from peers.
Windows.Storage.Streams.DataReader dataReader =
       new Windows.Storage.Streams.DataReader(proximitySocket.InputStream);
StartReader(dataReader);
</pre>

Create a DataReader, also from the socket.

## Step Eight: Reading

We have a connection, we have enabled a DataReader&#8230; Now we have to figure out what they''re saying to us!

Add the following function to the `MainPage` class:

<pre class="brush:csharp; toolbar: false">private async void StartReader( Windows.Storage.Streams.DataReader reader )
{
    try
    {
        uint bytesRead = await reader.LoadAsync(sizeof(uint));
        if (bytesRead &gt; 0)
        {
            uint strLength = (uint)reader.ReadUInt32();
            bytesRead = await reader.LoadAsync(strLength);
            if (bytesRead &gt; 0)
            {
                String message = reader.ReadString(strLength);
                WriteMessageText("Received message: " + message);
                StartReader(reader); // Start another reader
            }
            else
            {
                CloseReader(reader, "No string length!");
            }
        }
        else
        {
            CloseReader(reader, "No bytes read!");
        }
    }
    catch
    {
        CloseReader(reader);
    }
}
</pre>

First, we wrap it all in a try/catch that closes the reader if we run into any errors.

Then, we attempt to LoadAsync from the reader. If what we just read is <= 0, close the reader.

Then, we attempt to turn this into a string. If the string is <= 0 characters long, close the reader.

Lastly, we read the string into a variable, display it onto the screen, and recursively call the function.

## Step Nine: Reader Cleanup

You guessed it, cleanup time!

Let''s make the CloseReader function from above.

<pre class="brush:csharp; toolbar: false">private void CloseReader( Windows.Storage.Streams.DataReader reader, string err = "")
{
    WriteMessageText("The peer app closed the socket. "+err);
    reader.Dispose();
    CloseSocket();
}
</pre>

## Step Ten: Close Socket

Speaking of keeping clean, let’s implement that CloseSocket function we''ve been writing everywhere.

<pre class="brush:csharp; toolbar: false">private void CloseSocket()
{
    if (proximitySocket != null)
    {
        proximitySocket.Dispose();
        proximitySocket = null;
    }

    if (dataWriter != null)
    {
        dataWriter.Dispose();
        dataWriter = null;
    }
}
</pre>

# Up next:

In part six, we''ll start looking for peers on our local network/bluetooth/wifi.

-DEADNAME