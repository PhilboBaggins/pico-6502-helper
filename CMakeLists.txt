# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
#set(PICO_SDK_PATH "/path/to/Pico/pico-sdk")

set(PICO_BOARD pico CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

if (PICO_SDK_VERSION_STRING VERSION_LESS "1.4.0")
  message(FATAL_ERROR "Raspberry Pi Pico SDK version 1.3.0 (or later) required. Your version is ${PICO_SDK_VERSION_STRING}")
endif()

project(Pico6502Helper C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(Pico6502Helper Pico6502Helper.c)

pico_set_program_name(Pico6502Helper "Pico6502Helper")
pico_set_program_version(Pico6502Helper "0.1")

pico_enable_stdio_uart(Pico6502Helper 1)
pico_enable_stdio_usb(Pico6502Helper 0)

# Add the standard include files to the build
target_include_directories(Pico6502Helper PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}
  ${CMAKE_CURRENT_LIST_DIR}/.. # for our common lwipopts or any other standard includes, if required
)

# Add any libraries
target_link_libraries(Pico6502Helper
  pico_stdlib
  hardware_pio
  hardware_timer
  hardware_clocks
)

pico_add_extra_outputs(Pico6502Helper)
