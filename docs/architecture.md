# Firmware Architecture

## Overview

The firmware is a simple event-driven keypad scanner:
1. `setup()` initializes 12 LED GPIOs as outputs and sets them LOW.
2. `loop()` polls keypad input via `keypad.getKey()`.
3. A `switch` dispatches key actions to per-LED or grouped LED operations.
4. `delay(10)` provides a small poll interval/debounce window.

No Wi-Fi stack is used in the current logic.

## Source Layout

- `src/main.cpp`: original firmware logic (kept unchanged).
- `CMakeLists.txt`: scaffold for repository organization.
- `diagram.json`: hardware definition source from Wokwi input.
- `docs/wiring.md`: pinout + wiring reference.
- `docs/architecture.md`: this file.

## Module Notes

### Keypad handling

- Uses `Keypad.h` API with matrix definition:
  - 4 rows, 4 columns
  - `keys[][]` char map (`1..9,0,A..D,*,#`)
- Row/column pin arrays are explicitly defined and passed to `Keypad` constructor.

### LED control

- `ledPins[]` maps logical LED index to GPIO.
- Individual keys map to one LED each.
- Group keys execute `for` loops over fixed subranges.

## Assumptions and Constraints

- Source is Arduino-style C++ intended for RP2040-compatible Arduino core / Wokwi Arduino runtime.
- To keep behavior unchanged, no migration to raw Pico SDK GPIO APIs was performed.
- If a pure Pico SDK build is required later, preserve the same key-to-LED mapping and scan cadence.
