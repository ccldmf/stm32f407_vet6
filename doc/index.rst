.. __f407vet6_board:

STM32 F407VET6 Development Board
####################################

Overview
********

The STM32 F407VET6 board features an ARM Cortex-M4 based STM32F407xx MCU
with a wide range of connectivity support and configurations. There are
multiple version of this board like ``stm32_f407vet6``.
Here are some highlights of the STM32F407_VET6 board:

- STM32 microcontroller in LQFP100 package
- Extension header for all LQFP100 I/Os for quick connection to prototyping
  board and easy probing
- Flexible board power supply:

       - USB VBUS or external source (3.3V, 5V)
       - Power management access point

- Three LEDs:

       - 3.3 V power on (LD0)
       - Three user LEDs: red (LD1), red (LD2), red (LD3) 

- Four push-buttons: RESET, K1, K2 and K3
- Mini-AB connector

.. image:: img/STM32F407VET6.jpg
     :width: 500px
     :align: center
     :height: 500px
     :alt: STM32_F407VET6

See also board descriptions at `STM32-base website`_,
`STM32F407VET6 board`_ and `MCUDev STM32F407VET6`_

.. warning:: The +5V pins on this board are directly connected to the +5V pin
	     of the USB connector. There is no protection in place. Do not
	     power this board through USB and an external power supply at
	     the same time.


Hardware
********

STM32F407_VET6 board provides the following hardware components:

- STM32F407_VET6 in LQFP100 package
- ARM |reg| 32-bit Cortex |reg| -M4 CPU with FPU
- 168 MHz max CPU frequency
- VDD from 1.8 V to 3.6 V
- 25MHz system crystal
- JTAG/SWD header
- 512 kB Flash
- 192+4 KB SRAM including 64-Kbyte of core coupled memory
- GPIO with external interrupt capability
- 3x12-bit ADC with 24 channels
- 2x12-bit D/A converters
- Advanced-control Timer (2)
- General Purpose Timers (12)
- Watchdog Timers (2)
- USART (3), UART (2)
- I2C (3)
- I2S (2)
- SPI (3)
- SDIO (1)
- CAN (2)
- USB 2.0 OTG FS with on-chip PHY
- USB 2.0 OTG HS/FS with dedicated DMA, on-chip full-speed PHY and ULPI
- 10/100 Ethernet MAC with dedicated DMA
- CRC calculation unit
- True random number generator
- DMA Controller
- Micro SD
- 1x 10/100 Ethernet MAC
- 1x 8 to 12-bit Parallel Camera interface
- Micro USB for power and comms
- 2x jumpers for bootloader selection
- 2x16 FMSC LCD Interface
- NRF24L01 socket

More information about STM32F407VET6 SOC can be found here:
       - `STM32F407VE on www.st.com`_

Supported Features
==================

The Zephyr stm32f407_vet6 board configuration supports the following hardware
features:

+-----------+------------+-------------------------------------+
| Interface | Controller | Driver/Component                    |
+===========+============+=====================================+
| NVIC      | on-chip    | nested vector interrupt controller  |
+-----------+------------+-------------------------------------+
| UART      | on-chip    | serial port-polling;                |
|           |            | serial port-interrupt               |
+-----------+------------+-------------------------------------+
| PINMUX    | on-chip    | pinmux                              |
+-----------+------------+-------------------------------------+
| GPIO      | on-chip    | gpio                                |
+-----------+------------+-------------------------------------+
| PWM       | on-chip    | pwm                                 |
+-----------+------------+-------------------------------------+
| USB       | on-chip    | usb                                 |
+-----------+------------+-------------------------------------+
| CAN       | on-chip    | CAN controller                      |
+-----------+------------+-------------------------------------+
| SPI       | on-chip    | spi                                 |
+-----------+------------+-------------------------------------+

.. note:: CAN feature requires CAN transceiver.
	  Zephyr default configuration uses CAN_2 exclusively, as
	  simultaneous use of CAN_1 and CAN_2 is not yet supported.

Other hardware features are not yet supported on Zephyr porting.

The default configuration can be found in the defconfig file:

	``boards/arm/stm32f407_vet6/stm32f407_vet6_defconfig``


Pin Mapping
===========

Default Zephyr Peripheral Mapping:
----------------------------------

.. rst-class:: rst-columns

- UART_1_TX : PB6
- UART_1_RX : PB7
- UART_2_TX : PA9
- UART_2_RX : PA10
- USER_PB : PA0
- USB DM : PA11
- USB DP : PA12
- CAN1_RX : PD0
- CAN1_TX : PD1
- CAN2_RX : PB12
- CAN2_TX : PB13
- SPI1 MISO : PA6
- SPI1 MOSI : PB5
- SPI1 SCK : PA3

System Clock
============

STM32F407_VET6 System Clock could be driven by internal or external oscillator,
as well as main PLL clock. By default System clock is driven by PLL clock
at 168MHz, driven by 25MHz high speed external clock.

Serial Port
===========

STM32F407_VET6 has up to 6 UARTs. The Zephyr console output is assigned to UART2.
Default settings are 115200 8N1.
Please note that ST-Link Virtual Com Port is not wired to chip serial port.
In order to enable console output you should use a serial cable and connect
it to UART2 pins (PA9/PA10).


Programming and Debugging
*************************

Applications for the ``stm32f407_vet6`` board configuration can be built and
flashed in the usual way (see :ref:`build_an_application` and
:ref:`application_run` for more details).

Flashing
========

STM32F407_VET6 board includes an ST-LINK/V2 embedded debug tool interface.
This interface is supported by the openocd version included in Zephyr SDK.

Flashing an application to STM32F407_VET6
---------------------------------------

Here is an example for the :ref:`blinky-sample` application.

Run a serial host program to connect with your board:

.. code-block:: console

   $ minicom -D /dev/ttyACM0

Build and flash the application:

.. zephyr-app-commands::
   :zephyr-app: samples/basic/blinky
   :board: stm32f407_vet6
   :goals: build flash

You should see user led "LD1" blinking.

Debugging
=========

You can debug an application in the usual way.  Here is an example for the
:ref:`hello_world` application.

.. zephyr-app-commands::
   :zephyr-app: samples/hello_world
   :board: stm32f407_vet6
   :maybe-skip-config:
   :goals: debug

.. _STM32-base website:
   https://stm32-base.org/boards/STM32F407VET6-STM32-F4VE-V2.0.html

.. _STM32F407VE on www.st.com:
   http://www.st.com/en/microcontrollers/stm32f407ve.html

.. _STM32F407VET6 black board:
   https://os.mbed.com/users/hudakz/code/STM32F407VET6_Hello/

.. _MCUDev Black STM32F407VET6:
   https://github.com/mcauser/BLACK_F407VE
