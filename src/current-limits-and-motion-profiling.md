# Current Limits and Motion Profiling

	The battery only has a certain amount of voltage, and when the robot uses too much voltage and the battery voltage goes below 6.8V, the roboRIO enters *brownout protection mode*, which disables all motors and actuators and effectively disables the robot until the voltage comes back up again. The effect of this is that the robot stutters, and on the driver station the battery icon turns red and it tells you it is in brownout protection mode.
