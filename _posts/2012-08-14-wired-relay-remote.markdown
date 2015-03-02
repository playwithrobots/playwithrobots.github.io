---
layout: post
title: "Wired relay remote"
category: "remote-control-circuits"
comments : true
redirect_from: "/robotics-pool/remote-control-circuits/wired-relay-remote/"
---
This tutorial focuses on making a wired remote control circuit for a differential drive robot.  This remote can control DC motors with maximum load current of 7A DC. However the current rating can be increased by changing the relays with higher rating.

You can see the remote in action in the video below: 

<iframe src="http://www.youtube.com/embed/Sgiectb69fw" frameborder="0" width="640" height="360"></iframe>

### Components required:

* **Relays:**

{% include image.html img="images/old/relay.jpg" title="Relays" caption="Relays" class="lazyload" %}

To know about how to use relays, go through this [short tutorial](/dc-motor-driver-circuits#relay "controlling motor using relays") on controlling relays. 

* **Push buttons:**

{% include image.html img="images/old/Buttons.jpg" title="Push buttons" caption="Push buttons" class="lazyload" %}

They have four terminals, two pair of terminals are shorted and when button is pressed all four terminals become shorted. 

* **General purpose board (GPB):**

{% include image.html img="images/old/relay_PCB.jpg" title="General purpose board" caption="General purpose board" class="lazyload" %}

On this board we will solder the remote circuit. 

* Eight Diodes, one 9V battery and its battery cap and one 4-pin and 2-pin connector each. 

### Circuit diagram : 

{% include image.html img="images/old/relay-remote.png" title="Circuit diagram [TOP VIEW]" caption="Circuit diagram [TOP VIEW]" class="lazyload" %}

### Working of circuit: 

The logic of above circuit is that when no button is pressed all the four relays are inactive therefore potential difference across motor is zero volts. As soon as any one button is pressed it triggers two relays and depending on the relay triggered the motors will rotate in CW or ACW direction. For example Button B2 activates coil C1 and C4 of relays. which make potential difference -12V across M1 and 12V across M2 and thus making an in-place rotation. 

Now let us solder the circuit. It would be better to solder a male 4-pin connector on GPB and connect motors to GPB via this 4-pin connector. This will make the circuit easier to attach/detach from the robot. Similarly a 2-pin connector for connecting 12V battery.

See the picture of the complete circuit soldered: 

{% include image.html img="images/old/relay_remote.jpg" title="Complete soldered circuit" caption="Complete soldered circuit" class="lazyload" %}

To connect this circuit with the bot use ribbon wires. The choice of wire depends on your motor current requirement.  

{% include image.html img="images/old/ribbon_wire.jpg" title="Ribbon wire" caption="Ribbon wire" class="lazyload" %}

Connect 4-pin female and 2-pin female connector with one end of ribbon wire. See the picture below. 

{% include image.html img="images/old/ribbon_wire_end.jpg" title="End Connection of ribbon wire" caption="End Connection of ribbon wire" class="lazyload" %}

Now connect the robot with other end of ribbon wire. If the motors are not moving in desired direction try changing the polarity of motor. To make the robot seen in video below go to [manual controlled robot](/manually-controlled-robot "manual controlled robot") tutorial. 

Watch the robot is action!.  

<iframe src="http://www.youtube.com/embed/Sgiectb69fw" frameborder="0" width="640" height="360"></iframe> 

Hope you liked the above tutorial. Subscribe to PlaywithRobots on facebook for more updates.