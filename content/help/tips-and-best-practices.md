---
title: "Tips & Best Practices"
description: "Practical advice for using PanicVault: protect your master password, keep backups, use TOTP, organize with groups and tags, and tune your lock timeout."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Reference"
weight: 180
---

A short collection of habits that make PanicVault safer and easier to live with. Each section below is a small change you can make once and benefit from every day.

## Protect Your Master Password

- Choose a unique, strong master password that you do not use anywhere else
- Consider using a passphrase (several random words) for easier memorization
- Never share your master password
- If you write it down, store the paper in a secure physical location (like a safe)

The [Password Generator](/help/password-generator/) can create a passphrase for you.

## Make Regular Backups

- Export your vault periodically and store the .kdbx file in a safe backup location
- If you use [iCloud Drive](/help/icloud-drive-sync/) or [Google Drive](/help/google-drive-sync/) sync, your vault is automatically backed up to the cloud
- Consider keeping a copy on an external drive or a second cloud service for extra safety
- The .kdbx file is fully encrypted -- it is safe to store backups in locations you do not fully control

Exporting is covered in [Vault Settings](/help/vault-settings/).

## Use TOTP for Important Accounts

- Set up two-factor authentication on your most important accounts (email, banking, social media)
- Store the TOTP secrets in PanicVault alongside the passwords
- This gives you 2FA codes without relying on a separate authenticator app

See [Two-Factor Authentication (TOTP)](/help/two-factor-authentication/) for setup steps.

## Organize with Groups and Tags

- Create groups for different categories (Personal, Work, Finance, Social Media)
- Use nested subgroups for finer organization
- Add tags for cross-cutting categories (for example, "important", "shared", "expiring")
- Use the search feature to quickly find entries when your vault grows large

See [Groups & Folders](/help/groups/) and [Entries (Passwords)](/help/entries/).

## Set Entry Expiration Dates

- Set expiry dates on entries for accounts where you want to rotate passwords regularly
- Expired entries show a visible "EXPIRED" badge so you know which passwords need updating

## Review Lock Timeout Settings

- Keep the lock timeout short (30 seconds or 1 minute) for maximum security
- If you are in a secure environment, you can extend the timeout
- Remember that the same timeout applies when the app goes to the background -- if you briefly switch apps and come back before the timer expires, the vault stays unlocked

The timeout lives in [Security & Settings](/help/security-and-settings/).
