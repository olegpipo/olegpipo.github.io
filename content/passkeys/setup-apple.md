---
title: "How to Set Up Passkeys on Apple Devices"
description: "Step-by-step guide to creating, using, and managing passkeys on iPhone, iPad, and Mac. Covers iCloud Keychain sync, Face ID, Touch ID, and third-party apps."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Passkeys & Passwordless"
---

Apple was among the first companies to implement passkey support, and their implementation is among the most polished. If you use an iPhone, iPad, or Mac, setting up passkeys is straightforward -- but there are details worth understanding to get the most out of the experience. This guide, part of our [passkeys and passwordless authentication](/passkeys/) resource, walks through everything from initial setup to advanced management.

## Prerequisites

Before creating your first passkey, ensure your devices meet the minimum requirements:

- **iPhone**: iOS 16 or later (iOS 17+ recommended for the best experience)
- **iPad**: iPadOS 16 or later
- **Mac**: macOS Ventura (13) or later
- **Apple Watch**: watchOS 9 or later (for passkey-related notifications)
- **iCloud Keychain**: Must be enabled for passkey syncing across devices
- **Two-factor authentication**: Must be enabled on your Apple ID

If you are using an older device or operating system, you can still use passkeys on individual devices but they will not sync across your Apple devices through iCloud Keychain.

## Enabling iCloud Keychain

Passkeys created on Apple devices are stored in iCloud Keychain and automatically synced across all devices signed into the same Apple ID. If iCloud Keychain is not already enabled, here is how to turn it on:

### On iPhone or iPad

1. Open **Settings**.
2. Tap your name at the top (Apple ID).
3. Tap **iCloud**.
4. Tap **Passwords and Keychain**.
5. Toggle on **Sync this iPhone** (or iPad).

### On Mac

1. Open **System Settings**.
2. Click your name at the top (Apple ID).
3. Click **iCloud**.
4. Click **Passwords and Keychain**.
5. Toggle on **Sync this Mac**.

Once enabled, any passkey you create on one Apple device will appear on all your other Apple devices within seconds. This is what makes the [Apple ecosystem](/apple/) particularly convenient for passkey use -- you set up a passkey once and it works everywhere.

## Creating Your First Passkey

The process varies slightly by website, but the general flow is consistent. Let us walk through creating a passkey for a Google account, which is one of the most common services supporting passkeys.

### Step-by-Step: Creating a Passkey on iPhone

1. Open **Safari** and navigate to [myaccount.google.com](https://myaccount.google.com).
2. Sign in with your existing password if you are not already signed in.
3. Go to **Security** > **How you sign in to Google** > **Passkeys and security keys**.
4. Tap **Create a passkey**.
5. Safari will display a prompt asking if you want to save a passkey for your Google account. Tap **Continue**.
6. Authenticate with [Face ID or Touch ID](/apple/face-id-touch-id-setup/) when prompted.
7. The passkey is created and saved to iCloud Keychain.

That is it. The next time you visit Google's login page, you will see an option to sign in with your passkey. Tap it, confirm with Face ID or Touch ID, and you are authenticated in under two seconds.

### Step-by-Step: Creating a Passkey on Mac

1. Open **Safari** (or Chrome, which also supports passkeys on macOS).
2. Navigate to the website's account security settings.
3. Find and click the option to create a passkey.
4. macOS will display a system prompt asking you to confirm passkey creation.
5. Authenticate with **Touch ID** (on MacBook Pro, MacBook Air, or with a Touch ID keyboard) or your **system password**.
6. The passkey is saved to iCloud Keychain and synced to your other devices.

### What About Non-Safari Browsers?

Chrome on macOS supports passkeys and can store them in iCloud Keychain (as of Chrome 118 and later) or in Google Password Manager. Firefox has added passkey support as well. When you create a passkey in a non-Safari browser, you may be asked to choose where to store it -- iCloud Keychain, the browser's own credential store, or a third-party password manager.

For the most seamless experience across all Apple devices, storing passkeys in iCloud Keychain is the recommended approach. For details on browser-specific behavior, see our guide to [Safari, Chrome, and Firefox on Mac](/apple/safari-chrome-firefox-mac/).

## Using Passkeys to Sign In

Once a passkey is created, using it is simpler than using a password:

### On iPhone

1. Navigate to the website's login page in Safari.
2. Tap the username or email field. If a passkey exists for this site, iOS will display a passkey autofill suggestion above the keyboard (similar to password autofill).
3. Tap the passkey suggestion.
4. Confirm with Face ID or Touch ID.
5. You are signed in.

The entire process takes two to three seconds. There is no password to type, no authenticator app to open, no code to copy.

### On Mac

1. Navigate to the login page.
2. Click the username field. macOS will offer the passkey through the autofill dropdown.
3. Click the passkey option.
4. Confirm with Touch ID or your system password.
5. You are signed in.

### On iPad

The process mirrors the iPhone experience. If the iPad has Face ID, you authenticate with Face ID. If it uses Touch ID (like the iPad Air or iPad mini), you authenticate with Touch ID.

## Managing Your Passkeys

Apple provides a central location for viewing and managing all your passkeys.

### Viewing Passkeys on iPhone or iPad

1. Open **Settings**.
2. Tap **Passwords**.
3. Authenticate with Face ID, Touch ID, or your passcode.
4. You will see a list of all saved credentials. Passkeys are indicated with a key icon next to the account name.
5. Tap any entry to see details, including when the passkey was created and which device created it.

### Viewing Passkeys on Mac

1. Open **System Settings**.
2. Click **Passwords**.
3. Authenticate with Touch ID or your system password.
4. Browse or search for specific passkeys.

Alternatively, on macOS Sonoma and later, you can use the standalone **Passwords** app, which provides a more full-featured interface for managing credentials. For a deeper look at Apple's built-in password management, see our [Apple Passwords app comparison](/apple/apple-passwords-app-comparison/).

### Deleting a Passkey

If you need to remove a passkey (for example, if you are closing an account), navigate to the passkey in your Passwords settings and tap **Delete Passkey**. This removes it from iCloud Keychain and all synced devices. The website will still have your account -- you will just need to use a different authentication method (like a password) to sign in.

## Using Passkeys with Third-Party Password Managers

Apple's iCloud Keychain is not the only option for storing passkeys on Apple devices. Starting with iOS 17 and macOS Sonoma, Apple opened its [credential provider extension framework](/apple/credential-provider-extensions/) to allow third-party apps to store and provide passkeys.

This means password managers like 1Password, Bitwarden, Dashlane, and KeePass-compatible apps can serve as your passkey store. If you already use a password manager for your passwords, storing passkeys in the same app keeps all your credentials in one place.

### Setting Up a Third-Party Passkey Provider

1. Open **Settings** > **Passwords** > **Password Options** (on iPhone/iPad) or **System Settings** > **Passwords** > **Password Options** (on Mac).
2. Under **Use passwords and passkeys from**, select your preferred password manager alongside or instead of iCloud Keychain.
3. When you create a passkey on a website, you will be prompted to choose which credential store to use.

For PanicVault users, this integration means you can store passkeys alongside your traditional KeePass passwords in a single KDBX database, maintaining the data portability that defines the [KeePass ecosystem](/keepass/). For more on this topic, see [passkeys and your KeePass database](/passkeys/keepass-and-passkeys/).

## Cross-Device Authentication

What happens when you need to sign in on a device that does not have your passkeys? Apple supports cross-device authentication through QR codes and Bluetooth.

### Signing in on a Non-Apple Device Using Your iPhone

1. On the device where you need to sign in (for example, a Windows PC), navigate to the website's login page and select the passkey option.
2. The site will display a QR code.
3. Open the camera on your iPhone and scan the QR code.
4. Your iPhone will display a prompt asking if you want to sign in to the website.
5. Confirm with Face ID or Touch ID.
6. The website on the other device authenticates you.

This works because your iPhone communicates with the other device over Bluetooth Low Energy (BLE) to complete the authentication. The devices need to be physically near each other, which provides an additional layer of security against remote attacks.

For more complex cross-platform scenarios, including using passkeys across Apple, Android, and Windows, see our guide on [how to sync passkeys across devices](/passkeys/sync-across-devices/).

## Passkeys and Apple's Ecosystem Advantages

The [Apple ecosystem](/apple/) offers several advantages for passkey users:

**Seamless sync.** iCloud Keychain syncs passkeys across all your Apple devices with end-to-end encryption. No extra setup, no third-party tools needed.

**Biometric integration.** [Face ID and Touch ID](/apple/face-id-touch-id-setup/) provide fast, secure authentication for passkey use. The hardware-backed [Secure Enclave](/apple/secure-enclave/) protects the private keys.

**System-level autofill.** Passkeys work in Safari, other browsers, and native apps through macOS and iOS system autofill. There is no browser extension to install or maintain.

**Apple Passwords app.** The standalone Passwords app (macOS Sonoma and later, iOS 18 and later) provides a visual interface for managing all your credentials including passkeys.

**Third-party extensibility.** The credential provider framework lets you choose where passkeys are stored, so you are not locked into iCloud Keychain if you prefer another solution.

## Common Setup Issues and Solutions

### Passkey Option Does Not Appear

If a website supports passkeys but you do not see the option:
- Ensure you are using a compatible browser (Safari, Chrome, or Firefox on macOS/iOS).
- Check that iCloud Keychain is enabled and syncing.
- Verify your device is running the minimum required OS version.
- Some websites only show passkey options after you have signed in with a password and navigated to security settings.

### Passkey Not Syncing to Other Devices

If a passkey you created on one device is not appearing on another:
- Confirm both devices are signed into the same Apple ID.
- Verify iCloud Keychain is enabled on both devices.
- Check your internet connection -- iCloud Keychain requires a network connection to sync.
- Wait a few minutes. Sync is usually fast but can take time on slow connections.

### Face ID or Touch ID Prompt Not Appearing

If the biometric prompt does not appear when using a passkey:
- Ensure Face ID or Touch ID is set up and functioning in Settings > Face ID & Passcode (or Touch ID & Passcode).
- Restart your device and try again.
- If biometrics fail, the system will fall back to requesting your device passcode.

## Best Practices for Passkeys on Apple Devices

1. **Enable iCloud Keychain on all your Apple devices** so passkeys sync automatically.
2. **Protect your Apple ID** with a strong password and two-factor authentication. Your Apple ID is now the key to your passkeys.
3. **Set up passkeys for your most important accounts first** -- email, banking, cloud storage.
4. **Keep your passwords** even after creating passkeys. Most services maintain password login as a fallback.
5. **Consider a dedicated password manager** for unified credential management, especially if you need cross-platform support or prefer the [data portability of the KeePass format](/keepass/).
6. **Stay updated.** Apple adds passkey improvements with each OS release. Keep your devices on the latest software.

The setup process is simpler than most security improvements. A few minutes spent creating passkeys today eliminates real, ongoing risks from phishing and credential theft. Start with one account, see how it feels, and expand from there.

## Related Articles

- [What Are Passkeys? Complete Guide for 2026](/passkeys/what-are-passkeys/)
- [How to Sync Passkeys Across Devices](/passkeys/sync-across-devices/)
- [Google, Apple, Microsoft Passkey Implementations Compared](/passkeys/google-apple-microsoft/)
- [Face ID and Touch ID Setup Guide](/apple/face-id-touch-id-setup/)
- [Which Websites Support Passkeys in 2026?](/passkeys/supported-sites/)
