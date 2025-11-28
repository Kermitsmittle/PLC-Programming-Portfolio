# Bin Tipper Automation - CODESYS | Structured Text Demo

This is a modular demo project simulating a fully automated bin handling and tipping system, built using Structured Text (IEC 61131-3) in CODESYS V3.5.

Originally conceived as a quick Reddit solution for a conveyor-sequencing question, it quickly revealed the hidden complexity of "simple" automation systems. This project has since evolved into a learning lab, a portfolio piece, and a step-by-step showcase of real-world PLC logic design.

## Project Purpose

To demonstrate:

- Structured Text logic
- Modular development with Function Blocks and STRUCTs
- Conveyor sequencing and bin flow control
- Timer-based delay coordination (TON/TOF)
- Potential for PID integration (bin spacing control)
- Scalable architecture for real-world automation systems

## Origin Story

"It started as a Reddit reply... I just wanted to help someone with 3 conveyors and a stepper motor.  
But the moment I dug in, I realized: this isn't just about moving bins—it's about thinking modular, timing logic, and anticipating real-world problems."

— Nathanael K. Binu (aka *Kermitsmittle*)

## System Overview

**Hardware Simulated:**

- 3 Conveyor Belts (Conveyor_1, Conveyor_2, Conveyor_3)
- 3 Sensors (one per conveyor)
- 1 Stepper Motor for the bin tipper
- PLC: CODESYS Control Win (PC-based simulation)

**System Functionality:**

- Bins travel via conveyors in sequence
- Sensors detect bin presence
- Time delays ensure spacing between bins
- Stepper motor triggers tipper when bin reaches final position
- (Optional) PID logic to maintain spacing between bins based on sensor feedback (upcoming module)

## Project Modules

| Component        | Status        | Description                                       |
|------------------|---------------|---------------------------------------------------|
| FB_Conveyor      | Done          | Controls individual conveyor logic with timing    |
| BinHandler       | In Progress   | Coordinates sensor signals and motor sequence     |
| StepperMotor_FB  | In Progress   | Controls tipper actuation with pulses/direction   |
| PID_SpacingCtrl  | Planned       | Adjusts conveyor speed to maintain bin spacing    |
| HMI_Interface    | Planned       | Visual interface for bin count and manual override |

Stay tuned for updates as this demo project continues evolving into a mini digital twin of a real-world bin handling system.
