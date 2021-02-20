# hackintosh

## info

A collection of my Hackintosh builds.

Please note that these configurations are customized specifically for my builds and needs. Beware that copy and paste from here may not work for you, even with the same hardware. Also remembar to change the data regarding the PlatformInfo inside the config.plist with your personal one ([see here](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#platforminfo)).

## smbios

If you change your SMBIOS configuration in your config.plist (SystemProductName, SystemSerialNumber, MLB, SystemUUID) inside an already installed Hackintosh drive, then beware that your current installation could experience some (little) issues:
* you'll need to map your USB port from scratch
* you'll need to enter again your ssh keys' passphrase
* some applications could reset themselves (like Google Chrome)
* some applications could ask again for their license serial number (like Luminar), but other won't (like PhpStorm)
* some os settings could be reset to default (like the screensaver and the status bar)

## tips

Read the Hackintosh guide from [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/).

To download macOS use [gibMacOS](https://github.com/corpnewt/gibMacOS).

To edit a config.plist file use [ProperTree](https://github.com/corpnewt/ProperTree).

To generate SMBIOS data use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).

To map your USB ports use [USBMap](https://github.com/corpnewt/USBMap).

To better explore hardware information use [IORegistryExplorer](https://github.com/vulgo/IORegistryExplorer).

To interact with an EFI partition with macOS, use the following commands.

```bash
diskutil list
```

```bash
sudo diskutil mount disk0s1
```

```bash
sudo diskutil unmount disk0s1
```

