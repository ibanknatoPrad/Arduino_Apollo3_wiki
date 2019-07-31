The Apollo3 module has many hardware peripherals capable of generating software interrupts. In order to use these, a special function naming system is used to call the various ISRs (Interrupt Service Routines).

## Software Interrupts
For more information on how and when each peripheral-specific interrupt is called, have a look at the Apollo3 [datasheet](https://cdn.sparkfun.com/assets/d/a/7/c/d/Apollo3_Blue_MCU_Data_Sheet_v0_9_1.pdf) and the examples in the [Ambiq SDK](https://ambiqmicro.com/static/mcu/files/AmbiqSuite-Rel2.2.0_vVeIKav.zip).

Note: this does not include hardware interrupts. To use those, look at the interrupts example [here](../blob/master/libraries/Examples/examples/Example10_Interrupts/Example10_Interrupts.ino) and the official Arduino reference [here](https://www.arduino.cc/reference/en/language/functions/external-interrupts/attachinterrupt/).

The Apollo3 microcontroller's interrupts are mapped through the NVIC (Nested Vectored Interrupt Controller). See section 3.1 of the datasheet for more details. The following is a table of the specific peripheral interrupt, its IRQ number, and its ISR name.

| Peripheral Name | IRQ Number | ISR Name |
| -- | -- | -- |
| Brownout | 0 | am_brownout_isr |
| Watchdog | 1 | am_watchdog_isr |
| RTC | 2 | am_rtc_isr |
| Voltage Comparator | 3 | am_vcomp_isr |
| I2C/SPI Slave | 4 | am_ioslave_ios_isr |
| I2C/SPI Slave Register Address | 5 | am_ioslave_acc_isr |
| I2C/SPI Master 0 | 6 | am_iomaster0_isr |
| I2C/SPI Master 1 | 7 | am_iomaster1_isr |
| I2C/SPI Master 2 | 8 | am_iomaster2_isr |
| I2C/SPI Master 3 | 9 | am_iomaster3_isr |
| I2C/SPI Master 4 | 10 | am_iomaster4_isr |
| I2C/SPI Master 5 | 11 | am_iomaster5_isr |
| BLE | 12 | am_ble_isr |
| GPIO | 13 | am_gpio_isr |
| Counter/Timers | 14 | am_ctimer_isr |
| UART0 | 15 | am_uart_isr |
| UART1 | 16 | am_uart1_isr |
| SCARD | 17 | am_scard_isr |
| ADC | 18 | am_adc_isr |
| PDM | 19 | am_pdm_isr |
| MSPI | 20 | am_mspi_isr |
| Stimer Capture/Overflow | 22 | am_stimer_isr |
| Stimer Compare 0 | 23 | am_stimer_cmpr0_isr |
| Stimer Compare 1 | 24 | am_stimer_cmpr1_isr |
| Stimer Compare 2 | 25 | am_stimer_cmpr2_isr |
| Stimer Compare 3 | 26 | am_stimer_cmpr3_isr |
| Stimer Compare 4 | 27 | am_stimer_cmpr4_isr |
| Stimer Compare 5 | 28 | am_stimer_cmpr5_isr |
| Stimer Compare 6 | 29 | am_stimer_cmpr6_isr |
| Stimer Compare 7 | 30 | am_stimer_cmpr7_isr |
| Clock Control | 31 | am_clkgen_isr |

## Using Interrupts
To use any of the ISRs listed, make sure to prefix the function with `extern "C"` before the function declaration. For example:
```ino
extern "C" void am_pdm0_isr(void) {
    ...
}
```
Note: all variables used within an ISR should also be declared with the `volatile` keyword.

The names of all of the ISRs can be found in the startup_gcc.c files for each variant of Apollo3 board.
