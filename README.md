# Pico W Keypad-to-LED Controller

A Raspberry Pi Pico W project that reads a 4x4 matrix keypad and controls 12 LEDs using fixed key mappings.

> This repository focuses on **clean structure and documentation** while preserving the provided firmware behavior.

## Repository Structure

```text
.
├── CMakeLists.txt
├── diagram.json
├── docs/
│   ├── architecture.md
│   └── wiring.md
├── include/
└── src/
    └── main.cpp
```

## Features

- 4x4 keypad input handling.
- 12 LED outputs mapped to numeric/alphanumeric keys.
- Group ON/OFF controls:
  - `9` / `0` for LEDs 1..8
  - `*` / `#` for LEDs 9..12
- Deterministic polling loop with 10ms delay.

## Hardware Summary

See full details in [docs/wiring.md](docs/wiring.md).

- Board: Raspberry Pi Pico W (RP2040)
- Input: 4x4 membrane keypad
- Outputs: 12 LEDs + 220Ω series resistors
- Pull-ups: 4x 1kΩ on keypad row lines

## Build and Flash Options

Because the provided code uses Arduino APIs (`setup`, `loop`, `digitalWrite`, `Keypad.h`), use one of the following:

### Option A (Recommended): Arduino / Wokwi-compatible flow

1. Open Wokwi and create/import a Pico project.
2. Use `src/main.cpp` as your firmware source.
3. Ensure the `Keypad` library is available in the environment.
4. Import wiring from the provided `diagram.json` (or recreate per `docs/wiring.md`).
5. Start simulation and press keypad keys.

### Option B: Port to pure Pico SDK (future)

- Keep the exact mapping and logic from `src/main.cpp`.
- Replace Arduino GPIO + Keypad calls with Pico SDK equivalents.
- Preserve behavior documented in `docs/architecture.md`.

## Running on Real Hardware (Pico W)

1. Wire components exactly as in [docs/wiring.md](docs/wiring.md).
2. Build firmware with a compatible toolchain (Arduino-Pico recommended for current source).
3. Flash UF2 to Pico W by holding **BOOTSEL** and mounting as USB mass storage.
4. Reset and verify keypad-to-LED responses.

## Wi-Fi/Credentials

- This firmware does **not** use Wi‑Fi.
- No credentials are required or stored.
- If Wi‑Fi is added later, keep credentials in a local ignored config file (e.g., `.env` or `secrets.h`) and never commit secrets.

## Behavior Reference

| Key | Action |
|---|---|
| `1..8` | Turn ON corresponding LED in numeric bank |
| `9` | Turn ON LEDs 1..8 |
| `0` | Turn OFF LEDs 1..8 |
| `A..D` | Turn ON corresponding LED in alpha bank |
| `*` | Turn ON LEDs 9..12 |
| `#` | Turn OFF LEDs 9..12 |

## Notes

- Core logic in `src/main.cpp` is preserved from the provided source.
- Repository organization and docs were added to improve maintainability.
