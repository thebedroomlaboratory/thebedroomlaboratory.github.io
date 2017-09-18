---
id: 751
title: 'Day 5 API Month &#8211; London Air Quality'
date: 2015-12-05T16:48:47+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=751
permalink: /2015/12/05/day-5-api-month-london-air-quality/
image: /wp-content/uploads/2015/12/Air-pollution-in-London-001.jpg
categories:
  - Uncategorised
tags:
  - API
---
API purpose: Getting London Air Quality Data
  
Signup: None, its open data
  
Documentation: <a href="http://api.erg.kcl.ac.uk/AirQuality/help" target="_blank">http://api.erg.kcl.ac.uk/AirQuality/help</a>
  
Github: <a href="https://github.com/gregario/API-Month/tree/master/Day5%20AirQuality" target="_blank">https://github.com/gregario/API-Month/tree/master/Day5%20AirQuality</a>
  
Comment: Really well made API, not real time though, about a day delay

So Kings College run an array of air quality monitors across London. Its a really interesting piece of data to work with that is so relevant to our day to day lives. Thought I would have a look at the API and try to pull the data from my nearest air quality monitor to my home.

The call from the API documentation requires the use of their site codes to work, which isn&#8217;t the most intuitive. A quick peruse of the maps at <a href="http://www.londonair.org.uk/LondonAir/Default.aspx" target="_blank">http://www.londonair.org.uk/LondonAir/Default.aspx</a> found that my closest monitor was at Holloway Road and measures <a href="https://en.wikipedia.org/wiki/Carbon_monoxide" target="_blank">carbon monoxide</a>, <a href="https://en.wikipedia.org/wiki/Nitrogen_dioxide" target="_blank">nitrogen dioxide</a> and 10 micron <a href="https://en.wikipedia.org/wiki/Particulates" target="_blank">particulate matter</a>. Cool so IS2 is my air quality roadside monitor. As a bonus there&#8217;s 15 years of data from the monitor.

So <a href="http://api.erg.kcl.ac.uk/AirQuality/help/operations/GetRawDataSitesSpeciesJSON" target="_blank">here</a> is the link to the call we want. It actually leads to a pretty straightforward script. [Edit an hour later]. Getting strings converted to floats is apparently not straight forward. Anywho, here&#8217;s the completed script. As always I explain the crap out of the code in the code so I think it kind of explains itself!

[code language=&#8221;python&#8221;]

import requests
  
import json
  
url = "http://api.erg.kcl.ac.uk/AirQuality/Data/SiteSpecies/SiteCode=IS2/SpeciesCode=NO2/StartDate=04-12-15/EndDate=05-12-15/Json" # Gives data in closest AQ monitor
  
r = requests.get(url).json() # Make a request to the LAQN API for data

rLoop = r\[&#8216;RawAQData&#8217;\]\[&#8216;Data&#8217;\] # You got to define this here as you can&#8217;t nest it below. the for loop below only works for the list embedded in the JSON object
  
AQugm3 = [] # A list to store the readins
  
for key in rLoop:
  
AQugm3temp = key[&#8216;@Value&#8217;] # This loops through each data packet in the list and pulls out our relevant datapoint
  
try: # A try catch is included here as there are blank datapoints returned from the LAQN API that would mess this up occasionally if there wasn&#8217;t a catch in place
  
AQugm3temp = float(AQugm3temp) # Converts from a string to a float so we can perform operations on it
  
AQugm3.append(AQugm3temp) # Adds output to AQugm3 variable
  
\# Catches exceptions
  
except:
  
print &#8216;error in parsing, oops&#8217;
  
pass

\# Really simple averages. Sums all elements in the list and divides by the length of the list
  
average = sum(AQugm3) / float(len(AQugm3))
  
average = round(average,2)
  
# This is an EU defined goal for NO2 in the city. I figure if our daily average is below this we&#8217;re doing well. Its more to give context to the number.
  
goal = 40.0

# Simple check to give context to the number.
  
if average < goal:
  
print "Hurray! The air quality today is less than the yearly average target of 40 ug/m3 NO2 target in the UK and reads " +str(average)+ " ug/m3"
  
elif average > goal:
  
print "Unfortunately the air quality today is more than the yearly average target of 40 ug/m3 NO2 in the UK and reads " + str(average)+ " ug/m3"

[/code]

&nbsp;

<p class="p1">
  <span class="s1">So when I run python AQ.py.</span>
</p>

> <p class="p1">
>   <span class="s1">Unfortunately the air quality today is more than the yearly average target of 40 ug/m3 NO2 in the UK and reads 69.71 ug/m3</span>
> </p>

<p class="p1">
  Interesting stuff 🙂
</p>

So I had the thought of making a bigger project at the end of each week, not necessarily more work but wrapping up the work I&#8217;ve done into one bigger program. I have a good idea to wrap this weeks work up which I&#8217;ll explain on Monday but its missing one big element. I need to be able to easily calculate the distance between two sets of GPS coordinates. So tomorrow I&#8217;ll work on this. I&#8217;ll be pulling an address in the UK, converting to GPS data and checking its linear distance to tower bridge in London.