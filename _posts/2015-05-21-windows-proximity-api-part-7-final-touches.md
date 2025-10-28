---
id: 102791
title: 'Windows Proximity API Part 7: Final touches'
date: 2015-05-21T14:25:18+00:00
author: DEADNAME
excerpt: |
  We are almost done! We just need to do a few more finishing touches and we'll be done with our Proximity API example.
  
  After this we'll be done. Hopefully you've learned a bit from the process of creating this.
  
  Read on for the final part of this series!
layout: post
guid: http://www.OLDURL/?p=102791
permalink: /2015/05/21/windows-proximity-api-part-7-final-touches/
categories:
  - Tips and tricks
tags:
  - Bluetooth
  - NFC
  - Proximity API
  - Wifi Direct
---
We are almost done! We just need to do a few more finishing touches and we''ll be done with our Proximity API example.

## Proximity API series overview

  * [Part 1 – What is the Proximity API?](http://www.OLDURL/2015/04/windows-proximity-api-part-1-what-is-the-proximity-api/ "Part 1 – What is the Proximity API?")
  * [Part 2 – Demo project setup](http://www.OLDURL/2015/04/windows-proximity-api-part-2-demo-project-setup/ "Part 2 - Demo project setup")
  * [Part 3 – ProximityDevice](http://www.OLDURL/2015/04/windows-proximity-api-part-3-proximitydevice/ "Part 3 – ProximityDevice")
  * [Part 4 – Expand demo project](http://www.OLDURL/2015/04/windows-proximity-api-part-4-expand-demo-project/ "Part 4 – Expand demo project")
  * [Part 5 – PeerFinder](http://www.OLDURL/2015/05/windows-proximity-api-part-5-peerfinder/ "Part 5 - PeerFinder")
  * [Part 6 – FindAllPeersAsync](http://www.OLDURL/2015/05/windows-proximity-api-part-6-findallpeersasync/ "Part 6- FindAllPeersAsync")
  * Part 7 – Final touches
  * [Part 8 – Bonus: Proximity with the CoronaSDK](http://www.OLDURL/2015/06/windows-proximity-api-proximity-coronasdk-coronacards/ "Part 8 – Bonus: Proximity with the CoronaSDK")

# Part Seven: Final touches

<!--more-->

## Step One: Dispose

As I''ve been repeating this whole time, have to clean up after ourselves! We need to do so in a couple of places, so let''s make a dispose function in our `MainPage` class in **MainPage.xaml.cs**.

<pre class="brush:csharp; toolbar: false">public void Dispose()
{ 
    PeerFinder.Stop();
    _advertising = false;

    CloseSocket(); //Cleans up proximitySocket and dataWriter

    if (_proximityDevice != null)
    {
        if (_subscribedMessageID != -1) //Stop Subscribing
        {
            _proximityDevice.StopSubscribingForMessage(_subscribedMessageID);
            _subscribedMessageID = -1;
        }
        if (_publishedMessageID != -1) //Stop publishing
        {
            _proximityDevice.StopPublishingMessage(_publishedMessageID);
            _publishedMessageID = -1;
        }
    }
}
</pre>

Similar to the cleanup code we''ve been including in other parts of the program, but all mashed together.

## Step Two: SuspendingEventHandler

What if the user suspends the app? We want to make sure we break our connection.

In the MainPage constructor, add the following line before we get our ProximityDevice.

<pre class="brush:csharp; toolbar: false">Application.Current.Suspending += new SuspendingEventHandler(OnSuspending);
</pre>

Then add the following function to our MainPage class:

<pre class="brush:csharp; toolbar: false">private void OnSuspending(Object sender, Windows.ApplicationModel.SuspendingEventArgs e)
{
    WriteMessageText("App is suspending, disposing");

    Dispose();
}
</pre>

## Step Three: OnNavigatingFrom

What if the user navigates away from the app? Again, we want to break the connection. This time we need a special function, add to the bottom of our MainPage class:

<pre class="brush:csharp; toolbar: false">protected override void OnNavigatingFrom(NavigatingCancelEventArgs e)
{
    Dispose();
} 
</pre>

Now you might be wondering why we add this if OnNavigatingForm is not called in this demo app.

Well, it''s true we don''t need it. But, it''s good practice to include this anyway, in case in some point in the future you do need it and forget to go back and add it.

# Finished!

We now have a finished application!

Hopefully you''ve learned a bit from the process of creating this. From here, you should be able to integrate the Proximity API in your own applications.

Of course, if you ever have any questions, please [contact me](http://www.OLDURL/contact/) and let me know!

## Full Sample Code

For reference, here is a completed **MainPage.xaml** file:

<pre class="brush:xml; toolbar: false">&lt;Page
    x:Class="ProximityDemo.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:ProximityDemo"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}"&gt;

    &lt;!-- Top part of grid is pivot view of controls, bottom is output text --&gt;
    &lt;Grid&gt;  
        &lt;Grid.RowDefinitions&gt;
            &lt;RowDefinition Height="Auto"/&gt;
            &lt;RowDefinition Height="*"/&gt;
        &lt;/Grid.RowDefinitions&gt;
        &lt;Pivot Title="Proximity API Demos" Grid.Row="0" SelectionChanged="PivotChanged"&gt;
            &lt;PivotItem Header="ProximityDevice"&gt;
                &lt;StackPanel Orientation="Vertical"&gt;
                    &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center"&gt;
                        &lt;TextBox x:Name="TapMessageTextBox" Text="Hello World!" Width="256"/&gt;
                    &lt;/StackPanel&gt;
                    &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center"&gt;
                        &lt;Button x:Name="PublishButton" Content="Publish" Margin="5,0,5,0"
                                    Click="PublishButtonPressed" /&gt;
                        &lt;Button x:Name="StopPublishingButton" Content="Stop Publishing" Margin="5,0,5,0"
                                    Click="StopPublishingButtonPressed" /&gt;
                    &lt;/StackPanel&gt;
                    &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center"&gt;
                        &lt;Button x:Name="SubscribeButton" Content="Subscribe" Margin="5,0,5,0"
                                    Click="SubscribeButtonPressed" /&gt;
                        &lt;Button x:Name="StopSubscribingButton" Content="Stop Subscribing" Margin="5,0,5,0"
                                    Click="StopSubscribingButtonPressed" /&gt;
                    &lt;/StackPanel&gt;
                &lt;/StackPanel&gt;
            &lt;/PivotItem&gt;
            &lt;PivotItem Header="PeerFinder"&gt;
                &lt;StackPanel Orientation="Vertical"&gt;
                    &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center"&gt;
                        &lt;TextBox x:Name="DisplayNameTextBox" Width="225"/&gt;
                        &lt;Button x:Name="AdvertiseButton" Content="Advertise" Margin="10,0,0,0"
                                Click="AdvertiseButtonPressed" /&gt;
                    &lt;/StackPanel&gt;
                    &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center"&gt;
                        &lt;TextBox x:Name="MessageTextBox" Text="Hello World!" Width="225"/&gt;
                        &lt;Button x:Name="SendButton" Content="Send" Margin="10,0,0,0"
                                Click="SendButtonPressed" /&gt;
                    &lt;/StackPanel&gt;
                    &lt;StackPanel Orientation="Horizontal" HorizontalAlignment="Center"&gt;
                        &lt;Button x:Name="Find" Content="Find" Margin="5,0,5,0"
                                    Click="FindButtonPressed" /&gt;
                        &lt;Button x:Name="StopButton" Content="Stop" Margin="5,0,5,0"
                                    Click="StopButtonPressed" /&gt;
                        &lt;Button x:Name="AcceptButton" Content="Accept" Margin="5,0,5,0"
                                    Click="AcceptButtonPressed" /&gt;
                    &lt;/StackPanel&gt;
                &lt;/StackPanel&gt;
            &lt;/PivotItem&gt;
        &lt;/Pivot&gt;
        &lt;ScrollViewer Grid.Row="1"&gt;
            &lt;TextBlock x:Name="MessageBlock" FontSize="18" TextWrapping="WrapWholeWords"
                       Text="Welcome to Proximity API Demos!
Swipe to switch between examples."
                       VerticalAlignment="Top" Margin="10,0,10,0" /&gt;
        &lt;/ScrollViewer&gt;
    &lt;/Grid&gt;

&lt;/Page&gt;
</pre>

Now for the completed **MainPage.xaml.cs** file:

<pre class="brush:csharp; toolbar: false">using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Runtime.InteropServices.WindowsRuntime;
using Windows.Foundation;
using Windows.Foundation.Collections;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Controls.Primitives;
using Windows.UI.Xaml.Data;
using Windows.UI.Xaml.Input;
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Navigation;

// Add Proxmity API on top of defaults
using Windows.Networking.Proximity;

namespace ProximityDemo
{
    /// &lt;summary&gt;
    /// A page that showcases use of the Proximity API
    /// &lt;/summary&gt;
    public sealed partial class MainPage : Page
    {
        #region General elements

        #region General variables

        // Last pivot index
        private int current_pivot_index = 0;
        // Dispatcher for messages we display to the screen
        private Windows.UI.Core.CoreDispatcher messageDispatcher = Window.Current.CoreWindow.Dispatcher;

        #endregion //Variables

        /// &lt;summary&gt;
        /// Page constructor
        /// &lt;/summary&gt;]
        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;

            Application.Current.Suspending += new SuspendingEventHandler(OnSuspending);
 
            #region ProximityDevice example initialization
            //For sending and receiving messages
            _proximityDevice = ProximityDevice.GetDefault();
            if (_proximityDevice == null)
            {
                WriteMessageText("Failed to initialized proximity device.\n" +
                                 "Your device may not have proximity hardware.");
            }
            #endregion
        }

        /// &lt;summary&gt;
        /// Writes a message to MessageBlock on the UI thread.
        /// &lt;/summary&gt;
        /// &lt;param name="message"&gt;The message to be added. Automatically includes a new line.&lt;/param&gt;
        /// &lt;param name="overwrite"&gt;Should this message clear all the other messages from the screen?&lt;/param&gt;
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

        /// &lt;summary&gt;
        /// Invoked when Pivot element is changed/swiped.
        /// Sets up the next example, cleans up the last example.
        /// &lt;/summary&gt;
        private void PivotChanged(object sender, SelectionChangedEventArgs e)
        {
            switch (current_pivot_index)
            {
                case 0: //Leaving Proximity Device demo
                    StopSubscribingButtonPressed(null, null);
                    StopPublishingButtonPressed(null,null);
                    break;
                case 1: //Leaving Proximity Finder demo
                    // Detach the callback handler (there can only be one PeerConnectProgress handler).
                    PeerFinder.TriggeredConnectionStateChanged -= TriggeredConnectionStateChanged;
                    // Detach the incoming connection request event handler.
                    PeerFinder.ConnectionRequested -= ConnectionRequested;
                    if (_advertising)
                    {
                        PeerFinder.Stop();
                        CloseSocket();
                        _advertising = false;
                    }
                    WriteMessageText("Stopping PeerFinder");
                    break;
            }

            current_pivot_index = (((Pivot)sender).SelectedIndex);

            #region PeerFinder socket example initialization/deconstructor
            if (current_pivot_index == 1) // Initialize PeerFinder.
            {
                // If supported, add handler
                if ((PeerFinder.SupportedDiscoveryTypes & PeerDiscoveryTypes.Triggered) == PeerDiscoveryTypes.Triggered)
                {
                    PeerFinder.TriggeredConnectionStateChanged += TriggeredConnectionStateChanged;
                }
                PeerFinder.ConnectionRequested += ConnectionRequested;
                WriteMessageText("Starting PeerFinder");
            }
            #endregion
        }

        /// &lt;summary&gt;
        /// Invoked when leaving this page. Clean up our variables
        /// NOTE: If MainPage is only page, this is not invoked!
        /// &lt;/summary&gt;
        protected override void OnNavigatingFrom(NavigatingCancelEventArgs e)
        {
            Dispose();
        }

        /// &lt;summary&gt;
        /// Invoked when app suspends. Clean up our variables
        /// &lt;/summary&gt;
        private async void OnSuspending(Object sender, Windows.ApplicationModel.SuspendingEventArgs e)
        {
            WriteMessageText("App is suspending, disposing");

            Dispose();
        }

        /// &lt;summary&gt;
        /// Dispose of this page 
        /// &lt;/summary&gt;
        public void Dispose()
        {

            PeerFinder.Stop();
            _advertising = false;

            CloseSocket(); //Cleans up proximitySocket and dataWriter

            if (_proximityDevice != null)
            {
                if (_subscribedMessageID != -1) //Stop Subscribing
                {
                    _proximityDevice.StopSubscribingForMessage(_subscribedMessageID);
                    _subscribedMessageID = -1;
                }
                if (_publishedMessageID != -1) //Stop publishing
                {
                    _proximityDevice.StopPublishingMessage(_publishedMessageID);
                    _publishedMessageID = -1;
                }
            }
        }

        #endregion //General elements

        #region ProximityDevice example

        #region ProximityDevice variables

        // Proximity Device
        private ProximityDevice _proximityDevice;
        // Published Message ID
        private long _publishedMessageID = -1;
        // Subscribed Message ID
        private long _subscribedMessageID = -1;

        #endregion //Variables

        #region ProximityDevice functions

        /// &lt;summary&gt;
        /// Invoked when a message is received
        /// &lt;/summary&gt;
        /// &lt;param name="device"&gt;The ProximityDevice object that received the message.&lt;/param&gt;
        /// &lt;param name="message"&gt;The message that was received.&lt;/param&gt;
        private void messageReceived(ProximityDevice device, ProximityMessage message)
        {
            WriteMessageText("Message received: " + message.DataAsString);
        }

        #endregion //ProximityDevice functions

        #region ProximityDevice example buttons
        /// &lt;summary&gt;
        /// When the Subscribe button is pressed, start listening for other devices.
        /// &lt;/summary&gt;
        private void SubscribeButtonPressed(object sender, RoutedEventArgs e)
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

        /// &lt;summary&gt;
        /// When the stop subscribing button is pressed, stop listening for other devices.
        /// &lt;/summary&gt;
        private void StopSubscribingButtonPressed(object sender, RoutedEventArgs e)
        {
            if (_subscribedMessageID != -1)
            {
                _proximityDevice.StopSubscribingForMessage(_subscribedMessageID);
                _subscribedMessageID = -1;
                WriteMessageText("Stopped subscribing");
            }
        }

        /// &lt;summary&gt;
        /// When the Publish button is pressed, start broadcasting a message on the Windows.ExampleMessage channel.
        /// &lt;/summary&gt;
        private void PublishButtonPressed(object sender, RoutedEventArgs e)
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

        /// &lt;summary&gt;
        /// When the stop publishing button is pressed, stop broadcasting.
        /// &lt;/summary&gt;
        private void StopPublishingButtonPressed(object sender, RoutedEventArgs e)
        {
            if (_publishedMessageID != -1)
            {
                _proximityDevice.StopPublishingMessage(_publishedMessageID);
                _publishedMessageID = -1;
                WriteMessageText("Stopped publishing");
            }
        }
        #endregion //ProximityDevice example buttons

        #endregion //ProximityDevice example

        #region ProximityFinder example

        #region ProximityFinder variables

        // Handle external connection requests.
        PeerInformation requestingPeer;
        // Current peer socket and datawriter
        Windows.Networking.Sockets.StreamSocket proximitySocket;
        Windows.Storage.Streams.DataWriter dataWriter;
        // Are we currently advertising?
        bool _advertising = false;

        #endregion //Variables

        #region ProximityFinder functions

        /// &lt;summary&gt;
        /// Invoked when this page is about to be displayed in a Frame.
        /// Set the default value for the Display Name textbox
        /// &lt;/summary&gt;
        /// &lt;param name="e"&gt;Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.&lt;/param&gt;
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            // Prepare Proximity Finder example device name textbox
            DisplayNameTextBox.Text = PeerFinder.DisplayName;

        }

        /// &lt;summary&gt;
        /// Handler for when the connection state changes
        /// &lt;/summary&gt;
        private void TriggeredConnectionStateChanged(object sender, TriggeredConnectionStateChangedEventArgs e)
        {
            if (e.State == TriggeredConnectState.PeerFound)
            {
                WriteMessageText("Peer found. You may now pull your devices out of proximity.");
            }
            if (e.State == TriggeredConnectState.Completed)
            {
                WriteMessageText("You are now connected and may exchange messages!");
                EnableMessaging(e.Socket);
            }
        }

        /// &lt;summary&gt;
        /// When another device requests a connection, tell us!
        /// &lt;/summary&gt;
        private void ConnectionRequested(object sender, ConnectionRequestedEventArgs e)
        {
            requestingPeer = e.PeerInformation;
            WriteMessageText("Connection requested by " + requestingPeer.DisplayName + ". " +
                "Click 'Accept Connection' to connect.");
        }

        /// &lt;summary&gt;
        /// Connect to a peer
        /// &lt;/summary&gt;
        /// &lt;param name="peerInfo"&gt;Information about the peer requesting to connect.&lt;/param&gt;
        async private void ConnectToPeer(PeerInformation peerInfo)
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

        /// &lt;summary&gt;
        /// Define socket and data writer for sending and reading messages.
        /// &lt;/summary&gt;
        private void EnableMessaging(Windows.Networking.Sockets.StreamSocket socket)
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

        /// &lt;summary&gt;
        /// Read out and print messages from the DataReader
        /// &lt;/summary&gt;
        /// &lt;param name="reader"&gt;The current DataReader&lt;/param&gt;
        private async void StartReader( Windows.Storage.Streams.DataReader reader )
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

        /// &lt;summary&gt;
        /// Close the reader, triggered from the StartReader function
        /// &lt;/summary&gt;
        /// &lt;param name="reader"&gt;The current DataReader&lt;/param&gt;
        /// &lt;param name="err"&gt;The error message (default blank)&lt;/param&gt;
        private void CloseReader( Windows.Storage.Streams.DataReader reader, string err = "")
        {
            WriteMessageText("The peer app closed the socket. "+err);
            reader.Dispose();
            CloseSocket();
        }

        /// &lt;summary&gt;
        /// Close the current socket and datawriter
        /// &lt;/summary&gt;
        private void CloseSocket()
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

        /// &lt;summary&gt;
        /// Send the current message to peer
        /// &lt;/summary&gt;
        private async void SendMessageText()
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

        #endregion //ProximityFinder functions

        #region ProximityFinder example buttons

        /// &lt;summary&gt;
        /// When the Advertise button is pressed, start to advertise for peers.
        /// Display an message if "Discovery" or "Tap" types are not supported.
        /// &lt;/summary&gt;
        private void AdvertiseButtonPressed(object sender, RoutedEventArgs e)
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

        /// &lt;summary&gt;
        /// When the Find button is pressed, find other devices advertising their connections.
        /// &lt;/summary&gt;
        async private void FindButtonPressed(object sender, RoutedEventArgs e)
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

        /// &lt;summary&gt;
        /// When the Accept button is pressed, agree to connect to a peer whose request we have already received.
        /// &lt;/summary&gt;
        private void AcceptButtonPressed(object sender, RoutedEventArgs e)
        {
            if (requestingPeer == null)
            {
                WriteMessageText("No peer connection has been requested.");
                return;
            }

            ConnectToPeer(requestingPeer);
        }

        /// &lt;summary&gt;
        /// When the Stop button is pressed, stop advertising and close sockets
        /// &lt;/summary&gt;
        private void StopButtonPressed(object sender, RoutedEventArgs e)
        {
            _advertising = false;
            PeerFinder.Stop();
            CloseSocket();
            WriteMessageText("Stopped PeerFinder and closed socket");
        }

        /// &lt;summary&gt;
        /// When the Send button is pressed, call SendMessageText.
        /// &lt;/summary&gt;
        private void SendButtonPressed(object sender, RoutedEventArgs e)
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

        #endregion //ProximityFinder example buttons

        #endregion //ProximityFinder example
    }
}
</pre>

## Completed Proximity API Project

If you''d like the latest code in case this example is ever updated, or you want the complete visual studio project, you can get it [from my GitHub](https://github.com/DEADNAMEZ/ProximityDemo).

# Up next:

The main tutorial may be finished, but I''m going to squeeze in a bonus!

In the bonus, I''ll go over how to include the Proximity API in a Corona based application.

-DEADNAME