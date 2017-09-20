---
id: 721
title: 'API Month Day 2 - Weather Underground'
date: 2015-12-02T16:24:23+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=721
permalink: /2015/12/02/api-month-day-2-weather-underground/
image: /wp-content/uploads/2015/12/Cycle-wet1.jpg
categories:
  - Uncategorised
tags:
  - API
---
**Highlights**

**API purpose:** Weather Conditions
  
**Signup: **<a href="http://www.wunderground.com/weather/api/" target="_blank">http://www.wunderground.com/weather/api/</a>
  
**Documentation:** <a href="http://www.wunderground.com/weather/api/d/docs" target="_blank">http://www.wunderground.com/weather/api/d/docs</a>
**Github:** <a href="http://bit.ly/1OxwFrc" target="_blank">http://bit.ly/1OxwFrc</a>
  
> **Comment:** Feature rich and worldwide weather!

OK so day two of API month. Exciting, right? Yesterday it occured to me if I'm making a decision when debating my cycle vs tube debate it would also be good to see the near term forecast. So I did some reading and found weather underground. Its a system of weather stations around the world, with data provided by official and hobbyist sources. Their API is pretty good too!

**Getting the Data**

So I swung over and setup an account. Straight forward process. I want to pull relevant information from the API so I did a sample call for London to see what I would get.

> http://api.wunderground.com/api/[INSERTKEY]/conditions/q/uk/London.json

Pretty straightforward. A slightly different system than citymapper but very usable. It returned this: ``

```json
{
  "response": {
      "version":"0.1",
      "termsofService":"http://www.wunderground.com/weather/api/d/terms.html",
      "features": {
        "conditions": 1
      }
    }
  , "current_observation": {
        "image": {
        "url":"http://icons.wxug.com/graphics/wu2/logo_130x80.png",
        "title":"Weather Underground",
        "link":"http://www.wunderground.com"
        },
        "display_location": {
        "full":"Dublin, Ireland",
        "city":"Dublin",
        "state":"",
        "state_name":"Ireland",
        "country":"IE",
        "country_iso3166":"IE",
        "zip":"00000",
        "magic":"1",
        "wmo":"03969",
        "latitude":"53.43000031",
        "longitude":"-6.25000000",
        "elevation":"85.00000000"
        },
        "observation_location": {
        "full":"Paulie - Swords West, Swords, DUBLIN",
        "city":"Paulie - Swords West, Swords",
        "state":"DUBLIN",
        "country":"IRELAND",
        "country_iso3166":"IE",
        "latitude":"53.463554",
        "longitude":"-6.249463",
        "elevation":"138 ft"
        },
        "estimated": {
        },
        "station_id":"IDUBLINS3",
        "observation_time":"Last Updated on December 2, 4:08 PM GMT",
        "observation_time_rfc822":"Wed, 02 Dec 2015 16:08:49 +0000",
        "observation_epoch":"1449072529",
        "local_time_rfc822":"Wed, 02 Dec 2015 16:09:02 +0000",
        "local_epoch":"1449072542",
        "local_tz_short":"GMT",
        "local_tz_long":"Europe/Dublin",
        "local_tz_offset":"+0000",
        "weather":"Mostly Cloudy",
        "temperature_string":"51.1 F (10.6 C)",
        "temp_f":51.1,
        "temp_c":10.6,
        "relative_humidity":"99%",
        "wind_string":"Calm",
        "wind_dir":"SW",
        "wind_degrees":217,
        "wind_mph":0.0,
        "wind_gust_mph":0,
        "wind_kph":0,
        "wind_gust_kph":0,
        "pressure_mb":"1017",
        "pressure_in":"30.04",
        "pressure_trend":"+",
        "dewpoint_string":"51 F (11 C)",
        "dewpoint_f":51,
        "dewpoint_c":11,
        "heat_index_string":"NA",
        "heat_index_f":"NA",
        "heat_index_c":"NA",
        "windchill_string":"NA",
        "windchill_f":"NA",
        "windchill_c":"NA",
        "feelslike_string":"51.1 F (10.6 C)",
        "feelslike_f":"51.1",
        "feelslike_c":"10.6",
        "visibility_mi":"6.2",
        "visibility_km":"10.0",
        "solarradiation":"0",
        "UV":"0.0","precip_1hr_string":"0.00 in ( 0 mm)",
        "precip_1hr_in":"0.00",
        "precip_1hr_metric":" 0",
        "precip_today_string":"0.07 in (2 mm)",
        "precip_today_in":"0.07",
        "precip_today_metric":"2",
        "icon":"mostlycloudy",
        "icon_url":"http://icons.wxug.com/i/c/k/mostlycloudy.gif",
        "forecast_url":"http://www.wunderground.com/global/stations/03969.html",
        "history_url":"http://www.wunderground.com/weatherstation/WXDailyHistory.asp?ID=IDUBLINS3",
        "ob_url":"http://www.wunderground.com/cgi-bin/findweather/getForecast?query=53.463554,-6.249463",
        "nowcast":""
    }
}
```

Wow... That is a lot more info than our last tutorial. This is great though, it gives me a chance to play with more information. Here's what I wrote up.

```python
# -*- coding: utf-8 -*-
# Program to check how long it will take me to get to work
# Greg Jackson 1st dev 2015
# Twitter @gr3gario or github gregario
# Day one of the Month of API

import requests
import json 
import sys # needed to pass arguments from command line 



country=  str(sys.argv[1])
location = str(sys.argv[2])
url = "http://api.wunderground.com/api/[INSERTAPIKEY]/conditions/q/"+str(country)+"/"+str(location)+".json"

r = requests.get(url).json()
print("The current wind speed (mph) is: "+ str(r['current_observation']['wind_mph']))
print("The current temperature (C) is: " +str(r['current_observation']['temp_c']))
print("Sure what's the weather like? : "+ str(r['current_observation']['icon']))
print("The current relative RH is: "+str(r['current_observation']['relative_humidity']))
print("Will it rain soon? : "+str(r['current_observation']['precip_1hr_metric']))

# So I have a good indication of the weather from a current loation. 
# I introduced two super simple things here. 
# One is string concatonation in python. This lets us declare a location by variable instead of in line. 
# this can be better than the payload option as it gives you more flexibility. 

## Finally I thought I could declare from the command line the location to search. 
## I've always wondered how this could be done so now I know! 

```

Still pretty straightforward too!

**Nested JSON**

Yesterday our JSON was super easy. It was one series of machine tag pairs inside a JSON object. We asked for our machine tag (estimated\_time) in that array and we were good to go with the value associated with that. However in JSON, each variable in an array can have an array of machine tags nested inside it. Its actually quite elegant if you work through the logic but we don't care about this, we just want the data, right?!!! So let's take wind speed from above. We wanted to get the current\_observation array and inside that get the wind_mph tag and its associated value. To do this we used the following syntax.

```python

print("The current wind speed (mph) is: "+ str(r\['current\_observation'\]\['wind\_mph'\]))

```

**So What Next? **

So that's that for today. Another simple example with some useful tricks to get you going with weather APIs. So what shall I do tomorrow??? I like this work around my commute to work. I think I'm going to solve a final challenge tomorrow with a good one, I live a 4 minute walk from my local train to work. The train comes every 15 minutes. The arrival time of the next train dictates if I have breakfast each day. I check this every day on google maps so I want to write a script that checks the TFL API and displays the next train time for me so I can quickly glance and see how long I have!