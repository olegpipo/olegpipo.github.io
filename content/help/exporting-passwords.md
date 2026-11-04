---
title: "Exporting Passwords to CSV"
description: "Export your PanicVault vault to a CSV file with tags, dates and custom fields — what the columns hold, how to import it back, and how to handle the file."
date: 2026-08-26
lastmod: 2026-11-04
draft: false
silo: "User Manual"
helpgroup: "Passwords & Entries"
weight: 75
---

You can export the passwords in the open vault to a CSV file — the counterpart to importing. This is useful for moving your passwords into another password manager or keeping a readable copy. The file uses KeePassXC's column layout with three more columns — tags, expiry, and custom fields — so it imports cleanly into KeePassXC, Bitwarden, and other password managers, and PanicVault reads it back whole.

## Different from Export Vault

CSV export is not a backup. **Export Vault** writes an encrypted **.kdbx** file that only your master password can open — that is the safe way to back up or move your whole vault, and it is covered in [Vault Settings](/help/vault-settings/). A **CSV** export is a plain, unencrypted text file that anyone can read. Choose CSV only when another app specifically needs one, and delete it as soon as you are done.

## Starting an Export

You must open and unlock a vault first, so the export command stays disabled until a vault is open.

- **Mac**: Choose **File > Export Passwords to CSV...** from the menu bar.
- **iOS**: Tap the **"..."** (ellipsis) menu in the entry list toolbar and choose **Export Passwords to CSV**.

Before anything is written, PanicVault shows a warning that tells you how many passwords are about to be exported and reminds you that the file is unencrypted, custom fields included. Tap **Export Unencrypted CSV** to continue, or **Cancel** to stop. When you confirm, you choose where to save the file; it is named after your vault (for example, **My Vault.csv**).

## What the File Contains

The CSV has one row per entry. The first ten columns are KeePassXC's own, in KeePassXC's order:

- **Group** — the full folder path, starting with your vault's name (for example, **My Vault/Banking**), so your organization is preserved; importing the file into PanicVault rebuilds the groups (see [The Import Sheet](/help/importing-passwords/#the-import-sheet)).
- **Title**, **Username**, **Password**, **URL**, and **Notes**.
- **TOTP** — the entry's one-time password, as an **otpauth://** link (or the bare secret, for an entry that holds only that). An entry whose one-time password was set up in KeePass or KeeTrayTOTP gets a link with the same settings, so the other app shows the same codes. See [Two-Factor Authentication (TOTP)](/help/two-factor-authentication/).
- **Icon** — the number of the entry's standard icon.
- **Last Modified** and **Created** — the entry's dates, in UTC (for example, **2024-01-15T10:30:00Z**).

Then three columns of PanicVault's own:

- **Tags** — the entry's tags, separated by semicolons (see [Tags](/help/entries/#tags)). KeePassXC imports this column too.
- **Expires** — when the entry expires, written like the dates; empty when it doesn't (see [Entry Expiration](/help/entries/#entry-expiration)).
- **Custom Fields** — all the entry's custom fields (see [Custom Fields](/help/entries/#custom-fields)), in their order, one per line, each as its name, a colon, and its value: `Account Number: 12345678`. A protected field has **(protected)** after its name: `PIN (protected): 0000`. So that each field stays on one line, a line break in a value is written `\n`, and a colon in a name `\:`.

Other apps see these three as extra columns: KeePassXC and Bitwarden ignore them (KeePassXC reads the tags), and other password managers keep them as text at most.

Entries in the **Recycle Bin** are never exported. Attachments, password history, passkeys, custom icons (the standard icon's number is written instead), the Override URL, entry colors, auto-type settings, and groups without entries are not included.

## Importing the File Back

Importing the file into PanicVault restores everything it holds. PanicVault recognizes its own export and gives every entry back its title, username, password, website, notes, one-time password, group, tags, icon, dates, expiry, and every custom field with its name, its protection, and its place in the list, as they were, spaces and line breaks included. See [Importing Passwords](/help/importing-passwords/).

{{< callout type="tip" >}}
If you edit the file in a spreadsheet, keep each custom field on its own line in the Custom Fields cell. A line without a colon is read as more of the value above it.
{{< /callout >}}

## Security Notes

The CSV is built entirely in memory and is only written to disk when you pick a destination — PanicVault never leaves a stray copy behind. But once the file exists, it is your responsibility:

- A CSV export is **plaintext** — anyone who opens the file can read every password in it, and every custom field, protected ones included: PINs, card numbers, and security codes are written out in full, like the passwords. As soon as you no longer need the file, delete it, then empty the Trash so it cannot be recovered.

{{< callout type="warning" >}}
Never leave an exported password CSV sitting in your Downloads folder or a cloud drive. Treat it like a written list of all your passwords, because that is exactly what it is.
{{< /callout >}}

Going the other way — bringing passwords in from another app — is covered in [Importing Passwords](/help/importing-passwords/).
