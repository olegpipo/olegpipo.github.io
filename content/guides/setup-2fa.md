---
title: "How to Set Up 2FA Using Your Password Manager"
description: "Step-by-step guide to setting up two-factor authentication with TOTP codes in your password manager. Covers setup, backup, and security tradeoffs."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

Two-factor authentication is the single most effective upgrade you can make to your account security after adopting a password manager. A strong, unique password protects you from brute-force attacks and credential stuffing. Adding 2FA protects you even if your password is somehow compromised -- an attacker also needs the second factor, which changes every 30 seconds and lives on your device. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, shows you how to set up TOTP-based 2FA using your password manager and addresses the important question of whether storing 2FA codes alongside your passwords is a good idea.

## What Is TOTP?

TOTP stands for Time-based One-Time Password. It is the technology behind the six-digit codes that apps like Google Authenticator, Authy, and your password manager generate. Here is how it works:

1. When you enable 2FA on a website, the site gives you a **secret key** (usually displayed as a QR code)
2. Your authenticator app stores this secret key
3. Every 30 seconds, the app combines the secret key with the current time to generate a new six-digit code
4. When you log in, the site performs the same calculation and checks that your code matches

The beauty of TOTP is that it works offline -- no internet connection is needed after the initial setup. The code is generated locally on your device.

For a deeper technical explanation, see our [two-factor authentication overview](/two-factor-authentication/).

## Should You Store 2FA Codes in Your Password Manager?

This is a legitimate debate in the security community. Here are both sides.

### The Case For

- **Convenience**: [AutoFill](/guides/autofill-setup/) can fill both your password and your TOTP code in sequence, making logins fast and friction-free
- **Single backup**: Your vault backup covers both passwords and 2FA codes. No separate authenticator app to back up
- **No device dependency**: If you lose your phone and your authenticator app was only on that phone, you are locked out of every 2FA-protected account. With codes in your password manager, you can access them from any device with your vault
- **Practical security improvement**: For most people, the alternative to storing 2FA codes in their password manager is not using 2FA at all. Slightly imperfect 2FA is vastly better than no 2FA

### The Case Against

- **Single point of failure**: If an attacker gains access to your vault, they have both your passwords and your 2FA codes. The "two factors" become one factor
- **Purist separation**: True two-factor authentication means the factors are independent. Something you know (password) on a different system than something you have (TOTP device)

### The Practical Answer

For most people, storing TOTP codes in your password manager is the right choice. The realistic threat model for individuals is not a targeted attacker breaking into your encrypted vault -- it is automated credential stuffing attacks using passwords from data breaches. 2FA stops those attacks completely, regardless of where the TOTP secret is stored.

If you want maximum security separation, use a dedicated authenticator app for your most critical accounts (email, banking) and your password manager for everything else.

## Which Accounts Should Have 2FA?

### Priority 1: Enable Immediately

These accounts, if compromised, give attackers the ability to compromise everything else:

- **Primary email**: Attackers use email access to reset passwords on every other service
- **Apple ID**: Controls access to all your Apple devices, iCloud data, and purchases
- **Google Account**: If you use Gmail, Google Drive, or Google Photos
- **Password manager account** (for cloud-based managers like Bitwarden or 1Password)
- **Banking and financial accounts**: Direct financial risk

### Priority 2: Enable This Week

- Secondary email accounts
- Social media (Facebook, Instagram, X, LinkedIn)
- Cloud storage (Dropbox, OneDrive)
- Mobile carrier account (prevents SIM swap attacks)
- Amazon and shopping accounts with saved payment methods

### Priority 3: Enable When Convenient

- Streaming services
- Professional tools (Slack, GitHub, etc.)
- Gaming platforms
- Forums and community sites
- Any other service that offers 2FA

### How to Check Which Accounts Support 2FA

The website 2fa.directory maintains a comprehensive list of services and their 2FA support. Search for any service to see whether it supports TOTP, SMS, hardware keys, or other methods.

## Setting Up 2FA in PanicVault

PanicVault supports TOTP natively, meaning you can generate six-digit codes directly within the app.

### Step-by-Step Setup

1. **Log into the account** where you want to enable 2FA (e.g., your Google account)
2. **Navigate to security settings**: Usually under Settings > Security > Two-Factor Authentication or Similar
3. **Select "Authenticator App"** as your 2FA method (not SMS -- SMS is less secure)
4. **The site will display a QR code and/or a text-based secret key**
5. **In PanicVault**:
   a. Open the vault entry for this account
   b. Edit the entry
   c. Add the TOTP secret:
      - If PanicVault supports QR scanning: Use the camera to scan the QR code from your screen
      - If entering manually: Copy the text-based secret key and paste it into the TOTP/OTP field
   d. Save the entry
6. **Verify**: PanicVault will now show a six-digit code that refreshes every 30 seconds. Enter this code on the website to confirm setup
7. **Save recovery codes**: The website will provide one-time backup codes. Store these in the entry's notes field (see below)

### Saving Recovery Codes

When enabling 2FA, most services provide 8-12 one-time-use recovery codes. These are your emergency backup if you lose access to your TOTP generator. Store them in the same vault entry:

```
2FA Recovery Codes (saved 2026-02-14):
1. abc-def-ghi
2. jkl-mno-pqr
3. stu-vwx-yza
4. bcd-efg-hij
5. klm-nop-qrs
```

Note the date you saved them. Some services expire recovery codes after a period of time or after generating new ones.

## Setting Up 2FA in Other Password Managers

### KeePassXC

KeePassXC supports TOTP natively:

1. Open the entry for the account
2. Click **Edit Entry**
3. Go to the **Advanced** section
4. Under TOTP, click **Set up TOTP**
5. Enter the secret key (from the website's QR code -- you may need to decode the QR to get the text key, or use KeePassXC's screenshot QR reader)
6. Save the entry
7. The TOTP code appears in the entry details and can be copied with Ctrl+T

### 1Password

1Password handles TOTP as a built-in field type:

1. Edit the login entry
2. Add a "One-Time Password" field
3. Scan the QR code with 1Password's camera or paste the secret key
4. Save -- 1Password will auto-copy the code during autofill

### Bitwarden

1. Edit the login entry (premium feature)
2. Scroll to the "Authenticator Key (TOTP)" field
3. Enter the secret key or scan the QR code (mobile app)
4. Save -- Bitwarden will display the code in the entry and auto-copy it during autofill

## Using 2FA Codes Day-to-Day

### The AutoFill Flow With TOTP

When AutoFill is working correctly with TOTP:

1. You visit a login page
2. [AutoFill](/guides/autofill-setup/) offers your credential
3. You authenticate with Face ID or Touch ID
4. AutoFill fills your username and password
5. The site asks for your 2FA code
6. PanicVault automatically suggests the current TOTP code (or copies it to your clipboard)
7. You paste or tap to fill the code
8. Login complete

The entire process takes about 5 seconds -- barely longer than a login without 2FA.

### When AutoFill Does Not Handle TOTP Automatically

Some sites and apps have login flows that break the automatic TOTP fill. In these cases:

1. Open PanicVault
2. Find the entry for the account
3. Tap the TOTP code to copy it
4. Switch back to the login screen and paste it
5. This adds about 10 seconds to the process

## Migrating 2FA From Another Authenticator

### From Google Authenticator

Google Authenticator now supports export:

1. Open Google Authenticator
2. Tap the menu > Transfer accounts > Export accounts
3. Select the accounts to export
4. Scan the resulting QR code with your password manager or decode the transfer data

However, some implementations of this export are complex. An alternative approach:

1. For each account in Google Authenticator:
   a. Log into the account's website
   b. Navigate to 2FA settings
   c. Remove the existing 2FA
   d. Re-enable it, this time scanning the QR code with PanicVault
   e. Delete the account from Google Authenticator after confirming the new setup works

### From Authy

Authy makes migration difficult by design. The most reliable method is re-enrolling each account:

1. Log into each 2FA-protected account
2. Disable 2FA
3. Re-enable with your password manager
4. Remove from Authy after confirming

### From a Previous Password Manager

If you are [switching from LastPass](/guides/switch-from-lastpass/) or [1Password](/guides/switch-from-1password/), TOTP secrets may transfer during the vault export/import. Check each entry after migration. If TOTP codes did not transfer, re-enroll using the method above.

## Backup and Recovery

### What Happens If You Lose Your Device

If your TOTP codes are in your password manager and your vault is [synced via iCloud](/cloud-sync/):

1. Get a new device
2. Install PanicVault
3. Open your vault from iCloud Drive
4. All your TOTP codes are intact

This is a significant advantage over a standalone authenticator app, which may be locked to the lost device.

### What If You Lose Access to Your Vault

This is where recovery codes become essential. For each critical account:

1. Use a stored recovery code to log in
2. Regain access to the account
3. Disable and re-enable 2FA with your restored vault

If you have no recovery codes and no vault access, you will need to go through each service's account recovery process -- often involving identity verification, support tickets, and significant delays.

### Backup Your Vault

Your vault backup is now even more important because it contains both passwords and 2FA secrets. See our [vault backup guide](/guides/backup-vault/) for strategies.

## Common 2FA Mistakes

**Not saving recovery codes.** When a site offers recovery codes during 2FA setup, save them immediately in your vault. They are your safety net.

**Using SMS instead of TOTP.** SMS-based 2FA is vulnerable to SIM swap attacks. Always choose "Authenticator app" over "Text message" when given the option.

**Enabling 2FA without testing.** After setup, log out and log back in to confirm the 2FA flow works before walking away.

**Not enabling 2FA on your email.** If your email is not protected by 2FA, an attacker who compromises your email password can reset passwords on every other service. Email is the foundation.

**Enabling 2FA only on "important" accounts.** Any compromised account can be used as a stepping stone. A breached social media account can be used for social engineering attacks on your more sensitive accounts.

## Related Articles

- [How to Audit Your Existing Passwords](/guides/audit-passwords/)
- [How to Back Up Your Password Vault](/guides/backup-vault/)
- [Two-Factor Authentication Overview](/two-factor-authentication/)
- [How to Set Up a Password Manager for the First Time](/guides/first-time-setup/)
- [How to Use AutoFill on iPhone/iPad With a Password Manager](/guides/autofill-setup/)
