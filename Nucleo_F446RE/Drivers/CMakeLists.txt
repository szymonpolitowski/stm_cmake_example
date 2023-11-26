
set (HAL_DRIVER_DIR ${CMAKE_CURRENT_SOURCE_DIR}/STM32F4xx_HAL_Driver)
set (CMSIS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/CMSIS)

add_library (STM32_Drivers 
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_dma.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_exti.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_flash_ex.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_gpio.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_pwr_ex.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_rcc_ex.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_tim_ex.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_cortex.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_dma_ex.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_flash.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_flash_ramfunc.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_pwr.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_rcc.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_tim.c
    ${HAL_DRIVER_DIR}/Src/stm32f4xx_hal_uart.c
)

target_compile_definitions (STM32_Drivers PRIVATE USE_HAL_DRIVER=1)
target_include_directories (STM32_Drivers PUBLIC 
    # project
    ${CMAKE_SOURCE_DIR}/Core/Inc
    
    # CMSIS
    ${CMSIS_DIR}/Include
    ${CMSIS_DIR}/Device/ST/STM32F4xx/Include
    
    # HAL
    ${HAL_DRIVER_DIR}/Inc
    ${HAL_DRIVER_DIR}/Inc/Legacy
)
