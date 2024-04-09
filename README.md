# DRV8825 Low Current StandStill
To avoid overheating the stepper motor

- Based on the operation of the TMC2209 driver, it is possible to reduce the stepper motor standby current using the DRV8825 driver. To do this, it is necessary to interact with the reference voltage that the potentiometer produces for the DRV8825. The TMC2209 driver is very attractive, but the DRV8825 is easier to find and cheaper.

- One possibility is to use a 2N7000 transistor, which works well in this case.

- Regarding the software, it may be necessary to add time after deactivating the HOLD function, to avoid losing steps. For example, for the STEP command to automatically deactivate the HOLD function:
(Tested with PIC and MPLABX, that's why it has this '_Bool' instead of the Arduino 'bool')

```C++
void DRV8825_hold(void) {
    DRV_LOW_CURRENT_pin = 1;
}

_Bool DRV8825_step(void) {
    _Bool res = false;

    if (DRV8825_fault() == false) {
        if (DRV_LOW_CURRENT_pin == 1) {
            DRV_LOW_CURRENT_pin = 0;
            __delay_us(50);
        }

        _step = true;
        DRV8825_update();
        _step = false;
        DRV8825_update();

        res = true;
    }

    return res;
}
```

![img](https://raw.githubusercontent.com/rtek1000/DRV8825_LOW_CURRENT_STANDSTILL/main/DRV8825_1.png)


![img](https://raw.githubusercontent.com/rtek1000/DRV8825_LOW_CURRENT_STANDSTILL/main/DRV8825.png)

-----

- To have greater control over the DRV8825, it is interesting to remove the resistor that connects the SLEEP pin to the FAULT pin. And there is also a resistor on the FAULT pin (maybe because many people are confusing the way of use and think that this FAULT pin must be powered with 5V. The resistor (R4 1.5k) on the FAULT pin may prevent the voltage value from reaching GND, and the microcontroller may not be able to understand the signal.

![img](https://raw.githubusercontent.com/rtek1000/DRV8825_LOW_CURRENT_STANDSTILL/main/DRV8825_board_schematic.jpg)

![img](https://raw.githubusercontent.com/rtek1000/DRV8825_LOW_CURRENT_STANDSTILL/main/DOH.jpg)


------

- Another thing is about the driver adjustment current. It is not necessary to adjust the driver to the maximum motor current, as some users teach on the Internet. The current can be much lower as long as steps are not being lost. Carry out tests before making it definitive. For example, in my application, a 1.6A (1600mA) motor worked very well with just 700mA.

------

Hardware:

Released under CERN OHL 1.2: https://ohwr.org/cernohl
