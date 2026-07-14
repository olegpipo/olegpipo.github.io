---
title: "Vault Settings"
description: "Per-vault settings in PanicVault: database info, default username, entry history limits, Recycle Bin, changing your master password, and exporting a .kdbx file."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Settings"
weight: 160
---

Vault settings (also called Database Settings) apply to a single vault rather than the whole app. This page covers the database info panel, general and history options, the Recycle Bin switch, changing your master password, and exporting your vault.

Access vault-specific settings by tapping the gear icon in the entry list toolbar (while a vault is unlocked).

## Database Info

Read-only information about your vault:

- **Generator** -- the application that created the database
- **Entries** -- total number of entries
- **Groups** -- total number of groups
- **Attachments** -- number of binary attachments in the vault
- **Custom Icons** -- number of custom icons stored in the vault

## General Settings

- **Database Name** -- the display name of the vault (also updates the vault card)
- **Description** -- a text description for your vault
- **Default Username** -- a default username for new entries. When set, a **Use default** button appears next to the username field when creating a new entry, letting you quickly fill in your usual username or email. This setting is also compatible with other KeePass applications.

See [Entries (Passwords)](/help/entries/) for how the **Use default** button behaves when you create an entry.

## History Settings

Control how [entry history](/help/entries/) is stored:

- **Max History Items** -- the maximum number of previous versions kept per entry (default: 10)
- **Max History Size** -- the maximum total size of history data (default: 6 MB, options from 1 MB to 20 MB)
- **Maintenance Days** -- how many days of history to retain (default: 365)

## Recycle Bin

- **Recycle Bin Enabled** -- when on, deleted entries are moved to the Recycle Bin instead of being permanently deleted. When off, deletions are permanent.

## Changing Your Master Password

You can change your vault's master password from Database Settings:

1. Unlock your vault and tap the gear icon in the entry list toolbar to open **Database Settings**
2. In the **Master Password** section, tap **Change Master Password**
3. Enter your current master password
4. Enter and confirm your new master password
5. Tap **Change Password**

PanicVault re-encrypts the entire vault with your new password and saves it. If your vault syncs with [iCloud Drive](/help/icloud-drive-sync/) or [Google Drive](/help/google-drive-sync/), the updated file is automatically uploaded so all your devices use the new password. If biometric unlock (Face ID / Touch ID) is enabled, the stored key is also updated automatically.

{{< callout type="important" >}}
After changing your master password, you must use the new password on all devices. If another device still has the vault open with the old password, it will need to be unlocked with the new password next time.
{{< /callout >}}

## Exporting Your Vault

You can export your vault as a .kdbx file at any time:

- **iOS**: Tap the share icon in the entry list toolbar
- **Mac**: Click the export icon in the toolbar, or use **Cmd+Shift+E**

The exported file is a standard .kdbx file that can be opened in any compatible KeePass application. See [KeePass Compatibility](/help/keepass-compatibility/) for the list of apps that read the format.
