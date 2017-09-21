---
id: 751
title: 'Day 5 API Month - London Air Quality'
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
  
Documentation: [http://api.erg.kcl.ac.uk/AirQuality/help](http://api.erg.kcl.ac.uk/AirQuality/help)
  
Github: [https://github.com/gregario/API-Month/tree/master/Day5%20AirQuality](https://github.com/gregario/API-Month/tree/master/Day5%20AirQuality)
  
Comment: Really well made API, not real time though, about a day delay

So Kings College run an array of air quality monitors across London. Its a really interesting piece of data to work with that is so relevant to our day to day lives. Thought I would have a look at the API and try to pull the data from my nearest air quality monitor to my home.

The call from the API documentation requires the use of their site codes to work, which isn't the most intuitive. A quick peruse of the maps at [particulate matter](http://www.londonair.org.uk/LondonAir/Default.aspx). Cool so IS2 is my air quality roadside monitor. As a bonus there's 15 years of data from the monitor.

So [here](http://api.erg.kcl.ac.uk/AirQuality/help/operations/GetRawDataSitesSpeciesJSON) is the link to the call we want. It actually leads to a pretty straightforward script. [Edit an hour later]. Getting strings converted to floats is apparently not straight forward. Anywho, here's the completed script. As always I explain the crap out of the code in the code so I think it kind of explains itself!

```python
#coding: utf-8
# Day 5 of month of API
# Looking at local air quality data and what the last 24 hours have been like in your local area
# Greg Jackson 05/12/15 gr3gario on twitter ang gregario on github
import requests
import json 


url = "http://api.erg.kcl.ac.uk/AirQuality/Data/SiteSpecies/SiteCode=IS2/SpeciesCode=NO2/StartDate=04-12-15/EndDate=05-12-15/Json" # Gives data in closest AQ monitor
r = requests.get(url).json() # Make a request to the LAQN API for data

rLoop = r['RawAQData']['Data'] # You got to define this here as you can't nest it below. the for loop below only works for the list embedded in the JSON object
AQugm3 = [] # A list to store the readins


for key in rLoop:
	AQugm3temp = key['@Value'] # This loops through each data packet in the list and pulls out our relevant datapoint
	try: # A try catch is included here as there are blank datapoints returned from the LAQN API that would mess this up occasionally if there wasn't a catch in place
		AQugm3temp = float(AQugm3temp) # Converts from a string to a float so we can perform operations on it
		AQugm3.append(AQugm3temp) # Adds output to AQugm3 variable
	# Catches exceptions
	except:
		print 'error in parsing, oops'
		pass

# Really simple averages. Sums all elements in the list and divides by the length of the list 
average = sum(AQugm3) / float(len(AQugm3))
average = round(average,2)
# This is an EU defined goal for NO2 in the city. I figure if our daily average is below this we're doing well. Its more to give context to the number.
goal = 40.0 

# Simple check to give context to the number. 
if average < goal:
	print "Hurray! The air quality today is less than the yearly average target of 40 ug/m3 NO2 target in the UK and reads " +str(average)+ " ug/m3"
elif average > goal: 
	print "Unfortunately the air quality today is more than the yearly average target of 40 ug/m3 NO2 in the UK and reads " + str(average)+ " ug/m3"
```

So when I run python AQ.py.
> Unfortunately the air quality today is more than the yearly average target of 40 ug/m3 NO2 in the UK and reads 69.71 ug/m3

Interesting stuff 🙂


So I had the thought of making a bigger project at the end of each week, not necessarily more work but wrapping up the work I've done into one bigger program. I have a good idea to wrap this weeks work up which I'll explain on Monday but its missing one big element. I need to be able to easily calculate the distance between two sets of GPS coordinates. So tomorrow I'll work on this. I'll be pulling an address in the UK, converting to GPS data and checking its linear distance to tower bridge in London.