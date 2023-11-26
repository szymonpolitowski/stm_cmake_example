# STM Cmake Example

Repozytorium przedstawia proste budowanie projektu wykorzystującego HAL przy pomocy CMake oraz Ninja.

Wymagane są:

- CMake
- Ninja
- arm toolchain (gcc-arm-none-eabi)
- wygenerowany project w STM32CubeIDE przy pomocy generatora

## Budowanie i kompilacja projektu

Przygotowanie plików:

```shell
cmake -S . -B build -G Ninja -DCMAKE_TOOLCHAIN_FILE="cmake/arm-gcc-toolchain.cmake"
```

Kompilacja projektu:

```shell
ninja -C build
```

## Instalacja wymaganych rozszerzeń (Linux)

CMake:

```shell
sudo apt-get -y install cmake
```

Ninja:

```shell
sudo apt-get install ninja-build
```

toolchain:

```shell
sudo apt install gcc-arm-none-eabi
```
