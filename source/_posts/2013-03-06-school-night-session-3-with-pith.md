---
id: 152
title: 'School Night Session #3 &#8211; WITH PITH'
date: 2013-03-06T21:16:39+00:00
author: gregario
layout: post
guid: http://thebedroomlaboratory.com/?p=152
permalink: /2013/03/06/school-night-session-3-with-pith/
image: /wp-content/uploads/2013/03/crowd1.jpg
categories:
  - Projects
  - School Night Sessions
---
Tonight we are going to design a people counter for entering and exiting rooms.
  
We&#8217;re going to call it the WITH PITH (Who&#8217;s in the House, People in the House)

We&#8217;re going to go for an IR transmitter receiver pair where it counts a person every time the beam is interrupted.
  
We&#8217;re going to aim for the following features:
  
&#8211; Battery Powered
  
&#8211; Two units, a transmitter and a receiver pair
  
&#8211; Screen to display the number of people coming into the room
  
&#8211; Buttons to reset the counter and turning off and on the screen

As we go we&#8217;re going to have to revisit this list, as we want it to be battery powered it will need to be ultra low power, so certain features may get &#8220;sidelined&#8221;&#8230; or dumped really!

Martin will start designing the transmitter and Greg will work on the receiver.
  
Will keep you updated.

<!--more-->

### Update &#8211; End of session

So after an evening of planning and tea, we have looked into a few different options for the device:

  1. The simplest way of implementing the device is to have an IR LED on one side of a doorway and a photo-transistor on the other to detect something breaking the beam. This would not be very well protected from IR interference from other sources though.
  2. A slightly more complex method is to send bursts of 38 kHz light from the IR LED periodically and then use a 38 kHz IR receiver (probably the TSOP28238) to receive these and cause an interrupt on the microcontroller. This means more sleep time for microcontroller, less transmission time for the LED and higher protection against external sources of IR light.

We&#8217;re thinking of trying both options out on a breadboard and comparing the power consumption and capabilities of each. From there we can go ahead and design and order some PCBs (looking at itead for this). For approach two we&#8217;d be adapting the circuit shown at http://pcbheaven.com/circuitpages/Long\_Range\_IR\_Beam\_Break_Detector/ for our transmission purposes, maybe with a CMOS 556 timer and a higher burst interval. While the tutorial on that site also has a reception circuit, we will just be hooking up the 38 kHz IR receiver to our 328p microcontroller. We think it&#8217;d be nice to singleboard the whole thing or to make it as a shield for our upcoming low-powered arduino (with pro mini footprint).

Anyway, we&#8217;re gonna go ahead and get the parts in for testing out this stuff. I think the plan is to continue this in next week&#8217;s school night session when we have all the stuff here to actually build the circuits on breadboards. In the meantime Greg is going to work on some circuit drawings for the low-powered arduino and the WITH PITH, while Martin is getting started on component pricing and ordering. Tune in next week for more!