---
title: "How to Sync Passkeys Across Devices"
description: "Guide to syncing passkeys across Apple, Android, and Windows devices. Covers iCloud Keychain, Google Password Manager, cross-device QR authentication, and third-party managers."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Passkeys & Passwordless"
---

One of the most practical concerns about passkeys is portability: how do you use a passkey created on your iPhone when you need to log in on your Mac, a Windows PC, or a friend's computer? The answer depends on your device ecosystem and credential storage strategy. This guide, part of our [passkeys and passwordless authentication](/passkeys/) resource, covers every syncing scenario and provides practical recommendations.

## How Passkey Syncing Works

Unlike passwords, which are simple text strings that can be stored anywhere, passkeys involve cryptographic key pairs. The private key must be protected by secure hardware or strong encryption, and the sync mechanism must maintain that protection in transit and at rest.

There are three approaches to making passkeys available across devices:

1. **Cloud credential sync** -- The passkey is encrypted and stored in a cloud credential manager that syncs across devices.
2. **Cross-device authentication** -- The passkey stays on one device, and that device authenticates on behalf of another device nearby.
3. **Third-party credential manager** -- A password manager stores passkeys in its own vault and provides them across platforms.

Each approach has trade-offs in convenience, security, and platform coverage.

## Apple iCloud Keychain Sync

For users within the [Apple ecosystem](/apple/), iCloud Keychain provides the most seamless passkey syncing experience.

### How It Works

When you create a passkey on any Apple device, it is automatically encrypted and uploaded to iCloud Keychain. The passkey then syncs to all your other Apple devices signed into the same Apple ID. The sync is:

- **End-to-end encrypted**: Apple cannot read your passkeys. The encryption keys are derived from your device passcodes.
- **Automatic**: No manual steps required after initial iCloud Keychain setup.
- **Fast**: Passkeys typically appear on other devices within seconds.

### Setup Requirements

- All devices signed into the same Apple ID.
- iCloud Keychain enabled on each device (Settings > Apple ID > iCloud > Passwords and Keychain).
- [Two-factor authentication](/two-factor-authentication/) enabled on your Apple ID.
- Minimum OS versions: iOS 16, iPadOS 16, macOS Ventura.

### What Syncs

Passkeys, passwords, WiFi credentials, credit cards, and other iCloud Keychain items all sync through the same mechanism. For setup instructions, see our guide to [setting up passkeys on Apple devices](/passkeys/setup-apple/).

### Limitations

iCloud Keychain only syncs within the Apple ecosystem. If you need a passkey on an Android phone or a Linux computer, iCloud Keychain cannot provide it natively. There is a basic iCloud Passwords extension for Chrome on Windows, but it has limitations. For cross-platform needs, you will need cross-device authentication or a third-party manager.

## Google Password Manager Sync

Google's approach mirrors Apple's within the Android and Chrome ecosystem.

### How It Works

On Android devices (9+), passkeys are stored in Google Password Manager and synced across devices signed into the same Google account. On any desktop, Chrome can also store passkeys in Google Password Manager.

### Setup Requirements

- Google account with a screen lock enabled on Android devices.
- Chrome signed into the same Google account on desktop.
- Android 9+ for mobile devices.

### What Syncs

Passkeys and passwords stored in Google Password Manager sync across Android devices and Chrome installations. The sync uses Google's infrastructure with encryption.

### Limitations

Google Password Manager is tightly coupled to Chrome on desktop. If you prefer Safari or Firefox, the passkeys in Google Password Manager are not natively accessible through those browsers. On iOS, Google Password Manager is not a system-level credential provider, so Google-stored passkeys are not available for autofill in Safari.

For a detailed comparison of how Google, Apple, and Microsoft handle passkeys, see [Google, Apple, Microsoft passkey implementations compared](/passkeys/google-apple-microsoft/).

## Cross-Device Authentication (QR + Bluetooth)

When you need to use a passkey on a device that does not have it -- say, logging into a website on a Windows PC but your passkey is on your iPhone -- the FIDO Alliance's hybrid transport protocol handles this.

### How It Works

1. The website on Device A (the one without the passkey) displays a QR code when you select the passkey login option.
2. You open the camera on Device B (your phone, which has the passkey) and scan the QR code.
3. Device B displays a prompt asking if you want to sign in to the website shown.
4. You authenticate with biometrics ([Face ID, Touch ID](/apple/face-id-touch-id-setup/), or fingerprint) on Device B.
5. Device B communicates the authentication to Device A over Bluetooth Low Energy (BLE).
6. Device A receives the authentication and you are logged in.

### Requirements

- Both devices must have Bluetooth enabled.
- The devices must be physically near each other (Bluetooth range, typically 10-15 meters).
- The phone must have the passkey and a supported OS.

### Security Properties

The Bluetooth proximity requirement is a deliberate security feature. It prevents remote phishing scenarios where an attacker could trick you into authenticating for a distant session. The QR code contains connection information, and the Bluetooth handshake confirms physical proximity.

### When to Use This

Cross-device authentication is ideal for:

- **Logging in on a friend's or public computer** without installing anything.
- **Using a passkey from your iPhone on a Windows PC** that does not have your credential store.
- **Temporary device access** where you do not want to sync credentials permanently.

It is less ideal for daily use on devices you own, where synced passkeys (through iCloud Keychain, Google Password Manager, or a third-party manager) provide a faster experience.

## Third-Party Password Managers

Password managers that support passkeys provide the most flexible cross-platform syncing. Instead of being tied to one platform's credential store, your passkeys live in the password manager's vault and are available wherever the manager runs.

### How It Works

1. When a website offers passkey creation, the password manager intercepts the WebAuthn request.
2. The passkey is generated and stored in the manager's encrypted vault.
3. The vault syncs across all devices where the manager is installed.
4. When authentication is needed, the manager provides the passkey through the operating system's credential provider framework or browser extension.

### Managers with Passkey Support

| Manager | Platforms | Passkey Sync |
|---|---|---|
| 1Password | macOS, iOS, Windows, Android, Linux, browsers | Full cross-platform |
| Bitwarden | macOS, iOS, Windows, Android, Linux, browsers | Full cross-platform |
| Dashlane | Browser extensions, iOS, Android | Full cross-platform |
| PanicVault | macOS, iOS, iPadOS | Apple ecosystem via iCloud Drive or Google Drive |
| Strongbox | macOS, iOS | Apple ecosystem |

For KeePass-compatible tools like PanicVault, the passkey is stored in your [KDBX database file](/keepass/), which can be synced through any [cloud storage service](/cloud-sync/) -- iCloud Drive, Google Drive, Dropbox, or even a local network. This gives you maximum control over where your data lives.

For a detailed overview of how the industry is handling this transition, see [how password managers are adapting to passkeys](/passkeys/password-managers-adapting/).

### Advantages of Third-Party Managers

- **True cross-platform**: One manager works on every device and OS.
- **Unified credential view**: Passkeys, passwords, TOTP codes, and notes in one place.
- **Organizational features**: Tags, folders, search, and security auditing.
- **Data portability**: Export your credentials if you switch managers (though passkey export standards are still evolving).

### Disadvantages

- **Additional software**: One more app to install and maintain on every device.
- **Another account to protect**: The manager's master password or account passkey becomes a critical security dependency.
- **Potential friction**: On some platforms, third-party credential providers may not integrate as smoothly as the native option.

## Platform-Specific Syncing Strategies

### All Apple Devices

**Recommended**: iCloud Keychain for passkeys. Optionally, a KeePass-compatible app like PanicVault for password management with KDBX portability.

This is the simplest setup. iCloud Keychain handles passkey creation, storage, and sync automatically. [Face ID](/apple/face-id-touch-id-setup/) on iPhone and Touch ID on Mac provide fast authentication. Everything works in Safari and native apps without browser extensions.

### Apple + Windows

**Recommended**: Either a third-party password manager with passkey support across both platforms, or iCloud Keychain on Apple with cross-device QR authentication for Windows.

If your Windows use is occasional, QR-based authentication from your iPhone works fine. If you regularly use both platforms, 1Password or Bitwarden provides a more seamless daily experience.

### Apple + Android

**Recommended**: A third-party password manager. Neither iCloud Keychain nor Google Password Manager works well across this divide.

If you carry both an iPhone and an Android device, having your passkeys in a manager available on both is significantly less friction than constantly using QR codes.

### All Android / Chrome

**Recommended**: Google Password Manager. It syncs automatically across Android devices and Chrome on any platform.

### Mixed (Three or More Platforms)

**Recommended**: A third-party password manager with full cross-platform support. Managing separate credential stores for each platform becomes unwieldy with three or more ecosystems.

## Troubleshooting Sync Issues

### Passkey Not Appearing on Another Device

1. **Verify same account**: Ensure both devices are signed into the same Apple ID, Google account, or password manager account.
2. **Check sync is enabled**: On Apple, verify iCloud Keychain is enabled on both devices.
3. **Network connection**: Cloud sync requires an active internet connection. Try connecting to WiFi and waiting a few minutes.
4. **Restart the app**: Close and reopen your password manager or the Passwords app on both devices.
5. **Check OS version**: Ensure both devices meet minimum OS requirements for passkey support.

### Cross-Device QR Code Not Working

1. **Enable Bluetooth**: Both devices need Bluetooth turned on.
2. **Proximity**: Ensure the devices are within Bluetooth range (within a few meters).
3. **Camera permissions**: The phone scanning the QR code needs camera access.
4. **Try again**: Sometimes the BLE handshake fails on the first attempt. Re-display the QR code and scan again.

### Passkey Works on One Browser but Not Another

Different browsers may use different credential stores. A passkey saved in Chrome's Google Password Manager is not available in Safari's iCloud Keychain and vice versa. Consider storing passkeys in a third-party manager that works across all browsers, or ensure you create passkeys in your preferred credential store.

## Future Developments

The FIDO Alliance is working on several improvements to passkey syncing:

**Credential exchange protocol**: A standard format for transferring passkeys between credential providers. This would allow you to move passkeys from iCloud Keychain to 1Password, or from Google Password Manager to a KeePass database, without recreating them.

**Multi-provider interoperability**: Improved protocols for having multiple credential providers (e.g., iCloud Keychain and 1Password) coexist on the same device without conflicting.

**Enterprise credential distribution**: Mechanisms for organizations to provision passkeys to employee devices centrally.

These developments will significantly improve the passkey syncing experience over the next few years. For now, choosing your credential storage strategy thoughtfully and sticking with it provides the most reliable experience. For the latest on adoption trends, see our [passkey adoption statistics](/passkeys/adoption-statistics/).

## Related Articles

- [How to Set Up Passkeys on Apple Devices](/passkeys/setup-apple/)
- [Google, Apple, Microsoft Passkey Implementations Compared](/passkeys/google-apple-microsoft/)
- [How Password Managers Are Adapting to Passkeys](/passkeys/password-managers-adapting/)
- [The Transition: Managing Passwords and Passkeys Together](/passkeys/managing-both/)
- [Cloud Sync for Password Databases](/cloud-sync/)
