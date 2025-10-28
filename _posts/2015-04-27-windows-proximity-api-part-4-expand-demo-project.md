---
id: 102081
title: 'Windows Proximity API Part 4: Expand demo project'
date: 2015-04-27T13:00:59+00:00
author: DEADNAME
excerpt: |
  Now that we have ProximityDevice working, we have to get ready for the PeerFinder example. Like before, this part isn’t specific to the Proximity API, but will expand our demo application to run the example code coming up in part five, six, and seven.
  
  Read on for full instructions!
layout: post
guid: http://www.OLDURL/?p=102081
permalink: /2015/04/27/windows-proximity-api-part-4-expand-demo-project/
categories:
  - Tips and tricks
tags:
  - Bluetooth
  - NFC
  - Proximity API
  - Wifi Direct
---
Now that we have ProximityDevice working, we have to get ready for the PeerFinder example. Like before, this part isn’t specific to the Proximity API, but will expand our demo application to run the example code coming up in part five, six, and seven.

## Proximity API series overview

  * [Part 1 – What is the Proximity API?](http://www.OLDURL/2015/04/windows-proximity-api-part-1-what-is-the-proximity-api/ "Part 1")
  * [Part 2 – Demo project setup](http://www.OLDURL/2015/04/windows-proximity-api-part-2-demo-project-setup/ "Part 2")
  * [Part 3 – ProximityDevice](http://www.OLDURL/2015/04/windows-proximity-api-part-3-proximitydevice/ "Part 3")
  * Part 4 – Expand demo project
  * [Part 5 – PeerFinder](http://www.OLDURL/2015/05/windows-proximity-api-part-5-peerfinder/ "Part 5")
  * [Part 6 – FindAllPeersAsync](http://www.OLDURL/2015/05/windows-proximity-api-part-6-findallpeersasync/ "Part 6")
  * [Part 7 – Final touches](http://www.OLDURL/2015/05/windows-proximity-api-part-7-final-touches/ "Part 7")
  *Part 8 – Bonus: Proximity with the CoronaSDK</li> </ul> 
    
    # Part Four: Expand demo project
    
    <!--more-->
    
    ## Step one: More XAML!
    
    Continuing from part 2, we need to add a few more lines of code to the **MainPage.xaml** file''s `<Pivot>` element.
    
    Right after the `<PivotItem>`, add the following:
    
    <pre class="brush:xml; toolbar: false">&lt;PivotItem Header="PeerFinder"&gt;
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
</pre>
    
    Now we have two `<PivotItem>`&#8216;s for our Pivot table. This one has more buttons! We''ll go over what they do in part five.
    
    ## Step Two: Pivot change
    
    You may remember that in part two, we added the parameter `SelectionChanged="PivotChanged"` to `<Pivot>`
    
    This is a function that is triggered whenever the user swipes left/right on their device and moves to a new PivotItem. Before, it was never triggered since we only had one element. Now that we have two, we ought to define it.
    
    Back to **MainPage.xaml.cs**, add the following within the `MainPage` class
    
    <pre class="brush:csharp; toolbar: false">// Last pivot index
private int current_pivot_index = 0;

/// 
/// Invoked when Pivot element is changed/swiped.
/// Sets up the next example, cleans up the last example.
/// 
private void PivotChanged(object sender, SelectionChangedEventArgs e)
{
    switch (current_pivot_index)
    {
        case 0: //Leaving Proximity Finder demo
            break;
        case 1: //Leaving Proximity Device demo
            break;
    }

    current_pivot_index = (((Pivot)sender).SelectedIndex);

    if (current_pivot_index == 1)
    {
        //Initialize PeerFinder.
    }
}
</pre>
    
    #### Breakdown:
    
    <pre class="brush:csharp; toolbar: false; first-line: 1">// Last pivot index
private int current_pivot_index = 0;
</pre>
    
    Creates a class variable that keeps track of which pivot index we are on. Starts with 0, as does the index.
    
    <pre class="brush:csharp; toolbar: false; first-line: 10">switch (current_pivot_index)
{
    case 0: //Leaving Proximity Device demo
        break;
    case 1: //Leaving Proximity Device demo
        break;
}
</pre>
    
    The skeleton code that will trigger when we switch pivots. Whatever the value of current\_pivot\_index is, that is the pivot we are leaving as we haven''t set the new value yet.
    
    Later, we''ll write some cleanup code here.
    
    <pre class="brush:csharp; toolbar: false; first-line: 18">current_pivot_index = (((Pivot)sender).SelectedIndex);
</pre>
    
    Set the current value to the index.
    
    <pre class="brush:csharp; toolbar: false; first-line: 20">if (current_pivot_index == 1)
{
    //Initialize PeerFinder.
}
</pre>
    
    Now that we have arrived at a new index, we can run any initialization code we need. ProximityDevice doesn''t happen to need any, but PeerFinder does!
    
    Skeleton code for now, we''ll fill it out in part five.
    
    ## Step three: Clean up PeerDevice
    
    Always remember to clean up your code when you are done with something! This is extra important when handling things that use the device''s hardware, as it could cause bugs or drain battery life.
    
    In the switch statement we just created above, add the following to case 0 (when we leave the ProximityDevice demo):
    
    <pre class="brush:csharp; toolbar: false; first-line: 22">case 0: //Leaving Proximity Device demo
    StopSubscribingButtonPressed(null, null);
    StopPublishingButtonPressed(null,null);
    break;
</pre>
    
    Since we already have nice functions to stop Subscribing/Publishing ready to go with button presses, we can trigger those same functions here.
    
    ## Step four: Initialize DisplayNameTextBox
    
    We have a new textbox for PeerFinder! This is going to display the name of the device. Let''s give it an initial value.
    
    Replace your `OnNavigatedTo` function with the following:
    
    <pre class="brush:csharp; toolbar: false">protected override void OnNavigatedTo(NavigationEventArgs e)
{
    // Prepare Proximity Finder example device name textbox
    DisplayNameTextBox.Text = PeerFinder.DisplayName;

}
</pre>
    
    DisplayNameTextBox is the name we gave it in the XAML in step one. PeerFinder.DisplayName gives us the name of the device, but since it is in a text box can tweak it to any name we want at runtime.
    
    # Up next:
    
    In part five, we''ll start making these new XAML elements do stuff and connect to a peer using NFC and PeerFinder.
    
    -DEADNAME