# Raspberry Pi 4 Hat - PCB extends away from fan 

This header exposes most of the GPIO pins of the Raspberry Pi module in form of three 14 pin headers (headers are in 2x7 format).
Idea is that you develop more boards which get plugged into one of these headers.

  - **J1 header** - Exposes has only Tx/Rx (aka GPIO14/GPIO15) and MOSI/MISO/SCK (aka GPIO10/GPIO9/GPIO11) communication pins of RaspPi exposed (alongwith 4 SPIO pins 17,18,19,20).
  - **J2 header** - Exposes only I2C pins SDA/SDL (aka GPIO2/GPIO3) alongwith 7 GPIO pins 5,6,7,8,12,13,16
  - **J3 header** - Exposes only I2C pins (aka GPIO2/GPIO3) alongwith 7 GPIO pins 21,22,23,24,25,26,227

Note that board created for J1 header will not be compatible with J2/J3 (as Tx/Rx in J1 get replace by SDA/SDL in J2/J3 at corresponding places).

The 3.3 V of RaspBerry Pi gets routed to 3V pins of the 3 headers via a Schotteky diode to avoid any damage to RPi (if some circuit monted on one of the 3 headers starts pushing 3.3 V or 5V on these lines . This also works in advatgae that some other system can share the 3.3 V load alongwith RPi e.g. the I/O expander board the Triket 3V output is routed to 3V pin of the heades via a Schotteky diode).

The headers for a Fan control . GPIO 4 pin can be used to control switching On/Off the fan (if fan pins are connected to the header marked FAN). Note that GPIO4 is reserved for fan control (hence not exposed on any of the header), so do not use this for any purpose.

The four optional LEDs (and their series resistors) are connected to GPIO pin 17,18,19 and 20 . However these LED will not blink as the resistor tails reach connector 5 pin header LED-4 (one of pin is ground). If you short all these pins together , then only LEDs will blink (in case you are getting distracted by blinking LEDs , this is your control in the same - but they are good to check if the stuff is working).


There are two 40 pin headers. The one near to edge is supposed to be plugged into to RPi 40 pin header (you should install a female 40 pin connector at the bottom of the board. The inner 40 pin header is optional one and supposed to have a male header on top side (so that you can connect it via 40 pin cable to some external circuit - but be careful of conencting anything on this header alongwith other PiHatHat boards on one or more 14 pin headers - its ok till you know what you are doing).


**Caution** - Please note that the PiHatHats mounted on the 14 pin headers has to be in sync with RPi GPIO pins i.e. the external circuit and RPi need to be clear that pins RPi exposes as OUT should be configured as IN on the external circuit side (and vise versa). Configuring the GPIO pin on RPi side and connected pin on external circuit (via 14 pin headers) as OUT at the same time is recipe for disaster. So have discpline in program you write on RPi side (and external circuit side) to leave the GPIO pins in tri state (or in INPUT mode) at exit of your programs. On RPi side the solution is simple. Use Python programs to control the GPIO and your python programs should be a catch block which leaves GPIO pin in either TriStae or in INPUT mode.
