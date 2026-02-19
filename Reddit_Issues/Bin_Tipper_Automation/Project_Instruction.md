#  Bin Tipper Automation – Simulated in CODESYS | Structured Text

This project implements a **fully automated bin tipping system** using **Structured Text (IEC 61131-3)** and simulated entirely in **CODESYS V3.5**. It recreates the behavior of an industrial bin handling line featuring 3 conveyors, a tipper, sensors, limit switches, and a bin counter.

The logic is written in Structured Text and tested using **CODESYS SoftPLC**, making it a safe, clean, and hardware-free way to learn and showcase PLC automation.

---

##  System Overview

**Goal:** Automate bin transport and tipping through a chain of conveyors and tipper motor control in a simulated environment.

###  Components:
- **3 Conveyors**: 
  - Conveyor 1 (Infeed)  
  - Conveyor 2 (Post-tip feeder)  
  - Conveyor 3 (Outfeed/ejection)  
- **1 Tipper**:
  - Controlled by forward & reverse outputs
- **6 Sensors**: 
  - Detect bin presence & tipper positions
- **2 Limit Switches**:
  - Detect forward and home tipper positions
- **1 Timer**:
  - Waits 4 seconds for tipping stability
- **1 Counter**:
  - Tracks how many bins are processed

---

##  Sequence Logic

1. **Bin enters Conveyor 1** → Detected by Sensor 1 → Start Conveyor 1 & increment bin counter
2. **Bin passes Sensor 2** → Start tipper conveyor
3. **Bin reaches Sensor 4** → Stop Conveyor 1 & Tipper Conveyor
4. **Tipper forward movement** until it hits Limit Switch 1
5. **Wait 4 seconds** at forward position
6. **Reverse tipper** until home position (Limit Switch 2)
7. **Start Conveyor 2** → Then Conveyor 3 when Sensor 5 is triggered
8. **When Sensor 6 is active**, stop Conveyor 3 and decrement bin counter
9. **Repeat cycle** if bins remain

---

##  Tools Used

- **CODESYS V3.5** for development and simulation
- **Structured Text (IEC 61131-3)** as the primary language
- **CODESYS SoftPLC** for runtime
- **Built-in Visualizations** (optional) for user control & simulation interface

---

##  Preview

> _Coming Soon_: Screenshots or GIFs showing the conveyor/tipper sequence in CODESYS simulation.

---

##  Author

 **Nathanael K Binu**  
 Automation Developer & Controls Enthusiast  
 [GitHub Portfolio](https://github.com/Kermitsmittle)

---

##  License

This project is open-source and available under the MIT License.

>  **NOTE:** This project is purely a simulation. No physical PLC hardware is required to run or test the logic.

---
