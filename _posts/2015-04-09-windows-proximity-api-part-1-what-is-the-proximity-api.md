---
id: 101881
title: 'Windows Proximity API Part 1: What is the Proximity API?'
date: 2015-04-09T09:10:37+00:00
author: Tobiah
excerpt: |
  Because of a new game I’ve been working on, I spent some time messing around with NFC and the Windows Proximity API. I had not done much local network stuff before, and I thought some of you out there might be interested in learning it as well. I’ve put together a new blog series to go over the basics of the API and how to implement it.
  
  Part One: What is the Proximity API?
  The Proximity API allows you to easily establish a StreamSocket between two devices using either WiFi or Bluetooth. You can set up this connection through peer discovery, or via Near Field Communication (NFC)
  
  To learn more about the Proximity API, read on!
layout: post
guid: http://www.tobiahmarks.com/?p=101881
permalink: /2015/04/09/windows-proximity-api-part-1-what-is-the-proximity-api/
categories:
  - Tips and tricks
tags:
  - Bluetooth
  - NFC
  - Proximity API
  - Wifi Direct
---
Because of a new game I’ve been working on, I spent some time messing around with NFC and the Windows Proximity API. I had not done much local network stuff before, and I thought some of you out there might be interested in learning it as well. I’ve put together a new blog series to go over the basics of the API and how to implement it.

## Proximity API series overview

  * Part 1 – What is the Proximity API?
  * [Part 2 – Demo project setup](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-2-demo-project-setup/ "Part 2 - Demo Project Setup")
  * [Part 3 – ProximityDevice](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-3-proximitydevice/ "Part 3 - ProximityDevice")
  * [Part 4 – Expand demo project](http://www.tobiahmarks.com/2015/04/windows-proximity-api-part-4-expand-demo-project/ "Part 4 - Expand Demo Project")
  * [Part 5 – PeerFinder](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-5-peerfinder/ "Part 5")
  * [Part 6 – FindAllPeersAsync](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-6-findallpeersasync/ "Part 6")
  * [Part 7 – Final touches](http://www.tobiahmarks.com/2015/05/windows-proximity-api-part-7-final-touches/ "Part 7")
  * [Part 8 – Bonus: Proximity with the CoronaSDK](http://www.tobiahmarks.com/2015/06/windows-proximity-api-proximity-coronasdk-coronacards/ "Part 8 – Bonus: Proximity with the CoronaSDK")

I will update these links as each post is released.
  
Ready to start? Let’s first go over exactly what the Proximity API is and why you might want to use it.

# Part One: What is the Proximity API?

<!--more-->


  
The [Proximity API](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.aspx) allows you to easily set up a StreamSocket between two devices using either WiFi or Bluetooth. You can set up this connection through peer discovery, or via Near Field Communication (NFC)

### Is this for Windows 8 or Windows Phone?

Both! Although worth noting, Wifi Direct is Windows 8 only and not available on Windows Phones.

### Why would I want to use it?

If you want to have your app communicate with another device also running your app.
  
You can use it for just a quick exchange of data/information, or for a long term connection such as a multiplayer game.
  
Users can either tap their devices to connect (NFC), or use peer discovery to find other devices through Bluetooth or WiFi Direct.

### What are the requirements?

Exact requirements depend on which aspect of the Proximity API you are using.

  * Bluetooth
  * Used for peer discovery on phone
  * Pairing not required for phone to phone communication
  * Range: 10 meters or less
  * WiFi Direct
  * Used for peer discovery on PC
  * PC only! Sadly not supported on Windows Phone
  * Infrastructure WiFi (TCP/IP)
  * Must be on a shared network
  * Devices must be able to ping each other
  * Near Field Communication (NFC)
  * Used to establish connection, and acquire or exchange small content
  * Device must support NFC
  * Range: Very close/touching (less than 4 centimeters)

In all cases, you app will be required to enable the **Networking** / **Internet** and **Proximity** capabilities in your Package.appxmanifest file.

Or, if you are using Windows Phone 8.0, instead in your WMAppManifest.xml file enable:

  * `ID_CAP_NETWORKING`
  * `ID_CAP_PROXIMITY`

### What if I don’t want to use [Bluetooth/Wifi Direct/Infrastructure]?

You can enable or disable various properties with these functions

  * [PeerFinder.AllowBluetooth](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.peerfinder.allowbluetooth.aspx)
  * [PeerFinder.AllowWiFiDirect](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.peerfinder.allowwifidirect.aspx)
  * [PeerFinder.AllowInfrastructure](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.peerfinder.allowinfrastructure.aspx)

To check which discovery types are supported, you would use [PeerFinder.SupportedDiscoveryTypes](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.peerfinder.supporteddiscoverytypes.aspx)

### What classes will we be using?

  * [PeerFinder](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.peerfinder.aspx)
  * [ProximityDevice](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.proximitydevice.aspx)
  * [PeerInformation](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.peerinformation.aspx)
  * [ProximityMessage](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.proximitymessage.aspx)
  * [ConnectionRequestedEventArgs](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.connectionrequestedeventargs.aspx)
  * [TriggeredConnectionStateChangedEventArgs](http://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.proximity.triggeredconnectionstatechangedeventargs.aspx)

All the example code I will use will be in C#. However, the API also supports JavaScript, C++, and Visual Basic.

# Up next:

In part two, we will do the first setup for our Proximity Demo application in Visual Studio.

-Tobiah