# 🖥️ Asus TUF B760M - macOS Tahoe 26.7.2

**macOS Tahoe 26.7.2** | **OpenCore 1.0.8** | **Intel i5-14400F** + **RX 6900 XT**

<img width="3440" height="1440" alt="Screenshot 2026-11-06 at 11 54 13" src="https://github.com/user-attachments/assets/b5ff5714-ebb9-4e56-bdb4-30dcc99dec79" />



---

## 🛠️ Hardware Configuration

| Component | Model |
|-----------|-------|
| **CPU** | Intel Core i5-14400F |
| **GPU** | AMD Radeon RX 6900 XT 16 GB |
| **Motherboard** | Asus TUF B760M-PLUS WIFI D4 |
| **Audio** | Realtek ALC897 |
| **WiFi/BT** | Intel CNVi Wi-Fi 8086:7A70 + BT (AirportItlwm / IntelBluetooth stack) |
| **Native WiFi/BT** | BCM94360CD *(recommended)* |
| **SSD** | Samsung 980 EVO Plus 256 GB |
| **RAM** | Corsair Vengeance 4×8 GB DDR4 |
| **Case** | CORSAIR Crystal Series 280X |

---

## 📦 Kexts (EFI/OC/Kernel)

| Kext | Purpose |
|------|---------|
| **Lilu.kext** | Core patching framework |
| **AppleALC.kext** | Realtek ALC897 audio *(layout-id: 11)* |
| **SimpleHDA.kext** | Restores AppleHDA on Tahoe *(must load after AppleALC)* |
| **VirtualSMC.kext** | SMC emulation (sensors, power mgmt) |
| **SMCProcessor.kext** | CPU sensors |
| **SMCSuperIO.kext** | Motherboard sensors |
| **CpuTopologyRebuild.kext** | Raptor Lake core topology |
| **NVMeFix.kext** | NVMe power management |
| **NootRX.kext** | AMD RX 6900 XT accelerator |
| **RestrictEvents.kext** | Block macOS security restrictions |
| **LucyRTL8125Ethernet.kext** | Realtek 2.5GbE LAN |
| **IntelBluetoothFirmware.kext** | Intel BT firmware |
| **IntelBTPatcher.kext** | Bluetooth stack patches |
| **BlueToolFixup.kext** | Bluetooth controller fixes |
| **AirportItlwm.kext** | Intel Wi-Fi, native Wi-Fi menu *(laobamac fork, Tahoe build)* |
| **USBMap.kext** | Custom USB port mapping |
| **AMFIPass.kext** | AMFI bypass |
| **XHCI-unsupported.kext** | USB XHCI unlock *(DISABLED)* |

> **Boot-args**: `agdpmod=pikera lilucpu=10 -radcodec shda-lang=pt_PT`

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
**layout-id**: `11` *(PciRoot(0x0)/Pci(0x1F,0x3), stored as Data `0B000000`)*  
**Supported layouts**: `11, 12, 13, 21, 22, 23, 66, 69, 77, 98, 99`

macOS 26 no longer ships `AppleHDA.kext`, so AppleALC alone cannot provide analog audio on Tahoe.
[SimpleHDA](https://github.com/laobamac/SimpleHDA) (Lilu plugin, v1.0.1) restores the AppleHDA stack through OpenCore injection, without touching the system volume.
Verified in Hackintool: the ALC897 codec is loaded by `com.apple.driver.AppleHDA` (alongside the AMD HDMI/DP audio).

- Kernel -> Add order: `Lilu` -> `AppleALC` -> `SimpleHDA`
- Requires `Kernel -> Quirks -> DisableLinkeditJettison = true`
- Keep the `layout-id` in a single place (DeviceProperties here, no `alcid` boot-arg)
- `shda-lang=pt_PT` sets the language of the device names (default is Chinese)

---

## 📶 Wi-Fi Configuration

**Card**: Intel CNVi Wi-Fi, PCI `8086:7A70` at `PciRoot(0x0)/Pci(0x14,0x3)`  
**Kext**: [AirportItlwm](https://github.com/laobamac/itlwm) 2.4.0 (laobamac fork), **Tahoe** build

- Do **not** block `IOSkywalkFamily` (`Kernel -> Block`). That entry is only for legacy Broadcom Wi-Fi and removes the system framework that AirportItlwm depends on
- `AMFIPass.kext` must be enabled
- Wi-Fi 6 (HE) is off by default; add `itlwm_he=1` to boot-args to try it

Verified on this machine: the card shows up as `en0` (`com.zxystd.AirportItlwm`), the firmware loads (`fw: 68.01d30b0c.0`) and `system_profiler SPAirPortDataType` lists the nearby networks.

**macOS does not create the Wi-Fi network service by itself.** After the first boot with AirportItlwm, `networksetup -listnetworkserviceorder` has no Wi-Fi entry, the status stays `Network Service Inactive` and the Wi-Fi pane has nothing to show. Add it once (see [itlwm issue #5](https://github.com/laobamac/itlwm/issues/5)):

- System Settings -> Network -> `...` -> Add Service -> Interface: **Wi-Fi**, or
- `sudo networksetup -createnetworkservice Wi-Fi Wi-Fi`

Do not delete the `Ethernet` service: on this machine it is the Realtek LAN (`en1`).

Troubleshooting:

- `networksetup -listallhardwareports` - `en0` must be listed as `Wi-Fi`
- `system_profiler SPAirPortDataType` - firmware version and visible networks
- `log show --last 20m --predicate 'process == "airportd"' --style compact` - scan and join errors
- The RELEASE build of AirportItlwm logs almost nothing in the kernel log; use the DEBUG build from the [releases page](https://github.com/laobamac/itlwm/releases) when you need driver logs

---

## 🧬 USB Port Mapping

<img width="139" alt="Screenshot 2025-04-05 at 17 46 52" src="https://github.com/user-attachments/assets/451d6c00-8183-4299-b0e5-b491406f1631" />


**USBMap.kext** - *12 active ports (15-port limit compliant)*

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

- **❌ AirDrop**: Not working *(AirportItlwm does not support AWDL)*
- **⚠️ Wi-Fi**: WPA3-only and mandatory-PMF networks are not supported by AirportItlwm; WPA2-Personal and WPA2/WPA3 transition are supported according to its README *(joining a network not yet verified on this machine)*
- **ℹ️ Audio / Wi-Fi on Tahoe**: both depend on third-party kexts (SimpleHDA, AirportItlwm) that are still alpha-quality; re-check them after every macOS update
- **✅ Recommendation**: Use BCM94360CD for full Continuity/AirDrop/Handoff

---

Written by @snackk
