# Raspberry Pi Pico W Keypad-to-LED Controller

## Overview
This project targets the **Raspberry Pi Pico W (RP2040)** and maps key presses from a **4x4 membrane keypad** to 12 independent LEDs.

The core firmware logic is preserved exactly from the provided source. The repository has been organized for maintainability and handoff.

## Repository Structure

```text
.
├── CMakeLists.txt
├── include/
├── src/
│   └── main.cpp
└── docs/
    ├── architecture.md
    └── wiring.md
```

## Features
- 4x4 matrix keypad scanning using `Keypad.h`
- 12 GPIO-driven LEDs (8 numeric-group, 4 alpha-group)
- Group ON/OFF behavior:
  - `9` -> turn ON LEDs 1..8
  - `0` -> turn OFF LEDs 1..8
  - `*` -> turn ON LEDs A..D
  - `#` -> turn OFF LEDs A..D
- Individual key mapping for `1..8`, `A..D`

## GPIO Assignment Summary
- **Keypad rows:** GP26, GP22, GP21, GP20
- **Keypad columns:** GP19, GP18, GP17, GP16
- **LED outputs:** GP11, GP10, GP9, GP8, GP7, GP6, GP5, GP4, GP3, GP2, GP28, GP27

For full mapping, see `docs/wiring.md`.

## Build / Flash Options

### Option A: Wokwi (fast simulation)
1. Create a new **Raspberry Pi Pico / Pico W** project in Wokwi.
2. Paste the provided `diagram.json` into the Wokwi diagram editor.
3. Use `src/main.cpp` as the firmware logic (or equivalent Arduino sketch runtime).
4. Start simulation and use the keypad to validate LED behavior.

### Option B: Real hardware (Pico W)
1. Wire the circuit exactly as documented in `docs/wiring.md`.
2. Ensure each LED has a 220 ohm series resistor.
3. Provide common GND across Pico W, keypad, and LEDs.
4. Build firmware according to your runtime choice:
   - **Arduino-Pico toolchain** (recommended for this source as-is), or
   - **Pico SDK** with an adaptation layer for `Keypad.h` + Arduino-style GPIO APIs.

### Pico SDK Setup (if using SDK workflow)
```bash
sudo apt update
sudo apt install cmake gcc-arm-none-eabi build-essential
git clone https://github.com/raspberrypi/pico-sdk
export PICO_SDK_PATH=$PWD/pico-sdk
cmake -B build -S .
cmake --build build
```

## Wi-Fi Note
Although the target board is **Pico W**, this firmware does **not** currently use Wi-Fi. No credentials are required or stored.

## Safety / Assumptions
- Some keypad row lines include external pull-up resistors (1k to 3V3) in the provided diagram.
- Logic is untouched; only repository layout and documentation were improved.
