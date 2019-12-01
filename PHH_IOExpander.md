# MCP23017 I/O expander board
This board desined to act as I/O expander for Raspberry Pi. The concept is simple. The MCP23017 receives instructions 
from uP over I2C line and has got two 8 bit register that map to two 8-bit port pins. The ports can either act as 
either Output or Input. The board is desined as a RPI HatHat and hence works on 3.3V .The two 8 bit ports drives 16 LED . 
However the ground connection for the LED resistors is open by default (so LED do not work unless you close the Jumpers 
LEDA-GND and LEDB-GND). The two 8 bit ports are also exposed on two connetors GAH and GBH. Since these ports are connected 
to the IC pins via LEDs , they can accept input voltage of more than 3.3 V (reverse biasing the LEDs). So these  ports are 5V 
tolerant (even though th eboard is a 3.3V board). So to make the ports as input , set them for pull up mode (so that when 
extenal circuit put a high the LED do not conduct but pull up makes the port bit high).


## Features
Provides RPi expanded I/O
The Board operates on 3.3V (pulling supply from RPi Hat header).
The two ports GAH and GBH headers exposes the two 8 bit ports of 23017.
These two headers (GAH and GBH) are 5V tolerant (due to proteection from LEDs)

## Cautions
When using port GAH and GBH , do not set any of the 2 ports are output (as any externa circuit putting low on the 
header pin will cause huge current to flow thru corresponding LED.

So in a Nutshell
  - Used as a LED blink mode (not connecting anything on headers GAH and GBH) , safe to put 23017 ports in output mode.
  - When using the header GAH and GBH to connect to extetnal circuits, advisable to put the 23017 ports as input mode with pullup.


