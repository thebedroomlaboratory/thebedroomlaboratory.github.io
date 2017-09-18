---
id: 197
title: 'School Night Session #5 &#8211; WITH PITH 3'
date: 2013-03-21T00:05:26+00:00
author: catchmartin
layout: post
guid: http://thebedroomlaboratory.com/?p=197
permalink: /2013/03/21/school-night-session-5-with-pith-3/
image: /wp-content/uploads/2013/03/WITHPITH-LowPower11.png
categories:
  - School Night Sessions
---
As you can see we&#8217;ve gotten the thing working and not only that but the current draw of the system has been optimized hugely too. The photo shows a current draw of 4.3uA for when the chip is asleep. This climbs to 5mA when the system wakes up for 4ms at a time. This means that off a single 2.6Ah 3.7V battery we should get about 308 days of battery life out of the thing (if sleeping for 60ms at a time). I am basing the 60ms sleep period on some rough calculations which you can see here (60ms asleep and 4ms awake):

[<img class="aligncenter size-large wp-image-208" alt="WITH_PITH-HowLong" src="/wp-content/uploads/2013/03/WITH_PITH-HowLong-1024x610.png" width="700" height="416" />](/wp-content/uploads/2013/03/WITH_PITH-HowLong.png)I&#8217;ve popped the Arduino code up on github too, if people want to have a look at it. It is very rough at the moment but will be tidied up and made more compact in the near future: <a title="https://github.com/thebedroomlaboratory/WITHPITH" href="https://github.com/thebedroomlaboratory/WITHPITH" target="_blank">https://github.com/thebedroomlaboratory/WITHPITH</a> I have used two libraries in writing this code, Ken Shirriff&#8217;s <a href="http://www.righto.com/2009/08/multi-protocol-infrared-remote-library.html" target="_blank">IR Library</a> and Rocket Scream&#8217;s <a href="https://github.com/rocketscream/Low-Power" target="_blank">Low Power Library</a>. We were using the IR library to send a 38kHz pulse burst but the commands had additional overhead in the region of 30ms each for sending marks and spaces. This was unacceptable for our purposes here, so we migrated the library code into the sketch and changed how/when the delayMicroseconds() function was used. The Low Power Library is used for putting the 328p to sleep and setting a watchdog timer for waking it up 60ms later.

In order to reduce the current draw of the system even more, we are now powering the TSOP28238 directly from a digital pin on the 328p, just for the duration required to check the IR beam. Additionally, we have moved from using an external 8MHz crystal to using the 8MHz internal oscillator on the 328p and removed the pullup resistor on the reset pin too. There are a few resources that were invaluable for when we were trying to optimize the current draw:

  * <a href="http://qed.princeton.edu/main/CEE474/LowPower" target="_blank">http://qed.princeton.edu/main/CEE474/LowPower</a>
  * <a href="http://www.gammon.com.au/forum/?id=11497" target="_blank">http://www.gammon.com.au/forum/?id=11497</a>
  * <a href="http://www.sparkfun.com/tutorials/309" target="_blank">http://www.sparkfun.com/tutorials/309</a>

We are currently waiting on screens to arrive from dx.com but then will go ahead with the full build of the system. More on that again. Maybe the same time next week 😉

[<img class="aligncenter size-large wp-image-200" alt="It's Alive" src="/wp-content/uploads/2013/03/Its-Alive-1024x546.png" width="700" height="373" />](/wp-content/uploads/2013/03/Its-Alive.png)