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
# [
  
](http://thebedlab.com/wp-content/uploads/2014/11/20141124_134215.jpg) INtroduction to Edison

<p style="text-align: justify;">
  I&#8217;ve been playing with the Edison that I got at the hardware hackathon BedLab attended a few weeks back. Thanks to the guys from Intel for donating a few to the BedLab fund. (Full disclosure on the post, i work for Intel over in London (<a title="Linked Here" href="http://www.cities.io" target="_blank">www.cities.io</a>) so I&#8217;ll try to keep the gushing praise to a minimum)
</p>

[<img class="aligncenter size-large wp-image-512" src="http://thebedlab.com/wp-content/uploads/2014/11/20141124_155131-1024x768.jpg" alt="20141124_155131" width="700" height="525" />](http://thebedlab.com/wp-content/uploads/2014/11/20141124_155131.jpg)

<p style="text-align: justify;">
  Its pretty cool, out of the box its a lot more functional than the Gen one Intel Galileo and was pretty easy to get updated and up and running. I won&#8217;t go into the detail of setting it up as there was a pretty straightforward step by step guide for doing it. Broadly the steps are:
</p>

  * Install FTDI driver for the board
  * Install Arduino IDE with Intel addon
  * Install Edison drivers

<p style="text-align: justify;">
  Being on the internal trial for the Edison pre release they did a good job of integrating all the tools into one installer in order to talk to and work with the board.<br /> The drivers in particular are cool, they let you:
</p>

  * connect to the device over serial (using putty to access the linux side of things),
  
    -Transfer Arduino scripts if you want to program it via Arduino
  * Access the storage on the Edison as an external drive

So pretty functional. Anywho links are here&#8230;

> Getting started: https://communities.intel.com/docs/DOC-23147.

<p style="text-align: justify;">
  The one quirk I&#8217;ll say is that you need two USB&#8217;s to connect to a computer to do the programming, which is a little cumbersome.I set mine up and connected it to my home wifi and then just SSH&#8217;ed into it, this is where you should be at once you complete the above getting started guide.
</p>

<p style="text-align: justify;">
  Some other handy things to know when playing with the device. You are not limited to Yocto, the native Linux distro that comes with the board. If you like to work through Python or Node you can use their package managers to get most things working. Working with Yocto itself can be challenging for the hobbyist. There&#8217;s no apt-get for instance, which is a bit of a pain. Yocto was designed to be for robust embedded applications. Its designed to be made from source for a specific application. Its a barebones version of linux where you only load the parts of the stack you need for your application. The theory holds that the less stuff on the build the less can go wrong and the more robust your system will be.
</p>

<p style="text-align: justify;">
  So if you want to make a smart thermostat you can only load the systems you need, if you want to prototype something though it can take 4 hours to add that new wifi driver and build the system again from source. If you want to play with Debian on the board Emutex have released a debian build: http://www.emutexlabs.com/blog/220-emutex-release-ubilinux-for-intel-edison
</p>

<p style="text-align: justify;">
  The next handy thing is accessing the edison as an external hard drive. You can plug it in and transfer over any files you want. SCP also works if you want to go down that route but if you want to transfer big files or pass information via a PC easily this is a nice trick. Found the inspiration here:  https://communities.intel.com/thread/55510. Once you&#8217;ve transferred your files from the PC to the edison, the next step is to mount the drive on the Edison  itself.
</p>

> &nbsp;
> 
> rmmod g_multi
> 
> mkdir /update
> 
> losetup -o 8192 /dev/loop0 /dev/disk/by-partlabel/update
> 
> mount /dev/loop0 /update
> 
> &nbsp;

&nbsp;

<div>
  Then if you want to reverse the process:
</div>

<div>
</div>

> <div>
>   <p>
>     cd /
>   </p>
>   
>   <p>
>     umount /update
>   </p>
>   
>   <p>
>     modprobe g_multi
>   </p>
>   
>   <p>
>     then pull the usb cable and re-insert it, at which stage the disk should re-appear on your host machine.
>   </p>
> </div>

<div>
  Finally there&#8217;s been some nice benchmarking done by David Hunt (He also has made some pretty cool photography hacks, its worth checking out his work)
</div>

<div>
</div>

> <div>
>   http://www.davidhunt.ie/raspberry-pi-beaglebone-black-intel-edison-benchmarked/
> </div>

&nbsp;

# Cloud Infrastructures

<p style="text-align: justify;">
  The Edison is pitched as an enabler of the internet of things (IoT) so I thought I would talk a little bit about using the Edison as a platform for sensors. There are lots of cloud based infrastructures that one can use to send data from these devices. I&#8217;m going to stick to the Linux side of things as I&#8217;m used to operating in that environment rather than through the arduino cross compiler.
</p>

<p style="text-align: justify;">
  There&#8217;s actually an IoT development kit baked into the Edison, it posts to an intel backend. It seemed quick to setup, I had a bit of a play of a Monday evening to see what its like. There&#8217;s a tutorial <a title="IoT_Dev_Kit" href="http://iotkit-comm-js.s3-website-us-west-2.amazonaws.com/" target="_blank">here</a> if you&#8217;re interested. There&#8217;s a node and C version depending on preference. In an hour or so I had an account setup and the device associated with its backend sending a virtual sensor reading. Can&#8217;t speak to its scalability/feature set but it had a shallow learning curve at the very least.
</p>

<p style="text-align: justify;">
  Another option is to build your own cloud storage system. At Bedlab this is becoming a bit of a specialty with with a bunch of different types of IoT style systems with various time series datastore types being made and even (feel free to correct me here guys)  3 RESTful API&#8217;s being built at this stage for various projects. Check out the following for more info:
</p>

  * BrewLab backend storage and graphing
  * NodeRed implementation for Treo
  * How to build your own RESTful API tutorial over at http://blog.jonnie.io/creating-a-restful-api-with-node-js/ by our own Jonnie.

<p style="text-align: justify;">
  There&#8217;s other online based systems that can quickly be setup to do the heavy lifting for your IoT device. I&#8217;ve had a play with GERAS from the guys over at www.1248.io, its quite good, doing exactly what you need it to, reminiscent of the old Pachube system. Xively is probably the best known system. Formerly Cosm, Formerly Pachube&#8230; Its so good they named it trice. Anywho, how I&#8217;ve finished kludgening that previous sentence into my post lets wrap up. I&#8217;ll write a follow up post on playing with the Edison over Xively. Stay tuned for more .
</p>