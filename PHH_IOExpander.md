# MCP23017 I/O expander board
This board designed to act as I/O expander for uP. The concept is simple. The MCP23017 receives instructions 
from uP over I2C line and has got two 8 bit register that map to two 8-bit port pins. The ports can either act as 
either Output or Input. Chip MCP23017 is verstile whose ports in input mode can either be made pull up or pull down or none. At the same time it can be configured to generate interrupt on change in logic state or wither rising /falling edge of any of the ports . Note that 23017 is a versatile chip with many features and this board is configured to use few of them.

## Caution
  - Never connect RPi header (14 pin - left side) as well as 3V/5V-I2C header (6 pin - right side) at the same time (if the 6 pin header pushes 5V on Vcc line, then the normally 3V lines on Pi header (first two pins) start getting 5V (though it may not damage RPi as the PiHat contains a Schotteky diode which will get reverse bias tgus protecting the RPi, but any other parallel circuits on RPi Hat will suddely see 5V coming on 3V . Second risk is the SDA and SDL lines will get 5V signals - though series resistors R1-SD and R1-SL have been added alongwith Zener 3.3V diodes for protection but it seems zener has around 50pF capacitance and will make bus speed slow - see https://electronics.stackexchange.com/questions/140412/how-does-a-zener-protect-my-microcontroller and https://electronics.stackexchange.com/questions/140412/how-does-a-zener-protect-my-microcontroller - so if u face issues simply remove the zeners and short the resistors - and be careful not to connect any 5V stuff at 6pin header. The Adafruit I2C safe bidir level shifter is out of stock and we can opt to make similar circuit ourselves using BSS138 FET  ).
  - Never plugin Trinket M0 in the Trinket header when board is operating at 5V 
  - Insert Trinket M0 header in right orientation (else it may damage the board as well as Trinket - see the legends on board showing the pins while inserting).
  - When using GBH to connect external circuit, do not set the B port as output (as any external circuit putting LOW on the header pin , while B port pin is set to HIGH, will cause huge current to flow thru corresponding LED - damaging wither of two or both circuits).

## Usage
The board is desined so that it can work I/O expander for four different cases
  - **Expand-1** - As RPiHatHat board that can be connected to RPiHat with 14 pin header **PIHAT-HEADER1** to any of J1 and  J2 ( **not** J3) connectors of RPiHat. This this mode the whole board is working at 3.3 V (Amongst signal pins , only SDA, SDL , and G7 are used. No other signal pins used. 3V is used to power Vcc of board, 5V is conected to Triket M0 header as Vbat and G7 is connected to REST of Trinket M0)
  - **Expand-2** - Board's header **5V/3V I2C** plugins into RPiHatHat header **3V-I2C/SPI-1** or **3V-I2C/SPI-2**  (Board operates at 3.3 V)
  - **Expand-3** - Board's header **5V/3V I2C** plugins into RPiHatHat header **5V-I2C/SPI-1** or **5V-I2C/SPI-2**  (Board operates at 5 V)
  - **Expand-4** - As a I/O expander for any uC that comes with I2C signal (that can be connected to header **5V/3V I2C** ) ( Board operates at volatge supplied by the connector).

## Operation

## Trinket M0 header
The board provides a 10 pin header to plug a Adafruit Trinket M0  (which is a SAM21D 32 bit 32K RAM 256K EPROM plus 2M flash and comes preloaded with Circuit Python). The SDA/DSL of the Trinket M0 can be attached to main SDA/SDL via jumpers SW-TMSD/SW-TMSL. The Triket works at 3.3V level and expects the board to be running at 3.3V signal level , so its ok to plugin when board is connected to RPiHat (it draws power from 5V connector so does not require USB connection - you can connect USB if you want). 

When **5V/3V-I2C** header is connected, it is only safe to plug trinket the board only on two conditions
  - The Vcc of the header is at 3.3V and signals are also at 3.3V
  - The Trinket M0 is powered from USB

Never connect Trinket if **5V/3V-I2C** is connected and operating at 5V signals levels (maybe add a I2C bidirectional convertor to work around this limitation).

### LEDs
The two 8 bit ports drives 16 LEDs . However the ground connection for the LED resistors is open by default for Port B (so LED do not work unless you close the Jumpers LEDB-GND). By setting the 23017 B port pins as output, you can blink all the possible LED you wanted to blink. Regarding port A , all the eonnected LEDS series resistors' tail are routed to pins on header GAH (along with a GND pin). So if you short all the pins of the GBH (or selective pins are connected to ground), you can blink the port A connected LEDs.

## Headers GAH/GBH
The two 8 bit ports (viz A and B) are also exposed on two headers GAH and GBH. 
  - **GAH Header** - This header is desinged to primarily work as output (with a protection series resistor - so that if its connected to a external circuit which also want to act as output - the resistor will limit the current). The LED protects if the chip is workgin at 3.3 V and some 5V stuff is applied at the header pin (though even resistor itself could protect - so you can even short the pins of LEDs and still the board will have protection). The board can also work as input but remember to set the port to hugh pullup.
  - **GBH Header** - Primarily desiged to work as input (no series protection resistors - but the LED try to protect if chip is running at 3.3V and someone try to put 5V at the header pin). When setting as input port, remember to set the PullUp option on (so that if someone try to put 5V or 3.3 V at output when chip is running at 3.3 V thus reverse biasing the LED, the internal pull up resistor option will make the input read high). This will work even if chip is operating at 5 V and you try to connect a 3.3V as input on the header (but the header will require to sink current going from pull up resistor). If you are not planngin to connect any external circuit to GBH header and plan to use it to blink LEDs , the LEDs won't work unless you close the jumper **LEDB-GND**.
 

Note that it can be risky to set the 23017 B port (connected to header GBH) to Output when anything is connected at the headers GBH. Reason being if the connected external circuit also sets their port as output and 23017 pin is high while external circuit is low , it will damage any or both chips due to huge current flow (if you are sure what you are doign you can opt to set the B port to output).


## Features
Provides RPi expanded I/O
The Board operates on 3.3V (pulling supply from RPi Hat header).
The two ports GAH and GBH headers exposes the two 8 bit ports of 23017.
These two headers (GAH and GBH) are 5V tolerant (due to protection from LEDs going reverse bias stopping current flow)


So in a Nutshell
  - When board is used to just blink LEDs (not connecting anything on headers GAH and GBH) , safe to put both 23017 ports in output mode.
  - When using the header GBH to connect to external circuits, advisable to put the 23017 B port as INPUT mode with pullup. Port A can be put in output mode in all cases.
  - Header GAH has series resistors (alongwith a series LEDs) when connecting port A , so bit safe to put as output with external circuits (though don't test limits).


## I2C address
There are 3 pins viz A0,A1,A2 using which you can use 8 different I2C addres son which the 23017 can be addresses.
When all 3 pins are pulled low , the address is 0x20. With A0 pulled high , address is 0x21 .
On the board all the 3 pins have been pulled high by a pull up resistors hence the I2C address of 23017 will be 0x27. But there are 3 jumpers viz GNDA0, GNDA1 and GNDA2 (@ Middle Right) using which you can selectively pull these 3 pins down to configure the I2C address of 23017.

## Interrupts
When 23017 ports are set as INPUT you can configure them to generate interrupts on any logic status changes on any of the port pins. These pins on the board are left disconneted by default but can be routed to the 3V/5V-I2C connector via jumpers INTA and INTB (@ Right Bottom).
