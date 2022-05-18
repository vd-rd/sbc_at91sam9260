# AT91SAM9260 Glasnost SBC

![board_render](/assets/front.png)
## Description
The second installment in the embedded Linux hardware development learning exercise.
The board is an updated version of the previous [AT91RM9200_SBC](https://github.com/vd-rd/sbc_at91rm9200/).
Detailed documentation and resources can be found in the [docs](docs) and [resources](resources) folders.

Note: the CPU comes in two variants, 208 pin PQFP and 217 pin BGA. The PFQP version is pin compatible with AT91SAM9XE. The BGA version is compatible with the improved AT91SAM9G20 and has its own [board](https://github.com/vd-rd/sbc_at91sam9g20).

### Features
 * CPU - AT91SAM9260 processor (ARM926EJ @ 200MHz)
 * RAM - 1Gb SDRAM max ( 3V3 and 1V8 types supported)
 * NVM - AT45DB dataflash for U-boot
 * microSD card slot
 * microUSB client interface
 * USB host breakout
 * RMII interface for Ethernet
 * standard Apollo.IoT expansion header

### Resources
You can find all necesary information to build or evaluate the module here:
   - [View layout and schematic](https://cadlab.io/project/1695) 
   - [View 3D board render](https://a360.co/2PfLcwq)
   - [Fabrication files](https://github.com/vd-rd/sbc_at91sam9260/releases)

