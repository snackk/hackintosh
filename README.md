# Description
MacOs Sonoma 14.3.1 running with OpenCore 1.0.4

![Screenshot 2025-03-19 at 15 14 17](https://github.com/user-attachments/assets/9253d484-2f8d-4ebe-bc69-3120159d0b6c)

### Configuration

| **Component**     | **Model**                        |
|-------------------|----------------------------------|
| CPU               | Intel Core i5 14400F             |
| Dedicated GPU     | AMD Radeon RX 6650 XT 8GB        |
| Motherboard       | Asus TUF B760M WIFI PLUS WIFI D4 |
| Audio             | Realtek ALC897	                |
| Network/Bluetooth | Intel AX201 / BCM94360CD         |
| SSD               | Samsung 980 Evo Plus 256GB       |
| RAM               | Corsair Vengeance 2x 8GB         |
| Case              | CORSAIR Crystal Series 280X      |

### Kexts

| Kext                   | Description                                                                                                                                                                          |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lilu                   | Essential                                                                                                                                                                            |
| AppleALC               | Audio driver                                                                                                                                                                         |
| BlueToolFixup          | Bluetooth repair patch                                                                                                                                                               |
| CpuTopologyRebuild     | Intel Alder Lake, Raptor Lake, and Arrow Lake core fix                                                                                                                               |
| IntelBTPatcher         | Bluetooth driver                                                                                                                                                                     |
| IntelBluetoothFirmware | Bluetooth driver                                                                                                                                                                     |
| LucyRTL8125Ethernet    | Ethernet driver                                                                                                                                                                      |
| NVMeFix                | NVMe hard drive power management                                                                                                                                                     |
| RestrictEvents         | Lilu Kernel extension for blocking unwanted processes causing compatibility issues on different hardware and unlocking the support for certain features restricted to other hardware |
| VirtualSMC             | Emulates critical Apple hardware to allow for battery / sensors / sleep functionality                                                                                                |
| SMCProcessor           | Intel Processor sensors                                                                                                                                                              |
| SMCSuperIO             | -                                                                                                                                                                                    |
| NootRX                 | Graphical driver for RX 6650 XT                                                                                                                                                      |
| XHCI-Unsupported       | Turn on unsupported features                                                                                                                                                         |
| Itlwm                  | Intel Wireless Driver for AX201                                                                                                                                                      |

### UEFI Configuration

| Disable     | Enable                                                 |
|-------------|--------------------------------------------------------|
| Fast-Boot   | VT-x                                                   |
| Secure-Boot | VT-d (**DisableIoMapper** should be **YES**)           |
| VMD         | Above 4G Decoding                                      |
| -           | Resizable BAR (**ResizeAppleGpuBars** should be **0**) |
| -           | EHCI/XHCI Hand-off                                     |

### Audio Layout-id
[https://github.com/acidanthera/AppleALC/wiki/Supported-codecs](ALC897 - supported codecs)

Possible layouts [11, 12, 13, 21, 22, 23, 66, 69, 77, 98, 99]

### Not Working / Current Issues
- AirDrop;
