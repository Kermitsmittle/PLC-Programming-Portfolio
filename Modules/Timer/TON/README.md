# Timer_TON – CODESYS TON Delay Simulation

This project demonstrates the use of a **TON (ON-delay) timer** in **Structured Text** using **CODESYS V3.5**.

It’s a basic logic program where a **pushbutton triggers a fan** after a 5-second delay, simulating real-world ON-delay timing used in industrial control systems.

---

## How to Use

### Option 1: Project Archive

1. Download the file:  
   `Timer_TON.projectarchive`
2. Open CODESYS.
3. Go to **File → Open Project Archive** and select the file.
4. Hit **Login**, then **Download**, then **Run (F5)**.

### Option 2: Raw Project File

1. Download `Timer_TON.project3` and open it in CODESYS.
2. You may need to reassign the **Device**:
   - Right-click the device → **Update Device** to match your local runtime (e.g., CODESYS Control Win).
3. Login and download the program.
4. Run it and play with the HMI.

---

## What You’ll See

- A virtual **pushbutton** in the Visualization tab.
- When pressed, the **TON** timer starts counting.
- After 5 seconds, the **Fan output turns ON**.
- When released, the fan turns OFF immediately.