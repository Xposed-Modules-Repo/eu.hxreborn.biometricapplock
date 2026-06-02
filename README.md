<h1 align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/hxreborn/biometric-app-lock/main/assets/banner_dark_medium_trimmed.png">
    <img src="https://raw.githubusercontent.com/hxreborn/biometric-app-lock/main/assets/banner_light_medium_trimmed.png" alt="Biometric App Lock">
  </picture>
</h1>

<p align="center">
  Xposed module that intercepts the launches of a user-defined list of apps at the System Framework level. Those activities are never created until you authenticate via fingerprint or face unlock.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Android-11%2B-3DDC84?style=for-the-badge&logo=android&logoColor=white" alt="Android 11+">
  <img src="https://img.shields.io/badge/libxposed-API_101-ff69b4?style=for-the-badge" alt="libxposed API 101">
  <img src="https://img.shields.io/github/downloads/Xposed-Modules-Repo/eu.hxreborn.biometricapplock/total?style=for-the-badge&logo=github&label=Downloads" alt="Downloads">
</p>

> [!NOTE]
> Built for AOSP and Pixel. Other Android flavors may work if not heavily modified, such as One UI 8+, but others are untested. If you're on HyperOS, OxygenOS, ColorOS, etc. your device already includes a built-in app lock and you probably don't need this.

## About this module

Stock Android never had a native per-app lock, and [Private Space](https://source.android.com/docs/security/features/private-space) (available since Android 15 Beta 2) is a secondary isolated profile where apps run as separate installs with their own data.

This module intercepts activity launches at the system framework level before the target app starts. The Activity is never created until auth succeeds. Tapping a locked app from the recents screen is intercepted too.

A reboot is required after install or update because framework hooks only load at boot (for now 😉). Changing which apps are locked takes effect immediately.

## Requirements

- Android 11+ with an enrolled biometric
- Xposed manager with libxposed API 101 support

## Install

1. Install APK from [Releases](../../releases)
2. Enable module in your Xposed manager with System Framework scope
3. Reboot
4. Select apps to lock in the Apps tab

## Prevent uninstall

Toggle in Settings → Lock & privacy. While on, the module blocks every attempt to uninstall itself, including `adb uninstall` and `pm uninstall`, since it's enforced in the system framework.

> [!IMPORTANT]
> To remove the module with the toggle on:
> 1. Turn it off in the app, then uninstall. No reboot needed.
> 2. If for some reason you can't open the app to disable the toggle, either disable the module in your Xposed manager and reboot or boot to safe mode where Xposed is off and uninstall.

## Reporting issues

About → Links → Share logs exports the module's log lines as a text file and opens a share sheet. Reproduce the issue first, then share via [email](mailto:hxreborn@duck.com), [GitHub issue](https://github.com/hxreborn/biometric-app-lock/issues/new), or [Telegram](https://t.me/hxreb0rn).

Root is required to read the LSPosed logs. If unavailable, the row is disabled. Only this module's own log lines are exported — no other data is gathered. Debug builds are the most useful for diagnosing issues.

## License

[![GPL-3.0-only](https://img.shields.io/badge/LICENSE-GPL--3.0--only-%23A42E2B?style=for-the-badge&logo=gnu&logoColor=white&logoPosition=right)](https://github.com/hxreborn/biometric-app-lock/blob/main/LICENSE)
