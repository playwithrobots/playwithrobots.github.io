---
layout: post
title: "Basic hardware and software required for AVR"
category: "AVR-Tutorials"
comments : true
redirect_from: "/robotics-pool/avr/getting-started/"
---
For proper working of an AVR, we requires the following four things to start:

* An [IDE](http://en.wikipedia.org/wiki/Integrated_development_environment "Integrated Development Environment "), in which we can write a program in C language/assembly language; which compiles it and generates a .hex file (machine language file) as Microcontrollers only understand .hex file.
* A Programmer hardware that act as a link between computer and Microcontroller.
* A programming software interface that uses programmer hardware and sends necessary .hex file to be placed in Microcontroller through that programmer.
* An ATmega32 microcontroller and its [basic circuit](/images/old/basic_circuit.jpg).

##IDE

Among the many softwares available, the two most popular are:

* [Code Vision AVR](http://www.hpinfotech.ro/html/cvavr_features.htm "COde Vision AVR") evaluation version.
* [AVR studio 4](http://www.atmel.in/tools/STUDIOARCHIVE.aspx "AVR studio") + [WinAVR](http://winavr.sourceforge.net/ "Winavr") (WinAVR is compiler and AVR studio is text editor and debugger. Together they make an IDE.)

##Programmer

A programmer depends upon the communication port (Serial, parallel or USB port) of a computer. As new computers rarely have serial or parallel port, I will be here using a USB programmer.

**[USBasp](http://www.fischl.de/usbasp/ "USBasp"):** It is a USB in-circuit programmer for Atmel AVR controllers.

**Programming software:**

* [AVRDUDE](http://download.savannah.gnu.org/releases/avrdude/) Linux or windows.
* [Khazama AVR Programmer](http://khazama.com/project/programmer/) is a Windows XP/Vista GUI application for USBasp and avrdude.
* [eXtreme Burner](http://extremeelectronics.co.in/avr-tutorials/gui-software-for-usbasp-based-usb-avr-programmers/) - AVR is a Windows GUI Software for USBasp based USB AVR programmers.

Combination of Avr studio 4 , WinAVR and eXtreme burner will be good for windows user.

Basic setting of how to make a new project in AVR studio 4 is shown in the video below: (watch it at full screen high resolution!)
<div class="embed-responsive embed-responsive-16by9">
  <iframe class="embed-responsive-item" src="http://www.youtube.com/embed/wXbSVQhS8G8"></iframe>
</div>
For Linux user a simple text editor, avr-gcc compier and avr-dude. You can use this [makefile](/files/Makefile) for building your AVR code.

Now we can move ahead and understand the[ basic input output concepts of AVR microcontrollers](/avr-basic-io).

<span>Hope this was helpful to you! Any questions ? Comment here!</span>