---
title: "How to Switch From LastPass: Migration Guide"
description: "Complete step-by-step guide to migrating from LastPass to PanicVault, KeePassXC, Bitwarden, or 1Password. Export, import, and verify your credentials."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

LastPass's security incidents have prompted millions of users to reconsider where they store their most sensitive data. If you have decided to move on, the good news is that migration is straightforward -- you can export your entire LastPass vault and import it into another manager in about 30 minutes. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, walks you through the complete process for PanicVault, KeePassXC, Bitwarden, and 1Password.

## Before You Begin

### What You Will Need

- Access to your LastPass account (web vault at lastpass.com)
- A computer (not a phone -- the export works best from a desktop browser)
- Your new password manager installed and configured (see our [first-time setup guide](/guides/first-time-setup/))
- 30-60 minutes of uninterrupted time

### What Gets Exported

LastPass exports include:

- Website URLs, usernames, and passwords
- Secure notes
- Folder structure
- Custom fields (credit cards, addresses, etc. -- exported differently depending on the method)

### What Might Not Transfer Cleanly

- **Shared folders**: Items shared with you by other LastPass users will not export. You need the original sharer to provide those credentials separately
- **Attached files**: File attachments in LastPass are not included in the standard export
- **Password history**: Only the current password for each entry exports
- **TOTP secrets**: Two-factor authentication secrets stored in LastPass Authenticator may not export via the standard CSV. Back these up separately
- **Form fill data**: Addresses and identity information may need to be re-entered manually

## Step 1: Export From LastPass

### Method A: CSV Export (Recommended)

1. Open your web browser and go to **lastpass.com**
2. Log in with your LastPass master password and complete any 2FA challenges
3. Click **Advanced Options** in the left sidebar (or navigate to Account Settings)
4. Click **Export** under "Manage Your Vault"
5. Enter your master password again when prompted
6. LastPass will generate a CSV file. Save it to your desktop or a temporary folder

**Security warning**: This CSV file contains every password in your vault in plain text. Do not email it, upload it to cloud storage, or leave it on your computer after the import is complete.

### Method B: Encrypted Export (If Available)

Some LastPass plans offer encrypted export options. If available:

1. Follow the same steps as above
2. Choose the encrypted format when given the option
3. You will need the encryption password during import

### Troubleshooting Export Issues

**"Export is not available"**: Some LastPass plans restrict exports. Try the browser extension instead: click the LastPass icon > Account Options > Export.

**"Export is grayed out"**: Your employer's LastPass policy may prevent exports. Contact your IT department or administrator.

**"The exported file is empty or incomplete"**: Try a different browser. Chrome tends to work most reliably with LastPass exports. Also verify that your account is not in a locked state.

**"I can't log in to LastPass"**: If you have forgotten your LastPass master password, use their recovery options first. You need account access to export.

## Step 2: Import Into Your New Password Manager

### Importing Into PanicVault

PanicVault reads the [KDBX format](/keepass/) natively and can import from CSV:

1. Open PanicVault on your Mac
2. Open your vault (or create a new one if you have not already)
3. Go to **File > Import** or find the Import option
4. Select **LastPass CSV** as the import format (or Generic CSV if LastPass is not listed)
5. Navigate to the exported CSV file
6. Preview the entries -- check that URLs, usernames, and passwords are mapped to the correct fields
7. Confirm the import
8. Your LastPass entries are now in your vault, protected by [KeePass-level encryption](/keepass/encryption-explained/)

**Folder mapping**: If your LastPass vault used folders, PanicVault should recreate them as groups. Verify the folder structure matches your expectations.

### Importing Into KeePassXC

1. Open KeePassXC and unlock your database
2. Go to **Database > Import > CSV File**
3. Select the LastPass CSV
4. Map the columns:
   - `url` → URL
   - `username` → Username
   - `password` → Password
   - `name` → Title
   - `grouping` → Group (this preserves your LastPass folder structure)
   - `extra` → Notes
5. Click **OK**
6. Review the imported entries

For more detailed KeePass migration steps, see our [LastPass to KeePass migration guide](/keepass/migrate-from-lastpass/).

### Importing Into Bitwarden

1. Log into the Bitwarden web vault at vault.bitwarden.com
2. Go to **Tools > Import Data**
3. Select **LastPass (csv)** from the format dropdown
4. Click **Choose File** and select your exported CSV
5. Click **Import Data**
6. Bitwarden will show a success message with the number of imported items
7. Review the import in your vault

### Importing Into 1Password

1. Open 1Password on your Mac (or use the web vault)
2. Go to **File > Import**
3. Select **LastPass** as the source
4. Upload the CSV file
5. 1Password will map fields and show a preview
6. Confirm the import
7. Review the imported entries for accuracy

## Step 3: Verify the Import

Do not assume everything transferred correctly. Spend 15 minutes verifying:

### Spot Check Critical Accounts

Log into these accounts using credentials from your new password manager (not from memory or your browser):

1. **Primary email** -- If this does not work, you cannot reset other passwords
2. **Banking** -- High-value target, must be correct
3. **Apple ID / Google Account** -- Controls device and cloud access
4. **2-3 accounts you use daily** -- Amazon, social media, streaming services

### Check for Missing Entries

Compare the entry count:
- In LastPass: Check the total number of items before deleting your account
- In your new manager: Count the imported entries
- If there is a discrepancy, check for entries that failed to import (often due to special characters or unusual formatting)

### Verify Secure Notes

If you stored secure notes in LastPass (Wi-Fi passwords, software licenses, etc.), verify they transferred to your new manager's notes or secure notes section. CSV exports sometimes mangle formatting in notes fields.

### Check Credit Card and Identity Data

Credit cards and addresses stored in LastPass may not import cleanly via CSV. You may need to re-enter them manually. See our guide on [storing secure notes, credit cards, and IDs](/guides/store-notes-cards/).

## Step 4: Handle Two-Factor Authentication

If you stored TOTP secrets in LastPass Authenticator:

1. **Before deleting LastPass**: Go through every account with 2FA and note which ones use LastPass Authenticator
2. **Re-enroll 2FA**: For each account, disable 2FA, then re-enable it using your new password manager's TOTP feature (PanicVault supports this) or a dedicated authenticator app
3. **Save backup codes**: When re-enrolling, save the recovery codes in your new password manager's notes

See our [2FA setup guide](/guides/setup-2fa/) for detailed instructions on setting up TOTP in your new manager.

## Step 5: Set Up Your New Manager

If you have not already:

1. [Configure AutoFill](/guides/autofill-setup/) on all your devices
2. Enable [Face ID / Touch ID](/apple/face-id-touch-id-setup/)
3. [Organize your vault](/guides/organize-vault/) -- this is a good time to clean up the folder structure
4. Set up [iCloud or Google Drive sync](/cloud-sync/) (for PanicVault) or cloud sync (for Bitwarden/1Password)

## Step 6: Clean Up

### Delete the CSV Export File

This is critical. The unencrypted CSV contains all your passwords in plain text:

1. Delete the file from your computer
2. Empty the Trash / Recycle Bin
3. If you saved it to a cloud-synced folder, verify it is deleted from the cloud as well

### Transition Period

Use your new password manager exclusively for 1-2 weeks. During this time:

- Keep LastPass installed but stop saving new entries to it
- If AutoFill offers both LastPass and your new manager, always choose the new one
- Note any entries that are missing from your new manager and add them

### Deactivate LastPass

Once you are confident that all your credentials are in your new manager:

1. Remove the LastPass browser extension from all browsers
2. Delete the LastPass app from your phone and tablet
3. **Optional but recommended**: Delete your LastPass account entirely
   - Log into lastpass.com
   - Go to Account Settings > My Account > Delete Account
   - Follow the prompts
   - This permanently removes your data from LastPass's servers

### Update Your Master Password Strategy

Your new password manager deserves a strong, unique [master password](/guides/master-password/). Do not reuse your LastPass master password -- create a fresh one. This ensures that even if your LastPass master password was somehow compromised during the security incidents, your new vault remains protected.

## Common Migration Pitfalls

**Rushing through verification.** Taking 15 minutes to spot-check critical accounts can save hours of frustration later. Do not skip this step.

**Forgetting about 2FA.** If you delete LastPass without re-enrolling your 2FA codes in a new authenticator, you can get locked out of accounts. Handle 2FA before deactivating LastPass.

**Not deleting the CSV file.** That file is an unencrypted copy of your entire digital life. Delete it immediately after import.

**Keeping LastPass "just in case" indefinitely.** Set a deadline. Two weeks of parallel use is enough. After that, commit to your new manager and remove LastPass.

**Not telling family members.** If you shared folders or entries with family members on LastPass, they need to migrate too or you need to re-share credentials through your new manager's [sharing features](/guides/share-with-family/).

## Why PanicVault for LastPass Refugees

If you are leaving LastPass partly because of trust concerns about cloud-hosted password managers, PanicVault offers a fundamentally different architecture:

- **No cloud service to breach**: Your vault is a local file on your device, synced via [iCloud Drive](/cloud-sync/) -- a service you already trust with your photos, documents, and device backups
- **Open format**: The [KDBX format](/keepass/) is open and auditable. Your data is not locked into any vendor's proprietary system
- **No account required**: There is no PanicVault account that could be breached. There is no server storing your credentials. There is nothing to hack
- **One-time purchase**: No subscription means no ongoing relationship with a company that might change its security posture or pricing
- **Apple-native security**: [Face ID, Touch ID](/apple/face-id-touch-id-setup/), and the [Secure Enclave](/apple/secure-enclave/) provide hardware-backed protection that cloud-based managers cannot replicate

## Related Articles

- [How to Switch From 1Password: Migration Guide](/guides/switch-from-1password/)
- [How to Set Up a Password Manager for the First Time](/guides/first-time-setup/)
- [How to Audit Your Existing Passwords](/guides/audit-passwords/)
- [Migrate from LastPass to KeePass](/keepass/migrate-from-lastpass/)
- [KeePass Data Portability](/keepass/data-portability/)
