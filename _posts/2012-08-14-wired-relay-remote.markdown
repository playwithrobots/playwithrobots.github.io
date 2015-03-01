---
layout: post
title: "Wired relay remote"
category: "make-it-from-scratch"
redirect_from: "/2012/04/02/minimal-urls-jekyll/"
---
##[ Wired relay remote](/robotics-pool/remote-control-circuits/wired-relay-remote)

	
This tutorial focuses on making a wired remote control circuit for a differential drive robot.  This remote can control DC motors with maximum load current of 7A DC. However the current rating can be increased by changing the relays with higher rating.

You can see the remote in action in the video below: 

 <iframe src="http://www.youtube.com/embed/Sgiectb69fw" frameborder="0" width="640" height="360"></iframe>

### Components required:

1. **Relays: **<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Relays](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_relay.jpg "Relays")](/images/relay.jpg "Relays")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Relays</td></tr></table>

To know about how to use relays, go through this [short tutorial](/robotics-pool/motor-driver-circuits/dc#relay "controlling motor using relays") on controlling relays. 

2. **Push buttons: **<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Push buttons](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_Buttons.jpg "Push buttons")](/images/Buttons.jpg "Push buttons")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Push buttons</td></tr></table>

They have four terminals, two pair of terminals are shorted and when button is pressed all four terminals become shorted. 

3. **General purpose board (GPB): **

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![General purpose board](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_relay_PCB.jpg "General purpose board")](/images/relay_PCB.jpg "General purpose board")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >General purpose board</td></tr></table>

On this board we will solder the remote circuit. 

4. Eight Diodes, one 9V battery and its battery cap and one 4-pin and 2-pin connector each. 

### Circuit diagram : 

<table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Relay remote circuit diagram [TOP VIEW] ](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_relay-remote.png "Circuit diagram [TOP VIEW]")](/images/relay-remote.png "Circuit diagram [TOP VIEW]")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Circuit diagram [TOP VIEW]</td></tr></table>

### Working of circuit: 

The logic of above circuit is that when no button is pressed all the four relays are inactive therefore potential difference across motor is zero volts. As soon as any one button is pressed it triggers two relays and depending on the relay triggered the motors will rotate in CW or ACW direction. For example Button B2 activates coil C1 and C4 of relays. which make potential difference -12V across M1 and 12V across M2 and thus making an in-place rotation. 

Now let us solder the circuit. It would be better to solder a male 4-pin connector on GPB and connect motors to GPB via this 4-pin connector. This will make the circuit easier to attach/detach from the robot. S<span>imilarly a 2-pin connector for connecting 12V battery. </span>

<span>See the picture of the complete circuit soldered: <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Complete soldered circuit](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_relay_remote.jpg "Complete soldered circuit")](/images/relay_remote.jpg "Complete soldered circuit")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Complete soldered circuit</td></tr></table></span>

To connect this circuit with the bot use ribbon wires. The choice of wire depends on your motor current requirement.  

 <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![Ribbon wire](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_ribbon_wire.jpg "Ribbon wire")](/images/ribbon_wire.jpg "Ribbon wire")</td></tr><tr><td class="mtCapStyle"  style=" width:200px; height:0px;" >Ribbon wire</td></tr></table>

 Connect 4-pin female and 2-pin female connector with one end of ribbon wire. See the picture below. <table class="caption multithumb"  cellspacing="0" cellpadding="0" style="border: ;"    ><tr><td >[![End Connection of ribbon wire](http://playwithrobots.com/cache/multithumb_thumbs/b_200_200_16777215_00_images_ribbon_wire_end.jpg "End Connection of ribbon wire")](/images/ribbon_wire_end.jpg "End Connection of ribbon wire")</td></tr><tr><td class="mtCapStyle"  style=" width:161px; height:0px;" >End Connection of ribbon wire</td></tr></table> 

Now connect the robot with other end of ribbon wire. If the motors are not moving in desired direction try changing the polarity of motor. To make the robot seen in video below go to [manual controlled robot](/make-it-form-scratch/manually-controlled-robot "manual controlled robot") tutorial. 

Watch the robot is action!.  

<iframe src="http://www.youtube.com/embed/Sgiectb69fw" frameborder="0" width="640" height="360"></iframe> 

 Hope you liked the above tutorial. Subscribe to PlaywithRobots on facebook for more updates.

<div style="clear:both"></div>

 ** We have changed our commenting engine for better notification and privacy, previous comments for this article are available   [here.](http://graph.facebook.com/comments/?ids=http://playwithrobots.com/robotics-pool/remote-control-circuits/wired-relay-remote)  **

