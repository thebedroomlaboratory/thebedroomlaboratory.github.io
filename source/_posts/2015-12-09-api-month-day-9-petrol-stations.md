---
id: 771
title: 'API Month Day 9 &#8211; Petrol Stations'
date: 2015-12-09T15:22:16+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=771
permalink: /2015/12/09/api-month-day-9-petrol-stations/
image: /wp-content/uploads/2015/12/manlookingthroughbino.jpg
categories:
  - Uncategorised
tags:
  - API
---
**API purpose** Interfacing and searching google maps
  
**Signup** Via your google account
  
**Documentation** <a href="https://developers.google.com/places/" target="_blank">https://developers.google.com/places/<br /> </a>**Github** <a href="https://github.com/gregario/API-Month/tree/master/Day10%20Twitter" target="_blank">Click here for link</a>
  
**Comment** So much that could be done with this

Today I wanted to play with the google places API. Its very cool, it lets you search within a distance of your current location for various services. Pretty cool to see from this what&#8217;s around you. You can even pull out reviews from the locations!

So I wrote a script that takes in an address and checks for nearby petrol stations. Nice little function that could easily be extended to take in any service in your area from user input.

Nothing too tricky today, but it turns out there are not very many petrol stations in my area. I did change the argv input to a raw_input prompt from the user, its a little bit nicer and means you can be dynamically prompted for inputs during the programs operation without having to build a GUI. This can be used later to build simple command line menus etc&#8230;

Here is an example output from the script:

[<img class="alignnone size-medium wp-image-774" src="http://localhost/wp-content/uploads/2015/12/Day9Output-300x67.jpg" alt="Day9Output" width="300" height="67" />](http://localhost/wp-content/uploads/2015/12/Day9Output.jpg)