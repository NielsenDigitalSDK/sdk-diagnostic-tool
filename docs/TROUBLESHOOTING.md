# Troubleshooting Guide

This guide covers common issues and solutions for the Nielsen SDK Diagnostic Tool across all supported platforms.

---

## ⚡ Before You Start

### Correct Order of Operations

The most common issue is running things in the wrong order. The tool must be **listening before the app launches**, because SDK Init and Config events fire only once — at app startup.

**Correct workflow:**

1. Open the tool and select your device/platform.
2. Select your product type (DCR Video, DCR Static, or DTVR).
3. **Click Play on the test case first.**
4. **Then launch (or relaunch) your app** on the device.

If you launched the app before clicking Play, the tool will miss the SDK Init and Config events. To fix this:
- Close/kill the app completely on the device.
- Make sure the test case is running (Play is active) in the tool.
- Relaunch the app. There is no need to uninstall and reinstall.

> **Re-running the first test case:** If you complete test case 1, move on to test case 2, and then go back to test case 1, the SDK Init/Config events will not fire again unless a fresh SDK instance is created. If you are unsure whether your app creates a new instance, relaunch the app to guarantee those events fire again.

### Debug Flag Requirement

**The app under test must have the Nielsen SDK debug/logging flag enabled.** Without this, the SDK produces no log output and the tool will not capture anything.

- **App SDK (iOS/Android/tvOS):** Verify that `nol_devDebug` is set to `DEBUG` in the SDK initialization options. Other values like `INFO` or `WARN` do not produce the detailed logs the tool needs. If `nol_devDebug` is missing or set to a non-`DEBUG` value, the SDK health test case will fail and no logs will appear.
- **Browser SDK (BSDK):** The tool automatically appends the debug parameter when you enter the URL, so no manual action is needed for browser validation.

> **If you see no logs at all**, the debug flag is the first thing to check. Ask the app developer to confirm that `nol_devDebug` is set to `DEBUG` in their build.

---

## 📱 iPhone / iPad (USB)

### Enable Developer Mode (required for iOS 16+)

If your iPhone or iPad is running iOS 16 or later, Developer Mode must be enabled:

1. Go to **Settings → Privacy & Security → Developer Mode**.
2. Toggle Developer Mode **ON**.
3. The device will prompt you to restart — tap **Restart**.
4. After reboot, confirm the Developer Mode prompt.

> If you don't see the Developer Mode option, connect the device to a Mac with Xcode installed — this makes the option appear.

### Device not detected

- **Unlock your device** — the screen must be awake and unlocked.
- **Tap "Trust"** — when connecting via USB, a "Trust This Computer?" dialog should appear. Tap Trust and enter your passcode.
- **Verify the cable** — use an Apple-certified cable. Some third-party cables are charge-only.
- **Try a different USB port** — avoid USB hubs; plug directly into the Mac.

### "Trust" dialog does not appear

This is the most common iPhone connection issue.

**Step 1: Verify via Console.app**
1. Open **Console.app** on your Mac (Finder → Applications → Utilities → Console).
2. Select your iPhone in the left sidebar.
3. If logs are streaming → macOS can see the device — it's a trust/pairing issue, continue to Step 2.
4. If the iPhone doesn't appear → cable or USB port problem.

**Step 2: Reset Location & Privacy** ✅
1. On iPhone: **Settings → General → Transfer or Reset iPhone → Reset → Reset Location & Privacy**.
2. Enter your passcode when prompted.
3. Disconnect and reconnect the USB cable.
4. The "Trust This Computer?" dialog should now appear — tap **Trust**.

> This fix forces iOS to forget all previous computer pairings and re-prompt. It resolves the majority of "device not detected" cases.

**Step 3: If still not working**
- Restart the iPhone.
- Restart the Mac.
- Try a different USB cable and port.

### No Nielsen SDK logs appearing

- Ensure the app under test is running in the foreground.
- Confirm the app has the Nielsen SDK integrated and `nol_devDebug` is set to `DEBUG` (see [Debug Flag Requirement](#debug-flag-requirement)).
- Check you selected the correct product type (DCR Video, DCR Static, or DTVR).

### "idevicesyslog" errors

- Can happen after macOS updates that change system library paths.
- Restart the tool — the bundled binary should work without external dependencies.

---

## 📱 Android Phone (USB)

### Device not detected

1. **Enable USB Debugging:**
   - Go to **Settings → About Phone** → tap **Build Number** 7 times to unlock Developer Options.
   - Go to **Settings → Developer Options → USB Debugging → ON**.

2. **Authorize the computer:** When you connect via USB, an "Allow USB debugging?" dialog should appear on the phone — tap **Allow**.

3. **Verify ADB sees the device:** The tool runs `adb devices` internally. If the device shows as `unauthorized` instead of `device`, go to **Settings → Developer Options → Revoke USB debugging authorizations**, then reconnect the cable.

### ADB server version mismatch

If Android Studio is running, its ADB server may conflict with the tool's bundled ADB. The tool automatically starts its own ADB server on launch, but if you still see connection issues:

- Close Android Studio.
- Relaunch the tool (it runs `adb kill-server` then `adb start-server` on startup).

---

## 📱 Android Emulator

### Emulator not detected

- Start the emulator from Android Studio **before** opening the tool.
- Emulators appear as `emulator-5554` (or similar) in the device list.
- If the emulator is running but not listed, the tool's ADB server may need a restart. Close and reopen the tool — it automatically restarts ADB on launch.

---

## 📺 Fire TV (Standard — Wi-Fi)

### Cannot connect

1. **Enable ADB Debugging:** Settings → My Fire TV → Developer Options → ADB Debugging → **ON**.
   - If Developer Options is not visible: **Settings → My Fire TV → About → click Serial Number 7 times**.
2. **Find the IP address:** Settings → My Fire TV → About → Network.
3. **Same Wi-Fi network** — your Mac/PC and Fire TV must be on the same local network. The tool connects via `adb connect <IP>:5555`.
4. **Firewall** — ensure port **5555** is not blocked on your network.
5. If connection still fails: toggle ADB Debugging off and on, or restart the Fire TV.

### Connected but no logs

- Ensure the app is running in the foreground on Fire TV.
- Verify you selected **"Fire TV"** (not "Fire TV VegaOS") as the device type.
- Confirm `nol_devDebug` is set to `DEBUG` in the app (see [Debug Flag Requirement](#debug-flag-requirement)).

---

## 📺 Fire TV (VegaOS)

VegaOS is Amazon's newer operating system for certain Fire TV devices. It uses `loggingctl` instead of standard Android `logcat`, which the tool handles automatically.

### No logs appearing

- **USB connection required** — VegaOS log capture works via USB only, not Wi-Fi. The tool runs `adb shell loggingctl log -f` over a USB connection.
- The tool filters for the **BSDKDOMless** marker. If your app does not use the Domless SDK, no logs will appear on this platform. Use standard **"Fire TV"** instead.
- VegaOS logs may arrive concatenated (multiple log entries joined together). The tool splits them automatically by timestamp patterns — no action needed on your end.

---

## 📺 Apple TV (Wi-Fi)

Apple TV uses a 3-step connection process: **Discover → Pair → Connect**. Issues can occur at each step.

### Step 1: No Apple TVs discovered

- **Same Wi-Fi network** — your Mac and Apple TV must be on the same network and subnet.
- **Bonjour not blocked** — corporate/enterprise networks sometimes block mDNS discovery. Try a simpler network if nothing is found. **Tip:** Use your phone's mobile hotspot — connect both your Mac and Apple TV to it as a quick workaround for restrictive office Wi-Fi.
- On first use, the tool downloads a helper binary (`uv`). If this fails, check your internet connection and ensure your firewall is not blocking `github.com`.
- The `uv` binary is cached in `~/.nielsen-sdk-iadt/`. Delete this folder to force a fresh download if you suspect a corrupted install.

### Step 2: Pairing fails or no PIN appears

- A **6-digit PIN** should appear on the Apple TV screen when you initiate pairing.
- If no PIN appears: ensure Apple TV is **awake** and on the home screen (not in screensaver or inside an app).
- Restart Apple TV: **Settings → System → Restart**.
- The PIN is time-sensitive — enter it promptly in the tool.
- Pairing is **persistent** — you do not need to re-pair every time unless the Apple TV is factory reset.

### Step 3: Tunnel fails to start

- The tunnel requires **sudo (admin) access** — enter your Mac login password when prompted.
- If the tunnel doesn't start, check for an existing tunnel process:
  ```
  ps aux | grep tunneld
  ```
- Kill any existing tunnel daemons and retry:
  ```
  sudo pkill -f tunneld
  ```

### Syslog verification fails

- Apple TV may have gone to sleep — wake it up and retry.
- Stop the tunnel in the tool and restart it.
- Ensure **Developer Mode** is enabled on Apple TV: **Settings → Privacy & Security → Developer Mode → ON** (requires restart).

---

## 🌐 Browser (Chrome / Firefox / Safari)

> **Desktop browsers only.** Mobile browser BSDK log capture is not supported — see [Known Limitations](../README.md#%EF%B8%8F-known-limitations) in the README.

### Browser fails to launch

- Playwright browser binaries are automatically installed on first use. This requires an internet connection and approximately 500 MB of disk space.
- If installation fails: check your internet connection, ensure your firewall is not blocking `playwright.azureedge.net`, and verify available disk space.

### URL is required

- You must enter the full URL including the protocol (e.g., `https://example.com/player`).
- The tool opens this URL in a Playwright-controlled browser instance and captures SDK log output automatically.

### Safari / WebKit differences

- Playwright uses **WebKit** (Safari's rendering engine), not the actual Safari application.
- Behavior should be very similar but not identical to Safari.

---

## 🍎 macOS — General

### "NielsenTool" is damaged / can't be opened

This should not happen with the signed and notarized builds. If it does:
- Try: **right-click → Open** (bypasses the first-launch Gatekeeper check).
- If it persists, remove the quarantine attribute:
  ```
  xattr -cr /Applications/NielsenTool.app
  ```

### Port 3000 already in use

If the tool fails to start because port 3000 is occupied:
```
lsof -i :3000
```
Kill the process using that port, then relaunch the tool.

---

## 🔄 Auto-Update Issues

### Update fails

- The tool checks `github.com` for new releases on every launch. An internet connection is required.
- Corporate proxy servers may cause the update check to fail silently — the tool will continue running with the current version.
- **Manual update:** Download the latest version from the [Releases page](https://github.com/NielsenDigitalSDK/sdk-diagnostic-tool/releases/latest) and replace the existing installation.

---

## 🔍 General

### Rules stay gray (never pass or fail)

- Rules only activate when you **click Play** on a test case. If Play is not active, rules remain gray.
- Ensure you selected the correct product type for your content (DCR Video, DCR Static, or DTVR).
- Some rules require a complete playback sequence (play → playhead updates → stop). Perform the full flow described in the test case label.

### Rules show red (failed)

- **Expand the failed rule** to see the FAQ/help text — it explains what the rule expected.
- **Metadata failures:** The rule checks specific metadata field values against expected patterns. Expand the rule to see which fields failed and what the expected format is.
- **Sequence failures:** Events were received in the wrong order. Sequence rules use latching failure — once a sequence fails, it stays red for that session. Click **Reset** in the tool and relaunch the app to retry.
- **Playhead failures:** Playhead values did not meet validation criteria (e.g., playhead not incrementing, unexpected jumps).

> After clicking Reset, all rule states are cleared. You will need to relaunch the app and re-run the test case from the beginning.

---

---

*For additional help, contact the Nielsen Ops/Certification team or your Nielsen Technical Account Manager (TAM).*
