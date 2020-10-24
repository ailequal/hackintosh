# hackintosh

## info

A collection of my Hackintosh builds.

Please note that these configurations are customized specifically for my builds and needs. Beware that copy and paste from here may not work for you, even with the same hardware. Also remembar to change the data regarding the PlatformInfo inside the config.plist with your personal one ([see here](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#platforminfo)).

## tips

Read the Hackintosh guide from [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/).

To download macOS use [gibMacOS](https://github.com/corpnewt/gibMacOS).

To edit a config.plist file use [ProperTree](https://github.com/corpnewt/ProperTree).

To generate SMBIOS data use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).

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

