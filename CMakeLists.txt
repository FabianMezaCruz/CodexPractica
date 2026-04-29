cmake_minimum_required(VERSION 3.13)

project(pico_w_keypad_led C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# NOTE:
# The current firmware in src/main.cpp is Arduino-style (setup/loop + Keypad.h).
# Keep this CMake file as repository scaffolding for Pico SDK projects.
# For direct builds, either:
#   1) use Arduino-Pico tooling (recommended for this exact source), or
#   2) port src/main.cpp to Pico SDK APIs.

add_custom_target(scaffold_only ALL
  COMMAND ${CMAKE_COMMAND} -E echo "Project scaffold generated. See README.md for build/flash options."
)
