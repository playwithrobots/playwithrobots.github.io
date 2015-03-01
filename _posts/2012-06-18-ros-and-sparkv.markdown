---
layout: post
title: "ROS and SparkV"
category: "make-it-from-scratch"
redirect_from: "/2012/04/02/minimal-urls-jekyll/"
---
##[ ROS and SparkV](/working-on-robots/sparkv/15-ros-and-sparkv)

[ROS (Robot Operating System)](http://ros.org/) provides libraries and tools to help software developers create robot applications. ROS is released under the terms of the [BSD license](http://en.wikipedia.org/wiki/BSD_license "BSD license"), and is [open source software](http://en.wikipedia.org/wiki/Open_source_software "Open source software"). It is free for commercial and research use. Most of my future tutorials will be based on ROS.

A small custom robot integrated with ROS can help you make various project easily and effectively.

Today's tutorial will be on making ROS node for SparkV robot. The prerequisite for this tutorial is basic understanding of [ROS](http://www.ros.org "ROS ") and [SparkV](http://www.nex-robotics.com/products/spark-v-robot/spark-v.html "SparkV robot") robot. 

### Package summary : 

ROS_SparkV is basic ROS package that integrates SparkV robot and ROS. It is build using [rosserial](http://www.ros.org/wiki/rosserial "rosserial stack") Stack. It lets you to send velocity commands to SparkV and read states of various sensors and position encoders. 

### Installation : 

Download the beta testing version of hex file for [ATmega32](/makefile/avr_chatter.hex.zip "HEX file for ATmega32"). Upload it and use it, it's as simple as this. Also you need to have [sparkV_msg](https://github.com/AbhishekMehta/sparkV_msg) package in your ros workspace and make this package using rosmake. 

Due less SRAM (1kb)  in ATmega16, the first version of code does not work reliably with ATmega16. 

Source code will be released soon.  

### Published topics: 

<span style="font-family: 'courier new', courier;">sparkV</span> ([sparkV_msg/sparkV](#sparkV_msg)) 

SparkV sensors values, battery voltage, buzzer state, encoders reading are published on this topic. Default publishing frequency is 10Hz.

### Subscribed topics : 

<span style="font-family: 'courier new', courier;">motor</span> ([sparkV_msg/velocity](#velocity))

receives velocity commands.

<span style="font-family: 'courier new', courier;">buzzer</span> ([std_msgs/bool](http://www.ros.org/doc/api/std_msgs/html/msg/Bool.html))

receives buzzer on/off signal. 

### Message types :

1. <a name="sparkV_msg"></a>**sparkV_msg/sparkV: **

**<span style="font-family: 'courier new', courier;">Message description:</span>**

**<span style="font-family: 'courier new', courier;"> </span>**

 2. <a name="velocity"></a>**sparkV_msg/velocity: **

**<span style="font-family: 'courier new', courier;">Message description: </span>**

### Usage : 

In a terminal window, launch roscore

<pre class="brush:bash">roscore</pre>

<span style="text-align: justify; line-height: 1.3em;">Start the rosserial client </span><span style="text-align: justify; line-height: 1.3em;"> (replace /dev/ttyUSB0 with the serial port your SparkV is connected to (serial port can be checked by command : dmesg | grep tty): </span>

<pre class="brush:bash">rosrun rosserial_python serial_node.py /dev/ttyUSB0</pre>

<span style="line-height: 1.3em; text-align: justify;">Now see the sensor state using </span>

<pre class="brush:bash">rostopic echo /sparkV</pre>

<span style="line-height: 1.3em; text-align: justify;">Testing steps: </span>

1. To turn on buzzer 

<pre class="brush:bash">rostopic echo /sparkV</pre>

 <span style="line-height: 1.3em; text-align: justify;">2. To rotate both motors forward with full speed </span>

<pre class="brush:bash">rostopic pub -1 /motor sparkV_msg/velocity -- true true true true true true true true true </pre>

 <span style="line-height: 1.3em; text-align: justify;">3. To rotate both motors backward with full speed </span>

<pre class="brush:bash">rostopic pub -1 /motor sparkV_msg/velocity -- true true true true true true true true true</pre>

4. To rotate both motors forward at half speed 

<pre class="brush:bash">rostopic pub -1 /motor sparkV_msg/velocity -- true true true true false false true false false</pre>

**NOTE: **If you are using Xbee, it must be configured for 57600 baud rate.  

Using the above node we [controlled SparkV using android phone's accelerometer!](/working-on-robots/sparkv/16-controlling-sparkv-using-android-phone-s-accelerometer). 

Comments and feedback are welcomed :)  

<div style="clear:both"></div>

 ** We have changed our commenting engine for better notification and privacy, previous comments for this article are available   [here.](http://graph.facebook.com/comments/?ids=http://playwithrobots.com/working-on-robots/sparkv/15-ros-and-sparkv)  **

