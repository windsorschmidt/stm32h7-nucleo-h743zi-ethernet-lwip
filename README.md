# Nucleo-H743ZI + Ethernet + LwIP (without RTOS)

## About

* A Working (tested) example of **LwIP** stack usage (without RTOS).
* Adapted from https://github.com/MX-Master/STM32H7_Nucleo-H743ZI_Ethernet_LwIP
* CubeMX project modified to generate a **Makefile** instead of a SW4STM32 project.
* Requies GNU ARM toolchain and OpenOCD installed

## Build & Flash

* From a shell, run ```make flash-openocd```

## Testing

* Power up the **Nucleo-H743ZI** board (connect to USB port or use external 5V/3.3V)
* Build and flash firmware to the **STM32H743ZIT6** using **ST-LINK**
* Connect **Nucleo-H743ZI** board to your PC (or router) using **Ethernet** cable
* Setup **IP / network mask** for the PC as **192.168.1.XXX / 255.255.255.0** (XXX = 1-99 or 99-254)
* Open console/terminal window and use commad - **ping 192.168.1.100**

## Remarks

Pay attention to the code lines below. It will help you to understand how to configure **H7** for the correct **Ethernet/LwIP** work.

[STM32H743ZITx_FLASH.ld](/STM32H743ZITx_FLASH.ld):
- [#L35-L39](/STM32H743ZITx_FLASH.ld#L35-L39) : stack/heap size
- [#L134](/STM32H743ZITx_FLASH.ld#L134), [#L151](/STM32H743ZITx_FLASH.ld#L151), [#L162](/STM32H743ZITx_FLASH.ld#L162) : data/bss/heap location
- [#L166-L175](/STM32H743ZITx_FLASH.ld#L166-L175) : LwIP Rx/Tx data location

[main.c](/Src/main.c):
- [#L133-L141](/Src/main.c#L133-L141) : HAL_Delay() & MX_LWIP_Process() usage
- [#L237-L262](/Src/main.c#L237-L262) : MPU configuration

[ethernetif.c](/Src/ethernetif.c):
- [#L189](/Src/ethernetif.c#L189), [#L196](/Src/ethernetif.c#L196), [#L203](/Src/ethernetif.c#L203), [#L210](/Src/ethernetif.c#L210) : Ethernet GPIOs speed
