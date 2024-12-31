# Unbrick bootloader

In this section, we will cover how to recover a bricked GuruPlug that cannot be accessed due to a broken [U-Boot bootloader]( https://en.wikipedia.org/wiki/Das_U-Boot). The recovery process involves connecting via JTAG and booting the GuruPlug to load a new U-Boot bootloader using the serial port. Once the boot process is stopped, we will access the U-Boot shell.


## Unbricking

### Set up

Download the latest U-Boot bootloader for the GuruPlug:

```console
wget [http://ftp.debian.org/debian/dists/bullseye/main/installer-armel/current/images/kirkwood/u-boot/GuruPlug/u-boot.kwb](http://ftp.debian.org/debian/dists/bullseye/main/installer-armel/current/images/kirkwood/u-boot/GuruPlug/u-boot.kwb)
```

We must also download the `kwboot` recovery utility. Here is how to do it in Debian systems:

```console
sudo apt install u-boot-tools
```


### Loading U-Boot from other device

First, make sure all connections to the GuruPlug are closed and that the device starts from a turned-off state. Then we connect JTAG between the GuruPlug and our device. After that we run this command that loads our `U-Boot` into the GuruPlug NAND memory:


```console
kwboot -t -B 115200 /dev/ttyUSB0 -b u-boot.kwb
```

* `-t`: flag that enables a terminal on the device.
* `-B`: baud rate. Speed of the communication between our device and the GuruPlug.
* `-b`: boot with a custom bootloader.
* `/dev/ttyUSB0`: device associated with the JTAG connection. The data will be sent over this channel. `ls /dev/tty*` can be used to list which devices are connected.

After running the command we should see something like this:

```console
kwboot version 2024.01
Detected kwbimage v0 with NAND boot signature
Patching image boot signature to UART
Sending boot message. Please reboot the target...
```

The TX and RX LED lights on the JTAG should be flashing if it's connected correctly. This indicates that the device is recieving and sending data.

Restart the GuruPlug and you will see the following:

```console
Sending boot image...
  0 % [......................................................................]
 99 % [....................................]
```

When the `U-Boot` image is completely sent our GuruPlug will reboot and we should see the `U-Boot` shell.



## Related links

- https://gitlab.com/fosc-space/GuruPlug-2024
- https://wiki.debian.org/GuruPlugTesting
- https://oinkzwurgl.org/attic/GuruPlug/GuruPlug_U-Boot/
- https://groups.google.com/g/linux.debian.ports.arm/c/NBsvsnRBQp8?pli=1
- https://en.wikipedia.org/wiki/Das_U-Boot
- https://manpages.debian.org/bookworm/u-boot-tools/kwboot.1.en.html
- https://tadeubento.com/2018/sheevaplug-2018-upgrade-u-boot/
