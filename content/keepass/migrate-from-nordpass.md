---
title: "Migrate from NordPass to KeePass"
description: "Step-by-step guide to migrating from NordPass to KeePass. Export your NordPass vault as CSV, import into KeePassXC, and verify all entries transferred."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "How do I export my NordPass passwords?"
    a: "Open NordPass, go to Settings, select Export Items, and choose CSV format. Authenticate with your master password. The CSV file will contain your URLs, usernames, passwords, notes, and folder names."
  - q: "Can I import NordPass passwords into KeePassXC?"
    a: "Yes. KeePassXC's CSV import function works with NordPass exports. Go to Database > Import > CSV File, select your NordPass CSV, map the columns to KeePass fields, and complete the import."
  - q: "Does NordPass CSV export include folders?"
    a: "Yes. NordPass includes folder names in the CSV export, which can be mapped to KeePass groups during import. This preserves your organizational structure in the new database."
  - q: "What data does NordPass not export?"
    a: "NordPass CSV exports do not include file attachments, password history, sharing configurations, or Data Breach Scanner results. Credit cards and personal information may export with limited structure."
  - q: "Is NordPass harder to export from than other password managers?"
    a: "No. NordPass provides a straightforward CSV export through its settings menu. The process is similar to other password managers and produces a standard CSV that works with any KeePass-compatible application."
---

NordPass, created by the team behind NordVPN, is a competent password manager, but it operates as a proprietary cloud service with recurring subscription costs. If you prefer to own your credential data outright -- stored locally in an open format with no ongoing fees -- migrating to a [KeePass-compatible application](/keepass/) is a straightforward process. This guide walks you through exporting your NordPass vault, importing it into KeePass, and verifying that every credential made the journey intact.

## Why Migrate from NordPass to KeePass

### Subscription Fees

NordPass offers a limited free tier and paid plans for individuals, families, and businesses. The premium features that most users need -- including multi-device sync and secure item sharing -- require an ongoing subscription. KeePass-compatible applications are free and open source with no premium tiers, no feature restrictions, and no recurring costs.

### Data Control

NordPass stores your encrypted vault on Nord Security's cloud servers. While the zero-knowledge architecture means Nord Security cannot read your data, you are still relying on a third party to store and manage access to your encrypted vault. With KeePass, your database file lives on your own devices. You control the storage, backups, and synchronization without any intermediary.

### Format Freedom

NordPass uses a proprietary vault format. Your data can only be accessed through NordPass applications unless you go through an explicit export process. The open [KDBX format](/keepass/kdbx-format-guide/) used by KeePass is supported by dozens of independent applications. You can freely switch between KeePassXC on desktop, PanicVault on Apple devices, KeePassDX on Android, and many other options without converting or re-exporting. Our guide on [data portability](/keepass/data-portability/) explains why this matters long term.

### Open Source Transparency

NordPass is closed-source software. While Nord Security commissions third-party security audits, the code itself is not publicly available for independent review. KeePass and KeePassXC are fully open source, allowing anyone to verify the encryption, inspect the code, and confirm that the software handles your data as claimed.

## Before You Start: Back Up Everything

Take these precautions before beginning the migration.

1. **Count your entries.** Check the total number of items in your NordPass vault -- logins, secure notes, credit cards, and personal information. Write this number down for later verification.
2. **Identify items that need special handling.** NordPass stores more than just logins. Credit cards, personal identity items, and secure notes may require manual attention after the CSV import.
3. **Keep NordPass active.** Do not cancel your subscription or delete your account until you have verified the migration is complete. Maintain access for at least two to four weeks.
4. **Note your folder structure.** If you organized entries into folders in NordPass, review the structure so you can verify it transfers correctly.

## Step 1: Export Your Data from NordPass

NordPass provides a CSV export that captures the essential data from your vault.

### Export Steps

1. Open NordPass on your desktop (the web interface or desktop application).
2. Navigate to **Settings** from the menu.
3. Find and select **Export Items**.
4. Choose **CSV** as the export format.
5. Enter your master password to authenticate.
6. Save the CSV file to a secure location on your local drive -- not to any cloud-synced folder.

### What the NordPass CSV Export Includes

The NordPass CSV export contains well-structured data for login entries:

- **name** -- The entry title
- **url** -- The website URL
- **username** -- Your login username or email
- **password** -- The password in plain text
- **note** -- Any notes attached to the entry
- **cardholdername, cardnumber, cvc, expirydate** -- Credit card fields (for card entries)
- **folder** -- The folder name where the entry was organized

NordPass organizes the CSV clearly, with login entries, credit cards, secure notes, and personal information typically appearing in distinct sections or with distinguishing fields.

### What Does Not Export

- **File attachments**: Any files stored within NordPass are not included in the CSV.
- **Password history**: Only the current version of each credential is exported.
- **Sharing configurations**: Shared item relationships do not transfer.
- **Data Breach Scanner results**: NordPass's breach monitoring data stays within NordPass.
- **Passkeys**: If you stored passkeys in NordPass, these are not exportable via CSV. You will need to re-create passkeys on each service using your new password manager.

### Security Precautions

Your exported CSV file contains all your passwords in plain text. Treat it accordingly:

- Store it only on local, non-synced storage.
- Do not transmit it via email, messaging apps, or file-sharing services.
- Delete it securely after confirming the import is successful.
- If working on a shared computer, ensure no one else can access the file.

## Step 2: Import into KeePass

With the NordPass CSV ready, import it into your KeePass-compatible application.

### Importing into KeePassXC

1. Open KeePassXC and create a new database or open an existing one. For a new database, set a strong master passphrase and keep the default encryption settings (AES-256 with Argon2id key derivation).
2. Go to **Database** then **Import** then **CSV File**.
3. Select your NordPass CSV file.
4. Map the columns to KeePass fields in the mapping interface:
   - "name" to **Title**
   - "url" to **URL**
   - "username" to **User Name**
   - "password" to **Password**
   - "note" to **Notes**
   - "folder" to **Group**
5. Check the option to treat the first row as field names.
6. Review the preview and confirm the mapping looks correct.
7. Click **OK** to complete the import.

### Importing into KeePass 2.x

1. Open KeePass 2.x and open or create a database.
2. Go to **File** then **Import**.
3. Select **Generic CSV Importer**.
4. Browse to the NordPass CSV file.
5. Configure column mapping manually.
6. Complete the import.

### Handling Credit Cards and Personal Info

NordPass exports credit card entries and personal information as part of the CSV, but these items use different fields than login entries. After importing:

- Credit card entries may appear with the card details in the notes field or in separate columns that did not map to standard KeePass fields.
- Review these entries and organize the data into KeePass custom string fields for cleaner storage.
- Alternatively, create a dedicated "Payment Cards" group and store card details in structured notes within each entry.

### Importing on Apple Devices

For Apple users, the most convenient workflow is to create your KDBX database using KeePassXC, then open it in [PanicVault](https://panicvault.com) on macOS, iPhone, and iPad. PanicVault is a KeePass-compatible app designed natively for Apple platforms, offering system autofill integration and iCloud sync for your KDBX file. This gives you the seamless experience you had with NordPass while keeping your data in an open format. See our [compatible apps guide](/keepass/compatible-apps/) for all available options.

## Step 3: Verify Your Data

Never assume a migration worked perfectly. Verify thoroughly.

### Compare Entry Counts

Count entries in your new KeePass database and compare against the number you noted from NordPass. Account for the fact that credit cards and personal information items may have imported differently than login entries.

### Test Critical Accounts

Log in to your most important accounts using credentials from KeePass:

- Primary email accounts
- Banking and financial services
- Cloud storage services
- Work accounts and VPNs
- Social media profiles

A successful login confirms the credential transferred correctly.

### Verify Folder Structure

Check that NordPass folders translated into KeePass groups correctly. If the folder names imported as expected, your organizational structure should be preserved. If not, manually reorganize entries into the appropriate groups.

### Check Notes Content

Open several entries and compare notes against the originals in NordPass. Verify that nothing was truncated or garbled during the CSV export and import process.

## Step 4: Clean Up

With verification complete, finalize the transition.

### Delete the CSV Export

Securely delete the plain text CSV file. It has served its purpose and is now a liability.

### Back Up Your KeePass Database

Create a backup of your KDBX file immediately. Store it separately from the primary copy -- on a different drive, an encrypted USB stick, or a secure cloud location. Our [backup guide](/keepass/backup-database/) covers comprehensive strategies.

### Manage Your NordPass Account

Keep NordPass accessible for two to four weeks. Once confident in the migration:

- Delete all items in NordPass to remove your data from their servers
- Cancel your subscription through your Nord account settings
- Delete your NordPass account if desired

### Set Up Your New Workflow

Install the KeePassXC Browser extension for desktop autofill. On Apple devices, configure PanicVault or your chosen KeePass app for system-level autofill. Disable NordPass's browser extension and mobile autofill to avoid conflicts.

## What Transfers and What Does Not

| Data Type | Transfers via CSV | Notes |
|-----------|:-:|-------|
| Login credentials | Yes | URL, username, password, title, notes |
| Folders | Yes | Map to KeePass groups |
| Secure notes | Yes | Text content transfers |
| Credit cards | Partial | Fields may need manual reorganization |
| Personal information | Partial | Flattened into text fields |
| File attachments | No | Must be saved and re-attached manually |
| Password history | No | Only current passwords export |
| Passkeys | No | Must be re-created on each service |
| Sharing configurations | No | NordPass-specific feature |
| Breach monitoring data | No | NordPass-specific feature |

## Related Articles

- [What Is the KDBX Format and Why It Matters](/keepass/kdbx-format-guide/)
- [KeePass-Compatible Apps for Every Platform](/keepass/compatible-apps/)
- [How to Back Up Your KeePass Database](/keepass/backup-database/)
- [KeePass vs. Proprietary Password Managers](/keepass/vs-proprietary/)
- [Migrate from LastPass to KeePass](/keepass/migrate-from-lastpass/)
