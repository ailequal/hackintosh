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
- RAM : Corsair Vengeance LPX DDR4 3000 MHz 8 GB X 4
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
- Advanced/Chipset Configuration/Primary Graphics Adapter: Onboard
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

OpenCore 0.6.2 (RELEASE), which means all the debugging features are currenctly disabled.

### config.plist

The SMBIOS is set to iMac18,1. It's the best one for this build: it's the last iMac with iGPU and it does recognize enough temperaturs sensors for me (I am using VirtualSMC) instead of the old FakeSMC (which actually recognize more sensors for my build, but it's quite old at this point). I tried iMac19,1 (the best choice from the main guide) but it wasn't that great in terms of sensors. There is also the iMac19,2 which has the exactly same CPU as mine (I haven't tested it yet).

Under PciRoot(0x0)/Pci(0x2,0x0) there are two extra records that will fix a bug that will cause the HDMI port to display a purple/violet screen. These are the following needed for this board.

| Label                   | Type | Data     |
| ----------------------- | ---- | -------- |
| framebuffer-con1-enable | Data | 01000000 |
| framebuffer-con1-type   | Data | 00080000 |

The AppleALC kext is present inside the configuration, but it's disabled, since I am using an external audio interface through USB (that's why there is no specific boot flag for it).

Double check that SecureBootModel is set to 'Disabled', otherwise you will be stuck in an endless bootloop.

A custom kext for USB mapping is included, so the XhciPortLimit is set to False.

### acpi

Right now I am using the following Pre-Built SSDTs. I will sooner compile them manually.

* SSDT-AWAC.aml
* SSDT-EC-USBX-DESKTOP.aml
* SSDT-PLUG-DRTNIA.aml

### drivers

* HfsPlus.efi
* OpenRuntime.efi

### kext

| Kext                                          | Version |
| --------------------------------------------- | ------- |
| Lilu                                          | 1.4.8   |
| VirtualSMC (with SMCProcessor and SMCSuperIO) | 1.1.7   |
| AppleALC                                      | 1.5.3   |
| IntelMausi                                    | 1.0.4   |
| USBMap                                        | Custom  |
| WhateverGreen                                 | 1.4.3   |

### tools

* OpenShell.efi

### usb-mapping

The USBMap.kext is custom made for my specific setup.

### to do

* Create custom SSDTs.
* Setup rEFInd.
* Test iCloud login and features.

### bugs

* VirtualSMC doesn't show all sensors (like FakeSMC used to do).
* Overcloking the RAM will create wierd bug issues with the USB when going to sleep.
* Removing a USB device during sleep will wake the computer.
* DRM features doesn't really work well with iTunes and Safari.

