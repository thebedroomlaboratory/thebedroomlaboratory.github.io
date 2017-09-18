---
id: 762
title: 'API Month Day 8 &#8211; SPACE'
date: 2015-12-08T13:29:51+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=762
permalink: /2015/12/08/api-month-day-8-space/
image: /wp-content/uploads/2015/12/640px-International_Space_Station_after_undocking_of_STS-132.jpg
categories:
  - Uncategorised
tags:
  - API
---
**API purpose** Finding information about the International Space Station
  
**Signup** No signup necessary
  
**Documentation** <a href="http://open-notify.org/Open-Notify-API/" target="_blank">http://open-notify.org/Open-Notify-API/</a>
  
**Github** <a href="https://github.com/gregario/API-Month/tree/master/Day8%20International%20Space%20Station" target="_blank">Click here for link</a>
  
**Comment** Really fun dataset to play with

I did promise some time manipulation stuff today  but it was super boringso I got interested in space instead. Fellow bedlabber (that&#8217;s a word) vykta sent on a link to Urethcast, a service which provides pictures from the International Space Station (ISS). He&#8217;s promised to write up a post on it this month so stay tuned for that. It did get me thinking about what other sources of open data are available from the ISS.

I did some googling and found open-notify, a wrapper API for some of the data Nasa puts out. Turns out space agencies have a good understanding of where the ISS is at any given time, who would have thought? Open-notify provides information on where the ISS is, when it will be visible over a given GPS coordinates and who is on board. All cool stuff 🙂

It did give me the opportunity to implement a few things:
  
&#8211; Epoch converter, epoch time (or unix time) is time quoted in seconds since 00:00:00 UTC on Thursday, 1 January 1970. Its useful for comparing times on servers but is not very human readable.
  
&#8211; Reverse geocoding, for if I got a set of GPS coordinates and want a real address, I&#8217;ve made a function for that now

Its a nice little script, returns a little table of data like so:

[<img class="alignnone size-medium wp-image-763" src="http://localhost/wp-content/uploads/2015/12/Day8-Output-300x160.png" alt="Day8 Output" width="300" height="160" />](http://localhost/wp-content/uploads/2015/12/Day8-Output.png)

I also realised I&#8217;ve been consistently spelling longitude incorrectly all week for my variables. Oh well. Check out the code, again its all commented so hopefully is understandable. Any questions pop them in the comments.

All the code is on the github. I&#8217;ve realised that its not exactly readable without the indents now that my programs are more complex. I&#8217;ll have a read on the wordpress nexus to see how its done and maybe only copy the interesting bits from now on.