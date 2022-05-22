# Software loading

**Note: This page is still WIP**


After building the board a method to load software on it is desired with minimum external tools involved. Luckily AT91SAM9260 has an embedded bootloader that makes this process easy.

## Microchip SAM-BA
This tool communicates with the embedded bootloader and loads applets that help with flashing or debugging. The latest version that works with AT91SAM9260 is SAM-BA v2.18 and can be downloaded from the [Microchip website](https://www.microchip.com/en-us/development-tool/SAM-BA-In-system-Programmer).

If the board is connected via USB to the host computer without a valid SPL in the SPI Flash, the embedded bootloader will enable the USB port. SAM-BA can be used to connect to the board.

The AT45 DataFlash applet is of interest and should be executed to be able to load code on the flash memory.

The first step is to run **Enable DataFlash on CS0** that will test if DataFlash is present and correctly wired.

The second step is to run **Send boot file** that will ask to load the binary for AT91Bootstrap. 

The third step is to flash the U-Boot bootloader at 0x8000 offset. This leaves room between between AT91Bootstrap and U-Boot for the environment variables.
