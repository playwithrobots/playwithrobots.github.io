---
layout: post
title: "Simple Line Follower robot"
category: "make-it-from-scratch"
redirect_from: "/2014/04/02/minimal-urls-jekyll/"
---
![Image alt text]({{ site.baseurl }}/images/config.png)
After reading this section completely you will be playing with the one shown below. Moreover we will make it modular so that it can be easily modified in future.
The main electronics/mechanical components that will be used in making this line follower robot are two sensors made using LDRs, transistors as motor driver circuit, acrylic sheet, General purpose board, Two DC motors and battery. 
<iframe src="http://www.youtube.com/embed/o5qvvWnSbkE" frameborder="0" width="560" height="315"></iframe>
So let’s start making its chassis.
## Chassis
It’s basically the frame of the robot on which motors and wheels are mounted and all the circuitry part is also placed on it.
For base, we will be using Acrylic sheet of dimension 14x13cm square and thickness of 4mm for our chassis, it can be easily available at any picture frame shop.
Acrylic sheet
## Drive Mechanism
We will be using a three wheel differential drive using two motors and one caster wheel or an Omni directional wheel. The Direction and speed of the two motors can be controlled independently.  
Our first step would be drilling holes to fix caster and clamps for motors. Though i haven't done any drilling while making this line following robot, just pasted caster and motor clamps with the help of double sided tape!!. But if you are making it for any small college project or competition fix every thing properly with screws. Also solder a 2 pin connector to the motors pins. 
Now fix motors, caster and also attach wheels to the motors. As I said it is to made modular, attach a two pin connector to each motor.

Now the chassis is complete. Lets make its circuit!. 
Circuit
We will be using light sensors, particularly Light dependent Resistors (LDRs) to detect black line on white surface. The figure below will explain how to detect black line on white surface.
The overall circuit for this robot is shown below. To know in detail about sensor circuit see this <a class="caption" href="/robotics-pool/sensors/light-sensors" target="_blank" title="Light sensors">tutorial</a> and for motor driver circuit part see <a class="caption" href="/robotics-pool/motor-driver-circuits/dc" target="_blank" title="DC-motor driver circuits">this</a>. 
## How would the above circuit works?
The logic is simple. Left sensor will be controlling left motor, when the sensor is on white surface motor will be switched on else switched off. Similarly right motor is controlled by right sensor. The picture below will give you an idea.
  iv id="related_article" style="background-color: #eeeeee; text-align: justify;">
<p style="text-align: center;"><strong>Related articles on PlayWithRobots</strong>
<a href="/make-it-form-scratch/advance-line-follower-robot" target="_blank">Advance line follower robot</a>  |  <a href="/make-it-form-scratch/edge-avoider-robot" target="_blank">Edge avoider robot </a> |  <a href="/robotics-pool/sensors/light-sensors" target="_blank">Sensor circuits</a>  |  <a href="/robotics-pool/motor-driver-circuits/dc" target="_blank">Motor driver circuts</a>  |  <a href="/robotics-pool/avr/basic-input-output" target="_blank">AVR basic input output concepts</a></div>
Now lets make it. To sense the line properly sensors must be placed on the robot is such a way that they are very close to the ground. For this we have divided the circuit into two parts, first part would be LDR and LED pairs. These are to be soldered on a small general purpose board and mounted just in front of caster wheel facing downwards. This circuit is connected to the second part with the help of a 4 pin connector. This sensor part is modular as we can use them for another purpose also. You don't need to solder them again, just unplug the connector and use them. Ensure that distance between two LDR must be 4-5mm greater than the width of the black line. It is necessary to cover the LED LDR pair with some absorbing material in order to avoid ambient light (enviremnet light) to fall on LDR. See the pictures below. 
Second part consist of motor driver circuit and the threshold adjusting potentiometer. This part would be soldered on another general purpose board and would be placed on the top of chassis. The reason for placing potentiometer in this part is that it would be easier to adjust sensor threshold. See the pictures below. 
Now all the chassis and circuit part is done lets combine them all!.
<h2 style="text-align: justify;">Combining all
Fix the sensor part just in front caster,facing downwards. ensure that there is very less clearance between sensor covering and ground. See the picture below.
Now connect the battery to the circuit and also plugin the motors in there respective connectors. For more information regarding battery and there charging circuit see <cite class="caption" title="Coming Soon" dir="ltr">this tutorial</cite>. I am using two 3.7V Li-ions cells in series for this robot.
Small cheap 9 V batteries will not be able to drive this robot for more that 4-5 minutes.
Adjust the threshold of LDR such that when sensor is on black surface voltage at base of transistor must be less than 0.5Volts. If motors are rotating is reverse direction just change the polarity of that motor. After all this you would be able to make a robot that moves like the one below!.
<iframe src="http://www.youtube.com/embed/o5qvvWnSbkE" frameborder="0" width="560" height="315"></iframe>
Hope you liked the above tutorial. Subscribe to PlaywithRobots on facebook for more updates.