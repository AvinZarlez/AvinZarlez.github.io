---
id: 102731
title: 'Windows Proximity API Part 6: FindAllPeersAsync'
date: 2015-05-11T13:31:24+00:00
author: Tobiah
excerpt: |
  Now that we have the basics in for PeerFinder, we'll start looking for local peers without using NFC.
  
  Read on for full instructions!
layout: post
guid: http://www.tobiahmarks.com/?p=102731
permalink: /2015/05/11/windows-proximity-api-part-6-findallpeersasync/
categories:
  - Tips and tricks
tags:
  - Bluetooth
  - NFC
  - Proximity API
  - Wifi Direct
---
Now that we have the basics in for PeerFinder, we''ll start looking for local peers without using NFC.

## Proximity API series overview

  * [Part 1 – What is the Proximity API?](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-1-what-is-the-proximity-api/ "Part 1 – What is the Proximity API?")
  * [Part 2 – Demo project setup](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-2-demo-project-setup/ "Part 2 - Demo project setup")
  * [Part 3 – ProximityDevice](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-3-proximitydevice/ "Part 3 – ProximityDevice")
  * [Part 4 – Expand demo project](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-4-expand-demo-project/ "Part 4 – Expand demo project")
  * [Part 5 – PeerFinder](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-5-peerfinder/ "Part 5 - PeerFinder")
  * Part 6 – FindAllPeersAsync
  * [Part 7 – Final touches](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-7-final-touches/ "Part 7- Final touches") 
  * [Part 8 – Bonus: Proximity with the CoronaSDK](http://www.tobiahmarks.com/2015/06/windows-proximity-api-proximity-coronasdk-coronacards/)

# Part Six: FindAllPeersAsync

<!--more-->

## Step One: Look for peers

So far, we can only connect via tapping. Let’s implement the Find button!

Once again in **MainPage.xaml.cs** at the bottom of our `MainPage` class add the following:

<pre class="brush:csharp; toolbar: false">async private void FindButtonPressed(object sender, RoutedEventArgs e)
{
    if ((PeerFinder.SupportedDiscoveryTypes & PeerDiscoveryTypes.Browse) != PeerDiscoveryTypes.Browse)
    {
        WriteMessageText("Peer discovery using Wi-Fi is not supported.");
        return;
    }

    try
    {
        WriteMessageText("Attempting to find connection.");
        var peerInfoCollection = await PeerFinder.FindAllPeersAsync();
        if (peerInfoCollection.Count &gt; 0)
        {
            // Connect to the first peer
            // NOTE: In production, would provide a list
            ConnectToPeer(peerInfoCollection[0]);
        }
    }
    catch (Exception err)
    {
        WriteMessageText("Error finding peers: " + err.Message);
    }
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 3">if ((PeerFinder.SupportedDiscoveryTypes & PeerDiscoveryTypes.Browse) != PeerDiscoveryTypes.Browse)
    {
        WriteMessageText("Peer discovery using Wi-Fi is not supported.");
        return;
    }
</pre>

If browse discovery (finding peers through WiFi) is not supported, display a message to the user and return out of the function.

<pre class="brush:csharp; toolbar: false; first-line: 9">try
    {
        WriteMessageText("Attempting to find connection.");
        
        //...

    }
    catch (Exception err)
    {
        WriteMessageText("Error finding peers: " + err.Message);
    }
</pre>

Try to connect, but handle failures.

<pre class="brush:csharp; toolbar: false; first-line: 12">var peerInfoCollection = await PeerFinder.FindAllPeersAsync();
</pre>

Using FindAllPeersAsync(), we get a list of peers in the area and put it into an array.

<pre class="brush:csharp; toolbar: false; first-line: 13">if (peerInfoCollection.Count &gt; 0)
        {
            //..
        }
</pre>

If the count is more than 0, that means there is a peer!

<pre class="brush:csharp; toolbar: false; first-line: 15">// Connect to the first peer
            // NOTE: In production, would provide a list
            ConnectToPeer(peerInfoCollection[0]);
</pre>

For this application, we''re just going to connect to the first peer. In a real app, we would let the user have a little more choice in the matter. Most likely let them chose from some sort of list of potential connections.

But this is just a demo/example, so we don''t need any of that!

Let''s ask to connect to them via the ConnectToPeer() function we''ll make in Step Three.

## Step Two: Found a peer!

Somebody is asking to connect to us, let''s accept the connection!

Another new function for our MainPage class:

<pre class="brush:csharp; toolbar: false">private void AcceptButtonPressed(object sender, RoutedEventArgs e)
{
    if (requestingPeer == null)
    {
        WriteMessageText("No peer connection has been requested.");
        return;
    }

    ConnectToPeer(requestingPeer);
}
</pre>

This one is pretty simple. If there is no requestingPeer (a variable we made in Part 5), give an error message and return out of the function. Otherwise, connect to the peer.

## Step Three: ConnectToPeer

Once we find a peer through FindAllPeersAsync, we need to connect to it.

<pre class="brush:csharp; toolbar: false">async private void ConnectToPeer(PeerInformation peerInfo)
{
    WriteMessageText("Peer found. Connecting to " + peerInfo.DisplayName);
    try
    {
        Windows.Networking.Sockets.StreamSocket socket =
            await PeerFinder.ConnectAsync(peerInfo);

        WriteMessageText("Connection successful. You may now send messages.");
        EnableMessaging(socket);
    }
    catch (Exception err)
    {
         WriteMessageText("Connection failed: " + err.Message);
    }

    requestingPeer = null;
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 4">try
    {
        //...
    }
    catch (Exception err)
    {
         WriteMessageText("Connection failed: " + err.Message);
    }

    requestingPeer = null;
</pre>

Try to connect, if failed write a nice message to the user. Either way, since there is no longer a requesting peer, null that out.

<pre class="brush:csharp; toolbar: false; first-line: 6">Windows.Networking.Sockets.StreamSocket socket =
            await PeerFinder.ConnectAsync(peerInfo);
</pre>

Make a socket variable, and then attempt to connect using PeerFinder and ConnectAsync.

<pre class="brush:csharp; toolbar: false; first-line: 9">WriteMessageText("Connection successful. You may now send messages.");
        EnableMessaging(socket);
</pre>

If we didn''t enter the catch, it was successful! Now we just need to enable messaging like we did in Part 5.

## Step Four: Don’t be shy, say something!

We went to all this trouble to connect, now what do we do?

I guess it''s time to say something!

<pre class="brush:csharp; toolbar: false">private void SendButtonPressed(object sender, RoutedEventArgs e)
{
    if (proximitySocket != null)
    {
        SendMessageText();
    }
    else
    {
        WriteMessageText("You must enter proximity to send a message.");
    }
}
</pre>

When we hit send, check if proximitySocket has a value. If it doesn''t, let the user know they need to connect.

Otherwise, we''ll send the current text in the message box from the function in Step Five.

## Step Five: SendMessageText

<pre class="brush:csharp; toolbar: false">private async void SendMessageText()
{
    string msg = MessageTextBox.Text;

    if (msg.Length &gt; 0)
    {
        var msgLength = dataWriter.MeasureString(msg);
        dataWriter.WriteInt32(msg.Length);
        dataWriter.WriteString(msg);
        try
        {
            await dataWriter.StoreAsync();
            WriteMessageText("Message sent: " + msg);
        }
        catch (Exception e)
        {
            WriteMessageText("Send error: " + e.Message);
            CloseSocket();
        }
    }
    else
    {
        WriteMessageText("Error: Write something first, silly!");
    }
}
</pre>

#### Breakdown:

<pre class="brush:csharp; toolbar: false; first-line: 3">string msg = MessageTextBox.Text;
</pre>

Grab the current value of the MessageTextBox

<pre class="brush:csharp; toolbar: false; first-line: 5">if (msg.Length &gt; 0)
    {
        //...
    }
    else
    {
        WriteMessageText("Error: Write something first, silly!");
    }
</pre>

If the length of that message less than or equal to 0, give an error message.

<pre class="brush:csharp; toolbar: false; first-line: 4">var msgLength = dataWriter.MeasureString(msg);
        dataWriter.WriteInt32(msg.Length);
        dataWriter.WriteString(msg);
</pre>

Read the string into the dataWriter

<pre class="brush:csharp; toolbar: false; first-line: 4">try
        {
            await dataWriter.StoreAsync();
            WriteMessageText("Message sent: " + msg);
        }
        catch (Exception e)
        {
            WriteMessageText("Send error: " + e.Message);
            CloseSocket();
        }
</pre>

Attempt to StoreAsync the string. If there are any errors, give a message and close the socket.

With that, we''re able to chat!

## Step Six: Stop button

What happens when we''re done?

<pre class="brush:csharp; toolbar: false">private void StopButtonPressed(object sender, RoutedEventArgs e)
{
    _advertising = false;
    PeerFinder.Stop();
    CloseSocket();
    WriteMessageText("Stopped PeerFinder and closed socket");
}
</pre>

Stop the PeerFinder, which of course means we need to set the _advertising to false, and close the socket.

# Up next:

We have a (mostly) working application! Now we just need to add some finishing touches in part seven.

-Tobiah