﻿[![EN](https://user-images.githubusercontent.com/9499881/27683803-659dc988-5cd8-11e7-9c05-0b747e917666.png)](https://github.com/TrueOpenVR/TrueOpenVR-Core/blob/master/Library/README.md) 
[![RU](https://user-images.githubusercontent.com/9499881/27683795-5b0fbac6-5cd8-11e7-929c-057833e01fb1.png)](https://github.com/TrueOpenVR/TrueOpenVR-Core/blob/master/Library/README.RU.md) 
[![CN](https://user-images.githubusercontent.com/9499881/31012373-978ce414-a522-11e7-9936-387b1c530e2f.png)](https://github.com/TrueOpenVR/TrueOpenVR-Core/blob/master/Library/README.CN.md) 
[![ES](https://user-images.githubusercontent.com/9499881/31012379-9d8f7764-a522-11e7-8bf4-739077369e8b.png)](https://github.com/TrueOpenVR/TrueOpenVR-Core/blob/master/Library/README.ES.md) 
[![FR](https://user-images.githubusercontent.com/9499881/31012387-a7b4aaac-a522-11e7-8485-36ce58dc2d4a.png)](https://github.com/TrueOpenVR/TrueOpenVR-Core/blob/master/Library/README.FR.md) 
[![DE](https://user-images.githubusercontent.com/9499881/31012392-ac051326-a522-11e7-9c8c-2186ddf553d0.png)](https://github.com/TrueOpenVR/TrueOpenVR-Core/blob/master/Library/README.DE.md) 
[![PT](https://user-images.githubusercontent.com/9499881/31012384-a1d1b544-a522-11e7-8a13-3cb53450d55c.png)](https://github.com/TrueOpenVR/TrueOpenVR-Core/blob/master/Library/README.PT.md)
# Functions TrueOpenVR
All functions are imported directly from the "TOVR.dll" library. The library path can be obtained from the registry.


**GetHMDData** - Receiving rotation data (Yaw, Pitch, Roll) and positioning (X, Y, Z) of the VR headset. In case of successful reception, returns 1, otherwise 0.

If you need a quaternion, you can calculate from Yaw, Pitch, Roll as follows:

t0, t1, t2, t3, t4, t5, qW, qX, qY, qZ - double.
```c
t0 = cos(DegToRad(yaw) * 0.5);
t1 = sin(DegToRad(yaw) * 0.5);
t2 = cos(DegToRad(roll) * 0.5);
t3 = sin(DegToRad(roll) * 0.5);
t4 = cos(DegToRad(pitch) * 0.5);
t5 = sin(DegToRad(pitch) * 0.5);
qW = t0 * t2 * t4 + t1 * t3 * t5;
qX = t0 * t3 * t4 - t1 * t2 * t5;
qY = t0 * t2 * t5 + t1 * t3 * t4;
qZ = t1 * t2 * t4 - t0 * t3 * t5;
```

qW, qX, qY, qZ - quaternion.<br>

**GetControllersData** - Receiving data (buttons, sticks, triggers) about the VR controller. In case of successful reception, returns 1, otherwise 0.


**SetControllerData** - Reverse feedback for the controller (vibration). In case of successful set, returns 1, otherwise 0.


**SetCentering** - Centering the device (reset rotation). In case of successful set, returns 1, otherwise 0.


Types and parameters of functions can be seen in libraries.

# Parameters TrueOpenVR
It is desirable that the application has two windows, a main window with a game or program for the VR display and a second small window located on the desktop of a conventional display (not a VR), with the ability to close the application and possibly some more functions.
The main window should be launched in the "Borderless Windowed FullScreen" mode, which means a normal window, without borders, with the size of the display resolution.

![](https://user-images.githubusercontent.com/9499881/27838382-5d76aadc-60fb-11e7-9a1c-a312f2dddccc.png)


All parameters are in the registry branch **"HKEY_CURRENT_USER\Software\TrueOpenVR"**.


The **"ScreenIndex"** parameter is responsible for the display number. For example, 1 is the main display, and 2 is the VR headset.


The **"ScreenControl"** parameter is responsible for the auto enable and disable VR display. Enable option - 1, disable - 0.


The **"Scale"** parameter is responsible for scaling the image. If the parameter is set to "True", then the image with width "UserWidth" and height of "UserHeight" is stretched to the entire display "ScreenIndex".
If the parameter is set to "False", the image is not scaled and displayed in the center of the window, empty areas of the window have a black background. The parameter is necessary to eliminate blind areas in the VR headset.


The **"FOV"** parameter is responsible for the field of vision seen by the eye.


The **"UserWidth"** and **"UserHeight"** parameters are responsible for the size of the image in the window. By default, this is the size of the "ScreenIndex" display, but the user can change it to eliminate blind areas.


The **"RenderWidth"** and **"RenderHeight"** parameters are responsible for resolution in applications or games. For example, a user lacks a productive computer and reduces the resolution of the game or application to improve performance.


The **"Library"** parameter is responsible for the path to the main library with the functions that you need to load to retrieve data.


The **"Drivers"** parameter is responsible for the path to the folder with the drivers.


The **"Driver"** parameter is responsible for the name of the current driver.