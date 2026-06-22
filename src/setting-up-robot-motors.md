# Setting Up Robot Motors With Phoenix Tuner

Upon receiving a built robot (which could just be the drive base), the **first thing you should always do is configure motor IDs and names.** Each motor must have a specific ID and a name that nicely lays out its job. 

*1148 Standard Configuration Conventions:*

**For drive motors:**
1. Identify the sides the motors are on (front and back, left and right) as well as which turn and drive motors go together.
2. Starting from ID 1-2, pick a side (ex. Front left). Set the ID of the drive motor to the odd ID and the turn motor to the even ID.
3. Repeat for every other corner, with IDs 3-4, 5-6, 7-8.

**The following is a sample configuration of the drive**

ID 1 → Front Left Go\
ID 2 → Front Left Turn\
ID 3 → Back Left Go\
ID 4 → Back Left Turn\
ID 5 → Front Right Go\
ID 6 → Front Right Turn\
ID 7 → Back Right Go\
ID 8 → Back Right Turn\
**Ensure you do not assign duplicate IDs.**

**Subsystems:**

Once a subsystem motor (ex. Intake, elevator) is added, it must be assigned an ID and name. **Use the same system as drive motors (ex. ID 9 → Intake). Do this after any subsystem motor is added.**

**CAN Buses:**\
**CAN Bus modules should be named after the side they are tracking (ex. Front Left) and assigned an ID.**

**Pigeon:**\
The standard name can be kept, **but the ID cannot be a duplicate.**
