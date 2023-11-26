cmake_minimum_required(VERSION 3.20)

set(CMAKE_TRY_COMPILE_TARGET_TYPE "STATIC_LIBRARY")

project(NUCLEO_F446RE)

add_executable(${PROJECT_NAME} main.c)
# add if the C compiler is not able to compile a simple test program before project()
# set(CMAKE_TRY_COMPILE_TARGET_TYPE "STATIC_LIBRARY")

