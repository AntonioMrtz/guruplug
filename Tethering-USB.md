# Tethering using USB

* Connect phone or other device to USB port of the GuruPlug.
* If using an Android device share wifi option will be displayed once you connect it to the USB port of the Guruplug.


## Activate the USB net interface

```console
ifconfig usb0 up
```

## Check interface status


```console
ifconfig usb0
```


If no ip is provided by ifconfig on that interface we can manually try to get an ip. This command request an ipv4 ip to usb0 interface:

```console
dhclient usb0
```


## Try connection

Now we should have and ipv4 assigned. Ping google DNS to check the connection:

```console
ping 8.8.8.8
```