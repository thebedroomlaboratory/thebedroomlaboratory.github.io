---
title: 'API Month Day 10 - Oasis or Blur'
date: 2015-12-10T14:03:25+00:00
author: gregario
tags:
  - API
---
![](/wp-content/uploads/2015/12/oasisorblur.jpg)

**API purpose** Interfacing and searching twitter
  
**Signup** <a href="https://dev.twitter.com/apps/new" target="_blank">https://dev.twitter.com/apps/new</a>
  
**Documentation** <a href="https://dev.twitter.com/rest/public" target="_blank">https://dev.twitter.com/rest/public</a>
  
**Github** <a href="https://github.com/gregario/API-Month/tree/master/Day10%20Twitter" target="_blank">Click here for link</a>
  
**Comment** So much that could be done with this

Today is so easy. After reading into the Twitter API it became obvious that people had written so much on this subject. So to get started you do the following.

After running

{% codeblock %}
easy_install twitter
{% endcodeblock %}

Just look at this resource: <a href="https://github.com/ideoforms/python-twitter-examples" target="_blank">https://github.com/ideoforms/python-twitter-examples </a>

It's so good, gives examples for searching by hashtag (both as a sample or from the streaming service), searching by area, posting to your feed and doing a bunch of general analytics.

Make sure you have installed twitter tools (via the above command) and not python-twitter which is a separate set of tools. This lead to a bit of confusion on my part. I wrote a simple app that searches hashtags for Oasis and Blur to answer the age old question once and for all. Enjoy!

Apparently it's Blur!

![](/wp-content/uploads/2015/12/Day10Output.jpg)