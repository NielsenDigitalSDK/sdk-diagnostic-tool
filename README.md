# SDK Diagnostic Tool

Nielsen SDK Integration and Validation Tool for client developers.

---

## 🚀 Downloads

### Global Version (with DTVR)

| Platform | Download |
| --- | --- |
| **macOS** | [NielsenTool.dmg](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/NielsenTool.dmg) |
| **Windows** | [nls-validator-win.zip](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/nls-validator-win.zip) |

### AGF Version (without DTVR)

| Platform | Download |
| --- | --- |
| **macOS** | [NielsenTool-AGF.dmg](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/NielsenTool-AGF.dmg) |
| **Windows** | [nls-validator-win-agf.zip](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/nls-validator-win-agf.zip) |

> 💡 These links always point to the **latest version**. The tool auto-updates itself!

---

## 📦 Installation

### macOS

1. Download the appropriate `.dmg` file (Global or AGF).
2. Double-click to open the disk image.
3. Drag **NielsenTool** to your **Applications** folder.
4. Open **NielsenTool** from Applications.

> ✅ The macOS version is **signed and notarized** by Apple — no security warnings!

### Windows

1. Download the appropriate `.zip` file (Global or AGF).
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
| **AGF** | AGF-specific integration (Germany) without DTVR |

---

## 🆘 Support

For assistance, contact the Nielsen Ops/Certification team.

---

## 📜 License

© Nielsen. Internal use only.

---
