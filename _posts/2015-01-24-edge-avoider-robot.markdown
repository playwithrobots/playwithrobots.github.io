---
layout: post
title: "Edge avoider robot"
category: "make-it-from-scratch"
redirect_from: "/2012/04/02/minimal-urls-jekyll/"
---
##[ Edge avoider robot](/make-it-form-scratch/edge-avoider-robot)

A robot that moves on an elevated surface by automatically detecting edges and avoiding the fall. !!

This tutorial is on making edge avoider robot can be seen in the video below: 

 <iframe src="http://www.youtube.com/embed/9R7hQVO5Se8" frameborder="0" width="640" height="360"></iframe>

###  

### Components used: 

#### Electronics

L293D, NE555 IC, one sensor made using IR LED, photodiode and LM324 IC

#### Mechanical

Acrylic sheet, General Purpose Board and two DC motors.  

### Concept: 

Robot will be move forward as long as the sensor detects an surface under it. As soon as edge detector sensor goes out of the table, the robot will make an in-place rotation greater than 90 degree and then continue as per sensor value. 

### Chassis: 

Its chassis is similar to the one made for [simple line follower robot](/make-it-form-scratch/simple-line-follower-robot#chassis "Chassis tutorial"). You can make exactly the same one, picture of complete chassis is attached below:

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Chassis complete](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_dsc_0278.jpg "Chassis complete")](/images/dsc_0278.jpg "Chassis complete")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Chassis complete</td></tr></table>

### **Circuit: **

I tried to make it as simple as possible. Its circuit is divided into two parts, one is sensor part and other is logic and motor driver part.

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Circuit Diagram- control part](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_EDGE-circuit-new.png "Circuit Diagram - control part")](/images/EDGE-circuit-new.png "Circuit Diagram - control part")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Circuit Diagram - control part</td></tr></table>

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Circuit Diagram- sensor part](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_Edge-sensor_circuit.png "Circuit Diagram- sensor part")](/images/Edge-sensor circuit.png "Circuit Diagram- sensor part")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Circuit Diagram- sensor part</td></tr></table>

Now its sensor will be placed write in front of the robot. So the sensor circuit will be soldered on a small General Purpose Board and the remaining circuit will be soldered on other General Purpose Board and both will be connected with the help of 3 pin connector. 

The sensor circuit for this robot is similar to that of object detection sensor made earlier for [Advance line follower robot](/make-it-form-scratch/advance-line-follower-robot#obstacle "Obstacle sensor tutorial"). As said earlier, while making that sensor, that we will make it modular so that it can be used with any other robot, now sticking to my words I'm using that board for this robot as edge detector sensor, I haven't made a new circuit. This is the benefit of making modular circuits. You can make exactly the same sensor circuit, it will look like the picture below: 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Edge Detector sensor circuit](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_obstacle_sensor.jpg "Edge Detector sensor circuit")](/images/obstacle sensor.jpg "Edge Detector sensor circuit")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Edge Detector sensor circuit</td></tr></table>

L293d is used for motor driver circuit, if you haven't used this IC yet for any project, you can read this quick and easy tutorial of [motor driver circuits using L293D](/robotics-pool/motor-driver-circuits/dc#l293d-l298 "L293d usage tutorial")

The figure below shows my soldered circuit of logic and motor driver part. A 3-pin connector is visible in the image (left of 555 timer) , which will be used for connecting this circuit and sensor circuit. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Soldered circuit-2 ](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_Edge-circuit.jpg "Soldered circuit -2")](/images/Edge-circuit.jpg "Soldered circuit -2")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Soldered circuit -2</td></tr></table>

### Logic:

Now a question may arise that what is the use of NE555 timer in this circuit? The answer is NE555 is used as a monostable vibrator i.e. once triggered (Voltage at pin 2 falls below Vcc/3), a high logic pulse of specific time will appear on the output pin i.e. pin 3. The width of this pulse depends on the Resistance R (between 7th pin and Vcc) and capacitor C1 by the equation

<div id="related_article" style="background-color: #eeeeee; text-align: justify;">

**Related articles on PlayWithRobots**

[Simple line follower robot](/make-it-form-scratch/simple-line-follower-robot)  |  [Advance line follower robot ](/make-it-form-scratch/advance-line-follower-robot) |  [Sensor circuits](/robotics-pool/sensors/light-sensors)  |  [Motor driver circuts](/robotics-pool/motor-driver-circuits/dc)  |  [AVR basic input output concepts](/robotics-pool/avr/basic-input-output)</div>

T (pulse width in seconds) = 1.1RC1

Now I have connected a variable resistance of 20K in place of R so that we can adjust the pulse width. So the maximum pulse width possible from this combination is 2.2sec.

Till now, we are able to generate a pulse of fixed time whenever sensor comes out of the table. We will be using this pulse to reverse the direction of one motor in order to make a in-place rotation for certain duration. For this a transistor is used as NOT gate. Adjust the duration of this in-place rotation by changing the pulse width such that when edge is detected angle of rotation should be in-between 110-150 degree. 

NOTE: When powered on, the robot will make an in-place rotation while placed on table and after that will continue normally.

### Combining all: 

Now sensor, motor driver circuit, and chassis are ready so lets combine them all!.

Sensor placement is important, fix it in the front of the robot by extending robot chassis. During robot's motion sensor may vibrate, adjust the threshold and height of sensor such that its output will not fluctuate. The picture below will give you an idea. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Sensor Placement ](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_Edge-sensor_placement.jpg "Sensor Placement ")](/images/Edge-sensor placement.jpg "Sensor Placement ")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Sensor Placement </td></tr></table> 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Complete bot](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_Edge-complete.jpg "Complete bot")](/images/Edge-complete.jpg "Complete bot")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Complete bot</td></tr></table>

The video once again !!

<iframe src="http://www.youtube.com/embed/9R7hQVO5Se8" frameborder="0" width="640" height="360"></iframe>

<span>Hope you liked the above tutorial. Subscribe to PlaywithRobots on facebook for more updates.</span>

<div style="clear:both"></div>

 ** We have changed our commenting engine for better notification and privacy, previous comments for this article are available   [here.](http://graph.facebook.com/comments/?ids=http://playwithrobots.com/make-it-form-scratch/edge-avoider-robot)  **

