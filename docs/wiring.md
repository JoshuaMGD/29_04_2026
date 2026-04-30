# Wiring and GPIO Mapping (Raspberry Pi Pico W)

## Components (from `diagram.json`)
- 1x Raspberry Pi Pico / Pico W board
- 1x 4x4 membrane keypad
- 12x LEDs
  - 8x blue LEDs (numeric group: 1..8)
  - 4x red LEDs (alpha group: A..D)
- 12x 220 ohm resistors (LED current limiting)
- 4x 1k ohm resistors (keypad row pull-ups to 3V3)
- Jumper wires

## Keypad Connections
| Keypad Pin | Pico W GPIO |
|---|---|
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |

### Keypad Pull-up Network
In the provided Wokwi diagram, R1..R4 row lines are tied to 3V3 via four 1k resistors.

## LED Connections
All LED cathodes (`C`) connect to Pico GND.

| Logical LED | Key Label | Pico W GPIO | Series Resistor |
|---|---|---|---|
| LED1 | 1 | GP11 | 220 ohm |
| LED2 | 2 | GP10 | 220 ohm |
| LED3 | 3 | GP9 | 220 ohm |
| LED4 | 4 | GP8 | 220 ohm |
| LED5 | 5 | GP7 | 220 ohm |
| LED6 | 6 | GP6 | 220 ohm |
| LED7 | 7 | GP5 | 220 ohm |
| LED8 | 8 | GP4 | 220 ohm |
| LED9 | A | GP3 | 220 ohm |
| LED10 | B | GP2 | 220 ohm |
| LED11 | C | GP28 | 220 ohm |
| LED12 | D | GP27 | 220 ohm |

## Power and Ground
- Pico `3V3` feeds keypad pull-up resistor chain.
- Pico `GND` is common return for all 12 LEDs.

## Practical Real-Hardware Notes
- Keep wiring short on keypad lines to reduce noise.
- If key chatter appears, increase software debounce and/or validate pull-up strategy.
