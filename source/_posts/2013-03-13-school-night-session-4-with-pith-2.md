---
id: 187
title: 'School Night Session #4 - WITH PITH 2'
date: 2013-03-13T23:31:19+00:00
author: gregario
layout: post
guid: http://thebedroomlaboratory.com/?p=187
permalink: /2013/03/13/school-night-session-4-with-pith-2/
image: /wp-content/uploads/2013/03/2013-03-13-21.20.02-Medium1.jpg
categories:
  - Projects
---
We've begun the second run at the WITH PITH people counter. We've been learning how to bootload arduinos for the last hour, the following tutorial was really helpful! See the main photo above.

http://arduino.cc/en/Tutorial/ArduinoToBreadboard

We have two bootloaded ATMEGA 328p's to test with now. Martin is working on getting the low power modes to respectable levels to that the device will run for a long time off the battery and Greg is working on making the IR receiver throw an interrupt when it receives a signal...

[ ](/wp-content/uploads/2013/03/2013-03-13-21.20.02-Medium.jpg)

**Update 22:54 **

Martins been playing with watchdog timers and we think we could get it down to 6uA in sleep mode, seriously low power.
  
Greg built a basic EE101 style analogue circuit to start seeing current consumption.

We started with this circuit:
  
![Capture](/wp-content/uploads/2013/03/Capture.png)

Which in real life looks like this:
  
![20130313_230246 (Medium)](/wp-content/uploads/2013/03/20130313_230246-Medium-300x225.jpg)

So the bit on the left is the infrared LED and the bit on the right is the phototransistor. Putting your hand in the middle and breaking the beam would be just like someone walking through a door. This induces a voltage change on the line marked output. We played with the passives and got the 360uA... A good start for a proof of concept!

** Update 23:51**

So we've been operating under the assumption that we would have two power units with two power supplies and two sets of timing. Using the millis() function was the only was to count between pulses to see if consecutive beam pulses had been blocked in this system.This went at odds with our need for low power and our hope for a 6-9 month lifetime! So playing around with different options we went back to the one unit idea for all the intelligence.

This was a bit of a brick wall, we started thinking about single units. We started thinking about the reflector idea where the transmitter and receiver were on the same unit facing out and there was a mirror directly opposite. We didn't like this though, the power needed to reach the opposite end and back would be double the original way and also we couldn't be sure that at these power levels it wouldn't reflect back from the person walking past the door and not be counted as a beam break.

Then we started thinking about speakers. In particular their wires. Then we started thinking about windscreens and realised we had gone off topic. But then we started thinking about speakers again and decided we would just wire the transmitter around the frame of the door using speaker wire. This idea made martin do his happy dance:

![20130313_230546 (Medium)](/wp-content/uploads/2013/03/20130313_230546-Medium-225x300.jpg)
  
Its such a blurry dance!

So we got going making a very long wire, which looked something like this:

![20130313_231651 (Medium)](/wp-content/uploads/2013/03/20130313_231651-Medium-225x300.jpg)



We made about 8ft of wire, for testing over distance. We found that using 1kOhm resister in series with the IR led was enough to be detected by the receiver. This is good as it consumes less power.

We're taking the bits of code and putting something together to test this now, our time is up (its 00:33 here and its a school night!!!) so we'll document code and put up schematics on Github tomorrow. Don't want to get you overly excited but the system seems to be working a treat 🙂