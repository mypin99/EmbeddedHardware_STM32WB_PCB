# Bluetooth-Enabled STM32WB Device

## Overview
This project is a **Bluetooth-enabled STM32WB** device designed using **STM32WB55CEU6**, 
A dual-coreArm Cortex-M4** microcontroller with **Bluetooth LE 5.4** and **802.15.4** support. 
The project includes a **schematic and PCB design**, incorporating RF components, oscillators, and power management features. The goal is to develop a functional hardware platform for wireless communication and embedded systems applications.
I developed both schematic and PCB in KICAD version 9.0 tool. 
(N/B I designed this PCB as a learning project to enhance my skills in schematic and PCB design, 
understand design rules, and deepen my knowledge in embedded systems, even though similar PCBs exist.)

## Microcontroller Used
**STM32WB55CEU6**
- Ultra-low power **dual-core Arm Cortex-M4 (64 MHz) & Cortex-M0+ (32 MHz)**
- **512 KB flash memory**
- **Bluetooth LE 5.4**, **802.15.4**, **USB**, **LCD support**, and **AES-256 encryption**
- Integrated **SMPS for power efficiency**

## Power Management
- **VDD (3.3V)**: Main supply for the microcontroller
- **VDDA**: Analog supply for ADC/DAC
- **VDDRF**: RF frontend power supply
- **VBAT**: Battery input (connected to VDD if not using a battery)
- **VDDUSB**: USB transceiver power supply
- **VDDSMPS**: Internal voltage regulator supply

### **Decoupling/BYPASS Capacitors**
- **100nF per power pin**
- **4.7µF for microcontroller and VDDSMPS**

## SMPS Configuration
- **Capacitor C2 (4.7µF)**
- **Two inductors in series**
  - **L1 = 10nH**
  - **L2 = 10µH**

## **Crystal Oscillators**
- **High-Speed External Crystal (HSE - 32 MHz)**: Provides precise system clock
- **Low-Speed External Crystal (LSE - 32.768 kHz)**: Used for real-time clock (RTC) applications

## **RF Section (Bluetooth & Wireless Communication)**
- **Impedance Matching Network**
  - Ensures maximum power transfer and signal integrity
  - **Components:** 2 capacitors (**0.8pF, 0.3pF**) & 1 inductor (**2.7nH**)
- **Low Pass Filter (DLF162500LT-5028A1)**: Suppresses unwanted harmonics
- **U.FL Connector**: Enables external antenna connection

## **Programming & Debugging Interface**
- **Boot Modes (BOOT0 pin)**
  1. Boot from user flash (normal operation)
  2. Boot from system memory (bootloader mode for firmware updates via USB/UART/I2C/SPI)
  3. Boot from embedded SRAM
- **NRST Pin**
  - Used for external reset (active low)
  - Connected to ST-Link/debugger
  - Includes a filtering capacitor
- **SWD (Serial Wire Debug)**
  - Used for firmware flashing & debugging
  - **Tag-Connect ARM SWD** interface used

## **USB & ESD Protection**
- **USB Connector**: Used for programming, data streaming and powering the device using VBUS.
- **ESD Protection (USBLC6-2SC6)**: Protects VBUS and differential data lines
- **CC1 & CC2**: **5.1kΩ pulldown resistors** for USB Type-C detection

## **Status Indicators & Communication Headers**
- **Power Indicator LED**: Indicates device power status
- **UART Header**: For serial communication debugging

## **Power Supply Design**
- **VBUS (5V from USB) powers the system**
- **Regulator converts 5V → 3.3V for MCU**

![image.alt](https://github.com/mypin99/EmbeddedHardware_STM32WB_PCB/blob/main/STM32WB%20Bluetooth%20Capable%20Schematic.png?raw=true)

## Possible Applications
Once assembled, this PCB can be used for:
1. **Wireless Sensor Node** – Collect and transmit data (e.g., temperature, humidity) via **Bluetooth Low Energy (BLE)**.
2. **BLE Gateway or Bridge** – Connect Bluetooth devices to **cloud or Wi-Fi networks**.
3. **Custom Embedded Systems Development** – Useful for **motor control, robotics, or IoT projects among other applications**.

## **Reference Documents**
- **Application Notes:**
  - [AN5165](https://www.st.com/resource/en/application_note/an5165-how-to-develop-rf-hardware-using-stm32wb-stmicroelectronics.pdf): STM32WB RF Hardware Design Guide
  - [AN2867](https://www.st.com/resource/en/application_note/cd00221665-stm32-microcontroller-oscillator-design-guide-stmicroelectronics.pdf): Oscillator Design Guide
  - [AN4989](https://www.st.com/resource/en/application_note/an4989-stm32-microcontroller-debug-toolbox-stmicroelectronics.pdf): Debug Toolbox
- **Datasheet:** [STM32WB55xx](https://www.st.com/resource/en/datasheet/stm32wb55ce.pdf)
