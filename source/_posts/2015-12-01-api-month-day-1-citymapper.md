---
id: 718
title: 'API Month Day 1 &#8211; Citymapper'
date: 2015-12-01T17:08:47+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=718
permalink: /2015/12/01/api-month-day-1-citymapper/
image: /wp-content/uploads/2015/12/waiting-for-the-train-kronberg-im-taunus.jpg
categories:
  - Uncategorised
tags:
  - API
---
So day one has arrived, if you are curious as to what I&#8217;m talking about have a look here. So I have to decide every day if I am going to cycle to work or take my local train. Lots of info helps me make this decision.

How long will the train take?
  
Will it rain?
  
How hungover am I?

Now API&#8217;s can&#8217;t help with the last one (although google now is getting pretty close to being able to guess) but it can help with the first two. To start today I thought I would start with a really simple one, how long will it take to get to work by train?

This can very variable. I have to change from train to tube and then change tube too to get to work. It&#8217;s a pain. So hence why I check. So I wrote this simple program, Train.py, to check to see my estimated commuting time to work. As my bike commute is a pretty predictable 44-48 minutes i can then make a decision.

This is a simple piece of code but I&#8217;ll describe what you need to use an API and the practicalities around using it in python and manipulating its output.

&nbsp;

Lets start with the Citymapper API itself. It&#8217;s very straightforward:
  
&#8211; Head <a href="https://content.citymapper.com/i/897/citymapper-for-developers" target="_blank">here</a> to register for an account and an API key.
  
&#8211; Head <a href="https://citymapper.3scale.net/docs" target="_blank">here</a> to check out the API documentation.

You can use the documentation page to do a sample push and get an idea of the form of a request. I use a chrome extension called postman to check my calls and responses to make sure I have everything right before I start programming. So as an example to check the API to see travel time between two points you would call:

> https://staging-developer.citymapper.com/api/1/traveltime/?startcoord=51.2688199%2C-0.1783686&endcoord=51.560117%2C-0.0722408&time_type=arrival&key=[INSERT KEY]

So its pretty human readable, to go through it, you are checking the Citymapper mapper API server for a travel time. Then after the ? you can specify a list of parameters, the order doesn&#8217;t matter but there are required inputs. You can see above I specify start location, end location, arrival time and my key.

I obviously haven&#8217;t included my own key but if you were to put your own key there and put that whole message into POSTMAN or your browser you would see the following response.

> { u&#8217;travel\_time\_minutes&#8217;: 54, u&#8217;diagnostic&#8217;: {u&#8217;milliseconds&#8217;: 2907} }

Again this is in a lovely human readable JSON (Just Simple Ordinary Notation) format. If we were to do some JSON parsing we could pull out the &#8220;54&#8221; minutes variable and we&#8217;d have our answer.

So how do I program this? I use python for all my programming needs so I&#8217;ll discuss this now. The requests library is your friend so if you don&#8217;t have it installed pop  over to your favourite terminal window and run:

> sudo easy_install requests

Once that is installed, you can run the following python program to print out on the command line what we just ran in a browser window.

> #import requests
  
> #import json
> 
> r = requests.get (&#8220;https://staging-developer.citymapper.com/api/1/traveltime/?startcoord=51.2188199%2C-0.1013686&endcoord=51.560117%2C-0.0722408&time_type=arrival&key=[INSERTKEYHERE]&#8221;)
  
> #print(r.json())

Output looks like this:

> { u&#8217;travel\_time\_minutes&#8217;: 54, u&#8217;diagnostic&#8217;: {u&#8217;milliseconds&#8217;: 2907} }

Look familiar? Yes? Great. If you use the following code you will just return 54.

> r = requests.get (&#8220;https://staging-developer.citymapper.com/api/1/traveltime/?startcoord=51.2188199%2C-0.1013686&endcoord=51.560117%2C-0.0722408&time_type=arrival&key=[INSERTKEYHERE]&#8221;).json()
  
> print(r[&#8216;travel\_time\_minutes&#8217;])

There you go. If you want to play with JSON more have a look at this tutorial <a href="http://docs.python-guide.org/en/latest/scenarios/json/" target="_blank">here</a>. I found it super helpful. Finally I want to make this a little more user friendly by including the payload as a separate variable. This way you can make changes easily or include this as a function in a larger program or load the start/end coordinates from a file.

> url = &#8220;https://staging-developer.citymapper.com/api/1/traveltime/&#8221;
  
> payload = {&#8216;startcoord&#8217;: &#8216;51.4618199,-0.1793686&#8217;, &#8216;endcoord&#8217;: &#8216;51.560117,-0.0722408&#8242;,&#8217;time_type&#8217;:&#8217;arrival&#8217;,&#8217;key&#8217;:&#8217;INSERTKEYHERE&#8217;}
  
> r = requests.get(url, params=payload).json()
  
> print(r[&#8216;travel\_time\_minutes&#8217;])

So that&#8217;s me, day one was pretty simple but this is a learning experience for me. I haven&#8217;t played with a lot of these simple programming methods before so I&#8217;m learning as I go. My code is up on Github <a href="https://github.com/gregario/API-Month/tree/master/Day%201%20-%20Time%20to%20train" target="_blank">here</a> if you want to play.

I got curious to see how much this commuting time varied over the course of a day. So I wrote another program TrainLoop.py that ran forever, checking once every 90 seconds and piping out a file that I can plot tomorrow. Why 90 seconds you ask? There&#8217;s a 1000 call limit per day on the free API for Citymapper. 24 hours / 1000 is a API call every 86 seconds.

Tomorrow I&#8217;ll look at a weather service to find out will it rain and if it will rain during the day. Could be useful for a comparison. Should be fun 🙂