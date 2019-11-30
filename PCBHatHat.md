## RaspBerry Pi Hat's Hat 

### Conventions
  - **RPi** stands for Raspberry Pi
  - All jumpers have **SW** in their name (stand for Swich) - except PB0-GP1 , PB2-GP2 and RGB8_PI_TINY.
  - **+3** means 3.3 V
  - **+5** means +5V
  - Just  **+**  means either a 5V or 3.3V or some other positive voltage (more often it stands for +5V)
  - **G** as well as **GND** means ground.
  - **~** char means its a Analog signal
  - **DA** and **DL** stands for SDA and SDL I2C signal respectively (any number suffix/prefix is voltage level of the signal e.g. DA5 means 5V SDA signal).
  - **G1**, **G2** ... **G7** stands for the GPIO pins from RPi (depending upon which header among J1, J2 or J3 you connect the board). Any number prefix tells the volateg level (e.g. 5G3 is 5V level G3 signal).
  - **SHTKY** are Schotteky Diodes
  - Things starting with **R** are mostly Resistors
  - Things starting with **C** are mostly Capacitors
  

### Jumpers
Jumpers make the board highly configurable providing you more choice and control over Singal routing and Power supply.
  1) **PWR-SW-5V** (@ Left Bottom) - Choose 5V power supply source between 5V-RPi or EXT or FTDI
  2) **SW-3VPWR**  (@ Left  Top)   - Choose 3.3V supply source between Pi or LM1117 regu (LM1117 sources from 5V)
  3) **SW-PD4** (@ Top Middle) - Routes pin PD4 (T0/XCK) of Mega 328 to CD4@MEGA-3DIGI-5V or Joystick or DHT11 (Temperature/Humidity sensor 1-wire proto)
  4) **SW-HALL** (@ Bottom Right) - Routes pin PC1 (A1) of Mega 328 to CA3@328-2A1D-5V or HALL Analog Sensor A1302 (Magnet sensor)
  5) **SW-IR-RECV** (@ Bottom right)- Routes pin PD5 of Mega 328 to CD5@MEGA-3DIGI-5V or TSOP-4838 (3-pin IR Receiver IC for remote)
  6) **SW-LM35Z** (@ Top Right) - Connect Mega 328 pin PC0 (A0) to either connector pin CA2 or to LM35Z Analog temperature sensor.
  7) **PB0-GP1** (@ Top Middle) - Connects PB0 Mega 328 pin to either 5G1 or 5G5
  8) **PB1-GP2** (@ Top Middle) - Connects PB1 Mega 328 pin to either 5G2 or 5G7
  9) **RGB8_PI_TINY** - Route with PB2 of (Mega 328) or 5G1 to Data input of the circular RGB LED strip
In simple words Mega 328's A0 and A1 either connect to Analog sensors (LM35Z temperature or Magnet Hall respectively) or to the connector 328-2A1D-5V. Similarly PD4 connect either to DHT11or to Joystick or to connector MEGA-3DIGI-5V. While PD5 connect either to TSOP-4838 (IR Recv IC) or to connector MEGA-3DIGI-5V.

### Do not power on board unless you have
  1) Choosen right 5 V supply either from RPi or Ext or FTDI  by jumper PWR-SW-5V (@ Left Bottom)
  2) Choosen right 3 V supply either from RPi or LM1117 regu  by SW-3VPWR (@ Left  Top)

### Safe Power Settings 
  - when board connected to RPi via 14 pin header (@ Top Left)
     1) Both PWR-SW-5V and SW-3VPWR set to PI - Current drawn from both 3.3.V and 5V of Pi for respective circuitry
     2) PWR-SW-5V to PI and SW-3VPWR set to LM - Board draws all power from 5V supply of Pi (Note that LM1117 does not have Capcacitors on the input side - assuming path to RPi is so short that capcaitor on RPi side will be suffice)

  - when board NOT connected to RPi 
     1) SW-3VPWR set to LM and PWR-SW-5V to either FTDI or EXT (depending upon where 5V supply is coming from)

### Connectors
  - **14 pin PIHAT-HEADER** connects to RPiHat (one of the 3) or any other such board providing such header. Pins G1 to G7 are 7 GPIO pins from RPi routed (depending upon which connector you connect to). These are 3V in nature . Among them four (G1 to G4) are routed to TXB0104 while rwo (G5 and G7) are routed to I2C BiDir - both routing for conversion of 3V singnal to 5V (so e.g. 3G1 means 3V side of G1 while 5G1 means 5V side of the same signal). Pin G6 is connected to OE pin of TXB0104 (so putting OE as LOW makes TXB0104 to go into Tri State thus disabling the 3 V to 5 V conversion of signals - important protection feature - no such protection for I2C BiDir convertor as its just 4 MOSFET slapped with some resistors - not an IC - see Adafruit side for link to principalbehind the operation).
#### RPi and Mega 328 related
  - **GPIO-3V-2** - Exposes  3V side  of G1 to G4 (alongwith 3V supply and GND) 
  - **GPIO-5V-2** - Exposes  5V side of G1 to G4 (alongwith 5V supply and GND)
  - **3V-I2C/SPI-1** - Exposes 3V side of I2C (i.e SDA/SDL) , G5 and G7 (alongwith 3V supply and GND) (for expansion)
  - **3V-I2C/SPI-2** - Exposes 3V side of I2C (i.e SDA/SDL) , G5 and G7 (alongwith 3V supply and GND) (for expansion)
  - **5V-I2C/SPI-1** - Exposes 5V side of I2C (i.e SDA/SDL) , G5 and G7 (alongwith 5V supply and GND) (for expansion)
  - **5V-I2C/SPI-2** - Exposes 5V side of I2C (i.e SDA/SDL) , G5 and G7 (alongwith 5V supply and GND) (for expansion)
#### Mega 328 only
  - **INTR-IN** - Exposes Mega 328 PD2 (INT0) and PD3 (INT1/OC2B) alongwith 5V and GND
  - **328-2A1D-5V** - Exposes Mega 328 two Analog pins PC2 (A2), PC3(A3) (both subject to jumper setting) and one Digital pin PD7 alongwith 5V and GND
  - **MEGA-3DIGI-5V** - Exposes Mega 328 pins PD4 (T0/XCK) , PD5 (T1/OC0B) (both subject to jumper setting) and PD7 (AIN1) alongwith 5V and GND
  - **RX-TX** - Exposes Tx and Rx pin of Mega 328 (with 5V and GND)
  - **FTDI** - Meant to be used with FTDI breakout for booloader loaded Mega 328 but can be used for other purpose as it exposes Mega 328 RESET (subject to jumper) , Tx and Rx pin alongwith GND. It expects 5V supply to come from outside which can be routed to 5V supply of the board with jumper PWR-SW-5V set to FTDI side.
  - **PROG328** and **PROG328-2** - Exposes PB3 (MOSI/OC2A), PB4 (MISO) , PB5 (SCK) and PD0 (RESET) pin of Mega 328 with intention to be programmed by Arduino as ISP (though you can simply see it as exposre of these pins on a connector) alongwith 5V and GND.
  
### Important
  - When you have inserted **TXB0104** and **I2C BiDir** breakouts in the provided slots 
     1) When connected to Pi - Setting GPIO MI , 13 and 26 (depend upon which 14 pin header you connect the board) to low to disable **TX0104** (upper converter) putting it in Tri State. Setting these GPIO pins to high will enable it. You can use this to protect both **RPi** and **Mega 328** of both accidentally set corresponding pins as output (G1, G2, G3 and G4 correspond to RPi GPIO 17/5/21, 18/6/22 , 19/7/23, 20/8/24). Maybe if you ensure that MI (10), 13 and 26 are highly controlled so that upper convertor use is safe .
     2) No protection like above is available for Lower Converter (**I2C safe BiDir**) - though SDL and SDA are safe as they both rely on pull down , but pins 3G5 (correspond to GPIO MO, 12 and 25) and 3G7 (correspond to RPi GPIO CLK, 16 and 27) .That is the reason jumpers PB0-GP1 and PB1-GP2 play role to avoid such situation. Please be sure that before using these jumpers to connect 3G5 and/or 3G7,  corresponding pins not set output on side of both RPi and Mega 328. If you do not use these jumpers at all, lower converter is all safe.
  - When TXB0104 and I2C BiDir breakout are NOT inserted in the slots
     1) There can be no communication between RPi and Mega 328 .On positive side all cautions fromupper section are not applicable and you can be more relaxed :)
     

### Features 
  1) Can use FTDI to load code (via Tx/Rx line) if Mega 328 has been pre-loaded with bootloader 
  2) If powered from FTDI-5V ,maybe safe to remove the TX0104 and I2C safe BiDir BreakOuts (alternatively you can be careful with all jumper settings and setting pins )
  3) Be careful with setting jumpers . Know what you are doing.
  4) 5V Jumper either has to use RPi or Ext supply (when not using FTDI 5V) - Rght Bttm
  5) Connector PROG328 (as well PROG328-2 both @ Right Middle) expose MISO, MOSI, SCK and RST pin so that you can use Arduino as ISP to load code into Mega 328 (if Mega 328 already conntains a bootloader then even FTDI pin is enough to program via Tx/Rx pins).
  6) LCD-RPi1 (@ Left Bottom) connector is for refurbished B=Nikia 5110 LCD
  7) POT01 (@ Bottom Middle) controls the Brighness of the Nokia LCD
  8) XT header at left side of Mega 328 is to put optional 16MHz Crystal (or any other preferred freq) alingwith two capacitors. But if you choose to use internal 8LHz oscillagtor then these two pins PB7 and PB7 are free to use as two more I/Os.
  9) 3VIND and 5VIND headers are for optional LED (they already have resistor connected) to show status of power of 3V and 5V side correspondingly (if one of them is not glowing you may want to be careful).
  10) Preferred communication between RPi and Mega 328 be done with I2C as its safe (be careful when playing with RPi GPIO when TX0104 and I2C BiDir are inserted in respective slots 
  11) Connector pins CD6 and PD7 are directly connected to Mega 328 PD6 and PD7 pins (no jumpers to control it).
  12) Similarly Rx/Tx are also straight conncted to the connector pin (connector RX-TX @ Middle Right) with no control by any jumper (note that even FTDI connector also use same pins so do not use FTDI and RX-TX connector at same time - ubnless you know exactly what you are doing).
  13) Mega 328 pins INT0 and INT1 are exposed via connector INTR-IN (@ Right Middle) - you can use them as INT pins or normal I/O pins depending on your program.
  14) 

### Operating board at 3.3V
  - Note that its possible to make this board work at 3.3 V as well (choose EXT power then supply 3.3. V at the EXT Supply). However you have to work with following limitations
    1) LM1117 low dropout regulator may not function well and not able to generate 3.3 V (as minimun dropout for it is 1.2V). In such situation you have to set 3.3 V jumper to PI (that means board has to be connected to RPi). 
    2) Most of the sensors on board require 5V supply (else they do not work). Low voltage possibly may even damage the sensors.So do not set any jumpers to connect to Sensors (DHT11, A1302, LM35Z and TSOP-4838). 
    3) Do not connect Joystick at all.  
    4) Do not use FTDI or Arduino as ISP at all when operating board at 3 V.
    5) You cannot use 16 MHz external crystal (and have to opt for internal 8 MHz clock).
  
### Components
  - LM1117 3.3V Voltage regulator to be used is of 5V to 3.3V version (not adjustable voltage output) . Part number is LM1117T-3.3 (Tayda A-682) . This is fixed volatge output version.
  - 
