---
title: "How to Switch From 1Password: Migration Guide"
description: "Step-by-step guide to switching from 1Password to PanicVault or another password manager. Export vaults, preserve tags, and migrate TOTP secrets."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

Switching from 1Password -- whether because of subscription fatigue, data portability concerns, or simply a preference for owning your data in an open format -- is more straightforward than most people expect. 1Password provides several export options, and the import process into KDBX-compatible managers like PanicVault takes only a few minutes. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, covers every step including the details that other migration guides skip: custom fields, TOTP secrets, document attachments, and multiple vaults.

## Why People Leave 1Password

Understanding your motivation helps you choose the right replacement:

- **Subscription cost**: 1Password costs $36/year for individuals or $60/year for families. Over five years, that is $180-300. A one-time purchase like PanicVault or a free tool like KeePassXC eliminates this ongoing expense.
- **Data portability**: 1Password stores data in a proprietary format. The [KDBX format](/keepass/) used by PanicVault and KeePassXC is an open standard supported by dozens of apps -- you are never locked in.
- **Cloud dependency**: 1Password requires their cloud service. PanicVault stores your vault as a local file you control, synced via [iCloud Drive or Google Drive](/cloud-sync/) -- or any other file provider of your choosing.
- **Simplicity**: Some users find 1Password's feature set has grown beyond what they need. A focused tool that does core password management well may suit them better.

None of these are criticisms of 1Password's security or quality -- it is an excellent product. But excellent products are not always the right fit.

## Before You Begin

### Preparation Checklist

- [ ] 1Password installed on your Mac (the desktop app offers the best export options)
- [ ] Your new password manager installed and a vault created (see [first-time setup](/guides/first-time-setup/))
- [ ] A clear understanding of which 1Password vaults you need to export (Personal, Shared, Archive, etc.)
- [ ] 30-60 minutes of focused time
- [ ] Knowledge of which entries have TOTP/2FA -- you will handle these separately

### What Transfers Cleanly

- Website credentials (URL, username, password)
- Secure notes (text content)
- Basic custom fields
- Folder/vault structure (as groups)
- Tags (as tags in KDBX, where supported)

### What Requires Extra Attention

- **TOTP secrets**: May or may not export depending on the method. Plan to re-enroll if they do not
- **Document attachments**: Files attached to 1Password entries do not export via CSV. Save them separately
- **Credit cards and identities**: May export as secure notes rather than structured entries
- **Shared vaults**: Only your own vaults export. Items shared by others need to be re-shared through your new manager
- **Password history**: Only the current password exports

## Step 1: Export From 1Password

### Method A: 1PUX Export (Most Complete)

1Password's native export format (.1pux) preserves the most data:

1. Open 1Password on your Mac
2. Go to **File > Export** (or **1Password > Export** depending on version)
3. Authenticate with your account password
4. Select the vault to export (repeat for each vault if you have multiple)
5. Choose **1Password Unencrypted Export (.1pux)** format
6. Save the file

The 1PUX format is the most complete export option, including TOTP secrets, custom fields, and structured data. However, not all target managers can read it directly -- you may need to use a conversion tool.

### Method B: CSV Export (Most Compatible)

CSV is universally importable but loses some structure:

1. Open 1Password on your Mac
2. Go to **File > Export**
3. Authenticate with your account password
4. Select the vault to export
5. Choose **CSV** format
6. Save the file

**What CSV loses**: TOTP secrets, document attachments, custom field structure, and item types (everything becomes a generic login). Credit cards and identities export as text.

### Method C: Individual Item Copy (For Small Vaults)

If you have fewer than 50 entries, you can manually recreate them:

1. Open 1Password
2. For each entry, view the details
3. Create a corresponding entry in your new password manager
4. Copy each field individually

This is tedious but guarantees accuracy for small vaults.

### Exporting Multiple Vaults

If you have Personal, Shared, and Archive vaults:

1. Export each vault separately
2. Import each into your new manager as a separate group/folder
3. Or merge them during import if you prefer a single vault with folders

## Step 2: Import Into Your New Password Manager

### Importing Into PanicVault

1. Open PanicVault on your Mac
2. Open your KDBX database (or create one)
3. Go to **File > Import**
4. Select the appropriate format:
   - If you exported as 1PUX: Choose 1Password format if available, or convert to CSV first
   - If you exported as CSV: Choose **1Password CSV** or **Generic CSV**
5. Select your exported file
6. Review the field mapping:
   - Title → Title
   - URL → URL
   - Username → Username
   - Password → Password
   - Notes → Notes
   - Tags → Tags (if supported)
7. Confirm the import

### Importing Into KeePassXC

1. Open KeePassXC and unlock your database
2. Go to **Database > Import**
3. For 1PUX files: Use **Import > 1Password** if your KeePassXC version supports it
4. For CSV files: Use **Import > CSV File** and map columns:
   - Map 1Password's `Title` to KeePassXC's `Title`
   - Map `Username` to `Username`
   - Map `Password` to `Password`
   - Map `URL` to `URL`
   - Map `Notes` to `Notes`
5. Click OK to complete

For additional detail, see our [1Password to KeePass migration guide](/keepass/migrate-from-1password/).

### Importing Into Bitwarden

1. Log into vault.bitwarden.com
2. Go to **Tools > Import Data**
3. Select **1Password (1pux)** or **1Password (csv)** from the format dropdown
4. Upload your file
5. Click **Import Data**

## Step 3: Handle TOTP / Two-Factor Secrets

This is the step most migration guides gloss over, and it is the one that causes the most problems.

### If Your TOTP Secrets Exported (1PUX Format)

Check your imported entries for TOTP fields. If the secrets transferred:

1. Open an entry in your new password manager that had TOTP in 1Password
2. Look for a TOTP or OTP field with a secret key (usually a long string starting with `otpauth://` or a base32-encoded key)
3. If present, your manager should now generate the same 6-digit codes that 1Password did
4. **Verify**: Log into the site, go through the 2FA prompt, and confirm your new manager generates the correct code

### If Your TOTP Secrets Did Not Export (CSV Format)

You need to re-enroll 2FA for each affected account:

1. Make a list of every account where you used 1Password as your TOTP authenticator
2. For each account:
   a. Log in using your migrated credentials
   b. Go to the account's security settings
   c. Disable the existing 2FA
   d. Re-enable 2FA, this time scanning the QR code with your new password manager (PanicVault supports TOTP natively)
   e. Save the backup/recovery codes in the entry's notes field
3. Do not delete 1Password until you have re-enrolled all 2FA accounts

See our [2FA setup guide](/guides/setup-2fa/) for detailed instructions on configuring TOTP in PanicVault.

## Step 4: Handle Special Entry Types

### Credit Cards

1Password stores credit cards as a structured item type. In CSV exports, they become text entries. In your new manager:

1. Find the imported credit card entries
2. If your manager supports a credit card entry type, recreate them in the proper format
3. If not, store them as secure notes with structured information
4. See our guide on [storing credit cards and IDs](/guides/store-notes-cards/)

### Identity Documents

Similar to credit cards, identity documents (passports, driver's licenses) may not import as structured data. Recreate them manually in your new manager.

### Software Licenses

These typically export as secure notes. Verify the license keys are intact and add any missing metadata (purchase date, vendor, expiration).

### Document Attachments

1Password allows attaching files to entries. These do not export via CSV or 1PUX:

1. Before deactivating 1Password, go through entries with attachments
2. Download each attachment
3. Decide whether to store them in your new manager's notes, as separate encrypted files, or in a secure storage location
4. Attachments are typically things like recovery key PDFs, scanned documents, or screenshots -- handle each appropriately

## Step 5: Verify and Validate

### The Verification Checklist

1. **Entry count**: Compare the number of entries in 1Password vs. your new vault. Account for the difference (shared items that do not export, entry types that merged, etc.)
2. **Critical accounts**: Log into your 5 most important accounts using only your new password manager
3. **TOTP verification**: Generate a 2FA code from your new manager and confirm it works on at least 3 accounts
4. **Secure notes**: Open your most important secure notes and verify the content is complete
5. **Search**: Search for several entries to ensure they are findable
6. **AutoFill**: Visit a website in Safari and confirm [AutoFill](/guides/autofill-setup/) offers credentials from your new manager

### Common Issues After Import

**Duplicate entries**: If you imported multiple vaults, some entries may overlap. Merge duplicates, keeping the entry with the most complete information.

**Broken URLs**: 1Password's URL format may differ from your new manager's expectations. Check entries where AutoFill does not trigger and fix the URLs.

**Tags not importing**: If tags did not transfer, re-create the most important ones. This is a good opportunity to simplify your tagging system.

**Garbled characters in notes**: Special characters or formatting in secure notes may not survive the CSV export. Check important notes and fix any encoding issues.

## Step 6: Transition and Deactivation

### Two-Week Parallel Period

Run both password managers for two weeks:

1. Use your new manager for all daily logins
2. Keep 1Password installed but do not save new entries to it
3. If you discover a missing entry, copy it from 1Password to your new manager
4. Note any workflows that were easier in 1Password and find equivalents in your new tool

### Deactivate 1Password

Once you are confident the migration is complete:

1. Remove the 1Password browser extension
2. Delete the 1Password app from your devices
3. **Cancel your subscription**: Log into your 1Password account at my.1password.com, go to billing, and cancel
4. **Optional**: Delete your 1Password account entirely. Consider keeping it for 30 days after cancellation in case you discover a missing entry

### Delete Export Files

Remove all CSV and 1PUX files from your computer and empty the trash. These contain unencrypted copies of your vault.

## Why PanicVault for 1Password Users

If you valued 1Password's Mac-native experience, PanicVault preserves what you liked while addressing the concerns that prompted your switch:

- **Native Apple experience**: Like 1Password, PanicVault is built specifically for [macOS, iOS, and iPadOS](/apple/iphone-ipad-mac/). It follows Apple's design patterns and integrates with [Face ID, Touch ID](/apple/face-id-touch-id-setup/), and system [AutoFill](/apple/credential-provider-extensions/)
- **No subscription**: One-time purchase. Your cost does not grow over time
- **Open format**: The [KDBX format](/keepass/) means you can always leave -- open your vault in KeePassXC, Strongbox, or any of dozens of [compatible apps](/keepass/compatible-apps/)
- **No cloud service risk**: Your vault is a file on your device, synced by [iCloud or Google Drive](/cloud-sync/). No PanicVault server can be breached because there is no PanicVault server
- **TOTP built in**: PanicVault handles [two-factor authentication](/two-factor-authentication/) codes natively, just like 1Password

## Related Articles

- [How to Switch From LastPass: Migration Guide](/guides/switch-from-lastpass/)
- [How to Set Up a Password Manager for the First Time](/guides/first-time-setup/)
- [How to Audit Your Existing Passwords](/guides/audit-passwords/)
- [Migrate from 1Password to KeePass](/keepass/migrate-from-1password/)
- [KeePass Data Portability](/keepass/data-portability/)
