---
title: "Understanding Recovery Codes: Your 2FA Safety Net"
description: "Learn what 2FA recovery codes are, how they work, best practices for secure storage, common mistakes to avoid, and when to regenerate them."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Two-Factor Authentication"
---

Recovery codes are the part of [two-factor authentication](/two-factor-authentication/) that most people set up once and never think about again -- until the moment they desperately need them. They are the safety net that catches you when your authenticator app is gone, your phone is lost, or your hardware key is at the bottom of a lake. Understanding how recovery codes work, how to store them securely, and when to regenerate them is just as important as enabling 2FA in the first place.

If you skip recovery codes or store them carelessly, you are not adding security -- you are adding a new way to lock yourself out. This guide covers everything you need to know to handle recovery codes correctly.

## What Recovery Codes Are

Recovery codes are one-time-use alphanumeric strings that allow you to bypass your normal 2FA method. When you enable two-factor authentication on a service, the service typically generates a set of recovery codes (usually 8 to 16) and presents them to you exactly once. These codes function as an emergency backdoor: if you cannot provide your normal second factor, you can enter a recovery code instead.

Each recovery code can be used only once. After use, it is invalidated and cannot be reused. This single-use property prevents an attacker who intercepts one code from having permanent bypass access.

Recovery codes are unrelated to your TOTP secret, your hardware key, or your phone number. They are an independent authentication path -- a separate set of credentials that the service stores (hashed) on its servers and validates when presented.

### How They Differ From TOTP

TOTP codes change every 30 seconds and are derived from a shared secret using a time-based algorithm. Recovery codes are static -- they do not change or expire on a schedule. TOTP requires a working device and app; recovery codes require only the code itself, which could be written on paper, stored in a file, or memorized.

This makes recovery codes both more durable and more dangerous than TOTP. More durable because they work regardless of device state. More dangerous because if someone obtains your recovery codes, they work indefinitely until used or regenerated.

### How They Differ From Backup Codes

Some services use the terms "recovery codes" and "backup codes" interchangeably. They are the same thing. Other services distinguish between recovery codes (for regaining account access) and [backup TOTP strategies](/two-factor-authentication/backup-totp-codes/) (for preserving your TOTP secrets themselves). In this guide, "recovery codes" refers to the one-time-use codes provided by the service for bypassing 2FA.

## How Different Services Handle Recovery Codes

Not all services implement recovery codes the same way. Understanding the variations helps you plan your storage strategy.

### Google

Google provides a set of 10 backup codes, each 8 digits long. You can view, print, or download them from your Google Account security settings. Used codes are marked as such. You can regenerate a new set at any time, which invalidates all previous codes.

Google also offers other recovery options: a recovery phone number, a recovery email address, and Google Prompts on trusted devices. Recovery codes are the option that works when all your devices are unavailable.

### GitHub

GitHub generates 16 recovery codes during 2FA setup. Each code is a short alphanumeric string. GitHub also supports setting up a [hardware security key](/two-factor-authentication/hardware-keys-vs-totp/) as a backup second factor, which is stronger than recovery codes but requires physical possession of the key.

GitHub recently introduced passkey support, but recovery codes remain available as a fallback mechanism.

### Apple (iCloud)

Apple does not use traditional recovery codes for iCloud 2FA. Instead, Apple relies on trusted devices and trusted phone numbers for account recovery. If you lose all trusted devices, account recovery is handled through Apple Support with an identity verification process that can take days. This is a notably different approach -- Apple prioritizes preventing unauthorized access over self-service recovery.

### Microsoft

Microsoft provides a single recovery code (25 characters) for personal accounts. Enterprise accounts managed by Azure AD have different recovery mechanisms controlled by the organization's administrator.

### Financial Services

Banks and financial institutions vary widely. Some provide recovery codes. Others require phone-based recovery, branch visits, or mailed verification. For [priority accounts](/two-factor-authentication/priority-accounts/) like banking, always understand the recovery process before you need it.

### Patterns to Notice

- The number of recovery codes varies from 1 to 16+ depending on the service
- Some services let you view recovery codes again later; others show them only once
- Regenerating codes always invalidates the previous set
- A few services have moved away from recovery codes entirely in favor of alternative recovery flows

## Secure Storage Strategies

The security of recovery codes comes down to where and how you store them. The threat model has two sides: protecting against unauthorized access and ensuring you can actually find and use the codes when needed.

### Strategy 1: Encrypted Password Manager

Store recovery codes in the notes field of the corresponding password entry in your password manager. If you use a [KeePass-compatible app](/keepass/) such as [PanicVault](https://panicvault.com) on macOS/iOS, the codes are encrypted with the same AES-256 or ChaCha20 encryption that protects your passwords.

**Advantages**: Codes are encrypted, backed up with your vault, organized by service, and searchable. This is the most practical approach for most people.

**Risk**: If you lose access to your vault and the recovery code you need is inside the vault, you have a circular dependency. This is the same problem discussed in the context of [storing TOTP codes in a password manager](/two-factor-authentication/password-manager-as-authenticator/) -- and it has the same solution: keep codes for vault-critical services stored outside the vault.

### Strategy 2: Printed Paper, Stored Securely

Print your recovery codes and store the paper in a physically secure location: a home safe, a safe deposit box, or a sealed envelope in a secure location known to a trusted person.

**Advantages**: Works even if all electronic devices are compromised or unavailable. No digital attack surface. Immune to malware, cloud breaches, and device failures.

**Risk**: Paper can be lost, destroyed (fire, water), or found by someone with physical access. Paper is also inconvenient to update when you regenerate codes.

### Strategy 3: Encrypted File on Separate Media

Create an encrypted file (using a tool like an encrypted disk image, VeraCrypt volume, or GPG-encrypted text file) containing all your recovery codes. Store this file on a USB drive or other media kept in a secure location separate from your primary devices.

**Advantages**: Encrypted against physical theft. Portable. Can be updated without printing.

**Risk**: You must remember the encryption password. USB drives can fail. The encrypted file format must remain readable when you need it (years from now).

### Strategy 4: Split Storage (Critical Accounts)

For your most critical accounts, use more than one strategy:

- Recovery codes for your email: printed copy in a safe AND in your password manager
- Recovery codes for your cloud storage: in your password manager AND on an encrypted USB drive
- Recovery codes for your financial accounts: printed AND stored in a separate encrypted file

Redundancy protects against any single point of failure. If the safe floods, you have the digital copy. If the password manager is inaccessible, you have the paper copy.

### What About Memorization?

Memorizing recovery codes is impractical for most people. You would need to remember dozens of random strings across dozens of services. Memory is unreliable for this kind of data. Use memory as a supplement for one or two critical services, not as a primary strategy.

## Common Mistakes

### Mistake 1: Screenshotting Recovery Codes on Your Phone

Screenshots are typically synced to cloud photo services (iCloud Photos, Google Photos), not encrypted at rest in the same way a password manager is, and visible to anyone who picks up your unlocked phone. A recovery code screenshot in your photo library is essentially an unprotected plaintext file.

If you must use your phone to capture recovery codes temporarily, transfer them to a secure location immediately and delete the screenshot.

### Mistake 2: Saving Them in a Plain Text File on Your Desktop

A file called `recovery-codes.txt` on your desktop is accessible to any malware, any person with access to your user session, and any unencrypted backup of your system. This is barely better than no storage at all.

### Mistake 3: Assuming You Will Remember Where You Stored Them

You set up 2FA on a service, carefully saved the recovery codes... somewhere. Six months later, you need them and have no idea where they are. The solution is consistency: pick one or two storage strategies and use them for every service, every time. The discipline of always storing codes in the same place is more valuable than any individual storage method.

### Mistake 4: Never Checking if Codes Have Been Used

Some services mark used recovery codes. Periodically review your remaining codes. If codes have been used that you did not use, someone else may have accessed your account. This is a security incident that requires immediate investigation: change your password, regenerate recovery codes, and review recent account activity.

### Mistake 5: Not Regenerating After Use

After using a recovery code, your available set is reduced by one. If you started with 10 and used 3, you have 7 left. Regenerate a fresh full set as soon as you regain normal access. Do not wait until you are down to your last code.

### Mistake 6: Forgetting to Regenerate After a Security Incident

If you suspect your recovery codes may have been compromised -- through a device theft, a backup breach, or any other exposure -- regenerate them immediately. Regeneration invalidates all previous codes, neutralizing any compromised ones.

## When to Regenerate Recovery Codes

Regenerate your recovery codes in any of these situations:

**After using any recovery code.** Replenish the set to its full count.

**After a device loss or theft.** If your recovery codes were stored on the lost device (even encrypted), regenerate them as a precaution.

**After a suspected security incident.** Any breach, malware infection, or unauthorized access to a storage location containing recovery codes warrants regeneration.

**Periodically as a hygiene practice.** Once or twice a year, regenerate recovery codes for critical accounts. This limits the window of exposure if codes were compromised without your knowledge.

**When you change your 2FA method.** If you switch from a [standalone authenticator to a password manager](/two-factor-authentication/move-codes-to-password-manager/) or add a hardware key, regenerate recovery codes as part of the transition.

**When you change your storage strategy.** If you move from paper storage to a password manager (or vice versa), regenerate to ensure the old storage location's codes are invalidated.

### How to Regenerate

The process varies by service but generally follows this pattern:

1. Log into the service and navigate to security or 2FA settings
2. Find the recovery codes section (may be labeled "backup codes")
3. Select "Generate new codes" or "Regenerate"
4. The service creates a new set and invalidates all previous codes
5. Save the new codes using your chosen storage strategy
6. Verify you have saved them before navigating away

## Recovery Codes and Your Backup Strategy

Recovery codes should be one component of a broader backup and recovery plan. They protect against losing your 2FA device. But what about losing your vault? Or your backup drive? Or your memory of where things are stored?

A robust 2FA backup strategy includes:

- **Recovery codes** stored securely (this guide)
- **TOTP secrets** backed up inside your encrypted vault, with the vault itself backed up to multiple locations (see the [KeePass backup guide](/keepass/backup-database/))
- **A documented recovery plan** that you (or a trusted person) can follow step by step if you are incapacitated or starting from zero
- **Regular testing** -- actually restore from backup periodically to verify it works

The overlap between recovery codes and other backup strategies is intentional. Each mechanism covers different failure modes. Recovery codes work when your TOTP device is gone. TOTP backups work when you are on a new device but have your vault. A printed code sheet works when all electronic access has failed.

## Special Considerations for Families and Teams

If you are responsible for shared accounts (family subscriptions, team infrastructure, business services), recovery code management becomes more complex.

**Shared accounts**: If multiple people need access to an account with 2FA, recovery codes should be accessible to all authorized people. Store them in a shared vault or a physically shared secure location.

**Key person risk**: If only one person knows where the recovery codes are stored, that is a single point of failure. Document the storage strategy and share it with at least one other trusted person.

**Estate planning**: Consider what happens to your accounts if you become permanently unavailable. Recovery codes stored in a safe deposit box or with a trusted attorney can enable account access as part of estate management.

## Recovery Codes Are Insurance, Not Security Theater

Recovery codes often get dismissed as a minor detail in the 2FA setup process -- a screen to click past as quickly as possible. But they are the mechanism that keeps 2FA from becoming a self-inflicted lockout. Every security measure you add creates a corresponding failure mode. The recovery code is the answer to the failure mode created by 2FA.

Treat recovery codes with the same seriousness you apply to your [password manager](/password-managers/) and your vault backups. Store them deliberately. Check them periodically. Regenerate them when circumstances change. The few minutes you invest in recovery code management are the difference between a minor inconvenience and a major crisis the next time you [lose a 2FA device](/two-factor-authentication/lost-2fa-device/).
