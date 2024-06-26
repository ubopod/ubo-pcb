# Ubo PCBs
This repo contains Top and Side PCB schematics and layouts as well as documentation for each PCB function. We will be adding schematics and layouts of other newly designed PCBs here as well. The schematics and layout files are made in Eagle CAD and we plan to add KiCAD version as well.

## Top PCB Overview

![image](https://github.com/ubopod/ubo-pcb/assets/3680934/c8a65a35-d7b0-463a-8e53-6c7a4b00562b)

In designing Ubo Top PCB (HAT), we tried to use popular components that have already gained adoption among the developer community and are developer friendly. In addition, we made sure that we can source these components for manufacturing. There are several development boards with one or several of these components that you can buy from either Sparkfun, Adafruit, Tindie, SeedStudio or other vendors. At the end of this repo, we have provided links to some of the development boards as reference.

The main objective in designing Ubo was centred around improving developer and end-user experience through offering a rich user interface. Since Raspberry Pi by itself is just a compute brain with no peripherals, it is often challenging to offer a compelling UX/UI to the end user without an interface.

In the following section, we discuss how each sub-system was chosen to enhance user and developer experience as well as technical details of implementation.

## RASPBERRY PI HEADER

![RPi_Header](images/rpi-header.png)

## LCD

backlight is connected to GPIO26
TODO: link to datasheet

![LCD schematic](images/lcd.png)

## Keypad
![LCD schematic](images/keypad.png)

You can access the datasheet for GPIO Expander [here](datasheets/AW9523_GPIO_expander.pdf)

## RGB LED Ring

![RGB LED Ring](images/rgb-ring.png)

## Audio
### Speakers
### Line Out
### Microphones

## Temperature sensor
![RGB LED Ring](images/temperature-sensor.png)

## Light Sensor
![RGB LED Ring](images/light-sensor.png)

## EEPROM
![RGB LED Ring](images/eeprom.png)

## Fan
![RGB LED Ring](images/fan.png)

## Power Button
![RGB LED Ring](images/power-button.png)

## Security
![RGB LED Ring](images/security.png)

## Experimental SDR
![RGB LED Ring](images/sdr.png)

