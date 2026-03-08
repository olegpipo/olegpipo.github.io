---
title: "Migrate from RoboForm to KeePass"
description: "Complete guide to migrating from RoboForm to KeePass. Export logins as CSV, handle form-filling data, import into KeePassXC, and verify the migration."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "Can I export RoboForm passwords to KeePass?"
    a: "Yes. RoboForm lets you export your logins as a CSV file through Options > Account & Data > Export. The CSV can be imported into any KeePass-compatible application like KeePassXC or PanicVault."
  - q: "Does RoboForm export form-filling data?"
    a: "RoboForm's CSV export focuses on login credentials. Form-filling data like saved addresses, identities, and contact information may not export cleanly and often requires manual re-entry in your KeePass database."
  - q: "What happens to RoboForm bookmarks during migration?"
    a: "RoboForm bookmarks (Passcard-style entries) may export as login entries in the CSV. Review them after import to ensure they are categorized correctly in your KeePass database."
  - q: "Can I export RoboForm Safenotes to KeePass?"
    a: "RoboForm Safenotes may be included in the CSV export depending on your version. Check your export settings and verify that secure notes transferred correctly after importing into KeePass."
  - q: "How do I handle RoboForm's form-filling features in KeePass?"
    a: "KeePass does not have built-in form-filling for addresses and personal details. You can store this information in KeePass entries using custom fields or the notes section, but automated form-filling for non-login data is not a standard KeePass feature."
---

RoboForm has been in the password management space longer than most competitors, and many users have accumulated years of saved logins, form data, and bookmarks within it. Migrating to a [KeePass-compatible application](/keepass/) moves your credentials from a proprietary platform to an open, local-first format that you fully control. This guide covers the export process from RoboForm, the import into KeePass, and the special considerations for RoboForm's unique data types like form-filling profiles and Passcards.

## Why Migrate from RoboForm to KeePass

### Aging Architecture

RoboForm has a long history, which is both a strength and a weakness. The application carries legacy design decisions from an era when password management looked very different. While RoboForm has modernized over the years, its interface and data model can feel dated compared to newer solutions. KeePassXC and other modern KeePass-compatible applications offer cleaner interfaces, better keyboard shortcuts, and more intuitive workflows.

### Subscription Costs

RoboForm transitioned from a one-time purchase to a subscription model. The free tier has limitations, and the premium features require ongoing annual payments. KeePass-compatible applications are completely free with no subscription tiers or feature restrictions.

### Proprietary Format Lock-In

RoboForm stores your data in its own proprietary format. While the CSV export works for basic migration, RoboForm's rich form-filling data does not convert cleanly to other formats. The longer you use RoboForm, the more data accumulates in a format only RoboForm can fully access. The [KDBX format](/keepass/kdbx-format-guide/) used by KeePass is an open standard supported by dozens of applications, ensuring you are never locked into a single vendor.

### Data Sovereignty

RoboForm can sync your data through its cloud service. With KeePass, your vault file is stored locally on your devices. You choose whether and how to sync it, with no mandatory cloud dependency. For a deeper look at the advantages of open formats, see our [data portability guide](/keepass/data-portability/).

## Before You Start: Back Up Everything

RoboForm contains more than just login passwords, so prepare carefully.

1. **Audit your data types.** RoboForm stores several categories of data: Logins (Passcards), Bookmarks, Identities (form-filling profiles), Safenotes, and Contacts. Note what you have in each category.
2. **Count your entries.** Record the total number of items in each category for verification later.
3. **Identify form-filling data.** If you rely heavily on RoboForm's form-filling capabilities (addresses, credit cards, identity profiles), understand that this data will require special handling. KeePass does not have equivalent auto-fill for forms beyond login credentials.
4. **Keep RoboForm installed.** Do not uninstall or delete your RoboForm data until the migration is fully verified. Plan for a two-to-four-week overlap.

## Step 1: Export Your Data from RoboForm

RoboForm provides a CSV export that captures your login credentials and some additional data.

### Export Steps

1. Open RoboForm on your desktop (the full desktop application, not just the browser extension).
2. Navigate to **RoboForm** then **Options** (or **Settings** depending on your version).
3. Go to **Account & Data**.
4. Find the **Export** option.
5. Select **CSV** as the export format.
6. Choose which data types to export. At minimum, export **Logins**. You may also have options for Bookmarks, Safenotes, and Identities.
7. Enter your master password to authenticate.
8. Save the CSV file to a secure location on your local drive.

### What the RoboForm CSV Export Includes

For login entries, the CSV typically contains:

- **Name** -- The entry title or Passcard name
- **Url** -- The website URL
- **Username** -- The login username
- **Password** -- The password in plain text
- **Note** -- Any notes attached to the entry
- **Folder** -- The folder or category where the entry was stored
- **MatchUrl** -- Additional URL matching data used by RoboForm's autofill
- **RfFieldsV2** -- Encoded field data from RoboForm's advanced form matching

### Understanding RoboForm's Unique Data Types

RoboForm's data model differs from most password managers in several ways:

**Passcards**: These are RoboForm's login entries. Each Passcard stores the URL, login fields, and additional form data captured when you first saved the credential. The CSV export captures the core credentials (URL, username, password) but may not fully represent the extended form data.

**Identities**: RoboForm stores detailed personal profiles used for form-filling -- name, address, phone numbers, email, credit card information, and more. This structured identity data does not have a direct equivalent in KeePass. You will need to decide how to handle it after import.

**Safenotes**: These are secure text notes, similar to secure notes in other password managers. They should export as part of the CSV.

**Bookmarks**: RoboForm stores website bookmarks alongside passwords. These may appear in your export as entries without credentials.

### What Does Not Export Cleanly

- **Form-filling data**: RoboForm's advanced form-filling profiles (addresses, personal details, credit cards stored in identity templates) do not map to KeePass fields. The encoded `RfFieldsV2` data in the CSV is RoboForm-specific and not readable by other applications.
- **File attachments**: Not included in the CSV export.
- **Password history**: Only current passwords are exported.
- **Sharing configurations**: If you shared entries with other RoboForm users, the sharing relationships do not transfer.
- **Application passwords**: If you used RoboForm to store passwords for desktop applications (not websites), these may export with non-standard URL fields.

### Security Precautions

The exported CSV contains all your passwords in plain text:

- Save it only to local, non-synced storage.
- Do not transmit it via email or messaging.
- Delete it securely after the import is verified.
- Lock your screen if you step away during the process.

## Step 2: Import into KeePass

With the RoboForm CSV exported, import it into your KeePass-compatible application.

### Importing into KeePassXC

1. Open KeePassXC and create a new database or open an existing one. For new databases, choose a strong master passphrase and use the default encryption settings (AES-256 with Argon2id).
2. Go to **Database** then **Import** then **CSV File**.
3. Select your RoboForm CSV file.
4. Map the columns to KeePass fields:
   - "Name" to **Title**
   - "Url" to **URL**
   - "Username" to **User Name**
   - "Password" to **Password**
   - "Note" to **Notes**
   - "Folder" to **Group**
5. You can ignore the "MatchUrl" and "RfFieldsV2" columns, or map them to custom fields if you want to preserve the data for reference.
6. Check the option to treat the first row as field names.
7. Review the preview.
8. Click **OK** to import.

### Importing into KeePass 2.x

1. Open KeePass 2.x and go to **File** then **Import**.
2. Select **Generic CSV Importer** (or look for a dedicated RoboForm CSV option if available).
3. Browse to the CSV file and configure column mapping.
4. Complete the import.

### Handling Form-Filling Data

After importing login credentials, address the form-filling data that did not transfer automatically:

**Identity profiles**: Create a group in KeePass called "Identities" and create an entry for each identity profile. Use the notes field or custom string fields to store name, address, phone number, email, and other personal details.

**Credit cards**: Create entries in a "Payment Cards" group with card details stored in custom fields. KeePassXC supports hidden custom fields, which are appropriate for card numbers and CVVs.

**Addresses**: Store these in the notes field of an entry or in dedicated custom fields. While KeePass will not auto-fill address forms like RoboForm did, having the data accessible in your vault means you can copy and paste individual fields.

### Importing on Apple Devices

Apple users can create the KDBX database using KeePassXC on macOS, then open it in [PanicVault](https://panicvault.com) on all their Apple devices. PanicVault provides native system autofill on macOS and iOS, offering a modern interface for your imported RoboForm credentials. Store the KDBX file in iCloud Drive for seamless sync. See our [compatible apps guide](/keepass/compatible-apps/) for all platform options.

## Step 3: Verify Your Data

RoboForm's unique data types make verification particularly important.

### Compare Entry Counts

Count the login entries in your new KeePass database and compare against the number of Passcards in RoboForm. If you also exported Safenotes and Bookmarks, verify those separately.

### Test Critical Accounts

Log in to your most important accounts using credentials from KeePass:

- Primary email accounts
- Banking and financial services
- Cloud storage providers
- Work accounts and VPNs
- Social media profiles

Pay attention to accounts where RoboForm stored additional form fields beyond username and password. Some sites use multi-step login forms or additional fields that RoboForm captured but that the CSV export may have simplified.

### Check for Mangled Entries

RoboForm's extended form data can sometimes confuse CSV parsing. Look for entries where:

- The password field contains unexpected data
- URLs are malformed or truncated
- Entry titles contain CSV artifacts (extra commas or quotation marks)
- Notes contain encoded data that should have been in other fields

### Verify Safenotes

If you exported Safenotes, check that the text content is complete and properly formatted in your KeePass database.

### Check Folder Structure

Verify that RoboForm's folder hierarchy translated correctly into KeePass groups. RoboForm supports nested folders, which should map to nested KeePass groups.

## Step 4: Clean Up

With verification complete, finalize the migration.

### Delete the CSV File

Securely delete the plain text CSV export.

### Manually Transfer Remaining Data

For data that did not export cleanly -- identities, credit cards, specific form-filling profiles -- manually create entries in your KeePass database. This is the most time-consuming part of the RoboForm migration because of the form-filling data that has no direct KeePass equivalent.

Prioritize the data you use most frequently. You can transfer the rest over the following weeks as you encounter the need.

### Back Up Your KeePass Database

Create a backup of your KDBX file and store it separately. See our [backup guide](/keepass/backup-database/) for comprehensive strategies.

### Manage Your RoboForm Account

Keep RoboForm for two to four weeks as a reference, particularly for form-filling data you are gradually migrating. Once satisfied:

- Delete your data from RoboForm
- Cancel your subscription
- Uninstall the application and browser extension

### Set Up Your New Workflow

Install the KeePassXC Browser extension for autofill. Configure mobile autofill through your chosen KeePass app. Accept that KeePass will handle login autofill excellently but will not replicate RoboForm's address and identity form-filling. For non-login forms, you will copy and paste from your vault entries.

## What Transfers and What Does Not

| Data Type | Transfers via CSV | Notes |
|-----------|:-:|-------|
| Login credentials | Yes | URL, username, password, title |
| Folders | Yes | Maps to KeePass groups |
| Notes / Safenotes | Yes | Text content transfers |
| Form-filling data | No | RoboForm-specific encoded fields |
| Identity profiles | No | Must manually recreate as KeePass entries |
| Credit card data | No | Must manually recreate in KeePass |
| Bookmarks | Partial | May export as credential-less entries |
| Application passwords | Partial | May have non-standard URL fields |
| File attachments | No | Not included in CSV |
| Password history | No | Only current passwords export |
| Sharing configurations | No | RoboForm-specific feature |

## Related Articles

- [What Is the KDBX Format and Why It Matters](/keepass/kdbx-format-guide/)
- [KeePass-Compatible Apps for Every Platform](/keepass/compatible-apps/)
- [How to Import Browser Passwords into KeePass](/keepass/import-browser-passwords/)
- [KeePass Data Portability: Own Your Passwords Forever](/keepass/data-portability/)
- [Migrate from LastPass to KeePass](/keepass/migrate-from-lastpass/)
