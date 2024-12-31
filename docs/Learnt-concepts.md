# Learnt Concepts

## U-Boot (Universal Boot)

An open-source bootloader that initializes the hardware and starts the operating system, commonly used with ARM devices. Located in the NAND memory of the GuruPlug, it can become corrupted if written to incorrectly. A bricked GuruPlug means the system cannot boot the OS or access the U-Boot shell, preventing users from interacting with the device.

## uImage

Contains the kernel image compatible with the U-Boot bootloader. It has a modified header that allow U-Boot to load it into memory.

## uInitrd

Temporary filesystem loaded in RAM for the U-Boot. Contains info for creating the real OS filesystem.


## NAND Memory

Non-volatile storage. Information is persisted when the device is turned off. in the GuruPlug it stores critical components such as the U-Boot, uImage and uInitrd.

## JTAG (Joint Test Action Group)

Hardware interface for interacting the with board

It can be used to:

* Debug embeded software
* Program internal memory
* Firmware updates


### Leds

* Power: indicates wheter JTAG is connected to power.
* RX: indicates if the JTAG is reading data from the target device.
* TX: indicates if the JTAG is transmiting data to the target device.


## UART (Universal Asynchronous Receiver/Transmitter) 

Hardware comunication protocol that consists of two wires: one for sending and one for recieving data.

## Terminal Emulator

A terminal emulator is a software application that replicates the functionality of a traditional computer terminal within a graphical environment.