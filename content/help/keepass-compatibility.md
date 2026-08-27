---
title: "KeePass Compatibility"
description: "PanicVault uses the open KDBX 4 format — AES-256-CBC and ChaCha20 ciphers, Argon2d, Argon2id and AES-KDF key derivation, and full round-trip data preservation."
date: 2026-07-14
lastmod: 2026-08-27
draft: false
silo: "User Manual"
helpgroup: "Reference"
weight: 190
---

PanicVault stores your passwords in the open KeePass .kdbx file format rather than a proprietary database, so your data is never locked into one app. This page explains the format, which other applications can open your vaults, the ciphers and key derivation functions PanicVault supports, and exactly what it preserves when it saves a file.

## What is the KeePass Format?

KeePass is an open-source password manager that uses the .kdbx file format. This format is an open standard, meaning your passwords are never locked into a proprietary system. Many applications on different platforms can read and write .kdbx files.

PanicVault uses the KDBX 4 format, which is the current version of the standard.

## Interoperability

Your PanicVault databases can be opened in:

- **KeePass** (Windows) -- the original KeePass application
- **KeePassXC** (Windows, Mac, Linux) -- a popular cross-platform client
- **KeePassDX** (Android)
- **Strongbox** (iOS, Mac)
- Any other application that supports the KDBX 4 format

Similarly, PanicVault can open .kdbx files created by any of these applications. To bring an existing file in, see [Getting Started](/help/getting-started/).

## Opening an Older KeePass Database

If PanicVault tells you that a file is **an older KeePass database** — a KDBX 3.1 database, a KDBX 2.x database, or a KeePass 1.x `.kdb` file — nothing is wrong with it. PanicVault reads and writes KDBX 4 only, and the file is in an earlier format. Open it once in KeePassXC or KeePass, save it as KDBX 4, and PanicVault opens it from then on. **Your master password does not change**, and neither do your entries, attachments, key file or YubiKey setup.

**In KeePassXC** (Windows, Mac, Linux):

1. Open the database in KeePassXC and unlock it
2. Choose **Database → Database Settings**
3. Select the **Encryption** tab
4. Set **Database format** to **KDBX 4**
5. Click **OK**, then choose **Database → Save Database**

**In KeePass 2** (Windows, version 2.35 or later):

1. Open the database in KeePass and unlock it
2. Choose **File → Database Settings**
3. Select the **Security** tab
4. Set the key derivation function to **Argon2d**
5. Click **OK**, then choose **File → Save**

KeePass writes KDBX 4 whenever the database uses Argon2 or ChaCha20, so switching the key derivation function to Argon2d is what upgrades the format.

**A KeePass 1.x `.kdb` file** cannot be converted in place — it is a different format, not an older version of the same one. Import it first, then upgrade the result:

- **KeePass 2**: **File → Import**, choose **KeePass KDB (1.x)**, pick the `.kdb` file, then save the new database and follow the KeePass 2 steps above
- **KeePassXC**: **Database → Import → KeePass 1 Database**, pick the `.kdb` file, then save it and follow the KeePassXC steps above

Then add the converted `.kdbx` file to PanicVault the usual way — see [Getting Started](/help/getting-started/).

## Supported Encryption

PanicVault supports the following encryption algorithms for the outer database encryption:

- **AES-256-CBC** -- the default and most widely supported cipher
- **ChaCha20** -- a modern stream cipher, used by some KeePass clients

New vaults created in PanicVault use AES-256 by default.

## Supported Key Derivation

Key derivation functions transform your master password into the encryption key. PanicVault supports:

- **Argon2d** -- the default for new vaults. A memory-hard function that resists brute-force attacks even with specialized hardware. New databases use 64 MB of memory and 10 iterations by default.
- **Argon2id** -- a variant of Argon2 that combines data-dependent and data-independent memory access for additional side-channel resistance
- **AES-KDF** -- the legacy key derivation function used by older KeePass databases

## Hardware Keys and Challenge-Response

PanicVault supports **KeePassXC-style YubiKey HMAC-SHA1 challenge-response**, in both directions:

- A .kdbx file created in PanicVault with a YubiKey opens in KeePassXC with the same key and slot
- A KeePassXC database that uses challenge-response opens in PanicVault
- The same scheme is used by Strongbox and KeePassium, so those apps interoperate too

PanicVault reads a YubiKey **over NFC on iPhone, and over USB on Mac**. It cannot read one on iPad, over USB-C on an iPhone or iPad, or over Lightning (including the YubiKey 5Ci). See [Hardware Keys (YubiKey)](/help/hardware-keys/) for the full picture.

Two limits are worth knowing:

- **The KeeChallenge plugin format is not supported.** KeeChallenge is a KeePass 2 plugin that keeps an encrypted copy of the HMAC secret in an `.xml` file next to the database. That is a different mechanism from KeePassXC's, it needs a second file to be kept in sync, and it stores the secret at rest. If your database uses KeeChallenge, open it in KeePass 2, use its recovery mode to read out the secret, and reconfigure the database with KeePassXC-style challenge-response instead.
- **KDBX 3.x is not supported**, with or without a hardware key. PanicVault reads and writes KDBX 4 only — [Opening an Older KeePass Database](/help/keepass-compatibility/#opening-an-older-keepass-database) has the steps for converting one, and your YubiKey settings survive the conversion.

One behavioral difference, which does not affect compatibility: KeePassXC generates a new key derivation seed on every save and therefore asks for a YubiKey touch every time it saves. PanicVault reuses the seed for the unlocked session, so it asks for one touch when you unlock and none when you save. The files themselves are identical in format and open in either app.

## What PanicVault Preserves

When you open and save a .kdbx file in PanicVault, it preserves:

- All entries, groups, and their full hierarchy
- Entry history (previous versions)
- Custom fields (protected and unprotected)
- Attachments (binary files)
- Custom icons
- TOTP configurations (all supported formats)
- Passkey data (KeePassXC KPEX_PASSKEY_* fields)
- Auto-Type configurations
- Memory protection settings
- Recycle Bin state
- Database metadata (name, description, default username, colors)
- Entry and group metadata (creation time, modification time, expiry, tags, colors, last access time and usage count — and PanicVault keeps the usage counters up to date as you use an entry, the same way KeePassXC does)

For details on the individual formats, see [Two-Factor Authentication (TOTP)](/help/two-factor-authentication/) and [Passkeys (WebAuthn)](/help/passkeys/).
