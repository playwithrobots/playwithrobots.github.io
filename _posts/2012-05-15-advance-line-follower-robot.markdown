---
layout: post
title: "Advance Line Follower robot"
category: "make-it-from-scratch"
redirect_from: "/2012/04/02/minimal-urls-jekyll/"
---

As the name suggests an Advanced Line Follower Robot is just a [Simple Line Follower Robot](/make-it-form-scratch/simple-line-follower-robot "Simple line follower robot") with a few extra features<span>. It will move on a grid of black lines over white background in search of a white box and when the box is detected will raise an alarm and return to its original coordinate in the grid. </span>

<span><span>After reading this section completely you will be able to make one from simple components and play with it. Moreover we will make it modular so that it can be easily modified in future.</span></span>

The main electronics/mechanical components that will be used in making this line follower robot are ATmega32/16 micro-controller, L293D IC, five sensors made using IR LED, photodiode and LM324 IC, acrylic sheet, General purpose board, Two DC motors and battery. 

 <iframe src="http://www.youtube.com/embed/GqAMgG-gc0c" frameborder="0" width="640" height="360"></iframe>

## <span><span>Chassis</span></span>

The Chassis used for this line follower is same as the one we used in making Simple line follower robot. If you haven't made that, no worry just read the [chassis](/make-it-form-scratch/simple-line-follower-robot#chassis "Chassis") part in the [Simple line follower](/make-it-form-scratch/simple-line-follower-robot) robot article.

## <span>Sensors </span>

For this robot we will be using an IR transmitter and a receiver pair. If you don't know how to pair these two just read about it in [Light sensors](/robotics-pool/sensors/light-sensors#photodiode "Photodiode"). We will be using four such pairs. The main advantage of using them over LDR is that they are more sensitive to IR light in comparison to the visible light therefore will work better under different light conditions.The overall circuit diagram of the sensor part and the logic used for the moving robot on a grid of black lines is shown below. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Sensor Principle](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_snesor-principle.jpg "Sensor Principle")](/images/snesor-principle.jpg "Sensor Principle")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Sensor Principle</td></tr></table>

<span><table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Logic](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_logic-advance-line-follower.jpg "Logic")](/images/logic-advance-line-follower.jpg "Logic")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Logic</td></tr></table></span>

As described in above picture, the 2nd and the 3rd sensors are for line following and the 1st and the 4th sensors are for intersection detection.

*   In the First condition, when the 2nd and the 3rd sensors are on the black surface the robot will move forward.*   In the Second condition, when the 2nd sensor is on the black line but the 3rd sensor is on the white surface, the robot will rotate left.*   In the Third condition, when the 1st and the 4th sensors are on the black line, an intersection is detected.
*   In the Forth condition, when the 3rd sensor is on the black line but the 2nd sensor is on the white surface, the robot will rotate right.

<span>The complete circuit is divided into two parts. First, the IR LED and the photodiode pair is to be soldered on a small general purpose board. And a Comparator is to be soldered on another general purpose board, a little bigger than one used previously (Microcontroller circuit will also be soldered on this board later). Both boards are connected to each other with the help of connectors. Using two separate boards allows us to place the IR pairs below the robot for line sensing and the potentiometers above it, to make the adjustment of the threshold easier. Moreover it makes the circuit modular.</span>

<span><table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Circuit part 1](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_advance-lfr-sensor_part.jpg "Circuit part 1")](/images/advance-lfr-sensor part.jpg "Circuit part 1")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Circuit part 1</td></tr></table></span>

Given below is the picture of the above mentioned circuit in soldered form. The positioning of the IR LED and the Photodiode depends on the thickness of line. We will be using a black line of thickness 3 cm. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Soldered circuit](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_advance_lfr_part1.jpg "Soldered circuit")](/images/advance lfr part1.jpg "Soldered circuit")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Soldered circuit</td></tr></table>

Now insert a small piece of black insulating tape in the gap between IR LED and Photodiode. This will insure that no direct IR rays from the IR LED falls on the Photodiode. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Covering](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_ir_covering.jpg "Covering")](/images/ir_covering.jpg "Covering")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Covering</td></tr></table>

Placement of sensors plays a very important role in line sensing accuracy and the robot's movement. This circuit is fixed in front of the caster wheel below the robot and with the ground clearance of sensors as small as 2-3mm. Sensor circuit must be screwed tightly. See the picture below. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Sensor placement](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_sensor_placement1.jpg "Sensor placement")](/images/sensor_placement1.jpg "Sensor placement")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Sensor placement</td></tr></table>

## <span>Remaining circuit and AVR</span>

<span>The circuit diagram of part 2 is shown below. It may look a bit complex but will simplify as you read this page. </span>

<span><table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Circuit diagram part 2](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_advance_lfr_part2.jpg "Circuit diagram part 2")](/images/advance lfr part2.jpg "Circuit diagram part 2")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Circuit diagram part 2</td></tr></table></span>

 The overall Block diagram of this robot's circuit is shown below

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Block diagram](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_block_diagram_alfr.jpg "Block diagram")](/images/block diagram alfr.jpg "Block diagram")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Block diagram</td></tr></table>

It is always better if you divide big circuits into small modules (Parts). Here, I have divided the circuit into 5 different modules (blocks) named IR LED photodiode pair, Comparator, AVR, L293D and motor .

*   **IR LED photodiode pair: -** They simply gives analog output to the Comparator.*   **Comparator part: -** They takes the input from IR LED photodiode pair, compares it with the threshold set by potentiometer and gives a digital logic output to AVR .*   **AVR: -** They takes input from 4 different comparators, processes it and outputs different control signals to L293D according to the sensors condition.*   **L293D: -** They take input from the AVR and correspondingly give output to the motors. I<span>f you haven't used this IC yet for any project, you can read this quick and easy tutorial of </span>[motor driver circuits using L293D](/robotics-pool/motor-driver-circuits/dc#l293d-l298 "L293d usage tutorial")
*   **Motors: -** They revolve according to the input from L293D.*   **Batteries: - **It is advisable to use Li-ion, or NiCd or NiMh or small lead acid batteries. Small cheap 9V batteries will drain completely within 4-5 minutes. If you are using 9V batteries make sure whenever output voltage of 7805 falls below 5V replace the battery.
<div style="text-align: justify;">Similarly there is a obstacle sensor which gives output to AVR . </div>
<div id="related_article" style="background-color: #eeeeee; text-align: justify;">

**Related articles on PlayWithRobots**

[Simple line follower robot](/make-it-form-scratch/simple-line-follower-robot)  |  [Edge avoider robot ](/make-it-form-scratch/edge-avoider-robot) |  [Sensor circuits](/robotics-pool/sensors/light-sensors)  |  [Motor driver circuts](/robotics-pool/motor-driver-circuits/dc)  |  [AVR basic input output concepts](/robotics-pool/avr/basic-input-output)</div>
<div style="text-align: justify;">The logic used for grid following is dividing each intersection in grid as a coordinate. Allocate a direction nomenclature according to which the robot moves. This will be cleared from the image below. You can download the code for ATmega32 microcontroller that i used [here](/makefile/main.c "code"), but for information on basic concepts of AVR microcontrollers read the tutorials in [AVR](/robotics-pool/avr "AVR tutorials ") category. </div>

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Logic](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_arena_logic.jpg "Logic")](/images/arena logic.jpg "Logic")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Logic</td></tr></table>

Now its time to make obstacle sensor for the bot!. 

## <a name="obstacle"></a>Obstacle sensor 

This sensor will be used to detect obstacles in the robot's path, in our case the white block. The concept is same as that of line following sensors on reflection of light principal. We will be using IR LED and photodiode pair. To know more about them see this tutorial on [light sensors](/robotics-pool/sensors/light-sensors#photodiode "IR sensors"). 

 <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![IR LED Photodiode pair](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_ir_pair.jpg "IR LED Photodiode pair")](/images/ir pair.jpg "IR LED Photodiode pair")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >IR LED Photodiode pair</td></tr></table>

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![CIrcuit](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_obstacle-circuit.jpg "Circuit")](/images/obstacle-circuit.jpg "Circuit")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Circuit</td></tr></table>

The complete circuit is to be soldered on a small general purpose board. The reason for not soldering this on the same board with our part2 circuit is that we want to make this sensor modular. If we want to use the obstacle sensor, just plug-in the 3 pin connector. If you are not on an obstacle detection grid just remove the connectors. In this way this can be used with any other robot. In my case a white block can be detected from a distance of 3cm to 7cm, which can be adjusted with the help of potentiometer. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Obstacle sensor](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_obstacle_sensor.jpg "Obstacle sensor")](/images/obstacle sensor.jpg "Obstacle sensor")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Obstacle sensor</td></tr></table> 

Wow! chassis, sensors, circuit all done, lets combine them all!.

### Combining all

Now every part is ready, but each part is of no use unless we combine them all. 

#### Sensors

Placement of sensors is very important. They are the robots eyes. Line following sensors must be fixed tightly in front of caster with a ground clearance of 2-4mm. If the sensors are loose, the signals may fluctuate during robot's motion. Take time in fixing sensor and adjusting the threshold for sensors as a little time spend here may save lots of troubleshooting later on. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Line sensor placement](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_sensor_placement1.jpg "Line sensor Placement")](/images/sensor_placement1.jpg "Line sensor Placement")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Line sensor Placement</td></tr></table>

Obstacle sensor should be placed in front of the robot as can be seen in the final robot pictures at the end of this article.

#### Complete circuit

Place the remaining circuit on chassis and fix every connector to there respective places. There should be no loose wires hanging around, stick them with tape. 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Complete Bot -1 ](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_alr-1.jpg "Complete Bot -1 ")](/images/alr-1.jpg "Complete Bot -1 ")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Complete Bot -1 </td></tr></table>

#### <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Complete Bot -2](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_alfr-2.jpg "Complete Bot -2")](/images/alfr-2.jpg "Complete Bot -2")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Complete Bot -2</td></tr></table>

#### <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Complete Bot -3](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_alfr-3.jpg "Complete Bot -3")](/images/alfr-3.jpg "Complete Bot -3")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Complete Bot -3</td></tr></table>

#### <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Complete Bot -4](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_alfr-4.jpg "Complete Bot -4")](/images/alfr-4.jpg "Complete Bot -4")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Complete Bot -4</td></tr></table>

#### Arena

Obviously, without a grid the robot can't move. I made a sample arena on chart paper with black tapes though not the best one but still works . Arena must be neat and clean. The smallest marks here or there may fluctuate the sensors.

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Arena](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_arena.jpg "Arena")](/images/arena.jpg "Arena")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Arena</td></tr></table>

After adjusting all the sensors threshold and with some trail and error finally the robot will starts moving :) . See the video below. 

<iframe src="http://www.youtube.com/embed/GqAMgG-gc0c" frameborder="0" width="640" height="360"></iframe>

<span>Hope you liked the above tutorial. Subscribe to PlaywithRobots on facebook for more updates. </span>

<div style="clear:both"></div>

 ** We have changed our commenting engine for better notification and privacy, previous comments for this article are available   [here.](http://graph.facebook.com/comments/?ids=http://playwithrobots.com/make-it-form-scratch/advance-line-follower-robot)  **



