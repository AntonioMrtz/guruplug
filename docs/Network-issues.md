# Network issues

GuruPlug


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


## Script approach

It will run automatically on OS startup

### Create a init.d service

This script does the following:

1. Sets MAC adress
2. Gives static ip to network interface
3. Restarts netowork interface
4. Restart network service

#### Create the script file

```console
nano /etc/init.d/setup_network.sh
```

#### Replace `INTERFACE` y `MAC_ADDRESS` with the desired network interface and mac address 

```console
#!/bin/sh -e

# Define the interface and MAC address as variables
INTERFACE="eth0"
MAC_ADDRESS="00:11:22:33:44:66"

# Define the log file path
LOG_FILE="/var/log/setup_network.log"

# Log function to capture messages with timestamps
log_message() {
    echo "$(date) - $1" >> $LOG_FILE
}

# Clear previous log contents at the start
echo "Starting network setup script..." > $LOG_FILE

# Set MAC address for the specified interface
log_message "Setting MAC address for $INTERFACE to $MAC_ADDRESS"
if ip link set dev $INTERFACE address $MAC_ADDRESS; then
    log_message "Successfully set MAC address for $INTERFACE."
else
    log_message "Error: Failed to set MAC address for $INTERFACE."
    exit 1
fi

# Bring the interface down
log_message "Bringing $INTERFACE interface down..."
if ip link set $INTERFACE down; then
    log_message "Successfully brought $INTERFACE down."
else
    log_message "Error: Failed to bring $INTERFACE down."
    exit 1
fi

# Request DHCP lease for the specified interface
log_message "Requesting DHCP lease for $INTERFACE..."
if dhclient $INTERFACE >> $LOG_FILE 2>&1; then
    log_message "Successfully obtained DHCP lease for $INTERFACE."
else
    log_message "Error: Failed to obtain DHCP lease for $INTERFACE."
    exit 1
fi

# Bring the interface up
log_message "Bringing $INTERFACE interface up..."
if ip link set $INTERFACE up; then
    log_message "Successfully brought $INTERFACE up."
else
    log_message "Error: Failed to bring $INTERFACE up."
    exit 1
fi

# Log IP assignment to check status
log_message "Network configuration complete. Current IP configuration for $INTERFACE:"
ip a show $INTERFACE >> $LOG_FILE 2>&1

log_message "Network setup script completed."
```

#### Give the script permissions

```console
chmod 777 /etc/init.d/setup_network.sh
```

#### Create log file to catch script output

```
touch /var/log/setup_network.log
chmod 666 /var/log/setup_network.log
```