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
    - INA260 - Current, Voltage and Power meter (can plug into the I2C connector **328-I2C**
### Blink LEDs
The board also contain five LEDs which are connected to one or two pins (for 2313 there are two pins rest only 1 pin) of 4 Micro controllers. The name of LEDs is self evident to depict the chip name and pin e.g. T13B4 means Tiny 2313 pin B4 LED.

### External clock source for CPU unit
All the chip (except Mega 328) can accept external Clock source for the CPU unit (of course chip has to be configured to use this extermal source).  These are exposed via **EXTCLK** suffix (Prefix is the chip name like 2313 or 84 etc).

### I2C connector
For Mega 328 a two seperate connector (name **328-I2C** @ Left Mid and **328-I2C-2** on Top Left)  for I2C conenction is provided A9alongwith 5V and GND). Rest all AtTiny chips share the I2C bus pins with SPI pins (so they are available on those headers - in this Avatar of board we do not use connector to program the chips but can be used that way as well).

### UART
Connector **RX-TX** Mid Left exposes Tx/Rx pin of Mega 328 while TX-RX2 exposes Tx/Rx line of 2313.

### SPI
SPI pins (MISO, MOSI, SCK) are exposed on headers with name H-&lt;Chip&gt;  e.g. H-TINY84 exposes SPI pins of Tiny 84 chip.

### General connectors
  - **13GEN** connector (@ Bottom Middle) exposes the T0/T1/INT0/INT1 pins of Tiny 2313 uC.  T0 and T1 pins can act as input to the Timer0 and Timer1 of TINY2313 uC.
  - **OC1A/B** conenctor exposes PB1 (OC1A) and PB2 (OC1B) pins of Mega 328. These can be used ot generate various waveform using the timer circuits.
  
## Power
Board power source can be chosen by Jumper **SW-PWR** (middle of the board) to either power comign thru SPI connectors (MOSI/MISO/SCK) or from a JST header (Top Right). Please note that the 5V lines of all the H-&lt;Chip&gt; connectors (i.e. SPI connectors) are interconnected. So if you use two ISP programmer at the same time,  connect 5V only from one of the Arduino ISP programmer.

Note that 5V pin of both TX-RX and TX-RX2 headers feed into main 5V line of processor via Schotteky diode SHTKY1 and SHTKY2 (both @ Left Middle). So if you happen to load bootloader into uC 328 and 2313 , then try to connect some Rx/Tx connection from say FTDI or CP2104 or 2303 , then both interfaces are protected. Also output from SW-PWR feeds into V bus via Schotteky diode SHTKY3 (@ Middle of the board). If you are confident that youy will be careful with conectors, you can opt not to solder Schotteky diode and short the pins.

The power from JST connector need not be strictly 5V (can be between 4.5 to 5.5 V) but then do not connect to any other circuit via header (unless voltage level of two match).

## Peripherals
128x32 **OLED** I2C based monochrome LCD (from Adafruit)header at top middle .





