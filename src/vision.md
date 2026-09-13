# Vision

One of the most important, and most complex, systems in the entirety of the robot code is the vision system. Using cameras and a lot of complicated math, the vision system’s main purpose is to allow the robot to see where it is on the field for certain functionalities, such as our path finding systems. 

## The Basics of Vision
In essence, the entirety of the vision system relies on limelight cameras and some complicated math. The robot’s limelight cameras take snapshots of what they currently see, focusing specifically on special tags known as April Tags, which are in essence mini QR codes. From there, the limelight estimates its distance away from the limelight as well as at what angle the robot is looking at the April Tag from. From there, the code figures out how much we should trust that position measurement, accepting it or rejecting it based on ambiguity and its deviation from the mean position measurement it has. Finally, the robot updates where it thinks it is on the field, which we can see in Advantage Scope through its 3D field feature.  
In essence, the vision process follows a step by step process: 

1. *Limelight camera takes a snapshot* → A limelight mounted onto the robot takes a picture of what it sees.   
2. *Limelight identifies visible April Tags* → The limelight takes that picture and identifies any visible April Tags in the photo. If there are none, the limelight photo is discarded.  
3. *Limelight estimates position relative to April Tags*  → The limelight uses the amount of space taken up by each April Tag in the photo in order to estimate the distance of the robot from each of those tags and calculates the position of the robot based on those distances.  
4. *The robot calculates its position based on its measurements* → The robot takes the measurements it got from the limelights and uses them to calculate its position on the field. It then sets its position to the calculated position.  
5. *Repeat steps 1-5 indefinitely* → This process happens every 20 ms.

## Vision Hardware
Other than code, all Limelights are managed using the Limelight Hardware Manager. The Limelight Hardware Manager is important because it allows direct access to Limelight settings necessary for setting up, calibrating, and tuning the Limelights. The Limelight Hardware Manager has a logo that looks like this and is launched as a standalone application. 

When you open up the application, you need to scan for available Limelights connected to the robot. You will be able to access any Limelights that pop up through the web UI.

Opening up a Limelight will give you the screen above:

## Setting Up Vision
Before the robot can use Limelights for vision, they must be set up both in code and other software. This allows them to be functional for our measurement positions. You will need multiple things to be able to calibrate vision properly. 

## Focusing Limelights:
Before you do anything with Limelights, you should first make sure that they can at least see clearly on the field. An unfocused Limelight will be unable to accurately track AprilTags on the field. Before focusing a Limelight, place it in an environment with lighting as close as possible to a tournament.  
To focus a Limelight, open it in the Limelight Hardware Manager and change the mode of the Limelight from “Camera” to “Focus.” You should now see a large green number appear on the screen. **Your goal is to maximize that green number (a really well-focused limelight will have a score of 12,000-13,000 when looking directly at an AprilTag).** One way to do this is to play around with the contrast and brightness of the camera. Once you think that the camera’s contrast looks good, you can focus the Limelight itself by turning the ring around the lens on the Limelight.  
**Once a Limelight is fully focused, superglue the ring around the lens so that it doesn’t move.**

Once you have a focused Limelight, you can move onto calibration and optimization. 

## Calibration of Limelights:
Limelight calibration is extremely important and should be done once a Limelight is mounted onto the robot. Before beginning calibration, ensure that the Limelight you wish to calibrate is connected to the robot and is on. Additionally, make sure to have a ChArUco Board on hand. The ChArUco board is used specifically for limelight calibration; it is a big board full of tiny AprilTags:  
**Picture of Charucoboard here**

Once you are ready to begin calibration, open up the details of the Limelight you wish to calibrate using the Limelight Hardware Manager. Make sure that the camera can at the very least detect an AprilTag properly. Additionally, go to the “Snapshot” mode of the Limelight camera, delete all the previous snapshots it has (if any), then switch back to “Camera.” Now, follow these steps to calibrate:

1. *Capture snapshots* → Hold the ChArUco Board up to the Limelight at various angles (from the side, in front, over the top of the camera, etc.) and click the “Capture Snapshot” button to take a picture of the ChArUco board. **At the very minimum, you want around 25 snapshots, but it’s recommended to have 100+  snapshots for really accurate calibration.**  
2. *Calibrate* → Navigate to the “Calibration” tab of the Limelight (On the sidebar) and fill in the details in the “ChArUco Calibration” field. Look at the bottom of the ChArUco Board to fill in the details. Once you’re done, click the calibration button. Wait a few seconds, and the computer will tell you if the calibration was successful. **If calibration was not successful, redo it.**  
3. *Upload the Results* → The Limelight will not use your calibration results by default; you have to upload the results for them to take effect. In the “Calibration” tab, download the latest calibration results onto your computer, then upload them into the “Custom (File) Field.” Set your preferred calibration to the custom upload and you’re set! 

*Note: The calibration requires the dimensions of the board you’re using before it calibrates the limelights. Our board has 15x15 dimensions, with 30mm squares (22mm markers), and a 4x4 dictionary with 100 markers. This can also be found on the board itself.* 

## The Finishing Touches → Limelight Positions
When a Limelight estimates the robot’s position, it uses its position on the robot to accurately do so. So, you need to give each Limelight its position on the robot for accurate measurements. To do so, open up a Limelight in the Hardware Manager, then navigate to the “Advanced” tab. If “Full 3D Tracking” is not enabled, turn it on. You now want to get the position of each Limelight (in inches) from the design team. Input those into the position under “Field Space Localization Setup,” and make sure that the 3D view in the Visualizer is accurate to how the robot looks in real life.  
**Important:** **If you find that your odometry is flipped around (going left moves you right), that is likely because your Limelight positions are flipped around (as in the robot thinks the front Limelights are on the back of the robot).** 

## Vision in Code
The good news is that most of vision is already handled by the Limelights themselves, including pose estimation. *Your* job is to interpret the results and give it to the drive estimator for application. 

## Vision Filtering
Limelight filtering is done in two ways within our codebase: pose rejections and Kalman filtering. In terms of pose rejections, a pipeline needs to be set up within the code that rejects poses given by the cameras if they are way too untrustworthy. The Limelight is your friend in this as it gives a multitude of stats about its tag detections, including the ambiguity of the detection (i.e. how sure it is about its position) and the distance away from the tag (if a tag is too far away we should reject it automatically). Although base code is already in our codebase for this, it can always be updated depending on the circumstances and what we are doing with vision:

Kalman filtering is essentially figuring out exactly how much we trust the estimation of a pose. The Kalman filter takes in 3 different constants relating to x, y, and angle that all signify how much to trust the poses it receives. Although Kalman filtering is an extremely complicated topic, the basics needed for the 1148 codebase is that the standard deviations the Kalman receives essentially tells it how much the Limelight position deviates away from a predicted measurement (in this case, where manual odometry says we should be). Increasing the standard deviation for anything tells the filter that the Limelights will deviate more, causing it to trust them less. Decreasing them will cause the filter to trust the measurements more since it expects they will line up. As of now, these are constants within VisionConstants.java.  
Kalman filtering is automatically done for you within addVisionMeasurement, which is the method that applies an estimation from a Limelight to the robot:

## MegaTag1 v. MegaTag2 (and IMUs)
Limelight pose estimation can occur in one of two modes: MegaTag1 and MegaTag2. MegaTag1 is less accurate but requires a lot less information, therefore it is a lot easier to set up and can be relied upon when the robot does not need extremely precise positioning (i.e. shooting at the beginning of a match). MegaTag1 simply estimates the position using the distance of the robot away from the tags it detects, effectively picking the most likely scenario while trying its best to account for error. Because it does not take into account rotation, MegaTag1 can be really inaccurate while moving because the error grows with uncertainty in the tag.  
MegaTag2, meanwhile, takes into account the orientation of the robot while estimating the position. This significantly decreases error because the range of possible poses the robot can be at drastically decreases. Because MegaTag2 requires the precise orientation of the robot, you need to be sure that you are providing extremely up-to-date and accurate rotation info from the gyro. Otherwise, you could end up in a feedback loop that will cause the robot’s position to become really accurate really quickly.  
Additionally, each Limelight has a built-in IMU that can be used to get even more up-to-date estimations from tags. IMUs are essentially mini-gyros that report the Limelight’s current angular velocity, orientation, and other data. For the IMUs to work, the robot’s orientation needs to first be properly set (although if you have not done this you will have bigger problems than IMUs). There are 5 different modes for the IMUs although there are really only 3 that are needed for proper functionality.  
**IMU Mode 1 calibrates the internal IMU of the Limelight with the gyro rotation so that it can be used later on. You should use this while disabled.**   
**IMU Mode 3 can be used with MegaTag1. It fuses the internal IMU measurements of the Limelight with MegaTag1 poses to get better pose estimations (akin to a less accurate MegaTag2).**   
**IMU Mode 4 can be used with MegaTag2, fusing the rotation of the gyro with the IMU rotations, making MegaTag2 even more accurate.** 

Although this section covered almost everything that is needed to get started and handle a majority of vision, more advanced documentation can be found here.
