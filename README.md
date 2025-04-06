# Description

MacOs Sonoma 14.3.1 running with OpenCore 1.0.4
![Screenshot 2025-04-06 at 22 09 21](https://github.com/user-attachments/assets/ecd0e8eb-8d64-4fd9-9095-a64e7f724aa4)

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

### Motherboard / USB Mapping

<img width="139" alt="Screenshot 2025-04-05 at 17 46 52" src="https://github.com/user-attachments/assets/451d6c00-8183-4299-b0e5-b491406f1631" />

### Internal (255)
| Port | UK Code | Controller            | Hex Code       | Address   | Type   |
|------|---------|-----------------------|----------------|-----------|--------|
| 14   | UK14    | AppleUSB20XHCIPort   | 14 (0e000000)  | 14e00000  | Type 3 |
| 2    | UK02    | AppleUSB20XHCIPort   | 2 (02000000)   | 14200000  | Type 3 |
| 7    | UK07    | AppleUSB20XHCIPort   | 7 (07000000)   | 14700000  | Type 3 |
| 11   | UK11    | AppleUSB20XHCIPort   | 11 (0b000000)  | 14b00000  | Type 3 |

### USB 2.0 Type A (0)
| Port | UK Code | Controller            | Hex Code       | Address   | Type           |
|------|---------|-----------------------|----------------|-----------|----------------|
| 28   | UK03    | AppleUSB20XHCIPort   | 3 (03000000)   | 00300000  | Type 3 - USB 2 |
| 6    | UK06    | AppleUSB20XHCIPort   | 6 (06000000)   | 14600000  | Type 3 - USB 3 |
| 5    | UK05    | AppleUSB20XHCIPort   | 5 (05000000)   | 14500000  | Type 3 - USB 4 |
| 9    | UK09    | AppleUSB20XHCIPort   | 9 (09000000)   | 14900000  | Type 3 - USB 5 |
| 4    | UK04    | AppleUSB20XHCIPort   | 4 (04000000)   | 14400000  | Type 3 - USB 6 |
| 3    | UK03    | AppleUSB20XHCIPort   | 3 (04000000)   | 14400000  | Type 3 - USB 7 |

### Front Panel
| Port       | UK Code     | Controller            | Hex Code       | Address     | Type               |
|------------|-------------|-----------------------|----------------|-------------|--------------------|
| Front Panel1 - USB2.0     **10**      **UK10**

### Not Working / Current Issues

- AirDrop;
