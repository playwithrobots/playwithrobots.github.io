---
layout: post
title: "Controlling SparkV using Android phone's accelerometer"
category: "spark-V"
comments : true
redirect_from: "/working-on-robots/sparkv/16-controlling-sparkv-using-android-phone-s-accelerometer/"
---
After integrating [ROS and SparkV](/ros-and-sparkv "ROS and SparkV") robot, its very easy to control the SparkV robot using Android phone's accelerometer. The prerequisite for this tutorial is basic understanding of [ROS](http://www.ros.org/ "ROS ") and my previous tutorial of integrating [ROS and SparkV.](/ros-and-sparkv "ROS and SparkV ") 

### Package summary : 

[sparkV_android](https://github.com/playwithrobots/sparkV_android "sparkV_android Github") is a basic ROS package that subscribes to [imu](http://en.wikipedia.org/wiki/Inertial_measurement_unit "Inertial measurement unit") messages published by phone and according to the phone's orientation publishes motion command to sparkV robot. 

### Installation:

First install the ROS android sensor driver app from [android market](https://play.google.com/store/apps/details?id=org.ros.android.sensors_driver "ROS android sensor driver app"). 

After that you have to connect your phone and computer to same network. For this you can check this [tutorial](http://www.ros.org/wiki/android_sensors_driver/Tutorials/Connecting%20to%20a%20ROS%20Master "ROS android sensor driver app tutorial"). OR simply you can start a portable WiFi hotspot from your android device and connect your laptop to that network. After that open a new terminal and write 

{% highlight bash %}
ifconfig
{% endhighlight %}

You will see your IP address in wlan tab as 
{% highlight bash %}
inet addr:YOUR-IP
{% endhighlight %}

Now enter this IP address as <span style="font-family: 'courier new', courier;">http://YOUR-IP:11311/ <span style="font-family: arial, helvetica, sans-serif;">in the app and start the app. </span></span>

 <span style="font-family: arial, helvetica, sans-serif;">To verify the topics, try</span>
{% highlight bash %}
roscore
rostopic list
{% endhighlight %}

Somewhere in the list of topics you will see <span style="font-family: 'courier new', courier;">/android/fix</span> and <span style="font-family: 'courier new', courier;">/android/imu</span>.

You can analyze how the accelerometer data chances with change in your phone orientation by 

{% highlight bash %}
rostopic echo /android/imu
{% endhighlight %}

After this download the [sparkV_android](https://github.com/playwithrobots/sparkV_android "SparkV_android github") and [sparkV_msg](https://github.com/playwithrobots/sparkV_msg "sparkV_msg Github") package and make them. 

**Published topics:**

<span style="font-family: 'courier new', courier;">motor</span> ([sparkV_msg/velocity](/ros-and-sparkv#velocity)):

<p style="padding-left: 30px; text-align: justify;">Sends velocity commands to SparkV robot.</p>

**Subscribed topics:**

android/imu ([sensor_msgs/Imu](http://www.ros.org/doc/api/sensor_msgs/html/msg/Imu.html))

<p style="padding-left: 30px; text-align: justify;">accelerometer data is published on this topic.</p>

### Usage: 

After connecting the android device and sparkV robot run

{% highlight bash %}
roscore
rosrun rosserial_python serial_node.py /dev/ttyUSB0
rosrun sparkV_android android
{% endhighlight %}
<span>NOTE: You might have to edit android.cpp depending on your accelerometer data from phone. <span>
</span></span>

<span>See the video below how it works!. </span>

<iframe src="http://www.youtube.com/embed/bx-z-fK4GdU" frameborder="0" width="640" height="360"></iframe>