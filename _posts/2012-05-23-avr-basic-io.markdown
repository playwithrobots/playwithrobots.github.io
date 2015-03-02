---
layout: post
title: "Input/Output Concept"
category: "avr"
comments : true
redirect_from: "/robotics-pool/avr/basic-input-output/"
---
Like computers communicates with other devices (printers, pen-drives etc.) through ports (USB, serial etc.), ATmega32 Microcontroller communicates with other IC's through Ports. A Port is a combination of 8 pins, each of them able to send 1 bit data at a time. Together these 8 pins (Port) can send 8 bit of data at a time. ATmega32 Microcontroller has a four Ports namely Port A, Port B, Port C and Port D.

In this tutorial we will write a code, that will make LEDs attached to ATmega32 blink. 

Input Output functions of each port are set by three Registers:

*   **DDRX:** Determines whether a pin is input or output of Port X.
*   **PORTX:** Sets the output value of Port X.
*   **PINX:** Reads the value of Port X.

### DDRX (Data Direction Register):  

This register is used to make any bit in a port as an input or an output.

* To make a pin as an Input, set the corresponding bit value to 0
* To make a pin as an Output, set the corresponding bit value to 1.

If I write **DDRA = 0xFF** (0x for Hexadecimal number system) that is setting all the bits of DDRA to be 1, will make all the pins of Port A as Output. Similarly by writing **DDRD = 0x00** that is setting all the bits of DDRA to be 0, will make all the pins of Port A as Input.

According to [schematic](/images/old/blinking_led.jpg "Circuit diagram") LED’s are attached to PA0, PA1, PA2, and PA3. We have to make these pins as output pins.

<table style="width: 700px; height: 75px;" border="0" cellpadding="10" align="center">
<tbody>
<tr style="background-color: #00ccff;">
<td style="background-color: #00ccff;">Port A</td>
<td>PA7</td>
<td>PA6</td>
<td>PA5</td>
<td>PA4</td>
<td>PA3</td>
<td>PA2</td>
<td>PA1</td>
<td>PA0</td>
</tr>
<tr>
<td style="background-color: #00ccff;">Function</td>
<td>Input</td>
<td><span>Input</span></td>
<td><span>Input</span></td>
<td><span>Input</span></td>
<td>Output</td>
<td><span>Output</span></td>
<td><span>Output</span></td>
<td><span>Output</span></td>
</tr>
<tr style="background-color: #ffffcc;">
<td style="background-color: #00ccff;">DDRA</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>1</td>
<td>1</td>
<td>1</td>
<td>1</td>
</tr>
</tbody>
</table>

For this configuration we have to set DDRA as **00001111** which in hexadecimal is written as 0x0F. So we will write **DDRA=0x0f**.

**Note:** DDRA=0x0f (in hexadecimal), DDRA=0x0b00001111 (in binary), DDRA=15 (in decimal). These all are same in terms of functioning. It is a way of representing different number system.

### PORTX (PORTX Data Register) 

This register sets the value of the corresponding port. We'll discuss both cases, when the pin is set as Input and when the pin is set as an Output.

**1. Output Pin:**

If a pin is set to be output, then by setting bit value 1 we make output **High** that is +5V on that bit and by setting bit value 0 we make output **Low** that is 0V on that bit.

In our [schematic](/images/old/blinking_led.jpg) for this tutorial, to glow LED’s we have to make PA3, PA2, PA1and PA0 bits high.

<table style="width: 700px; height: 75px;" border="0" cellpadding="10" align="center">
<tbody>
<tr style="background-color: #00ccff;">
<td style="background-color: #00ccff;">Port A</td>
<td>PA7</td>
<td>PA6</td>
<td>PA5</td>
<td>PA4</td>
<td>PA3</td>
<td>PA2</td>
<td>PA1</td>
<td>PA0</td>
</tr>
<tr>
<td style="background-color: #00ccff;">Value</td>
<td>Low(0V)</td>
<td><span>Low(0V)</span></td>
<td><span>Low(0V)</span></td>
<td><span>Low(0V)</span></td>
<td>High(5V)</td>
<td><span>High(5V)</span></td>
<td><span>High(5V)</span></td>
<td><span>High(5V)</span></td>
</tr>
<tr style="background-color: #ffffcc;">
<td style="background-color: #00ccff;">PORTA</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>1</td>
<td>1</td>
<td>1</td>
<td>1</td>
</tr>
</tbody>
</table>

For this configuration we have to set **Port A** as **00001111** which in hexadecimal is **0f**. So we will write **PORTA=0x0f;**

**2. Input Pin:**

If a pin is set to be input, then by setting its corresponding bit in PORTX register will make it as follows,

*   Bit value 0 :- Tri-Stated
*   Bit value 1 :- Pull Up

Tri-stated means the input will be high Impedance (no specific value) if no input voltage is applied on that pin. Pull Up means input will go to **+5V** if no input voltage is specified on that pin.

### PINX (DATA READ REGISTER)  

This register is used to read the value of a port. If a pin is set as input then corresponding bit on PIN register is,

* 0 for Low Input.
* 1 for High Input.

For an example consider I have connected a sensor on PC4 and configured it as an input pin through DDR register. Now I want to read the value of PC4 whether it is Low or High. So I will just check 4th bit of PINC register.

We can only read bits of the PINX register; can never write on that as it is meant for reading the value of a port.

I hope you have got the basic idea about the functioning of I/O Ports. For detailed reading you can always refer to datasheet of Atmega32.

**Summary**

**DDRX:** Setting Port/Pins as inputs or outputs.

**PORTX:** To set value on port.

**PINX:** To read values from port.

**Circuit diagram for this tutorial:** [Blinking Led](/images/old/blinking_led.jpg)

**Code for this tutorial that makes LEDs blink is given below :**  

{% highlight cpp %}
/*************************************************************************************

Program for Blinking LEds for AtMega32 microcontroller

Crystal Frequency - No external crystal used 1Mhz internal

Low Fuse Bit 0xE1

High fuse Bit 0x99

Compiler optimization --- o1

LED's conected to port A pins :- PA0, PA1, PA2, PA3

Written by Abhishek

www.PlaywithRobots.com

***************************************************************************************/

#define F_CPU 1000000UL

#include <avr/io.h>;

#include <util/delay.h>;

void main (void)

{

DDRA=0x0F; // making LED's pins as output

PORTA=0x00;// making initial value to be zero

while(1)

{ PORTA|=0x0F; // making LED's glow

_delay_ms(500); // delay of 500ms

PORTA&amp;=0xF0; // making LED's off

_delay_ms(500); // delay of 500ms
}
}  
{% endhighlight %}

See how the above code works in a short video below!. Although the LEDs are blinking at 1s interval, the point of showing this video is that the circuit used in this video is same as used in Advance Line follower robots. This is main advantage of using Microcontrollers, just by changing the codes, same circuits will work differently.

<iframe src="http://www.youtube.com/embed/TAeIcF75KWQ" frameborder="0" width="640" height="360"></iframe>

Hope this was helpful to you! Any questions ? Comment here!