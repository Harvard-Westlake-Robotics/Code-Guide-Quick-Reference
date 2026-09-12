# RobotContainer and Robot.java

Much of the robot’s main functionality is initialized in RobotContainer.java and Robot.java. Simply put, RobotContainer.java (along with ControlMap.java) initializes the many elements of the robot using Java classes (such as intake, drive, etc.) while Robot.java runs the robot code itself and can also be modified for functionalities such as LEDs.

## Robot.java
**Robot.java is responsible for starting the robot code once it is enabled on the computer and initializing RobotContainer.java, which in turn initializes the subsystems of the robot.** The robot runs the code in RobotContainer.java periodically.

**Additionally, Robot.java has specific periodic commands which are able to be customized**. These commands really only be used for LED logic and status indications (ex. LEDs light up red if the robot’s intake is running, off if otherwise), while all subsystem periodic logic should go into RobotContainer.java. Finally, Robot.java initializes the Logger, which is explained in a later section. **In short, Robot.java is responsible for the robot as a whole.**

## RobotContainer.java
RobotContainer.java is responsible for initializing the main subsystems of the robot after it is created by Robot.java. RobotContainer.java initializes all subsystems such as Drive, Intake, and other added subsystems, as well as initializing the control schemes for the robot such as the driver and operator controllers. Specifically, RobotContainer is split into two main methods that create the functionality for the rest of the robot.

1. *RobotContainer()*

RobotContainer() serves as the constructor for the RobotContainer class and is called by Robot.java when the robot is started. This constructor initializes every subsystem for the robot (ex. Drive, Intake, etc.) as well as initializing all of the commands it will use (ex. Intake commands, drive movement commands, etc.).   
Additionally, the constructor registers all autonomous commands that the robot will use into PathPlanner’s NamedCommands list, which allows the robot to use those commands during the creation and execution of autonomous routines.  
 

2. *configureButtonBindings()*

configureButtonBindings() does exactly what the name implies:   
It configures the robot’s controls and default commands.   
It does this by setting a default command for each subsystem, which the subsystem will then automatically run in the absence of any other command. It then calls ControlMap.java to configure the controller and button bindings for the driver and operator.

The code in RobotContainer.java is run periodically by Robot.java, and RobotContainer in turn runs its own code periodically so as to make sure that the robot’s subsystems are constantly running. **Whereas Robot.java is responsible for the robot as a whole, RobotContainer.java manages its separate parts.**

> **OUTDATED.** Archived from the source guide. The table of contents marked ControlMap.java outdated. The body below is the original text, kept for history.

## ControlMap.java (OUTDATED)

ControlMap.java is a file that configures the controls for the robot that the driver and operator use during TeleOp command. Usually teams put this straight into RobotContainer’s configureButtonBindings(), however we found that separating the control presets into a separate file helps make everything more organized and also allows for the creation of multiple control presets for different drivers and situations.

ControlMap.java uses a singleton Instance system that is accessible to all files with the method getInstance(). **Since ControlMap has no public constructor, this is the only way you can get access to ControlMap and its methods.**

The only methods that ControlMap has are preset methods, such as configurePreset1.

**These preset methods, which you can write as many as you want of, should all configure the control bindings for a specific control scheme (ex. Xbox driver controller and PS5 driver controller, only Xbox driver controller, etc.).** These should then be called in configureButtonBindings() using the CodingMap Instance to be applied to the robot itself.   
**In short, ControlMap should be used to map out different presets for controlling the robot which will then be applied in RobotContainer.**
