# STM32 Ultrasonic Distance Measurement System

This repository contains an embedded C project developed for the **STM32 Nucleo-F446RE** development board. The project interfaces an **HC-SR04 Ultrasonic Sensor** to measure object distances and provides visual feedback using LEDs based on the calculated ranges.

---

##  Project Overview

The goal of this project is to implement a real-time distance tracking system using time-of-flight principles.
* **Trigger Pulse:** A GPIO output pin generates a 10 µs pulse to start the ultrasonic burst.
* **Echo Signal:** A General Purpose Timer (GPT) captures the duration ($\Delta t$) of the returning echo signal.
* **Visual Output:** Onboard/External LEDs change states to classify object distance ranges.

### The Physics Behind It
The distance is computed using the standard speed of sound formula:

$$d = \frac{v \times \Delta t}{2}$$

Where:
* $v$ = Speed of sound in air ($\approx 343 \text{ m/s}$ or $0.0343 \text{ cm/\mu s}$)
* $\Delta t$ = Round-trip time of flight captured by the microcontroller timer

---

##  Hardware Requirements

* **Development Board:** STM32 Nucleo-F446RE (ARM Cortex-M4)
* **Sensor:** HC-SR04 Ultrasonic Distance Sensor
* **Indicators:** Onboard LED (`PA5`) / External LED array
* **Peripherals:** User Push Button (`PC13`), Jumper wires, and a breadboard
* **Connectivity:** USB Type-A to Mini-B cable

---

##  Hardware & Peripheral Configuration

The system is initialized using **STM32CubeMX** with the following pin mapping:

| Peripheral / Component | MCU Pin | Configuration Mode | Notes |
| :--- | :--- | :--- | :--- |
| **HC-SR04 TRIG** | `PA9` | GPIO Output | Generates the 10 µs start pulse |
| **HC-SR04 ECHO** | `PA9` / Timer Input | Input Capture / GPIO Input | Measures echo pulse width |
| **User LED (LD2)** | `PA5` | GPIO Output (Push-Pull) | Range classification indicator |
| **Push Button (B1)** | `PC13` | GPIO Input | User interaction |
| **USART2 (Tx/Rx)** | `PA2` / `PA3` | Asynchronous Mode | For debugging and data logging |

### Clock & Timer Settings
* **System Clock:** Configured via internal oscillator (`RCC` Bypass mode) to run at its maximum stability limit of **84 MHz**.
* **Timer (TIM4):** Configured with an internal clock source and a prescaler value of `84-1`. This steps down the frequency so that the timer ticks exactly every **1 µs**, allowing for precise time-of-flight measurements.

---

##  Software & Tools Used

* **STM32CubeMX:** For graphical clock tree setup, pinout assignment, and peripheral initializations.
* **STM32CubeIDE:** For writing code, compiling the binary/hex binaries, and real-time debugging using the ST-LINK interface.

---

## Getting Started

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
