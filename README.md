# 🖥️ Asus TUF B760M Hackintosh - macOS Tahoe 26.2

**macOS Tahoe 26.2** | **OpenCore 1.0.6** | **Intel i5-14400F** + **RX 6650 XT**

![macOS Tahoe Desktop](https://github.com/user-attachments/assets/6a8ae3c4-5513-4c08-ac7a-c6776106cfcc)

---

## 🛠️ Hardware Configuration

| Component | Model |
|-----------|-------|
| **CPU** | Intel Core i5-14400F |
| **GPU** | AMD Radeon RX 6650 XT 8 GB |
| **Motherboard** | Asus TUF B760M-PLUS WIFI D4 |
| **Audio** | Realtek ALC897 |
| **WiFi/BT** | Intel AX201 (itlwm stack) |
| **Native WiFi/BT** | BCM94360CD *(recommended)* |
| **SSD** | Samsung 980 EVO Plus 256 GB |
| **RAM** | Corsair Vengeance 2×8 GB DDR4 |
| **Case** | CORSAIR Crystal Series 280X |

---

## 📦 Kexts (EFI/OC/Kernel)

| Kext | Purpose |
|------|---------|
| **Lilu.kext** | Core patching framework |
| **AppleALC.kext** | Realtek ALC897 audio *(layout-id: 11)* |
| **VirtualSMC.kext** | SMC emulation (sensors, power mgmt) |
| **SMCProcessor.kext** | CPU sensors |
| **SMCSuperIO.kext** | Motherboard sensors |
| **CpuTopologyRebuild.kext** | Raptor Lake core topology |
| **NVMeFix.kext** | NVMe power management |
| **NootRX.kext** | AMD RX 6650 XT accelerator |
| **RestrictEvents.kext** | Block macOS security restrictions |
| **LucyRTL8125Ethernet.kext** | Realtek 2.5GbE LAN |
| **IntelBluetoothFirmware.kext** | AX201 BT firmware |
| **IntelBTPatcher.kext** | Bluetooth stack patches |
| **BlueToolFixup.kext** | Bluetooth controller fixes |
| **itlwm.kext** | Intel AX201 WiFi |
| **USBMap.kext** | Custom USB port mapping |
| **AMFIPass.kext** | AMFI bypass |
| **XHCI-unsupported.kext** | USB XHCI unlock *(DISABLED)* |

> **Boot-args**: `agdpmod=pikera lilucpu=10 -radcodec`

---

## ⚡ ACPI Patches (EFI/OC/ACPI)

| SSDT File | Status | Purpose |
|-----------|--------|---------|
| SSDT-SBUS.aml | ✅ | USB power (SBUS-MCHC) |
| SSDT-EC.aml | ✅ | Embedded Controller |
| SSDT-PLUG-ALT.aml | ✅ | CPU power management |
| SSDT-RTCAWAC.aml | ✅ | RTC + AWAC clock source |
| SSDT-USBX.aml | ✅ | USB power injection |
| SSDT-BRG0.aml | ✅ | PCIe bridge renaming |
| SSDT-USB-Reset.aml | ❌ | USB reset *(disabled)* |

---

## 🔧 BIOS / UEFI Settings

| **DISABLE** | **ENABLE** |
|-------------|------------|
| Fast Boot | VT-x |
| Secure Boot | VT-d *(DisableIoMapper=YES)* |
| Intel VMD | Above 4G Decoding |
| CSM | Resizable BAR *(ResizeGpuBars=-1)* |
| CFG-Lock | EHCI/XHCI Hand-off |

---

## 🔊 Audio Configuration

**Codec**: Realtek ALC897  
**layout-id**: `11` *(PciRoot(0x0)/Pci(0x1F,0x3))*  
**Supported layouts**: `11, 12, 13, 21, 22, 23, 66, 69, 77, 98, 99`

---

## 🧬 USB Port Mapping

**USBMap.kext** - *12 active ports (15-port limit compliant)*
<img width="139" alt="Screenshot 2025-04-05 at 17 46 52" src="https://github.com/user-attachments/assets/451d6c00-8183-4299-b0e5-b491406f1631" />

### Internal Headers (255)

| Port | Controller | Hex | Address | Type |
|------|------------|-----|---------|------|
| 7 | USB20XHCI | 07 | 14700000 | 255 |
| 14 | USB20XHCI | 0E | 14E00000 | 255 |
| 2 | USB20XHCI | 02 | 14200000 | 255 |
| 11 | USB20XHCI | 0B | 14B00000 | 255 |
`T:7,14,2,11:255`

### USB 2.0 (0)

| Port | Notes |
|------|-------|
| 5 | Rear Port 4 |
| 6 | Rear Port 3 |
`T:5,6:0`

### USB 3.x + Front Panel

| Port | Controller | Hex | Address | Notes |
|------|------------|-----|---------|-------|
| 17 | USB30XHCI | 02 | 00200000 | Rear Port 1 |
| 16 | USB30XHCI | 01 | 00100000 | Rear Port 2 |
| 9 | USB20XHCI | 09 | 14900000 | Rear Port 5 |
| 4 | USB20XHCI | 04 | 14400000 | Rear Port 6 |
| 3 | USB20XHCI | 03 | 14300000 | Rear Port 7 |
| 10 | USB20XHCI | 0A | 14A00000 | Front Header |
`T:17,16,9,4,3,10:3`

---

## ⚠️ Known Issues

- **❌ AirDrop**: Not working *(Intel AX201 limitation)*
- **✅ Recommendation**: Use BCM94360CD for full Continuity/AirDrop/Handoff

---