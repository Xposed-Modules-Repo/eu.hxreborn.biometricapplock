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
  <img src="https://img.shields.io/badge/Android-13%2B-3DDC84?style=for-the-badge&logo=android&logoColor=white" alt="Android 13+">
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

- Android 13+ with an enrolled biometric
- Xposed manager with libxposed API 101 support

## Install

1. Install APK from [Releases](../../releases)
2. Enable module in your Xposed manager with System Framework scope
3. Reboot
4. Select apps to lock in the Apps tab

## Prevent uninstall

Toggle in Settings → Privacy & stealth. While on, the module blocks every attempt to uninstall itself, including `adb uninstall` and `pm uninstall`, since it's enforced in the system framework.

> [!IMPORTANT]
> To remove the module with the toggle on:
> 1. Turn it off in the app, then uninstall. No reboot needed.
> 2. If for some reason you can't open the app to disable the toggle, either disable the module in your Xposed manager and reboot or boot to safe mode where Xposed is off and uninstall.

## Block screenshots

Toggle it globally in Settings or per app in its detail screen. Changes apply immediately, no reboot or hot reload. While on, an unlocked locked app's screenshots, screen recording, and recents preview are blocked. The per-app setting overrides the global one, so an app can stay blocked with the global toggle off. It cannot beat modules that force FLAG_SECURE off, like Disable Flag Secure by aviraxp.

After you turn the block off, that app's recents card can stay blank since the system cached it while the block was on. Swipe it off recents and reopen the app for a fresh preview.

## Reporting issues

Settings → About → Export logs saves the module's log lines to a text file and opens a share sheet, so you can attach them to a [GitHub issue](https://github.com/hxreborn/biometric-app-lock/issues/new), send them by [email](mailto:hxreborn@duck.com), or share via [Telegram](https://t.me/hxreb0rn). Reproduce the issue first, then export.

Reading the LSPosed logs needs root. Only this module's own log lines are exported, so they're safe to attach to a public issue. Debug builds help me most.

## License

[![GPL-3.0-only](https://img.shields.io/badge/LICENSE-GPL--3.0--only-%23A42E2B?style=for-the-badge&logo=gnu&logoColor=white&logoPosition=right)](https://github.com/hxreborn/biometric-app-lock/blob/main/LICENSE)
