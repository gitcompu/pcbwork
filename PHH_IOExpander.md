# MCP23017 I/O expander board
This board desined to act as I/O expander for uPs. The concept is simple. The MCP23017 receives instructions 
from uP over I2C line and has got two 8 bit register that map to two 8-bit port pins. The ports can either act as 
either Output or Input. Chip MCP23017 is verstile whose ports in input mode can either be made pull up or pull down or none. At the same time it can be configured to generate interrupt on change in logic state or wither rising /falling edge of any of the ports.

## Usage
The board is desined so that it can work
  - **Expand-1** - As RPiHatHat bboard that can be connected to RPiHat with 14 pin header **PIHAT-HEADER1** to any of J1, J2 or J3 connectors of RPiHat. This this mode the whoel board is working at 3.3 V.
  - **Expand-2** - Board's header **5V/3V I2C** plugins into RPiHatHat header **3V-I2C/SPI-1** or **3V-I2C/SPI-2**  (Board operates at 3.3 V)
  - **Expand-3** - Board's header **5V/3V I2C** plugins into RPiHatHat header **5V-I2C/SPI-1** or **5V-I2C/SPI-2**  (Board operates at 5 V)
  - **Expand-4** - As a I/O expander for any uC that comes with I2C signal (that can be connected to header **5V/3V I2C** ) ( Board operates at volatge supplied by the connector).

## Operation

### LEDs
The two 8 bit ports drives 16 LEDs . However the ground connection for the LED resistors is open by default (so LED do not work unless you close the Jumpers LEDA-GND and LEDB-GND). By setting the 23017 port pins as output, you can blink all the possible LED you wanted to blink.

## Headers GAH/GBH
The two 8 bit ports (viz A and B) are also exposed on two headers GAH and GBH. 
  - **GAH Header** - This header is desinged to primarily work as output (with a protection series resistor - so that if its connected to a external circuit which also want to act as output - the resistor will limit the current). The LED protects if the chip is workgin at 3.3 V and some 5V stuff is applied at the header pin (though even resistor itself could protect - so you can even short the pins of LEDs and still the board will have protection). The board can also work as input but remember to set the port to hugh pullup.
  - **GBH Header** - Primarily desiged to work as input (no series protection resistors - but the LED try to protect if chip is running at 3.3V and someone try to put 5V at the header pin). When setting as input port, remember to set the PullUp option on (so that if someone try to put 5V or 3.3 V at output when chip is running at 3.3 V thus reverse biasing the LED, the internal pull up resistor option will make the input read high). This will work even if chip is operating at 5 V and you try to connect a 3.3V as input on the header (but the header will require to sink current going from pull up resistor).
 

Note that it can be risky to set the 23017 B port (connected to header GBH) to Output when anything is connected at the headers GBH. Reason being if the connected external circuit also sets their port as output and 23017 pin is high while external circuit is low , it will damage any or both chips due to huge current flow (if you are sure what you are doign you can opt to set the B port to output).


## Features
Provides RPi expanded I/O
The Board operates on 3.3V (pulling supply from RPi Hat header).
The two ports GAH and GBH headers exposes the two 8 bit ports of 23017.
These two headers (GAH and GBH) are 5V tolerant (due to proteection from LEDs)

## Cautions
When using header GBH , do not set the port as output (as any external circuit putting LOW on the 
header pin , while B port pin is set to HIGH, will cause huge current to flow thru corresponding LED.

So in a Nutshell
  - Used as a LED blink mode (not connecting anything on headers GAH and GBH) , safe to put 23017 ports in output mode.
  - When using the header GBH to connect to extetnal circuits, advisable to put the 23017 B port as INPUT mode with pullup.
  - Header GAH has series resistors (alongwith a series LEDs) when connecting port A , so bit safe to put as output with rough circuits (though don't test limits).


