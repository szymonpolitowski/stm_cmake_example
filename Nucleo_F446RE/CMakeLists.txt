cmake_minimum_required (VERSION 3.20)
project (NUCLEO_F446RE)

# CMake specific
enable_language(ASM)

# Color output logs
if (${CMAKE_CXX_COMPILER_ID} STREQUAL "GNU")
    add_compile_options (-fdiagnostics-color=always)
endif ()

# Includes
include (cmake/constants.cmake)

# Project specific
set (LINKER_SCRIPT              "../STM32F446RETX_FLASH.ld")
set (MCPU                       ${MCPU_CORTEX_M4})
set (MFPU                       ${MFPU_FPV4_SP_D16})
set (MFLOAT_ABI                 "")
set (RUNTIME_LIBRARY            ${RUNTIME_LIBRARY_REDUCED_C})
set (RUNTIME_LIBRARY_SYSCALLS   ${RUNTIME_LIBRARY_SYSCALLS_MINIMAL})

set (CMAKE_EXECUTABLE_SUFFIX ".elf")
set (CMAKE_STATIC_LIBRARY_SUFFIX ".a")
set (CMAKE_C_FLAGS "${MCPU} -std=gnu11 ${MFPU} ${MFLOAT_ABI} ${RUNTIME_LIBRARY} -mthumb -Wall -Werror")
set (CMAKE_EXE_LINKER_FLAGS "-T${LINKER_SCRIPT} ${RUNTIME_LIBRARY_SYSCALLS} -Wl,-Map=test.map -Wl,--gc-sections -static -Wl,--start-group -lc -lm -Wl,--end-group")
set (CMAKE_ASM_FLAGS "${CMAKE_C_FLAGS} -x assembler-with-cpp")

# Project
add_compile_definitions (STM32F446xx=1)

add_subdirectory (Drivers)

set (PROJECT_SOURCES
    Core/Src/main.c
    Core/Startup/startup_stm32f446retx.s
    Core/Src/stm32f4xx_hal_msp.c
    Core/Src/stm32f4xx_it.c
    Core/Src/syscalls.c
    Core/Src/sysmem.c
    Core/Src/system_stm32f4xx.c
)

add_executable(${PROJECT_NAME} ${PROJECT_SOURCES})
target_link_libraries (${PROJECT_NAME} PRIVATE STM32_Drivers)
target_include_directories (${PROJECT_NAME} PRIVATE Core/Inc)

add_custom_command(TARGET ${CMAKE_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_SIZE} $<TARGET_FILE:${CMAKE_PROJECT_NAME}>)

# Flash
find_program (STM32_Programmer STM32_Programmer_CLI) 

message (STATUS "")
if (STM32_Programmer)
    message (STATUS "STM32 Programmer was found. You can flash board with 'program' target now.")
else ()
    message (STATUS "STM32 Programmer was not found!")
endif ()

add_custom_target (program COMMAND ${STM32_Programmer} --connect port=SWD --write $<TARGET_FILE:${PROJECT_NAME}> --verify -rst) # test
