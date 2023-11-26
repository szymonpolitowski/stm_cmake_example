# STM Cmake Example

Repozytorium zawiera prosty projekt wykorzystujący STM32 oraz system budowania CMake. Do kompilacji użyty jest Ninja. Projekt bazowy został wygenerowany w STM32CubeIDE oraz odpowiednio dostosowany pod użycie CMake.

Wymagane są:

- CMake
- Ninja
- arm toolchain (gcc-arm-none-eabi)

## Budowanie i kompilacja projektu

Setup:

```shell
cmake -S . -B build -G Ninja -DCMAKE_TOOLCHAIN_FILE="cmake/arm-gcc-toolchain.cmake"
```

Build:

```shell
ninja -C build
```

Program:

```shell
ninja -C build program
```

## Environmental variables (Windows example)

```text
C:\Program Files\ninja
C:\Program Files\CMake\bin
C:\Program Files\LLVM\bin
C:\Program Files\Arm GNU Toolchain arm-none-eabi\13.2 Rel1\bin
C:\ST\STM32CubeIDE_1.14.0\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.cubeprogrammer.win32_2.1.100.202311100844\tools\bin
C:\ST\STM32CubeIDE_1.14.0\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.gnu-tools-for-stm32.11.3.rel1.win32_1.1.100.202309141235\tools\bin
```

### Ninja

<https://github.com/ninja-build/ninja/releases>

### CMake

<https://cmake.org/download/>

### LLVM

<https://github.com/llvm/llvm-project>

### STM32 tools

<https://www.st.com/en/development-tools/stm32cubeide.html>

## Instalacja wymaganych rozszerzeń (Linux)

CMake:

```shell
sudo apt-get -y install cmake
```

Ninja:

```shell
sudo apt-get install ninja-build
```

Toolchain:

```shell
sudo apt install gcc-arm-none-eabi
```
