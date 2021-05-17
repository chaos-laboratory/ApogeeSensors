# ApogeeSensors


This sketch uses Adafruit M4/M0, but it should be adaptable to any uC. The ADS1115 16-bit I2C differential ADC is used to read the differential channels of the pyranometer and pyrgeometer. The ADS1115 can be pwoered with either 5v or 3.3v, as long as the sensors to don't produce voltage higher than this. Despite the slightly misleading info on the adafruit page, the differential readings CAN be negative. To read both sensors, a third analog channel for reading the thermistor is required - but due to the much larger signal, a normal analog input is fine for this. The high side of the thermistor can be connected to 3.3v or 5v, though 3.3v is preferable.

Make sure to update the unique calibraton constants for your sensor. See below for wiring colors - 


ADC, ADS1115:
https://www.adafruit.com/product/1085


Pyranometer:
![image](https://user-images.githubusercontent.com/74724400/118511122-9bb24780-b6ff-11eb-9164-13e715623904.png)
https://www.apogeeinstruments.com/sp-510-ss-upward-looking-thermopile-pyranometer/
https://www.apogeeinstruments.com/content/SP-510-610-manual.pdf

Pyrgeometer:
![image](https://user-images.githubusercontent.com/74724400/118510996-7de4e280-b6ff-11eb-80d4-4860545fa8d6.png)
https://www.apogeeinstruments.com/sl-510-ss-pyrgeometer-upward-looking/
https://www.apogeeinstruments.com/content/SL-510-610-manual.pdf
