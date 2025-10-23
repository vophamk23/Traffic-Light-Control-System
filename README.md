# 🚦 TRAFFIC LIGHT CONTROL SYSTEM (FSM-BASED)

## 📘 Overview
This project implements a **Traffic Light Control System** for a **2-way intersection**, designed using **Finite State Machine (FSM)** principles on an embedded platform (e.g., STM32, Arduino, or similar MCU).

The system operates in **four main modes**, supporting **automatic timing**, **manual duration adjustment**, and **real-time countdown display** using **7-segment LEDs**.

---

## 🧩 System Modes

| Mode | Name | Description |
|------|------|--------------|
| **MODE 1** | **Auto Operation** | Automatic light switching cycle for two roads |
| **MODE 2** | **RED Duration Adjustment** | Allows manual setting of red light duration |
| **MODE 3** | **AMBER Duration Adjustment** | Allows manual setting of amber light duration |
| **MODE 4** | **GREEN Duration Adjustment** | Allows manual setting of green light duration |

**Constraint:**

The system automatically maintains this relationship through intelligent adjustment logic.

---

## ⚙️ Features

- 🧠 **Finite State Machine (FSM)**-based design for predictable, modular behavior  
- 🎛 **Three buttons** for mode switching, modifying, and saving durations  
- 💡 **Six LEDs** (3 colors × 2 roads) for signal visualization  
- ⏱ **7-segment display** for countdown timer display  
- 🔄 **Automatic duration adjustment** to maintain logical constraints  
- ⚡ **100Hz update rate** for smooth timing and responsive input  
- 🧱 **Modular structure** with separated functions for FSM, LED handling, button logic, and timing control  

---

## 🖥 Hardware Setup

| Component | Description |
|------------|-------------|
| **MCU** | STM32 / Arduino / ATmega (configurable) |
| **Buttons** | 3 push buttons for MODE / MODIFY / SET |
| **LEDs** | 6 total (RED, AMBER, GREEN for each road) |
| **7-Segment Display** | 2 digits for countdown display |
| **Power Supply** | 5V DC regulated |

---

## 🧠 Finite State Machine (FSM) Design

### 🔹 Traffic Cycle (Auto Mode)
