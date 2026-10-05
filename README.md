
---

# NODE IO BOARD

The **NODE IO BOARD** is an embedded hardware node featuring an **ESP32-C3** microcontroller, onboard environmental and motion sensors, USB-C power/data delivery, and external micro-SD card storage. It serves as a compact, all-in-one sensor node designed for IoT applications, environmental monitoring, and motion tracking.

---

## Technical Specifications

### 1. Main Controller

* **MCU:** ESP32-C3-MINI-1 / ESP32-C3-MINI-2 module (RISC-V single-core processor).


* **Auto-Flash/Reset Circuitry:** Dual NPN transistor circuit (DTR/RTS) for automatic bootloader entry and flashing over USB.


* **Tactile Switches:** Dedicated `RESET` and `BOOT` push buttons.



### 2. Power Supply

* **Power Input:** USB Type-C Receptacle (USB 2.0 interface) or external 5V input header (`J2`).


* **ESD Protection:** Dedicated ESD protection diodes (`ESD9B5.0ST5G`) across VBUS, D+, and D- lines.


* **Voltage Regulation:** Onboard **LD1117S33TR** LDO regulator stepping down 5V (VBUS) to 3.3V for MCU and sensor power rails.



### 3. USB to UART Bridge

* **Bridge IC:** **CP2102N** (QFN-28) USB-to-UART bridge controller.


* Communicates directly with the ESP32-C3 via `U0RXD` and `U0TXD` pins.



### 4. Onboard Sensors & Peripherals

* **Environmental Sensor:** **BME688** gas, temperature, pressure, and humidity sensor connected over I²C (`SCL`, `SDA`).


* **Inertial Measurement Unit (IMU):** **BMI323** 6-axis IMU connected via I²C (`SCL`, `SDA`) with dedicated interrupt lines (`BMI_INT1`, `BMI_INT2`).


* **MicroSD Card Slot:** SPI-driven SD card slot (`MEM2067`) connected via SPI lines (`SPI_CLK`, `MOSI`, `MISO`, `SPI_CS`) for local data logging.



---

## Block Diagram Overview

```text
               +-----------------------+
               |  USB-C / 5V Header    |
               +-----------+-----------+
                           |
            +--------------+--------------+
            |                             |
    +-------v-------+             +-------v-------+
    | 3.3V LDO      |             | CP2102N USB-  |
    | (LD1117S33)   |             | to-UART Bridge|
    +-------+-------+             +-------+-------+
            |                             |
            +--------------+--------------+
                           |
                 +---------v---------+
                 |    ESP32-C3       |
                 |  Microcontroller  |
                 +----+----+----+----+
                      |    |    |
       +--------------+    |    +---------------+
       | I2C               | SPI                | Interrupts / Controls
+------v-------+    +------v-------+    +-------v------+
|   BME688     |    |  MicroSD     |    | Boot & Reset |
| Env Sensor   |    | Card Slot    |    |   Buttons    |
+--------------+    +--------------+    +--------------+
|   BMI323     |
|  6-Axis IMU  |
+--------------+

```


## Project Design Files

This hardware project was designed in **KiCad 10.0**:

* `NODE IO BOARD.kicad_sch` — Schematic source file


* Hardware revision: **Rev 1.0**
