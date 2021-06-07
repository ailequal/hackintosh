# HOLLYWOOD

## index

* [build](#build)
* [bios](#bios)
* [opencore](#opencore)
* [config.plist](#config.plist)
* [acpi](#acpi)
* [drivers](#drivers)
* [kext](#kext)
* [tools](#tools)
* [usb mapping](#usb-mapping)
* [to do](#to-do)
* [bugs](#bugs)

### build

- Motherboard: Gigabyte Z390 Designare (BIOS F7)
- CPU: Intel Core i9-990K
- CPU Cooler: Dark Rock Pro 4
- iGPU: Intel UHD Graphics 630
- GPU: Radeon RX 580 8 GB
- RAM : Corsair Vengeance LPX DDR4 3000 MHz 16 GB X 2
- Storage 1: Silicon Power SSD PCIe M.2 NVMe 512 GB Gen3x4 (macOS 10.15.6)
- Storage 2: SanDisk 250 GB (Windows 10 Build 2004)
- PSU: Seasonic Focus+ 850 W
- Case: NZXT H700

### bios

- BIOS > Windows 8/10 Featues > Other OS
- BIOS > CSM Support > Disabled (Also check that secure boot is disabled)
- Peripherals > Initial Display Output > PCIe Slot 1 (or iGPU if you don't have descrete graphics)
- Peripherals > Intel Platform Trust Techonology > Disabled
- Peripherals > Thunderbolt Configuration > TBT Vt-d Base Security > Disabled
- Peripherals > Thunderbolt Configuration > Thunderbolt Boot Support > Disabled
- Peripherals > Thunderbolt Configuration > Security Level > No Security
- Peripherals > Thunderbolt Configuration > Discrete Thunderbolt Configuration > Thunderbolt USB Support > Enabled
- Peripherals > Thunderbolt Configuration > Discrete Thunderbolt Configuration > GPIO3 Force Pwr > Enabled
- Peripherals > USB Configuration > Legacy USB Support > Enabled
- Peripherals > XHCI Hand-off > Enabled
- Peripherals > Network Stack Configuration > Network Stack > Disabled
- Chipset > Vt-d > Disabled
- Chipset > Internal Graphics > Enabled
- Chipset > DVMT Pre-Alloc > 64M
- Chipset > DVMT Total Gfx Mem > 256M
- Chipset > Audio Controller > Enabled
- Chipset > Above 4G Decoding > Enabled
- Power > Erp > Disabled
- Power > RC6 > Enabled

### opencore

OpenCore 0.6.8 (RELEASE), which means all the debugging features are currenctly disabled.

### config.plist

The SMBIOS is set to iMac19,1.

The PlatformInfo data must be manually added, following [this](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#platforminfo) procedure with [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).

The USB mapping has excluded the integrated motherboard's bluetooth and wifi features. Also the two red USB ports on the rear of the motherboard are only enabled as USB3.

Double check that SecureBootModel is set to 'Disabled', otherwise you will be stuck in an endless bootloop.

A custom kext for USB mapping is included, so the XhciPortLimit is set to False.

### acpi

Right now I am using the following Pre-Built SSDTs. One day maybe I will compile them (maybe).

* SSDT-AWAC.aml
* SSDT-EC-USBX-DESKTOP.aml
* SSDT-PLUG-DRTNIA.aml
* SSDT-PMC.aml

### drivers

* HfsPlus.efi
* OpenRuntime.efi

### kext

| Kext                                          | Version  |
| --------------------------------------------- | -------- |
| AppleALC                                      | 1.5.9    |
| IntelMausi                                    | 1.0.5    |
| Lilu                                          | 1.5.2    |
| NVMeFix                                       | 1.0.6    |
| USBMap                                        | iMac19,1 |
| VirtualSMC (with SMCProcessor and SMCSuperIO) | 1.2.2    |
| WhateverGreen                                 | 1.4.9    |

### tools

* OpenShell.efi

### usb-mapping

The USBMap.kext is custom made for my specific setup and the iMac19,1 SMBIOS.

### to do

* Create custom SSDTs.
* Setup rEFInd.
* Test iCloud login and features.

### bugs

* The secondary ethernet port isn't working.
* Overcloking the RAM will create wierd bug issues with the USB when going to sleep.
* Removing a USB device during sleep will wake the computer.
* DRM features doesn't really work well with iTunes and Safari.
