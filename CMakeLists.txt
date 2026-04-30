cmake_minimum_required(VERSION 3.13)

project(pico_w_keypad_led C CXX ASM)

# Pico SDK import (set PICO_SDK_PATH in your environment)
include(pico_sdk_import.cmake)

pico_sdk_init()

add_executable(pico_w_keypad_led
  src/main.cpp
)

target_include_directories(pico_w_keypad_led PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}/include
)

# NOTE:
# This source uses Arduino-style APIs (pinMode/digitalWrite/delay) and Keypad.h.
# Keep logic intact; provide adaptation layer/library when integrating with Pico SDK build.

target_link_libraries(pico_w_keypad_led
  pico_stdlib
)

pico_enable_stdio_usb(pico_w_keypad_led 1)
pico_enable_stdio_uart(pico_w_keypad_led 0)

pico_add_extra_outputs(pico_w_keypad_led)
