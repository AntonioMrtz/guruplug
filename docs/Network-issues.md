# Network issues
This section covers:

* How to restart network ifaces
* How to obtain IP using dhclient
* How to set MAC address
* How to set network config on OS startup 

## Manual approach

For doing the process manually you can simply run this script changing the network iface and the MAC Adress:

```console
ip link set dev eth0 address 00:11:22:33:44:66
ip link set eth0 down
dhclient eth0
ip link set eth0 up
```

This configuration is cleaned after a reboot.

## Automatic approach

It will run automatically on OS startup and won't be cleaned after reboots.

Go to `/etc/network/interfaces` and add:

```console
auto eth0
iface eth0 inet dhcp
    hwaddress ether 00:11:22:33:44:66  # Replace with your desired MAC address
```

This configuration will:

* Tell `eth0` iface to start automatically on boot.
* Asign a MAC adress. Can't bring `eth` iface without a MAC adress.
* Use `ipv4` and `dhcp`.

Remove other `eth0` iface configuration found in that file.
