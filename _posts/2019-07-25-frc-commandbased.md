---
layout: post
title:  "FRC Basics: Command Based Programming"
date:   2019-07-25
excerpt: "A Summary"
tag:
- robotics 
- code
- hrtworkshops
comments: false
---


## Subsystems

Subsystems define parts of the robot that need to be controlled, like a drivebase, claw, elevator, or intake. They allow you to use commands to control hardware elements. Subsystems extend the abstract Subsystem class from WPILib. 
All motors should be included in a subsystem as fields. 

Here’s an example of a subsystem representing a simple claw which can open and close:

```java

import edu.wpi.first.wpilibj.command.Subsystem;
import org.usfirst.frc.team670.robot.RobotMap;

public class Claw extends Subsystem {

	Victor motor = RobotMap.clawMotor;  //motor included as field so we can control it using its methods

    public void initDefaultCommand() { 

     	/*  you can leave this method blank, but it needs to be there. This is because it is abstract in the superclass Subsystem, which every subsystem extends */ 

    }

/* Methods in the subsystem represent things the Claw can do. Since we have a motor that needs to be controlled, we’ll make calls to the motor’s methods in this subsystem’s methods. Then, when we use a command to control the Claw, it will be able to call the Claw’s methods to operate the motor and move the Claw.*/

    public void open() {
    	motor.set(1);  
    }

    public void close() {
    	motor.set(-1);
    }

    public void stop() {
    	motor.set(0);
    }
}
```


## Commands and Command Groups


Commands define things that parts of the robot can do. Their purpose is to break the task of operating the robot into smaller chunks, which are easier to work with and combine into sequences to accomplish complex actions. Every robot action can be placed into a command for easy integration with other commands.

Commands incorporate the abilities defined in subsystem methods. They extend the Command class from WPILib. The following 3 methods inherited from the WPILib Command class will often come in handy:

initialize() is called the first time this Command is run after being started.
execute(): does some work. This runs at every update from the driver station
isFinished(): tells you if the work is done. This runs at every update from the driver station



## Command Groups


Earlier, we mentioned that commands help you break actions into small parts which can be combined to accomplish actions. You can easily group commands into (wow, this name is creative) COMMAND GROUPS, which can be executed in 3 ways:
In sequence: run commands one after another
In parallel: run all commands at the same time
Combined: run some commands in a sequence, while running others together at the same time
A command group inherits the required subsystems of all commands in that group.
When executing, note that you can’t cancel the execution of specific commands in the group. You’ll have to cancel the whole group instead. 

Here are some examples of how and when to use command groups:

In this sample, we’ll place a box at a known height using an elevator. Since the actions (raising the elevator, moving the claw/wrist, and opening the claw to drop the box)  must happen in a specific order, the logical choice is to run the commands in sequence, using addSequential() to add new Commands.

```java
//Text in italics highlights Command objects.

public class PlaceBox extends CommandGroup {
	public PlaceBox() {
		addSequential(new SetElevatorSetpoint(Elevator.TABLE_HEIGHT));
		addSequential(new SetWristSetpoint(Wrist.PICKUP));
		addSequential(new OpenClaw());
	}
}
```


In our next example, we’ll get the elevator and claw to prepare to pick up something. The most efficient way to do this would be to move the elevator while the wrist and claw are also moving. So, we’ll have commands all running in parallel, and the class will look like this:


```java
public class PrepareToGrab extends CommandGroup {
	public PrepareToGrab() {
		addParallel(new SetWristSetpoint(Wrist.PICKUP));
		addParallel(new SetElevatorSetpoint(Elevator.BOTTOM));
		addParallel(new OpenClaw());
	}
}
```


Now, let’s say you want to grab something. To do this, you’ll need to close the claw, then stow it, as well as move the elevator back down. Since we can move the elevator and wrist at the same time, but the wrist needs to stow after the claw closes, we can combine sequentials and parallels. 


```java
public class Grab extends CommandGroup {
	public Grab() {
		addSequential(new CloseClaw());
		addParallel(new SetElevatorSetpoint(Elevator.STOW));
		addSequential(new SetWristSetpoint(Wrist.STOW));
	}
}
```


## Scheduling Commands


In order to run commands, you’ll have to schedule them. Every time the driver station receives new data, periodic methods in your Robot class get called -- autonomousPeriodic() during autonomous, teleopPeriodic() during teleop, and disabledPeriodic() when the robot is in disabled mode. (Additionally, there is the robotPeriodic() method, which is called for every packet received no matter what mode the robot is in.) These periodic methods run a Scheduler that checks for triggers for if any commands need to be scheduler or canceled. 

When a command is scheduled, the Scheduler checks to make sure that no other commands are using the same subsystems required by the new command. If any of those subsystems are currently in use, and the command currently running is interruptible, it will be interrupted and the new command will be scheduled. If the current command isn’t interruptible, the new command won’t be scheduled. 
There are 3 main ways to schedule commands:
* You can manually call the start() method on the command object. Use this for autonomous.
* Commands can be scheduled automatically by the scheduler based on trigger actions specified in the code, like a button being pressed or a joystick being moved. These will be checked by the Scheduler. You should define these triggers in the OI class.
* They can also be scheduled automatically on completion of a previous command. 




