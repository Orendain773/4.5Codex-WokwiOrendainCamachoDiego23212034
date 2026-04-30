# Firmware Architecture

## High-Level Flow
1. Initialize LED GPIO pins as outputs and force LOW at startup.
2. Poll keypad in the main loop.
3. If a key is detected, execute deterministic LED action via `switch`.
4. Delay 10 ms and repeat.

## Source Layout
- `src/main.cpp`
  - `keys[4][4]`: key matrix map
  - `ledPins[12]`: GPIO assignments for LEDs
  - `rowPins[4]`, `colPins[4]`: keypad scan pin assignments
  - `setup()`: one-time GPIO initialization
  - `loop()`: keypad read + action dispatch

## Key-to-Action Map
- `1..8`: turn ON one corresponding blue LED
- `9`: turn ON blue LED bank (1..8)
- `0`: turn OFF blue LED bank (1..8)
- `A..D`: turn ON one corresponding red LED
- `*`: turn ON red LED bank (A..D)
- `#`: turn OFF red LED bank (A..D)

## Behavior Preservation
The logic, key map, GPIO arrays, and per-key actions are kept semantically identical to the provided firmware.

## Portability Note
The provided code is Arduino-style C++. For Pico SDK-only C/C++, a keypad matrix scanner abstraction and GPIO wrappers would be needed. This repository keeps the original logic and documents the integration points rather than altering behavior.
