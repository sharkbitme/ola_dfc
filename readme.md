Draw Force Curve measuring Device based on the sparkfun OpenLog Artemis board, the NAU7802 Load Cell Amplifier, and VL53L1X Infrared Distance sensor

Openlog Artemis: https://www.sparkfun.com/products/16832

Load Cell Amp: https://www.sparkfun.com/products/15242

Infrared Distance Sensor: https://www.sparkfun.com/products/14722



so for updating firmware, download the sparkfun Artemis firmware updater GUI at: https://github.com/sparkfun/Artemis-Firmware-Upload-GUI/archive/master.zip

extract and go to the "Artemis-Firmware-Upload-GUI-master" directory, then go into Windows and run the 'artemis_firmware_uploader_gui.exe' 

vid as follows


SHORT TERM TODO:
  add functionality to allow changing of the ROI/FOV and optical center in IR sensor menu
  ranging fluctionation correction factor, look into the signal/sigma threshold settings outlined in the datasheet or custom code 
  implement changes to read relative distance instead of absolute
  
MID TERM TODO:
 start working on a re-write or simplification of the code and structure, to make it easier to work with and add features
 
 
LONG TERM TODO:
  ??????

