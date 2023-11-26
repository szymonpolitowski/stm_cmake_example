# STM Cmake Example

Repozytorium pokazujące proste budowanie projektu wykorzystującego HAL przy pomocy CMake oraz Ninja.

Wymagane są:
- CMake
- Ninja
- arm toolchain (gcc-arm-none-eabi)
- wygenerowany project w STM32CubeIDE przy pomocy generatora 

### Budowanie i kompilacja projektu

Przygotowanie plików do kompilacji: `cmake -S . -B build -G Ninja -DCMAKE_TOOLCHAIN_FILE="cmake/arm-gcc-toolchain.cmake"`

Kompilacja projektu: `ninja -C build`

### Instalacja wymaganych rozszerzeń (Linux)

- CMake: `sudo apt-get -y install cmake`
- Ninja: `sudo apt-get install ninja-build`
- Arm toolchain: `sudo apt install gcc-arm-none-eabi`
