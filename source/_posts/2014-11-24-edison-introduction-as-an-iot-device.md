---
id: 498
title: Edison as an IoT Device
date: 2014-11-24T15:56:32+00:00
author: gregario
layout: post
guid: http://thebedlab.com/?p=498
permalink: /2014/11/24/edison-introduction-as-an-iot-device/
image: /wp-content/uploads/2014/11/20141124_1551311.jpg
categories:
  - Projects
---
![Introduction to Edison](http://thebedlab.com/wp-content/uploads/2014/11/20141124_134215.jpg) 
# Introduction to Edison

I've been playing with the Edison that I got at the hardware hackathon BedLab attended a few weeks back. Thanks to the guys from Intel for donating a few to the BedLab fund. (Full disclosure on the post, I work for Intel over in London ([http://www.cities.io](http://www.cities.io) so I'll try to keep the gushing praise to a minimum)


![20141124_155131](http://thebedlab.com/wp-content/uploads/2014/11/20141124_155131-1024x768.jpg)

Its pretty cool, out of the box its a lot more functional than the Gen one Intel Galileo and was pretty easy to get updated and up and running. I won't go into the detail of setting it up as there was a pretty straightforward step by step guide for doing it. Broadly the steps are:


  * Install FTDI driver for the board
  * Install Arduino IDE with Intel addon
  * Install Edison drivers

Being on the internal trial for the Edison pre release they did a good job of integrating all the tools into one installer in order to talk to and work with the board.

The drivers in particular are cool, they let you:

  * connect to the device over serial (using putty to access the linux side of things),
  * Transfer Arduino scripts if you want to program it via Arduino
  * Access the storage on the Edison as an external drive

So pretty functional. Anywho links are here...

> Getting started: https://communities.intel.com/docs/DOC-23147.


The one quirk I'll say is that you need two USB's to connect to a computer to do the programming, which is a little cumbersome.I set mine up and connected it to my home wifi and then just SSH'ed into it, this is where you should be at once you complete the above getting started guide.



Some other handy things to know when playing with the device. You are not limited to Yocto, the native Linux distro that comes with the board. If you like to work through Python or Node you can use their package managers to get most things working. Working with Yocto itself can be challenging for the hobbyist. There's no apt-get for instance, which is a bit of a pain. Yocto was designed to be for robust embedded applications. Its designed to be made from source for a specific application. Its a barebones version of linux where you only load the parts of the stack you need for your application. The theory holds that the less stuff on the build the less can go wrong and the more robust your system will be.

So if you want to make a smart thermostat you can only load the systems you need, if you want to prototype something though it can take 4 hours to add that new wifi driver and build the system again from source. If you want to play with Debian on the board Emutex have released a debian build at [emutexlabs.com](http://www.emutexlabs.com/blog/220-emutex-release-ubilinux-for-intel-edison)


The next handy thing is accessing the edison as an external hard drive. You can plug it in and transfer over any files you want. SCP also works if you want to go down that route but if you want to transfer big files or pass information via a PC easily this is a nice trick. Found the inspiration here:  https://communities.intel.com/thread/55510. Once you've transferred your files from the PC to the edison, the next step is to mount the drive on the Edison  itself.


```bash
rmmod g_multi

mkdir /update

losetup -o 8192 /dev/loop0 /dev/disk/by-partlabel/update

mount /dev/loop0 /update
``` 

Then if you want to reverse the process:

```bash 
cd /
modprobe g_multi
umount /update
then pull the usb cable and re-insert it, at which stage the disk should re-appear on your host machine.
```


Finally there's been some nice benchmarking done by [David Hunt](raspberry-pi-beaglebone-black-intel-edison-benchmarked) (He also has made some pretty cool photography hacks, its worth checking out his work)

# Cloud Infrastructures

The Edison is pitched as an enabler of the internet of things (IoT) so I thought I would talk a little bit about using the Edison as a platform for sensors. There are lots of cloud based infrastructures that one can use to send data from these devices. I'm going to stick to the Linux side of things as I'm used to operating in that environment rather than through the arduino cross compiler.


There's actually an IoT development kit baked into the Edison, it posts to an intel backend. It seemed quick to setup, I had a bit of a play of a Monday evening to see what its like. There's a tutorial [here](http://iotkit-comm-js.s3-website-us-west-2.amazonaws.com) if you're interested. There's a node and C version depending on preference. In an hour or so I had an account setup and the device associated with its backend sending a virtual sensor reading. Can't speak to its scalability/feature set but it had a shallow learning curve at the very least.


Another option is to build your own cloud storage system. At Bedlab this is becoming a bit of a specialty with with a bunch of different types of IoT style systems with various time series datastore types being made and even (feel free to correct me here guys)  3 RESTful API's being built at this stage for various projects. Check out the following for more info:

  * BrewLab backend storage and graphing
  * NodeRed implementation for Treo
  * How to build your own RESTful API tutorial over at http://blog.jonnie.io/creating-a-restful-api-with-node-js/ by our own Jonnie.

There's other online based systems that can quickly be setup to do the heavy lifting for your IoT device. I've had a play with GERAS from the guys over at www.1248.io, its quite good, doing exactly what you need it to, reminiscent of the old Pachube system. Xively is probably the best known system. Formerly Cosm, Formerly Pachube... Its so good they named it trice. Anywho, how I've finished kludgening that previous sentence into my post lets wrap up. I'll write a follow up post on playing with the Edison over Xively. Stay tuned for more .
