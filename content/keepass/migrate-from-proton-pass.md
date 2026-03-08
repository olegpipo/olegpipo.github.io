---
title: "Migrate from Proton Pass to KeePass"
description: "Step-by-step guide to migrating from Proton Pass to KeePass. Export your vault as CSV, import into KeePassXC, and understand what transfers and what stays."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "Can I export my Proton Pass passwords to KeePass?"
    a: "Yes. Proton Pass lets you export your vault as CSV or PGP-encrypted file through Settings > Export. The CSV can be imported into any KeePass-compatible application like KeePassXC or PanicVault."
  - q: "Do Proton Pass email aliases transfer to KeePass?"
    a: "No. Proton Pass email aliases (hide-my-email addresses) are tied to Proton's infrastructure and remain functional in your Proton account, but the alias feature itself does not transfer. Your login credentials using those aliases do export normally."
  - q: "What is the PGP-encrypted export in Proton Pass?"
    a: "Proton Pass offers a PGP-encrypted export option that protects your exported data with PGP encryption. This is more secure than plain CSV for storage, but you will need to decrypt it before importing into KeePass."
  - q: "Does Proton Pass export include TOTP secrets?"
    a: "Yes. Proton Pass CSV exports typically include TOTP secrets for entries where two-factor authentication was configured. These can be imported into KeePassXC, which supports TOTP natively."
  - q: "Should I delete my Proton Pass account after migrating?"
    a: "You can stop using Proton Pass for password storage, but consider keeping your Proton account if you use other Proton services like Proton Mail or Proton VPN. Email aliases created through Proton Pass will continue working as long as your Proton account remains active."
---

Proton Pass is a privacy-focused password manager from the makers of Proton Mail, and it is a solid choice for users already invested in the Proton ecosystem. However, if you want your credentials in an open, locally stored format -- free from any cloud service dependency -- migrating to a [KeePass-compatible application](/keepass/) gives you that independence. This guide covers the complete migration from Proton Pass to KeePass, with particular attention to the unique aspects of Proton Pass like email aliases and the PGP-encrypted export option.

## Why Migrate from Proton Pass to KeePass

### True Local Storage

Proton Pass stores your encrypted vault on Proton's servers. While Proton's zero-access encryption is strong and the company has an excellent privacy reputation, the fundamental architecture still involves a third party holding your encrypted data. With KeePass, your vault file lives only on your devices unless you explicitly choose to sync it elsewhere. This is the most direct form of data sovereignty available.

### Open Format Independence

Proton Pass uses its own vault format. While Proton is open source and committed to transparency, your data is still tied to Proton Pass applications for day-to-day access. The [KDBX format](/keepass/kdbx-format-guide/) used by KeePass is an open standard supported by dozens of independent apps. You can use KeePassXC on Linux, PanicVault on macOS and iOS, KeePassDX on Android, and freely switch between them. Our [data portability guide](/keepass/data-portability/) explores this advantage in depth.

### No Subscription Required

Proton Pass offers a free tier with limitations and paid plans with additional features. KeePass-compatible applications are completely free with no premium tiers. Every feature is available at no cost, permanently.

### Ecosystem Independence

If you use Proton Pass as part of a broader Proton subscription (bundled with Proton Mail, VPN, and Drive), you may be paying for password management as part of a package you do not fully utilize. Migrating your passwords to KeePass lets you evaluate whether you still need the Proton bundle or whether a more targeted set of services better fits your needs.

## Before You Start: Back Up Everything

Prepare carefully before starting the export.

1. **Count your entries.** Note the total number of logins, secure notes, credit cards, and other items in your Proton Pass vault.
2. **Identify email aliases.** If you used Proton Pass's hide-my-email alias feature, make a list of which accounts use Proton aliases. These aliases remain functional through your Proton account but deserve special attention during migration.
3. **Check for TOTP entries.** Note which entries have TOTP (two-factor authentication) secrets stored. Proton Pass exports TOTP secrets in CSV, which is a significant advantage.
4. **Keep Proton Pass active.** Do not delete vault data until the migration is fully verified. Since Proton Pass is often part of a broader Proton account, there is no urgency to delete the password manager data even after migrating.

## Step 1: Export Your Data from Proton Pass

Proton Pass provides two export formats, both accessible through the settings menu.

### Export Steps

1. Open Proton Pass (desktop app, browser extension, or web interface).
2. Navigate to **Settings**.
3. Find the **Export** option.
4. Choose your export format:
   - **CSV** -- Plain text format compatible with all password managers. Use this for the import into KeePass.
   - **PGP-encrypted** -- An encrypted version of the export for secure storage. This requires decryption before import.
5. Enter your Proton account password to authenticate.
6. Save the file to a secure, local location.

### CSV vs. PGP-Encrypted Export

For the migration itself, you want the **CSV** file because it can be directly imported into KeePassXC and other KeePass-compatible applications.

The **PGP-encrypted** export is useful as a secure backup of your Proton Pass data. If you know how to work with PGP encryption, you can export in this format as a safety net, then decrypt it later if needed. For most users, the CSV export is sufficient for the migration, and your new KDBX database becomes your authoritative backup once verified.

### What the Proton Pass CSV Export Includes

The Proton Pass CSV export is well structured and includes:

- **name** -- The entry title
- **url** -- The website URL (Proton Pass may include multiple URLs per entry)
- **username** -- Your login username or email address
- **password** -- The password in plain text
- **note** -- Notes attached to the entry
- **totp** -- TOTP secret URI, if two-factor authentication was configured
- **vault** -- The vault name (if you use multiple vaults)

### What Does Not Transfer

- **Email aliases**: Proton Pass's hide-my-email feature creates email aliases that route to your Proton Mail inbox. These aliases are tied to Proton's infrastructure. The alias addresses will continue to work as long as your Proton account exists, but the alias management functionality does not move to KeePass. Your login credentials that use alias addresses will export normally -- only the alias management feature stays in Proton.
- **File attachments**: Not included in the CSV export.
- **Password history**: Only current passwords are exported.
- **Passkeys**: Passkeys stored in Proton Pass are not exportable via CSV.
- **Credit card details**: These may export with limited structure and require manual reorganization.

### The Email Alias Consideration

This deserves special attention because it is unique to Proton Pass. If you created hide-my-email aliases for various accounts (for example, random-string@proton.me for your Netflix account), those aliases are part of your Proton Mail account, not your password vault. They will continue to forward email to your inbox regardless of whether you use Proton Pass.

When you migrate to KeePass, the login entries using these aliases will show the alias email address as the username. Everything works as before -- you just manage the passwords in KeePass instead of Proton Pass. The only thing you lose is the ability to create new aliases through the password manager interface. You can still manage existing aliases through Proton Mail settings.

## Step 2: Import into KeePass

With your CSV file exported, import it into your KeePass-compatible application.

### Importing into KeePassXC

1. Open KeePassXC and create a new database or open an existing one. Choose a strong master passphrase for new databases.
2. Go to **Database** then **Import** then **CSV File**.
3. Select the Proton Pass CSV file.
4. Map the columns to KeePass fields:
   - "name" to **Title**
   - "url" to **URL**
   - "username" to **User Name**
   - "password" to **Password**
   - "note" to **Notes**
   - "vault" to **Group** (if you used multiple vaults)
5. Check the option to treat the first row as field names.
6. Review the preview and confirm correctness.
7. Click **OK** to import.

### Importing TOTP Secrets

One of Proton Pass's migration advantages is that TOTP secrets are included in the CSV export. After importing into KeePassXC:

1. Open entries that should have TOTP configured.
2. If the TOTP URI was mapped to a custom field during import, you can move it to the entry's TOTP configuration.
3. In KeePassXC, right-click the entry, select **TOTP** then **Set up TOTP**, and paste the TOTP secret or URI.
4. Verify that the generated codes match what Proton Pass was producing.

If TOTP data was included in the notes field instead of a dedicated column, extract the TOTP URI from the notes and configure it properly in KeePassXC.

### Importing into KeePass 2.x

1. Open KeePass 2.x and open or create a database.
2. Go to **File** then **Import** then **Generic CSV Importer**.
3. Select your CSV file and configure column mapping.
4. Complete the import. Note that KeePass 2.x requires a plugin for TOTP support (KeeOtp or similar).

### Importing on Apple Devices

For a seamless Apple experience, create your KDBX database using KeePassXC, then open it in [PanicVault](https://panicvault.com) on your Mac, iPhone, or iPad. PanicVault provides native system autofill on both macOS and iOS and supports iCloud Drive sync for your KDBX file. This makes the transition from Proton Pass particularly smooth for users in the Apple ecosystem. Check our [compatible apps guide](/keepass/compatible-apps/) for the full list of KeePass-compatible applications.

## Step 3: Verify Your Data

Careful verification prevents unpleasant surprises weeks later.

### Compare Entry Counts

Count entries in KeePass and compare to your Proton Pass vault count. If using multiple Proton vaults, verify that entries from each vault are present.

### Test Critical Accounts

Log in to your most important accounts using credentials from KeePass:

- Primary email accounts
- Banking and financial services
- Cloud storage services
- Work-related accounts
- Social media profiles

Pay special attention to accounts that use Proton email aliases as the username. Confirm that the alias address is correctly stored in the username field.

### Verify TOTP Codes

For entries with TOTP configured, generate a code in KeePassXC and compare it against the code shown in Proton Pass. The codes should match (within the same 30-second window). If they do not match, the TOTP secret may not have transferred correctly -- re-check the TOTP URI.

### Check Notes and Special Items

Review secure notes, credit card entries, and any items with custom fields. Verify that the content is complete and properly formatted.

## Step 4: Clean Up

Finalize the migration with these cleanup steps.

### Delete the CSV Export

Securely delete the plain text CSV file. It contains all your credentials unencrypted and should not be retained.

### Back Up Your KeePass Database

Create a backup of your new KDBX file and store it separately from the primary copy. See our [backup guide](/keepass/backup-database/) for comprehensive strategies.

### Manage Your Proton Account

Since Proton Pass is often bundled with other Proton services, you may want to keep your Proton account active for Proton Mail, VPN, or Drive. You can simply stop using Proton Pass for password management while keeping the account for other services. Your email aliases will continue to function.

If you want to clean up:

- Delete all items in Proton Pass to remove stored credentials from Proton's servers
- Keep your Proton account active for email aliases and other services
- Adjust your Proton subscription tier if you no longer need the full bundle

### Disable Proton Pass Autofill

Remove or disable the Proton Pass browser extension and mobile app autofill. Replace it with the KeePassXC Browser extension for desktop and your chosen KeePass app's autofill for mobile devices.

## What Transfers and What Does Not

| Data Type | Transfers via CSV | Notes |
|-----------|:-:|-------|
| Login credentials | Yes | URL, username, password, title, notes |
| TOTP secrets | Yes | URI format; configure in KeePassXC TOTP settings |
| Vault structure | Yes | Vault names can map to KeePass groups |
| Secure notes | Yes | Text content transfers |
| Email aliases | Functional but not managed | Aliases stay in Proton; credentials using them export normally |
| Credit cards | Partial | Fields may need reorganization |
| File attachments | No | Must download and re-attach manually |
| Password history | No | Only current passwords export |
| Passkeys | No | Must re-create on each service |

## Related Articles

- [What Is the KDBX Format and Why It Matters](/keepass/kdbx-format-guide/)
- [KeePass Data Portability: Own Your Passwords Forever](/keepass/data-portability/)
- [KeePass-Compatible Apps for Every Platform](/keepass/compatible-apps/)
- [KeePass vs. Proprietary Password Managers](/keepass/vs-proprietary/)
- [Migrate from Bitwarden to KeePass](/keepass/migrate-from-bitwarden/)
