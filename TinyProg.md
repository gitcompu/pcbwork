# Programming board for Mega 328 as well as AtTiny 84, 85 and 2313

## Uploading code to the Microcontrollers
One purpose of the PCB is to provide a board which can be used to program the AtTiny (84,85 and 2313) chips as well as Mega 328 chip. In this avatar of teh board it will have to zif socket (to easily be able to put in chip and remove) . One 28 pin Zif socket for Mega 328 while other 28 pin Zif socket for Tiny 2313 (upper part) and Tiny 84 (lower part). The Tiny 84 will not have Zif socket so has to insert and remove in a normal IC socket. It mainly exposes the MISO, MOSI , SCK and RESET pins of all these microprocessors (so no need of pin having bootloader installed) so that they can be programmed with Ardiuno as ISP programmer. These pins are exposed on connectors
  - H-TINY2313
  - H-TINY84
  - H-TINY85
  - H-MEGA328
## General pupose board
  Second avatar of the board is to used as general purpose board. 
### Sensors
The board is studded with place or headers for sensors and all sensors are connected to Tiny 84 chip. They are
    - DHT11 - temperatue and Humidity (1-wire interface)  (connected to PB2 of Tiny 84)
    - DS18B20 - Header for the connector for Temerature sensor encased in waterproof steel pipe  (connected to PA7 of Tiny 84)
    - LM35Z - Analog temperature monitor (20 mv per degreee centigrade)  (connected to PA1 of Tiny 84)
    - A1302 - Magenetic sensor (Hall sensor)  (connected to PA2 of Tiny 84)
    - TSOP-4838 - Infra Red seonsor IC for 38 KHz freq IR Remotes (connected to PB1 of Tiny 84)
### Blink LEDs
The board also contain five LEDs which are connected to one or two pins (for 2313 there are two pins rest only 1 pin) of 4 Micro controllers. The name of LEDs is self evident to depict the chip name and pin e.g. T13B4 means Tiny 2313 pin B4 LED.

### External clock source for CPU unit
All the chip (except Mega 328) can accept external Clock source for the CPU unit (of course chip has to be configured to use this extermal source).  These are exposed via **EXTCLK** suffix (Prefix is the chip name like 2313 or 84 etc).

### I2C connector
For Mega 328 a seperate connector (name **328-I2C** @ Left Mid) for I2C conenction in provided . Rest all AtTiny chips share the I2C bus pins with SPI pins (so they are available on those headers - inthis Avatar of board we do not use connector to program the chips but can be used that way as well).

### UART
Connector **RX-TX** Mid Left exposes Tx/Rx pin of Mega 328 while TX-RX2 exposes Tx/Rx line of 2313.

### SPI
SPI pins (MISO, MOSI, SCK) are exposed on headers with name H-<Chip>  e.g. H-TINY84 exposes SPI pins of Tiny 84 chip.
  
## Power
Board power source can be chosen by Jumper **SW-PWR** (middle of the board) to either power comign thru SPI connectors or from a JST header (Top Right). Please note that the 5V lines of all the H-<Chip> connectors (i.e.e PSI connectors) are interconnected. So if you use two ISP programmer at the same time,  connect 5V only from one of the Arduino ISP programmer.
  




