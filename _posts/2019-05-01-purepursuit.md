---
layout: post
title:  "Quick Intro to Pure Pursuit"
date:   2019-05-01
excerpt: "Path tracking and motion"
project: false
tag:
- code
- robotics
- frc
comments: false
---

Something our team tried to do this year was to implement vision-based pure pursuit. 
This is compiled as a resource to understand how this useful algorithm works, and how to get it working.

[XiaoXiae's visual implementation of a basic adaptive pure pursuit algorithm in Java with Processing](https://github.com/xiaoxiae/PurePursuitAlgorithm)

[A python implementation of Team 1712's Pure Pursuit Algorithm by arimb](https://github.com/arimb/PurePursuit)

[Pure pursuit motion sim - demonstrating the algorithm using a drivebase model](https://github.com/the-null-terminator/PurePursuitSim)


## So...what is it?

Pure pursuit is a path tracking algorithm. Basically, with pure pursuit, you generate target velocities 
based on where the robot is, relative to the path it wants to follow. One way to think about it:
the robot is "chasing" a moving point ahead of it, "looking ahead" some distance to _pursue_ the point.
The benefit of this method is that paths can adjust; since it moves based on location in relation to a target path,
the robot can correct itself if it is disturbed while moving. 


This is what the algorithm is doing (image from P. Sanjeevikumar):

![what this looks like mathematically](https://www.researchgate.net/profile/P_Sanjeevikumar/publication/319714221/figure/fig6/AS:631663394578442@1527611697713/Illustration-of-Pure-Pursuit-algorithm-principle-Knowing-the-current-robot-location-and.png)


## Implementation details - things to have
- lookaheadDistance is how far along the path we should "pursue"
- maxVel and maxAccel are in inches/s and inches/s^2 respectively.
- maxVelk is proportional to how fast you turn
- Feedback is supported, where kP should be around 0.001. With a higher kP, we can better compensate for being off the targeted velocity, but be aware that too large of a kP will cause oscillations
- Spacing is the distance between points along the path: the path generator will inject points along the coordinates you specify, at the given spacing.
- Tolerance is the maximum change for each "smoothing" operation. If tolerance is exceeded, the smoothing algorithm runs again, continuing until the change in the path is below the tolerance. If tolerance is too low, the smoothing might never converge, so try raising the tolerance if this occurs.

## Further reading
For more detailed information about this algorithm and how to implement it, Team 1712 has this super fancy writeup which can be found [here.](https://www.chiefdelphi.com/t/paper-implementation-of-the-adaptive-pure-pursuit-controller/166552) [This paper by Coulter and Craig is the original source of this algorithm, and nicely outlines the ideas.](https://www.ri.cmu.edu/pub_files/pub3/coulter_r_craig_1992_1/coulter_r_craig_1992_1.pdf)
