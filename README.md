# Nielsen SDK Diagnostic Tool

Nielsen SDK Integration and Validation Tool for client developers.

### [View the Interactive Client Guide →](https://nielsendigitalsdk.github.io/sdk-diagnostic-tool/)
Step-by-step walkthrough with embedded videos — installation, login, validation workflow, session sharing, interpreting results, and more.

---

## License

Nielsen SDK contains material that is protected by copyright laws, patent laws, trade secret laws, and by international treaty provisions and is Copyright © 2026 The Nielsen Company (US) LLC. All intellectual property rights and licenses therein are reserved by The Nielsen Company (US) LLC and its licensors. Please read the license agreement presented [here](https://engineeringportal.nielsen.com/docs/Special:ClickThrough), which must be accepted in order to download the Nielsen SDKs.
For more information, reach out to your Nielsen Technical Account Manager (TAM).

---

## Downloads

| Platform | Download |
| --- | --- |
| **macOS** | [NielsenSDKTool.dmg](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/NielsenSDKTool.dmg) |
| **Windows** | [NielsenSDKTool-win.zip](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest/download/NielsenSDKTool-win.zip) |

> These links always point to the **latest version**. The tool auto-updates itself!

---

## Installation

### macOS

1. Download the `.dmg` file.
2. Double-click to open the disk image.
3. Drag **NielsenSDKTool** to your **Applications** folder.
4. Open **NielsenSDKTool** from Applications.

> The macOS version is **signed and notarized** by Apple — no security warnings.

### Windows

1. Download the `.zip` file.
2. Extract the zip to a folder.
3. **To check for updates and launch:** Double-click `UpdateAndLaunch.bat`. Windows may show a security prompt — click "Run" to proceed.
4. **To launch directly (no auto-update):** Double-click `NielsenSDKTool.exe`. The `.exe` is signed by The Nielsen Company (US), LLC — no security warnings.

> The `.exe` is digitally signed with an EV code signing certificate. The `.bat` launcher handles auto-updates but may trigger a Windows security prompt since `.bat` files cannot be signed.

---

## Login

The tool requires authentication. Your Nielsen TAM provides your **username** during onboarding.

1. Launch the tool — a login screen appears.
2. Enter your **username** (case-sensitive, exactly as provided by your TAM).
3. You're logged in. No password or OTP required for client accounts.

> **Important:** Usernames are case-sensitive. Enter it exactly as provided by your Nielsen representative.

**Session behavior:**
- Sessions last 24 hours of inactivity. After that, you'll need to log in again.
- If the tool cannot reach the server (e.g., offline), it uses cached credentials so you can keep working.

**Don't have credentials?** Contact your Nielsen TAM to get onboarded.

---

## How to Use

1. **Log in** with the username provided by your Nielsen TAM.

2. **Connect your device:**
   * **iOS:** Connect via USB, unlock device and ensure it is "Trusted".
   * **Android:** Enable USB debugging.
   * **Simulators/Emulators:** Ensure the simulator or emulator is booted.
   * **Smart TVs:** Enable Developer Mode and note the device IP / debug port.
   * **Mobile Browser (iOS Safari):** iPhone and Mac on the same Wi-Fi.
   * **Mobile Browser (Android Chrome):** Connect via USB with USB debugging enabled.

3. **Launch the tool:**
   * **macOS:** Open NielsenSDKTool from Applications.
   * **Windows:** Double-click `NielsenSDKTool.exe`.

4. **Validate:** A browser window opens showing live logs and a validation checklist.

5. **Share results:** Click **"Share with Nielsen"** to send your session directly to your TAM for review.

---

## Share with Nielsen

After completing a validation session, you can share results with your Nielsen TAM in one click:

1. Run your validation tests until logs are captured.
2. Click the green **"Share with Nielsen"** button in the Session panel (right side).
3. Your session is uploaded and your TAM is notified automatically.

You can also view your previously shared sessions from the **Shared Sessions** page on the home screen.

> **Export still works.** If you prefer, you can still use the purple "Export" button to download a `.json` file and send it manually. But "Share with Nielsen" is faster and preferred.

---

## Auto-Update

The tool **automatically checks for updates** when launched via `UpdateAndLaunch.bat` (Windows) or the app (macOS).

> **Windows:** Auto-update only works when using `UpdateAndLaunch.bat`. Running `NielsenSDKTool.exe` directly skips the update check.

No action required — updates happen automatically.

---

## Supported Platforms

### Host Requirements

| Host OS | Architecture | Min Version |
| --- | --- | --- |
| **macOS** | Apple Silicon (M series) | macOS 13.0+ (Ventura) |
| **Windows** | x64 | Windows 10 (21H2)+ |

> Intel-based Macs are not supported.

### Device & Log Source Support

| Category | Platform | Connection | Host OS | Setup Complexity |
| --- | --- | --- | --- | --- |
| **Mobile** | iPhone / iPad (USB) | USB cable | macOS only | Low |
| **Mobile** | iOS Simulator | Xcode | macOS only | Low |
| **Mobile** | Android Phone (USB) | USB cable | macOS, Windows | Low |
| **Mobile** | Android Emulator | ADB | macOS, Windows | Low |
| **Browser** | Chrome | Playwright (auto) | macOS, Windows | None |
| **Browser** | Firefox | Playwright (auto) | macOS, Windows | None |
| **Browser** | Safari | Playwright (auto) | macOS, Windows | None |
| **Browser** | Android Chrome (USB) | USB + CDP | macOS, Windows | Medium |
| **Browser** | iOS Safari (Wi-Fi) | Wi-Fi proxy | macOS only | Medium |
| **TV / Streaming** | Apple TV | Wi-Fi (Bonjour) | macOS only | Medium |
| **TV / Streaming** | Android TV | ADB over Wi-Fi | macOS, Windows | Low |
| **TV / Streaming** | Android TV Emulator | ADB | macOS, Windows | Low |
| **TV / Streaming** | Fire TV | ADB over Wi-Fi | macOS, Windows | Low |
| **TV / Streaming** | Fire TV (VegaOS) | USB | macOS, Windows | Low |
| **TV / Streaming** | Fire TV (VegaOS) Emulator | ADB | macOS, Windows | Low |
| **TV / Streaming** | Samsung Tizen TV | CDP (IP + Port) | macOS, Windows | Medium |
| **TV / Streaming** | LG webOS TV | CDP (Port) | macOS, Windows | Medium |
| **TV / Streaming** | LG webOS Simulator | CDP (localhost) | macOS, Windows | Medium |

> **Note:** For Smart TVs (Samsung Tizen, LG webOS), the app must be launched in **debug mode** from the respective IDE (Tizen Studio / webOS CLI). The tool connects via Chrome DevTools Protocol (CDP) to capture logs.

---

## Client ID Verification

The tool verifies that you're testing your own app or website. When a capture session starts, the tool checks the `nol_clientid` from the Nielsen SDK config against your registered client IDs.

If there's a mismatch (e.g., you entered a URL belonging to a different client), the capture stops with:

> "Unauthorized — this app belongs to a different client."

This primarily applies to **browser** and **Smart TV** platforms where you enter a URL or connect to a device. For native apps you built yourself, this is unlikely to trigger since you're running your own app.

If you see this error:
- Verify the URL or app uses one of your registered Nielsen client IDs.
- Contact your TAM if you believe your client IDs need updating.

---

## Troubleshooting

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
| Samsung Tizen TV | Cannot connect — debug port or Developer Mode issue | See Interactive Guide |
| LG webOS TV | Cannot connect — ares-inspect not running or wrong port | See Interactive Guide |
| macOS | "NielsenSDKTool" is damaged / can't be opened | [View](docs/TROUBLESHOOTING.md#-macos--general) |
| Auto-Update | Update fails or settings lost | [View](docs/TROUBLESHOOTING.md#-auto-update-issues) |
| All Platforms | No logs — incorrect operation order or debug flag not enabled | [View](docs/TROUBLESHOOTING.md#-before-you-start) |
| All Platforms | Rules stay gray or show red (failed) | [View](docs/TROUBLESHOOTING.md#rules-stay-gray-never-pass-or-fail) |
| All Platforms | "Unauthorized — this app belongs to a different client" | Client ID mismatch — see [Client ID Verification](#client-id-verification) |

---

## Known Limitations

| Limitation | Details |
| --- | --- |
| **Intel-based Macs** | Not supported. Requires **Apple Silicon** (M series). |
| **Apple TV — Wi-Fi only** | Apple TV connectivity is Wi-Fi only (Bonjour discovery → PIN pairing → tunnel). USB log capture is not available for Apple TV. |
| **Domless SDK** | Domless SDK validation is currently supported **only via Fire TV (VegaOS)**. |
| **Smart TV — Debug mode required** | Samsung Tizen and LG webOS require apps to be launched in debug mode from the IDE. The tool cannot capture logs from apps launched normally via the TV's app store. |
| **iOS Safari — Proxy cleanup required** | After testing with iOS Safari (Wi-Fi), you must turn OFF the Wi-Fi proxy on your iPhone. Leaving it on with the tool closed will cause the iPhone to have no internet. |

---

## Support

For assistance, contact your Nielsen Technical Account Manager (TAM).

When reporting issues, please include:
1. **Tool version** (shown in the header or terminal on launch).
2. **Platform** (macOS/Windows) and **OS version**.
3. **Device type** being validated.
4. **Screenshot or export** of the error with reproducible steps.
