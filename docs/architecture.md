# Firmware Architecture

## Overview
The application is a simple event-driven loop:
1. Initialize all LED GPIOs as outputs and force LOW.
2. Poll keypad for a pressed key.
3. If a valid key is detected, execute LED action mapped by a `switch` block.
4. Delay 10 ms and repeat.

## Source Layout
- `src/main.cpp`:
  - Pin arrays (`ledPins`, `rowPins`, `colPins`)
  - Key matrix map (`keys`)
  - `setup()` GPIO initialization
  - `loop()` keypad read + command dispatch

## Functional Behavior Map
- Numeric single-key actions:
  - `1..8`: turn ON corresponding LED index `0..7`
- Numeric group actions:
  - `9`: turn ON LED indexes `0..7`
  - `0`: turn OFF LED indexes `0..7`
- Alpha single-key actions:
  - `A..D`: turn ON LED indexes `8..11`
- Alpha group actions:
  - `*`: turn ON LED indexes `8..11`
  - `#`: turn OFF LED indexes `8..11`

## Non-functional Characteristics
- No persistent storage
- No network usage
- No interrupts; polling-only approach

## Portability Notes
The provided logic is Arduino-style C++ (`pinMode`, `digitalWrite`, `delay`, `Keypad.h`).
To compile under Pico SDK directly, add a compatibility/adaptation layer without changing behavior.
