---
title: "Key Files"
description: "Use a key file as a second factor on a PanicVault vault — selecting one, generating one, biometric unlock, supported formats, and keeping it safe."
date: 2026-08-26
lastmod: 2026-08-26
draft: false
silo: "User Manual"
helpgroup: "Settings"
weight: 153
---

A key file is an optional second factor for your vault. In addition to your master password, a vault can be protected by a small file that acts like a physical key. When a vault uses a key file, it opens only when you supply **both** the master password **and** the key file — knowing the password alone is not enough, and having the key file alone is not enough. This gives you much stronger protection: someone would need to both know your password and possess your key file to open the vault.

Vaults you create in PanicVault always use a master password, with a key file as an optional extra factor. PanicVault can also open key-file-only vaults created in other KeePass apps — vaults protected by a key file with no password — by supplying just the key file.

A key file is not the only second factor PanicVault supports: a vault can also be protected by a physical YubiKey, which cannot be copied the way a file can. See [Hardware Keys (YubiKey)](/help/hardware-keys/). A vault can use both a key file and a YubiKey.

## Using a Key File When Unlocking

On the lock screen, just below the master password field, you see the **key file row**:

- If no key file is selected yet, the row reads **Add Key File** with an **Optional** label on the right. Tap it to browse for and select your key file.
- Once a key file is selected, the row shows a key icon and the file's name. Tap the **x** button at the end of the row to remove it if you need to choose a different file.

Enter your master password, make sure the correct key file is shown in the row, and tap **Unlock**.

## Using a Key File When Creating a Vault

When you create a new vault, scroll to the **Key File (Optional)** section. You have two choices:

- **Choose Existing Key File** — browse for a key file you already have (for example, one you created in KeePass or KeePassXC).
- **Generate New Key File** — PanicVault creates a brand-new key file filled with random data and asks you where to save it. The file is saved with a **.keyx** extension and is named after your vault by default.

After you choose or generate a key file, its name appears in the section along with a reminder to keep it safe. From that point on, both your master password and this key file are required to open the vault.

## PanicVault Remembers Your Key File

Once you select a key file for a vault, PanicVault remembers where it is, so you normally only pick it once. The next time you unlock that vault, the key file row is filled in for you automatically and you just type your master password.

PanicVault stores only a secure reference to the key file's location — it never stores the key file's contents, and it never uploads or copies the key file to iCloud Drive or Google Drive. Only your vault (.kdbx) file syncs between devices; the key file always stays wherever you keep it.

If the key file is moved, renamed, or deleted, PanicVault can no longer find it and shows a clear message such as "The saved key file could not be found. Add it to unlock." When this happens, tap the key file row and select the file again from its new location.

A key file you keep in iCloud Drive is fetched the same way the vault is: if iCloud has moved it off the device to save space, PanicVault downloads it before unlocking — the lock screen says **Downloading from iCloud...** while you wait, and should it take longer than a moment you are told your key file **hasn't finished downloading from iCloud** rather than that it could not be found.

## Biometric Unlock with a Key File

Face ID and Touch ID keep working on key-file vaults. When you unlock with biometrics, PanicVault automatically loads the remembered key file for you — you do not have to select it each time. If the key file cannot be found (because it was moved or deleted), PanicVault asks you to select it again before unlocking. Biometric unlock itself is covered in [Security & Settings](/help/security-and-settings/).

## Supported Key File Formats

PanicVault reads and writes key files interoperably with KeePass and KeePassXC. It supports every standard KeePass key file type:

- **KeePass XML key files** (versions 1.0 and 2.0, usually with a **.keyx** extension) — the modern format, including the integrity hash used by version 2.0
- **32-byte binary files** — the raw key bytes are used directly
- **64-character hexadecimal files** — decoded to the 32 key bytes
- **Any other file** — PanicVault uses a SHA-256 hash of the file's contents as the key, so you can turn almost any file into a key file

Key files you generate in PanicVault are written in the KeePassXC-compatible XML version 2.0 format, so they work in KeePass, KeePassXC, and other compatible apps as well. For more on working with other KeePass clients, see [KeePass Compatibility](/help/keepass-compatibility/).

## Keeping Your Key File Safe

A key file is only as useful as it is safe. Two rules matter most: keep a backup, and keep it separate from your vault.

{{< callout type="warning" >}}
If you lose your key file, your vault cannot be opened — not even with the correct master password. Back up the key file somewhere safe before you rely on it, and never store it in the same place as your vault file. If the key file and the .kdbx file sit in the same folder or the same cloud drive, anyone who gets one gets the other, which defeats the entire purpose of a second factor. Keep the two apart, and keep at least one backup of the key file.
{{< /callout >}}
