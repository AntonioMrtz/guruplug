# Boot from USB

setenv bootargs_console console=ttyS0,115200;
setenv bootcmd_usb 'usb start; ext2load usb 0:1 0x00800000 /uImage; ext2load usb 0:1 0x01100000 /uInitrd'
setenv bootcmd 'setenv bootargs ${bootargs_console}; run bootcmd_usb; bootm 0x00800000 0x01100000'
saveenv
