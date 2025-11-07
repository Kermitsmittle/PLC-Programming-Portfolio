# CODESYS Countdown Timer Display (Native TIME Formatting in Visualization)

This CODESYS project demonstrates a **clean, no-hacks-needed** way to display a timer countdown using the visualization’s built-in `%t[ss:ms]` format. Instead of manually converting TIME to STRING, we just let the visualization handle it—like a boss.

---

## What This Project Does

- Uses a **TOF (Timer Off-Delay)** block to handle cooldown timing.
- Calculates **remaining time** (`PT - ET`) using standard TIME arithmetic.
- Displays the remaining time via a **Text Field** using `%t[ss:ms]` formatting.
- Requires zero manual string conversion!

---

## Why I Built It

I needed a simple, readable countdown timer (e.g., `04:32`) inside the CODESYS visualization. Rather than mess around with `TO_STRING`, `TIME_TO_DINT`, and a sea of `CONCAT`s, I found that the **native visualization formatting** was far easier and cleaner.

---
