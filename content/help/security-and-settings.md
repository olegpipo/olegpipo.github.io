---
title: "Security & Settings"
description: "Configure PanicVault security: Face ID and Touch ID unlock, lock timeout, clipboard auto-clear, Universal Clipboard, appearance, and memory protection."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Settings"
weight: 150
---

PanicVault's app-wide settings control how your vaults are unlocked, how long they stay unlocked, and how copied values are handled. This page covers every option on the Settings screen, which you reach by tapping the gear icon on the home screen.

## Biometric Unlock (Face ID / Touch ID)

Enable biometric unlock to use Face ID (iPhone/iPad with Face ID) or Touch ID (Mac, or older iPhones/iPads) to unlock your vault without typing your master password.

1. Go to **Settings**
2. Toggle **Unlock with Face ID** (or Touch ID)
3. The next time you unlock with your master password, it is securely stored in the device Keychain
4. Subsequent unlocks can use biometrics

Your master password is stored in the iOS/macOS Keychain, protected by the Secure Enclave. It is never sent anywhere.

{{< callout type="tip" >}}
Even with biometric unlock enabled, PanicVault periodically requires your master password to make sure you still remember it (see "Master Password Re-entry" below).
{{< /callout >}}

## Lock Timeout

Choose how long PanicVault waits before locking your vault:

- 30 seconds
- 1 minute (default)
- 2 minutes
- 5 minutes
- Never

This timeout applies both to inactivity within the app and to time spent in the background. When you switch away from PanicVault, the timer starts counting down. If you return before it expires, the vault stays unlocked. The vault never auto-locks while you are actively using the app.

For more on when and how locking happens, see [Managing Your Vault](/help/managing-your-vault/).

## Clipboard Auto-Clear

When you copy a password or other sensitive value, PanicVault automatically clears your clipboard after a set time:

- 15 seconds
- 30 seconds (default)
- 1 minute
- Never

## Universal Clipboard (Continuity)

PanicVault can use Apple's Universal Clipboard (also called Continuity Copy & Paste) to share copied values between your Apple devices. When enabled, passwords and other values you copy on one device are available to paste on your other nearby devices signed in to the same Apple ID.

You can toggle this on or off in **Settings**. When disabled, copied values stay on the local device only. This can be useful if you want to prevent sensitive data from being transmitted to other devices on your network.

## Appearance

Choose the visual theme for PanicVault:

- **System** (default) -- follows your device's Light/Dark mode setting
- **Light** -- always uses the light theme
- **Dark** -- always uses the dark theme

The appearance setting is found in **Settings** on the home screen.

## Master Password Re-entry

Even with biometric unlock enabled, PanicVault requires you to type your master password periodically. This ensures you do not forget it. Options:

- Every 7 days
- Every 14 days (default)
- Every 30 days
- Always (every unlock requires the master password)

When the re-entry period has elapsed, the biometric option is temporarily hidden on the lock screen.

## Memory Protection

Memory protection settings (configured per-vault in [Database Settings](/help/vault-settings/)) control which fields are encrypted in memory using the inner stream cipher. By default, only the Password field is protected. You can also protect:

- Title
- Username
- URL
- Notes

These settings affect how data is stored in the .kdbx file and are compatible with KeePass and KeePassXC. See [KeePass Compatibility](/help/keepass-compatibility/) for more on what PanicVault preserves.
