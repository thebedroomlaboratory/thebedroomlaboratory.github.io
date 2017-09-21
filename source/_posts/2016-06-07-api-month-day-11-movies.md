---
title: 'API Month Day 11 - Movies'
date: 2016-06-07T17:36:55+00:00
author: gregario
tags:
  - API
  - Month
---
[API.png](/wp-content/uploads/2015/11/API.png)

**API purpose** Interfacing and searching IMDB database
  
**Signup** not needed
  
**Documentation** http://www.omdbapi.com/
  
**Github** [Click here for link](https://github.com/gregario/API-Month/tree/master/Day11%20Movies)
  
**Comment** Surprisingly fun game

So I went to a games night last night to decide who got what teams for the upcoming Euros 2016. I do live an exciting life. Anywho we play a game sometimes where you pick a number in days, hours and minutes and have to name 3 boxsets of popular TV that would get you there.

We found some inconsistencies (and were running out of games) so I had a quick look at the omdbapi (open movie database API) to see how the data was being gathered. I found a quick call that would return the IMDB ratings of movies so I whipped up a quick script to calculate the sum of an arbitrary number of movies.

See attached  link in the header for the source. It's very short and is a pretty standard requests format if you've seen any of my other posts. The one style change I made was to use raw_input() instead of a sys.argv() to pass arguments to the script. It's a lot neater and more flexible for the sort of scripts I've been writing so I think I'll change to using it in the future.

I also won that round ...;
