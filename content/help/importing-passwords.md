---
title: "Importing Passwords"
description: "Import a CSV export from Apple Passwords, Chrome, Firefox, Bitwarden, KeePassXC, or 1Password into PanicVault, including TOTP columns."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Passwords & Entries"
weight: 70
---

You can bring passwords into PanicVault from other password managers and browsers by importing a CSV file. Imported entries are added directly to the vault you have open, and PanicVault detects which app the file came from automatically.

## Before You Import

You must open and unlock a vault first. Importing adds the entries to the currently open vault, so the import command stays disabled until a vault is unlocked. If the menu item is greyed out, unlock a vault and try again.

## Starting an Import

- **Mac**: Choose **File > Import Passwords from CSV...** from the menu bar, or press **Cmd+Shift+I**.
- **iOS**: Tap the **"..."** (ellipsis) menu in the entry list toolbar and choose **Import Passwords from CSV**.

Then choose a CSV file. PanicVault reads the file, detects which app it came from, and shows an import sheet.

## Supported Formats

PanicVault automatically detects CSV exports from:

- **Apple Passwords / Safari**
- **Chrome, Edge, and other Chromium browsers** (including Brave)
- **Firefox**
- **Bitwarden**
- **KeePassXC**
- **1Password 8**

Any other CSV also works as long as it has a password column. PanicVault matches the remaining columns — title, username, URL, and notes — by their header names, so most generic exports import correctly without any setup.

## The Import Sheet

After you pick a file, the import sheet shows:

- **Detected format** — the app PanicVault recognized (or "Generic CSV")
- **Entries found** — how many rows were parsed into importable entries
- **Add to group** — the destination group for the imported entries. This defaults to a group named **General** if your vault has one, otherwise the vault root. You can choose any group you like.

Tap **Import** to add the entries. When the import finishes, a summary tells you how many entries were imported and how many empty rows were skipped. If you picked the wrong file, tap **Choose a Different File** before importing.

## Two-Factor (TOTP) Columns

If the CSV includes a one-time-password column — such as the **OTPAuth** column from Apple Passwords or the **TOTP** column from KeePassXC and Bitwarden — PanicVault imports it into the entry's One-Time Password field. Those entries generate 2FA codes right away, just like TOTP you set up by hand (see [Two-Factor Authentication (TOTP)](/help/two-factor-authentication/)).

## Exporting a CSV from Other Apps

Each source app has its own export command. A few common ones:

- **Apple Passwords** (Mac) — open the **Passwords** app and use **File > Export** to save your passwords as a CSV
- **Chrome** — open **Google Password Manager**, go to **Settings**, and choose **Export passwords**
- **Edge** — go to **Settings > Profiles > Passwords**, then use the **"..."** menu and choose **Export passwords**
- **Firefox** — open **Passwords** (about:logins), use the **"..."** menu, and choose **Export Logins...**
- **Bitwarden** — in the web or desktop app, choose **Tools > Export Vault** and pick the **.csv** format
- **KeePassXC** — choose **Database > Export > Export to CSV...**
- **1Password 8** — open the account or vault menu and choose **Export**, then select **CSV**

{{< callout type="tip" >}}
These menus change between app versions. If you cannot find the export command, search the app's help for "export CSV".
{{< /callout >}}

## Security Notes

Importing is designed to keep your passwords safe:

- The CSV is parsed entirely in memory. PanicVault never writes the raw CSV file to disk — only the resulting entries are saved into your encrypted vault.
- A CSV export is **plaintext** — anyone who opens the file can read every password in it. As soon as the import finishes, delete the CSV file, then empty the Trash so it cannot be recovered.

{{< callout type="warning" >}}
Never leave an exported password CSV sitting in your Downloads folder or a cloud drive. Treat it like a written list of all your passwords, because that is exactly what it is.
{{< /callout >}}
