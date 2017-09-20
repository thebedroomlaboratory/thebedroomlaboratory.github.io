---
id: 324
title: 'BrewMonitor: the Arduino-powered, cloud-based homebrewing controller'
date: 2014-10-02T15:07:32+00:00
author: catchmartin
layout: post
guid: http://thebedroomlaboratory.com/?p=324
permalink: /2014/10/02/brewmonitor-the-arduino-and-cloud-based-homebrewing-controller/
image: /wp-content/uploads/2014/10/IMG_20141002_1556521.jpg
categories:
  - Blog
  - Projects
tags:
  - ESP8266
  - Homebrew
  - REST API
---
<address>
  Demo: <a href="http://dev.thebedroomlaboratory.com/%7Emartin/brewmonitor/" target="_blank">http://dev.<wbr />thebedroomlaboratory.com/~<wbr />martin/brewmonitor/</a>
</address>

<address>
  Github: <a href="https://github.com/thebedroomlaboratory/BrewMonitor" target="_blank">https://github.com/thebedroomlaboratory/BrewMonitor</a>
</address>

I recently started brewing beer at home with a group of friends and one of the things that quickly came to light, is that maintaining a steady fermention temperature can be the key to a good brew. We have a stick on thermometer on our fermenter buckets which we can use for reading the temperature of the beer, locally, but I was wondering if there was a system I could hook up, so that all of us could check in on the beer via the web. Lo and behold, there are a few systems available for monitoring/controlling the temperature of a batch of homebrew beer as it ferments. But most of them require expensive equipment and the ones that don't are still based on the [Arduino-sensor and Raspberry Pi-gateway](http://shop.brewpi.com/index.php?route=product/combos) model, which will set you back the bones of €80, if you [make it yourself](http://www.homebrewtalk.com/f51/howto-make-brewpi-fermentation-controller-cheap-466106/). As well as that, the webserver for the BrewPi system (most popular as far as I could see) runs on the Raspberry Pi in your home network. This means you have to configure port forwarding and something like dyndns to access it from outside the house, making the system configuration a bit of a chore.

[<img class="alignright size-medium wp-image-332" src="/wp-content/uploads/2014/10/BrewMonitor-Site-300x254.png" alt="BrewMonitor-Site" width="300" height="254" />](http://dev.thebedroomlaboratory.com/~martin/brewmonitor/)With that in mind, have a gander at this: <a href="http://dev.thebedroomlaboratory.com/%7Emartin/brewmonitor/" target="_blank">http://dev.<wbr />thebedroomlaboratory.com/~<wbr />martin/brewmonitor/</a> It's just a basic site, based on [this Scotch.io tutorial](http://scotch.io/tutorials/php/create-a-laravel-and-angular-single-page-comment-application), which is currently plotting the temperature in my sitting room. It's got a PHP backend ([Laravel framework](http://laravel.com/) with RESTful API), [MySQL](http://www.mysql.com/) database and an [AngularJS](https://angularjs.org/) frontend with ([n3-chart/d3](http://n3-charts.github.io/line-chart/#/) for the graph). In the house, I've whacked together a quick breadboard circuit which comprises of an [Arduino clone](http://www.dx.com/p/diy-funduino-uno-r3-development-board-microcontroller-w-usb-cable-240588), a [DS18B20 Temperature Sensor](http://www.adafruit.com/product/381) (with resistor for the i2c connection) and an [ESP8266 module](https://nurdspace.nl/ESP8266). Every minute, this wireless sensor POSTs the temperature to our REST API. This value is saved in the database and will appear in the graph whenever the page is opened. To hook it up to a fermenter, the sensor would just be placed in a <a href="https://www.hopandgrape.co.uk/thermowell-stopper.html" target="_blank">thermowell</a> in the fermenter bucket so we can see the beer temperature over time.

It will be easy to add extra functionality to this basic system as time goes on (i.e. user accounts on the cloud, authentication, a screen for the Arduino, OTA firmware updates for the Arduino, relay control of a fridge/heater, etc.). The real beauty of this system, however, is that everything is saved to the _Cloud_ and we don't need an extra gateway device (Raspberry Pi) to get it there. This reduces the cost and complexity of the installation of the system immensely! The parts for the above circuit only set me back €17.20 (DS18B20, ESP8266 and 12v Adapter from ebay and Funduino from dx.com), and these costs could be reduced again by single boarding everything, instead of using the Arduino clone (we have done this for some of our other projects already)... Potential crowd-funding campaign possibly? I'll keep you in the loop.