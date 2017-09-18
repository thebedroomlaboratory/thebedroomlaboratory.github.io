---
id: 721
title: 'API Month Day 2 &#8211; Weather Underground'
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

> **API purpose:** Weather Conditions
  
> **Signup: **<a href="http://www.wunderground.com/weather/api/" target="_blank">http://www.wunderground.com/weather/api/</a>
  
> **Documentation:** <a href="http://www.wunderground.com/weather/api/d/docs" target="_blank">http://www.wunderground.com/weather/api/d/docs<br /> </a>**Github:** <a href="http://bit.ly/1OxwFrc" target="_blank">http://bit.ly/1OxwFrc</a>
  
> **Comment:** Feature rich and worldwide weather!

OK so day two of API month. Exciting, right? Yesterday it occured to me if I&#8217;m making a decision when debating my cycle vs tube debate it would also be good to see the near term forecast. So I did some reading and found weather underground. Its a system of weather stations around the world, with data provided by official and hobbyist sources. Their API is pretty good too!

**Getting the Data**

So I swung over and setup an account. Straight forward process. I want to pull relevant information from the API so I did a sample call for London to see what I would get.

> http://api.wunderground.com/api/[INSERTKEY]/conditions/q/uk/London.json

Pretty straightforward. A slightly different system than citymapper but very usable. It returned this: ``

> <pre>{
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
}</pre>

Wow&#8230; That is a lot more info than our last tutorial. This is great though, it gives me a chance to play with more information. Here&#8217;s what I wrote up.

> [code language=&#8221;python&#8221;]
   
> import requests
   
> import json
   
> import sys # needed to pass arguments from command line
> 
> country= str(sys.argv[1])
   
> location = str(sys.argv[2])
   
> url = "http://api.wunderground.com/api/[INSERTAPIKEY]/conditions/q/"+str(country)+"/"+str(location)+".json"
> 
> r = requests.get(url).json()
   
> print("The current wind speed (mph) is: "+ str(r\[&#8216;current\_observation&#8217;\]\[&#8216;wind\_mph&#8217;\]))
   
> print("The current temperature (C) is: " +str(r\[&#8216;current\_observation&#8217;\]\[&#8216;temp\_c&#8217;\]))
   
> print("Sure what&#8217;s the weather like? : "+ str(r\[&#8216;current_observation&#8217;\]\[&#8216;icon&#8217;\]))
   
> print("The current relative RH is: "+str(r\[&#8216;current\_observation&#8217;\]\[&#8216;relative\_humidity&#8217;\]))
   
> print("Will it rain soon? : "+str(r\[&#8216;current\_observation&#8217;\]\[&#8216;precip\_1hr_metric&#8217;\]))
> 
> [/code]

So as before I import requests and JSON to deal with requesting the data from the API service and using that data once it&#8217;s available. This is very similar to yesterday but I&#8217;ve added the following little tricks:

  * Passing arguments from the command line
  * Clever string concatenation
  * Nested JSON variable operations

**Passing arguments from command line**

&#8220;import sys&#8221; is used here. This allows us to work with our operating system. In my case here I define country and location using sys.argv[1] and sys.argv[2]. This looks complicated but I&#8217;ll talk through what I&#8217;m doing here with an example. So if I run the program with the command:

> python Weather.py UK London

This gets python to run my script and defines two variables (or system arguments) after the script. This allows me to feed in data to my script without rewriting it every time. So you may have figured out sys.argv[1] does that. The &#8220;sys&#8221; calls the above imported &#8220;sys&#8221; and argv is a function within that. Then you pass 1 to that function. Put all that together and you are asking the system to grab the first argument declared when the program was run. Cool!

**String Concatenation**

So once I have the country and city names I want to lookup I need to pass them into the API call I want to do. If you want to add a variable at the end of a string its super easy, you just do:

> [code language=&#8221;python&#8221;]
  
> var = "bar"
  
> print "foo" + var
  
> [/code]

Its a little trickier if you want to insert words mid string. The following syntax does this.

> [code language=&#8221;python&#8221;]
  
> var = "bar"
   
> print "foo" +bar+ "right??!?"
  
> [/code]

Still pretty straightforward too!

**Nested JSON**

Yesterday our JSON was super easy. It was one series of machine tag pairs inside a JSON object. We asked for our machine tag (estimated\_time) in that array and we were good to go with the value associated with that. However in JSON, each variable in an array can have an array of machine tags nested inside it. Its actually quite elegant if you work through the logic but we don&#8217;t care about this, we just want the data, right?!!! So let&#8217;s take wind speed from above. We wanted to get the current\_observation array and inside that get the wind_mph tag and its associated value. To do this we used the following syntax.

> [code language=&#8221;python&#8221;]
  
> print("The current wind speed (mph) is: "+ str(r\[&#8216;current\_observation&#8217;\]\[&#8216;wind\_mph&#8217;\]))
> 
> [/code]

**So What Next? **

So that&#8217;s that for today. Another simple example with some useful tricks to get you going with weather APIs. So what shall I do tomorrow??? I like this work around my commute to work. I think I&#8217;m going to solve a final challenge tomorrow with a good one, I live a 4 minute walk from my local train to work. The train comes every 15 minutes. The arrival time of the next train dictates if I have breakfast each day. I check this every day on google maps so I want to write a script that checks the TFL API and displays the next train time for me so I can quickly glance and see how long I have!