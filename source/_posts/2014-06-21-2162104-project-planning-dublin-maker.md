---
id: 258
title: Hacking Weekend (1)
date: 2014-06-21T21:28:40+00:00
author: cgreene
layout: post
guid: http://thebedroomlaboratory.com/?p=258
permalink: /2014/06/21/2162104-project-planning-dublin-maker/
image: /wp-content/uploads/2014/06/HackWeekend1.jpg
categories:
  - Projects
---
## Plan

### Day 1

  * Make circuits
  * Write Arduino code 
      * nRF working
      * readings
  * Hook up camera to Pi
  * Setup laptop as server

### Day 2

  * Design of look &#8211; wireframing
  * Chat about logo
  * Finish arduino stuff
  * OpenCV
  * Web app

## AFTERmATH

### Day 1

  * Circuit making was postponed as we couldn&#8217;t locate the sensors, hopefully we&#8217;ll get to it on Day 2.
  * Arduino code writiten: 
      * We have a <a href="http://maniacbug.wordpress.com/2012/03/30/rf24network/" target="_blank">network</a> of 3 Arduino nodes tested talking to each other 🙂
      * Same as for point one above 🙂 Couldn&#8217;t get the sensors so we&#8217;ll hopefully get to it on Day 2.
      * A endeavour into getting the <a href="http://knolleary.net/arduino-client-for-mqtt/" target="_blank">Arduino mqtt library</a> working with <a href="http://maniacbug.github.io/RF24/" target="_blank">nRF24L01(+)</a> instead of <a href="http://arduino.cc/en/reference/ethernet" target="_blank">Ethernet</a> was also made.
  * The raspberry camera was <a title="setup" href="http://www.raspberrypi.org/documentation/usage/camera/" target="_blank">setup </a>and tested, with the installation of the environment to make use of the <a title="python" href="http://www.raspberrypi.org/documentation/usage/camera/python/README.md" target="_blank">python</a> library underway.
  * A laptop setup with base <a href="http://xubuntu.org/" target="_blank">xubuntu</a> with added ssh and apache2 packages is ready for setting up the rest of the server.

### Day 2

  * Mick and John made it along for day two so it was nearly all hands on deck (Greg was at the Paris Maker Faire)
  * The first item on the list was a discussion about our Github 
      * We&#8217;ve decided to break the whole project into separate repositories for each discrete module
      * We can then import each repository into the Dublin Maker repository as submodules
  * Code for Arduino was improved to add profiles for the different types of sensor/devices 
      * this is still getting tidied up and then will go into the Github
      * Victor got cracking on the research for the power strip power measurement
  * Colin made some more headway with the Pi camera
  * John set up our AWS server with node and web stuff so that we can use it as our backend
  * Mick did a really nice sketch-up for the web frontend

[<img class="alignleft size-medium wp-image-278" src="/wp-content/uploads/2014/06/maker2014_mockupv1_doorClosed-300x240.jpg" alt="maker2014_mockupv1_doorClosed" width="300" height="240" />](/wp-content/uploads/2014/06/maker2014_mockupv1_doorClosed.jpg)[<img class="alignleft size-medium wp-image-277" src="/wp-content/uploads/2014/06/maker2014_mockupv1_doorOpen-300x240.jpg" alt="maker2014_mockupv1_doorOpen" width="300" height="240" />](/wp-content/uploads/2014/06/maker2014_mockupv1_doorOpen.jpg)