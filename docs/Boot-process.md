# Boot Process

1. Hardware setup when device is turned on.
2. U-Boot runs from NAND memory.
3. U-Boot initializes hardware.
4. U-Boot loads uImage and uInitrd. After that it passes control to the kernel.
5. Kernel contained in uImage mounts the filesystem with the information contained in uInitrd. Peripherals and memory are also set up in this part of the process.
6. Kernel inits the init process. It initializes the rest of the system.