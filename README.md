# DRV8825 Low Current StandStill
To avoid overheating the stepper motor

- Based on the operation of the TMC2209 driver, it is possible to reduce the stepper motor standby current using the DRV8825 driver. To do this, it is necessary to interact with the reference voltage that the potentiometer produces for the DRV8825. The TMC2209 driver is very attractive, but the DRV8825 is easier to find and cheaper.

- One possibility is to use a 2N7000 transistor, which works well in this case.

- To have greater control over the DRV8825, it is interesting to remove the resistor that connects the SLEEP pin to the FAULT pin. And there is also a resistor on the FAULT pin (maybe because many people are confusing the way of use and think that this FAULT pin must be powered with 5V. The resistor on the FAULT pin may prevent the voltage value from reaching GND, and the microcontroller may not be able to understand the signal.

![img](https://raw.githubusercontent.com/rtek1000/DRV8825_LOW_CURRENT_STANDSTILL/main/DRV8825_1.png)


![img](https://raw.githubusercontent.com/rtek1000/DRV8825_LOW_CURRENT_STANDSTILL/main/DRV8825.png)

![img](https://raw.githubusercontent.com/rtek1000/DRV8825_LOW_CURRENT_STANDSTILL/main/DRV8825_board_schematic.jpg)

------

Hardware:

Released under CERN OHL 1.2: https://ohwr.org/cernohl
