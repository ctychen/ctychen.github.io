---
layout: page
title:  The Launcher (Coilgun II)
sitemap: true
permalink: /launcher.html
---

<p>The next iteration on the coilgun was this device here. Instead of launching projectiles from a barrel, the challenge I made for myself this time was seeing how high I could launch something-I swapped the barrel and coil for a “pancake” coil of solid, thicker wire. I also made some modifications to the circuit so firing could be more controlled: in place of the first spark gap, I added a “control panel” connected by long wires, with a button for firing and another for switching between charging and firing modes. I swapped the second, big spark gap, for an SCR, which did a better job of handling high currents than my sketchy spark gap. I added relays as well to prevent the circuit from firing while the capacitors are charging as another safeguard-there’s two of them; the first controls power flowing to the circuit for charging and normally stays closed, and the second controls firing the SCR and is normally open.</p>

<img src="/images/posts/coilgun/launcher/Washer Launcher, Launching Washers_big.gif"/>

<img src="/images/posts/coilgun/launcher/sideview.png"/>

<p>In retrospect I wonder why I didn’t try adding a “control panel” earlier-with a switch for charging and a button to fire the launcher, it was both a precaution to prevent firing while charging the capacitors and a way for me to test the device in a more controlled way compared to the old coilgun circuit. Plus, with the old coilgun, after firing, if you wanted to discharge the circuit, you’d have to short the spark gap, which wasn’t exactly the safest move, while now you can just press ‘fire’ again to discharge again. For testing, I tried launching everything from small heatsinks to hard-drive platters...and, well, those were incredibly fun. I was able to launch some platters around 14 feet straight up! Unfortunately, it seems that the SCR wasn’t able to survive through all the tests, so I had to replace it with 2 smaller SCRs in parallel.</p>
