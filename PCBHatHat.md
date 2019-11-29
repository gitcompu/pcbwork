RaspBerry Pi Hat's Hat 

Important jumpers
  1) PWR-SW-5V (@ Left Bottom) - Choose 5V power supply source between Pi or Ext or FTDI
  2) SW-3VPWR  (@ Left  Top)   - Choose 3.3V supply source between Pi or LM1117 regu (LM1117 sources from 5V)
  3) SW-PD4 (@ Top Middle) - Routes pin PD4 of Mega 328 to CD4@MEGA-3DIGI-5V or Joystick or DHT11 (temperature sensor 1-wire proto)
  4) SW-HALL (@ Bottom Right) - Routes pin PA0 of Mega 328 to CA3@328-2A1D-5V or HALL Analog Sensor A1302 (Magnet sensor)
  5) SW-IR-RECV (@ Bottom right)- Routes pin PD5 of Mega 328 to CD5@MEGA-3DIGI-5V or TSOP-4838 (3-pin IR Receiver IC for remote)
  6) PB0-GP1 (@ Top Middle) - Connects PB0 Mega 328 pin to either 5G1 or 5G5 
  7) PB1-GP2 (@ Top Middle) - Connects PB1 Mega 328 pin to either 5G2 or 5G7
  

Do not power on board unless you have
  1) Choose right 5 V supply either from RPi or Ext or FTDI  by jumper PWR-SW-5V (@ Left Bottom)
  2) Choose right 3 V supply either from RPi or LM1117 regu  by SW-3VPWR (@ Left  Top)

Safe Power Settings 
  - when board connected to RPi via 14 pin header (@ Top Left)
     1) Both PWR-SW-5V and SW-3VPWR set to PI - Current drawn from both 3.3.V and 5V of Pi for respective circuitry
     2) PWR-SW-5V to PI and SW-3VPWR set to LM - Board draws all power from 5V supply of Pi

  - when board NOT connected to RPi 
     1) SW-3VPWR set to LM and PWR-SW-5V to either FTDI or EXT (depending upon where 5V supply is coming from)

Important
  1) When connected to Pi - Setting GPIO MI , 13 and 26 (depend upon which header you connect the board) to low to disable TX0104 (upper converter) putting it in Tri State. Setting these GPIO high will enable it. You can use this to protect both RPi and Mega 328 of both accidentally set corresponding pins as output (G1, G2, G3 and G4 correspond to RPi GPIO 17/5/21, 18/6/22 , 19/7/23, 20/8/24). Maybe if you ensure that MI, 13 and 26 are highly controlled upper part os safe.
  2) No protection like above is available for Lower Converter (I2C safe BiDir) - though SDL and SDA are safe as they both rely on pull down , but pins 3G5 (correspond to GPIO MO, 12 and 25) and 3G7 (correspond to RPi GPIO CLK, 16 and 27) .That is the reason jumpers PB0-GP1 and PB1-GP2 play role to avoid such situation. Please be sure that before using these jumpers,  corresponding pins not set output on side of both RPi and Mega 328. If you do not use these jumpers at all, lower converter is all safe.
  

Features 
  1) Can use FTDI to load code (via Tx/Rx line) if Mega 328 has been pre-loaded with bootloader 
  2) If powered from FTDI-5V ,maybe safe to remove the TX0104 and I2C safe BiDir BreakOuts (alternatively you can be careful with all jumper settings and setting pins )
  3) Be careful with setting jumpers . Know what you are doing.
  4) 5V Jumper either has to use RPi or Ext supply (when not using FTDI 5V) - Rght Bttm
  5) You can program using Arduino as ISP (but then do not connect FTDI)
  
