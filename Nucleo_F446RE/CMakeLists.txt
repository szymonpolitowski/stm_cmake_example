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
    main.c
    Core/Startup/startup_stm32f446retx.s
    Core/Src/syscalls.c
    Core/Src/sysmem.c
)

add_executable(${PROJECT_NAME} ${PROJECT_SOURCES})

target_link_libraries (${PROJECT_NAME} PRIVATE STM32_Drivers)

add_custom_command(TARGET ${CMAKE_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_SIZE} $<TARGET_FILE:${CMAKE_PROJECT_NAME}>)






# add_executable(${PROJECT_NAME} main.c Core/Startup/startup_stm32f446retx.s)

# set (PROJECT_SOURCES
# 	# LIST SOURCE FILES HERE
# 	Startup/startup_stm32f446retx.s
# 	Sources/main.c
# 	Sources/syscalls.c
# 	Sources/sysmem.c


# 	)

# set (PROJECT_DEFINES
# 	# LIST COMPILER DEFINITIONS HERE

#     )

# set (PROJECT_INCLUDES
# 	# LIST INCLUDE DIRECTORIES HERE

#     )

############ MODIFY ACCORDING TO REQUIREMENTS) ########################

#######################################################################

################## PROJECT SETUP ######################################




# add_compile_definitions (${PROJECT_DEFINES})
# include_directories (${PROJECT_INCLUDES})


