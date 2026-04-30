# Raspberry Pi Pico W Keypad-to-LED Controller

## Overview
This project runs on a **Raspberry Pi Pico W (RP2040)** and maps a **4x4 matrix keypad** to **12 discrete LEDs**.
Each key press turns on/off specific LEDs according to the original firmware behavior.

> Core behavior is preserved from the provided source code.

## Repository Structure
```text
.
├── CMakeLists.txt
├── README.md
├── include/
├── src/
│   └── main.cpp
└── docs/
    ├── architecture.md
    └── wiring.md
```

## Features
- 4x4 keypad scan via dedicated row/column GPIOs
- Individual LED control for keys `1..8`, `A..D`
- Group control:
  - `9`: turn ON LEDs 1..8
  - `0`: turn OFF LEDs 1..8
  - `*`: turn ON LEDs A..D
  - `#`: turn OFF LEDs A..D
- 10 ms loop delay for stable polling

## Components (from diagram.json)
- 1x Raspberry Pi Pico/Pico W
- 1x 4x4 membrane keypad
- 12x LEDs
  - 8 blue (labels 1..8)
  - 4 red (labels A..D)
- 12x 220Ω current-limiting resistors (LEDs)
- 4x 1kΩ resistors (keypad row pull-ups to 3.3V)
- Jumper wiring and shared ground

## GPIO Mapping
See [`docs/wiring.md`](docs/wiring.md) for full table.

## Build/Flash (Pico SDK style)
1. Install Pico SDK toolchain.
2. Set environment variable:
   ```bash
   export PICO_SDK_PATH=/path/to/pico-sdk
   ```
3. Configure and build:
   ```bash
   mkdir -p build && cd build
   cmake ..
   make -j
   ```
4. Hold `BOOTSEL`, connect Pico W over USB, copy generated `.uf2`.

## Run in Wokwi
1. Create a new Pico project in Wokwi.
2. Paste the provided `diagram.json` wiring.
3. Use firmware equivalent to `src/main.cpp` (or Arduino-mode equivalent as originally written).
4. Start simulation and press keypad keys.

## Real Hardware Notes
- Use **3.3V logic only**.
- Keep common GND between all LEDs/keypad and Pico W.
- Do not expose Wi-Fi credentials in source control (not used in current firmware).

