---
id: 745
title: 'Day 4 API Month - Google Maps Geocoding'
date: 2015-12-04T18:05:13+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=745
permalink: /2015/12/04/day-4-api-month-google-maps-geocoding/
image: /wp-content/uploads/2015/12/Screenshot-2013-05-15-at-12.38.58-AM.jpg
categories:
  - Uncategorised
---
API purpose: Getting GPS data (amongst a bunch of other things)
  
Signup: Via your google account.
  
Documentation: <a href="https://developers.google.com/maps/web-services/client-library" target="_blank">https://developers.google.com/maps/web-services/client-library</a>
  
Github:<a href="https://github.com/gregario/API-Month/tree/master/Day4%20GPS" target="_blank"> https://github.com/gregario/API-Month/tree/master/Day4%20GPS</a>
  
Comment: Easy Peasy!

A super simple one today. Working through these location maps I've had to input GPS coordinates for a call and I thought it would be nice to be able to feed in a nice address and get a nice GPS coordinates. Turns out google provide this service and its super easy to use.

So I looked at a function for geocoding (taking an address and converting to GPS), this can be simply altered for reverse geocoding too (taking GPS and converting to an address). The latter is important too as some functions in API's return a GPS and its not meaningful as an output (or nobody knows what the hell it means.

So the code today is super simple as a nice man made a python wrapper for all of this. So rock over to <https://github.com/googlemaps/google-maps-services-python> or just run:

> sudo pip install -U googlemaps

You are basically good to go then. So I wrote two short scripts that are available on the github link above, the scripts are pretty easy and build on the python tricks I built up in the other tutorials.

![JSON_Day4](/wp-content/uploads/2015/12/JSON_Day4.jpg)

Here's the API call, very similar structure to the TFL structure!

```bash
# -*- coding: utf-8 -*-
# Program to check how long it will take me to get to work
# Greg Jackson 4th deb 2015
# Twitter @gr3gario or github gregario
# Day four of the Month of API

import googlemaps # install using pip install -U googlemaps 
import sys # Used to take in input parameters from command line.

gmaps = googlemaps.Client(key='INSERT API KEY') # Get key from your google developer portal. 

# Geocoding an address
geocode_result = gmaps.geocode(sys.argv[1]) # passes address given on command line to google maps geocoding api
latlng = []

for key in geocode_result: # the returned object is a list with nested JSON objects inside each list. So you need to iterate through the list and do operations on each object separately
	latlng.append(key['geometry']['bounds']['northeast']['lat']) # pulls out nested latitude figure from call
	latlng.append(key['geometry']['bounds']['northeast']['lng']) # pulls out nested longditude figure from call

# easy peasy printing
print "Your latitude is: " +latlng[0]
print "Your londitude is: " +latlng[1]
```
And it works! Go me.
  
![day4 success](/wp-content/uploads/2015/12/day4-success.jpg)