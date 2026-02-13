---
title: "How to Move Your 2FA Codes to a Password Manager"
description: "Step-by-step guide for migrating TOTP codes from standalone authenticator apps to a password manager. Covers export methods, re-enrollment, verification, and avoiding lockouts."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Two-Factor Authentication"
---

Consolidating your [two-factor authentication](/two-factor-authentication/) codes into a password manager is one of the most impactful security improvements you can make -- not because it changes the underlying cryptography, but because it solves the practical problems that cause real 2FA failures. Lost phones, forgotten backup codes, and the inability to access a critical account at the worst possible moment are far more common than cryptographic attacks. Moving your TOTP secrets into an encrypted, backed-up vault addresses all of these.

This guide walks through the complete migration process: how to export or re-enroll your TOTP secrets, how to verify everything works, and how to avoid the pitfalls that can lock you out during the transition.

## Before You Start: What You Need

### A Password Manager That Supports TOTP

Not all password managers handle TOTP. You need one that can store TOTP secret keys (the `otpauth://` URI) and generate time-based codes. [KeePass-compatible apps](/keepass/) support TOTP through the standardized KDBX format, and many popular managers like 1Password and Bitwarden include it as well. PanicVault, for example, stores TOTP secrets inside your encrypted KeePass vault on Apple devices, giving you code generation alongside your passwords with full AES-256 or ChaCha20 encryption.

If you are evaluating options, our comparison of the [best authenticator apps](/two-factor-authentication/best-authenticator-apps/) covers TOTP support across different tools, and the [password manager as authenticator](/two-factor-authentication/password-manager-as-authenticator/) guide explains the tradeoffs in depth.

### A Complete Inventory of Your 2FA Accounts

Open your current authenticator app and count every entry. Write them down. It is surprisingly easy to miss an account during migration and discover the gap only when you need to log in weeks later.

Organize your inventory by priority:

- **Critical accounts**: Email, cloud storage, financial services, domain registrar, hosting providers
- **Important accounts**: Social media, work accounts, developer platforms
- **Standard accounts**: Shopping sites, forums, media subscriptions

### Time and Patience

This process takes time. Each account requires visiting the service's security settings, disabling and re-enabling 2FA, and verifying the new setup. Budget 3-5 minutes per account. If you have 30 accounts, set aside two hours.

### Recovery Codes for Critical Accounts

Before touching anything, ensure you have current recovery codes for your most important accounts. If the migration goes wrong on any individual service, recovery codes are your safety net. Store them temporarily in a secure location -- a printed sheet, an encrypted note, or your [password manager](/password-managers/) itself.

## Method 1: Re-Enrollment (Recommended)

Re-enrollment is the most reliable migration method. You disable 2FA on each service, then re-enable it, scanning the new QR code with your password manager instead of your old authenticator app.

### Why Re-Enrollment Is Best

When you re-enroll, the service generates a fresh TOTP secret. This means:

- The old secret in your previous authenticator becomes invalid immediately
- There is no ambiguity about which app has the active secret
- You get a clean start with a verified working setup
- The service often provides fresh recovery codes

Export-based methods (covered below) can leave you with stale or duplicate secrets, which creates confusion and potential lockout risk.

### Step-by-Step Re-Enrollment Process

**1. Log into the service and navigate to security settings.**

Find the 2FA or two-step verification section. This is typically under Settings > Security, Settings > Account Security, or Settings > Privacy & Security. Every service puts it somewhere slightly different.

**2. Disable the existing 2FA.**

Most services require you to enter a current TOTP code to disable 2FA. Open your old authenticator app and enter the code. Some services may require you to enter your password again as confirmation.

If the service does not let you disable 2FA without a current code and you have lost access to your authenticator, use a recovery code instead.

**3. Re-enable 2FA and choose "Authenticator app."**

The service will display a QR code and usually a text version of the secret key. Both contain the same information: the `otpauth://totp/` URI that includes the secret, issuer, account name, and algorithm parameters.

**4. Add the secret to your password manager.**

In your password manager, find the entry for this service (or create one if it does not exist). Add the TOTP secret. Most managers let you scan the QR code directly; others require you to paste the secret key or the full `otpauth://` URI.

If your password manager displays the QR code or lets you scan it via a camera, use that. If you need to enter the secret manually, use the text version shown by the service -- it is typically a base32-encoded string like `JBSWY3DPEHPK3PXP`.

**5. Verify the code.**

Before confirming the setup on the service's website, verify that your password manager generates the correct six-digit code. The service will ask you to enter a code to confirm. Enter the code from your password manager, not from your old authenticator app.

If the code does not match, check the time on your device (TOTP is time-sensitive), verify you entered the secret correctly, and try again with the next code.

**6. Save the recovery codes.**

Most services display a set of recovery codes after enabling 2FA. Save these in your password manager entry for the service, or store them separately according to your [recovery code strategy](/two-factor-authentication/recovery-codes/).

**7. Remove the entry from your old authenticator.**

Only after confirming the new setup works should you delete the entry from your old app. The old secret is now invalid (because you disabled and re-enabled 2FA), so the old entry would generate incorrect codes anyway.

**8. Mark the account as migrated on your checklist.**

Track your progress. Do not rely on memory for a process that spans dozens of accounts.

### Handling Services That Do Not Allow Disabling 2FA

Some services -- particularly enterprise and government services -- do not allow you to disable 2FA once it is enabled. For these, you have two options:

- **Use the original secret**: If you have the original QR code or secret key (some people save screenshots during initial setup), enter it into your password manager. Verify it generates matching codes.
- **Contact support**: Some services can reset your 2FA through their support process, allowing you to re-enroll.
- **Keep the old authenticator**: As a last resort, keep the old authenticator app installed with just these accounts until you find a way to re-enroll.

## Method 2: Export and Import

Some authenticator apps support exporting TOTP secrets, which can then be imported into a password manager. This method is faster but carries risks.

### Google Authenticator Export

Google Authenticator allows exporting accounts as QR codes (Settings > Transfer accounts > Export accounts). The export QR code contains the secrets for selected accounts in a proprietary protobuf format. Some tools and password managers can decode this format, but it is not a universal standard.

**Risks**: The export QR code contains your TOTP secrets in a transferable format. Anyone who photographs or scans this code has full access to those TOTP secrets. Perform the export in a private setting and do not save the QR code image.

### Aegis Authenticator Export

Aegis (Android) supports exporting to a JSON file, optionally encrypted. The JSON format is well-documented and many tools can parse it. This is one of the cleaner export paths available.

### Raivo Export

Raivo (iOS) supports exporting to a JSON or ZIP file. Check the export format documentation for compatibility with your target password manager.

### Importing Into a Password Manager

If your password manager supports importing from your authenticator's export format, the process is straightforward: export from the authenticator, import into the manager, verify codes, and then remove the entries from the authenticator.

For KeePass-compatible managers, you may need to use an intermediary tool or script to convert the export format into KDBX entries with TOTP fields. The KeePass community maintains several conversion tools for common formats.

### Why Export-Import Is Riskier

After an export-import, both your old authenticator and your password manager have valid copies of the same TOTP secrets. This creates ambiguity:

- Which app is the "real" one?
- If you later change the secret on the service, which app has the current one?
- If someone else gained access to the export file, they also have valid secrets

Re-enrollment avoids all of these problems by generating a fresh secret and invalidating the old one.

## Verification: The Step Most People Skip

After migrating each account, you must verify. Not "probably works" -- actually confirm it.

### Immediate Verification

Log out of the service and log back in using the TOTP code from your password manager. If the code works, the migration for that account is complete.

### Delayed Verification

Some TOTP timing issues only appear when codes are near the edge of a 30-second window. If you want to be thorough, verify again a few hours later to confirm consistent code generation.

### Cross-Device Verification

If your password manager syncs across devices, verify that the TOTP codes appear and work correctly on each device. Sync delays can occasionally cause issues, and it is better to discover them now than during an urgent login.

## Post-Migration: Securing Your New Setup

### Update Your Backup Strategy

Your password vault now contains both your passwords and your TOTP secrets. This makes the vault significantly more critical. If you lose it without a backup, you lose access to everything.

Ensure you have:

- **At least two backup copies** of your vault in different physical locations
- **A tested restoration process** -- have you actually restored from backup and verified it works?
- **Recovery codes** for your most critical accounts stored separately from the vault

For KeePass databases, the backup is straightforward: copy the `.kdbx` file. See the [KeePass backup guide](/keepass/backup-database/) for a comprehensive strategy.

### Strengthen Your Master Password

With TOTP secrets in the vault, the consequences of a compromised master password are higher. If your master password is not already strong, now is the time to upgrade it. A passphrase with 80+ bits of entropy is a reasonable target.

### Consider What Stays Outside the Vault

Some security-conscious users keep their most critical TOTP secrets outside the password manager:

- **Email account TOTP**: If your password manager recovery depends on email access, consider keeping the email TOTP in a separate authenticator or on a [hardware key](/two-factor-authentication/hardware-keys-vs-totp/).
- **Cloud storage TOTP**: If your vault is stored in cloud storage, the TOTP for that storage account creates a circular dependency. Keep it separate.
- **Password manager account TOTP**: If you use a cloud-based password manager, obviously do not store that service's TOTP inside itself.

For everything else -- social media, shopping sites, forums, developer tools -- consolidating into the vault is pragmatic and safe.

### Clean Up Your Old Authenticator

After all accounts are migrated and verified:

1. Double-check your migration checklist one final time
2. Remove all entries from the old authenticator
3. Optionally uninstall the old authenticator, or keep it for the few accounts that could not be migrated

Do not leave old, potentially outdated TOTP secrets in an abandoned authenticator app. Stale security configurations are a liability.

## Troubleshooting Common Issues

### "Invalid code" After Migration

**Time sync**: TOTP depends on accurate time. If your device's clock is off by more than 30 seconds, codes will not match. Enable automatic time sync in your device settings.

**Wrong algorithm or digits**: Most services use SHA-1 with 6-digit codes and 30-second periods. Some services use SHA-256, 8-digit codes, or different periods. Ensure your password manager entry matches the service's parameters.

**Stale secret**: If you used export-import and the service has since been re-enrolled, the old secret is invalid. Re-enroll the account fresh.

### Locked Out During Migration

If you disable 2FA on a service and then cannot re-enable it (or cannot log in at all), use your recovery codes. This is exactly what they are for. If you do not have recovery codes, contact the service's support for account recovery.

### Password Manager Does Not Support TOTP

If your password manager does not support TOTP storage, you may need to switch managers or use a [dedicated authenticator app](/two-factor-authentication/google-authenticator-vs-builtin/) alongside your password manager. KeePass-compatible apps universally support TOTP through the standard OTP field in the KDBX format.

## The Circular Dependency Problem

The most important thing to understand about storing TOTP in a password manager is the circular dependency risk. If your vault is locked behind a master password and you need a TOTP code to access the service where your vault is stored, you have a problem.

Avoid this by ensuring:

1. Your vault file is accessible without any 2FA-protected service (local copy on device, USB backup)
2. The TOTP for any service involved in accessing your vault is stored separately
3. You have printed recovery codes for critical services in a physically secure location

This is a solvable problem, but it requires intentional planning. The [backup TOTP codes guide](/two-factor-authentication/backup-totp-codes/) covers strategies for breaking circular dependencies.

## Migration Checklist Summary

Use this as a reference during your migration:

1. Inventory all 2FA accounts in your current authenticator
2. Save recovery codes for critical accounts
3. For each account:
   - Log into the service
   - Disable existing 2FA (enter current code)
   - Re-enable 2FA
   - Add the new TOTP secret to your password manager
   - Verify the code works by entering it on the service
   - Save new recovery codes
   - Remove the old entry from the authenticator
   - Check off the account on your list
4. Verify all migrated accounts on all devices
5. Update your vault backup
6. Clean up the old authenticator
7. Test a full vault restore from backup

The process is methodical, not complicated. Take it one account at a time, verify as you go, and do not rush. A careful migration takes a couple of hours and protects you for years.
