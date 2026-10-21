---
title: "How to Migrate from LastPass to KeePass: Step-by-Step Guide"
description: "Export your LastPass vault to CSV, import it into KeePassXC, KeePass 2.x or PanicVault on iPhone and Mac, verify every entry, and decide which passwords to change after the 2022 breach."
date: 2026-02-13
lastmod: 2026-10-21
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "How do I export my passwords from LastPass?"
    a: "In the LastPass web vault, choose Advanced Options in the left sidebar, then Export under Manage your Vault, and confirm the email LastPass sends you. In the browser extension, go to Account > Fix a problem yourself > Export vault items > Export data for use anywhere. Either way you get a plaintext CSV file."
  - q: "Can KeePass import a LastPass CSV file?"
    a: "Yes. KeePass 2.x has a LastPass format under File > Import. KeePassXC imports it through its CSV import wizard, where you match LastPass's columns to KeePass fields. PanicVault on iPhone, iPad and Mac imports it as a generic CSV with File > Import Passwords from CSV."
  - q: "Do my LastPass TOTP codes transfer to KeePass?"
    a: "Usually not. LastPass's help says exporting TOTP codes for password items is unsupported, so the totp column in the CSV is normally empty, and codes in LastPass Authenticator are a separate app. Plan to set up two-factor codes again in your KeePass app, which is a good idea anyway if your vault existed during the 2022 breach."
  - q: "Is KeePass free?"
    a: "KeePass 2.x and KeePassXC are free and open source. Some KeePass-compatible apps for iPhone and Mac are paid: PanicVault is a one-time purchase, and Strongbox and KeePassium have free versions with paid upgrades. All of them use the same .kdbx file, so you are never tied to one."
  - q: "Should I change my passwords after leaving LastPass?"
    a: "If your LastPass vault existed in 2022, yes, starting with the most valuable accounts. Attackers copied encrypted vault backups that year and can keep trying to crack them offline. Moving to KeePass protects you from now on; it does not change a password that was already in the stolen copy."
---

Moving from LastPass to a [KeePass-compatible app](/keepass/) takes an afternoon: you export a CSV file from LastPass, import it into KeePass, check the result and delete the CSV. This guide walks through each step with the current LastPass menus, covers KeePassXC and KeePass 2.x on a computer and [PanicVault](https://apps.apple.com/app/id6759188575) on iPhone, iPad and Mac, and ends with what to change if your vault was caught up in the 2022 LastPass breach.

## Why Move from LastPass to KeePass

**The 2022 breach.** In December 2022 LastPass [disclosed](https://blog.lastpass.com/posts/notice-of-recent-security-incident) that attackers had copied a backup of customer vault data. Passwords and notes in those vaults were encrypted, but website URLs were not, and the attackers can try to crack the encrypted parts offline for as long as they like. By September 2023, researchers had [linked the theft of more than $35 million in cryptocurrency](https://krebsonsecurity.com/2023/09/experts-fear-crooks-are-cracking-keys-stolen-in-lastpass-breach/) to secrets stored in those vaults.

**A shrinking free plan.** In 2021 LastPass [limited its free plan](https://blog.lastpass.com/posts/changes-to-lastpass-free) to one type of device -- computers or mobile devices -- so free users who relied on both had to pay or leave.

**Your own file.** With KeePass, your vault is a single encrypted `.kdbx` file that you keep where you choose: on your computer, in iCloud Drive or Google Drive, or anywhere else. No company holds a copy unless you put one there, and because the format is open, any KeePass-compatible app can open it. KeePass 2.x and KeePassXC are free and open source; on Apple devices you can use a paid app such as PanicVault, or Strongbox or KeePassium, which have free versions with paid upgrades. Our [data portability guide](/keepass/data-portability/) explains why the open format matters.

## Before You Start: Back Up Everything

1. **Note your entry count.** Count the items in your LastPass vault, at least roughly, so you can compare after the import.
2. **Download attachments.** File attachments are not included in the CSV export. Save any you need from LastPass before you close the account.
3. **List your shared folders.** Check that their items appear in your export; even when they do, the sharing itself does not carry over.
4. **Find your two-factor codes.** Make a list of accounts whose codes live in LastPass or LastPass Authenticator, because those codes will not come across (see below).
5. **Keep LastPass active.** Do not delete the account until you have verified the migration, ideally after two to four weeks of using KeePass.

## Step 1: Export Your Data from LastPass

LastPass exports to a CSV file. Both routes below produce the same file.

### From the LastPass Web Vault

1. Log in at lastpass.com and open your vault.
2. Choose **Advanced Options** in the left sidebar.
3. Under **Manage your Vault**, choose **Export**.
4. LastPass emails you to confirm the export. Open the link, return to the web vault and choose **Export** again, entering your master password if asked.
5. Your browser saves a `.csv` file. If the data appears on screen instead, copy all of it into a plain text file and save it with a `.csv` extension.

### From the LastPass Browser Extension

1. Click the LastPass icon in your browser toolbar and open the **Account** tab.
2. Choose **Fix a problem yourself**, then **Export vault items**, then **Export data for use anywhere**.
3. Enter your master password and save the `.csv` file.

LastPass changes these menus from time to time. If you cannot find them, search LastPass's help for "export vault items".

### What Is in the CSV

The file starts with a header row like this:

```
url,username,password,totp,extra,name,grouping,fav
```

| LastPass column | What it holds | KeePass field |
|---|---|---|
| `url` | Website address | URL |
| `username` | Login name | User name |
| `password` | Password | Password |
| `totp` | Two-factor secret; usually empty, because LastPass does not export TOTP codes for password items | Re-add codes by hand |
| `extra` | Notes, and the contents of secure notes | Notes |
| `name` | Entry name | Title |
| `grouping` | Folder | Group |
| `fav` | Favourite flag (1 or 0) | Not needed |

Secure notes and form-fill items are flattened into the `extra` column, so they arrive as notes rather than structured entries.

### Keep the CSV Safe

The CSV holds every password in plain text. Save it to your computer's local drive, not a synced folder such as Dropbox or iCloud Drive; do not email or message it; and delete it as soon as the import is verified.

## Step 2: Import into KeePass

### KeePassXC (Windows, Mac, Linux)

1. Choose **Database > Import...** to start KeePassXC's Import Wizard.
2. Choose **Comma Separated Values (.csv)** and select your LastPass file.
3. Treat the first row as field names, then check the column mapping: `name` to Title, `username` to Username, `password` to Password, `url` to URL, `extra` to Notes and `grouping` to Group.
4. Look over the preview and finish the wizard. If it creates a new database, give it a strong master password, then save it.

### KeePass 2.x (Windows)

1. Create a new database with **File > New**, or open an existing one.
2. Choose **File > Import**.
3. Choose **LastPass** from the list of formats and select your CSV file. KeePass maps the columns for you; the generic CSV importer is only needed if the dedicated option fails.
4. Save the database.

For more on the file your entries now live in, see our [KDBX format guide](/keepass/kdbx-format-guide/).

### Importing on Apple Devices

On iPhone, iPad or Mac you can import the LastPass CSV straight into [PanicVault](https://apps.apple.com/app/id6759188575):

1. Create a vault in PanicVault, or open and unlock the one you want to import into.
2. On a Mac, choose **File > Import Passwords from CSV...** (Cmd+Shift+I). On iPhone or iPad, tap the **...** menu in the entry list toolbar and choose **Import Passwords from CSV**.
3. Pick the LastPass file. LastPass is not one of the formats PanicVault recognises by name, so the import sheet shows **Generic CSV**; PanicVault uses the password column and matches title, username, URL and notes columns by their header names.
4. Choose the group to import into and tap **Import**.

All entries go into the one group you choose, so LastPass folders are not recreated. Check a few entries afterwards: LastPass calls its title column `name` and its notes column `extra`, and if those did not come through, the next route is the simpler fix. The [PanicVault import guide](/help/importing-passwords/) has the details.

If you want your LastPass folders as groups, import the CSV into KeePassXC first (above), save the database as KDBX 4, and open that `.kdbx` file in PanicVault on your Mac, iPhone or iPad. Keep it in iCloud Drive or Google Drive to sync it across your devices. For other options, see our list of [KeePass apps for every platform](/keepass/compatible-apps/).

## Step 3: Verify the Import

- **Compare entry counts** with the number you noted from LastPass. Gaps usually come from secure notes or form fills, or from rows with unusual characters that broke the CSV.
- **Log in to your most important accounts** -- email, banking, your main work account -- using the passwords from the new database.
- **Check that fields did not shift.** A column mapping mistake can put URLs in the username field or titles in the notes. Catching it now saves confusion later.
- **Open a few former secure notes** and make sure their content arrived intact.

## Step 4: Clean Up

### Delete the CSV File

Delete the export as soon as the import checks out, then empty the Trash or Recycle Bin. Do not keep it "just in case": if you need another export, LastPass can produce one while your account is open.

### Back Up the New Database

Copy the `.kdbx` file somewhere separate from the original, such as an external drive or a different cloud service. Losing your only copy would lock you out of everything. Our [KeePass backup guide](/keepass/backup-database/) covers a complete routine.

### Set Up Filling

On a computer, the KeePassXC-Browser extension fills logins in Chrome, Firefox, Edge and other browsers, and KeePass 2.x can type them into any window with Auto-Type. On phones, KeePass-compatible apps fill through the system: KeePassDX on Android, and PanicVault, Strongbox or KeePassium through AutoFill on iPhone. Then turn off the LastPass extension so the two do not compete.

### Close Your LastPass Account

Once you have used KeePass for a few weeks without missing anything, delete the items from your LastPass vault and then the account itself, so your current data no longer sits in your LastPass account. It does not affect the backups stolen in 2022, which is why the next section matters.

## If Your Vault Was in the 2022 Breach

If you had a LastPass account in 2022, assume the attackers have an encrypted copy of your vault as it was then. How long it resists cracking depends on your master password at the time and your account's iteration setting, so the safest course is to change the secrets that were in it, starting with the ones that matter most:

1. **Cryptocurrency.** Any seed phrase or private key that was ever stored in LastPass should be treated as exposed. Move the funds to a new wallet created with a new seed phrase.
2. **Email accounts.** Your email can reset almost every other password, so change these first and check their recovery phone numbers and addresses.
3. **Banking, payment and investment accounts.**
4. **Two-factor secrets and recovery codes.** If you kept TOTP secrets or backup codes in LastPass notes, set up two-factor authentication again on those accounts to get new ones.
5. **Work accounts and anything with admin rights**, plus API keys, SSH keys and other secrets kept in secure notes.
6. **Reused passwords.** Any password you also used elsewhere should be changed everywhere it appears. Our guide to [password reuse](/password-security/password-reuse-dangers/) explains why.
7. **Everything else**, as you next log in to each site.

Remember that the website URLs in the stolen vaults were not encrypted, so attackers may know which sites you use. Be wary of emails that appear to come from those services. For a fuller response plan, see [what happens when a password manager gets hacked](/password-managers/what-if-hacked/).

## Handling Common Migration Issues

### Entries with Special Characters

Passwords or notes containing commas, quotation marks or line breaks can split a CSV row in the wrong place. If an entry is missing or garbled after the import, find its row in the CSV and fix the entry by hand.

### Duplicate Entries

LastPass may hold several entries for the same site, for example after a password change. Search the new database for duplicates and delete the outdated ones.

### Two-Factor (TOTP) Codes

Because LastPass does not export TOTP codes for password items, re-add each code in your new app: open the account's security settings, set up two-factor authentication again, and scan the new QR code. KeePassXC, PanicVault and KeePass 2.x (from version 2.47, with menu commands since 2.51) all generate TOTP codes without a plugin.

### Passwords Saved in Your Browser

Your browser may also have saved passwords while you used LastPass. Consider [importing those into KeePass](/keepass/import-browser-passwords/) too, then turning off the browser's password saving so everything lives in one place.

## What Transfers and What Does Not

| Data | Transfers via CSV | Notes |
|---|:-:|---|
| Logins (URL, username, password, name) | Yes | Map the columns as shown above |
| Notes | Yes | From the `extra` column |
| Folders | Yes, as groups | Via `grouping` in KeePassXC or KeePass 2.x; PanicVault imports into one group |
| Secure notes | Partly | Arrive as plain notes |
| Form fills (addresses, cards) | Partly | Flattened into notes; recreate as entries if needed |
| TOTP codes | No | Set up two-factor again in your new app |
| File attachments | No | Download from LastPass first |
| Sharing | No | Shared items export, but not who they were shared with |

## Related Articles

- [Export Passwords From Any Manager](/keepass/export-passwords-any/)
- [Migrate from Bitwarden to KeePass](/keepass/migrate-from-bitwarden/)
- [Migrate from 1Password to KeePass](/keepass/migrate-from-1password/)
- [KeePass Apps for Every Platform](/keepass/compatible-apps/)
- [How to Back Up Your KeePass Database](/keepass/backup-database/)
- [Handling Password Manager Breaches](/password-managers/handling-breaches/)
