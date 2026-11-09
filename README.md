# SM6 POS Terminal SDK — V1.0.1

Software Development Kit for the **SM6 POS (Point-of-Sale) terminal**, an Android-based smart payment device. This SDK provides libraries, firmware, demo applications, and documentation to integrate and test the terminal's hardware peripherals.

---

## Repository Structure

```
├── 
├── demo/                 # Demo APKs and HardwareTest source project
│   ├── uf-hardwaretest/  # Android Studio project — hardware test application
│   ├── AppServer.apk     # Background service APK (required by the SDK)
│   ├── PinEntry.apk      # Secure PIN-entry keypad application
│   ├── loadtools.apk     # SP firmware update tool
│   └── HardwareTest.apk  # Built demo app for hardware testing
├── docs/                 # Documentation
├── libs/                 # Shared libraries (AAR, JAR, .so)
└── release note.txt      # Version history & changelog
```

---

## Supported Hardware Peripherals

| Module      | Description                              | Demo Activity            |
|-------------|------------------------------------------|--------------------------|
| **ICC**     | Integrated Circuit Card (smart card)     | `IccActivity`            |
| **MCR**     | Magnetic Card Reader (swipe)             | `McrActivity`            |
| **PICC**    | Contactless card reader (RFID / NFC)     | `PiccActivity`           |
| **PCI**     | PCI security module (PIN pad / SAM)      | `PciActivity`            |
| **Printer** | Built-in thermal receipt printer         | `PrinterActivity`        |
| **Fingerprint** | Fingerprint sensor                   | `FingerPrintActivity`    |
| **Serial**  | Serial port (RS-232 / external devices)  | `SerialActivity`         |
| **Secondary Display** | Customer-facing sub-screen     | `SecondActivity`         |
| **System**  | GPIO, power control, firmware info       | `SysActivity`            |

---

## Libraries Overview

| Library File                          | Type    | Purpose                                   |
|---------------------------------------|---------|-------------------------------------------|
| `DeviceAPI_ver20231031_release.aar`   | AAR     | Core Device API for POS peripherals       |
| `libraryuart-release.aar`             | AAR     | UART / serial communication (release)     |
| `libraryuart-debug.aar`               | AAR     | UART / serial communication (debug)       |
| `printerlib.jar`                      | JAR     | Thermal printer control library           |
| `securitymoduleapi.jar`               | JAR     | Security module (PCI / SAM) API           |
| `libprinter_dll.so`                   | .so     | Native printer driver (arm64-v8a)         |
| `libserial_port.so`                   | .so     | Native serial port driver (armeabi-v7a)   |
| `libfinger_dll.so`                    | .so     | Native fingerprint driver (armeabi-v7a)   |

---

## Firmware

- **SP Firmware:** `SM6-App_V1.0.3_1210_signed.bin` — Secure Processor application firmware. Loaded onto the device via `loadtools.apk`.
- **Printer firmware assets:** `PRT_UPDATE.bin`, printer model-specific firmware files included in the demo app's `assets/`.

---

## Demo App — HardwareTest

The `demo/uf-hardwaretest/` directory contains a full **Android Studio (Gradle)** project that demonstrates every hardware module.

### Build Info
- **compileSdk:** 33
- **minSdk:** 31 (Android 12)
- **targetSdk:** 33 (Android 13)
- **Language:** Java 8
- **Shared User ID:** `android.uid.system` (system-level application)

### Key Dependencies
- AndroidX (Fragment, ViewPager2, AppCompat, ConstraintLayout)
- Glide (image loading)
- Google Material Design
- FlatDir repository for local AAR/JAR libraries

### Usage Setup
1. Install `AppServer.apk` (background service).
2. Install `PinEntry.apk` (secure PIN keypad, invoked by AppServer).
3. Install `loadtools.apk` (used to load SP firmware onto the device).
4. Build and install the `HardwareTest` app (`demo/uf-hardwaretest`).

---

## Documentation

- **General API User Guide** (`docs/General API user guide[V1.0].docx`) — API reference for the Device SDK.

---

## Release History

| Date       | Notes                                                                                    |
|------------|------------------------------------------------------------------------------------------|
| 2026-02-03 | Initial release. System modules: ICC, MSR, PICC, Printer, PCI.                           |
| 2026-03-20 | `apidemo` renamed to `HardwareTest`. Added fingerprint & secondary-screen test modules. AppServer updated for Android 16 support. |

---

## Requirements

- **Device:** SM6 POS terminal (manufacturer: **Unifou**)
- **OS:** Android 12+ (API 31+)
- **Build:** Android Studio (Gradle 8.x, JDK 8+)
- **Signing:** System-level keystore required (shared UID `android.uid.system`)

---

## Notes

- The SDK is intended for **system-level** applications running on the SM6 POS terminal hardware. It is not a general-purpose Android library.
- Native libraries (`.so`) are currently provided for **arm64-v8a** and **armeabi-v7a** architectures.
- The `DeviceAPI` AAR is the primary entry point for peripheral control; the demo app's `MainActivity` shows the initialization pattern via `com.pos.api.Sys`.
