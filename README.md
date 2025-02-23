# Guruplug

<img src="docs/assets/guruplug.jpeg" width="500" />

## What was learnt from this experience

### 1. **JTAG**
   - JTAG (Joint Test Action Group) is used for debugging and testing embedded systems.
   - Used for serial communication and low-level debugging on hardware.
   - Helpful in unbricking devices and recovering from failed boot sequences.

### 2. **U-Boot, UImage, and UInitd**
   - **U-Boot**: A widely used bootloader for embedded systems.
   - **UImage**: A compressed kernel image used by U-Boot.
   - **UInitd**: The initialization script for U-Boot, used to configure the system before starting the operating system.

### 3. **Network Installation of Debian**
   - Installing Debian Linux on an ARM-based device over the network.
   - Configuring the device to boot from a network source (e.g., TFTP, NFS).
   - Ensuring network interfaces are correctly set up to facilitate installation.

### 4. **Boot from USB**
   - Configuring an embedded system to boot from a USB device.
   - Using U-Boot to select boot devices and initiate the boot process from a USB drive.
   - Troubleshooting boot failures when using USB devices.

### 5. **Unbricking ARM Device using `kwboot`**
   - Steps to restore an ARM-based device that is stuck in a boot loop or is not booting.
   - Methods include re-flashing U-Boot, using serial communication, and recovery via JTAG with `kwboot` ARM Marvell recovery software.
   
### 6. **Upgrade U-Boot**
   - Process of upgrading U-Boot to a newer version.
   - Flashing U-Boot to the device's bootloader partition.
   - Ensuring compatibility with new kernel images and boot processes.

### 7. **Auto Start Network and Assign MAC Address**
   - Configuring the device to automatically start the network interfaces during boot.
   - Assigning a static or dynamic MAC address for network identification.

### 8. **Serial Communication using `screen`**
   - Using the `screen` utility to communicate with an embedded system through a serial connection.

### 9. **Flash Internal NAND Memory**
   - Flashing the internal NAND memory to install or upgrade the operating system.
   - Methods for writing to NAND, verifying flash integrity, and booting from NAND storage.

### 10. **Update Outdated Repository Sources**
   - Replace outdated sources with archived repositories.
   - Add sources for drivers from non free repositories.
   - Handle outdated GPG keys.

### 11. **Manually Install Bluetooth and WiFi Drivers**
   - Building, installing and configuring Bluetooth and WiFi drivers on ARM Debian-based systems.

### 12. **Tethering using Phone**
   - Configuring an ARM device to tether internet access via a smartphone.
   - Setting up USB tethering or WiFi hotspot modes to provide network access.

### 13. **How Low-Level Boot Process Works**
   - Understanding the sequence of steps from power-on to full operating system boot.
   - Key components involved: Bootloader (U-Boot), Kernel initialization, and Root filesystem mounting.

## Launch server with documentation

### Setup

```console
python3 -m venv venv &&
source venv/bin/activate &&
pip install -r requirements.txt
```

### Run MKdocs server

```console
mkdocs serve -a 0.0.0.0:8000
```