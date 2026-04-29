# Wiring and GPIO Map (Raspberry Pi Pico W)

This project uses a **4x4 matrix keypad** to control **12 LEDs** on a Raspberry Pi Pico W.

## Components List (from `diagram.json` + provided design)

- 1x Raspberry Pi Pico / Pico W (target runtime: Pico W)
- 1x 4x4 membrane keypad
- 12x LEDs
  - 8x blue (numeric group)
  - 4x red (A/B/C/D group)
- 12x current-limiting resistors (220Ω, one per LED)
- 4x pull-up resistors (1kΩ) tied to keypad row lines
- Jumper wires and breadboard (for physical build)

## Keypad GPIO Mapping

| Keypad Pin | Pico W GPIO | Role |
|---|---:|---|
| C1 | GP19 | Column input/output scan line |
| C2 | GP18 | Column input/output scan line |
| C3 | GP17 | Column input/output scan line |
| C4 | GP16 | Column input/output scan line |
| R1 | GP26 | Row scan line |
| R2 | GP22 | Row scan line |
| R3 | GP21 | Row scan line |
| R4 | GP20 | Row scan line |

## LED GPIO Mapping

Firmware array order (`ledPins`) defines behavior:

| Logical LED | GPIO | Trigger key |
|---|---:|---|
| LED1 | GP11 | `1` |
| LED2 | GP10 | `2` |
| LED3 | GP9 | `3` |
| LED4 | GP8 | `4` |
| LED5 | GP7 | `5` |
| LED6 | GP6 | `6` |
| LED7 | GP5 | `7` |
| LED8 | GP4 | `8` |
| LED9 | GP3 | `A` |
| LED10 | GP2 | `B` |
| LED11 | GP28 | `C` |
| LED12 | GP27 | `D` |

Additional grouped actions:
- `9` turns ON LEDs 1..8
- `0` turns OFF LEDs 1..8
- `*` turns ON LEDs 9..12
- `#` turns OFF LEDs 9..12

## Power and Ground

- LED cathodes go to GND (common ground).
- Each LED anode is connected to a GPIO through a 220Ω resistor.
- Keypad row pull-ups (1kΩ network in the provided diagram) are tied to 3V3.

## Wokwi Notes

- The provided full design includes all 12 LEDs + resistors and the keypad.
- Serial monitor is wired on GP0/GP1 in the diagram; the current firmware does not print serial output.
