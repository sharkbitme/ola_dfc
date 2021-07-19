# Draw Force Curve measuring Device
### based on the sparkfun OpenLog Artemis board, the NAU7802 Load Cell Amplifier, and VL53L1X Infrared Distance sensor
## Hardware:

Openlog Artemis: https://www.sparkfun.com/products/16832

(testing the redboard artemis nano board as a more cost effective measure is going to be underway soon)

Load Cell Amp: https://www.sparkfun.com/products/15242

Infrared Distance Sensor: https://www.sparkfun.com/products/14722

Also recommend the Qwiic cables from sparkfun or adafruits STEMMA QT cables

# Wiring of the NAU7802 Load Cell Amplifier:


#### firmware update/flashing
##### have to do some more R&D on this area but easiest way is: 
so for updating firmware, download the sparkfun Artemis firmware updater GUI at: https://github.com/sparkfun/Artemis-Firmware-Upload-GUI/archive/master.zip

extract and go to the "Artemis-Firmware-Upload-GUI-master" directory, then go into Windows and run the 'artemis_firmware_uploader_gui.exe' 




## SHORT TERM TODO
* add functionality to allow changing of the ROI/FOV and optical center in IR sensor menu
* ranging fluctuation correction factor, look into the signal/sigma threshold settings outlined in the datasheet
* implement changes to read relative distance instead of absolute
* test on Redboard artemis nano board for functionality
  
## MID TERM TODO:
* ????
 
 
## LONG TERM TODO:
 * start working on a re-write or simplification of the code and structure, to make it easier to work with and add features

