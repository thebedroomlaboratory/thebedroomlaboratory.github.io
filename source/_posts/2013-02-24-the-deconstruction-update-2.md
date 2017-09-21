---
id: 140
title: 'The Deconstruction - Update 2'
date: 2013-02-24T22:49:48+00:00
author: gregario
layout: post
guid: http://thebedroomlaboratory.com/?p=140
permalink: /2013/02/24/the-deconstruction-update-2/
image: /wp-content/uploads/2013/02/2013-02-24-20.04.021.jpg
categories:
  - Blog
---
So we have the sensor reading temperature and light!

So what is the reason we included light you may ask o gentle reader?
  
I mentioned it talking to the deconstruction that heating in your home accounts for 33% of your energy use, well it turns out so does the lighting in your home. So 66% of your energy usage is tied up in these two thing, having them monitored and controlled is a good thing!

So we have our Raspberry Pi running off what we learned from our testbed.
  
As an aside our testbed consisted of 3 Raspberry Pi’s running over our home network so we could do all the programming we needed to from our laptops without tripping over eachother! We’ve ported all our code to the one “web enabled thermostat” and its up and running.

# So what does it do?

- Uses a sensor to measure light and temperature
  
- This is sent via serial to the raspberry pi which takes it in via Python
  
- The Python does all the control logic, deciding when the heating should be on and off, saving you money an keeping you warm!!!
  
- We’re using the GPIO on the raspberry Pi to trigger an LED (in place of a relay for our  existing thermostat)
  
- Theres a boost button on the GPIO too, in case someone felt chilly and wanted to turn on their heating manually
  
-  then the Raspberry Pi is a web server also, allowing to see if the heating is on and what temperature/light level your home is
  
- the site is mobile optimised, as checking on your phone is the easiest way to do these things!

We wanted to actually control our heating in the apartment, renting we felt playing with gas boilers may be an ever so slightly dangerous so we simulated with an LED, same difference from the outset, with the right relay (not in our box of tricks unfortunately) the logic doesn’t need to be changed. I’ll include how to do this in our documentation.

Also on the display, we had intended to do a display on the physical sensor so people could check and see in real time if they pressed the boost button. Greg, got the code working, schematic designed but managed to break the physical connector to the screen the nokia. He also set the Zigbee on fire… He is a man who has taken the word deconstruction a bit literally.

![2013-02-24 19.48.22](http://thedeconstruction.org/wp-content/uploads/2013/02/2013-02-24-19.48.22-300x225.jpg)

The square on the left should be connected to the black wires. It isn’t…

# What have we actually done!

It works and we’re delighted! We’ve developed a web enabled thermostat, which will be documented and released open source for everyone to use, out of our components spares box in 40 hours! Some pictures for your viewing pleasure.

![Capture1](http://thedeconstruction.org/wp-content/uploads/2013/02/Capture1-265x300.png)

The mobile website! It displays temperature along with a picture to say what the thermostat is doing.
  
- The sun means that the room is too warm and the heating is therefore turned off
  
- The leaf means that you are in your ideal zone, 18-22 degrees, we chose a leaf as keeping the system in this zone saves you money and is environmentally friendly
  
- there’s also a snowflake for when it is too cold and therefore the heating is turned on. (I couldn’t grab a shot of that as the room is really warm)

Here’s a pic of the sensor/webserver:

![2013-02-24 20.04.15](http://thedeconstruction.org/wp-content/uploads/2013/02/2013-02-24-20.04.15-225x300.jpg)

So the top Raspberry Pi is talking to the arduino, which is doing the heavy lifting re the sensors. I won’t go into detail here as we’re going to put up documentation separately! So we’d call this project a success (and look forward to our laser cutter [:)](http://thedeconstruction.org/wp-includes/images/smilies/icon_smile.gif) ). Seriously though, we learned a lot and had a good time. Good work team deconstruction!!!!

We’re polishing code, documenting and finishing everything off for the upload tomorrow. Had a great time and we hope people use our work to make it even better and learn themselves.

<em id="__mceDel"> [](http://thedeconstruction.org/wp-content/uploads/2013/02/DSC02622.jpg)</em>

So from (left to right) Greg, Martin, John, Colin and John… Thanks for watching and keep watching the stores… eh, I mean stars.