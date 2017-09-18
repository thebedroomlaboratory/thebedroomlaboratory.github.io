---
id: 781
title: 'API Month Day 7 &#8211; Where is my air?'
date: 2015-12-07T15:03:47+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=757
permalink: /2015/12/07/api-month-day-7-where-is-my-air/
image: /wp-content/uploads/2015/12/Screenshot-2015-12-07-12.29.20.png
categories:
  - Uncategorised
tags:
  - API
---
API purpose: Finding local air quality from address
  
Signup: air quality has no signup google, as always, does.
  
Documentation: <a href="https://developers.google.com/maps/web-services/client-library" target="_blank">https://developers.google.com/maps/web-services/client-library</a>
  
Github: <a href="https://github.com/gregario/API-Month/tree/master/Day7%20AQ%20Project" target="_blank">https://github.com/gregario/API-Month/tree/master/Day7%20AQ%20Project</a>
  
Comment: Wrapping up the first week into a useful script

So today was a culmination of all the learnings I achieved this week&#8230;. A bit of background on this one. I decided to do something a bit more abitious today. Since I now have the basic building blocks of data for getting and manipulating JSON API data I thought I would put it to the test for something more than one localised test. So today I&#8217;m going to build something chunkier. Using the work I&#8217;ve done all week from data manipulation, geocaching and the air quality API, I want to build an app that if you put in a post code in London it finds the nearest AQ monitor from the list and returns its air quality data.

This is more challenging than it sounds, the basic work flow would be.

Take input address and convert to GPS. Pull down list of all London Air Quality monitors and extract their locations. Do a diff between the two to find the closest distance from that new list. Then from that new list pull down a list of sensors associated with that sensor. Then from this pull down their data and average it for the day.

What I can then use this to do is to give Air quality information as an extension to map or location searches. An interesting wrapper library for future work. I&#8217;m going to try some more complex error handling in this too, as I&#8217;ve been pretty lax with this up until now.

As I&#8217;ve moved onto commenting inline the code should be self explanatory, it produces some nice pretty outputs too!

[<img class="alignnone size-medium wp-image-758" src="http://localhost/wp-content/uploads/2015/12/Screenshot-2015-12-07-12.29.20-300x188.png" alt="Screenshot 2015-12-07 12.29.20" width="300" height="188" />](http://localhost/wp-content/uploads/2015/12/Screenshot-2015-12-07-12.29.20.png)

[code language=&#8221;python&#8221;]

#coding: utf-8
  
\# Day seven of the month of API
  
# Today finds your nearest Air Quality monitor and returns its data
  
\# Greg Jackson @gr3gario on twitter and gregario on github

import requests
  
import json
  
import sys
  
import googlemaps
  
from APIKEY import googlekey
  
import math

\## Workflow
  
#Pull down list of all London Air Quality monitors and extract their locations.
  
#Do a diff between the two to find the closest distance from that new list.
  
#Then from that monitor pull out its air quality monitor.

\# This function takes in a command line post code (or address), performs a google maps call to check its GPS data and returns as a list
  
def addtoGPS():
  
attempts = 0
  
latlng = []

while attempts < 3:
  
try:
  
gmaps = googlemaps.Client(key=googlekey) # Get key from your google developer portal.
  
\# Geocoding an address
  
geocode_result = gmaps.geocode(sys.argv[1]) # passes address given on command line to google maps geocoding api

for key in geocode_result: # the returned object is a list with nested JSON objects inside each list. So you need to iterate through the list and do operations on each object separately
  
latlng.append(float(key\[&#8216;geometry&#8217;\]\[&#8216;bounds&#8217;\]\[&#8216;northeast&#8217;\]\[&#8216;lat&#8217;\])) # pulls out nested latitude figure from call
  
latlng.append(float(key\[&#8216;geometry&#8217;\]\[&#8216;bounds&#8217;\]\[&#8216;northeast&#8217;\]\[&#8216;lng&#8217;\])) # pulls out nested longditude figure from call
  
break

except:
  
attempts += 1
  
print "Error getting data from Google maps API"

return latlng

\# This function calls the London Air Quality API and returns a list of all the sites with their GPS Coordinates
  
def LAQNList():
  
url = "http://api.erg.kcl.ac.uk/AirQuality/Information/MonitoringSites/GroupName=All/JSON" # Gives all units in London for AQ
  
siteDetails=[]
  
siteDetail={}
  
attempts=0
  
distance = 0.0

while attempts < 3:
  
try:
  
r = requests.get(url).json() # Make a request to the TFL API for data
  
q = r\[&#8216;Sites&#8217;\]\[&#8216;Site&#8217;\] # This extracts the list from the JSON object

for key in q:
  
\# This is quite elegant. There are closed air quality units on the system which we want to ignore. So we check the dateclosed field. If its emply we include the unit.
  
dateclosed = key [&#8216;@DateClosed&#8217;]
  
if not dateclosed:
  
sitecode = key[&#8216;@SiteCode&#8217;]
  
latitude = float(key[&#8216;@Latitude&#8217;])
  
longditude = float(key[&#8216;@Longitude&#8217;])
  
siteDetail={&#8216;sitecode&#8217;: sitecode, &#8216;latitude&#8217;: latitude, &#8216;longditude&#8217;: longditude, &#8216;distance&#8217;:distance}
  
siteDetails.append(siteDetail)
  
break

except:
  
attempts += 1
  
#print "Error getting Location data from LAQN API"

return siteDetails

\# This function takes input values and calculates distance for every point and calculates the closest site code
  
def distance():
  
latlngin = addtoGPS()
  
siteDetails=LAQNList()
  
distance = []
  
for key in siteDetails:
  
lat = float(key [&#8216;latitude&#8217;])
  
lng = float(key [&#8216;longditude&#8217;])
  
output = math.sqrt((latlngin[0] &#8211; lat)\*\*2 + (latlngin[1] &#8211; lng)\*\*2)
  
key[&#8216;distance&#8217;] = output
  
distance.append(output)

mindistance = min(distance)

for key in siteDetails:
  
check = key[&#8216;distance&#8217;]
  
if check == mindistance:
  
finalsite = key[&#8216;sitecode&#8217;]

return finalsite

\## I now have my closest Air Quality Monitor, need to call this and see what sensors it has
  
## back to the API documentation

def whatSensor():
  
siteCode = distance()
  
speciesCode = []
  
attempts = 0
  
while attempts < 3:
  
try:
  
url= "http://api.erg.kcl.ac.uk/AirQuality/Daily/MonitoringIndex/Latest/SiteCode=" +siteCode+ "/json"
  
r = requests.get(url).json() # Make a request to the TFL API for data
  
q = r\[&#8216;DailyAirQualityIndex&#8217;\]\[&#8216;LocalAuthority&#8217;\]\[&#8216;Site&#8217;\]\[&#8216;Species&#8217;\] # This extracts the list from the JSON object
  
for key in q:
  
specie = key[&#8216;@SpeciesCode&#8217;]
  
species={&#8216;SpeciesCode&#8217;: specie}
  
speciesCode.append(species)
  
break

except:
  
attempts += 1
  
print "error finding speciesCode of sensors"

return speciesCode

\# Finally once we have the sensors associated with the closest air quality sensor we can do a check of the last day and return an average of the readings
  
\# I realise here it would be nice to check the current time and return it as a variable for input, will work on that on day 8
  
def sensorReadings():
  
siteCode = distance()
  
speciesCode = whatSensor()
  
attempts = 0
  
averageOut = []

for key in speciesCode:
  
speciesUrl = key[&#8216;SpeciesCode&#8217;]
  
url = "http://api.erg.kcl.ac.uk/AirQuality/Data/SiteSpecies/SiteCode="+siteCode+"/SpeciesCode="+speciesUrl+"/StartDate=05-12-15/EndDate=06-12-15/Json" # Gives data in closest AQ monitors
  
r = requests.get(url).json() # Make a request to the LAQN API for data

rLoop = r\[&#8216;RawAQData&#8217;\]\[&#8216;Data&#8217;\]
  
AQugm3 = []

for key in rLoop:
  
AQugm3temp = key[&#8216;@Value&#8217;]
  
try:
  
AQugm3temp = float(AQugm3temp)
  
AQugm3.append(AQugm3temp) # Adds output to AQugm3 variable
  
\# Catches exceptions
  
except:
  
print &#8216;error in parsing, oops&#8217;
  
pass
  
\# Really simple averages. Sums all elements in the list and divides by the length of the list
  
average = sum(AQugm3) / float(len(AQugm3))
  
average = round(average,2)
  
average={&#8216;SpeciesCode&#8217;: speciesUrl, &#8216;average&#8217;:average}
  
averageOut.append(average)

return averageOut

print sensorReadings()

[/code]

<p class="p1">
  On the code, apologies but the white spaces were not preserved when I copied it over, have a look at the github to get a more human readable version of the code.
</p>

<p class="p1">
  Running
</p>

> <p class="p1">
>   <span class="s1">python AQProject.py SW72bx</span>
> </p>

<p class="p1">
  Gives
</p>

> <p class="p1">
>   [{&#8216;SpeciesCode&#8217;: u&#8217;NO2&#8242;, &#8216;average&#8217;: 43.0}, {&#8216;SpeciesCode&#8217;: u&#8217;PM10&#8242;, &#8216;average&#8217;: 21.68}, {&#8216;SpeciesCode&#8217;: u&#8217;PM25&#8242;, &#8216;average&#8217;: 8.66}]
> </p>

<p class="p1">
  Turns out the air quality around work is pretty good, for NO2 43ug/m3 average is right at the 40ug/m3 target for a yearly average. Yay 🙂
</p>

<p class="p1">
  One thing I&#8217;ve noticed from this work is I need to have a play with times and dates to do it neatly. Tomorrow I&#8217;m going to play with NTP servers and the date module in python. Its a slight divergence from the API calling but will be a useful function to plug into other functions in the future.
</p>