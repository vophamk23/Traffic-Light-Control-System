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

| State | Road 1 | Road 2 |
|--------|--------|--------|
| RED_GREEN | 🔴 RED | 🟢 GREEN |
| RED_AMBER | 🔴 RED | 🟠 AMBER |
| GREEN_RED | 🟢 GREEN | 🔴 RED |
| AMBER_RED | 🟠 AMBER | 🔴 RED |

🧾 **Timing Example:**  
If RED = 5s, AMBER = 2s, GREEN = 3s → full cycle = 10s total.

---

## 🔄 Mode Transition Diagram

👉 *(Insert image of the mode transition diagram here)*

> 🖼 **Image placeholder:**  
> `![Mode Transition Diagram](images/mode_transition.png)`  
> *(Place your diagram image in `/images/mode_transition.png`)*

---

## ⚖️ Auto Duration Adjustment Logic

The **auto_adjust_duration()** function ensures that timing values remain valid and consistent.

| Modified Light | Strategy |
|----------------|-----------|
| **RED (0)** | Keep AMBER, calculate GREEN = RED − AMBER |
| **AMBER (1)** | Set GREEN = AMBER + 4, RED = GREEN + AMBER |
| **GREEN (2)** | Keep AMBER, calculate RED = GREEN + AMBER |

🧩 **Default Reset Values:**

---

## ⏱ Button Edge Detection

Edge detection ensures that **each button press triggers exactly one event**, even if the button is held.

| Time | Physical | prevState | currState | Detected | Action |
|------|-----------|------------|------------|-----------|---------|
| 0ms | OFF | RELEASE | RELEASE | - | - |
| 10ms | PRESS | RELEASE | PRESS | Rising ✓ | Process |
| 30ms | HOLD | PRESS | PRESS | - | Ignore |
| 50ms | RELEASE | PRESS | RELEASE | Falling | Ignore |

---

## 🧰 File Structure


---

## 🧩 Example Hardware Diagram

👉 *(Insert schematic or wiring diagram here)*  
> `![Hardware Diagram](images/hardware_diagram.png)`  

---

## 📸 Example Real Hardware

👉 *(Insert photo of the actual circuit here)*  
> `![Traffic Light Demo](images/traffic_demo.jpg)`  

---

## 🧪 Testing Procedure

1. **Power on the system** – All LEDs off → initialization  
2. **Enter MODE 1 (Auto)** – Observe automatic switching cycle  
3. **Press MODE button** – Enter RED adjustment  
4. **Press MODIFY** – Increment duration (loops 1→99→1)  
5. **Press SET** – Save & return to Auto Mode  
6. **Repeat for AMBER and GREEN**  
7. **Observe countdown** on 7-segment during each state  

---

## ⚡ Timing and Update Cycle

- **Timer Interrupt Rate:** 10ms (100Hz)
- **FSM Update:** Every 1 second (based on internal counter)
- **Blink Cycle:** 0.25s ON + 0.25s OFF

---

## 📚 Future Improvements

- Add **EEPROM save/load** for duration values  
- Integrate **pedestrian crossing button**  
- Use **PWM dimming** for night-time brightness adjustment  
- Display **mode indicators** on 7-segment or LCD  

---

## 👨‍💻 Author & Acknowledgements

- **Project Author:** Võ Phạm  
- **Advisor:** Dr. Phạm Minh Tuấn  
- **Institution:** University of Danang – University of Science and Technology  
- **Course:** Microprocessor and Microcontroller Lab  

---

## 🏁 License

This project is distributed under the **MIT License** – you are free to use, modify, and distribute it with attribution.

---

> ✨ *“Designed with precision, timed by logic, and powered by FSM.”*


