---
title: "How to Back Up Your TOTP Codes"
description: "Complete guide to backing up TOTP secrets and authenticator codes. Encrypted backups, password manager storage, QR code archiving, and recovery planning."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Two-Factor Authentication"
---

Every TOTP code you generate is derived from a shared secret -- a string of characters that your authenticator and the service agreed on when you first enabled [two-factor authentication](/two-factor-authentication/). That secret is the real credential. The six-digit code that changes every 30 seconds is just a mathematical derivative of it. If you lose the secret, you lose the ability to generate codes, and you lose access to your account.

Most people do not think about TOTP backup until they are staring at a login screen with no way to generate the required code. By then, the options are limited and unpleasant. This guide covers how to back up your TOTP secrets before that happens, so that losing a device never means losing access to your accounts.

## Why TOTP Backup Matters

The TOTP protocol was designed for simplicity: a shared secret plus the current time produces a predictable code. This simplicity is a strength for security but a weakness for resilience. There is no "forgot my code" link. There is no server-side reset for the TOTP secret itself. If you cannot produce the code, you are locked out until you can convince the service to reset your 2FA through an account recovery process -- which may take days, require government ID, or in some cases be impossible.

The scenarios that destroy TOTP access are mundane, not exotic:

- Your phone breaks. Screen shattered, water damage, battery failure.
- You factory-reset your phone without transferring authenticator data first.
- Your phone is lost or stolen.
- You switch to a new phone and forget to migrate your authenticator.
- Your authenticator app becomes corrupted or loses its data after an OS update.
- You uninstall the app by accident.

These are not rare events. They happen to millions of people every year. A [lost 2FA device](/two-factor-authentication/lost-2fa-device/) is one of the most common reasons people contact account support, and the recovery process is often painful.

## The TOTP Secret: What You Are Actually Backing Up

When a service shows you a QR code during 2FA setup, that QR code encodes a URI that looks like this:

```
otpauth://totp/ServiceName:user@email.com?secret=JBSWY3DPEHPK3PXP&issuer=ServiceName&algorithm=SHA1&digits=6&period=30
```

The critical piece is the `secret` parameter -- in this example, `JBSWY3DPEHPK3PXP`. This is a Base32-encoded string that, combined with the current time, generates your TOTP code. Everything else in the URI (issuer, algorithm, digits, period) is metadata that tells the authenticator how to interpret the secret. Most services use the defaults (SHA1, 6 digits, 30-second period), so the secret alone is usually sufficient to reconstruct the code generator.

Backing up your TOTP codes means preserving this secret for every service where you have enabled 2FA.

## Backup Strategy 1: Store TOTP Secrets in Your Password Manager

This is the most practical and secure approach for most people. A [password manager with TOTP support](/two-factor-authentication/password-manager-as-authenticator/) stores the TOTP secret directly in the vault entry for each service, alongside the username and password. The secret is encrypted with the same strong encryption that protects your passwords.

Benefits of this approach:

- **Automatic backup.** Your TOTP secrets are backed up every time your vault is backed up. If your vault syncs across devices, your TOTP codes are available on every synced device automatically.
- **No extra tools.** You do not need a separate authenticator app, a separate backup strategy, or a separate recovery process. Everything lives in one encrypted container.
- **Searchable.** You can quickly find the TOTP entry for any service by searching your vault.
- **Encrypted at rest.** The secrets are protected by your vault's encryption -- AES-256, ChaCha20, or Twofish with Argon2d key derivation in the case of KeePass-format databases.

PanicVault, built on the [KeePass](/keepass/) ecosystem, stores TOTP secrets as protected fields in the KDBX database. This means they receive the same multi-layered encryption as passwords, including inner random stream protection that keeps secrets encrypted even while the database is loaded in memory.

How to add a TOTP secret to your password manager:

1. Go to the service's 2FA settings and begin the enrollment process.
2. When the QR code appears, scan it with your password manager (or click "Can't scan?" to get the text secret).
3. The password manager stores the secret and begins generating codes.
4. Enter the current code on the service's site to complete enrollment.
5. Save the entry. Your TOTP secret is now backed up with your vault.

### Vault Backup Is Now Critical

When your password manager holds both passwords and TOTP secrets, your vault backup strategy becomes the most important piece of your digital security infrastructure. If your vault is lost or corrupted and you have no backup, you lose everything.

Follow the [KeePass database backup guide](/keepass/backup-database/) for specific strategies. The key principles:

- **Multiple copies.** Your vault should exist in at least three places: your primary device, a synced secondary device, and a separate backup location (external drive, different cloud provider).
- **Automated sync.** Use [cloud sync](/cloud-sync/) to keep copies current across devices. Manual backup alone is too easy to forget.
- **Version history.** Enable file versioning on your cloud storage so you can recover a previous vault state if the current one is corrupted.
- **Test restoration.** Periodically verify that your backup vault can be opened and that entries are intact.

## Backup Strategy 2: Save the QR Code During Setup

When a service displays the QR code during 2FA enrollment, you have a one-time opportunity to capture the secret in a visual format. The QR code encodes the complete TOTP URI, so saving it preserves everything needed to reconstruct the code generator.

How to save QR codes securely:

1. **Screenshot the QR code** during setup, before you scan it with your authenticator.
2. **Store the screenshot in an encrypted container.** Do not leave it as an unencrypted image file. Options include:
   - A password-protected archive (7z with AES-256 encryption).
   - An encrypted disk image (macOS Disk Utility or VeraCrypt).
   - An encrypted note in your password manager.
3. **Store the container in a backup location** separate from your primary device.

This approach has a significant limitation: it only works at setup time. If you already have dozens of TOTP codes in an authenticator and you did not save the QR codes when you enrolled them, you cannot retroactively capture the secrets from most authenticator apps. You would need to re-enroll 2FA on each service to get fresh QR codes.

### Security Caution

An unencrypted screenshot of a QR code is equivalent to an unencrypted password written on a sticky note. Anyone who obtains the image can generate valid TOTP codes for your account. Always encrypt QR code screenshots, and delete unencrypted copies from screenshot folders, cloud photo libraries, and recently-deleted albums.

## Backup Strategy 3: Record the Text Secret

Most services offer a "Can't scan the QR code?" link during 2FA setup that reveals the TOTP secret as a text string. This string (typically a Base32-encoded key like `JBSWY3DPEHPK3PXP`) is all you need to regenerate codes on any device.

How to store text secrets:

1. During 2FA setup, click the option to show the secret as text.
2. Copy the secret string.
3. Paste it into the TOTP field of the corresponding entry in your password manager.
4. If not using a password manager for TOTP, paste it into an encrypted note or document.

This is the most portable backup format. A text secret can be entered into any TOTP-compatible authenticator on any device. No QR code scanner needed, no proprietary format, no app dependency.

## Backup Strategy 4: Export from Your Authenticator

Some authenticator apps support exporting your TOTP secrets. This is the only option for backing up secrets that are already enrolled in a standalone authenticator without saved QR codes.

**Google Authenticator:** Offers a "Transfer accounts" feature that generates a QR code containing all your secrets. You can scan this QR code with another instance of Google Authenticator on a different device. Note that the transfer QR code is a temporary display -- screenshot it and encrypt the screenshot if you want a persistent backup.

**Authy:** Does not support direct export. Authy's cloud backup means your secrets are on their servers, but extracting the raw secrets for use in another app requires third-party tools and is intentionally difficult.

**Microsoft Authenticator:** Supports cloud backup through your Microsoft account. Does not offer easy export of raw TOTP secrets.

**Aegis Authenticator (Android):** Offers full export of all secrets in JSON or encrypted format. This is one of the most backup-friendly authenticator apps available.

**Raivo OTP (iOS):** Supports export to various formats. Another backup-friendly option for iOS users.

If your current authenticator does not support export, the migration path is to re-enroll 2FA on each service, capturing the secret in your password manager this time. It is tedious, but it is a one-time process. Our guide to [moving codes to a password manager](/two-factor-authentication/move-codes-to-password-manager/) walks through this process step by step.

## Backup Strategy 5: Recovery Codes as Last Resort

[Recovery codes](/two-factor-authentication/recovery-codes/) are not the same as TOTP secret backups. They are one-time codes that bypass 2FA entirely, provided by the service during setup. They do not let you generate new TOTP codes -- they let you sign in without a TOTP code.

Recovery codes serve as an emergency fallback, not a primary backup strategy. Use them to regain access after a device loss, then immediately set up 2FA again with proper backup.

That said, recovery codes are a critical layer in your backup strategy:

- Save recovery codes for every service in your password manager.
- If you print them, store the printout in a physically secure location.
- Regenerate recovery codes periodically (some expire or are limited in quantity).
- After using a recovery code, generate new ones immediately.

## What Not to Do

### Do Not Store Secrets in Plaintext Files

A text file on your desktop called `2fa-secrets.txt` is an invitation for trouble. Any malware, any unauthorized access to your computer, any unencrypted backup that includes your desktop folder, exposes every TOTP secret you own. Always encrypt.

### Do Not Rely on Screenshot Folders

Screenshots taken during 2FA setup often end up in cloud photo libraries (Google Photos, iCloud Photos, Amazon Photos) that are not encrypted at rest. They appear in "recent" folders on your device and may be visible to anyone who picks up your phone. Delete unencrypted screenshots after saving the secret in an encrypted location.

### Do Not Assume Your Authenticator Backs Up Automatically

Some authenticator apps backup to the cloud. Others do not. Some have changed their behavior between versions. Verify your specific app's backup status rather than assuming. Go to the app's settings and confirm that cloud backup is enabled and working.

### Do Not Store Secrets in the Same Place as Your Master Passphrase

If someone obtains your vault's master passphrase and a copy of your vault, they have everything. Your master passphrase should exist only in your memory and possibly in a sealed envelope held by a trusted person. It should not be stored in a digital file alongside your vault.

## Building a Complete TOTP Backup Plan

The most resilient approach combines multiple strategies:

1. **Primary:** Store all TOTP secrets in your password manager. This gives you encrypted, synced, searchable backup that is always current.

2. **Secondary:** Maintain recovery codes for every service in the password manager's notes field. This provides an alternative entry path if TOTP generation fails for any reason.

3. **Tertiary:** Keep an offline backup of your vault on an external drive, updated monthly. Store the drive in a separate location from your primary devices.

4. **Emergency:** Print recovery codes for your three most critical accounts (email, password manager if cloud-based, financial) and store the printout in a safe or lockbox.

This layered approach means that:

- If you lose your phone, you open your vault on another device. No disruption.
- If you lose all your devices, you restore your vault from your offline backup. Minor disruption.
- If your vault is somehow corrupted on all copies, you use printed recovery codes to access your critical accounts and rebuild. Major disruption, but not catastrophic.
- The only scenario that defeats this plan is losing all devices, all vault backups, and all printed recovery codes simultaneously -- which would require something like a house fire that destroys both the safe containing the printout and every device in the house, while the cloud backup is also inaccessible. At that point, you have larger problems than 2FA recovery.

## How Often to Verify Your Backups

A backup you have never tested is not a backup -- it is a hope. Schedule these verification tasks:

**Monthly:** Confirm that your vault syncs correctly across all devices. Open the vault on each device and verify that recent entries are present.

**Quarterly:** Open your vault from the offline backup to verify it is not corrupted. Check that you can read entries and generate TOTP codes.

**After any device change:** When you get a new phone, tablet, or computer, verify that your vault is accessible and TOTP codes generate correctly before wiping or returning the old device.

**After any 2FA change:** When you add 2FA to a new service or re-enroll on an existing one, verify that the secret is saved in your vault and that recovery codes are stored.

## The Cost of Not Backing Up

The time investment for a proper TOTP backup strategy is measured in minutes. Storing secrets in your password manager happens naturally during 2FA enrollment. Saving recovery codes takes thirty seconds per service. Setting up vault backup is a one-time task.

The cost of not backing up is measured in hours, days, or permanent loss. Account recovery processes are slow, stressful, and not guaranteed to succeed. Some accounts -- particularly cryptocurrency wallets and privacy-focused services -- may be permanently inaccessible without 2FA.

Every TOTP secret you add to your authenticator without a backup is a bet that you will never lose that device. It is a bet you will eventually lose. Back up your codes now, verify the backup works, and never worry about device loss again.
