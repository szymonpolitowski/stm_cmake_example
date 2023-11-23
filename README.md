# STM Cmake Example

Repozytorium z przykładowym wykorzystaniem Cmake z STM32.

Tworzenie szablonu przy pomocy STM32CubeIDE:
1. Utwórz nowy projekt: `File -> New -> STM32 Cmake Project`
2. Wybierz opcję: `Project from Cmake template`
3. Podaj nazwę projektu oraz wybierz Template: `Executable`
4. Wybierz właściwy MCU po czym kliknij Finish.

---

Przygotowanie plików projektowych: `cmake -S . -B build -G Ninja -DCMAKE_TOOLCHAIN_FILE="cubeide-gcc.cmake"`

Budowanie projektu: `ninja -C build`

