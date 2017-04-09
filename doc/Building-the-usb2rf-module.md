The usb2rf module acts as a bridge between the PC and the embeded system. Allows to communicate with the project, and to
update the firmware

Building the usb2rf module needs a little time but it needs to be done only once.

Through you can build one module based on a custom PCB, it is recommended to build a simple one with some jumper wires.

Lets start with the simplest option, a module with :
- A FTDI module
- A ProMini 3.3V
- CC1101 RF module
- Some Female-to-Female jumper wires

## FTDI module
![FTDI](https://github.com/pkarsy/rfboot/wiki/FTDI.jpg)

## A ProMini 3.3V
![Pro Mini 3.3](https://github.com/pkarsy/rfboot/wiki/ProMini33.jpg)

## A cc1101 module
![CC1101](https://github.com/pkarsy/rfboot/wiki/images/cc1101.jpg)

Here is the final result

Now the firmware needs to be uploaded. Again this need to be done only once.
Although the source code is a standard Arduino project you need to install the libraries
**[AltSoftSerial](https://github.com/PaulStoffregen/AltSoftSerial)** and **"DigitalWriteFast"**. For the lazy there is precompiled the

**usb2rf.hex** file in the usb2rf folder

## Installing the firmware.

adduser myUserName dialout.

If you are not already a member of dialout, you need to logout and login, otherwise you will not have access to
the serial port and the next commands will fail.

Open a terminal
tail -f /var/log/syslog
Connect the module to a usb port of the PC.
In the terminal is shown which port the FTDI is, usually /dev/ttyUSB0 or /dev/ttyUSB1
Open a console:
avrdude