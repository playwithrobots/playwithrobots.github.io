---
layout: post
title: "Simple Line Follower robot"
category: "make-it-from-scratch"
comments : true
redirect_from: "/make-it-form-scratch/simple-line-follower-robot/"
---
It is a machine that follows a line, either a black line on white surface or vise-versa. For Beginners it is usually their first robot to play with. In this tutorial, we will teach you to make the line follower robot move on the line with a type of feedback mechanism. It’s the most basic example of adding small intelligence to a robot, but it’s actually the designer’s intelligence!!

After reading this section completely you will be playing with the one shown below. Moreover we will make it modular so that it can be easily modified in future.

The main electronics/mechanical components that will be used in making this line follower robot are two sensors made using LDRs, transistors as motor driver circuit, acrylic sheet, General purpose board, Two DC motors and battery.

<iframe src="http://www.youtube.com/embed/o5qvvWnSbkE" frameborder="0" width="560" height="315"></iframe>

So let’s start making its chassis.

## Chassis

It’s basically the frame of the robot on which motors and wheels are mounted and all the circuitry part is also placed on it.

For base, we will be using Acrylic sheet of dimension 14x13cm square and thickness of 4mm for our chassis, it can be easily available at any picture frame shop.

{% include image.html img="images/old/dsc_0262.jpg" title="Acrylic sheet" caption="Acrylic sheet" class="lazyload" %}

## Drive Mechanism

We will be using a three wheel differential drive using two motors and one caster wheel or an Omni directional wheel. The Direction and speed of the two motors can be controlled independently.  

{% include image.html img="images/old/dsc_0267.jpg" title="Motor, Motor clamp and tyre" caption="Motor, Motor clamp and tyre" class="lazyload" %}

{% include image.html img="images/old/dsc_0270.jpg" title="Caster wheel" caption="Caster wheel" class="lazyload" %}

{% include image.html img="images/old/chasis diagram.jpg" title="Chassis Layout" caption="Chassis Layout" class="lazyload" %}

Our first step would be drilling holes to fix caster and clamps for motors. Though i haven't done any drilling while making this line following robot, just pasted caster and motor clamps with the help of double sided tape!!. But if you are making it for any small college project or competition fix every thing properly with screws. Also solder a 2 pin connector to the motors pins. 

{% include image.html img="images/old/dsc_0274.jpg" title="Motors with connector" caption="Motors with connector" class="lazyload" %}

Now fix motors, caster and also attach wheels to the motors. As I said it is to made modular, attach a two pin connector to each motor.

{% include image.html img="images/old/dsc_0278.jpg" title="Final chassis" caption="Final chassis" class="lazyload" %}

Now the chassis is complete. Lets make its circuit!. 

## Circuit

We will be using light sensors, particularly Light dependent Resistors (LDRs) to detect black line on white surface. The figure below will explain how to detect black line on white surface.

{% include image.html img="images/old/principle.jpg" title="Line detection logic" caption="Line detection logic" class="lazyload" %}

The overall circuit for this robot is shown below. To know in detail about sensor circuit see this [tutorial](/light-sensors "Light sensors") and for motor driver circuit part see [this](/dc-motor-driver-circuits "DC-motor driver circuits"). 

{% include image.html img="images/old/lfr-without mcu complete.jpg" title="Complete circuit" caption="Complete circuit" class="lazyload" %}

## How would the above circuit works?

The logic is simple. Left sensor will be controlling left motor, when the sensor is on white surface motor will be switched on else switched off. Similarly right motor is controlled by right sensor. The picture below will give you an idea.

{% include image.html img="images/old/lfr-logic.jpg" title="logic" caption="logic" class="lazyload" %}

**Related articles on PlayWithRobots**
<div class="related-articles">
[Advance line follower robot](/advance-line-follower-robot)  |  [Edge avoider robot ](/edge-avoider-robot) |  [Sensor circuits](/light-sensors)  |  [Motor driver circuts](/dc-motor-driver-circuits)  |  [AVR basic input output concepts](/avr-basic-io)</div>

Now lets make it. To sense the line properly sensors must be placed on the robot is such a way that they are very close to the ground. For this we have divided the circuit into two parts, first part would be LDR and LED pairs. These are to be soldered on a small general purpose board and mounted just in front of caster wheel facing downwards. This circuit is connected to the second part with the help of a 4 pin connector. This sensor part is modular as we can use them for another purpose also. You don't need to solder them again, just unplug the connector and use them. Ensure that distance between two LDR must be 4-5mm greater than the width of the black line. It is necessary to cover the LED LDR pair with some absorbing material in order to avoid ambient light (enviremnet light) to fall on LDR. See the pictures below. 

{% include image.html img="images/old/general_purpose_board.jpg" title="General purpose board" caption="General purpose board" class="lazyload" %}

{% include image.html img="images/old/sensor_ckt.jpg" title="Sensor Part soldered" caption="Sensor Part soldered" class="lazyload" %}

{% include image.html img="images/old/covered_sensor.jpg" title="Insulated soldered part" caption="Insulated soldered part" class="lazyload" %}

{% include image.html img="images/old/sensor_covering.jpg" title="sensor covering" caption="sensor covering" class="lazyload" %}

Second part consist of motor driver circuit and the threshold adjusting potentiometer. This part would be soldered on another general purpose board and would be placed on the top of chassis. The reason for placing potentiometer in this part is that it would be easier to adjust sensor threshold. See the pictures below. 

{% include image.html img="images/old/part2 ckt.jpg" title="Part 2 soldered" caption="Part 2 soldered" class="lazyload" %}

Now all the chassis and circuit part is done lets combine them all!.

## Combining all

Fix the sensor part just in front caster,facing downwards. ensure that there is very less clearance between sensor covering and ground. See the picture below.

{% include image.html img="images/old/sensor placment.jpg" title="Sensor Placement" caption="Sensor Placement" class="lazyload" %}

Now connect the battery to the circuit and also plugin the motors in there respective connectors. For more information regarding battery and there charging circuit see <cite class="caption" title="Coming Soon" dir="ltr">this tutorial</cite>. I am using two 3.7V Li-ions cells in series for this robot.

Small cheap 9 V batteries will not be able to drive this robot for more that 4-5 minutes.

{% include image.html img="images/old/battery.jpg" title="Li-ion battery" caption="Li-ion battery" class="lazyload" %}

{% include image.html img="images/old/complete bot.jpg" title="Complete Robot" caption="Complete Robot" class="lazyload" %}

Adjust the threshold of LDR such that when sensor is on black surface voltage at base of transistor must be less than 0.5Volts. If motors are rotating is reverse direction just change the polarity of that motor. After all this you would be able to make a robot that moves like the one below!.

<iframe src="http://www.youtube.com/embed/o5qvvWnSbkE" frameborder="0" width="560" height="315"></iframe>

Hope you liked the above tutorial. Subscribe to PlaywithRobots on facebook for more updates.