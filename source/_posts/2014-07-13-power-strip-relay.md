---
id: 304
title: 'Power Strip - Relay'
date: 2014-07-13T14:01:47+00:00
author: vykta
layout: post
guid: http://thebedroomlaboratory.com/?p=304
permalink: /2014/07/13/power-strip-relay/
image: /wp-content/uploads/2014/07/Relay-On1.jpg
categories:
  - Projects
---
Having worked on the voltage and current meter previously, this time around the relay was the focus of attention. Although I was initially worried about working with mains power (240v), I mitigated the fears by using an adapter that limited the risk to 12v.

The circuit and code were pretty straight forward to get to grips with, although my search skills were weak today as I couldn't find a complete pin-out for the Keyes_SR1y relay that I was working with, the closest I could get was <a title="a diagram" href="http://www.dx.com/p/arduino-5v-relay-module-blue-black-121354#.U8KIYlEyApK" target="_blank">a diagram</a> showing the Arduino related side only. Luckily it turns out that the power side of it is pretty straight forward: whatever is in the middle is connected to one side or the other depending on the Arduino input being High or Low.

I have checked the <a href="https://github.com/thebedroomlaboratory/Maker2014" target="_blank">code into github</a>, which, like the screenshot shows,

[<img class="aligncenter size-medium wp-image-305" src="/wp-content/uploads/2014/07/Relay-Screenshot-300x187.png" alt="Relay-Screenshot" width="300" height="187" />](/wp-content/uploads/2014/07/Relay-Screenshot.png)sends a High signal to the Relay when a 1 (49) is sent - via Serial Input and when a 0 (48) is sent, a Low signal is sent. Effectually turning the power on:

[<img class="aligncenter size-medium wp-image-306" src="/wp-content/uploads/2014/07/Relay-On-263x300.jpg" alt="Relay-On" width="263" height="300" />](/wp-content/uploads/2014/07/Relay-On.jpg)and off:

[<img class="aligncenter size-medium wp-image-307" src="/wp-content/uploads/2014/07/Relay-Off--300x261.jpg" alt="Relay-Off" width="300" height="261" />](/wp-content/uploads/2014/07/Relay-Off-.jpg)respectively.

The next step is to merge the meter and relay code and finally to link up the power meter to the automation station.

Bring on <a href="http://www.dublinmaker.ie/" target="_blank">Dublin Maker</a>.