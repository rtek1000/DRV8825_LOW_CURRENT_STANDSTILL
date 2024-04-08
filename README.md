# DRV8825 Low Current StandStill
To avoid overheating the stepper motor

- Based on the operation of the TMC2209 driver, it is possible to reduce the stepper motor standby current using the DRV8825 driver. To do this, it is necessary to interact with the reference voltage that the potentiometer produces for the DRV8825. The TMC2209 driver is very attractive, but the DRV8825 is easier to find and cheaper.

- One possibility is to use a 2N7000 transistor, which works well in this case.

![img](https://raw.githubusercontent.com/rtek1000/DRV8825_LOW_CURRENT_STANDSTILL/main/DRV8825_1.png)

------

Hardware:

Released under CERN OHL 1.2: https://ohwr.org/cernohl
