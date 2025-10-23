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
