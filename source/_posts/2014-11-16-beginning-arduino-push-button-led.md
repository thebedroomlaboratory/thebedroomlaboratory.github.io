---
id: 466
title: Turning on an LED from a Button
date: 2014-11-16T15:15:31+00:00
author: jonni3darko
layout: post
guid: http://thebedroomlaboratory.com/?p=466
permalink: /2014/11/16/beginning-arduino-push-button-led/
image: /wp-content/uploads/2014/11/push-Button-feature-Image1.jpg
categories:
  - Tutorials
tags:
  - Arduino
  - Beginner
  - tutorial
---
So you want to Learn to program and build projects with Arduino. Me too, and I want to help you learn from my experience, as I too am a beginner.

I could do the boring, pointless Arduino version of Hello Wold, [Blink!](http://arduino.cc/en/Tutorial/Blink?from=Tutorial.BlinkingLED "Boring Hello World Blink tutorial"), tutorial that most people start with, but it doesn&#8217;t involve enough as far as I am concerned ( it&#8217;s all already done for you), but go ahead if you feel its worth it. For me, I want to be able to interact with it.

So for my first Arduino project I want to press a button to turn on an LED. This involves 2 Arduino Fundamentals, reading input (the button), processing it in our program (an Arduino sketch) and output a result ( turning on or off an L.E.D.).

so without boring you, lets Jump straight in&#8230;

**Components we need**:

  * Arduino
  * Breadboard
  * Wires
  * LED
  * Push Button
  * 1 x 10k Ω Resistor
  * 1 x 220 Ω

First I Followed the Tutorial in [Arduino Project Handbook](http://www.amazon.com/Arduino-Project-Handbook-Complete-Creating/dp/0992952603) by setting up my circuit as in the image below:

[<img class="alignnone size-large wp-image-494" src="http://thebedlab.com/wp-content/uploads/2014/11/Screen-Shot-2014-11-17-at-10.05.48-PM-1024x518.png" alt="Push Button LED circuit" width="700" height="354" />](http://thebedlab.com/wp-content/uploads/2014/11/Screen-Shot-2014-11-17-at-10.05.48-PM.png)

**IMPORTANT: ** The LED legs must be in the correct direction, make sure the Negitive Leg ( the shorter leg on the side of the flat edge of the LED) is connected to the ground and the Positive Leg ( the longer leg at the side of the rounded edge of the LED) is connected to the input pin, otherwise you will likely burn out your LED.

&nbsp;

I then started up the Adruino IDE, available [here](http://arduino.cc/en/Main/Software "Arduino Downloads").

&nbsp;

Inside the sketch I added the following code:

[c]
  
const int buttonPin = 2;
  
const int ledPin = 13;
  
int buttonState = 0;

void setup(){
    
pinMode(ledPin, OUTPUT);
    
pinMode(buttonPin, INPUT);
  
}

void loop(){
    
buttonState = digitalRead(buttonPin);
    
if(buttonState == HIGH){
      
digitalWrite(ledPin, HIGH);
    
} else{
      
digitalWrite(ledPin, LOW);
    
}
  
}
  
[/c]

If you need more information about what the code is doing, have a look at the [Reference page](http://arduino.cc/en/Reference/HomePage), but it should be mostly obvious, I hope.

Selected the Arduino Uno the menu: **Tools > Board > Arduino Uno** 

[<img class="alignnone size-large wp-image-123" src="http://blog.jonnie.io/wp-content/uploads/2014/11/Select-Uno-1024x949.png" alt="Select Uno" width="550" height="509" />](http://blog.jonnie.io/wp-content/uploads/2014/11/Select-Uno.png)

Then select the Arduino Port:

  * For Linux/windows **Tools > Board > Comx** where x is usually 3 or higher
  * For Mac **Tools > Board > tty.usbmodemxxxx** where xxxx is some number

[<img class="alignnone  wp-image-476" src="/wp-content/uploads/2014/11/Screen-Shot-2014-11-16-at-7.01.13-PM-1024x901.png" alt="Screen Shot 2014-11-16 at 7.01.13 PM" width="555" height="488" />](/wp-content/uploads/2014/11/Screen-Shot-2014-11-16-at-7.01.13-PM.png)

Then plug in the USB into your computer and Arduino and upload the code using the button as shown in the picture below

[<img class="alignnone size-large wp-image-124" src="http://blog.jonnie.io/wp-content/uploads/2014/11/upload-to-Arduino-856x1024.png" alt="upload to Arduino" width="550" height="657" />](http://blog.jonnie.io/wp-content/uploads/2014/11/upload-to-Arduino.png)

When the program is uploaded you are supposed to be able to press the the button which the program is continuously reading in the loop function and light the L.E.D. while the button is pressed….

BUT…… for me this was not the case, at least not completely. I found that when I put my hand anywhere near the circuit without actually touching the button the L.E.D. would still light up and sometimes the L.E.D. would just light up and stay on with out even touching the button as shown in the video below.



Frustrated yet? I was. So what to do when the instructions don’t work? Well for me usually I turn to [stackoverflow](http://stackoverflow.com/) for programming problems. So I had a look on the [stackexchange](http://stackexchange.com/) which is the parent website of stack overflow and found an [electronics subsection](http://electronics.stackexchange.com/ "electronics.stackexchange.com").

So I posted my issue, along with the steps I took myself to try and solve the problem (**N.B.:** _if you go to any stack exchange and don’t show you made an effort, often you will be dismissed with comments like “have you even tried Googling it yourself”, So make the effort_)

So here was [my Question to the community](http://electronics.stackexchange.com/questions/137220/why-when-i-touch-the-input-cable-or-put-my-hand-near-it-the-led-comes-on "StackExchange Question")

What I learned was that the reason the L.E.D was lighting when my hand was close to the circuit was due to _ambient electromagnetic interference_ . As ‘[Shubham](http://electronics.stackexchange.com/users/4940/shubham)’ explained to me

> It&#8217;s because your button pin is floating (susceptible to ambient electromagnetic interference).

All the second resistor is doing is draining a little current from power to ground, when it should actually be functioning as the pull-down resistor for the button pin.To fix this issue I made the following change to the circuit:

I changed this:

[<img class="alignnone size-full wp-image-125" src="http://blog.jonnie.io/wp-content/uploads/2014/11/Floating-button.png" alt="Floating Button" width="272" height="256" />](http://blog.jonnie.io/wp-content/uploads/2014/11/Floating-button.png)

To this:
  
[<img class="alignnone size-large wp-image-126" src="http://blog.jonnie.io/wp-content/uploads/2014/11/non-floating-Button.png" alt="Non Floating Button: Resistor acting as pull down resistor" width="220" height="314" />](http://blog.jonnie.io/wp-content/uploads/2014/11/non-floating-Button.png)

And now the Circuit behaves as expected.



And there you go&#8230;a functional Arduino beginners project. I know some of you might be thinking &#8220;is it not a bit complex for simply turning on an L.E.D&#8221;. For that purpose yes, it is but imagine adding a few buttons, a few motors and a bit of work to the program, and it could turn into a basic remote controlled car. Or swap out the button for a light sensor and you could have an automated light that comes on when it gets dark. The possibilities are endless. But don&#8217;t worry, like you I&#8217;m a new to this too , so we can work on it together&#8230;

I based this post on a post I wrote for [my own blog](http://blog.jonnie.io/push-button-control-led/)