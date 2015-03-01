---
layout: post
title: "AVR fuse bits"
category: "make-it-from-scratch"
redirect_from: "/2012/04/02/minimal-urls-jekyll/"
---
##[ AVR fuse bits ](/robotics-pool/avr/fuse)

For Beginners Fuse bits seems to be very confusing but they are not so!

Just like to make some pins of microcontroller as output we have to set some bits in a DDR register, in order to microcontroller to work properly we have to set some fuse bits.In other words fuse bits are master registers whose values directly affects functioning of microcontroller.

ATmega32 microcontroller has two fuse bytes namely high fuse and low fuse. Both of them are 8 bits.

The default value of ATmega32 fuse bit is **0x99E1** i.e. **high fuse =0x99** and **low fuse =0xE1**.

Firstly we will understand what this is and then how to change it!

**NOTE: -** In fuse bits 0 means programmed and 1 means not programmed.

<table style="height: 75px; ; width: 700px;" border="0" cellpadding="10">
<tbody>
<tr style="background-color: #00ccff;">
<td>Bit No.</td>
<td>7</td>
<td>6</td>
<td>5</td>
<td>4</td>
<td>3</td>
<td>2</td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td style="background-color: #00ccff;">High Fuse</td>
<td>OCDEN</td>
<td>JTAGEN</td>
<td>SPIEN</td>
<td>CKOPT</td>
<td>EESAVE</td>
<td>BOOTSZ1</td>
<td>BOOTSZ0</td>
<td>BOOTRST</td>
</tr>
<tr style="background-color: #ffffcc;">
<td style="background-color: #00ccff;">Default Value</td>
<td>1</td>
<td>0</td>
<td>0</td>
<td>1</td>
<td>1</td>
<td>0</td>
<td>0</td>
<td>1</td>
</tr>
</tbody>
</table>

<table style="height: 75px; ; width: 700px;" border="0" cellpadding="10">
<tbody>
<tr style="background-color: #00ccff;">
<td>Bit No.</td>
<td>7</td>
<td>6</td>
<td>5</td>
<td>4</td>
<td>3</td>
<td>2</td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td style="background-color: #00ccff;">Low Fuse</td>
<td>BODLEVEL</td>
<td>BODEN</td>
<td>SUT1</td>
<td>SUT0</td>
<td>CKSEL3</td>
<td><span>CKSEL2</span></td>
<td><span>CKSEL1</span></td>
<td><span>CKSEL0</span></td>
</tr>
<tr style="background-color: #ffffcc;">
<td style="background-color: #00ccff;">Default Value</td>
<td>1</td>
<td>1</td>
<td>1</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>1</td>
</tr>
</tbody>
</table>

**OCDEN: **

This pin is used to enable or disable on chip debugging. On chip debugging provides a real time emulation of microcontroller when running in target system. By default it is disabled as 1 means not programmed.

**JTAGEN: **

There is a built in JTAG interfaces for debugging. It is enabled in new microcontroller. This is the reason why some newbies say “PORTC of ATmega32 not working!!” Disable it if you are not using JTAG by making JTAGEN bit 1(high).

**SPIEN: ** 

0 value (programmed) means Serial programing of ATmega32 is enabled. Don’t change this unless you have a parallel programmer! Because once disabled ATmega32 can’t be programmed using serial programmer.

**EESAVE: ** 

If programmed (0) it will save EEPROM from erasing during chip erase else EEPROM would also be erased with flash.

**BOOTSZ0 and BOOTSZ1: **

These are used to set the boot loader size.

**CKSEL [3-0]: ** 

These bits are used to select different clock options available. 

<table style="height: 150px; ; width: 300px;" border="0" cellpadding="10">
<tbody>
<tr style="background-color: #00ccff;">
<td>Device clocking options</td>
<td>CKSEL 3..0</td>
</tr>
<tr>
<td>External crystal/ceramic resonator</td>
<td>1111-1010</td>
</tr>
<tr style="background-color: #ffffcc;">
<td>External low frequency crystal</td>
<td>1001</td>
</tr>
<tr>
<td>External RC oscillator</td>
<td>1000-0101</td>
</tr>
<tr style="background-color: #ffffcc;">
<td>Calibrated Internal RC oscillator</td>
<td>0100-0001</td>
</tr>
<tr>
<td>External clock</td>
<td>0000</td>
</tr>
</tbody>
</table>

The default value of CKSEL3..0 is 0001 i.e. internal RC oscillator running at 1 MHz. If you want to add external crystal you need to change these values according to the table above. Some common fuse bits values are given in the end of the article.

**CKOPT: **

The CKOPT Fuse Selects between two different oscillator amplifier modes. When CKOPT is programmed, the oscillator output will oscillate with a full rail-to-rail swing on the output. When not programmed, the oscillator has a smaller output swing. If you are using external crystal oscillator it is better to program CKOPT i.e. CKOPT=0.

**BODEN: **

ATmega32 has an On-chip Brown-out Detection (BOD) circuit for monitoring the VCC level during operation by comparing it to a fixed trigger level. When the BOD is enabled (BODEN programmed), and VCC decreases to a value below the trigger level, the Brown-out Reset is immediately activated. When VCC increases above the trigger level, it starts the microcontroller again.

**BODLEVEL: **

The trigger level for the BOD can be selected by this fuse bit. When programmed (0) the trigger level is 4V and when not programmed (1) the trigger level is 2.7V.

**B****OOTRST: **

If BOOTRST bit is programmed (0), the device will jump on first address boot-loader block.

Some fuse bits values are

<table style="width: 400px; height: 200px;" border="0" cellpadding="10" align="center">
<tbody>
<tr style="background-color: #00ccff;">
<td>Low Fuse</td>
<td>High Fuse</td>
<td>Comments</td>
</tr>
<tr>
<td>0xE1</td>
<td>0x99</td>
<td> Default, Internal 1MHz</td>
</tr>
<tr style="background-color: #ffffcc;">
<td>0xE2</td>
<td>0x99</td>
<td><span>Internal 2MHz, rest all default</span> </td>
</tr>
<tr>
<td>0xE3</td>
<td>0x99</td>
<td><span>Internal 4MHz, rest all default</span> </td>
</tr>
<tr style="background-color: #ffffcc;">
<td>0xE4</td>
<td>0x99</td>
<td><span>Internal 8MHz, rest all default</span> </td>
</tr>
<tr>
<td>0xEE</td>
<td>0xC9</td>
<td>External 12/16MHz, JTAG disabled</td>
</tr>
<tr style="background-color: #ffffcc;">
<td>0xE1</td>
<td>0xD9</td>
<td>Internal 1MHz, JTAG disabled </td>
</tr>
<tr>
<td>0xE2</td>
<td>0xD9</td>
<td><span>Internal 2MHz, JTAG disabled</span> </td>
</tr>
<tr style="background-color: #ffffcc;">
<td>0xE3</td>
<td>0xD9</td>
<td><span>Internal 4MHz, JTAG disabled</span> </td>
</tr>
<tr>
<td>0xE4</td>
<td>0xD9</td>
<td><span>Internal 8MHz, JTAG disabled</span> </td>
</tr>
</tbody>
</table>

**Disclaimer:**

This tutorial is for informational purpose; do fuse bits settings at your own risk.

**Frequently Asked Questions (FAQs):**

1.  **Do I have to change fuse bit if I want to use external crystal oscillator?**

**Ans.** Yes, you have to write appropriate fuse bit value corresponding to your crystal frequency.

1.  **Do I need to write Fuse bits value every time after programming microcontroller?**

**Ans.** No, their value will not change during writing/reading flash/EEPROM memory.

 <span>Hope this was helpful to you! Any questions ? Comment here!</span>

<div style="clear:both"></div>

 ** We have changed our commenting engine for better notification and privacy, previous comments for this article are available   [here.](http://graph.facebook.com/comments/?ids=http://www.playwithrobots.com/robotics-pool/avr/fuse)  **

