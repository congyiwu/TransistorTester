This is is a build environment for firmware for my BSIDE ESR02 Pro from https://github.com/madires/Transistortester-Warehouse/.

Directory layout:
* `Transistortester-Warehouse`: upstream repo checked out as a submodule
* `src`: actual source code, configured for my BSIDE ESR02 Pro
* `ctester-VERSIONm.pdf`: manual

Steps for updating versions:
1. ```sh
   tar -xzvf Transistortester-Warehouse/Firmware/m-firmware/ComponentTester-CURR_VERSIONm.tgz
   tar -xzvf Transistortester-Warehouse/Firmware/m-firmware/ComponentTester-NEW_VERSIONm.tgz
   ```
2. 3-way merge `ComponentTester-CURR_VERSION`, `ComponentTester-NEW_VERSION`, and `src` to `src`
3. From "Chapter 8: Programming the Component Tester"
   ```sh
   make
   make upload # Wipes EEPROM settings
   ```
4. Press button to turn on
5. Double press button to enter menu
6. Press button until "Adjustment" is highlighted
7. Hold button to start

I have a USBasp programmer, the cable connector pinout looks like this.
See https://aaroneiche.com/2016/11/06/programming-avrs-using-a-usbasp-on-a-mac/
```
    ┌───┬───┐
VCC │   │   │ MOSI
    ├───┼───┤
    │   │   │
    ├───┼───╢║
    │   │   ║║ RST
    ├───┼───╢║
    │   │   │ SCK
    ├───┼───┤
GND │   │   │ MISO
    └───┴───┘
```

These are the corresponding pins on the J6 header on BSIDE ESR02 Pro.
See https://www.eevblog.com/forum/testgear/bside-esr02-pro-transistor-tester-(teardown-quick-test)/msg1868543/#msg1868543
```
   J6
  ┌───┐
V │ O │ VCC
  ├───┤
G │ O │ GND
  ├───┤
R │ O │ RST
  ├───┤
  │ O │ SCK
  ├───┤
  │ O │ MISO
  ├───┤
  │ O │ MOSI
  └───┘
```
