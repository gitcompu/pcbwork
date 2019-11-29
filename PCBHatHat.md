RaspBerry Pi Hat's Hat 

Important jumpers
  1) PWR-SW-5V (@ Left Bottom) - Choose 5V power supply source between Pi or Ext or FTDI
  2) SW-3VPWR  (@ Left  Top)   - Choose 3.3V supply source between Pi or LM1117 regu (LM1117 sources from 5V)
  3) SW-PD4 (@ Top Middle) - Routes pin PD4 of Mega 328 to CD4@MEGA-3DIGI-5V or Joystick or DHT11 (temperature sensor 1-wire proto)
  4) SW-HALL (@ Bottom Right) - Routes pin PA0 of Mega 328 to CA3@328-2A1D-5V or HALL Analog Sensor A1302 (Magnet sensor)
  5) SW-IR-RECV (@Bottom right)- Routes pin PD5 of Mega 328 to CD5@MEGA-3DIGI-5V or TSOP-4838 (3-pin IR Receiver IC for remote)

Do not power on board unless you have
  1) Choose right 5 V supply either from RPi or Ext or FTDI  by jumper PWR-SW-5V (@ Left Bottom)
  2) Choose right 3 V supply either from RPi or LM1117 regu  by SW-3VPWR (@ Left  Top)

Features 
  1) Can use FTDI if 328 has been loaded with bootloader (via Tx/Rx line)
  2) If powered from FTDI-5V remove the TX0104 and I2C safe BiDir BreakOuts (or choose LM1117 3V supply using SW-3VPWR jumper)
  3) Be careful with setting jumpers . Know what you are doing.
  4) 5V Jumper either has to use RPi or Ext supply (when not using FTDI 5V) - Rght Bttm
  5) You can program using Arduino as ISP (but then do not connect FTDI)
  
Power settings
  1) SW-3VPWR (top left) set to LM117 and  - Choose
