---
title: "KeePass Apps for Every Platform: Which Apps Open .kdbx Files (2026)"
description: "Which apps open KeePass .kdbx databases on Windows, Mac, Linux, Android and iPhone, which KDBX versions and ciphers each one reads, and how to share one database between them."
date: 2026-02-13
lastmod: 2026-10-21
draft: false
silo: "KeePass & Open Standards"
aliases:
  - /keepass/compatibility-guide/
faq:
  - q: "Which apps can open a KeePass .kdbx file?"
    a: "On Windows, KeePass 2.x and KeePassXC. On Mac, KeePassXC, MacPass, and App Store apps such as Strongbox, KeePassium and PanicVault. On Linux, KeePassXC. On Android, KeePassDX and Keepass2Android. On iPhone and iPad, PanicVault, Strongbox and KeePassium. All of them read KDBX 4, the current format; PanicVault reads KDBX 4 only."
  - q: "What is the difference between KDBX 3.1 and KDBX 4?"
    a: "KDBX 4, introduced in KeePass 2.35, added the Argon2 key derivation function, the ChaCha20 cipher and HMAC-authenticated data blocks. KDBX 3.1 supports only AES-KDF. Every maintained KeePass app reads KDBX 4, so it is the better choice unless you still depend on an app that reads only 3.1."
  - q: "Can different KeePass apps use the same database?"
    a: "Yes, as long as each app supports the database's format version, cipher and key derivation function. Keep the file in one synced folder and avoid editing it on two devices before changes have synced. KeePass 2.x, KeePassXC and PanicVault can merge two copies that have drifted apart."
  - q: "Do TOTP codes and YubiKeys work across KeePass apps?"
    a: "Usually, but test them. TOTP secrets live in entry fields whose names differ between apps, so a code set up in one app may not appear in another. A YubiKey challenge-response database made in KeePassXC opens in Strongbox, KeePassium and PanicVault, but the KeeChallenge plugin for KeePass 2.x uses a different scheme."
---

A KeePass database is not tied to the program that created it. Because the KDBX format is documented and openly implemented, a `.kdbx` file made in KeePass on Windows opens in KeePassXC on Linux, KeePassDX on Android and an iPhone app such as PanicVault, with no export or conversion. You choose the software that fits each device, and you can switch at any time without losing a single entry.

This guide lists the apps worth using on each platform, which format versions, ciphers and key derivation functions each one reads, and what to check before you share one database between several of them.

> **Quick answer**: On **Windows**, use KeePass 2.x or KeePassXC. On **Mac**, KeePassXC, or an App Store app such as Strongbox or PanicVault. On **Linux**, KeePassXC. On **Android**, KeePassDX or Keepass2Android. For **iPhone and iPad** there is no official KeePass app; see our guide to [KeePass for iPhone](/keepass/keepass-ios/). To use one database everywhere, save it as KDBX 4 with AES-256 or ChaCha20 and Argon2, and avoid Twofish.

## KeePass Database Versions in Brief

Before choosing apps, it helps to know which [KDBX version](/keepass/kdbx-format-guide/) your database uses:

- **KDB (KeePass 1.x)** -- The original format, now legacy. Most current apps can import it; only some open it directly.
- **KDBX 3.1** -- The long-standing KeePass 2.x format. It supports only the AES-KDF key derivation function.
- **KDBX 4.x** -- The current format, introduced in KeePass 2.35. It adds Argon2 key derivation, the ChaCha20 cipher and HMAC-authenticated data blocks. KDBX 4.1 (KeePass 2.48) is a minor revision.

Every maintained app below reads KDBX 4. KeePass 2.x, however, keeps saving a database as KDBX 3.1 until it needs version 4 -- typically when you switch its key derivation function to Argon2. Our format guide shows [how to check and upgrade a database to KDBX 4](/keepass/kdbx-format-guide/#how-to-upgrade-a-database-to-kdbx-4).

## Desktop Applications

### KeePass 2.x (Windows)

KeePass Password Safe is the original application that created the format. Developed by Dominik Reichl and first released in 2003, it remains actively maintained and is the reference implementation of KDBX.

**Platform**: Windows (runs on Linux and macOS via Mono)
**Format support**: KDBX 3.1 and KDBX 4.x; KeePass 1.x `.kdb` files through File > Import
**License**: GPL v2 or later (open source)

KeePass has the deepest feature set of any compatible application. Its plugin architecture supports hundreds of extensions: browser integration, cloud storage adapters, importers for other password managers, extra ciphers such as Twofish, and hardware-key schemes such as KeeChallenge. Auto-Type works system-wide on Windows, typing credentials into any application, not just browsers. It also generates TOTP codes without a plugin, from its own `TimeOtp-` entry fields: version 2.47 added the `{TIMEOTP}` placeholder for Auto-Type, and version 2.51 added menu commands to show and copy codes.

The trade-off is the interface, which looks and feels like a classic Windows utility. And plugins only run in KeePass itself: a database that depends on one (a Twofish-encrypted file, a KeeChallenge YubiKey setup) will not open in other apps.

### KeePassXC (Windows, macOS, Linux)

KeePassXC is a community-driven, cross-platform client that began as a fork of KeePassX (now discontinued). It is widely used on Linux and macOS and a common choice on Windows.

**Platforms**: Windows, macOS, Linux
**Format support**: KDBX 3.1 and KDBX 4.x; KeePass 1.x `.kdb` files through Database > Import
**License**: GPL v2 or v3 (open source)

KeePassXC is written in C++ with the Qt framework, so it needs neither Mono nor .NET and feels at home on all three platforms. It includes browser integration through the KeePassXC-Browser extension, an SSH agent, TOTP codes, a password generator with passphrases, YubiKey and OnlyKey challenge-response, and quick unlock with Touch ID on macOS or Windows Hello on Windows.

It is the default recommendation for desktop users who want an [open-source client](/keepass/open-source-security/) without plugins.

### MacPass (macOS)

MacPass is a native macOS client.

**Platform**: macOS only
**Format support**: KeePass 1.x `.kdb`, KDBX 3.1, KDBX 4.x (including Twofish)
**License**: GPL v3 (open source)

MacPass has a clean macOS interface with sidebar navigation, auto-type, custom icons and file attachments. Development is slower than KeePassXC's, but it remains an option for people who want a lightweight Mac-only client.

### KeeWeb (Barely Maintained)

KeeWeb is an Electron desktop app that also runs in a web browser, and for years it was the most visually polished KeePass client. Its last stable release, 1.18.7, came out in July 2021; since then the project has seen only occasional pre-release builds with small fixes. We no longer recommend it for new setups; KeePassXC covers the same desktop platforms.

## Android Applications

### KeePassDX

KeePassDX is the leading KeePass client for Android, built around Material Design.

**Platform**: Android
**Format support**: KeePass 1.x `.kdb`, KDBX 3.1, KDBX 4.x
**License**: GPL v3 or later (open source)

KeePassDX fills credentials through Android's autofill framework and includes a built-in keyboard for apps that do not support autofill. It unlocks with a fingerprint, generates TOTP codes and handles attachments. YubiKey challenge-response works through the separate Key Driver app; the project's wiki still describes hardware-key support as a beta feature, and says a database set up in KeePassXC opens in KeePassDX. It opens databases through any Android storage provider (Google Drive, Dropbox, Syncthing, Nextcloud and others), so syncing is left to the storage app of your choice.

### Keepass2Android

Keepass2Android is a long-established Android client with a loyal user base.

**Platform**: Android
**Format support**: KeePass 1.x `.kdb`, KDBX 3.1, KDBX 4.x
**License**: GPL v3 (open source)

It has built-in access to Dropbox, Google Drive, OneDrive, SFTP, WebDAV and more, autofill, fingerprint unlock, and QuickUnlock, which reopens the database with the last few characters of your master password. An offline variant, Keepass2Android Offline, drops network access entirely. Since version 1.06 it also supports KeePassXC-style YubiKey challenge-response, for KDBX 4 databases.

## iPhone, iPad and Mac App Store Apps

The KeePass project makes no iOS app, and neither does KeePassXC. Three independent apps are worth using: **[PanicVault](https://apps.apple.com/app/id6759188575)**, **Strongbox** and **KeePassium**. All three open KDBX 4 databases, fill passwords through iOS AutoFill, unlock with Face ID (a Pro feature in Strongbox), and have Mac versions; Strongbox and KeePassium also read KDBX 3.1 and KeePass 1.x files, while PanicVault reads KDBX 4 only. Our guide to [KeePass for iPhone](/keepass/keepass-ios/) compares them for people bringing a database over from a Windows PC, and [Strongbox vs KeePassium vs KeePassXC](/compare/keepass-apps-apple/) covers the Mac side.

## Browser Integration

On the desktop, browser filling usually comes from an extension that talks to the app holding your open database:

- **KeePassXC-Browser** -- The official extension for KeePassXC, for Chrome, Chromium, Vivaldi, Brave, Firefox, Tor Browser and Edge. It talks to KeePassXC over a local, encrypted channel, so nothing leaves your machine. This is the most widely used browser integration in the ecosystem.
- **Kee** (formerly KeeFox) -- A Firefox and Chrome extension that connects to KeePass 2.x through the KeePassRPC plugin.
- **KeePassHttp** -- An older KeePass 2.x plugin whose own README warns of a point where the encryption keys can be stolen. KeePassRPC with Kee, or KeePassXC with KeePassXC-Browser, are the usual choices today.

On phones and tablets there is no extension to install: the app fills passwords through the operating system's autofill service.

## Format and Encryption Support by App

The cipher and key derivation function are stored in your database's header, and every app that opens the file must support both. This matrix covers the apps above.

| App | Platforms | KDBX 4 | KDBX 3.1 | KeePass 1.x .kdb | AES-256 | ChaCha20 | Twofish | Argon2 |
|---|---|---|---|---|---|---|---|---|
| KeePass 2.x | Windows | Yes | Yes | Import | Yes | Yes | Plugin | Yes |
| KeePassXC | Windows, Mac, Linux | Yes | Yes | Import | Yes | Yes | Yes | Yes |
| MacPass | Mac | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| KeePassDX | Android | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Keepass2Android | Android | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Strongbox | iPhone, iPad, Mac | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| KeePassium | iPhone, iPad, Mac | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| PanicVault | iPhone, iPad, Mac | Yes | No | No | Yes | Yes | No | Yes |

Every app in the table also supports AES-KDF, the key derivation function KDBX 3.1 databases use. "Import" means the app converts a `.kdb` file into a new `.kdbx` database rather than opening it directly.

**KDBX 4 is now universal among maintained apps.** The days when KDBX 3.1 was needed for compatibility are over, though older copies of KeePass 2.x (before 2.35) and some unmaintained apps still read only 3.1.

**Twofish is the cipher to avoid when sharing.** KeePass 2.x needs the Twofish Cipher plugin to use it, and PanicVault does not support it. AES-256 and ChaCha20 work in every app above.

**Argon2 comes with KDBX 4.** Any app that reads KDBX 4 also handles Argon2 key derivation. Argon2id, a later variant, is not supported by some older app versions, so check every app before switching to it.

## Features Compared

| Feature | KeePassXC | KeePass 2.x | KeePassDX | Strongbox | PanicVault | KeePassium |
|---|---|---|---|---|---|---|
| **Windows** | Yes | Yes | -- | -- | -- | -- |
| **macOS** | Yes | Via Mono | -- | Yes | Yes | Yes (Mac Catalyst) |
| **Linux** | Yes | Via Mono | -- | -- | -- | -- |
| **Android** | -- | -- | Yes | -- | -- | -- |
| **iPhone / iPad** | -- | -- | -- | Yes | Yes | Yes |
| **Browser filling** | Via extension | Via plugin | -- | -- | -- | -- |
| **System autofill** | -- | -- | Android | iOS, macOS (Mac: Pro) | iOS, macOS | iOS |
| **TOTP** | Yes | Yes (2.47+) | Yes | Yes | Yes | Yes |
| **YubiKey** | Yes | Via plugin | Via Key Driver (beta) | Pro | iPhone NFC, Mac USB | Premium |
| **Biometric unlock** | Touch ID, Windows Hello | Via plugin | Fingerprint | Face/Touch ID (Pro) | Face/Touch ID | Face/Touch ID |
| **Open source** | Yes | Yes | Yes | Source published* | No | Source published* |
| **Price** | Free | Free | Free | Freemium | One-time purchase | Freemium |

\*Source code is public, but App Store builds can't be verified against it.

## Features That Behave Differently Between Apps

The KDBX format defines how entries, groups, custom fields, attachments and history are stored, and those carry across reliably. Some popular features are conventions on top of the format, and that is where apps differ.

### TOTP Codes

Two-factor (TOTP) secrets are stored in ordinary entry fields, and different apps use different field names. KeePassXC stores an `otpauth://` URI in a field named `otp`, which most other apps also read. KeePass 2.x's built-in TOTP uses fields named `TimeOtp-Secret-Base32` and similar, and the older KeeTrayTOTP plugin used `TOTP Seed` and `TOTP Settings`. PanicVault, Strongbox and KeePassium read all three conventions, and KeePassXC has read KeePass's fields since version 2.7.10 -- though KeePassXC and KeePassium read only the Base32 form of KeePass's secret field. If you set up codes in one app, open a few entries in each other app and check that the same code appears.

### Hardware Keys (YubiKey Challenge-Response)

A database can require a YubiKey's HMAC-SHA1 challenge-response as part of its master key, alongside the password and any key file. This is an application convention rather than a format feature: nothing in the file records that a hardware key is needed, so each app has to be told. KeePassXC, Strongbox, KeePassium and PanicVault use the same scheme, so one YubiKey-protected database opens in any of them -- PanicVault reads the key over NFC on iPhone and over USB on Mac. On Android, Keepass2Android supports the same scheme for KDBX 4 databases, and KeePassDX does through its Key Driver app. The KeeChallenge plugin for KeePass 2.x works differently, keeping an encrypted copy of the secret in a separate `.xml` file, and it is not interchangeable with the others.

### Plugin Data and App-Specific Settings

KeePass 2.x plugins and Auto-Type only do anything in KeePass itself, and KeePassXC keeps its browser-integration keys inside the database. Data like this travels with the file, and an app that preserves what it does not use leaves it in place for when you reopen the file in the original app; PanicVault, for example, preserves custom fields and Auto-Type configuration when it saves. What does not carry over is anything a plugin needs in order to decrypt the file, such as the Twofish cipher or KeeChallenge.

## Before You Share a Database Between Apps

When several apps or people use one `.kdbx` file, run through this checklist:

1. **Check format support.** Open the database in every app before you standardise on a format version.
2. **Check the cipher and key derivation function.** Confirm every app supports both, using the matrix above.
3. **Check the unlock time on your slowest device.** Argon2's memory setting has to fit every device that opens the file; a phone may refuse, or take much longer, with a setting tuned on a desktop. 64 MB is a reasonable starting point.
4. **Check feature fidelity.** After opening the database in a second app, confirm that custom fields, attachments, groups and TOTP codes look right.
5. **Watch for silent upgrades.** Changing the key derivation function or cipher in KeePass 2.x can switch the file to KDBX 4, which older apps cannot read.
6. **Know how each app handles changes made elsewhere.** KeePass 2.x checks whether the file changed before it saves and offers to [synchronize](https://keepass.info/help/v2/sync.html) the two versions entry by entry. KeePassXC can merge another copy into the open database with **Database > Merge From Database**; for entries that exist in both, the most recently modified version wins and the older one goes into the entry's history. PanicVault merges changes another app or device saved before it writes the file. A separate "conflicted copy" created by your sync service is not merged automatically by any of them; open it and merge it by hand. See [resolving sync conflicts](/cloud-sync/sync-conflicts/).

## Recommended Setups

- **Desktop plus Android** (for example KeePassXC and KeePassDX): KDBX 4, AES-256 or ChaCha20, Argon2.
- **A family on mixed apps** (KeePassXC, an iPhone app, Keepass2Android): KDBX 4, AES-256, Argon2 with memory set for the least powerful device.
- **PanicVault alongside anything else**: KDBX 4 with AES-256 or ChaCha20 and Argon2d, Argon2id or AES-KDF; no Twofish.
- **An app you depend on reads only KDBX 3.1**: KDBX 3.1 with AES-256 and AES-KDF, tuned to about a second on your slowest device, and plan to move to KDBX 4.

## Syncing One Database Across Devices

Because the database is a single encrypted file, any file sync tool works: iCloud Drive, Dropbox, Google Drive, OneDrive, Syncthing, Nextcloud or WebDAV. Our guide to [syncing your password database across devices](/cloud-sync/sync-across-devices/) compares the options.

## Which App Should You Use?

### Windows

**KeePassXC** is the default recommendation: a modern interface and built-in browser integration with no plugins to manage. Choose the original **KeePass 2.x** if you need a particular plugin or the deepest configurability.

### macOS

**KeePassXC** if you want the same open-source app on every desktop. An App Store app if you want a native Mac app that also covers your iPhone: **[PanicVault](https://apps.apple.com/app/id6759188575)** for a modern design, sold as a one-time purchase, with every commit adversarially audited by Fable ([how the continuous audit works](/engineering/ai-code-audit-fable-5/)); **Strongbox** for the most sync providers and settings. **MacPass** if you prefer a lightweight Mac-only client.

### Linux

**KeePassXC** is the clear leader, with packages for every major distribution plus Flatpak, Snap and AppImage builds.

### Android

**KeePassDX** for its modern interface and autofill. **Keepass2Android** if you want built-in cloud storage or QuickUnlock.

### iPhone and iPad

See our guide to [KeePass for iPhone](/keepass/keepass-ios/), or, if you use KeePassXC on your computer, our comparison of [KeePassXC alternatives for iPhone](/keepass/keepassxc-ios-alternatives/).

### Several Platforms at Once

Use **KeePassXC** on every desktop, **KeePassDX** on Android, and PanicVault, Strongbox or KeePassium on iPhone, all opening one KDBX 4 file in a synced folder.

## The Power of an Open Ecosystem

The number of compatible apps is a direct consequence of KDBX being an open format. Proprietary managers offer one app and one way of working; the KeePass ecosystem offers many, each built for a different platform or preference. If an app is discontinued, as KeePassX has been, or stops being updated, as KeeWeb largely has, you open your vault in another. That is the practical meaning of [data portability](/keepass/data-portability/), and it is why the [KeePass approach](/keepass/gold-standard/) is about a format rather than a single application.
