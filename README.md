# Nielsen SDK Diagnostic Tool

Nielsen SDK Integration and Validation Tool for client developers.

### 📖 [View the Interactive Client Guide →](https://nielsendigitalsdk.github.io/sdk-diagnostic-tool/)
Step-by-step walkthrough with embedded videos — installation, validation workflow, interpreting results, and more.

---

## 📜 License

© Nielsen SDK contains material that is protected by copyright laws, patent laws, trade secret laws, and by international treaty provisions and is Copyright © 2024 The Nielsen Company (US) LLC. All intellectual property rights and licenses therein are reserved by The Nielsen Company (US) LLC and its licensors. Please read the license agreement presented [here](https://engineeringportal.nielsen.com/docs/Special:ClickThrough), which must be accepted in order to download the Nielsen SDKs.
For more information, reach out to your Nielsen Technical Account Manager(TAM).

---

## 🚀 Downloads

### Global Version 

| Platform | Download |
| --- | --- |
| **macOS** | [NielsenTool.dmg](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/NielsenTool.dmg) |
| **Windows** | [nls-validator-win.zip](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/nls-validator-win.zip) |

### Cookieless Version 

| Platform | Download |
| --- | --- |
| **macOS** | [NielsenTool-AGF.dmg](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/NielsenTool-AGF.dmg) |
| **Windows** | [nls-validator-win-agf.zip](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/nls-validator-win-agf.zip) |

> 💡 These links always point to the **latest version**. The tool auto-updates itself!

---

## 📦 Installation

### macOS

1. Download the appropriate `.dmg` file (Global or Cookieless).
2. Double-click to open the disk image.
3. Drag **NielsenTool** to your **Applications** folder.
4. Open **NielsenTool** from Applications.

> ✅ The macOS version is **signed and notarized** by Apple — no security warnings!

### Windows

1. Download the appropriate `.zip` file (Global or Cookieless).
2. Extract the zip to a folder.
3. Double-click `nls-validator.bat`.

---

## ▶️ How to Use

1. **Connect your device:**
* **iOS:** Unlock device and ensure it is “Trusted”.
* **Android:** Enable USB debugging.
* **Simulators:** Ensure Xcode/Android Studio simulator is booted.


2. **Launch the tool:**
* **macOS:** Open NielsenTool from Applications.
* **Windows:** Double-click `nls-validator.bat`.


3. **Validate:** A browser window will open automatically showing live logs and a validation checklist.

---

## 🔄 Auto-Update

The tool **automatically checks for updates** every time you launch it.

```text
  ┌─────────────────────────────────────────────────┐
  │         Nielsen SDK Validator                   │
  └─────────────────────────────────────────────────┘

  📦 Version: 1.0.0
  🔍 Checking for updates...

  ┌─────────────────────────────────────────────────┐
  │  📦 Update available: 1.0.0 → 1.1.0             │
  └─────────────────────────────────────────────────┘

  ⬇ Downloading...
  📀 Installing...
  ✓ Updated to 1.1.0

  🚀 Starting...

```

No action required — updates happen automatically!

---

## 🛠️ Supported Platforms

| Platform | Log Source |
| --- | --- |
| iOS | Physical iPhone (USB) |
| tvOS | Apple TV |
| iOS | iOS Simulator |
| Android | Physical Android (USB) |
| Android | Android Emulator |
| Browser | Chrome, Firefox, Safari |
| Domless | Fire TV |

---

## 📋 Which Version Should I Use?

| Version | Use Case |
| --- | --- |
| **Global** | Standard Nielsen SDK integration with DTVR support |
| **Cookieless** | Cookieless-specific integration (Germany) without DTVR |

---

## 🔧 Troubleshooting

> For detailed step-by-step solutions, see the **[Troubleshooting Guide](docs/TROUBLESHOOTING.md)**.

| Platform | Issue | Details |
| --- | --- | --- |
| iPhone / iPad (USB) | "Trust" dialog missing or device not detected | [View](docs/TROUBLESHOOTING.md#-iphone--ipad-usb) |
| Android Phone (USB) | Device not detected — USB debugging not enabled | [View](docs/TROUBLESHOOTING.md#-android-phone-usb) |
| Android Emulator | Emulator not listed — ADB server conflict | [View](docs/TROUBLESHOOTING.md#-android-emulator) |
| Fire TV (Wi-Fi) | Cannot connect — ADB debugging or network issue | [View](docs/TROUBLESHOOTING.md#-fire-tv-standard--wi-fi) |
| Fire TV (VegaOS) | No logs — requires USB, uses loggingctl not logcat | [View](docs/TROUBLESHOOTING.md#-fire-tv-vegaos) |
| Apple TV (Wi-Fi) | Discovery, pairing, or tunnel issues | [View](docs/TROUBLESHOOTING.md#-apple-tv-wi-fi) |
| Browser (Chrome/Firefox/Safari) | Browser fails to launch or no logs | [View](docs/TROUBLESHOOTING.md#-browser-chrome--firefox--safari) |
| macOS | "NielsenTool" is damaged / can't be opened | [View](docs/TROUBLESHOOTING.md#-macos--general) |
| Auto-Update | Update fails or settings lost | [View](docs/TROUBLESHOOTING.md#-auto-update-issues) |
| All Platforms | No logs — incorrect operation order or debug flag not enabled | [View](docs/TROUBLESHOOTING.md#-before-you-start) |
| All Platforms | Rules stay gray or show red (failed) | [View](docs/TROUBLESHOOTING.md#rules-stay-gray-never-pass-or-fail) |

---

## ⚠️ Known Limitations

| Limitation | Details |
| --- | --- |
| **Intel-based Macs** | Not supported. Requires **Apple Silicon** (M1/M2/M3/M4). Intel Macs have known incompatibilities with the iOS and Apple TV connectivity toolchain. |
| **Apple TV — Wi-Fi only** | Apple TV connectivity is Wi-Fi only (Bonjour discovery → PIN pairing → tunnel). USB log capture is not available for Apple TV. |
| **Domless SDK** | Domless SDK validation is currently supported **only via Fire TV (VegaOS)**. Other platforms (Android, iOS, standard Fire TV) do not support Domless SDK log capture at this time. |
| **Mobile browser BSDK logs** | This tool cannot capture Browser SDK logs from a mobile device's browser (e.g., Chrome on iPhone). Mobile browsers sandbox console output. Browser validation uses **desktop Playwright only** (Chrome, Firefox, WebKit). |

---

## 🆘 Support

For assistance, contact the Nielsen Ops/Certification team or your Nielsen Technical Account Manager (TAM).

When reporting issues, please include:
1. **Tool version** (shown in the header or terminal on launch).
2. **Platform** (macOS/Windows) and **OS version**.
3. **Device type** being validated.
4. **Screenshot or export** of the error with reproducible steps.

