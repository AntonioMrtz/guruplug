# Wifi and Bluethooth drivers


## Enabling GuruPlug Server Marvell Libertas 8688 SDIO 802.11b/g WiFi

The GuruPlug Server Plus incorporates an AzureWave AW-GH381 IEEE 802.11 b/g Wireless LAN & Bluetooth 3.0 module IC, functionally equivalent to the Marvell 88W8688
WiFi

Enable the following as kernel modules and compile your modules:

```console
Device Drivers > Network device support > Wireless LAN
   Marvell 8xxx Libertas WLAN driver support
   Marvell Libertas 8385/8686/8688 SDIO 802.11b/g cards
```

The modules above will want to load firmware from the root filesystem that is not available until the filesystem is mounted. This will result in an initial error loading firmware (see below), but the kernel will retry later and should succeed. To mitigate this issue, I choose to compile these as loadable modules rather than built-in.

```console
mmc0: new high speed SDIO card at address 0001
libertas_sdio mmc0:0001:1: Direct firmware load failed with error -2
libertas_sdio mmc0:0001:1: Falling back to user helper
```

Download Binary BLOBs to /lib/firmware:

```console
mkdir /lib/firmware
cd /lib/firmware
wget http://git.kernel.org/cgit/linux/kernel/git/firmware/linux-firmware.git/plain/mrvl/sd8688_helper.bin
wget http://git.kernel.org/cgit/linux/kernel/git/firmware/linux-firmware.git/plain/mrvl/sd8688.bin
```

And reboot. The modules should now load. If not, manually load them using:

```console
insmod /lib/modules/<kernel ver>/kernel/drivers/net/wireless/libertas/libertas.ko 
insmod /lib/modules/<kernel ver>/kernel/drivers/net/wireless/libertas/libertas_sdio.ko 
```

When loaded, the following debug messages should be displayed:

```console
libertas_sdio mmc0:0001:1 (unregistered net_device): 00:24:23:1f:b3:e9, fw 10.38.1p25, cap 0x00000303
libertas_sdio mmc0:0001:1 wlan0: Marvell WLAN 802.11 adapter
```

## Bluetooth

Enable the following Linux kernel modules and recompile your kernel. These modules will want to load firmware from the root filesystem that is not available until mounted. This will result in an initial error loading firmware, but the kernel will retry later and should succeed. To mitigate this issue, I choose to compile these as loadable modules rather than built-in.

```console
Networking Support -> Bluetooth subsystem support 
Networking Support -> Bluetooth subsystem support -> Bluetooth device drivers
	Marvell Bluetooth driver support
	Marvell BT-over-SDIO driver
```

The WLAN/Bluetooth SoC has an ARMv5TE core that runs closed firmware. Download the Binary BLOBs (firmware) to /lib/firmware/mrvl/:

```console
mkdir /lib/firmware /lib/firmware/mrvl 
cd /lib/firmware/mrvl 
wget http://git.kernel.org/cgit/linux/kernel/git/firmware/linux-firmware.git/plain/mrvl/sd8688_helper.bin
wget http://git.kernel.org/cgit/linux/kernel/git/firmware/linux-firmware.git/plain/mrvl/sd8688.bin
```

Upon reboot, you should now see the following kernel message as the module loads:

```console
Bluetooth: vendor=0x2df, device=0x9105, class=255, fn=2
```

and be greeted with a Bluetooth hci device:

```console
$ hciconfig
hci0:   Type: BR/EDR  Bus: SDIO
        BD Address: 00:24:23:1F:B3:EA  ACL MTU: 1021:7  SCO MTU: 240:3
        DOWN
        RX bytes:647 acl:0 sco:0 events:22 errors:0
        TX bytes:442 acl:0 sco:0 commands:22 errors:0

If this is not the case, check that the btmrvl.ko & btmrvl_sdio.ko modules are loaded. 
```

## Related links

https://wiki.beyondlogic.org/index.php?title=GuruPlug_Libertas_SD8688