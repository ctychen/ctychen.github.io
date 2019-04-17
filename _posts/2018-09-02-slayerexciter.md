---
layout: post
title:  "Slayer Exciter AKA 'The Noob's Tesla Coil'"
date:   2018-09-02
excerpt: "Quick n' easy tutorial"
project: false
tag:
- electronics
- hv
- teslacoil
- tutorial
- theory
comments: false
---

Here is an easy tutorial for some electronics fun...

Finished product first:

![Build with custom PCB, burning some paper with the arc](https://lh3.googleusercontent.com/-oJiepHrblbA/XCxTVtqW0kI/AAAAAAABjg0/ldysHCIkjtc9N-nJ0-iXeqX8hDMuA_4aQCK8BGAs/s512/2019-01-01.png)

Materials:
1x ~50k Ohm Resistor

1x NPN transistor

Magnet Wire

Normal Wire

LED

Power source (9v battery used here)

CFL/CCFL/Neon bulb

Caution: This device creates an electromagnetic field which may affect devices like pacemakers. We are not responsible for anything, so use common sense! Please don’t try this if you’re clueless as to what you’re doing.

CIRCUIT DIAGRAM:

![Slayer Exciter Diagram](https://lh3.googleusercontent.com/-IqGgdvGPf-4/XCxTar0BKKI/AAAAAAABjg4/P4Tzgu6zdq0n-imgqjIkHA6hvQq82ZmhgCK8BGAs/s512/2019-01-01.png)

STEPS:

Step 1: Wrap magnet wire around a PVC pipe (250-500 turns).

Step 2: Wrap the normal wire 3 times around the pipe. This is the primary.

Step3: Connect the components as shown in the circuit diagram on the following page. IMPORTANT: YOU MUST WIRE THE LED WITH THE ANODE (Positive/long side) CONNECTED TO GROUND. FAILURE TO DO SO MAY FRY YOUR LED (and/or your face) !!! 

Step 4: Connect your battery and put the CFL/CCFL/Neon bulb next to the end of the secondary which is sticking out of the top of your PVC pipe. It should light up. If it doesn’t, swap the connections of your primary coil and it should work. Your LED should also light up. Warning: CFLs and CCFLs contain mercury. Don’t break it!



THEORY OF OPERATION:

A transistor acts as a switch. When current is applied to the base of a transistor, the switch opens, allowing current to flow from the collector to the emitter. When the 9V battery is inserted, the base receives some current from the battery. This allows current to flow through the primary, which creates a magnetic field. The current can either go to the base of the transistor through the resistor, or it can go through the coil and back (~0 resistance). Because electricity takes the path of least resistance, the transistor then switches off. However, now the only path is through the 22k resistor, which opens the transistor, and the cycle continues. When the coil turns off, the magnetic field collapses and creates a large voltage on the secondary. The oscillations are then fed back into the transistor and this tunes the transistor.
