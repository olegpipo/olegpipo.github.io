---
title: "Passkeys and Your KeePass Database: Current State"
description: "Yes, KeePass databases can store passkeys. Which KeePass apps support them (KeePassXC, Strongbox, KeePassium, PanicVault), how passkeys are stored in the KDBX file, and how to manage them."
date: 2026-02-14
lastmod: 2026-10-21
draft: false
silo: "Passkeys & Passwordless"
---

The KeePass ecosystem has always stood for principles that matter: open formats, local control, and data portability. As passkeys reshape authentication, KeePass users face a unique question: how does a decentralized, file-based credential system adapt to a technology designed primarily for cloud-synced credential stores? This article, part of our [passkeys and passwordless authentication](/passkeys/) series, examines where KeePass-compatible applications stand on passkey support, how passkeys are stored in a KDBX file, and how to manage your credentials during the transition.

**The short answer: yes, KeePass supports passkeys.** KeePassXC has stored and used passkeys since version 2.7.7 (March 2024), and Strongbox, KeePassium and PanicVault support them on Apple devices. All of them keep passkeys inside the same encrypted `.kdbx` file as your passwords, in a shared format.

## The KeePass Philosophy and Passkeys

The [KeePass ecosystem](/keepass/) is built on a few core principles:

- **Open format**: The KDBX file format is documented and supported by dozens of applications.
- **Local control**: Your database file stays where you put it. No cloud account required.
- **Data portability**: Switch between compatible apps freely. Your data is never locked in.
- **No subscription**: Most KeePass-compatible apps are free or one-time purchase.

These principles do not conflict with passkeys. In fact, they align well with the passkey model in some ways. Passkeys are standardized (FIDO2/WebAuthn), designed for interoperability, and do not inherently require a cloud service. The challenge is implementation: integrating passkey support into the KDBX format and the credential provider frameworks of modern operating systems.

## Current State of Passkey Support

### KDBX Format

The KDBX format was designed for passwords but is extensible: it supports custom fields, attachments, and structured data. Passkeys use that extensibility. KeePassXC defined the format now shared across the ecosystem: each passkey is an ordinary entry whose custom fields, prefixed `KPEX_PASSKEY_`, hold the private key and the passkey's details -- credential ID, relying party (the website), user name and user handle.

Because Strongbox, KeePassium and PanicVault use the same fields, a passkey saved in one KeePass-compatible app is readable in the others. This is consistent with the ecosystem's long-standing commitment to portability.

Storing a passkey is the easy part. Using it to sign in requires the app to answer the browser's WebAuthn request -- either through a browser extension or by registering as a credential provider with the operating system.

### KeePassXC

KeePassXC is the leading open-source desktop KeePass client. Its passkey status:

- **Supported since 2.7.7** (March 2024): KeePassXC can create, store and use passkeys.
- **Storage**: passkeys are saved in `KPEX_PASSKEY_*` attributes on the entry, inside your database.
- **Browser integration**: passkeys work only through the KeePassXC-Browser extension, which handles the website's passkey request in supported browsers.
- **Platform integration**: KeePassXC does not register as a system-level credential provider on macOS or Windows, so its passkeys are not offered to native apps or through the operating system's own passkey prompt.
- **Safari**: No Safari extension exists for KeePassXC, which is a significant limitation for Mac users who prefer Safari.
- **Import and export**: you can export a single passkey as a `.passkey` file and import it with Database > Import Passkey. The exported file is unencrypted JSON, so treat it like a plaintext password export and delete it after use.

### PanicVault

PanicVault occupies a unique position in the KeePass ecosystem: it is built natively for the [Apple ecosystem](/apple/) (macOS, iOS, iPadOS) while maintaining full KDBX compatibility. This native integration gives it several advantages for passkey support:

- **Credential provider extension**: PanicVault integrates with Apple's [credential provider extension framework](/apple/credential-provider-extensions/), which is the mechanism iOS and macOS use to provide passkeys and passwords to apps and browsers.
- **Safari support**: Through the credential provider framework, PanicVault can provide credentials (including passkeys) to Safari without requiring a separate browser extension.
- **Face ID / Touch ID**: Authentication for credential use is handled through [Face ID and Touch ID](/apple/face-id-touch-id-setup/), consistent with how platform-native passkey providers work.
- **KeePassXC format**: PanicVault stores passkey data in the same `KPEX_PASSKEY_` fields, so passkeys created in KeePassXC are visible in PanicVault -- with their relying party, user name and credential ID -- and vice versa. See [Passkeys (WebAuthn)](/help/passkeys/) in the user manual.
- **iCloud Drive sync**: Database files can be synced through [iCloud Drive](/cloud-sync/icloud-sync/), providing the cross-device availability that passkey users expect while maintaining the file-based approach that KeePass users value.

PanicVault represents the bridge between KeePass's open, portable philosophy and the native platform integration that modern authentication requires. For Apple users who want the data portability of KDBX with the passkey experience of iCloud Keychain, it is the most direct solution.

### Strongbox

Strongbox, another KeePass-compatible app on Apple platforms, has supported passkeys since October 2023. On iOS 17 and macOS Sonoma or later, it works as a passkey provider through the system AutoFill and saves passkeys in your KeePass database, in a format compatible with KeePassXC.

### KeePassium

KeePassium added passkey support in version 2.0 (December 2024), on iOS 17 and macOS 14 or later. It stores passkeys in your database using the same format as KeePassXC.

### KeePass 2.x (Windows)

The original KeePass 2.x on Windows has a plugin-based architecture that allows community extensions, so passkey support there depends on third-party plugins. On Windows, KeePassXC is the established way to use passkeys from a KDBX database today.

## The Technical Challenge

Understanding why passkey support in KeePass-compatible apps is more complex than it might seem requires understanding the architecture:

### The Credential Provider Requirement

When a website triggers passkey authentication through the WebAuthn API, the browser asks the operating system for available credentials. The operating system queries registered credential providers. On Apple devices, iCloud Keychain is the default provider, but third-party apps can register through the credential provider extension framework.

For a KeePass app to provide passkeys, it must:

1. Store the passkey's private key, relying party information, and credential ID in the KDBX database.
2. Register as a credential provider with the operating system.
3. Respond to the operating system's credential queries by searching the KDBX database.
4. Perform the cryptographic signing operation using the stored private key when the user authenticates.

This is significantly more complex than password autofill because it involves real-time cryptographic operations and adherence to the FIDO2 protocol's security requirements.

### The Sync Question

Synced passkeys (the default for consumer use) rely on cloud infrastructure to replicate credentials across devices. The KeePass model syncs the entire database file rather than individual credentials. This works well:

- The KDBX file containing passkeys is synced through whatever mechanism the user chooses (iCloud Drive, Google Drive, Dropbox, Syncthing, etc.).
- When a passkey is created or used, the database file is updated.
- The updated file syncs to other devices through the file sync service.

The potential issue is sync latency. If you create a passkey on your iPhone and immediately try to use it on your Mac, the KDBX file needs to have synced. With iCloud Drive, this is usually seconds. With other sync methods, it may take longer.

For a broader discussion of sync options, see our [cloud sync and storage](/cloud-sync/) guides.

### The Key Storage Question

Platform-native passkey implementations lean on secure hardware. On Apple devices, passkeys are iCloud Keychain items, end-to-end encrypted when they sync, whose keys are protected on each device by the [Secure Enclave](/apple/secure-enclave/). Windows Hello passkeys stay on the PC, protected by its TPM. A hardware security key goes furthest: the private key never leaves the key.

KeePass databases store everything in an encrypted file. The private keys are protected by the database's encryption (AES-256 or ChaCha20) and the user's master password, key file or YubiKey. This is strong encryption, but it is software-based: while the database is unlocked, the private key can theoretically be read from memory by malware on the device, which is not possible with a hardware security key. For a closer look at the threat model, see [can passkeys be hacked?](/passkeys/can-passkeys-be-hacked/#passkeys-stored-in-a-keepass-database)

This is a trade-off, not necessarily a weakness. The KeePass model provides portability and user control that hardware-bound storage cannot. The security is still strong -- breaking AES-256 encryption to access the private keys is not feasible. But it is worth understanding the architectural difference.

## Practical Guidance for KeePass Users

Here is how to manage passkeys if you are a KeePass user:

### Strategy 1: Hybrid Approach

Use iCloud Keychain for passkeys and your KeePass database for passwords. This gives you Apple's built-in passkey experience while maintaining the portability and control of KDBX for your password portfolio.

**Advantages**: Zero setup for passkeys. Your Apple Account recovery options cover them.

**Disadvantages**: Credentials split across two systems. Passkeys not in your portable KDBX file.

### Strategy 2: Keep Passkeys in Your KeePass Database

Store passkeys in the same `.kdbx` file as your passwords. On Apple devices, use an app that works as a passkey provider through AutoFill -- PanicVault, Strongbox or KeePassium. On Windows and Linux desktops, use KeePassXC with the KeePassXC-Browser extension. Because they share the `KPEX_PASSKEY_` format, the same database works in all of them.

**Advantages**: All credentials in one place. Full data portability. No cloud account to hijack.

**Disadvantages**: Your master password carries the whole load, so it must be strong. On the desktop, KeePassXC's passkeys work only in browsers with its extension.

### Regardless of Strategy

- Keep your KeePass database backed up. See our [KeePass backup guide](/keepass/backup-database/).
- Maintain strong, unique passwords for all accounts. The [password managers](/password-managers/) landscape is evolving, but password hygiene remains essential.
- Enable [two-factor authentication](/two-factor-authentication/) on accounts where passkeys are not yet available.
- Regularly review which of your accounts now support passkeys -- the list grows monthly. Check our [supported sites directory](/passkeys/supported-sites/).

## What Comes Next

**Moving passkeys between managers.** The FIDO Alliance's Credential Exchange Format reached Proposed Standard status in August 2025, and Apple added direct passkey transfers between credential manager apps in iOS, iPadOS and macOS 26. Whether you can move passkeys from iCloud Keychain or another manager straight into a KeePass database depends on your KeePass app supporting that transfer -- check its documentation. Within the KeePass ecosystem, no transfer is needed: the passkeys travel with the `.kdbx` file.

**Windows integration.** Since November 2025, Windows 11 lets third-party passkey managers plug into Windows Hello. It is up to each KeePass app to adopt it.

For KeePass users, passkeys no longer mean choosing between convenience and the principles that brought them to KeePass. Open formats, local control and data portability apply to passkeys just as they do to passwords.

## Related Articles

- [The Transition: Managing Passwords and Passkeys Together](/passkeys/managing-both/)
- [Can Passkeys Be Hacked? Security Model Explained](/passkeys/can-passkeys-be-hacked/)
- [Passkeys (WebAuthn) in PanicVault](/help/passkeys/)
- [KeePass Encryption Architecture Explained](/keepass/encryption-explained/)
- [KeePass Data Portability](/keepass/data-portability/)
