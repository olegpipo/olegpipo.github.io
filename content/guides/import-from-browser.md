---
title: "How to Import Passwords from Chrome, Safari, or Firefox"
description: "Step-by-step guide to exporting passwords from your browser and importing them into your password manager. Covers Chrome, Safari, and Firefox."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

Your browser has been quietly saving passwords for you, and that collection is the fastest path to a fully populated password vault. Rather than manually re-entering every credential, you can export them from Chrome, Safari, or Firefox and import them into your password manager in minutes. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, walks you through the entire process for each browser.

## Before You Start

### What You Will Need

- Your browser (Chrome, Safari, or Firefox) with saved passwords
- Your password manager installed and set up (see our [first-time setup guide](/guides/first-time-setup/) if you have not done this yet)
- About 15-30 minutes, depending on how many passwords you have saved

### Important Security Notes

The export process creates an unencrypted CSV file containing all your usernames and passwords in plain text. This file is a significant security risk if it falls into the wrong hands. Plan to:

1. Export to a location you control (your desktop or a temporary folder)
2. Import into your password manager immediately
3. Permanently delete the CSV file as soon as the import is complete
4. Empty your trash/recycle bin after deletion

Do not email the CSV file, upload it to cloud storage, or leave it sitting on your desktop.

## Exporting from Google Chrome

### On Mac

1. Open Chrome and click the three-dot menu in the top-right corner
2. Go to **Settings** (or type `chrome://settings` in the address bar)
3. Click **Autofill and passwords** in the left sidebar
4. Click **Google Password Manager**
5. Click **Settings** (gear icon)
6. Find the **Export passwords** option and click it
7. Chrome will warn you that passwords will be visible to anyone who can see the file. Click **Export passwords**
8. You will be prompted to authenticate with your Mac login password or Touch ID
9. Choose a save location and save the file (it will be a CSV)

### On iPhone/iPad

1. Open the Chrome app
2. Tap the three-dot menu, then **Settings**
3. Tap **Password Manager**
4. Tap **Settings** (gear icon)
5. Tap **Export Passwords**
6. Authenticate with Face ID or your device passcode
7. Choose how to share the file -- save it to Files, then import from there

### What Chrome Exports

Chrome exports: website URL, username, password, and any notes. It does not export saved payment methods or addresses -- those must be transferred manually.

## Exporting from Safari

Safari's password export is done through macOS System Settings, not through Safari itself.

### On Mac (macOS Ventura and Later)

1. Open **System Settings**
2. Click **Passwords** in the sidebar
3. Authenticate with Touch ID or your Mac login password
4. Click the three-dot menu (or the "..." button) at the bottom of the password list
5. Select **Export All Passwords**
6. Safari will warn you that passwords will be saved in an unencrypted file. Click **Export Passwords**
7. Choose a save location and click **Save**

### On iPhone/iPad

As of iOS 18, you can export passwords through the Passwords app:

1. Open the **Passwords** app
2. Tap the menu or settings option
3. Look for **Export Passwords** (the exact location may vary by iOS version)
4. Authenticate with Face ID or passcode
5. Save or share the exported CSV file

If the export option is not available on your iOS version, export from a Mac instead. Your iCloud Keychain syncs passwords across devices, so exporting from your Mac captures everything.

### What Safari Exports

Safari exports: website URL, username, and password. Notes and [two-factor authentication](/two-factor-authentication/) codes stored in iCloud Keychain are not included in the CSV export.

## Exporting from Firefox

### On Mac

1. Open Firefox
2. Click the hamburger menu (three horizontal lines) in the top-right corner
3. Click **Passwords** (or navigate to `about:logins`)
4. Click the three-dot menu in the top-right of the passwords page
5. Select **Export Logins**
6. Firefox will warn you about the unencrypted file. Click **Export**
7. Authenticate with your Mac login password
8. Choose a save location and save the CSV file

### On iPhone/iPad

Firefox on iOS does not have a direct CSV export option. You have two alternatives:

1. **Sync to desktop Firefox first**: Enable Firefox Sync on both devices, wait for passwords to sync, then export from the desktop version
2. **Export from Firefox's web interface**: Log into Firefox accounts at firefox.com and access your synced passwords there

### What Firefox Exports

Firefox exports: website URL, username, and password. Firefox does not export saved credit cards through the password export -- those must be transferred manually.

## Importing into Your Password Manager

### Importing into PanicVault

1. Open PanicVault on your Mac (CSV import is easiest from the desktop)
2. Go to **File > Import** or look for the Import option in settings
3. Select the source format -- choose **CSV (Generic)** or the specific browser option if available
4. Navigate to your exported CSV file and select it
5. PanicVault will preview the entries to be imported. Review them for accuracy
6. Confirm the import
7. Your credentials are now in your vault, encrypted with [KeePass-level encryption](/keepass/encryption-explained/)

### Importing into KeePassXC

1. Open KeePassXC and unlock your database
2. Go to **Database > Import > CSV File**
3. Select your exported CSV file
4. KeePassXC will show a field mapping dialog -- map the CSV columns to KeePassXC fields:
   - Column 1 (URL) → URL
   - Column 2 (Username) → Username
   - Column 3 (Password) → Password
   - Column 4 (Name/Title) → Title
5. Click **OK** to complete the import

### Importing into Bitwarden

1. Log into Bitwarden (web vault at vault.bitwarden.com or the desktop app)
2. Go to **Tools > Import Data**
3. Select the format that matches your export source (Chrome CSV, Firefox CSV, etc.)
4. Upload your CSV file or paste its contents
5. Click **Import Data**

### Importing into 1Password

1. Open 1Password and sign in
2. Go to **File > Import** (Mac app) or use the web vault import tool
3. Select the source (Chrome, Firefox, Safari, or generic CSV)
4. Follow the on-screen prompts to map fields and complete the import

## After the Import

### Delete the CSV File Immediately

This step is critical. Your exported CSV contains every password in plain text. Delete it and empty your trash:

**On Mac:**
1. Move the CSV file to Trash
2. Right-click the Trash icon in the Dock and select "Empty Trash"

**On iPhone/iPad:**
1. Open the Files app
2. Find and delete the CSV file
3. Go to "Recently Deleted" and permanently remove it

### Verify Your Import

Open your password manager and spot-check several entries:

- Do the URLs look correct?
- Are usernames and passwords in the right fields?
- Are there any duplicate entries?
- Did any entries import with garbled characters?

Log into 2-3 of your most important accounts using the imported credentials to confirm they work.

### Clean Up Duplicates

Most imports create some duplicates, especially if you had the same credentials saved in multiple browsers or if your password manager already had some entries. Go through your vault and merge or delete duplicates. See our [vault organization guide](/guides/organize-vault/) for strategies.

### Disable Browser Password Saving

Now that your passwords are in a proper manager, stop your browser from saving new ones. This prevents your credentials from accumulating in two places.

**Chrome:** Settings > Autofill and passwords > Google Password Manager > Settings > Toggle off "Offer to save passwords"

**Safari:** System Settings > Passwords > Password Options > Toggle off AutoFill

**Firefox:** Settings > Privacy & Security > Logins and Passwords > Uncheck "Ask to save logins and passwords"

### Optionally: Delete Saved Browser Passwords

Once you have confirmed your import is complete and working, you can delete the passwords stored in your browser. This reduces the number of places your credentials exist.

Be cautious here. Make sure your password manager has every credential before deleting the browser copies. A good approach is to wait a week or two, using your password manager exclusively, before cleaning out the browser.

## Troubleshooting Common Issues

### "Some Passwords Did Not Import"

This usually happens with entries that have unusual formatting, special characters in the password, or incomplete data (e.g., a saved password with no associated URL). Check the CSV file to identify missing entries and add them to your password manager manually.

### "Passwords Are in the Wrong Fields"

If usernames and passwords ended up swapped, or URLs imported as titles, the field mapping during import was incorrect. Delete the imported batch and try again, paying close attention to the column mapping step.

### "I Have Hundreds of Duplicates"

This is common when importing from multiple sources or when your browser had duplicate entries. Most password managers have a "find duplicates" or merge feature. In KeePassXC, you can sort by title and manually merge. In PanicVault, look for duplicate detection in the tools menu.

### "Safari Won't Let Me Export"

On older versions of macOS, the export option may be in a different location or may require you to first enable it through Safari preferences. Make sure you are running a recent version of macOS. If you are on an older system, consider updating before attempting the export.

### "My Exported File Is Empty"

This can happen if your browser passwords are stored in a cloud account that is not currently signed in. Make sure you are logged into your Google account (Chrome), Apple ID (Safari), or Firefox account before exporting.

## Passwords You Should Add Manually

Some important credentials may not be saved in your browser:

- **Email accounts** -- especially if you use a dedicated email app
- **Banking and financial accounts** -- many people avoid saving these in browsers
- **Work/corporate accounts** -- often managed separately
- **Wi-Fi passwords** -- not stored in browsers
- **App-specific passwords** -- credentials for native apps that do not have web logins
- **Two-factor authentication recovery codes** -- store these as secure notes

Take a few minutes to think through which accounts are missing and add them manually. For guidance on storing non-password items, see our guide on [storing secure notes, credit cards, and IDs](/guides/store-notes-cards/).

## Related Articles

- [How to Set Up a Password Manager for the First Time](/guides/first-time-setup/)
- [How to Organize Your Password Vault](/guides/organize-vault/)
- [How to Audit Your Existing Passwords](/guides/audit-passwords/)
- [How to Switch From LastPass: Migration Guide](/guides/switch-from-lastpass/)
- [How to Import Browser Passwords Into KeePass](/keepass/import-browser-passwords/)
