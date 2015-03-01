---
layout: post
title: "Controlling SparkV using Android phone's accelerometer"
category: "make-it-from-scratch"
redirect_from: "/2012/04/02/minimal-urls-jekyll/"
---
##[ Controlling SparkV using Android phone's accelerometer](/working-on-robots/sparkv/16-controlling-sparkv-using-android-phone-s-accelerometer)


After integrating [ROS and SparkV](/working-on-robots/sparkv/15-ros-and-sparkv "ROS and SparkV") robot, its very easy to control the SparkV robot using Android phone's accelerometer. The prerequisite for this tutorial is basic understanding of [ROS](http://www.ros.org/ "ROS ") and my previous tutorial of integrating [ROS and SparkV.](/working-on-robots/sparkv/15-ros-and-sparkv "ROS and SparkV ") [
](http://www.nex-robotics.com/products/spark-v-robot/spark-v.html "SparkV robot")

### Package summary : 

[sparkV_android](https://github.com/AbhishekMehta/sparkV_android "sparkV_android Github") is a basic ROS package that subscribes to [imu](http://en.wikipedia.org/wiki/Inertial_measurement_unit "Inertial measurement unit") messages published by phone and according to the phone's orientation publishes motion command to sparkV robot. 

### Installation:

First install the ROS android sensor driver app from [android market](https://play.google.com/store/apps/details?id=org.ros.android.sensors_driver "ROS android sensor driver app"). 

After that you have to connect your phone and computer to same network. For this you can check this [tutorial](http://www.ros.org/wiki/android_sensors_driver/Tutorials/Connecting%20to%20a%20ROS%20Master "ROS android sensor driver app tutorial"). OR simply you can start a portable WiFi hotspot from your android device and connect your laptop to that network. After that open a new terminal and write 

<pre class="brush:bash">ifconfig</pre>

<span style="line-height: 1.3em;">You will see your IP address in wlan tab as </span><span style="font-family: 'courier new', courier;">inet addr:YOUR-IP</span>

Now enter this IP address as <span style="font-family: 'courier new', courier;">http://YOUR-IP:11311/ <span style="font-family: arial, helvetica, sans-serif;">in the app and start the app. </span></span>

 <span style="font-family: arial, helvetica, sans-serif;">To verify the topics, try</span>

<pre class="brush:bash">roscore

rostopic list </pre>

Somewhere in the list of topics you will see <span style="font-family: 'courier new', courier;">/android/fix</span> and <span style="font-family: 'courier new', courier;">/android/imu</span>.

You can analyze how the accelerometer data chances with change in your phone orientation by 

<pre class="brush:bash">rostopic echo /android/imu<span style="color: #333333; font-family: Tahoma, Helvetica, Arial, sans-serif; font-size: 12px; line-height: 1.3em;"> </span></pre>

After this download the [sparkV_android](https://github.com/AbhishekMehta/sparkV_android "SparkV_android github") and [sparkV_msg](https://github.com/AbhishekMehta/sparkV_msg "sparkV_msg Github") package and make them. 

**Published topics:**

<span style="font-family: 'courier new', courier;">motor</span> ([sparkV_msg/velocity](/working-on-robots/sparkv/15-ros-and-sparkv#velocity)):

Sends velocity commands to SparkV robot.

**Subscribed topics:**

android/imu ([sensor_msgs/Imu](http://www.ros.org/doc/api/sensor_msgs/html/msg/Imu.html))

<span>accelerometer data is published on this topic. </span>

### Usage: 

After connecting the android device and sparkV robot run

<pre class="brush:bash">roscore

rosrun rosserial_python serial_node.py /dev/ttyUSB0

rosrun sparkV_android android</pre>

<span>NOTE: You might have to edit android.cpp depending on your accelerometer data from phone. <span>
</span></span>

<span>See the video below how it works!. </span>

<iframe src="http://www.youtube.com/embed/bx-z-fK4GdU" frameborder="0" width="640" height="360"></iframe>

<div style="clear:both"></div>

 ** We have changed our commenting engine for better notification and privacy, previous comments for this article are available   [here.](http://graph.facebook.com/comments/?ids=http://playwithrobots.com/working-on-robots/sparkv/16-controlling-sparkv-using-android-phone-s-accelerometer)  **
