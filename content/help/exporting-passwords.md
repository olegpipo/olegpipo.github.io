---
title: "Exporting Passwords to CSV"
description: "Export the passwords in your open PanicVault vault to a CSV file — how it differs from a .kdbx backup, what the columns hold, and how to handle the file."
date: 2026-08-26
lastmod: 2026-08-26
draft: false
silo: "User Manual"
helpgroup: "Passwords & Entries"
weight: 75
---

You can export the passwords in the open vault to a CSV file — the counterpart to importing. This is useful for moving your passwords into another password manager or keeping a readable copy. The file uses the KeePassXC column layout, so it imports cleanly into KeePassXC, Bitwarden, and PanicVault's own importer.

## Different from Export Vault

CSV export is not a backup. **Export Vault** writes an encrypted **.kdbx** file that only your master password can open — that is the safe way to back up or move your whole vault, and it is covered in [Vault Settings](/help/vault-settings/). A **CSV** export is a plain, unencrypted text file that anyone can read. Choose CSV only when another app specifically needs one, and delete it as soon as you are done.

## Starting an Export

You must open and unlock a vault first, so the export command stays disabled until a vault is open.

- **Mac**: Choose **File > Export Passwords to CSV...** from the menu bar.
- **iOS**: Tap the **"..."** (ellipsis) menu in the entry list toolbar and choose **Export Passwords to CSV**.

Before anything is written, PanicVault shows a warning that tells you how many passwords are about to be exported and reminds you that the file is unencrypted. Tap **Export Unencrypted CSV** to continue, or **Cancel** to stop. When you confirm, you choose where to save the file; it is named after your vault (for example, **My Vault.csv**).

## What the File Contains

The CSV has one row per entry, with these columns: **Group**, **Title**, **Username**, **Password**, **URL**, **Notes**, and **TOTP**. The Group column holds the full folder path (for example, **Root/Banking**) so your organization is preserved. If an entry has a one-time-password (TOTP) secret, it is written to the TOTP column — see [Two-Factor Authentication (TOTP)](/help/two-factor-authentication/).

Entries in the **Recycle Bin** are never exported. Attachments and custom fields are not included.

## Security Notes

The CSV is built entirely in memory and is only written to disk when you pick a destination — PanicVault never leaves a stray copy behind. But once the file exists, it is your responsibility:

- A CSV export is **plaintext** — anyone who opens the file can read every password in it. As soon as you no longer need the file, delete it, then empty the Trash so it cannot be recovered.

{{< callout type="warning" >}}
Never leave an exported password CSV sitting in your Downloads folder or a cloud drive. Treat it like a written list of all your passwords, because that is exactly what it is.
{{< /callout >}}

Going the other way — bringing passwords in from another app — is covered in [Importing Passwords](/help/importing-passwords/).
