---
title: "How to Migrate from 1Password to KeePass: Complete Guide"
description: "Step-by-step guide to migrating from 1Password to KeePass. Export your vaults, import passwords, handle tags and attachments, and set up sync."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

Switching from 1Password to a [KeePass-compatible application](/keepass/) is a decision driven by different motivations than most password manager migrations. 1Password has maintained a strong security track record, so the reasons for leaving tend to center on philosophy rather than crisis: a preference for open source software, a desire to eliminate subscription costs, concerns about data sovereignty, or a commitment to owning your vault file outright rather than trusting it to a cloud service. Whatever your reasons, this guide covers every step of the migration process, from exporting your 1Password data to verifying that every credential, attachment, and secure note has been successfully transferred.

## Why Switch from 1Password to KeePass

### Subscription Costs

1Password transitioned from a one-time purchase model to a subscription model several years ago. The current pricing requires an ongoing monthly or annual payment for individuals, with higher tiers for families and businesses. Over the lifetime of use, these costs accumulate significantly. KeePass-compatible applications are free and open source, with no subscription required. The total cost of ownership is zero, permanently.

### Data Sovereignty

1Password stores your encrypted vault data on its servers (or on servers managed by its infrastructure providers). While the encryption is strong and the company has not suffered a significant breach, the architectural reality is that a third party holds a copy of your encrypted data. Some users are uncomfortable with this arrangement on principle, regardless of the company's track record.

With KeePass, your vault is a file on your device. No copy exists on any server unless you explicitly place one there. You control the storage, the backups, and the access. If you want to understand the broader question of whether commercial password managers deserve your trust, our analysis of [trusting password managers with your data](/password-managers/trust-with-passwords/) explores the tradeoffs in depth.

### Open Source Transparency

1Password is proprietary software. While the company publishes security white papers and undergoes third-party audits, the source code is not available for independent review. KeePass and KeePassXC are open source -- anyone can inspect the code, verify the encryption implementation, and confirm that the software does exactly what it claims to do. For users who value transparency as a security property, this distinction matters.

### Vendor Independence

Proprietary password managers create a dependency relationship. If the company changes its pricing, discontinues a feature, or pivots its business model, you are affected. If the company is acquired, its privacy policies and security priorities may change. With KeePass, the KDBX file format is an open standard supported by dozens of independent applications -- including [PanicVault](https://panicvault.com) for macOS and iOS users who want a native Apple experience. You are never locked into a single vendor's ecosystem.

## Step 1: Prepare for the Export

Before exporting your data from 1Password, take a few preparatory steps to ensure a clean migration.

### Audit Your Vaults

1Password supports multiple vaults (Personal, Shared, Travel, and custom vaults). Review each vault and note which ones contain data you want to migrate. If you have vaults shared with family members or team members, decide whether those shared credentials need to be included in your personal KeePass database or handled separately.

### Identify Non-Standard Items

1Password stores more than just login credentials. Common item types include:

- **Logins** -- Standard username and password entries with associated URLs
- **Secure Notes** -- Free-form encrypted text
- **Credit Cards** -- Payment card details
- **Identities** -- Personal information like addresses and phone numbers
- **Software Licenses** -- Product keys and license information
- **Documents** -- File attachments stored in the vault
- **SSH Keys** -- Cryptographic keys for server access
- **API Credentials** -- Tokens and secrets for developer tools

Not all of these item types will export cleanly or import directly into KeePass. Knowing what you have helps you plan for manual transfers where needed.

### Choose Your Export Format

1Password offers two primary export formats:

**1PUX (1Password Unencrypted Export)**: This is 1Password's native export format. It preserves the most data, including attachments, tags, and item metadata. However, it is specific to 1Password and not directly importable by most KeePass applications. Some import tools and converters support it, but availability varies.

**CSV (Comma-Separated Values)**: This is the universal format. It works with virtually every password manager's import function. The tradeoff is that CSV exports are flat -- they lose the hierarchical structure of vaults and tags, and they do not include attachments or binary data. Complex item types like credit cards and identities may be flattened into text fields.

For most migrations, the CSV export is the practical choice. If you have significant attachments or complex items, you may want to export in both formats: CSV for the bulk import and 1PUX as a reference for items that need manual attention.

## Step 2: Export Your Data from 1Password

### Exporting via the 1Password Desktop Application

1. Open the 1Password desktop application.
2. Select the vault you want to export from the vault sidebar. If you want to export all vaults, you may need to repeat the process for each one, or select "All Vaults" if the option is available.
3. Go to **File** then **Export** (on macOS) or look for the export option in the application menu.
4. Choose your export format (CSV or 1PUX).
5. Authenticate with your master password or biometrics.
6. Save the export file to a secure location on your local drive.

### Exporting via the 1Password Web Interface

1. Log in to your 1Password account at my.1password.com.
2. Click your name or profile icon in the top right corner.
3. Select **Export Data** from the dropdown.
4. Choose the vault to export and the format.
5. Authenticate and download the file.

### Security Precautions for the Export File

Just as with any password manager export, the resulting file contains your credentials in an unencrypted format. Handle it with care:

- Save it only to local storage, never to cloud-synced folders.
- Do not transmit it via email, messaging apps, or file sharing services.
- Delete it securely after the import is verified.
- If you step away from your computer during the migration process, lock your screen.

## Step 3: Import into KeePass

### Importing CSV into KeePassXC

1. Open KeePassXC and either create a new database or open an existing one. If creating a new database, choose a strong master passphrase and configure the encryption settings (the defaults -- AES-256 with Argon2 key derivation -- are appropriate for most users).
2. Go to **Database** then **Import** then **CSV File**.
3. Select your 1Password CSV export.
4. KeePassXC will display a column mapping interface. Map the 1Password CSV columns to KeePass fields:
   - "Title" or "Login" maps to **Title**
   - "Website" or "URL" maps to **URL**
   - "Username" maps to **User Name**
   - "Password" maps to **Password**
   - "Notes" maps to **Notes**
   - "Type" or "Vault" can be used for group assignment or ignored
5. Enable the option to treat the first row as field names.
6. Review the preview to confirm the mapping looks correct.
7. Click **OK** to complete the import.

### Importing CSV into KeePass 2.x

1. Open KeePass 2.x and open or create your database.
2. Go to **File** then **Import**.
3. Select **Generic CSV Importer** from the format list.
4. Browse to your 1Password CSV file.
5. Configure the column mapping in the import dialog, matching each CSV column to the appropriate KeePass field.
6. Complete the import.

### Importing 1PUX Format

If you exported in 1PUX format, your options are more limited. KeePassXC does not natively support 1PUX imports. However, several approaches are available:

- **Third-party conversion tools**: Open source tools exist that convert 1PUX files to KDBX or CSV format. Search for "1pux to kdbx converter" for current options. Verify that any tool you use is reputable and open source before feeding it your password data.
- **Import into another manager first**: Some password managers that support both 1PUX import and KDBX export can serve as an intermediary. This is a workaround rather than an ideal solution.

For most users, the CSV path is simpler and sufficient.

## Step 4: Handle Vaults and Tags

1Password's organizational structure uses vaults (top-level containers) and tags (labels that can span vaults). KeePass uses groups (hierarchical folders) and does not have a native tagging system, though KeePassXC supports a tag-like feature through entry attributes.

### Recreating Vault Structure

If you exported multiple vaults separately, import each one into a different group in your KeePass database. Create top-level groups that mirror your 1Password vault names:

- **Personal** -- Your individual credentials
- **Shared** -- Credentials shared with family or team
- **Work** -- Professional accounts

Within each group, create subgroups for categories as needed. KeePass supports unlimited nesting depth, so you can build a structure as detailed as you want.

### Handling Tags

Tags from 1Password do not transfer through CSV export. If you relied heavily on tags for organization, you have two options:

1. **Recreate tags as groups.** If a tag represented a category (like "Finance" or "Social Media"), create a corresponding group in KeePass and move entries into it.
2. **Use custom attributes.** In KeePassXC, you can add custom string fields to entries. Create a field called "Tags" and enter the relevant tag names. This preserves the metadata even though it does not function as a searchable tag system.

Neither approach perfectly replicates 1Password's tagging, but the group hierarchy in KeePass is flexible enough to accommodate most organizational needs.

## Step 5: Migrate Attachments and Secure Notes

### Attachments

1Password allows you to attach files to entries -- documents, photos, certificates, and other binary files. These attachments are not included in CSV exports. If you exported in 1PUX format, attachments may be included depending on the export options.

For attachments that did not export:

1. Open 1Password and navigate to each entry that has attachments.
2. Download the attachment to your local drive.
3. In your KeePass database, open the corresponding entry.
4. In KeePass 2.x, use the **Advanced** tab to add file attachments. In KeePassXC, use the entry editor's attachment section.
5. Attach the downloaded file to the entry.

This is a manual process and can be time-consuming if you have many attachments. Prioritize the most important ones first and work through the rest over time.

### Secure Notes

Secure notes from 1Password should export as entries in the CSV file, typically with the note content in the notes field and no URL or password. Verify that these imported correctly by spot-checking a few. Long notes or notes with special formatting may be truncated or altered during the CSV export.

### Credit Cards and Identities

These structured item types are flattened during CSV export. The fields (card number, expiration date, CVV for credit cards; name, address, phone for identities) will typically appear in the notes field as plain text. In KeePass, you can:

- Leave them as notes within an entry, which works fine for reference purposes.
- Recreate them using custom string fields in the entry editor, which provides more structured storage.

## Step 6: Verify the Migration

Thorough verification prevents unpleasant surprises weeks later when you try to log into an account and find the credential is missing or incorrect.

### Count and Compare

Compare the total number of items in your 1Password vaults against the number of entries in your KeePass database. Account for the fact that some item types (like identities and credit cards) may have been combined or reformatted during import.

### Test Critical Accounts

Log in to your highest-priority accounts using credentials from KeePass:

- Primary email accounts
- Banking and financial services
- Cloud storage (Google Drive, iCloud, Dropbox)
- Work accounts and VPNs
- Social media profiles

Each successful login confirms that the credential transferred correctly.

### Verify Secure Notes and Special Items

Open several secure notes and compare their content against the originals in 1Password. Check for truncation, character encoding issues, or missing formatting.

### Check for Missing Entries

If your count comparison revealed discrepancies, identify which entries are missing. Common causes include:

- Items in vaults you did not export
- Entries with special characters that broke CSV parsing
- Item types that the importer did not recognize
- Entries in the 1Password Trash that were excluded from the export

## Step 7: Set Up Sync

One of the most significant workflow differences between 1Password and KeePass is synchronization. 1Password syncs automatically through its cloud infrastructure. KeePass requires you to configure sync yourself.

### File-Based Sync Options

Since your KeePass database is a single file, you can sync it using any file synchronization service:

- **Syncthing** -- Open source, peer-to-peer sync with no cloud server. Your data travels directly between your devices, encrypted in transit.
- **Dropbox, Google Drive, or iCloud** -- Place your database file in a synced folder. The file itself is encrypted by KeePass, so even if the cloud provider is compromised, the vault contents remain protected. Apple users migrating from 1Password may find iCloud Drive particularly convenient, especially when paired with a native macOS/iOS client like PanicVault or Strongbox.
- **Nextcloud or other self-hosted solutions** -- For maximum control, host your own sync server.

### Conflict Resolution

When syncing a KeePass database file across devices, conflicts can arise if you edit the database on two devices simultaneously before a sync occurs. KeePassXC and KeePass 2.x both include merge capabilities that can resolve most conflicts automatically, but the safest practice is to ensure your database is synced before making changes on a different device.

For a detailed comparison of KeePass-compatible apps and their sync capabilities, see our [compatible apps guide](/keepass/compatible-apps/). For ensuring your vault is protected against data loss, our [backup guide](/keepass/backup-database/) covers comprehensive backup strategies.

## Post-Migration Considerations

### Transition Period

Keep your 1Password account active for at least two to four weeks after the migration. During this period, you may discover entries that did not migrate correctly, attachments you forgot to transfer, or accounts whose credentials need to be looked up in the original vault. Once you are confident that everything has been transferred, you can cancel your 1Password subscription and delete your account.

### Browser Password Saving

If you previously relied on 1Password's browser extension for autofill, you will need to install the browser extension for your chosen KeePass application. KeePassXC offers a well-maintained browser extension that provides similar functionality. After installing the extension and connecting it to your database, disable your browser's built-in password saving to avoid credential sprawl. For a comparison of browser-based password storage versus dedicated managers, see our analysis of [password managers versus browser saving](/password-managers/vs-browser-saving/).

### Family and Team Sharing

1Password's family and team plans include built-in sharing features. If you were sharing vaults with others, you will need to establish a new sharing workflow. Options include:

- A shared KeePass database file distributed to authorized users, with the passphrase communicated through a separate secure channel.
- A shared database file placed in a jointly accessible synced folder.
- Separate databases for personal and shared credentials.

### Evaluate Your New Workflow

After a week or two of daily use, evaluate whether your KeePass setup meets your needs. Are you able to autofill credentials efficiently? Is sync working reliably? Are there entries that need better organization? The flexibility of KeePass means you can customize your workflow significantly, but it also means you need to invest some initial effort in configuration.

If you migrated from LastPass before moving to 1Password, or are comparing migration approaches, our [LastPass to KeePass migration guide](/keepass/migrate-from-lastpass/) covers the specifics of that transition path. For understanding how your vault file format works under the hood, our [data portability guide](/keepass/data-portability/) explains the open standards that protect your ability to move freely between applications.

## Conclusion

Migrating from 1Password to KeePass is a deliberate choice to trade convenience for control. The process requires more manual effort than switching between cloud-based managers, because you are taking direct ownership of your data rather than handing it to a new service. The CSV export path handles the vast majority of credentials cleanly, while attachments and complex item types may require individual attention.

The payoff is a password vault that belongs entirely to you: stored locally, encrypted with algorithms you can verify, managed by software you can inspect, and free from subscription fees or vendor dependencies. Your passwords are among your most sensitive digital assets. Storing them in an open format under your direct control is one of the most meaningful steps you can take toward genuine digital sovereignty.
