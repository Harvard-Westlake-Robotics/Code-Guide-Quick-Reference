# FRC Coding 101

## WPILib and Vendor Dependencies
FRC Coding traditionally uses a library called WPILib, which comes in different forms for different programming languages (we use Java). In general, WPILib allows us to connect to Driver Station and other important FRC tools in order to run the robot. Any code should be done on a version of VS Code with WPILib enabled.  
The installation guide can be found [here.](https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html)  
Certain aspects of WPILib, such as vendor dependencies, can only be used by accessing the WPILib menu located in the top right hand corner of VS Code.

Over the course of FRC competitions, certain teams and companies have created extensions for WPILib. These extensions are known as **vendor dependencies** (for example, AdvantageKit is a vendor dependency) and must be installed from the internet on WPILib in order to use them. In order to install new vendor dependencies, you will need an install link (which can usually be found on the vendor website or GitHub page). You will then want to go to the WPILib menu in the top right corner, and **search up Manage Vendor Libraries. After, click Install New Libraries (online) and paste in the new link.**

To uninstall libraries, go back to Manage Vendor Libraries and click on Manage Existing Libraries. You can then select whichever libraries you want to uninstall.

## Standard Practice
In general, there is some standard practice that you will want to follow when coding with FRC. For starters, pretty standard shortcuts that can already be used in VS Code are also commonly used in FRC Coding (ex. Cmd+S to save, Shift \+ F5 to upload code to the robot). Additionally, **ALWAYS UPLOAD ANY SUBSTANTIAL AND WORKING CODE YOU HAVE WRITTEN TO THE GITHUB**. This cannot be stressed enough as if it allows everyone to be on the same page and prevents any code from being lost due to you forgetting a computer or the computer breaking. Instead of merging to main, make  a separate branch and upload your code there. This makes sure that we don’t accidentally break anything or lose any code from overriding someone else’s code during the GitHub upload.
