# Raspberry Pi 4 Hat - faces PCB away from fan

This header exposes most of the GPIO pins of the Raspberry Pi module in form of 3 14 pin headers (headers are in 2x7 format).
Idea is that you develop more boards which get plugged into one of these headers.

J1 header - Exposes has only Tx/Rx  and SPI communication pins of RaspPi exposed (alongwith 4 SPIO pins 17,18,19,20)
J2 header - Exposes only I2C interface alongwith 7 GPIO pins 5,6,7,8,12,13,16
J3 header - Exposes only I2C interface alongwith 7 GPIO pins 21,22,23,24,25,26,227

Note that board created for J1 header will not be compatible with J2/J3 (as Tx/Rx in J1 get replace by SDA/SDL in J2/J3).

It has also got two 

The 3.3 V of RaspBerry Pi gets routed to 3V pins of the 3 headers via a Schotteky diode to avoid any damage to RPi (if some circuit monted on one of the 3 headers starts pushing 3.3 V or 5V on these lines . This also works in advatgae that some oetehr system can share the 3.3 V load alongwith RPi).

The headers for a Fan control . GPIO 4 pin can be used to control switching On/Off the fan (if fan pins are connected to the header marked FAN).


The four optional LEDs (and their series resistors) are connected to GPIO pin 17,18,19 and 20 .
