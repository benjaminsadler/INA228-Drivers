# INA228-Drivers
I present four simple, lightweight drivers for the INA228 power monitor chip from Texas Instruments.

I struggled to use the INA228 with linux -- TI does not offer linux drivers, and the only other solution I found was a package from Adafruit.  Unfortunately, Adafruit's drivers require several compatibility layers, e.g. circuit python on top of blinka on top of python all of which must be run in a special environment.  I found this very clunky.

These four drivers provide quick measurements of four different values (bus voltage, current, power, and die temp) with simple bash scripts.  They are easy to integrate into linux project without any compatibility layers or special python environments.

Each driver performs three basic functions: they query the INA228 using the 'i2ctransfer' function from the i2c-tools package, then repack the three bytes response into a single 24-bit variable, and finally they calibrate the rough float value into a physical measurement by multiplying by appropriate conversion factors.  The bit packing process and conversion factors were replicated from the Adafruit python package.

These drivers do not report measurement units; the implied units are:

  *ina228_vbus: volts
  *ina228_power: watts
  *ina228_current: milliamps
  *ina228_temp: degree Celsius
