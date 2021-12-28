# CUPERTINO

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

- Motherboard: ASRock Z370 Pro4 (BIOS 3.30)
- CPU: Intel Core i7-8700
- CPU Cooler: Cooler Master Hyper H412R
- iGPU: Intel UHD Graphics 630
- GPU: Radeon RX 580
- RAM: Corsair Vengeance LPX DDR4 3000 MHz 8 GB X 4
- Bluetooth: ASUS USB-BT400 USB 2.0 Bluetooth 4.0 Adapter
- Storage 1: Samsung 850 EVO 250 GB (macOS 10.14.6)
- Storage 2: Samsung 840 EVO 250 GB (Windows 10 Build 2004)
- Storage 3: Seagate 1 TB 7200 RPM
- PSU: EVGA SuperNOVA 750 G3
- Rear Fan: Noctua NF-P12 Redux-1700 PWM
- Case: Thermaltake Versa J21 Tempered Glass Edition

### bios

- OC Tweaker/DRAM Configuration/Load XMP Setting: XMP 2.0 Profile 1 (NOPE)
- OC Tweaker/Load Usser Default: Press F5
- Advanced/CPU Configuration/Intel Virtualization Technology: Enabled
- Advanced/Chipset Configuration/Onboard HD Audio: Disabled
- Advanced/Chipset Configuration/Onboard WAN Device: Disabled
- Advanced/Chipset Configuration/Vt-d: Disabled
- Advanced/Chipset Configuration/IOAPIC 24-119 Entries: Enabled
- Advanced/Chipset Configuration/Primary Graphics Adapter: PCI Express
- Advanced/Chipset Configuration/Share Memory: 128MB
- Advanced/Chipset Configuration/IGPU Multi-Monitor: Enabled
- Advanced/Storage Configuration/SATA_0/SATA Device Type: Solid State Drive
- Advanced/Storage Configuration/SATA_1/SATA Device Type: Solid State Drive
- Advanced/Storage Configuration/SATA_2/SATA Device Type: Hard Disk Drive
- Advanced/Storage Configuration/Sata Mode Selection: AHCI
- Advanced/Super IO Configuration/Serial Port: Disabled
- Advanced/USB Configuration/Legacy USB Support : Enabled
- Advanced/USB Configuration/PS/2 Simulator: Disabled
- Advanced/USB Configuration/XHCI Hand-off: Enabled
- Advanced/UEFI Setup Style: Advance Mode
- H/W Monitor/FAN-Tastic Tuning: 40C 30% +10
- Security/Secure Boot/Secure Boot: Disabled
- Security/ Intel Platform Trust Technology: Disabled (Discrete TPM Module)
- Boot/Boot Option #1: SATA_0
- Boot/Boot Option #2: Disabled
- Boot/Fast Boot: Disabled
- Boot/Boot From Onboard LAN: Disabled
- Boot/CSM (Compatibility Support Module)/CSM: Disabled

### opencore

OpenCore 0.7.6 (RELEASE), which means all the debugging features are currenctly disabled.

### config.plist

The SMBIOS is set to iMac19,1. I have a few sensors missing with VirtualSMC, but I overall it's working really great, so I don't mind.

The PlatformInfo data must be manually added, following [this](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#platforminfo) procedure with [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).

If you are using the same motherboard without a descrete GPU, you could encounter a bug that will cause the HDMI port to display a purple/violet screen. To fix this weird behavior go under "PciRoot(0x0)/Pci(0x2,0x0)" and add these two extra records.

| Label                   | Type | Data     |
| ----------------------- | ---- | -------- |
| framebuffer-con1-enable | Data | 01000000 |
| framebuffer-con1-type   | Data | 00080000 |

The AppleALC kext is present inside the configuration, but it's disabled, since I am using an external audio interface through USB (that's why there is no specific boot flag for it).

Double check that SecureBootModel is set to 'Disabled', otherwise you will be stuck in an endless bootloop.

A custom kext for USB mapping is included, so the XhciPortLimit is set to False.

The bluetooth usb dongle works natively.

### acpi

Right now I am using the following Pre-Built SSDTs. One day maybe I will compile them (maybe).

* SSDT-AWAC.aml
* SSDT-EC-USBX-DESKTOP.aml
* SSDT-PLUG-DRTNIA.aml

### drivers

* HfsPlus.efi
* OpenRuntime.efi

### kext

| Kext                                          | Version  |
| --------------------------------------------- | -------- |
| AppleALC                                      | 1.6.7    |
| IntelMausi                                    | 1.0.7    |
| Lilu                                          | 1.5.8    |
| USBMap                                        | iMac19,1 |
| VirtualSMC (with SMCProcessor and SMCSuperIO) | 1.2.8    |
| WhateverGreen                                 | 1.5.5    |

### tools

* OpenShell.efi

### usb-mapping

The USBMap.kext is custom made for my specific setup and the iMac19,1 SMBIOS.

### to do

* Create custom SSDTs.
* Setup rEFInd.
* Test iCloud login and features.

### bugs

* VirtualSMC doesn't show all sensors (like FakeSMC used to do).
* Overcloking the RAM will create wierd bug issues with the USB when going to sleep.
* Removing a USB device during sleep will wake the computer.
* DRM features doesn't really work well with iTunes and Safari.
