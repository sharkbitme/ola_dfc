# Draw Force Curve measuring Device
## Leveraging the Sparkfun OpenLog Artemis board, the NAU7802 Load Cell Amplifier, and VL53L1X Infrared Distance sensor
### co-developed by Jake Kaminski and Tristan (@delivermyshark)
https://www.youtube.com/watch?v=teMO9oCl4YE
## Hardware:

Openlog Artemis: https://www.sparkfun.com/products/16832

(testing the redboard artemis nano board as a more cost effective measure is going to be underway soon)

Load Cell Amp: https://www.sparkfun.com/products/15242

Infrared Distance Sensor: https://www.sparkfun.com/products/14722

Any loadcell that is capable of at minimum of 40 Kg (88 pounds) of force 

Also recommend the Qwiic cables from sparkfun or adafruit's STEMMA QT cables, 50mm cable length should be sufficient


# OLA General Setup and overview
General guide here: https://learn.sparkfun.com/tutorials/openlog-artemis-hookup-guide/introduction

Arduino IDE setup: https://learn.sparkfun.com/tutorials/artemis-development-with-the-arduino-ide

## One very important thing to note is when installing the Apollo3 board definitions, that you install version 1.2.1, there are known issues with higher versions that will cause compilation in the arduino IDE to fail

There are a pretty large number of libraries that need to be installed, all are outlined with links to install the library in the `ola_dfc.ino` sketch, listed before the global variable declarations

# Wiring of the NAU7802 Load Cell Amplifier:


#### firmware update/flashing
##### have to do some more R&D on this area but easiest way is: 
so for updating firmware, download the sparkfun Artemis firmware updater GUI at: https://github.com/sparkfun/Artemis-Firmware-Upload-GUI/archive/master.zip

extract and go to the "Artemis-Firmware-Upload-GUI-master" directory, then go into Windows and run the 'artemis_firmware_uploader_gui.exe' 

# Implementing functions for the VL53L1X IR sensor that haven't been implemented in the OLA base code:

Reference the vl53l1x-api-user-manual under the /Documentation folder for descriptions of various functions and overall flow

The [libraries/SparkFun_VL53L1X.h](https://github.com/sharkbitme/ola_dfc/blob/main/libraries/SparkFun_VL53L1X.h) header contains a list of supported functions for the device class and calling conventions with brief descriptions of each function


In [libraries/SparkFun_VL53L1X.cpp](https://github.com/sharkbitme/ola_dfc/blob/main/libraries/SparkFun_VL53L1X.cpp) contains the implementations of the functions

## Areas to change are:

### Sensors.ino, Starting at Line 196

For example, added the following lines for debugging to make sure the ROI settings took correctly:

> //print out the current ROI X & Y values

> //debugging with print statements ayyyyy lmaoooo YOLO COWABUNGA
> 
> line 218:
> 
>              if (nodeSetting->printROIX)
>              {sprintf(tempData, "%d,", nodeDevice->getROIX());
>                strcat(outputData, tempData);
>              }
>              if (nodeSetting->printROIY)
>              { sprintf(tempData, "%d,", nodeDevice->getROIY());
>                strcat(outputData, tempData);
>              }



### autoDetect.ino
line 624

>     //call the setROI() function pointing to vars in the struct_VL531LX in settings.h
>     //and pass those as args to the setROI() function
>     sensor->setROI(sensorSetting->x, sensorSetting->y, sensorSetting->opticalCenter);


### settings.h ~line 150
this is where you need to add/declare the datatype, and name of the var to pass as an arg to the function you want to add



>       int x = 4;
>       int y = 4;
>       int opticalCenter = 69;


### nvm.ino
line 487
Where the values of the new function get saved to NVM and/or SD card

>            settingsFile.println((String)base + "x=" + nodeSetting->x);
>            settingsFile.println((String)base + "y=" + nodeSetting->y);
>            settingsFile.println((String)base + "opticalCenter=" + nodeSetting ->opticalCenter);

line 900
>             //add the logic to read the new settings/parameters from the SD card
>          else if (strcmp(deviceSettingName, "x") == 0)
>            nodeSetting->x = d;
>          else if (strcmp(deviceSettingName, "y") == 0)
>            nodeSetting->y = d;
>          else if (strcmp(deviceSettingName, "opticalCenter") == 0)
>            nodeSetting->opticalCenter = d;

OLA.ino ~line 350 to add start prompt

> 	  if (promptToStart == 1);
>     {
>      int choice = -1;
>     Serial.println("press ENTER to when ready to keep some limb manufacturers honest :D .");
>      while (choice == -1) {
>       choice = Serial.read();
>       switch (char(choice)) {
>         case ' ':
>           promptToStart = 0;
>           break;
>         }
>       }
>     }
## SHORT TERM TODO
* add functionality to allow changing of the ROI/FOV and optical center in IR sensor menu
* ranging fluctuation correction factor, look into the signal/sigma threshold settings outlined in the datasheet
* implement changes to read relative distance instead of absolute
* test on Redboard artemis nano board for functionality
  
## MID TERM TODO:
* ????
 
 
## LONG TERM TODO:
 * start working on a re-write or simplification of the code and structure, to make it easier to work with and add features

