---
layout: post
title: "Pioneer P3-DX and ADstar planner"
category: "Pioneer-P3DX-Robot"
comments : true
redirect_from: "/working-on-robots/pioneer/13-pioneer-p3dx-adstar/"
---
Today we all will be playing with Pioneer P3-DX robot. We'll learn how to program the robot to navigate in a grid world approach using the ADstar planning algorithm provided in the ROS[ SBPL](http://www.ros.org/wiki/sbpl "SBPL package in ROS") package.

Before Starting the tutorial, you should know the basics of [ROS](http://www.ros.org).

This project was made at [RISE LAB](http://rise.cse.iitm.ac.in/wiki/index.php/RISE_Robotics_Group "RISE Robotics group"), [IITM](http://www.iitm.ac.in/ "IIT Madras").

**Package Link :** [P3DX_SBPL](https://github.com/playwithrobots/P3DX_sbpl "github repo")

**Dependency :** [ROSARIA](http://www.ros.org/wiki/ROSARIA "ROSARIA package on ros.org"), [roscpp](http://www.ros.org/wiki/roscpp "roscpp ")

### Overview

The Robot uses ADstar planner for navigation through the environment. The environment is a grid with each cell a square of 40cm by 40cm (can be changed). Initial environment is empty i.e. without obstacles as the P3DX moves toward its goal it keeps on updating its environment with the help of on-board eight front sonar sensors. The figure below will describe overall working. 

{% include image.html img="images/old/ADstar_Planner.png" title="Package overview" caption="Package overview" class="lazyload" %}

### Nodes

**1. ADstar :** This is planner node

**1.1 Subscribed topics :**

<span style="font-family: 'courier new', courier;">sonar</span> ([P3DX_sbpl/sonar_msg](#sonar_msg))  

<p style="padding-left: 30px; text-align: justify;">Sonar information is passed on this topic.</p>

<span style="font-family: 'courier new', courier;">sbpl_wait</span> ( [P3DX_sbpl/sbpl_msg](#sbpl_msg))    

<p style="padding-left: 30px; text-align: justify;">Subscribe to an acknowledgement signal for each step from P3DX driver node.</p>

<span style="font-family: 'courier new', courier;">start_sbpl</span> ([P3DX_sbpl/start_msg](#start_msg))  

<p style="padding-left: 30px; text-align: justify;">Width,height,start coordinates, end coordinates and obstacle threshold  are published on this topic; only after receiving this planner starts.</p>

**1.2 Published topics :**

<span style="font-family: 'courier new', courier;">sbpl_xy</span> ([P3DX_sbpl/sbpl_msg](#sbpl_msg))  

<p style="padding-left: 30px; text-align: justify;">Publish robots present coordinated and new coordinates to driver node.</p>

**2. P3DX_motion :** This is driver node for P3DX robot.

**2.1 Subscribed topics :**

<span style="font-family: 'courier new', courier;">sbpl_xy</span> ([P3DX_sbpl/sbpl_msg](#sbpl_msg))  

<p style="padding-left: 30px; text-align: justify;">Receives robots present coordinated and new coordinates from planner node.</p>

**2.2 Published topics :**

<span style="font-family: 'courier new', courier;">sonar</span> ([P3DX_sbpl/sonar_msg](#sonar_msg))  

<p style="padding-left: 30px; text-align: justify;">Sonar information is passed on this topic.</p>

<span style="font-family: 'courier new', courier;">sbpl_wait</span> ([ P3DX_sbpl/sbpl_msg](#sbpl_msg))  

<p style="padding-left: 30px; text-align: justify;">Publish an acknowledgement signal after each step to P3DX planner node.</p>

### 3 Message Types :

**3.1 <a name="sbpl_msg"></a>sbpl_msg :**

{% highlight bash %}
bool sbpl_wait_flag
int8 sbpl_present_x
int8 sbpl_present_y
int8 sbpl_new_x
int8 sbpl_new_y
bool start_P3DX_motion
{% endhighlight %}

**3.2  <a name="sonar_msg"></a>sonar_msg :**

{% highlight bash %}
bool l  		# weather obstacle is in left or not
bool fl 		# weather obstacle is in front-left or not
bool f 			# weather obstacle is in front or not
bool fr 		# weather obstacle is in front-right or not
bool r 			# weather obstacle is in right or not
int8 direction 	# direction of the robot
{% endhighlight %}

**3.3  <a name="start_msg"></a>start_msg :**

{% highlight bash %}
int8 width 		# width of grid
int8 height 	# height of grid
int8 startx 	# initial x coordinate of robot
int8 starty 	# initial y coordinate of robot
int8 goalx 		# x coordinate of goal
int8 goaly 		# y coordinate of goal
char obsthresh 	# obstacle threshold  
{% endhighlight %}

**4. Launch File :** P3DX_sbpl.launch 

### 5. Usage : 

{% highlight bash %}
roscore
roslaunch P3DX_sbpl P3DX_sbpl.launch
rostopic pub -1 /start_sbpl P3DX_sbpl/start_msg - - 5 5 0 0 4 4 1
{% endhighlight %}

**NOTE :** The only concern should be about start\_sbpl topic and start\_msg type. Rest all topics,message types are used by the two nodes internally. **Planner will not start until it receives message on start_sbpl topic.** Initial direction of robot is East unless you have changed it in P3DX_motion.cpp. 


**6.** Direction Map

The direction nomenclature i used is shown below. 

{% include image.html img="images/old/P3DX_sbpl.jpg" title="Direction map" caption="Direction map" class="lazyload" %}

See the working of this planner in the video below : 

<div class="embed-responsive embed-responsive-16by9">
  <iframe class="embed-responsive-item" src="http://www.youtube.com/embed/sW-yAaGKBJ0"></iframe>
</div>

The goal coordinate of the robot is somewhere nearer to the blue basket. 

Comments are welcomed :)