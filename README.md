# INA228-Drivers
I present four simple, lightweight drivers for the INA228 power monitor chip from Texas Instruments.

I struggled to use the INA228 with linux -- TI does not offer linux drivers, and the only other solution I found was a package from Adafruit.  Unfortunately, Adafruit's drivers require several compatibility layers, e.g. circuit python on top of blinka on top of python all of which must be run in a special environment.  I found this very clunky.

These drivers provide quick measurements of four different values (bus voltage, current, power, and die temp) with simple bash scripts.  They are easy to integrate into a linux project without any compatibility layers or special python environments.

Each driver performs three basic functions: they query the INA228 using the 'i2ctransfer' function from the i2c-tools package, then repack the two or three-byte response into a single 16 or 24-bit variable, and finally they calibrate the rough float value into a physical measurement by multiplying by appropriate conversion factors.  The bit packing process and conversion factors were replicated from the Adafruit python package.

These drivers deliver their output to stout, and do not report measurement units nor append a newline at the end (of course, you may easily add these!).  The implied units are:

  1) ina228_vbus: volts
  2) ina228_power: watts
  3) ina228_current: milliamps
  4) ina228_temp: degree Celsius

The drivers are hard-coded to assume the INA228 is found at I2C address 0x40, but if the INA228 is configured for another I2C address you may change the standard address in line 3 of each driver.
