---
title: "Migrate from Keeper to KeePass"
description: "Complete guide to migrating from Keeper Security to KeePass. Export your vault as CSV, import into KeePassXC, and verify all passwords transferred correctly."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "Can I export my passwords from Keeper to KeePass?"
    a: "Yes. Keeper allows you to export your vault as a CSV file through Settings > Export. The CSV can then be imported into any KeePass-compatible application like KeePassXC or PanicVault."
  - q: "Does Keeper export include shared folders?"
    a: "Shared folders may require separate exports depending on your Keeper plan. Personal vault items export normally, but items in shared team folders may need to be exported by the folder owner or handled individually."
  - q: "What data does Keeper include in a CSV export?"
    a: "Keeper's CSV export includes record titles, login URLs, usernames, passwords, notes, and custom fields. TOTP secrets and file attachments are typically not included in the CSV format."
  - q: "Will my Keeper TOTP codes transfer to KeePass?"
    a: "TOTP secrets are generally not included in Keeper's CSV export. You will need to manually re-add TOTP secrets to your KeePass entries or re-enroll two-factor authentication for affected accounts."
  - q: "How long should I keep my Keeper account after migrating?"
    a: "Keep your Keeper account active for two to four weeks after the migration. This gives you time to verify that all credentials transferred correctly and to catch any entries that may have been missed during the export."
---

Keeper Security is a well-regarded password manager, but its proprietary nature means your vault data lives within Keeper's ecosystem. If you want full control over your credentials -- stored locally in an open format with no subscription fees -- migrating to a [KeePass-compatible application](/keepass/) puts you in charge. This guide covers the complete migration process from Keeper to KeePass, including the export procedure, import steps, verification, and cleanup.

## Why Migrate from Keeper to KeePass

### Subscription Costs

Keeper operates on a subscription model with pricing tiers for individuals, families, and businesses. Additional features like secure file storage and dark web monitoring carry extra costs on top of the base subscription. Over years of use, these recurring fees add up to a substantial amount. KeePass-compatible applications are free and open source, with a lifetime cost of zero.

### Data Sovereignty

Keeper stores your encrypted vault on its cloud infrastructure. While the zero-knowledge encryption model means Keeper cannot read your data, the encrypted vault still resides on servers outside your control. With KeePass, your vault file stays on your devices. You choose where to store it, how to back it up, and whether to sync it -- no third party involved.

### Open Format Freedom

Keeper uses a proprietary vault format. If you want to leave, you must go through an export process. The open [KDBX format](/keepass/kdbx-format-guide/) used by KeePass is supported by dozens of independent applications. You can freely move between KeePassXC, PanicVault, Strongbox, KeePassDX, and many others without any conversion or re-export. For a deeper look at why format independence matters, see our guide on [KeePass data portability](/keepass/data-portability/).

### Transparency Through Open Source

Keeper publishes security audits and white papers, but the source code is not fully open for public inspection. KeePass and KeePassXC are open source -- anyone can review the code, verify the encryption implementation, and confirm the software does exactly what it claims. This transparency is a fundamental security advantage.

## Before You Start: Back Up Everything

Before beginning the migration, protect yourself against data loss.

1. **Note your entry count.** Open your Keeper vault and check the total number of records. Record this number so you can compare it against your KeePass import later.
2. **Identify shared folders.** If you use Keeper's shared folder feature (common in business plans), note which folders are shared. Shared folder items may need separate handling during export.
3. **Check for attachments.** Keeper allows file attachments on records. These will not export via CSV and must be handled manually.
4. **Keep Keeper active.** Do not cancel your subscription until you have fully verified the migration. A two-to-four-week overlap period is recommended.

## Step 1: Export Your Data from Keeper

Keeper provides a CSV export that captures the core credential data from your vault.

### Exporting via the Keeper Web Vault

1. Log in to your Keeper vault at keepersecurity.com.
2. Click your account name or profile icon to access **Settings**.
3. Navigate to the **Export** option (found under the account or data management section).
4. Select **CSV** as the export format.
5. Authenticate with your master password when prompted.
6. Save the CSV file to a secure location on your local drive.

### Exporting via the Keeper Desktop App

1. Open the Keeper desktop application and log in.
2. Go to **Settings** or the account menu.
3. Find the **Export** option.
4. Choose **CSV** format.
5. Authenticate and save the file locally.

### What the Keeper CSV Export Includes

The Keeper CSV export typically contains:

- **Folder** -- The folder path where the record was stored
- **Title** -- The record name
- **Login URL** -- The website address
- **Username** -- The login username
- **Password** -- The password in plain text
- **Notes** -- Any notes attached to the record
- **Custom fields** -- Additional fields you added to records (these may appear as extra columns)

### What Does Not Export Cleanly

- **TOTP secrets**: Keeper's TOTP (two-factor authentication) secrets are generally not included in the CSV export. You will need to re-enroll two-factor authentication on affected accounts or manually transfer TOTP seeds.
- **File attachments**: Documents, photos, and other files attached to records are not included in the CSV.
- **Shared folder permissions**: The sharing relationships and access controls for shared folders are Keeper-specific and do not transfer.
- **Password history**: Keeper tracks password changes over time, but only the current password is included in the export.
- **BreachWatch data**: Keeper's dark web monitoring alerts are not exported.

### Handling Shared Folders

If your Keeper vault includes shared folders, the records within those folders should be included in your personal export. However, the behavior may differ depending on your Keeper plan:

- **Personal plans**: All records you have access to, including those in shared folders, should appear in your export.
- **Business/Enterprise plans**: Your administrator may have restricted export capabilities. Records in team-managed shared folders may require the folder owner to export them separately. Check with your admin if you notice missing entries.

### Security Precautions

The exported CSV file contains all your passwords in plain text. Handle it with extreme care:

- Save it only to local, non-synced storage.
- Do not email, message, or share the file.
- Delete it securely after the import is verified.
- Lock your screen if you step away during the process.

## Step 2: Import into KeePass

With the Keeper CSV file ready, you can now import your data into a KeePass-compatible application.

### Importing into KeePassXC

1. Open KeePassXC and create a new database or open an existing one. For a new database, choose a strong master passphrase and use the default encryption settings (AES-256 with Argon2id).
2. Go to **Database** then **Import** then **CSV File**.
3. Select your Keeper CSV export.
4. Map the columns to KeePass fields:
   - "Title" to **Title**
   - "Login URL" to **URL**
   - "Username" to **User Name**
   - "Password" to **Password**
   - "Notes" to **Notes**
   - "Folder" to **Group**
5. Enable the option to treat the first row as field names.
6. Review the preview to verify the mapping.
7. Click **OK** to import.

### Importing into KeePass 2.x

1. Open KeePass 2.x and open or create your database.
2. Go to **File** then **Import**.
3. Select **Generic CSV Importer** from the format list.
4. Browse to your Keeper CSV file.
5. Configure the column mapping manually, matching each column to the corresponding KeePass field.
6. Complete the import.

### Importing on Apple Devices

Apple users can create a KDBX database using KeePassXC on macOS (or any platform), then open that same database file in [PanicVault](https://panicvault.com) on their Mac, iPhone, or iPad. PanicVault is a KeePass-compatible app built natively for Apple platforms, providing system-level autofill integration and a polished interface. Store your KDBX file in iCloud Drive for seamless sync across all your Apple devices. See our [compatible apps guide](/keepass/compatible-apps/) for a full list of options.

### Handling Custom Fields

Keeper allows custom fields on records (additional username/password pairs, PINs, security questions, etc.). These custom fields may appear as extra columns in the CSV. During the import, you can either:

- Map them to KeePass's custom string fields (available in the entry editor's "Advanced" or "Extra" tab)
- Let them import into the Notes field as concatenated text
- Ignore them during import and manually re-create them in KeePass after

The first option preserves the data most faithfully, but requires more effort during the import configuration.

## Step 3: Verify Your Data

Thorough verification ensures nothing was lost or corrupted during the migration.

### Compare Entry Counts

Count the entries in your new KeePass database and compare against your Keeper vault count. If numbers do not match, investigate the gap. Common reasons for discrepancies include:

- Records in shared folders that were not included in the export
- Entries with special characters that broke CSV parsing
- Deleted records in Keeper's trash that were unexpectedly included or excluded

### Test Critical Accounts

Log in to your highest-priority accounts using credentials from KeePass:

- Primary email accounts
- Banking and financial services
- Cloud storage providers
- Work accounts and VPNs
- Social media profiles

Each successful login confirms a correct transfer.

### Verify Folder Structure

Check that the Keeper folder hierarchy translated correctly into KeePass groups. If the folder paths did not map properly, you may need to manually reorganize entries into the correct groups.

### Check Notes and Custom Fields

Open several entries and compare the notes and custom field content against the originals in Keeper. Look for truncation, encoding issues, or missing data.

## Step 4: Clean Up

With verification complete, finalize the migration.

### Delete the CSV File

Securely delete the plain text CSV export. Do not keep it as a backup -- your KDBX database is now your authoritative vault.

### Back Up Your KeePass Database

Create an immediate backup of your KDBX file and store it in a location separate from the primary copy. For comprehensive backup strategies, see our [KeePass database backup guide](/keepass/backup-database/).

### Handle Your Keeper Account

Maintain your Keeper account for two to four weeks as a safety net. Once you are confident the migration is complete:

- Delete all records in Keeper to remove your data from their servers
- Cancel your subscription to stop future billing
- Delete the account entirely through account settings if desired

### Re-enroll TOTP

For accounts where you had TOTP secrets stored in Keeper, you will need to re-enroll two-factor authentication. Go to each account's security settings, disable the existing TOTP enrollment, and set up a new one using your KeePass application. KeePassXC supports TOTP natively, so you can store the secret and generate codes directly from your vault.

### Set Up Autofill

Install the browser extension for your KeePass application (KeePassXC Browser for desktop browsers) and configure system autofill on mobile devices. On Apple devices, PanicVault integrates with iOS and macOS autofill, providing the same convenience you had with Keeper's browser extension and mobile app.

## What Transfers and What Does Not

| Data Type | Transfers via CSV | Notes |
|-----------|:-:|-------|
| Login credentials | Yes | URL, username, password, title |
| Notes | Yes | Text content preserves |
| Folders | Yes | Maps to KeePass groups |
| Custom fields | Partial | Extra CSV columns may need manual mapping |
| TOTP secrets | No | Must re-enroll or manually transfer |
| File attachments | No | Download from Keeper and re-attach manually |
| Password history | No | Only current passwords export |
| Shared folder permissions | No | Keeper-specific feature |
| BreachWatch alerts | No | Keeper-specific feature |

## Related Articles

- [What Is the KDBX Format and Why It Matters](/keepass/kdbx-format-guide/)
- [KeePass-Compatible Apps for Every Platform](/keepass/compatible-apps/)
- [KeePass Data Portability: Own Your Passwords Forever](/keepass/data-portability/)
- [How to Back Up Your KeePass Database](/keepass/backup-database/)
- [Migrate from Dashlane to KeePass](/keepass/migrate-from-dashlane/)
