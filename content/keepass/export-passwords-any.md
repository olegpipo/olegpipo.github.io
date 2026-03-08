---
title: "Export Passwords From Any Manager"
description: "Universal guide to exporting passwords from Chrome, Safari, Firefox, 1Password, Bitwarden, LastPass, Dashlane, Keeper, and NordPass into KeePass KDBX format."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "What is the best format for exporting passwords to KeePass?"
    a: "CSV is the most universal format and works with every KeePass-compatible app. If your password manager offers JSON export (like Bitwarden), that often preserves more data. Enpass can export directly to KDBX format, which is ideal."
  - q: "Is it safe to export passwords as CSV?"
    a: "CSV files contain passwords in plain text, so they must be handled carefully. Save the file only to local storage, never to cloud-synced folders, and delete it securely immediately after importing into KeePass."
  - q: "Can I export passwords from my phone?"
    a: "Most password managers require the desktop app or web vault for exports. Chrome mobile passwords can be exported via passwords.google.com. Safari iOS passwords sync to macOS via iCloud Keychain for export there."
  - q: "Do all password managers let you export your data?"
    a: "Yes, all major password managers provide an export function, typically CSV at minimum. Some make it easier than others, but data portability regulations and user expectations ensure export is universally available."
  - q: "What do I lose when exporting passwords as CSV?"
    a: "CSV exports typically lose password history, file attachments, sharing configurations, and some metadata. TOTP secrets, custom fields, and folder structure may or may not be preserved depending on the source application."
---

Whether you are consolidating passwords from multiple sources, switching to a new manager, or simply want an open-format backup of your credentials, knowing how to export your passwords is an essential skill. This guide covers the export process for every major password manager and browser, with the goal of getting your credentials into the open [KDBX format](/keepass/kdbx-format-guide/) used by [KeePass-compatible applications](/keepass/). If you have passwords scattered across multiple tools, this is your comprehensive reference for bringing everything into one secure vault.

## Why Export to KeePass / KDBX

### One Format, Dozens of Apps

The KDBX format is an open standard supported by KeePassXC, KeePass 2.x, PanicVault, Strongbox, KeePassDX, and many more. Exporting your passwords into a KDBX database means you are never locked into a single application. If your preferred app is discontinued, raises its price, or changes in a way you do not like, you simply open the same file in a different app. No re-export, no conversion, no data loss.

### Local Storage, Full Control

A KDBX file lives on your device. You control where it is stored, how it is backed up, and whether it syncs to any cloud service. No third party holds a copy unless you explicitly place one there. This is the most direct form of data sovereignty for your credentials.

### No Recurring Costs

KeePass-compatible applications are free and open source. Once your passwords are in KDBX format, you never need to pay for access to them again. For a detailed comparison of open and proprietary approaches, see our [KeePass vs. proprietary](/keepass/vs-proprietary/) guide.

## Export Comparison Table

This table summarizes the export capabilities of every major password manager and browser. Use it to quickly find the relevant instructions for your source.

| Source | Export Formats | TOTP Included | Folders Preserved | Attachments Included | Best Format for KeePass |
|--------|:-:|:-:|:-:|:-:|:-:|
| Chrome | CSV | No | No | N/A | CSV |
| Safari | CSV | Yes (OTPAuth) | No | N/A | CSV |
| Firefox | CSV | No | No | N/A | CSV |
| 1Password | CSV, 1PUX | No (CSV) | Partial | 1PUX only | CSV |
| Bitwarden | CSV, JSON | Yes (JSON) | Yes (JSON) | No | JSON |
| LastPass | CSV | Partial | Yes | No | CSV |
| Dashlane | CSV, DASH | Partial | Yes | No | CSV |
| Keeper | CSV | No | Yes | No | CSV |
| NordPass | CSV | No | Yes | No | CSV |
| Enpass | CSV, JSON, KDBX | Varies | Yes (KDBX) | Varies | KDBX |
| RoboForm | CSV | No | Yes | No | CSV |
| Proton Pass | CSV, PGP | Yes | Yes | No | CSV |

## Exporting from Browsers

### Google Chrome

1. Navigate to `chrome://password-manager/settings` or open **Settings** then **Autofill and passwords** then **Google Password Manager**.
2. Click **Settings** within the password manager.
3. Select **Export passwords**.
4. Authenticate with your system password or biometrics.
5. Save the CSV file locally.

**Fields exported**: name, URL, username, password. Chrome does not export notes or custom fields. For mobile, sync to desktop or export from passwords.google.com.

### Apple Safari / iCloud Keychain

1. Open **System Settings** on macOS (Ventura or later).
2. Navigate to **Passwords**.
3. Authenticate with your Mac password, Touch ID, or Apple Watch.
4. Click the three-dot menu and select **Export All Passwords**.
5. Save the CSV file.

**Fields exported**: title, URL, username, password, notes, OTPAuth (TOTP secrets). Safari's export is notably comprehensive because it includes TOTP secrets. For iOS passwords, sync to macOS via iCloud Keychain and export from there.

### Mozilla Firefox

1. Navigate to `about:logins` or open the hamburger menu and click **Passwords**.
2. Click the three-dot menu in the top-right corner.
3. Select **Export Logins**.
4. Authenticate and save the CSV.

**Fields exported**: URL, username, password, httpRealm, formActionOrigin, guid, timeCreated, timeLastUsed, timePasswordChanged. Firefox includes useful timestamp metadata.

For detailed browser import instructions, see our [browser passwords import guide](/keepass/import-browser-passwords/).

## Exporting from Password Managers

### 1Password

1. Open the 1Password desktop app or web vault at my.1password.com.
2. Go to **File** then **Export** (desktop) or **Profile** then **Export** (web).
3. Choose **CSV** for universal compatibility or **1PUX** for maximum data preservation.
4. Authenticate and save.

**Best format**: CSV for KeePass migration. 1PUX preserves more data but requires conversion tools. TOTP secrets are not included in CSV exports. See our detailed [1Password to KeePass migration guide](/keepass/migrate-from-1password/) for the complete process.

### Bitwarden

1. Open the Bitwarden web vault or desktop app.
2. Navigate to **Settings** then **Export vault**.
3. Choose **JSON** (recommended) or **CSV**.
4. Authenticate and save.

**Best format**: JSON. KeePassXC has a dedicated Bitwarden JSON import that preserves folders, TOTP secrets, custom fields, and item types. This is one of the highest-fidelity migrations available. See our [Bitwarden to KeePass migration guide](/keepass/migrate-from-bitwarden/) for details.

### LastPass

1. Log in to the LastPass web vault.
2. Navigate to **Advanced Options** then **Export**.
3. Authenticate with your master password.
4. Save the CSV file (or copy the displayed data into a .csv file).

**Fields exported**: URL, username, password, extra notes, name, grouping, favorite flag. The export includes logins, secure notes, and form data. See our complete [LastPass to KeePass migration guide](/keepass/migrate-from-lastpass/).

### Dashlane

1. Open Dashlane and go to **Settings** then **Export data**.
2. Choose **CSV** for KeePass migration or **DASH** for encrypted Dashlane backup.
3. Authenticate and save.

**Fields exported**: name, URL, username, password, note, category, TOTP (partial). The DASH format is encrypted but only readable by Dashlane. See our [Dashlane to KeePass migration guide](/keepass/migrate-from-dashlane/).

### Keeper

1. Open Keeper and go to **Settings** then **Export**.
2. Select **CSV** format.
3. Authenticate and save.

**Fields exported**: folder, title, login URL, username, password, notes, custom fields. Shared folders may require separate export. See our [Keeper to KeePass migration guide](/keepass/migrate-from-keeper/).

### NordPass

1. Open NordPass and go to **Settings** then **Export Items**.
2. Choose **CSV** format.
3. Authenticate and save.

**Fields exported**: name, URL, username, password, note, folder, credit card fields (for card entries). The export is well structured with clear field separation. See our [NordPass to KeePass migration guide](/keepass/migrate-from-nordpass/).

### Enpass

1. Open Enpass and go to **Settings** then **Export**.
2. Choose **KeePass (.kdbx)** for direct migration, or CSV/JSON as alternatives.
3. Set a master password for the KDBX file if using that format.
4. Save the file.

**Best format**: KDBX. Enpass is unique in offering direct KDBX export, making it the easiest migration of any password manager. The exported file can be opened immediately in any KeePass-compatible application. See our [Enpass to KeePass migration guide](/keepass/migrate-from-enpass/).

### RoboForm

1. Open RoboForm desktop and go to **Options** then **Account & Data** then **Export**.
2. Select **CSV** format.
3. Choose which data types to export (Logins, Safenotes, etc.).
4. Authenticate and save.

**Fields exported**: name, URL, username, password, note, folder, plus RoboForm-specific encoded form data. Form-filling profiles (addresses, identities) do not map cleanly to KeePass. See our [RoboForm to KeePass migration guide](/keepass/migrate-from-roboform/).

### Proton Pass

1. Open Proton Pass and go to **Settings** then **Export**.
2. Choose **CSV** or **PGP-encrypted** format.
3. Authenticate and save.

**Fields exported**: name, URL, username, password, note, TOTP, vault. Proton Pass includes TOTP secrets in the CSV export, which is a significant advantage. Email aliases remain functional in Proton but the management feature does not transfer. See our [Proton Pass to KeePass migration guide](/keepass/migrate-from-proton-pass/).

## The Import Process: CSV to KDBX

Regardless of which source you exported from, the import into KeePass follows a similar pattern.

### Importing into KeePassXC

1. Open KeePassXC and create a new database or open an existing one.
2. Go to **Database** then **Import** then **CSV File** (or select a dedicated import format if available, such as Bitwarden JSON).
3. Select your export file.
4. Map the source columns to KeePass fields: Title, URL, User Name, Password, Notes, Group.
5. Check the option to treat the first row as field names.
6. Review the preview and complete the import.
7. Save the database.

### Importing from Multiple Sources

If you are consolidating from several sources (for example, Chrome plus LastPass plus some entries in Safari), import each source into a separate group within the same KeePass database:

1. Create a group for each source: "Chrome Import," "LastPass Import," "Safari Import."
2. Import each CSV into its respective group.
3. After all imports are complete, deduplicate and reorganize. Sort by URL to find entries that appear in multiple import groups. Keep the most complete version and delete duplicates.

### Handling TOTP Secrets

If your source included TOTP secrets (Bitwarden JSON, Proton Pass CSV, Safari CSV):

1. After import, open entries that should have TOTP configured.
2. In KeePassXC, right-click the entry and select **TOTP** then **Set up TOTP**.
3. Enter the TOTP secret or URI.
4. Verify that generated codes work correctly.

### Using PanicVault on Apple Devices

Once your passwords are in a KDBX database, Apple users can open that file in [PanicVault](https://panicvault.com) on macOS, iPhone, and iPad. PanicVault provides native system autofill integration and supports iCloud Drive sync, making it a seamless experience for users in the Apple ecosystem. The database file is the same regardless of which app you use to access it -- that is the power of the open KDBX format. See our [compatible apps guide](/keepass/compatible-apps/) for all platform options.

## Security During Export

Every password export carries inherent risk because your credentials exist in plain text during the process. Follow these precautions for every export, regardless of source.

### Before Exporting

- Work on a device you trust, free of malware.
- Close unnecessary applications, especially screen-sharing software.
- Ensure no one is looking over your shoulder.

### During Export

- Save files only to local storage, never to cloud-synced folders (Dropbox, Google Drive, iCloud Drive, OneDrive).
- Use an encrypted volume if possible (BitLocker, FileVault, or VeraCrypt).
- Do not open the CSV file in Google Sheets or any cloud-based editor.

### After Import

- Delete all CSV and JSON export files securely.
- Empty your trash / recycle bin.
- Back up your new KDBX database to a separate secure location. See our [backup guide](/keepass/backup-database/) for strategies.
- Verify the import by testing logins to critical accounts.

## Post-Migration Checklist

After completing your export and import, work through this checklist:

- [ ] Entry counts match between source and KeePass database
- [ ] Critical accounts (email, banking, cloud storage) log in successfully
- [ ] TOTP codes generate correctly for accounts with two-factor authentication
- [ ] Folder/group structure is logical and organized
- [ ] Notes and custom fields are intact
- [ ] Export files (CSV, JSON) are securely deleted
- [ ] KDBX database is backed up to a separate location
- [ ] Browser extension or autofill is configured for your KeePass app
- [ ] Source application's autofill is disabled or removed
- [ ] Master passphrase is strong and stored securely as a backup

## Related Articles

- [What Is the KDBX Format and Why It Matters](/keepass/kdbx-format-guide/)
- [KeePass-Compatible Apps for Every Platform](/keepass/compatible-apps/)
- [How to Import Browser Passwords into KeePass](/keepass/import-browser-passwords/)
- [KeePass Data Portability: Own Your Passwords Forever](/keepass/data-portability/)
- [How to Back Up Your KeePass Database](/keepass/backup-database/)
