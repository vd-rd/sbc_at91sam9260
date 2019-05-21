## Boot process
AT91SAM9 series processors depend on the state of the BMS pin for boot source selection When pulled down, it boots a NAND flash on the EBI bus. As NAND is expensive and takes a considerable area on the board, the boot strategy was devised relaying on the internal BootROM selected via a high signal on BMS pin and a small NVM memory attached to SPI0.

The U-Boot bootloader and a small Busybox are stored in the NVM. Instructions to build and tailor the U-Boot, Kernel and Busybox for this particular board are under development. 
U-Boot tries to load the kernel and rootfs from microSD if present, or falls back to the NVM environment otherwise.
