---
layout: page
title: Eureka-1 Flight Computer Stack
sitemap: true
permalink: /e1fc.html
---

My biggest project of 2022 has been designing, building, and testing the flight computer stack for Eureka-1, Space Enterprise at Berkeley (SEB)'s liquid bipropellant rocket. Eureka-1, or E-1, is projected to reach an altitude of 30,000 ft, using a pressure-fed system with liquid propane and LOx as propellants. This is UC Berkeley's first-ever liquid bipropellant rocket and will set collegiate records if successful, and we are aiming to launch on November 19, 2022. 


For flight we aimed to have a smaller, more compact set of boards. The idea was one of the boards would be a "general" flight computer that would support a Teensy 4.1 microcontroller, sensors including a barometer, IMU, and GPS module, and handle IO and communication between other external boards such as our capacitive fill sensors, an external black box, and our custom radio. This board would then be usable for both solid and liquid rockets. Then the other board in the stack, the E-1 extension, would be specifically to support our liquid bipropellant system, with channels for controlling solenoids and driving the linear actuators we use for our valves, an ADC for reading pressure transducers (much needed to see how much pressure is in our tanks, what our dome regulators are at, and the pressure at our injectors), and thermocouple amps for reading engine temperature data. 

Aside from the shape and size a significant difference on this set of boards is that hardware overcurrent protection is built into all channels on this board. This is implemented with a current sense amplifier and comparator for detecting overcurrent, and a bistable multivibrator circuit for latching the channel off if the current does exceed some threshold. 

<!-- <img src="/images/posts/seb/e1ext/e1h.png" width="600"/> -->

In retrospect although this set of boards was definitely more complex than it needed to be, which made it a pain to debug and assemble, many valuable lessons were learned...


### Development Pics

<img src="/images/posts/seb/e1av/stack.jpg" alt="E-1 Board" width="600"/>

<img src="/images/posts/seb/e1av/ab2.jpg" alt="E-1 Board" width="600"/>

<img src="/images/posts/seb/e1av/e11.jpg" alt="E-1 Board" width="600"/>

<img src="/images/posts/seb/e1av/ab1.jpg" alt="E-1 Board" width="600"/>

<img src="/images/posts/seb/e1av/av3.jpg" alt="E-1 Board" width="600"/>

<img src="/images/posts/seb/e1av/av4.jpg" alt="E-1 Board" width="600"/>

<img src="/images/posts/seb/e1av/ab1.jpg" alt="E-1 Board" width="600"/>

<img src="/images/posts/seb/e1av/r.jpg" alt="E-1 Board" width="600"/>


### E-1 Extension Development Pics

<img src="/images/posts/seb/e1ext/e1h.png" width="600"/>

<img src="/images/posts/seb/e1ext/38.PNG" width="600"/>

<img src="/images/posts/seb/e1ext/39.PNG" width="600"/>

<img src="/images/posts/seb/e1ext/40.PNG" width="600"/>

<img src="/images/posts/seb/e1ext/41.PNG" width="600"/>

<img src="/images/posts/seb/e1ext/sig.png" width="600"/>

<img src="/images/posts/seb/e1ext/pcb1.png" width="600"/>

<img src="/images/posts/seb/e1ext/pcb3d.png" width="600"/>

<img src="/images/posts/seb/e1ext/b1.jpg" width="600"/>


Assembly... 

<img src="/images/posts/seb/e1ext/b2.png" width="600"/>

<img src="/images/posts/seb/e1ext/b3.png" width="600"/>

<img src="/images/posts/seb/e1ext/pop2.jpg" width="600"/>


With the flight computer:

<img src="/images/posts/seb/e1ext/pop3.jpg" width="600"/>

<img src="/images/posts/seb/e1ext/pop4.jpg" width="600"/>


The Stack (TM) (Unpopulated):

<img src="/images/posts/seb/e1ext/stack1.jpg" width="600"/>


Debugging & Troubleshooting....

<img src="/images/posts/seb/e1ext/troubleshooting1.jpg" width="600"/>
