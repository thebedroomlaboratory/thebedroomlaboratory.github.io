---
id: 754
title: 'Day 6 API Month - GPS Distance'
date: 2015-12-06T22:42:58+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=754
permalink: /2015/12/06/day-6-api-month-gps-distance/
image: /wp-content/uploads/2015/12/Snapshot_R01.png
categories:
  - Uncategorised
tags:
  - API
---
API purpose: GPS Distance
  
Signup: Using the google developer portal
  
Documentation: <a href="https://developers.google.com/maps/web-services/client-library" target="_blank">https://developers.google.com/maps/web-services/client-library</a>
  
Github: <a href="https://github.com/gregario/API-Month/tree/master/Day6%20GPS%20Distance" target="_blank">https://github.com/gregario/API-Month/tree/master/Day6%20GPS%20Distance</a>
  
Comment: Continuation of day 4, interesting problem.

Quick one today after yesterday drove me mad. Wanted to do a quick function that takes in two sets of GPS data and works out the distance between them. I did some reading on calculating distances between two points on a map. Apparently its a real issue in the mapping community with many implementations of map hashing being discussed.

My first thoughts would be to take the two latitudes from each other, take the absolute of that. Then do the same with longditude and then add those two numbers together. In math-y terms it would be:

> distance = abs(lat2 - lat1) + abs(long2 - long2)

But then I had a flashback to my school maths and it would be more appropriate to do a pythagoras job on it. Basically take the two points as a hypotenuse of a right angled triangle. Then I had the fun of programming it in python, I got:

> math.sqrt((p0[0] - p1[0])\*\*2 + (p0[1] - p1[1])\*\*2)

A small aside but another thing I did for today was to make an API key file that I can use with all my programs. So commiting your API keys to Git is generally a bad thing. People have scripts running to search for API key, particularly for anything to do with AWS, and start hammering them once they're found. It can end up costing a bunch of money. So I have a separate file I do not commit to any Git repository and I add to my files by importing it like any other module in python. It also is a nice system for configuration files if you want to make your python scripts more abstract.

So new code, here it it.

```python
# -*- coding: utf-8 -*-T
# Program to check the linear distance between two sets of GPS coordinates. 
# Continuation of day 4 of API Month
# Greg Jackson 6th deb 2015
# Twitter @gr3gario or github gregario
# Day 6 of the Month of API

import googlemaps # install using pip install -U googlemaps 
import sys # Used to take in input parameters from command line.
from APIKEY import googlekey
import math # Added to do sqrt 

# Geocoding an address
geocode_result = gmaps.geocode(sys.argv[1]) # passes address given on command line to google maps geocoding api
gmaps = googlemaps.Client(key= googlekey) # Get key from your google developer portal. 
latlng = []
latlngTB = [51.5054564,-0.0753565]


for key in geocode_result: # the returned object is a list with nested JSON objects inside each list. So you need to iterate through the list and do operations on each object separately
	latlng.append(key['geometry']['bounds']['northeast']['lat']) # pulls out nested latitude figure from call
	latlng.append(key['geometry']['bounds']['northeast']['lng']) # pulls out nested longditude figure from call


def distance(p0, p1):
    return math.sqrt((p0[0] - p1[0])**2 + (p0[1] - p1[1])**2)

# Obsolete Method, simplier than other.
#distance = abs(latlngTB[0] - latlng[0]) + abs(latlng[1] - latlngTB[1]) 

distance = distance(latlng,latlngTB)
print "The distance to Tower Bridge is: " +str(distance)
```