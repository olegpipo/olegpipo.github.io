---
title: "Migrate from Enpass to KeePass"
description: "Step-by-step guide to migrating from Enpass to KeePass. Export directly to KDBX, or use CSV/JSON, and verify all credentials transferred correctly."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "Can Enpass export directly to KeePass format?"
    a: "Yes. Enpass is one of the few password managers that can export directly to KDBX format, which is the native KeePass database format. This makes migration seamless since no CSV conversion or column mapping is needed."
  - q: "What export formats does Enpass support?"
    a: "Enpass supports exporting to CSV, JSON, and KDBX formats. The KDBX export is the best option for migrating to KeePass since it preserves the most data and requires no import conversion."
  - q: "Does the Enpass KDBX export preserve all my data?"
    a: "The KDBX export preserves login credentials, notes, folder structure, and custom fields. File attachments and some Enpass-specific features like tags may not transfer completely. Always verify the exported database."
  - q: "Do I need KeePassXC to import from Enpass?"
    a: "Not if you use the KDBX export. The KDBX file exported from Enpass can be opened directly in any KeePass-compatible app including KeePassXC, PanicVault, Strongbox, or KeePass 2.x. No import step is needed."
  - q: "Should I use CSV or KDBX when migrating from Enpass?"
    a: "Use KDBX whenever possible. It preserves more data, maintains your folder structure, and requires no column mapping or data conversion. Use CSV only as a fallback if the KDBX export does not work for your specific setup."
---

Enpass stands out among proprietary password managers because it already stores your vault locally rather than on a cloud server, and it supports exporting directly to the KDBX format used by KeePass. This makes Enpass one of the easiest password managers to migrate away from. If you want to move to a fully open source [KeePass-compatible application](/keepass/) while preserving your data with minimal friction, this guide covers every step of the process.

## Why Migrate from Enpass to KeePass

### Full Open Source Stack

Enpass stores your vault locally (which is good), but the application itself is proprietary. You trust Enpass to handle your encryption and data management correctly, but you cannot verify this yourself. KeePass and KeePassXC are fully open source -- the encryption implementation, the database format, and the application code are all publicly auditable. For more on how this transparency benefits you, see our [encryption explained guide](/keepass/encryption-explained/).

### No License Fees

Enpass uses a one-time purchase model on desktop and a subscription model on mobile (or a one-time lifetime purchase). While more reasonable than many competitors, it still costs money. KeePass-compatible applications are completely free, permanently.

### Broader App Ecosystem

Enpass is developed by a single company. If that company discontinues the product, changes its business model, or gets acquired, your workflow is affected. The [KDBX format](/keepass/kdbx-format-guide/) is supported by dozens of independent applications. You can choose the best app for each platform and switch freely. KeePassXC for desktop, PanicVault for Apple devices, KeePassDX for Android -- the choice is yours and can change at any time.

### Community and Ecosystem

The KeePass ecosystem is supported by a global community of developers and users. Plugins, tools, and integrations are continuously developed. If one application stops being maintained, others are ready to fill the gap. This distributed development model is more resilient than depending on a single company.

## Before You Start: Back Up Everything

Even though Enpass makes migration easy, take precautions.

1. **Back up your Enpass vault.** Enpass stores your vault as a local file. Make a copy of this file before starting the migration.
2. **Count your entries.** Note the total number of items in Enpass -- logins, secure notes, credit cards, identities, and other item types.
3. **Review your vault structure.** Note your folder and tag organization so you can verify it transfers correctly.
4. **Identify attachments.** If you have file attachments in Enpass entries, these may not transfer via any export format. Make a list of entries with attachments.
5. **Keep Enpass installed.** Do not uninstall Enpass or delete your vault until the migration is verified.

## Step 1: Export Your Data from Enpass

Enpass provides three export formats, and the KDBX option makes this migration uniquely straightforward.

### Option A: Export Directly to KDBX (Recommended)

This is the simplest and most complete migration path.

1. Open Enpass on your desktop.
2. Go to **Settings** (or **File** menu, depending on your platform).
3. Navigate to the **Export** option.
4. Select **KeePass (.kdbx)** as the export format.
5. Choose a master password for the exported KDBX file. This can be the same as your Enpass master password or a new one. You will need this password to open the file in your KeePass application.
6. Select the vaults you want to export (if you have multiple).
7. Save the KDBX file to a secure location on your local drive.

That is it. The exported KDBX file is a fully functional KeePass database. You can open it directly in KeePassXC, PanicVault, Strongbox, KeePass 2.x, or any other compatible application. No import, no column mapping, no conversion.

### Option B: Export as JSON

If you want more control over the import process or need to transform the data:

1. Open Enpass and go to **Settings** then **Export**.
2. Select **JSON** as the format.
3. Authenticate and save the file.

JSON preserves entry structure, custom fields, and metadata. You can then import the JSON into KeePassXC using its import function, though you may need to do some manual mapping.

### Option C: Export as CSV

As a fallback option:

1. Open Enpass and go to **Settings** then **Export**.
2. Select **CSV** as the format.
3. Save the file.

CSV is the most universal format but loses the most data during conversion. Use this only if the KDBX and JSON options do not work for your situation.

### What the KDBX Export Preserves

The Enpass KDBX export typically preserves:

- **Login credentials** -- URLs, usernames, passwords
- **Folder structure** -- Enpass folders map to KeePass groups
- **Notes** -- Entry notes and secure notes
- **Custom fields** -- Additional fields like security questions, PINs, and custom data
- **Entry metadata** -- Creation dates, modification dates

### What May Not Transfer Completely

- **File attachments**: Depending on the Enpass version and export settings, file attachments may not be included in the KDBX export. Verify after export.
- **Tags**: Enpass uses tags for organization. KeePass does not have a native tagging system (though KeePassXC supports tags). Tag assignments may not survive the KDBX export.
- **TOTP secrets**: Check whether TOTP configurations transfer. If not, you will need to re-enroll two-factor authentication.
- **Password history**: Enpass tracks password changes. This history may not transfer to the KDBX file.

## Step 2: Open or Import into KeePass

The process differs depending on which export format you chose.

### If You Exported as KDBX (Recommended)

There is no import step. Simply open the KDBX file in your KeePass-compatible application:

1. Open KeePassXC (or your chosen app).
2. Click **Open Existing Database** (or **File** then **Open**).
3. Navigate to the KDBX file exported from Enpass.
4. Enter the master password you set during export.
5. Your vault opens with all entries ready to use.

If you want to change the master password or encryption settings:

1. In KeePassXC, go to **Database** then **Database Settings**.
2. Change the master password if desired.
3. Review the encryption settings (AES-256 with Argon2id is recommended).
4. Save the database.

### If You Exported as JSON

1. Open KeePassXC and create a new database or open an existing one.
2. Go to **Database** then **Import** and look for an Enpass or generic JSON import option.
3. If a dedicated Enpass import is not available, you may need to use a third-party conversion tool to convert the Enpass JSON to CSV or KDBX format first.

### If You Exported as CSV

1. Open KeePassXC and go to **Database** then **Import** then **CSV File**.
2. Select the Enpass CSV.
3. Map columns to KeePass fields (Title, URL, Username, Password, Notes, Group).
4. Check the option to treat the first row as field names.
5. Complete the import.

### Using PanicVault on Apple Devices

The KDBX file exported from Enpass can be opened directly in [PanicVault](https://panicvault.com) on your Mac, iPhone, or iPad. Simply place the KDBX file in iCloud Drive (or your preferred sync location) and open it from PanicVault. The app provides native macOS and iOS autofill integration, making it an excellent replacement for Enpass on Apple devices. See our [compatible apps guide](/keepass/compatible-apps/) for all available KeePass-compatible applications.

## Step 3: Verify Your Data

Even with the seamless KDBX export, verification is essential.

### Compare Entry Counts

Count entries in your new KeePass database and compare against the Enpass vault. Check each category -- logins, notes, cards, identities.

### Test Critical Accounts

Log in to your most important accounts using credentials from KeePass:

- Primary email accounts
- Banking and financial services
- Cloud storage providers
- Work accounts and VPNs
- Social media profiles

### Verify Folder Structure

Check that the Enpass folder hierarchy transferred correctly to KeePass groups. The KDBX export should preserve the structure faithfully, but verify.

### Check Custom Fields

Enpass supports extensive custom fields on entries. Open several entries with custom data and verify that the fields and values are present and correct.

### Verify TOTP

If you had TOTP configured in Enpass entries, check whether the TOTP secrets transferred. Generate a test code and compare it against what Enpass produces. If TOTP did not transfer, you will need to re-enroll on each affected account.

### Check Attachments

If you had file attachments, verify whether they are present in the exported database. If not, download them from Enpass and manually attach them to the corresponding entries in your KeePass application.

## Step 4: Clean Up

With verification complete, finalize the transition.

### Secure the Export Files

If you created CSV or JSON exports in addition to the KDBX file, delete those plain text files securely. The KDBX file is encrypted, so it can be retained as a backup if needed.

### Back Up Your KeePass Database

Create a backup of your finalized KDBX file and store it in a separate location. An encrypted USB drive, a different device, or a secure cloud location all work. See our [backup guide](/keepass/backup-database/) for comprehensive strategies.

### Update Your Master Password (Optional)

If you used the same master password for the Enpass KDBX export as you used for Enpass itself, consider whether you want to change it. If Enpass was compromised at any point, using a new master password for your KeePass database adds a layer of separation.

### Uninstall Enpass

After two to four weeks of successful use with your new KeePass setup, you can uninstall Enpass. Before uninstalling:

- Confirm one final time that all entries are present in KeePass
- Download any remaining file attachments
- Note any entries that relied on Enpass-specific features

### Set Up Autofill

Install the KeePassXC Browser extension for desktop autofill. On mobile devices, configure your KeePass app's system-level autofill. Remove Enpass from your autofill settings to avoid conflicts.

## What Transfers and What Does Not

| Data Type | KDBX Export | CSV Export | Notes |
|-----------|:-:|:-:|-------|
| Login credentials | Yes | Yes | URL, username, password |
| Folder structure | Yes | Partial | KDBX preserves groups directly |
| Notes | Yes | Yes | Text content transfers |
| Custom fields | Yes | Partial | KDBX preserves field structure |
| TOTP secrets | Varies | Varies | Verify after export |
| Tags | No | No | KeePass has limited tag support |
| File attachments | Varies | No | Check KDBX export; may need manual transfer |
| Password history | No | No | Only current credentials export |
| Credit cards | Yes | Partial | KDBX preserves structured data |
| Identities | Yes | Partial | KDBX preserves structured data |

## Related Articles

- [What Is the KDBX Format and Why It Matters](/keepass/kdbx-format-guide/)
- [KeePass-Compatible Apps for Every Platform](/keepass/compatible-apps/)
- [KeePass Data Portability: Own Your Passwords Forever](/keepass/data-portability/)
- [KeePass Encryption Explained](/keepass/encryption-explained/)
- [How to Back Up Your KeePass Database](/keepass/backup-database/)
