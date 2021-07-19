# Implementing functions for the VL53L1X IR sensor that haven't been implemented in the OLA base code:

Reference the vl53l1x-api-user-manual under the /Documentation folder for descriptions of various functions and overall flow

The [libraries/SparkFun_VL53L1X.h](https://github.com/sharkbitme/ola_dfc/blob/main/libraries/SparkFun_VL53L1X.h) header contains a list of supported functions for the device class and calling conventions with brief descriptions of each function


In [libraries/SparkFun_VL53L1X.cpp](https://github.com/sharkbitme/ola_dfc/blob/main/libraries/SparkFun_VL53L1X.cpp) contains the implementations of the functions

## Areas to change are:

### Sensors.ino, Starting at Line 196 where the  

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
