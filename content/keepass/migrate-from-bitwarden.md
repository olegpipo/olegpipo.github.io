---
title: "Migrate from Bitwarden to KeePass"
description: "Complete guide to migrating from Bitwarden to KeePass. Export as JSON or CSV, import into KeePassXC, preserve TOTP secrets, and verify your data."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "Should I export Bitwarden as CSV or JSON for KeePass?"
    a: "Use JSON if possible. Bitwarden's JSON export preserves more data including folder structure, item types, TOTP secrets, and custom fields. CSV is simpler but loses some metadata. KeePassXC supports importing Bitwarden JSON directly."
  - q: "Do Bitwarden TOTP secrets transfer to KeePass?"
    a: "Yes. TOTP secrets are included in Bitwarden's JSON export and can be imported into KeePassXC, which supports TOTP natively. CSV exports may also include TOTP URIs depending on the Bitwarden version."
  - q: "Can I import Bitwarden JSON directly into KeePassXC?"
    a: "Yes. KeePassXC includes a dedicated Bitwarden JSON import option under Database > Import. This provides the cleanest migration path with the most data preserved."
  - q: "What does Bitwarden not export?"
    a: "Bitwarden exports do not include file attachments, Send items, organization vault data (unless you are an admin), or emergency access configurations. These must be handled separately."
  - q: "Why switch from Bitwarden to KeePass if Bitwarden is already open source?"
    a: "While Bitwarden's code is open source, your vault still lives on Bitwarden's cloud servers. KeePass gives you a local-first approach where your vault file stays on your devices. Some users also prefer eliminating the subscription cost for Bitwarden's premium features like TOTP support."
---

Bitwarden is one of the most respected password managers available, and its open source codebase sets it apart from most commercial competitors. Migrating from Bitwarden to a [KeePass-compatible application](/keepass/) is not about escaping a bad product -- it is about choosing a different architecture. Where Bitwarden is cloud-first with optional self-hosting, KeePass is local-first with optional cloud sync. If you prefer complete local control, no subscription costs, and the flexibility of the open KDBX format, this guide walks you through the migration process.

## Why Migrate from Bitwarden to KeePass

### Local-First Architecture

Bitwarden stores your encrypted vault on its cloud servers (or your own server if you self-host). Even with self-hosting, you need to maintain a server infrastructure. KeePass takes a fundamentally different approach: your vault is a file on your device. There is no server component, no sync infrastructure to maintain, and no cloud dependency. You can sync the file using any method you choose -- iCloud Drive, Dropbox, Syncthing, or a USB drive -- but the vault itself is always local.

### No Premium Tier

Bitwarden's free tier is generous, but several important features require a premium subscription: TOTP authentication, advanced reports, emergency access, and additional storage. With KeePass, every feature is available at no cost. KeePassXC supports TOTP natively, provides detailed entry management, and has no artificial feature restrictions.

### True Format Portability

Bitwarden uses its own vault format. While the project is open source and self-hostable, your data is still accessed through Bitwarden clients. The [KDBX format](/keepass/kdbx-format-guide/) used by KeePass is supported by dozens of independent applications across every platform. You can open the same vault file in KeePassXC, PanicVault, Strongbox, KeePassDX, or any other compatible app without any conversion. For more on why format independence matters, see our [data portability guide](/keepass/data-portability/).

### Simplicity

Self-hosting Bitwarden (or Vaultwarden) requires server maintenance, updates, backups, and security monitoring. A KeePass database is a single encrypted file. Back it up by copying it. Sync it by placing it in a shared folder. There is no server to maintain, no Docker containers to update, and no infrastructure to monitor.

## Before You Start: Back Up Everything

Prepare for the migration with these steps.

1. **Count your entries.** Note the total number of items in your Bitwarden vault, broken down by type: logins, secure notes, cards, and identities.
2. **Check for attachments.** If you use Bitwarden premium and have file attachments on entries, download them before exporting. Attachments are not included in either CSV or JSON exports.
3. **Note Send items.** Bitwarden Send (secure sharing) items are not included in vault exports. If you have active Sends, handle them separately.
4. **Review organization vaults.** If you belong to a Bitwarden organization, entries in organization collections require admin-level access to export. Personal vault items export normally.
5. **Keep Bitwarden active.** Maintain your account until the migration is fully verified.

## Step 1: Export Your Data from Bitwarden

Bitwarden offers two export formats, and the choice between them significantly affects the quality of your migration.

### JSON Export (Recommended)

The JSON export preserves the most data and is the recommended format for migrating to KeePass.

1. Open the Bitwarden web vault at vault.bitwarden.com, or use the desktop application.
2. Navigate to **Settings** then **Export vault** (or **Tools** then **Export vault** depending on your Bitwarden version).
3. Select **JSON** as the export format.
4. Enter your master password to authenticate.
5. Save the file to a secure, local location.

**What JSON preserves that CSV does not:**
- Folder structure with full hierarchy
- Item type distinctions (login, note, card, identity)
- TOTP secrets in their complete URI format
- Custom fields with their types (text, hidden, boolean)
- Multiple URIs per login entry
- URI match detection settings

### CSV Export (Alternative)

If you prefer a simpler format or need broader compatibility:

1. Follow the same steps as above but select **CSV** as the format.
2. The CSV will contain a flattened view of your vault.

The CSV export includes: folder, favorite flag, type, name, notes, fields, reprompt, login URI, login username, login password, and login TOTP.

### Encrypted JSON Export

Bitwarden also offers an encrypted JSON export protected by your master password or account encryption key. This is useful as a Bitwarden-specific backup but cannot be directly imported into KeePass. Use the unencrypted JSON for the migration.

### Security Precautions

Both CSV and unencrypted JSON exports contain your passwords in plain text. Handle the files accordingly:

- Save only to local storage, not cloud-synced folders.
- Delete securely after confirming the import.
- Do not share or transmit the file.
- Work in a private environment where your screen is not visible to others.

## Step 2: Import into KeePass

KeePassXC includes dedicated support for Bitwarden imports, making this migration particularly smooth.

### Importing Bitwarden JSON into KeePassXC

1. Open KeePassXC and create a new database or open an existing one. For new databases, set a strong master passphrase.
2. Go to **Database** then **Import** then **Bitwarden JSON File** (or look for Bitwarden in the import format list).
3. Select your Bitwarden JSON export.
4. KeePassXC will automatically map the Bitwarden fields to KeePass fields, preserving:
   - Folder structure as KeePass groups
   - Login URLs, usernames, and passwords
   - TOTP secrets
   - Notes
   - Custom fields
5. Review the import preview.
6. Click **OK** to complete the import.

This is the cleanest import path because KeePassXC understands the Bitwarden JSON structure natively. No manual column mapping is required.

### Importing Bitwarden CSV into KeePassXC

If you chose to export as CSV:

1. Go to **Database** then **Import** then **CSV File**.
2. Select the Bitwarden CSV.
3. Map columns to KeePass fields:
   - "name" to **Title**
   - "login_uri" to **URL**
   - "login_username" to **User Name**
   - "login_password" to **Password**
   - "notes" to **Notes**
   - "folder" to **Group**
4. Check the option to treat the first row as field names.
5. Complete the import.

### Importing into KeePass 2.x

1. Open KeePass 2.x and go to **File** then **Import**.
2. For JSON: Look for a Bitwarden import option or use a plugin that supports Bitwarden JSON.
3. For CSV: Use the **Generic CSV Importer** and configure column mapping.
4. Complete the import.

### Using PanicVault on Apple Devices

Apple users who want a native experience can create the KDBX database using KeePassXC, then open it in [PanicVault](https://panicvault.com) on macOS, iPhone, and iPad. PanicVault reads the KDBX format natively and provides system-level autofill on both platforms. Store the KDBX file in iCloud Drive for automatic sync across your Apple devices. For the complete list of KeePass-compatible apps, see our [compatible apps guide](/keepass/compatible-apps/).

### Handling TOTP Secrets

One of the key advantages of the Bitwarden migration is that TOTP secrets survive the export (especially via JSON). After importing:

1. Open an entry that should have TOTP configured.
2. In KeePassXC, check if the TOTP was imported correctly by going to the entry's TOTP settings.
3. Generate a test code and compare it against the code shown in Bitwarden. They should match within the same time window.
4. If using Bitwarden's free tier, you did not have TOTP support -- this is a feature upgrade in your new KeePass setup, as KeePassXC supports TOTP at no cost.

## Step 3: Verify Your Data

Thorough verification is essential, even with the high-fidelity Bitwarden JSON import.

### Compare Entry Counts

Count entries in KeePass by type and compare against your Bitwarden vault:

- Logins
- Secure notes
- Credit card entries
- Identity entries

Small discrepancies are normal if some item types did not convert cleanly.

### Test Critical Accounts

Log in to your highest-priority accounts:

- Primary email accounts
- Banking and financial services
- Cloud storage providers
- Work accounts and VPNs
- Developer platforms (GitHub, AWS, etc.)

### Verify Folder Structure

Check that the Bitwarden folder hierarchy translated correctly into KeePass groups. The JSON import should preserve this structure faithfully.

### Verify TOTP Codes

For every entry with TOTP, generate a code in KeePassXC and verify it works for login. This is critical because a corrupted TOTP secret could lock you out of an account.

### Check Custom Fields

If you used Bitwarden's custom fields feature, verify that custom fields imported correctly. In KeePassXC, custom fields appear in the entry's Advanced or Extra section.

## Step 4: Clean Up

Finalize the migration with these steps.

### Delete Export Files

Securely delete both the JSON or CSV export file and any intermediate files created during the process.

### Back Up Your KeePass Database

Create an immediate backup of your KDBX file. Store it in a separate location from the primary copy. Our [backup guide](/keepass/backup-database/) covers comprehensive strategies.

### Manage Your Bitwarden Account

Keep Bitwarden accessible for two to four weeks as a safety net. Once verified:

- Delete all vault items to remove data from Bitwarden's servers
- Cancel any premium subscription
- Delete the account if desired, or keep it dormant

If you were self-hosting Bitwarden or Vaultwarden, you can decommission the server after confirming the migration.

### Set Up Your New Workflow

Install the KeePassXC Browser extension for desktop autofill. Configure your mobile KeePass app for system-level autofill. Remove or disable the Bitwarden browser extension and mobile app to avoid conflicts.

## What Transfers and What Does Not

| Data Type | CSV | JSON | Notes |
|-----------|:-:|:-:|-------|
| Login credentials | Yes | Yes | URL, username, password |
| Folder structure | Partial | Yes | JSON preserves full hierarchy |
| TOTP secrets | Partial | Yes | JSON preserves complete TOTP URIs |
| Custom fields | Partial | Yes | JSON preserves field types |
| Secure notes | Yes | Yes | Text content transfers |
| Credit cards | Partial | Yes | JSON preserves structured fields |
| Identities | Partial | Yes | JSON preserves structured fields |
| Multiple URIs | No | Yes | CSV includes only the first URI |
| File attachments | No | No | Must download and re-attach |
| Send items | No | No | Not included in vault exports |
| Organization vault items | No | No | Requires admin-level export |
| Emergency access config | No | No | Bitwarden-specific feature |

## Related Articles

- [What Is the KDBX Format and Why It Matters](/keepass/kdbx-format-guide/)
- [KeePass Data Portability: Own Your Passwords Forever](/keepass/data-portability/)
- [KeePass Encryption Explained](/keepass/encryption-explained/)
- [Migrate from 1Password to KeePass](/keepass/migrate-from-1password/)
- [Migrate from LastPass to KeePass](/keepass/migrate-from-lastpass/)
