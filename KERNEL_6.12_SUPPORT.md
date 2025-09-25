# Kernel 6.12 Support for RTL8723DU Bluetooth Driver

## Overview
This branch adds support for modern Linux kernels (6.12+) and the Edimax RTL8723DU combo WiFi/Bluetooth adapter.

## Changes Made

### 1. Kernel Compatibility Fixes
- **File**: All .c files
- **Change**: `#include <asm/unaligned.h>` → `#include <linux/unaligned.h>`
- **Reason**: Header location changed in kernel 6.12+

### 2. USB Device Support
- **File**: `usb/bluetooth_usb_driver/rtk_bt.c`
- **Change**: Added vendor ID `0x7392` (Edimax) to USB device table
- **Reason**: Enable driver to recognize Edimax devices

### 3. Firmware Patch Support
- **File**: `usb/bluetooth_usb_driver/rtk_misc.c`
- **Change**: Added PID `0xd611` to firmware patch table
- **Reason**: Enable firmware loading for Edimax RTL8723DU variant

## Tested Devices
- **Device**: Edimax Wi-Fi N150 Bluetooth4.0 USB Adapter
- **USB ID**: 7392:d611
- **Chipset**: RTL8723DU
- **Kernel**: 6.12.47-current-sunxi64
- **Architecture**: aarch64 (ARM64)

## Installation

### Prerequisites
```bash
sudo apt update
sudo apt install build-essential dkms git linux-headers-$(uname -r)
```

### Build and Install
```bash
git clone https://github.com/YOUR_USERNAME/rtkbt.git
cd rtkbt
git checkout kernel-6.12-support
sudo make install INTERFACE=usb
```

### Verify Installation
```bash
sudo hciconfig
# Should show hci0 device
sudo hciconfig hci0 up
sudo hciconfig hci0 piscan
```

## Known Issues
- Driver may need to be reloaded after WiFi driver changes
- Some older kernels may not have the new header location

## Contributing
This is a community contribution. If you have improvements or find issues:
1. Test on your hardware
2. Document your findings
3. Submit a pull request

## Original Repository
Based on: https://github.com/radxa/rtkbt
