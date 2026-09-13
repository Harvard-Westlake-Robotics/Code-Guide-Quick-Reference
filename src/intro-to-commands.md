# Intro To Commands

How do we tell our subsystems to do specific things, such as beginning to intake or to raise an elevator? That’s where commands come in. Commands are a built-in structure in WPILib that allow you to tell subsystems to do things continuously until a condition is met. For example, a command could tell the intake to spin until a coral has been detected in the robot.   
All commands that you write should be written in the commands folder and extend the Command class built into WPILib. 

Standard commands act in the same way as classes (with instance variables and constructors) and also have three methods:  
*Initialize:* This method is called once and sets anything up that needs to be set up before the main command actually executes. Although this should always be present, this method can be empty if there’s nothing that needs to be done once before the command executes.

*Execute:* The execute method is called periodically and contains the main content of the command. For example, an intake command will tell the intake to run at a certain velocity. This is also the place to put down any switching logic you want in the command (ex. The intake runs at 10 m/s without a coral, but runs at 5 m/s once a game piece enters the robot). 

*End:* The end method is called once when the command stops happening and does whatever is needed at the end of the command to reset the relevant subsystems, such as setting an intake to 0\. This method will either be called when ended manually (such as by letting go of a button) or when the isFinished method returns true, which signifies that the command has accomplished its goal and can end naturally.

*isFinished:* This is an optional command, but it returns a boolean that signifies when the command should end naturally. For example, an intake command could end naturally when a game piece enters the robot. 

There is also one more thing to note about commands. The Command library has a special method known as addRequirements, which takes in a SubsystemBase object (reminder: *your subsystem code should extend SubsystemBase in their \[Subsystem\].java file)*. The method adds a required subsystem to the command; a command can have multiple required subsystems at any time. **If a command has required subsystems, it will be unable to be run *unless* all required subsystems have no other commands going on.**   
Sh…, you didn’t see anything… Want a treat?  
[https://www.youtube.com/watch?v=ZAbeyDc03aw\&list=RDZAbeyDc03aw\&start\_radio=1](https://www.youtube.com/watch?v=ZAbeyDc03aw&list=RDZAbeyDc03aw&start_radio=1)

There are bugs inside your walls
