---
title: "Migrate from Dashlane to KeePass"
description: "Step-by-step guide to exporting your Dashlane vault and importing it into KeePass. Covers CSV and DASH exports, field mapping, and data verification."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "Can I export my Dashlane passwords to KeePass?"
    a: "Yes. Dashlane lets you export your vault as a CSV file through Settings > Export data. The CSV can then be imported into any KeePass-compatible app like KeePassXC or PanicVault using their CSV import function."
  - q: "What is the difference between Dashlane CSV and DASH export?"
    a: "CSV is a plain-text format readable by any password manager. DASH is Dashlane's encrypted export format that can only be re-imported into Dashlane. For migrating to KeePass, use the CSV export."
  - q: "Does Dashlane export include secure notes and payment info?"
    a: "Dashlane's CSV export includes logins, secure notes, and some identity data. However, payment cards, IDs, and receipts may not export cleanly and often require manual re-entry in your new KeePass database."
  - q: "Will I lose my Dashlane password history after migrating?"
    a: "Yes. Dashlane's password change history does not transfer via CSV. Only the current version of each credential is exported. If you need historical passwords, note them before exporting."
  - q: "Is it safe to export passwords from Dashlane as CSV?"
    a: "The CSV file contains all your passwords in plain text, so it must be handled carefully. Save it only to local storage, never to cloud-synced folders, and delete it securely after confirming your KeePass import is complete."
---

Moving from a subscription password manager to an open, self-hosted vault is one of the most empowering steps you can take for your digital security. If you are considering leaving Dashlane, migrating to a [KeePass-compatible application](/keepass/) gives you full ownership of your credentials in the open KDBX format -- no recurring fees, no vendor lock-in, and no dependency on a company's continued existence. This guide walks you through every step of the process, from exporting your Dashlane vault to verifying that every entry landed safely in your new KeePass database.

## Why Migrate from Dashlane to KeePass

### Rising Subscription Costs

Dashlane has steadily increased its pricing over the years while trimming features from its free tier. The free plan now limits users to a single device, making it impractical for anyone who uses more than one computer or phone. The premium plan carries a recurring annual cost that accumulates over time. KeePass-compatible applications are free and open source, eliminating subscription fees entirely.

### Data Ownership and Privacy

Dashlane stores your encrypted vault on its cloud servers. While the encryption is solid (AES-256), the architectural reality is that a third party holds a copy of your data. With KeePass, your vault is a local file that you control. No company stores a copy unless you explicitly choose to sync it via a cloud service. This distinction matters for users who prioritize data sovereignty.

### Vendor Independence

Dashlane is a proprietary platform. If the company changes its terms of service, raises prices further, gets acquired, or discontinues a feature you rely on, your options are limited. The open [KDBX format](/keepass/kdbx-format-guide/) is supported by dozens of independent applications across every operating system. You can switch apps at any time without re-exporting or converting your data.

### Open Source Transparency

KeePass and its ecosystem are open source. The encryption implementation, the database format, and the application code are all publicly auditable. You do not need to trust a company's security claims -- you can verify them yourself, or rely on the community of researchers who do. For more on how this transparency benefits you, see our guide on [KeePass encryption explained](/keepass/encryption-explained/).

## Before You Start: Back Up Everything

Before making any changes, take precautions to ensure you do not lose data during the migration.

1. **Back up your Dashlane vault.** Export a copy using the DASH (encrypted) format as a safety net. This Dashlane-specific backup can be re-imported into Dashlane if anything goes wrong.
2. **Note your entry count.** Check how many items are in your Dashlane vault (logins, secure notes, payment info, personal info). You will use this number later to verify the import.
3. **Keep Dashlane active.** Do not cancel your Dashlane subscription or delete your account until you have fully verified the migration. Plan on a two-to-four-week overlap period.

## Step 1: Export Your Data from Dashlane

Dashlane provides two export formats. You will use CSV for the migration and optionally DASH as a backup.

### Exporting via Dashlane Desktop or Web App

1. Open Dashlane and log in to your account.
2. Navigate to **Settings** (the gear icon or your profile menu).
3. Look for **Export data** or **Export vault** under the account or security section.
4. Select **CSV** as the export format.
5. Authenticate with your master password when prompted.
6. Save the CSV file to a secure location on your local drive -- not to a cloud-synced folder like Dropbox, Google Drive, or iCloud.

### Understanding the Two Export Formats

**CSV (Comma-Separated Values)**: A plain text file containing your credentials. This is the format you need for importing into KeePass. It works universally across all password managers but contains your passwords in unencrypted plain text.

**DASH (Dashlane Encrypted Archive)**: An encrypted backup that can only be read by Dashlane. This preserves more metadata and structure than CSV but cannot be imported into KeePass or any non-Dashlane application. Use this only as a safety backup.

### What the Dashlane CSV Export Includes

The Dashlane CSV export typically contains the following fields for login entries:

- **name** -- The entry title
- **url** -- The website address
- **username** -- Your login username or email
- **password** -- The password in plain text
- **note** -- Any notes attached to the entry
- **category** -- The folder or category in Dashlane
- **totp** -- TOTP secret key if two-factor authentication was stored

Secure notes are exported as separate entries with the note content in the appropriate field. Payment cards, IDs, and personal information items may be included in separate sections of the CSV or may require individual attention.

### What Does Not Export Cleanly

- **Password history**: Dashlane tracks password change history for entries. This history is not included in the CSV export. Only the current password is exported.
- **Attachments**: Any files attached to secure notes or entries are not included in the CSV.
- **Sharing relationships**: If you shared credentials with other Dashlane users, the sharing configuration does not transfer.
- **Dark web monitoring alerts**: Dashlane's security monitoring data stays within Dashlane.

## Step 2: Import into KeePass

With your CSV file in hand, you can now import it into your KeePass-compatible application of choice.

### Importing into KeePassXC

1. Open KeePassXC and create a new database, or open an existing one. If creating a new database, choose a strong master passphrase and leave the encryption settings at their defaults (AES-256 with Argon2id key derivation).
2. Go to **Database** then **Import** then **CSV File**.
3. Select your Dashlane CSV export file.
4. KeePassXC will display a preview and a column mapping interface. Map the columns as follows:
   - "name" to **Title**
   - "url" to **URL**
   - "username" to **User Name**
   - "password" to **Password**
   - "note" to **Notes**
   - "category" to **Group** (this preserves your Dashlane folder structure)
5. Check the box to treat the first row as field names.
6. Review the preview to confirm the mapping is correct.
7. Click **OK** to complete the import.

### Importing into KeePass 2.x

1. Open KeePass 2.x and open or create a database.
2. Go to **File** then **Import**.
3. Select **Generic CSV Importer** from the format list. Some versions also include a dedicated Dashlane CSV option.
4. Browse to your CSV file and configure the column mapping.
5. Complete the import.

### Importing into PanicVault

If you are an Apple user, [PanicVault](https://panicvault.com) provides a native macOS and iOS experience for working with KDBX files. You can first import the CSV into KeePassXC to create a KDBX database, then open that database in PanicVault on all your Apple devices. Alternatively, PanicVault may support direct CSV import -- check the app's current import options. For a full list of compatible apps, see our [KeePass-compatible apps guide](/keepass/compatible-apps/).

### Handling TOTP Secrets

If your Dashlane vault included TOTP (time-based one-time password) secrets for two-factor authentication, these should appear in the CSV export. KeePassXC supports TOTP natively -- after import, you can add TOTP secrets to each entry's properties and generate codes directly from your vault. Verify that the TOTP field was included in the export and mapped correctly during import.

## Step 3: Verify Your Data

Verification is the most important step. A migration is not complete until you have confirmed that every credential transferred correctly.

### Compare Entry Counts

Count the number of entries in your new KeePass database and compare it to the number of items in your Dashlane vault. If there is a discrepancy, investigate which entries are missing. Common causes include:

- Secure notes or payment cards that exported into a different section of the CSV
- Entries with special characters that caused CSV parsing errors
- Duplicate entries that were merged during import

### Spot-Check Critical Accounts

Log in to your most important accounts using credentials from your new KeePass database:

- Primary email accounts (Gmail, Outlook, iCloud)
- Banking and financial services
- Cloud storage services
- Social media accounts
- Work-related accounts and VPNs

Each successful login confirms that the credential imported correctly.

### Verify URLs and Usernames

Scan through your imported entries to ensure that URLs and usernames populated the correct fields. CSV column mapping errors can sometimes shift data into the wrong fields, putting a URL where the username should be or vice versa.

### Check Secure Notes

Open several secure notes and compare their content against the originals in Dashlane. Look for truncation, missing formatting, or character encoding issues.

## Step 4: Clean Up the Source

Once you have verified the migration is complete, take these cleanup steps.

### Delete the CSV Export File

The plain text CSV file contains all your passwords in unencrypted form. Delete it immediately after verification. Do not keep it as a backup -- if you need to re-export, you can do so from Dashlane while your account is still active.

### Back Up Your New KeePass Database

Create a backup of your KDBX file and store it in a separate location from the primary copy. An encrypted USB drive, a different device, or a secure cloud storage service are all reasonable options. For a comprehensive backup strategy, see our [KeePass database backup guide](/keepass/backup-database/).

### Decide on Your Dashlane Account

Keep your Dashlane account active for two to four weeks as a fallback. During this period, you may discover entries that did not migrate correctly. Once you are confident everything transferred, you can:

- Delete all entries in Dashlane but keep the account
- Delete the account entirely through Dashlane's account management settings
- Let the subscription lapse at the next renewal date

### Disable Dashlane Browser Extension

Remove or disable the Dashlane browser extension to prevent it from interfering with your new KeePass workflow. Install the browser extension for your chosen KeePass application instead (KeePassXC Browser for KeePassXC, for example).

## What Transfers and What Does Not

| Data Type | Transfers via CSV | Notes |
|-----------|:-:|-------|
| Login credentials | Yes | URL, username, password, and entry name |
| Secure notes | Yes | Text content transfers; formatting may change |
| Folders/categories | Yes | Maps to KeePass groups |
| TOTP secrets | Partial | Depends on Dashlane export version |
| Password history | No | Only current passwords export |
| Attachments | No | Must be manually downloaded and re-attached |
| Payment cards | Partial | May appear in notes; fields not structured |
| IDs and personal info | Partial | Often flattened into text |
| Sharing permissions | No | Sharing relationships are Dashlane-specific |
| Dark web monitoring | No | Dashlane-specific feature |

## Organizing Your New Vault

After the import, spend some time organizing your KeePass database for long-term usability.

### Refine the Group Structure

If your Dashlane categories imported as KeePass groups, review the structure and adjust it. KeePass supports unlimited nesting depth, so you can create a more detailed hierarchy than Dashlane allowed:

- **Email** -- All email account credentials
- **Financial** -- Banking, investment, payment services
- **Social Media** -- Social networking accounts
- **Shopping** -- E-commerce sites
- **Work** -- Professional accounts
- **Subscriptions** -- Streaming, software, news

### Clean Up Entry Titles

Dashlane sometimes generates entry titles from URLs or domain names. Rename entries to be descriptive and consistent (for example, "chase.com" becomes "Chase Banking").

### Set Up Autofill

Install the browser extension for your KeePass application and configure autofill. On Apple devices, PanicVault integrates with the system autofill framework on both macOS and iOS, providing a seamless transition from Dashlane's autofill experience. Our [compatible apps guide](/keepass/compatible-apps/) covers the autofill setup process for each platform.

## Related Articles

- [What Is the KDBX Format and Why It Matters](/keepass/kdbx-format-guide/)
- [KeePass Data Portability: Own Your Passwords Forever](/keepass/data-portability/)
- [How to Back Up Your KeePass Database](/keepass/backup-database/)
- [KeePass-Compatible Apps for Every Platform](/keepass/compatible-apps/)
- [Migrate from LastPass to KeePass](/keepass/migrate-from-lastpass/)
