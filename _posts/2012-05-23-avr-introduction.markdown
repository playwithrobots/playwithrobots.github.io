---
layout: post
title: "Introduction to AVR microcontrollers"
category: "make-it-from-scratch"
redirect_from: "/2012/04/02/minimal-urls-jekyll/"
---
##[ Introduction to AVR microcontrollers](/robotics-pool/avr/intro)

	
![I AM EVERY WHERE!!](/images/introduction%20to%20avr%20picture1.jpg "I AM EVERY WHERE!!")

We are surrounded by lots of electronic gadgets. Mobile phones, mp3 players, air conditioner, microwave, dishwasher, home theater, pen drives, digital cameras, laser printers, automobiles, refrigerators and many more ….. All of these devices contains microcontroller.

Now a question will arise in your mind that if microcontrollers are so ubiquitous then what is a microcontroller!

## **What is microcontroller?**

A microcontroller can be considered as a very small and simple version of a computer. Like a computer can be divided into number of small parts like CPU, RAM , hard disk, Keyboard, mouse, monitor and an operating software ( Windows or Linux or MAC) running into it.

An AVR microcontroller also contains some of these parts. It contains a CPU, just like on computers have but a very simpler one, not very fast. It contains flash memory (same thing that a pen-drive contains) on which it stores program (Its microcontroller hard-disk!). It contains RAM, just like that of computer. An EEPROM memory to store data even after power is turned off. All these parts are on a single chip!.

## AVR Microcontrollers

There are dozens of types of microcontrollers available according to different architectures and vendors. Here, I am introducing you to AVR family microcontrollers.

AVR family is quite big, the main series of microcontrollers in AVR 8bit family are:

<table style="width: 750px; height: 100px;" border="0" cellpadding="10" align="center">
<tbody>
<tr style="background-color: #00ccff;">
<td style="background-color: #00ccff;">Series Name</td>
<td>Program Memory</td>
<td>No. of Pins</td>
<td>Special Features</td>
</tr>
<tr>
<td style="background-color: #00ccff;">tinyAVR</td>
<td>0.5-8kB program memory</td>
<td>6-32 pin package</td>
<td>Limited peripheral set</td>
</tr>
<tr style="background-color: #ffffcc;">
<td style="background-color: #00ccff;">megaAVR</td>
<td>4-256kB program memory</td>
<td>28-100 pin package</td>
<td>Extended and extensive instruction set</td>
</tr>
<tr>
<td style="background-color: #00ccff;">XMEGA</td>
<td>16-384kB program memory</td>
<td>44-64-100 pin package</td>
<td>Extensive peripheral set with DACs and many more features</td>
</tr>
</tbody>
</table>

We will now focus our study on ATmega32 microcontroller; it comes under mega category of AVR, Its main features are:

*   32Kb flash memory
*   2Kb SRAM
*   1Kb EEPROM
*   10bit ADC
*   Two 8bit timers
*   One 16bit timer
*   USART interface
*   SPI interface
*   I2C interface
*   4 PWM channels

The main terms used in microcontrollers:

**CLOCK: - **Microcontrollers require a clock source to work. It is basically a signal that oscillates between high and low with a fixed time period. An AVR microcontroller executes most of its instructions in one clock cycle.

**CLOCK SOURCE: - **ATmega32 has an inbuilt internal RC oscillator. By changing [fuse bit](/robotics-pool/avr/fuse "Fuse bits settings") values it is possible to configure internal RC oscillator to run at 1/2/4/8 MHz. It also has an option of using an external crystal if you require special clock rate like 7.3728MHz or 12MHz. Their advantage over internal RC oscillator is that their precision is high and clock frequencies don’t drift with temperature. Other options are also available for clock sources. To change a clock source you need to change the appropriate fuse bit.

**FLASH MEMORY: -** ATmega32 has a 32Kb of flash memory. It’s like the hard disk of a microcontroller. Program that is to be executed by microcontroller is stored here. It is also commonly called program memory.

**SRAM: - **Static Random Access Memory, this is the volatile memory of microcontroller i.e., data is lost as soon as power is turned off. ATmega32 is equipped with 2KB of internal SRAM. A small portion of SRAM is set aside for general purpose registers used by CPU and some for the peripheral subsystems of the microcontroller.

**EEPROM: -** It is Electrically Erasable Programmable ROM. It retains its data even after power off. It can be used to store variables whose value we want to retain after power off.

**ISP: - **In System Programmable. The flash memory of AVR microcontrollers is In System self-Programmable. This means that AVR microcontrollers can be programmed using an ISP programmer in its application circuit.

**PORTS: - **Like computers have several ports for communication (serial, parallel or USB) with another devices; microcontrollers also have Ports to interface it with LED’s, LCD’s ,buttons, another ICs/microcontrollers etc. ATmega32 has four ports namely Port A, Port B , Port C and Port D.

**VCC: -** Supply voltage.

**GND: - **Ground

So let’s move ahead with next article [Basic hardware and software requirement for AVR!](/robotics-pool/avr/getting-started). 

<span>Hope this was helpful to you! Any questions ? Comment here!</span>

<div style="clear:both"></div>

 ** We have changed our commenting engine for better notification and privacy, previous comments for this article are available   [here.](http://graph.facebook.com/comments/?ids=http://www.playwithrobots.com/robotics-pool/avr/intro)  **

