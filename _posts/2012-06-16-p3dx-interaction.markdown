---
layout: post
title: "Human Interaction with Pioneer P3-DX"
category: "pioneer"
redirect_from: "/working-on-robots/pioneer/14-p3dx-interaction/"
---
Developers have always tried to improve their ways of interaction with machines. From simple levers to radio buttons and then from push buttons to touch screens, developers have always tried to devise out simple yet more effective ways for interaction with robots. 

Moving on from the revolutionary soft-touch techniques, interacting via gestures is on the rise. In this article I will show you how to operate the P3-DX robot via pointing gestures. To understand this tutorial you should have basic knowledge and understanding of [ROS](http://www.ros.org "ROS ") and [Pioneer P3-DX and ADstar planner](/pioneer-p3dx-adstar).

This project was made at [RISE LAB](http://rise.cse.iitm.ac.in/wiki/index.php/RISE_Robotics_Group "RISE Robotics group"), [IITM](http://www.iitm.ac.in/ "IIT Madras").

Package Link : [tf_experiment,](https://github.com/playwithrobots/tf_experiments), [P3DX_SBPL](https://github.com/playwithrobots/P3DX_sbpl "github repo")

Dependency : [ROSARIA](http://www.ros.org/wiki/ROSARIA "ROSARIA package on ros.org"), [roscpp](http://www.ros.org/wiki/roscpp "roscpp ")

### Overview

Here I will be using gesture control to point out to the robot about a location and the robot judge and calculate out that coordinate and then will move towards that location.

### Working

To figure out the location of the point Openni\_tracker node is used. By using Kinect depth sensors, transforms of the human skeleton are published by Openni_tracker node. Then from these transforms, coordinates of right shoulder and right hand are found. They are then used to find the coordinates of the point on the ground where the hand is pointing by extending the line joining right shoulder and right hand.

This point is then quantized to the nearest grid coordinate in the P3-DX robot's frame and new goal is published to sbpl\_start topic, making the robot go to that point.

### Nodes

**listener :** listens to the transforms published by openni\_tracker node and sends the goal to P3DX robot using [P3DX_sbpl](/pioneer-p3dx-adstar "Adstar planner") package.

**Published topics :** /start_sbpl ([P3DX_sbpl/start_msg](/pioneer-p3dx-adstar#start_msg))  :  Width, height, start coordinates, end coordinates and obstacle threshold relative to the pointed point are published on this topic.

### Usage:

{% highlight bash %}
roscore
rosrun openni_tracker openni_tracker
rosrun tf_experiment listner
roslaunch P3DX_sbpl P3DX_sbpl.launch
{% endhighlight %}

Then go in front of the Robot and point at a location!!. 

NOTE: You may have to calibrate you body before pointing depending on version of Openni and NITE installed. For details read openni_tracker node [wiki](http://www.ros.org/wiki/openni_tracker "Openni_tracker") page. 

### Video:

<iframe src="http://www.youtube.com/embed/Jis2Leavhok" frameborder="0" width="480" height="360"></iframe>

Now a person can be randomly moving his right hand here and there, in order to avoid random point calculation, whenever a user raises his left hand above the head, right hand is used to calculate the point. 

Comments are welcomed :)