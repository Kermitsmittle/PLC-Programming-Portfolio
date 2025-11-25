# Basic Pushbutton Control Example
This Structured Text (ST) example demonstrates a fundamental PLC control pattern:
Using a single pushbutton (PB1) input to control a lamp (LAMP1) output.

## Description
When the pushbutton PB1 is pressed (logic HIGH), the output LAMP1 turns ON.
When PB1 is released (logic LOW), LAMP1 turns OFF.
This basic ON/OFF control is the foundation of many industrial control logic scenarios.

## Inputs
PB1 (BOOL): Digital input from a pushbutton, active HIGH when pressed.

## Outputs
LAMP1 (BOOL): Digital output controlling a lamp.

## Usage
-Deploy this program to your PLC or simulator.

-Press and release the pushbutton in the simulation or hardware.

-Verify that LAMP1 follows the state of PB1 instantly.

## Learning Objectives
- Understand basic digital input/output mapping in ST.

- Get familiar with simple variable declarations and program structure.

- Build confidence writing minimal, clear ST code for fundamental automation tasks.