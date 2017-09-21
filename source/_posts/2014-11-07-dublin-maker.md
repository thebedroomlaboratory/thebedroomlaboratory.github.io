---
id: 388
title: Dublin Maker
date: 2014-11-07T19:23:43+00:00
author: gregario
layout: post
guid: http://thebedroomlaboratory.com/?p=388
permalink: /2014/11/07/dublin-maker/
image: /wp-content/uploads/2014/09/DSC_0105_1_compressed1.jpg
categories:
  - Maker
---
![Preparation](/wp-content/uploads/2014/09/DSC_0161_1_compressed.jpg) 
# Preparation
The final prep was/is upon us! We were incredibly tight to the deadline so we're doing this one post hoc...
Two nights of pain, misery and electronics lay/lie ahead/?. Baton down the hatches and tell your other halves you love them.


## Thursday night

![Martin and Greg do science.](/wp-content/uploads/2014/10/DSC_0115.jpg) 

Martin and Greg do science.

![DSC_0115_1_compressed](/wp-content/uploads/2014/09/DSC_0115_1_compressed.jpg)

Martin worked on the sensor aggregation and Greg worked on the sensor box enclosure and PCB design. The PCB came out awesome. It was made using the etching process described in a related post. It is surprisingly detailed!!! Check out the close up...

![DSC_0105_1_compressed](/wp-content/uploads/2014/09/DSC_0105_1_compressed.jpg)


For a compact package it does quite a lot! temperature, humidity and light are being measured. It is then read on a ATTIny chip and then transferred over bluetooth to a gateway device. It is, to borrow a word, the tits.

## Box enclosure

The box came out alright! Pic of drawing it up with martin during the week... I'm going to write up a post about the process separately. It was quite nice to go from an idea to a working prototype in 3 days. shows the power of modern maker tools. Anywho, the output was pretty!
![DSC_0161_1_compressed](/wp-content/uploads/2014/09/DSC_0161_1_compressed.jpg)

It was cut in the UCL institute of making, on their super awesome laser cutter. we're going to go through a big upload of the various parts of the design, between thingiverse and github. Stay tuned, we've a big lump of this to do over the coming month or so!

Plug was fun, it always facinates me the practical mechanical solutions to older technologies. I would always think of electronic solutions to problems.

The classic example is the shower (bear with me)

![bear-and-man.jpg](http://www.thisblogrules.com/wp-content/uploads/2010/02/bear-and-man.jpg)

A shower does PID style portortional control of temperature using purely mechanical technologies. The mixer uses a 3/2 valve to mix the hot and cold.

![HydraulicSystems DVHFigure](http://www.daerospace.com/HydraulicSystems/DVHFigure%203.png)

However as you shower the hot water reduces and the cold water increases and your temperature changes. how the system adjusts for this is by including a wax in the inside of the barrel of the 3/2 valve. The wax contracts as it gets colder and shifts the valve over a bit. This increases the flow of hot water in relation to cold water and to the user maintains (theoretically) a more steady and temperature consistent flow of water.

This obviously has its downsides... The response time of the material (or its {science term for what I'm talking about}) is quite slow and cannot account for sudden reducitions in hot or cold water. This is why a flush of your toilet can scald you or someone turning on the hot tap in the kitchen makes you super cold. Anyway I digress... So 3/2 valv... Extension cords.

![DSC_0150_compressed](/wp-content/uploads/2014/09/DSC_0150_compressed.jpg)


Its super mechanical. Taking it apart was a lot of fun and brought me back to my mechatronic roots. It was a simple fix. Remove the switch and wire in wires to each of the individual live lines of each switch. We stripped a kettle lead to get the proper thickness wire and broke our the wires through the the bottom part of the plug through drill holes. These fed into the acrylic box through the lasercut holes. This was attached to relays and hey presto, electromechanical switches that can be arduino controlled. Check out the final product:

![DSC_0067_compressed](/wp-content/uploads/2014/09/DSC_0067_compressed.jpg)
stay tuned for github and thingiverse link ups here and feel free to comment on any suggestions for changes below the fold.

Hope you learned something about <span style="text-decoration: line-through;">showers</span> smart plugs.


## Friday night
I'm tagging in the gang WWE style here as I was sleeping


## MakerFaire Day
The weekend went really well. Got to talk to a lot of people about our open source projects and how home automation can be improved through the use of open source technologies. The stand looked pretty cool too!

![DSC_0065_1_compressed](/wp-content/uploads/2014/09/DSC_0065_1_compressed.jpg)

One of my favourite bits of the faire was the twitter knitter from TOG. You can see our bedlab scarf on the table, it was awesome!!!

There were some other really fun projects. There was a modular music modulator box system, a turntable giant spirograph and a blacksmith.

We also met our first fan, everyone was happy about this other than the fan.

![DSC_0075_compressed](/wp-content/uploads/2014/09/DSC_0075_compressed.jpg)

I spent a fair bit of my time at the intel stand as it was a bit of a work trip for me. It was a lot of fun, I played the Mrs. Doubtfire for the night (sans the crossdressing (or even a reversible shirt)) managed to get over to both for much of the day. I was showing a twitter activated bubble maker. I never thought I would utter the phrase &#8220;I just can't get my bubble machine to connect to the internet&#8221; but alas I did. It looks pretty nice though!

![Embedded image permalink](https://pbs.twimg.com/media/By4CtGoIEAAetbY.jpg)

  Anywho, that was us. We look forward to the next one... Bring it on!!!
