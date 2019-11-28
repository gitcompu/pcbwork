RaspBerry Pi Hat's Hat
Do not power on board unless you have
  1) Choose right 5 V supply either from RPi or Ext or FTDI (@ Right Bottom) by jumper PWR-SW-5V
  2) Choose right 3 V supply either from RPi or LM1117 regu (@ Right Bottom) by SW-3VPWR

Features 
  1) Can use FTDI if 328 has been loaded with bootloader (via Tx/Rx line)
  2) If powered from FTDI-5V remove the TX0104 and I2C safe BiDir BreakOuts (or choose LM1117 3V supply using SW-3VPWR jumper)
  3) Be careful with setting jumpers . Know what you are doing.
  4) 5V Jumper either has to use RPi or Ext supply (when not using FTDI 5V) - Rght Bttm
  5) You can program using Arduino as ISP (but then do not connect FTDI)
  
