---
id: 45
title: 'School Night Sessions 1 - The Ultra Low Power Arduino'
date: 2013-02-13T23:29:39+00:00
author: gregario
layout: post
guid: http://thebedroomlaboratory.com/?p=45
permalink: /2013/02/13/school-night-sessions-1-the-ultra-low-power-arduino/
image: /wp-content/uploads/2013/02/lparduino11.jpg
categories:
  - Projects
  - School Night Sessions
---
The idea behind school night sessions is to take an idea from the back of our brain to an orderable design in 3 hours.

A deadline does funny things to people, and working to tight deadlines tends to bring out the creativity in Martin in particular!
  
So having started our first nights session at 9pm and having opened an eagle schematic to begin at 11.30pm, I think we can safely say that we fail this weeks task...

But hey, the website is in much better shape, we've set our repositories and social media who-sie-whats-its in motion and we've set up software we'll be using in the coming weeks so we can easily work together. So its a start.

So expect an honest effort at a low powered arduino, along with a proper setup/design and delivery process in place that we're going to work on over the weekend.

Stay tuned... And stay classy.

**Update Midnight! **

So we finished our 3 hour stint, the timer is gone and we're fit for bed. We learned a lot about how to properly document what we're doing an how and when to update! Will try this project again next week and hopefully be able to get it complete in the 3 hours.


**Update 2 (Also Midnight)**

Just on the power input, one thing we decided early on is that the system would be run from either a coin cell battery or a single AA battery. I've been thinking about a simple boost converter with the excellent AS1310 from austria microsystems so I thought I would try it out. Here's the sample layout:

[AS1310-300x145.png](/wp-content/uploads/2013/02/AS1310.png)

The nice thing about this part (besides being light on passives) is that it can work down to 0.7V. This means that you can use much more of the energy contained in an AA battery without worrying about a drooping voltage over the lifetime of the battery. The goal we've been looking to hit is the ability to code the arduino to last for 6 months on 1AA battery.