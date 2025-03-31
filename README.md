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
### To Be Updated

| Kext | Function |
|------|----------|
| AirportItlwm | Intel wireless card driver |
| AppleMCEReporterDisabler | Turn off AppleIntelMCEReporter to avoid errors on AMD CPU devices |
| IntelBluetoothFirmware | Bluetooth driver |
| Lilu | Essential |
| NootRX | Graphical driver for RX 6650 XT |
| NVMeFix | NVMe hard drive power management |
| RealtekRTL8111 | Ethernet drivers |
| RestrictEvents | Lilu Kernel extension for blocking unwanted processes causing compatibility issues on different hardware and unlocking the support for certain features restricted to other hardware |
| VirtualSMC | Emulates critical Apple hardware to allow for battery / sensors / sleep functionality |
| AppleALC | Audio driver |
| BlueToolFixup | Bluetooth repair patch |
| IntelBTPatcher | Bluetooth driver |
| SMCProcessor | -- |
| SMCSuperIO | -- |

### Not Working / Current Issues
- AirDrop;
