---
title: "How to Migrate from LastPass to KeePass: Step-by-Step Guide"
description: "Complete guide to migrating from LastPass to KeePass. Export your vault, import passwords, organize entries, and verify your data for a clean transition."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

Migrating away from a commercial password manager can feel daunting, but the process of moving from LastPass to a [KeePass-compatible application](/keepass/) is straightforward once you understand the steps involved. Whether you are leaving because of security concerns after the LastPass breach incidents, frustration with pricing changes, or a desire for greater control over your data, this guide walks you through every stage of the migration -- from exporting your LastPass vault to verifying that every credential has been successfully transferred.

## Why Migrate from LastPass to KeePass

Several factors have driven users away from LastPass in recent years, and understanding them helps frame why a migration is worth the effort.

### Security Incidents

The 2022 LastPass breach was one of the most significant password manager compromises in history. Attackers gained access to encrypted vault backups for millions of users. While the encryption on those vaults provides a layer of protection, the reality is that vaults secured with weak or reused master passwords are vulnerable to brute force cracking. Subsequent reports linked cryptocurrency thefts totaling hundreds of millions of dollars to credentials extracted from those stolen vaults.

For users whose vaults were included in the breach, the risk is ongoing. Attackers have the encrypted data indefinitely and can attempt to crack it as computing power improves. If your vault was breached and your master password was not exceptionally strong, migrating to a new password manager is only the first step -- you should also rotate every password stored in the compromised vault. Our guide on [what happens when a password manager gets hacked](/password-managers/what-if-hacked/) covers the full implications and response steps.

### Pricing Changes

LastPass has progressively restricted its free tier over the years. The platform once offered unlimited devices on its free plan, then limited free users to a single device type (mobile or desktop), and has continued to push more features behind its premium paywall. For users who relied on the free tier, these changes forced a choice: pay a recurring subscription or find an alternative.

KeePass-compatible applications are free and open source. There is no subscription, no premium tier, and no risk of features being removed from a plan you depend on. The software is maintained by the open source community and funded by donations rather than user fees.

### Privacy and Data Control

LastPass stores encrypted vault data on its own servers. While the company cannot read your encrypted data (in theory), the 2022 breach demonstrated that server-side storage creates a target. An attacker who compromises the service gains access to millions of vaults at once.

With KeePass, your vault is a local file on your device. You decide where it lives, how it is backed up, and whether it is synced to any cloud service. No third party holds a copy of your encrypted data unless you explicitly place one there. This architectural difference is fundamental to the KeePass security model.

## Step 1: Export Your Data from LastPass

Before you can import anything into KeePass, you need to get your data out of LastPass. LastPass supports exporting to CSV format, which is the most universally compatible option for importing into other password managers.

### Exporting via the LastPass Web Vault

1. Log in to your LastPass account at lastpass.com.
2. Navigate to **Advanced Options** in the left sidebar (or click your account icon and look for **Advanced Options**).
3. Select **Export** under the "Manage Your Vault" section.
4. You will be prompted to enter your master password again for verification.
5. LastPass will generate a CSV file and either download it directly or display the data in your browser window. If the data is displayed in the browser, select all of it, copy it, and paste it into a plain text file saved with a `.csv` extension.

### Exporting via the LastPass Browser Extension

1. Click the LastPass extension icon in your browser toolbar.
2. Go to **Account Options** then **Advanced** then **Export**.
3. Enter your master password when prompted.
4. Save the resulting CSV file to a secure location on your device.

### Important Warnings About the Export

The CSV file produced by LastPass contains all your passwords in plain text. This is inherently risky. While it is necessary for the migration, you must handle this file with extreme care:

- Save it to your local drive only, not to a cloud-synced folder like Dropbox or Google Drive.
- Do not email the file or share it through any messaging service.
- Delete the file securely after you have completed the import and verified your data. On most operating systems, simply deleting the file and emptying the recycle bin is insufficient for true secure deletion, but it is adequate for most threat models. If you need stronger guarantees, use a secure deletion tool.

### What the Export Includes

The LastPass CSV export typically includes the following fields: URL, username, password, extra notes, name (the entry title), grouping (folder path), and a "fav" flag for favorites. It covers standard login entries, secure notes, and form fill data, though the format for notes and form fills may require manual adjustment after import.

## Step 2: Import into KeePass

The import process varies slightly depending on which KeePass-compatible application you are using. The two most common options are KeePass 2.x (the classic Windows application) and KeePassXC (the cross-platform community edition).

### Importing into KeePass 2.x

1. Open KeePass and create a new database (or open your existing one).
2. Go to **File** then **Import**.
3. In the import dialog, select **Generic CSV Importer** from the list of formats. Some versions of KeePass also include a dedicated **LastPass CSV** import option -- use that if available, as it maps fields automatically.
4. Browse to and select your exported CSV file.
5. If using the generic CSV importer, you will need to map the CSV columns to KeePass fields. The mapping is typically: "name" to Title, "url" to URL, "username" to User Name, "password" to Password, "extra" to Notes, and "grouping" to Group.
6. Click **OK** to complete the import.

### Importing into KeePassXC

1. Open KeePassXC and create a new database or open an existing one.
2. Go to **Database** then **Import** then **CSV File**.
3. Select your LastPass CSV export file.
4. KeePassXC will display a preview of the CSV data and allow you to map columns to fields. Verify that the column assignments are correct.
5. Check the option to consider the first row as field names if your CSV includes a header row.
6. Click **OK** to import.

For details on the database format your entries are being stored in, see our [KDBX format guide](/keepass/kdbx-format-guide/).

## Step 3: Organize Your Imported Entries

After the import, your entries will likely be organized into groups (folders) that mirror your LastPass folder structure. Take some time to review and reorganize them.

### Review the Group Structure

LastPass uses a flat or lightly nested folder system. KeePass supports a hierarchical group structure that can be as deep as you need. Consider reorganizing your entries into logical categories:

- **Email** -- All email account credentials
- **Financial** -- Banking, investment, payment services
- **Social Media** -- Social networking accounts
- **Shopping** -- E-commerce sites
- **Work** -- Professional accounts and services
- **Subscriptions** -- Streaming, news, software licenses
- **Secure Notes** -- Non-login sensitive information

You do not need to complete this reorganization immediately. The important thing is that your entries are imported and accessible. You can refine the structure over the following days and weeks.

### Handle Secure Notes and Form Fills

LastPass secure notes and form fill profiles may not import cleanly into KeePass. The CSV export format flattens these into text fields that may need manual editing. Review your imported secure notes to ensure the information is intact. For form fill profiles (addresses, credit cards), you may need to recreate these entries manually in KeePass, as the field structure differs between the two applications.

### Deal with Shared Folders

If you used LastPass shared folders (a premium feature), the entries from those folders will be included in your personal export. However, the sharing relationship itself does not transfer. If you were sharing passwords with family members or team members through LastPass, you will need to establish a new sharing method.

For KeePass-based sharing, the simplest approach is to create a separate database file for shared credentials and distribute that file (along with its passphrase) to the people who need access. Some KeePass-compatible applications also support more sophisticated sharing mechanisms. See our guide on [KeePass-compatible apps](/keepass/compatible-apps/) for options that include built-in sharing features.

## Step 4: Verify the Import

Verification is a critical step that many people skip. A migration is not complete until you have confirmed that every entry transferred correctly.

### Spot-Check Critical Accounts

Log in to your most important accounts -- email, banking, primary social media -- using the credentials from your new KeePass database. This confirms that the passwords imported correctly and that you can access your accounts through the new manager.

### Compare Entry Counts

Check how many entries are in your LastPass vault versus how many were imported into KeePass. If there is a discrepancy, investigate which entries are missing. Common causes of missing entries include:

- Secure notes or form fills that did not export properly
- Entries with unusual characters in the password or notes field that caused CSV parsing errors
- Duplicate entries that were merged during import

### Verify URLs and Usernames

Scan through your imported entries and verify that the URL and username fields populated correctly. Occasionally, CSV column mapping issues can cause fields to shift, putting the URL in the username field or vice versa. Catching this early saves frustration later.

## Step 5: Set Up Browser Integration and Autofill

One of the most noticeable differences between LastPass and KeePass is how autofill works. LastPass installs a browser extension that fills credentials automatically. KeePass-compatible applications offer several autofill approaches.

### KeePassXC Browser Extension

KeePassXC provides a browser extension for Chrome, Firefox, Edge, and other Chromium-based browsers. Once installed and connected to your open database, it detects login forms and offers to fill credentials, similar to LastPass. This is the closest experience to what you are used to.

### KeePass Auto-Type

KeePass 2.x uses an "Auto-Type" feature that simulates keyboard input to fill login forms. You select the entry in KeePass and trigger Auto-Type (usually with a keyboard shortcut like Ctrl+Alt+A), and KeePass types the username, presses Tab, types the password, and presses Enter. This works across all applications, not just browsers, but requires your KeePass database to be open.

### Mobile Autofill

On mobile devices, KeePass-compatible apps like KeePassDX (Android) and Strongbox or KeePassium (iOS) integrate with the operating system's autofill framework. Once configured, they offer to fill credentials in apps and browsers just like LastPass did on mobile. Our guide to [compatible apps](/keepass/compatible-apps/) covers the best options for each platform.

## Step 6: Post-Migration Cleanup

With your data successfully migrated and verified, there are several cleanup tasks to complete.

### Delete the CSV Export File

The plain text CSV file containing all your passwords should be deleted immediately after you have verified the import. Do not keep it "just in case." If you need to re-export later, you can do so from LastPass as long as your account is still active.

### Back Up Your New KeePass Database

Create an immediate backup of your new KeePass database file. Store it in a separate location from the primary copy -- an encrypted USB drive, a different device, or a secure cloud storage location. Losing your only copy of the database would be catastrophic. For a comprehensive approach to vault backup, see our [KeePass database backup guide](/keepass/backup-database/).

### Decide What to Do with Your LastPass Account

You have several options:

- **Keep it temporarily** as a fallback while you verify that everything migrated correctly over the next few weeks. This is the safest approach.
- **Delete all entries** in LastPass but keep the account active, giving you a safety net without leaving your credentials on LastPass servers.
- **Delete the account entirely** once you are confident the migration is complete. This removes your encrypted vault data from LastPass servers.

If the 2022 breach was a factor in your decision to migrate, deleting your LastPass data is advisable. However, remember that the breached vault backups are already in the hands of attackers -- deleting your current account does not affect data that was already exfiltrated.

### Rotate Compromised Passwords

If your LastPass vault was potentially included in the 2022 breach, consider rotating all passwords stored in that vault. This is time-consuming but eliminates the risk of attackers eventually cracking the stolen vault backup. Prioritize high-value accounts first: email, banking, and any accounts that could lead to identity theft or financial loss.

The risk of [password reuse](/password-security/password-reuse-dangers/) is amplified when a vault breach is involved, because every credential in the vault is exposed simultaneously rather than one at a time.

### Update Your Recovery Information

With your new KeePass database as your primary vault, update your recovery plan:

- Write down your master passphrase and store it in a physically secure location.
- Document the location of your database file and backups.
- Ensure a trusted person knows how to access your vault in an emergency.

## Handling Common Migration Issues

### Entries with Special Characters

Some passwords containing unusual characters (curly braces, backslashes, quotation marks) can cause CSV parsing errors. If you notice missing or garbled entries after import, check the original CSV file for rows that might have been split incorrectly by special characters. You may need to manually correct these entries.

### Duplicate Entries

LastPass sometimes stores multiple versions of the same login if you updated a password and the previous version was retained. After import, scan your KeePass database for duplicates and merge or delete as appropriate.

### Multi-Factor Authentication Secrets

If you stored TOTP (time-based one-time password) secrets in LastPass, these may export as part of the secure notes or within the URL field. KeePassXC supports TOTP natively -- you can add the TOTP secret to an entry's properties and generate codes directly from your vault. KeePass 2.x requires a plugin for this functionality.

### Browser Saved Passwords

After migrating from LastPass, check whether your browsers also have saved copies of your passwords. If so, consider [importing those into KeePass](/keepass/import-browser-passwords/) as well, then disabling browser password saving to consolidate everything in one place.

## Why KeePass Is Worth the Transition

The migration from LastPass to KeePass requires an afternoon of focused effort, but the long-term benefits are substantial. You gain complete ownership of your data with no cloud servers holding copies of your vault. You eliminate subscription costs permanently. You gain the portability and transparency of the open KDBX format, which is supported by dozens of applications across every platform.

The KeePass ecosystem may lack the polish of commercial alternatives, but it compensates with flexibility, security, and control that no subscription service can match. Your passwords belong to you, stored in a format you can read and verify, protected by encryption you can audit, and accessible through applications you choose. For a deeper understanding of how data portability protects you from vendor lock-in, see our guide on [KeePass data portability](/keepass/data-portability/).

For broader context on how password manager breaches affect users and how to evaluate your risk, our guide on [handling password manager breaches](/password-managers/handling-breaches/) covers the decision framework for when and how to respond.
