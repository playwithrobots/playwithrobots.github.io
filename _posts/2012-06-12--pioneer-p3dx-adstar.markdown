---
layout: post
title: "Pioneer P3-DX and ADstar planner"
category: "make-it-from-scratch"
redirect_from: "/2012/04/02/minimal-urls-jekyll/"
---
##[ Pioneer P3-DX and ADstar planner](/working-on-robots/pioneer/13-pioneer-p3dx-adstar)

Today we all will be playing with Pioneer P3-DX robot. We'll learn how to program the robot to navigate in a grid world approach using the ADstar planning algorithm provided in the ROS[ SBPL](http://www.ros.org/wiki/sbpl "SBPL package in ROS") package.

Before Starting the tutorial, you should know the basics of [ROS](http://www.ros.org).

This project was made at [RISE LAB](http://rise.cse.iitm.ac.in/wiki/index.php/RISE_Robotics_Group "RISE Robotics group"), [IITM](http://www.iitm.ac.in/ "IIT Madras").

**Package Link : -** [P3DX_SBPL](https://github.com/AbhishekMehta/P3DX_sbpl "github repo")

**Dependency : -** [ROSARIA](http://www.ros.org/wiki/ROSARIA "ROSARIA package on ros.org"), [roscpp](http://www.ros.org/wiki/roscpp "roscpp ")

### Overview

The Robot uses ADstar planner for navigation through the environment. The environment is a grid with each cell a square of 40cm by 40cm (can be changed). Initial environment is empty i.e. without obstacles as the P3DX moves toward its goal it keeps on updating its environment with the help of on-board eight front sonar sensors. The figure below will describe overall working. <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Package overview](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_ADstar_Planner_.png "Package overview")](/images/ADstar_Planner .png "Package overview")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Package overview</td></tr></table>

### Nodes

1. **ADstar : -** This is planner node

1.1** Subscribed topics :**

<span style="font-family: 'courier new', courier;">sonar</span> ([P3DX_sbpl/sonar_msg](#sonar_msg))  

Sonar information is passed on this topic.

<span style="font-family: 'courier new', courier;">sbpl_wait</span> ( [P3DX_sbpl/sbpl_msg](#sbpl_msg))    

Subscribe to an acknowledgement signal for each step from P3DX driver node.

<span style="font-family: 'courier new', courier;">start_sbpl</span> ([P3DX_sbpl/start_msg](#start_msg))  

Width,height,start coordinates, end coordinates and obstacle threshold  are published on this topic; only after receiving this planner starts.

1.2 **Published topics :**

<span style="font-family: 'courier new', courier;">sbpl_xy</span> ([P3DX_sbpl/sbpl_msg](#sbpl_msg))  

Publish robots present coordinated and new coordinates to driver node.

2 **P3DX_motion : -** This is driver node for P3DX robot.

2.1 **Subscribed topics : **

<span style="font-family: 'courier new', courier;">sbpl_xy</span> ([P3DX_sbpl/sbpl_msg](#sbpl_msg))  

Receives robots present coordinated and new coordinates from planner node.

2.2 **Published topics : **

<span style="font-family: 'courier new', courier;">sonar</span> ([P3DX_sbpl/sonar_msg](#sonar_msg))  

Sonar information is passed on this topic.

<span style="font-family: 'courier new', courier;">sbpl_wait</span> ([ P3DX_sbpl/sbpl_msg](#sbpl_msg))  

Publish an acknowledgement signal after each step to P3DX planner node.

### 3 Message Types :

3.1 **<a name="sbpl_msg"></a>sbpl_msg :**

3.2  **<a name="sonar_msg"></a>sonar_msg :**

<span style="font-family: 'courier new', courier;">3.3  **<a name="start_msg"></a>start_msg :**</span>

4 **Launch File :** P3DX_sbpl.launch 

### 5. Usage : 

<pre class="brush:bash">roscore

roslaunch P3DX_sbpl P3DX_sbpl.launch

rostopic pub -1 /start_sbpl P3DX_sbpl/start_msg - - 5 5 0 0 4 4 1</pre>

**NOTE :** The only concern should be about start_sbpl topic and start_msg type. Rest all topics,message types are used by the two nodes internally. **Planner will not start until it receives message on start_sbpl topic. **Initial direction of robot is East unless you have changed it in P3DX_motion.cpp. 

### **
**6. Direction Map

The direction nomenclature i used is shown below. 

 <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Direction map](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_P3DX_sbpl.jpg "Direction map")](/images/P3DX_sbpl.jpg "Direction map")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Direction map</td></tr></table>

See the working of this planner in the video below : 

<iframe src="http://www.youtube.com/embed/sW-yAaGKBJ0" frameborder="0" width="480" height="360"></iframe>

The goal coordinate of the robot is somewhere nearer to the blue basket. 

Have a doubt ? Don't hesitate, ask a Question. 

<div style="clear:both"></div>

 ** We have changed our commenting engine for better notification and privacy, previous comments for this article are available   [here.](http://graph.facebook.com/comments/?ids=http://playwithrobots.com/working-on-robots/pioneer/13-pioneer-p3dx-adstar)  **

