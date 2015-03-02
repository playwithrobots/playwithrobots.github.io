---
layout: post
title: "ROS and SparkV"
category: "spark-V"
redirect_from: "/working-on-robots/sparkv/15-ros-and-sparkv/"
---
[ROS (Robot Operating System)](http://ros.org/) provides libraries and tools to help software developers create robot applications. ROS is released under the terms of the [BSD license](http://en.wikipedia.org/wiki/BSD_license "BSD license"), and is [open source software](http://en.wikipedia.org/wiki/Open_source_software "Open source software"). It is free for commercial and research use. Most of my future tutorials will be based on ROS.

A small custom robot integrated with ROS can help you make various project easily and effectively.

Today's tutorial will be on making ROS node for SparkV robot. The prerequisite for this tutorial is basic understanding of [ROS](http://www.ros.org "ROS ") and [SparkV](http://www.nex-robotics.com/products/spark-v-robot/spark-v.html "SparkV robot") robot. 

### Package summary : 

ROS_SparkV is basic ROS package that integrates SparkV robot and ROS. It is build using [rosserial](http://www.ros.org/wiki/rosserial "rosserial stack") Stack. It lets you to send velocity commands to SparkV and read states of various sensors and position encoders. 

### Installation : 

Download the beta testing version of hex file for [ATmega32](/files/avr_chatter.hex.zip "HEX file for ATmega32"). Upload it and use it, it's as simple as this. Also you need to have [sparkV_msg](https://github.com/playwithrobots/sparkV_msg) package in your ros workspace and make this package using rosmake. 

Due less SRAM (1kb)  in ATmega16, the first version of code does not work reliably with ATmega16. 

Source code will be released soon.  

### Published topics: 

<span style="font-family: 'courier new', courier;">sparkV</span> ([sparkV_msg/sparkV](#sparkV_msg)) 

<p style="padding-left: 30px; text-align: justify;">SparkV sensors values, battery voltage, buzzer state, encoders reading are published on this topic. Default publishing frequency is 10Hz.</p>

### Subscribed topics : 

<span style="font-family: 'courier new', courier;">motor</span> ([sparkV_msg/velocity](#velocity))

<p style="padding-left: 30px; text-align: justify;">receives velocity commands.</p>

<span style="font-family: 'courier new', courier;">buzzer</span> ([std_msgs/bool](http://www.ros.org/doc/api/std_msgs/html/msg/Bool.html))

<p style="padding-left: 30px; text-align: justify;">receives buzzer on/off signal.</p>

### Message types :

**1. <a name="sparkV_msg"></a>sparkV_msg/sparkV:**
{% highlight bash %}
uint8 LlS         
uint8 ClS          
uint8 RlS          
uint8 Lir         
uint8 Cir         
uint8 Rir         
uint8 bat         
bool buz          
uint16 tL         
uint16 tR
{% endhighlight %}

<span style="font-family: 'courier new', courier;">Message description:</span>
{% highlight bash %}
LlS          Left line sensor current reading 
ClS          Center line sensor current reading 
RlS          Right line sensor current reading 
Lir          Left IR sensor current reading 
Cir          Center IR sensor current reading 
Rir          Right IR sensor current reading 
bat          Battery current voltage reading ( in scale of 0 to 255 ) 
buz          Buzzer present state on or off
tL           Left position encoder reading 
tR           Right position encoder reading
{% endhighlight %}

**2. <a name="velocity"></a>sparkV_msg/velocity:**
{% highlight bash %}
bool left          
bool right         
bool start         
bool s2L           
bool s1L
bool s0L
bool s2R           
bool s1R
bool s0R
{% endhighlight %}

<span style="font-family: 'courier new', courier;">Message description: </span>
{% highlight bash %}
left          To rotate left motor, true means in fwd direction false means in backward direction
right         To rotate right motor, true means in fwd direction false means in backward direction
start         To enable motors, true means motor enabled, false means disabled. 
s2L           To control speed of left motor, 8 possible speed combination are available selected using s2L (MSB) , s1L, s0L (LSB) 
s1L
s0L
s2R           To control speed of right motor, 8 possible speed combination are available selected using s2R (MSB) , s1R, s0R (LSB) 
s1R
s0R
{% endhighlight %}
### Usage : 

In a terminal window, launch roscore

{% highlight bash %}
roscore
{% endhighlight %}

<span style="text-align: justify; line-height: 1.3em;">Start the rosserial client </span><span style="text-align: justify; line-height: 1.3em;"> (replace /dev/ttyUSB0 with the serial port your SparkV is connected to (serial port can be checked by command : dmesg | grep tty): </span>

{% highlight bash %}
rosrun rosserial_python serial_node.py /dev/ttyUSB0
{% endhighlight %}

Now see the sensor state using

{% highlight bash %}
rostopic echo /sparkV
{% endhighlight %}

Testing steps:

1. To turn on buzzer

{% highlight bash %}
rostopic echo /sparkV
{% endhighlight %}

2. To rotate both motors forward with full speed 

{% highlight bash %}
rostopic pub -1 /motor sparkV_msg/velocity -- true true true true true true true true true
{% endhighlight %}

3. To rotate both motors backward with full speed

{% highlight bash %}
rostopic pub -1 /motor sparkV_msg/velocity -- true true true true true true true true true
{% endhighlight %}

4. To rotate both motors forward at half speed 

{% highlight bash %}
rostopic pub -1 /motor sparkV_msg/velocity -- true true true true false false true false false
{% endhighlight %}

**NOTE:**If you are using Xbee, it must be configured for 57600 baud rate.  

Using the above node we [controlled SparkV using android phone's accelerometer!](/controlling-sparkv-using-android-phone-accelerometer). 

Comments and feedback are welcomed :)  