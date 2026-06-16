# Step by Step — Intelligent Activity Tracker & Real-Time Blood Oxygen Monitor

**41070 Embedded Mechatronic Systems — Autumn 2026**  
University of Technology Sydney · Faculty of Engineering  
**Team:** Eva · Varun · Nischay · Nithish  

---

## Project Overview

Step by Step is a wearable health monitoring device built around an Arduino Nano shield PCB. The device tracks step count and pace in real time using an ADXL335 MEMS accelerometer, monitors blood oxygen saturation (SpO₂) and heart rate using a MAX30102 optical sensor, and displays all metrics live on an SSD1306 OLED display. A tri-colour LED array provides instant SpO₂ status feedback, and a single button drives a full navigable on-screen menu.

The system is powered by a dual-input power architecture accepting either a 12V DC barrel jack or a 9V rechargeable battery, regulated down through a LM2596S buck converter and dual AP2112K LDOs to provide stable 5V, 3.3V, and 1.8V rails across all subsystems.

---

## Hardware

| Subsystem | Key Components |
|---|---|
| Power | PJ-102A barrel jack, S2B-EH JST battery connector, PMEG3020DEP OR-ing diodes, LM2596S-5.0 buck converter, AP2112K-3.3 & AP2112K-1.8 LDOs |
| Motion Sensing | ADXL335 (analog, A0–A2), Sallen-Key LPF signal conditioning |
| Biometric Sensing | MAX30102EFD+ (I2C, 0x57), 1.8V core / 3.3V LED supply |
| Display | SSD1306 OLED 128×64 (I2C, 0x3C), SLW-104-01-F-S connector |
| Indicators | WP7113SYD yellow, WP7113SGD green, LTL-1CHEE red, LTST-C190KGKT orange — MOSFET-switched (2N7002LT1G) |
| MCU | Arduino Nano (ATmega328P) |
| Enclosure | 3D printed two-part enclosure, designed in SolidWorks |

The PCB is a 4-layer Arduino Nano shield designed in Altium Designer and fabricated by JLCPCB.

---

## Firmware

The embedded firmware runs on the Arduino Nano and provides:

- System initialisation (OLED, I2C, GPIO, LDO enable via D7/D8)
- MAX30102 SpO₂ and heart rate acquisition and calculation
- ADXL335 3-axis acceleration sampling, step detection (hysteresis threshold), pace calculation (moving average), and calorie estimation
- Navigable 4-screen OLED menu (Heart & SpO₂ · Step Count · Accelerometer · Settings) driven by a single debounced button (D4)
- Tri-colour SpO₂ LED feedback (D9/D10/D11): green ≥95%, orange 90–94%, red <90%
- MCU-controlled power rail switching to reduce idle current draw

---

## Repository Structure
