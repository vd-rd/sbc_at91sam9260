# Boot process

## General considerations

The boot strategy is common for most of the AT91SAM9 series processors. After exiting RESET state, BMS pin is sampled for boot source selection[^1].

For the Glasnost MK2 board, NAND was not desired, due to space constraints. Instead, the board has a SPI NOR Flash, populated with a 32Mbit AT45DB321[^2] chip. On the board there is also a microSD connector for additional storage.

The proposed boot strategy for this board is implemented as follows:
![boot_process](/assets/boot_proc.png)

## Boot process

![bootloaders](/assets/bootloaders.png)

The boot process for this board involves 3 bootloaders that are chain-loaded and prepare the board for the next one. The order of execution is outlined in the diagram above. After exiting the reset state, the embedded BootRom (1st bootloader) looks for a valid sequence in the attached SPI flash. It proceedes to load AT91Bootstrap (SPL - 2nd bootloader) in the internal SRAM area. The SPL enables the SDRAM and loads U-Boot (TPL - 3rd bootloader) in the last MB of SDRAM. The TPL scans the available boot sources and loads the Linux Kernel.

### BOOTRom
The embedded BOOTRom is not user changeable. Its mode of operation and description is outlined in the datasheet. The only function it performs is to scan the SPI bus for a valid memory and load the executable in the 4KB internal SRAM area.

### AT91Bootstrap

The SPL(second program loader) is a project created by the former ATMEL (currently Microchip) engineers to provide a bootloader for the AT91 and ATSAMA line of chips. It's an open source project [hosted on GitHub](https://github.com/linux4sam/at91bootstrap). It has a wide range of features, such as loading U-Boot, directly the Linux Kernel, or preparing the CPU for JTAG debugging.
For the boards purposes, it sets up the clocks and SDRAM with appropriate timings and then loads the U-Boot binary form the SPI flash in the last MB of SDRAM. 
Special attention should be considered when configuring this bootloader, as SDRAM capacity and timings are static and depend on the parts populated on the board.

### U-Boot

For the AT91SAM chips, U-Boot is the TPL (third program loader). It is also an open source project [hosted on Gitlab](https://source.denx.de/u-boot/u-boot).

![UBootFlow](/assets/uboot-flow.png)

As outlined above, UBoot performs a number of tasks:
 - sets up SPI, MMC and Ethernet
 - reads the environment from FLASH
 - searches for an microSD card and loads linux from there if present
 - if SD is not available, looks for a TFTP  server to load an application
 - loads a recovery environment stored on SPI Flash if above steps are unsuccesful.

## Loading linux
TBD

## Loading recovery
TBD

## Tools and versions

At the time of writing this documents the following versions and tools were used:
 - AT91Bootstrap - v3.10.4 version from git 
 - U-Boot v2022.04 version
 - Linux Kernel - 5.17.5 version

Compilers:
 - GCC-ARM-none-EABI - v11.2
 - GCC-ARM-GNULINUXHF - v11.2

[^1]: BMS pin function and code relocation [AT91SAM9260 datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-6221-32-bit-ARM926EJ-S-Embedded-Microprocessor-SAM9260_Datasheet.pdf), section 6.1.1, page 20 
[^2]: Although [AT45DB321](https://www.dialog-semiconductor.com/sites/default/files/2021-04/DS-AT45DB321E-8784L-032019.pdf) was chosen, any member of the AT45 series can be used with capacities ranging from 4Mbit to 256Mbit
