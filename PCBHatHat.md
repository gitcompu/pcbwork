## RaspBerry Pi Hat's Hat 

### Important jumpers
  1) PWR-SW-5V (@ Left Bottom) - Choose 5V power supply source between Pi or Ext or FTDI
  2) SW-3VPWR  (@ Left  Top)   - Choose 3.3V supply source between Pi or LM1117 regu (LM1117 sources from 5V)
  3) SW-PD4 (@ Top Middle) - Routes pin PD4 of Mega 328 to CD4@MEGA-3DIGI-5V or Joystick or DHT11 (temperature sensor 1-wire proto)
  4) SW-HALL (@ Bottom Right) - Routes pin PA0 of Mega 328 to CA3@328-2A1D-5V or HALL Analog Sensor A1302 (Magnet sensor)
  5) SW-IR-RECV (@ Bottom right)- Routes pin PD5 of Mega 328 to CD5@MEGA-3DIGI-5V or TSOP-4838 (3-pin IR Receiver IC for remote)
  6) SW-LM35Z (@ Top Right) - Connect Mega 328 pin A0 to either connector pin CA2 or to LM35Z Analog temperature sensor.
  7) PB0-GP1 (@ Top Middle) - Connects PB0 Mega 328 pin to either 5G1 or 5G5 
  8) PB1-GP2 (@ Top Middle) - Connects PB1 Mega 328 pin to either 5G2 or 5G7
  

### Do not power on board unless you have
  1) Choose right 5 V supply either from RPi or Ext or FTDI  by jumper PWR-SW-5V (@ Left Bottom)
  2) Choose right 3 V supply either from RPi or LM1117 regu  by SW-3VPWR (@ Left  Top)

### Safe Power Settings 
  - when board connected to RPi via 14 pin header (@ Top Left)
     1) Both PWR-SW-5V and SW-3VPWR set to PI - Current drawn from both 3.3.V and 5V of Pi for respective circuitry
     2) PWR-SW-5V to PI and SW-3VPWR set to LM - Board draws all power from 5V supply of Pi (NOte that LM1117 does not have Capcacitors at its input and output - so its supply may contain ripples and may effect the RPi - so use with caution)

  - when board NOT connected to RPi 
     1) SW-3VPWR set to LM and PWR-SW-5V to either FTDI or EXT (depending upon where 5V supply is coming from)

### Important
  - When you have inserted TXB0104 and I2C BiDir breakouts in the provided slots 
     1) When connected to Pi - Setting GPIO MI , 13 and 26 (depend upon which header you connect the board) to low to disable TX0104 (upper converter) putting it in Tri State. Setting these GPIO high will enable it. You can use this to protect both RPi and Mega 328 of both accidentally set corresponding pins as output (G1, G2, G3 and G4 correspond to RPi GPIO 17/5/21, 18/6/22 , 19/7/23, 20/8/24). Maybe if you ensure that MI, 13 and 26 are highly controlled upper part os safe.
     2) No protection like above is available for Lower Converter (I2C safe BiDir) - though SDL and SDA are safe as they both rely on pull down , but pins 3G5 (correspond to GPIO MO, 12 and 25) and 3G7 (correspond to RPi GPIO CLK, 16 and 27) .That is the reason jumpers PB0-GP1 and PB1-GP2 play role to avoid such situation. Please be sure that before using these jumpers,  corresponding pins not set output on side of both RPi and Mega 328. If you do not use these jumpers at all, lower converter is all safe.
  - When TXB0104 and I2C BiDir breakout are NOT inserted in the slots
     1) There can be no communication between RPi and Mega 328 .On positive side all cautions fromupper section are not applicable and you can be more relaxed :)
     

### Features 
  1) Can use FTDI to load code (via Tx/Rx line) if Mega 328 has been pre-loaded with bootloader 
  2) If powered from FTDI-5V ,maybe safe to remove the TX0104 and I2C safe BiDir BreakOuts (alternatively you can be careful with all jumper settings and setting pins )
  3) Be careful with setting jumpers . Know what you are doing.
  4) 5V Jumper either has to use RPi or Ext supply (when not using FTDI 5V) - Rght Bttm
  5) You can program using Arduino as ISP (but then do not connect FTDI)
  6) LCD-RPi1 (@ Left Bottom) connector is for refurbished B=Nikia 5110 LCD
  7) POT01 (@ Bottom Middle) controls the Brighness of the Nokia LCD
  8) XT header at left side of Mega 328 is to put optional 16MHz Crystal (or any other preferred freq) alingwith two capacitors. But if you choose to use internal 8LHz oscillagtor then these two pins PB7 and PB7 are free to use as two more I/Os.
  9) 3VIND and 5VIND headers are for optional LED (they already have resistor connected) to show status of power of 3V and 5V side correspondingly (if one of them is not glowing you may want to be careful).
  10) Preferred communication between RPi and Mega 328 be done with I2C as its safe (be careful when playing with RPi GPIO when TX0104 and I2C BiDir are inserted in respective slots 
  11) Connector pins CD6 and PD7 are directly connected to Mega 328 PD6 and PD7 pins (no jumpers to control it).
  12) Similarly Rx/Tx are also straight conncted to the connector pin (connector RX-TX @ Middle Right) with no control by any jumper (note that even FTDI connector also use same pins so do not use FTDI and RX-TX connector at same time - ubnless you know exactly what you are doing).
  13) Mega 328 pins INT0 and INT1 are exposed via connector INTR-IN (@ Right Middle) - you can use them as INT pins or normal I/O pins depending on your program.
  14) Connector PROG328 (as well PROG328-2 both @ Right Middle) expose MISO, MOSI, SCK and RST pin so that you can use Arduino as ISP to load code into Mega 328 (if Mega 328 already conntains a bootloader then even FTDI pin is enough to program via Tx/Rx pins).

### Operating board at 3.3V
  - Note that its possible to make this board work at 3.3 V as well (choose EXT power then supply 3.3. V at the EXT Supply) but problem is that LM1117 low dropout regulator may not fucntion well and not able to generate 3.3 V. In such situation you have to set 3.3 V jumper to PI. But most of the sensors on board require 5V supply so this may not work in practice. But all the sensors (except Joystick whose output directly connected to Mega pin A2/A3) are connected to Mega 328 via jumpers. So if you operate board on 3.3. volt do not route any sensor pins to Mega 328 via jumpers and do not connect JoyStick as well. At the same time do not use FTDI or Arduino as ISP at all . SO under these strict condition you can operate board at 3.3V.
  
  
