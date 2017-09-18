---
id: 735
title: 'API Month Day 3 &#8211; TFL API'
date: 2015-12-04T17:00:33+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=735
permalink: /2015/12/04/api-month-day-3-tfl-api/
image: /wp-content/uploads/2015/12/JSON_TFL.jpg
categories:
  - Uncategorised
tags:
  - API
---
API purpose: Commuting Data
  
Signup: No Signup
  
Documentation: <a href="https://api-portal.tfl.gov.uk/docs" target="_blank">https://api-portal.tfl.gov.uk/docs</a>
  
Github: <a href="https://github.com/gregario/API-Month/tree/master/Day3%20Maps" target="_blank">https://github.com/gregario/API-Month/tree/master/Day3%20Maps </a> Comment: surprisingly challenging

So as I said yesterday today I want to find the arrival time of my local train so I can plan my morning breakfast intake! It turned out to be quite challenging&#8230; Firstly a comment on the TFL (transport for london) API services. They&#8217;re all over the place. I found the following resources to extract data about journeys, stop locations and times:

<a href="https://api.tfl.gov.uk/#Journey" target="_blank">https://api.tfl.gov.uk/#Journey</a>
  
<a href="http://countdown.tfl.gov.uk/" target="_blank">http://countdown.tfl.gov.uk/</a>

and two sets of documentation at:

<a href="https://api-portal.tfl.gov.uk/docs" target="_blank">https://api-portal.tfl.gov.uk/docs</a>
  
<a href="https://api.tfl.gov.uk/" target="_blank">https://api.tfl.gov.uk/</a>

So I eventually used the API portal to get access to arrival times, it wasn&#8217;t the most straightforward information set to work with however. Check out the photo!
  
[<img class="alignnone size-medium wp-image-740" src="http://localhost/wp-content/uploads/2015/12/JSON_TFL-300x166.jpg" alt="JSON_TFL" width="300" height="166" />](http://localhost/wp-content/uploads/2015/12/JSON_TFL.jpg)

The photo shows a typical API response from a station arrival time call. We want one variable from this giant list! This is a good time to work with a list like this as many API&#8217;s are complex like this one so it gives me an opportunity to go through the detail and figure out how to extract the data.

I got to play with some good stuff here such as operating on, iterating over and extracting conditional data from JSON objects. Also doing operations on time while pulling the current real time from the python datetime module.

The key for the code here is that the API is a list where each element in the list is a JSON object (that we manipulate as a python dict). Confused? I was&#8230; But its OK to work with in practice. What happens here is we write some code to loop through the list and for every JSON element in the list do a value search for arrival time. This gives us the arrival time of all trains into my station. However I only want certain trains heading in one direction. So I run an if with the loop checking for the relevant trains. If they are present pop the arrival time from that train into a new array. Then we have an array with all the relevant arrival times. Just sort that and you have the train that will arrive first. Pop that out and you have a variable to work with. YAY. Taking that from the current time gives you the number you are looking for.

I&#8217;ve explained the logic of what I want to do now let&#8217;s look at the code. If you are reading this (I do doubt anyone is) I am trying to improve the way in which I write these tutorials. Today I&#8217;m trying to explain how all the code works as comments. Hopefully one can understand how it works just from that.

[code language=&#8221;python&#8221;]

\# -\*- coding: utf-8 -\*-
  
\# Program to check how long it will take me to get to work
  
# Greg Jackson 1st dev 2015
  
# Twitter @gr3gario or github gregario
  
# Day three of the Month of API

import requests
  
import json
  
import sys # needed to pass arguments from command line
  
import datetime

url = "https://api.tfl.gov.uk/StopPoint/910grctryrd/arrivals" # the stop number is returned from the TFL website from a manual search. This calls the data
  
r = requests.get(url).json() # Make a request to the TFL API for data
  
time = [] # List for my future train arrivals
  
for key in r: # the returned object is a list with nested JSON objects inside each list. So you need to iterate through the list and do operations on each object separately
  
if key[&#8216;destinationName&#8217;] == ("Cheshunt Rail Station") or ("Enfield Town Rail Station"): # This filters out trains to different destinations. I can take either of these trains
  
time.append(key[&#8216;expectedArrival&#8217;]) # Adds expected arrival time from each train data structure to the time list

time_sorted = sorted(time) # sorts the time list so we get the train due to arrive first
  
time\_train = time\_sorted.pop(0) # pops out the first train to arrive and stores as a string
  
\# this translates the time from a string in the list to a usable string, taking out the date.
  
\# A note on how I deal with the date and time operations here.
  
\# Its TERRIBLE. it works but I&#8217;m sure there&#8217;s a much cleaner way of doing this.
  
time\_train\_temp = time_train.split(&#8216;T&#8217;,1)[-1]
  
time\_train\_parsed = time\_train\_temp.split(&#8216;.&#8217;,1)[0]

current_time = str(datetime.datetime.now())
  
current\_time\_temp = current_time.split(&#8216; &#8216;,1)[-1]
  
current\_time\_parsed = current\_time\_temp.split(&#8216;.&#8217;,1)[0]
  
#print k

\# Converts the two hour:minute:second strings back into time variables.
  
timeA = datetime.datetime.strptime(time\_train\_parsed, &#8216;%H:%M:%S&#8217;)
  
timeB = datetime.datetime.strptime(current\_time\_parsed, &#8216;%H:%M:%S&#8217;)

\# Takes the time of the next train away from the current time to give an estimated time until arrival of the next train I can take
  
time_delta = timeA-timeB
  
print ("The next train to work will arrive in " +str(time_delta))

[/code]

And it works!
  
[<img class="alignnone size-medium wp-image-739" src="http://localhost/wp-content/uploads/2015/12/Output_day3-300x38.jpg" alt="Output_day3" width="300" height="38" />](http://localhost/wp-content/uploads/2015/12/Output_day3.jpg)

I&#8217;ve never been so happy to see some command line arguments! This was day three but I ran over time so I&#8217;m going to immediately do day 4 too 🙂 Stay tuned.

&nbsp;