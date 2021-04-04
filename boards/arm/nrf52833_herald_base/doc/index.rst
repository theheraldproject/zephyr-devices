.. _nrf52833_herald_base_linkname:

[Board Name]
nrf52833_herald_base

Overview
********
The base (main board only) Herald project wearable and beacon board using the nRF52833 SOC.


.. figure:: board_name.png
   :width: 800px
   :align: center
   :alt: nRF52833 Herald Base

   nRF52833 Herald Base (Credit: The Herald Project)

Hardware
********
This board is based on an nRF52833 SOC via a [BC833M](https://www.fanstel.com/bc833) pre-qualified board.
The board includes an accelerometer, an ambient light sensor, and two multi colour LEDs.

The accelerometer is the primary user interface. Double tap combinations will change
the mode of the board, with the LEDs providing information on charge status (LED0) and
application/wearer status (LED1).

The board was designed for low cost (<$10 per board) Digital Contact Tracing (DCT)
applications but can be used for a wide variety of other purposes, including as an
eHealth wearable or fixed Bluetooth LE/Mesh beacon.

The board features a small ribbon connector that allows a 'lower' companion board
to be used for body worn sensors, such as a pulse rate and blood oximeter and
temperature sensors. We shall release this board design in future for Zephyr too.
You can use your own external board to add functionality to our base design.

The board design itself is available 
[in the Herald Hardware project](https://github.com/theheraldproject/herald-hardware/).
Those board designs are licensed under
the CERN Open Hardware License V2 - Permissive (CERN-OHL-V2-P). The software in
this repository is licensed under the Apache 2.0 license so it can be contributed
back to the Zephyr project.

Zephyr RTOS via the NRF Connect SDK is the primary development environment for
the Herald Project's wearables and beacons and so the board has full Zephyr compatibility.

Supported Features
==================
The following features are supported in Zephyr RTOS:-

- All [nRF52833](https://www.nordicsemi.com/Products/Low-power-short-range-wireless/nRF52833) capabilities supported by the [BC833M](https://www.fanstel.com/bc833)
- Two multi-coloured LEDs (APHF1608LSEEQBDZGKC via LED0, LED1)
- An accelerometer (ST Microelectronics LIS2DE12 via I2C0 on address 0011001b (0x19))
- An ambient light sensor supporting IR,R,G,B (Broadcom APDS-9250 via I2C0 on address TBD)
- A real time clock external to the BCM833 to allow for sleeping and timed awake for extremely low power operation (PCF85063A via I2C address TBD)
- USB-C connector for charging, USB Serial, and debugging (124018802112A)
- External 1MB flash (MX25R8035 via QSPI)

Some features not currently supported by Zephyr:-

- NFC connectivity

For a version with skin temperature (TMP1075) and pulse oximeter & HRM (MAX30102) in addition to the above
there will be a nrf52833-herald-health wearable board definition in future.

The board has a >500mAh battery and when the battery goes below 15% the board will sleep,
using the RTC to maintain date/time and enabling a flashing RED LED to indicate low battery.
At this point all Bluetooth/NFC and external IC capabilities will be disabled. The reason
for this is that accurate date and time being kept when remote to an external time source
is key for digital contact tracing applications. Doing this on the main battery removes
the need for an additional RTC battery which adds weight and cost.

Connections and IOs
===================

Standard nRF52833 interfaces that are supported:-

+-----------+------------+----------------------+
| Interface | Controller | Driver/Component     |
+===========+============+======================+
| ADC       | on-chip    | adc                  |
+-----------+------------+----------------------+
| CLOCK     | on-chip    | clock_control        |
+-----------+------------+----------------------+
| FLASH     | on-chip    | flash                |
+-----------+------------+----------------------+
| GPIO      | on-chip    | gpio                 |
+-----------+------------+----------------------+
| I2C(M)    | on-chip    | i2c                  |
+-----------+------------+----------------------+
| MPU       | on-chip    | arch/arm             |
+-----------+------------+----------------------+
| NVIC      | on-chip    | arch/arm             |
+-----------+------------+----------------------+
| PWM       | on-chip    | pwm                  |
+-----------+------------+----------------------+
| RADIO     | on-chip    | Bluetooth,           |
|           |            | ieee802154           |
+-----------+------------+----------------------+
| RTC       | on-chip    | system clock         |
+-----------+------------+----------------------+
| RTT       | Segger     | console              |
+-----------+------------+----------------------+
| SPI(M/S)  | on-chip    | spi                  |
+-----------+------------+----------------------+
| UART      | on-chip    | serial               |
+-----------+------------+----------------------+
| USB       | on-chip    | usb                  |
+-----------+------------+----------------------+
| WDT       | on-chip    | watchdog             |
+-----------+------------+----------------------+

Custom interfaces added by this board:-

+-----------+------------+----------------------+
| Interface | Controller | Driver/Component     |
+===========+============+======================+
| EXT RTC   | I2C        | system clock         |
+-----------+------------+----------------------+
| EXT I2C   | I2C        | i2c via i2c1         |
+-----------+------------+----------------------+

The External I2C is the ribbon connector designed for
interfacing to daughter boards providing power and I2C.

Connections and IOs
===================

LED
---

* LED1 (multi) = P0.13
* LED2 (multi) = P0.14

Programming and Debugging
*************************

Flashing
========
This board can be flashed using the same method as any nRF52833 based device.
See :ref:`build_an_application` and
:ref:`application_run` for more details on building and running.

Debugging
=========
This board supports serial logging through Zephyr's logging interface.
It also supports an external RTT JLink debugger via TBC connector.


References
**********
- LIS2DE12 Accelerometer Datasheet [PDF](https://www.st.com/resource/en/datasheet/lis2de12.pdf)
- Broadcom APDS-9250 Ambient light sensor [PDF](https://www.broadcom.com/products/optical-sensors/ambient-light-photo-sensors/apds-9250)

