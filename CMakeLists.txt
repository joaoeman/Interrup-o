# Generated CMake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.0)
set(toolchainVersion 13_3_Rel1)
set(picotoolVersion 2.1.0)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico_w CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(interrupt C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable
add_executable(interrupt interrupt.c matriz_leds.c)

pico_set_program_name(interrupt "interrupt")
pico_set_program_version(interrupt "0.1")

# Gerar cabeçalho para o código PIO
pico_generate_pio_header(interrupt ${CMAKE_CURRENT_LIST_DIR}/pio_matrix.pio)

# Habilitar saída via UART e USB
pico_enable_stdio_uart(interrupt 1)
pico_enable_stdio_usb(interrupt 1)

# Linkar bibliotecas
target_link_libraries(interrupt
    pico_stdlib
    hardware_pio
    hardware_clocks
)

# Incluir diretórios
target_include_directories(interrupt PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}
)

# Gerar arquivos extras (UF2, binário, etc.)
pico_add_extra_outputs(interrupt)


