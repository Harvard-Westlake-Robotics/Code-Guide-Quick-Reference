# New Robot Checklist

***Before Receiving the Robot:***
1. Create code for all the subsystems the robot will have. For the drive, use the CTRE swerve template created by MechanicalAdvantage (designed specifically for AdvantageKit). In other words, use last year’s drive code and don’t change a thing unless absolutely needed.
    1. This means setting up all IO System basics, structural code, and constants classes
    2. The goal is to have every subsystem as fully functional as possible before even getting the robot.

***After Receiving the Robot:***
1. **Set up the drive system in Phoenix Tuner X.**
2. **Begin preliminary PID Tuning for the drive.** Set up angle offsets and run SysID if you are able to.
3. **Set up controls for the robot.** Create the control scheme for the robot driver and operator. Make sure to set up the control exactly as the driver and operator want them.
4. **When the hardware for a new subsystem is fully installed:**
    1. **Set it up in Phoenix Tuner X**
    2. **Test the code written and fix any bugs**
    3. **Run SysID tests and PID tuning**
    4. **Repeat this with every new subsystem**
5. **After all subsystems are functional in a way that is satisfactory, begin creating autonomous routines and continue testing the robot. **
