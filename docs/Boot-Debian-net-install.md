# Boot Debian net install

fatload usb 0:1 0x00800000 /uImage; 
fatload usb 0:1 0x01100000 /uInitrd; 
setenv bootargs console=ttyS0,115200n8 base-installer/initramfs-tools/driver-policy=most; 
bootm 0x00800000 0x01100000