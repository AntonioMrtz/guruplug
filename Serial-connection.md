# Connect to serial console using UART

Using the JTAG provided with the GuruPlug and a terminal emulator we can connect using the UART protocol. This will allow us to interact with the GuruPlug if we don't know the state of the device or the credentials to establish a ssh connection. 

## Install terminal emulator

```console
sudo apt install screen
```

## Connect JTAG to GuruPlug

## List serial devices connected

```console
ls /dev/tty*
```

The output will look like something this:


```console
...
/dev/tty63  /dev/ttyS13  /dev/ttyS21  /dev/ttyS3   /dev/ttyUSB0
/dev/tty15  /dev/tty23  /dev/tty31  /dev/tty4   /dev/tty48  /dev/tty56  /dev/tty7   /dev/ttyS14  /dev/ttyS22  /dev/ttyS30
```

If we have connected the GuruPlug using USB the serial device that we're searching for is `/dev/ttyUSBx`. If we're not sure about which serial device is GuruPlug we can plug and unplug to see which one disappears from the list.

## Terminal emulator connection

We select the serial device that represents our GuruPlug and the baud rate for the connection, the latter is the communication speed over serial channel.

```console
sudo screen /dev/ttyUSB0 115200
```

## Connect to GuruPlug terminal

Reboot GuruPlug and then we should have the emulated terminal connected. 

* Press enter for stopping autoboot.
* If enter was not pressed the boot will continue and you will get access to the Guruplay OS.

## Credentials

Default login credentials for GuruPlug OS (Based on Debian5) are:

* User: `root`
* Password: `nosoup4u`

## Related links

- https://101pro.wordpress.com/2013/02/25/connect-to-guru-using-jtag/
