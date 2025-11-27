# Motor Control Function Block – CODESYS | Structured Text Implementation

This project implements a modular motor control function block (FB_Motor) using Structured Text (IEC 61131-3) in CODESYS V3.5, simulating an automated door or gate system with state machine logic, fault handling, and safety interlocks. It is designed to demonstrate robust real-world automation principles including emergency stop priority, timer-based position control, and extensible fault diagnostics. This serves as a portfolio-ready component for scalable industrial applications.

## Project Purpose

The function block provides:
- State machine-driven motor control for opening and closing operations.
- Comprehensive safety features, including immediate E-Stop override and fault reset.
- Sensor integration for limit detection with TON/TOF timer fallbacks.
- Structured data types for status monitoring and diagnostics.

## System Overview

**Simulated Hardware:**
- Bidirectional motor with forward/reverse direction control.
- UpLimit and DownLimit sensors for position feedback.
- E-Stop input for safety shutdown.
- PLC: CODESYS Control Win (PC-based simulation).

**Core Functionality:**
- Transitions through states: Closed → Opening → Opened → Closing → Closed.
- Jam detection, power management, and alarm flagging.
- Fault codes for troubleshooting (e.g., 99 for E-Stop, 2 for Jam).

## Key Components

| Component       | Description                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `Motor_State`   | ENUM type defining states: Opening, Opened, Closing, Closed, Fault.         |
| `Motor_Status`  | STRUCT holding direction, state, sensors, alarms, fault codes, and outputs. |
| `FB_Motor`      | Main function block with inputs (Open, Close, E-Stop, ResetFault) and TON/TOF timers. |

## Usage Instructions

1. Declare an instance: `MotorInstance: FB_Motor;`.
2. Map inputs:  
   `MotorInstance.Open := xDoorOpenPB;`  
   `MotorInstance.Close := xDoorClosePB;`  
   `MotorInstance.E_Stop := xEStop;`  
   `MotorInstance.ResetFault := xResetPB;`.
3. Call the function block in your PLC program: `MotorInstance();`.
4. Monitor motor status via `MotorInstance.Status` for HMI or diagnostic purposes.

Test this function block in CODESYS simulation by toggling the input signals and observing state transitions and motor outputs.

## Future Enhancements

- PID integration for advanced speed control.
- HMI visualization for status display and manual override.
- Expanded fault diagnostics and logging capabilities.

