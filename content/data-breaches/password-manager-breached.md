---
title: "What to Do If Your Password Manager Is Breached"
description: "Action plan for the worst-case scenario -- your password manager has been breached. How to assess exposure, rotate credentials, and choose a resilient architecture."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Data Breaches & Identity"
---

A password manager breach represents a category of security incident unlike any other. When a retail website is hacked, a handful of your credentials are exposed. When your password manager is breached, every credential you own could be at risk -- every login, every secure note, every payment card, every piece of sensitive information you trusted to the vault. This guide, part of our [Data Breaches & Identity Protection](/data-breaches/) resource center, addresses this specific and deeply unsettling scenario with practical steps for assessing your exposure, responding effectively, and building a more resilient password management architecture.

## Understanding the Threat

Not all password manager breaches are equal. The severity depends on what the attackers obtained and how well the vault's encryption holds up under attack.

### What Attackers Get

In a cloud-based password manager breach, attackers typically obtain:

- **Encrypted vault files**: These contain all your passwords, notes, and other stored data, but encrypted with your master password.
- **Metadata**: Information about your account, such as your email address, billing information, and in some cases, unencrypted URLs and site names stored in your vault.
- **Infrastructure data**: Server configurations, API keys, and other technical assets that may facilitate further attacks.

The encrypted vault is the crown jewel. Whether the attacker can actually read your passwords depends on the strength of the encryption, the key derivation function, and most critically, the strength of your master password.

### The Offline Cracking Race

Once an attacker has a copy of your encrypted vault, they can attempt to crack it offline at their own pace, with their own hardware, for as long as they want. There is no rate limiting, no lockout after failed attempts, no way for you to revoke access to the copy they already have. This is fundamentally different from an online brute-force attack against a login page.

The attacker's ability to crack your vault depends on:

- **Your master password strength**: A 12-character password with mixed case and numbers can be cracked in days or weeks with modern GPU clusters. A 20-character random passphrase is effectively uncrackable with current technology.
- **The key derivation function**: Argon2 is significantly more resistant to GPU-based cracking than older functions like PBKDF2. The number of iterations matters enormously.
- **The encryption algorithm**: AES-256 and ChaCha20, used by reputable managers, are computationally secure against brute force when properly implemented.

### The LastPass Example

The [LastPass breach](/data-breaches/lastpass-breach-lessons/) is the definitive case study. Attackers obtained encrypted vaults for 33 million users. Users with strong master passwords and high iteration counts remained protected. Users with weak master passwords -- particularly those who had created accounts years earlier when LastPass's default iteration count was much lower -- faced genuine risk of vault decryption.

## Immediate Response: First 24 Hours

If you learn that your password manager vendor has been breached, act immediately. Do not wait for the vendor to confirm the severity or for security researchers to complete their analysis.

### 1. Assess the Breach Disclosure

Read the vendor's breach notification carefully. Identify:

- **What data was accessed**: Was it just user account data, or were encrypted vaults obtained?
- **When the breach occurred**: There may be a gap of weeks or months between the breach and disclosure, during which attackers had access.
- **What the vendor recommends**: Follow their guidance, but do not stop there.

If encrypted vaults were taken, proceed with the assumption that your vault will eventually be cracked unless your master password is exceptionally strong.

### 2. Change Your Master Password

Change your master password immediately. Choose a strong, random passphrase of at least 20 characters. This does not protect the copy of your vault that was already stolen -- that copy is encrypted with your old master password -- but it secures the going-forward version of your vault.

### 3. Prioritize Credential Rotation

You likely have hundreds of passwords in your vault. Rotating all of them simultaneously is overwhelming. Prioritize by impact:

**Tier 1 -- Change immediately (first 2 hours)**:
- Email accounts (these are the keys to your other accounts via password resets)
- Banking and financial services
- Cryptocurrency wallets and exchanges
- Your new password manager (if switching)
- Cloud storage (iCloud, Google Drive, Dropbox)

**Tier 2 -- Change within 24 hours**:
- Work and business accounts
- Social media accounts (especially if used for SSO/OAuth login elsewhere)
- Shopping accounts with saved payment methods
- Government accounts (tax, benefits, healthcare)

**Tier 3 -- Change within one week**:
- All remaining accounts
- Accounts at services you no longer actively use but have not deleted

### 4. Enable Two-Factor Authentication Everywhere

If the breached vault's passwords are eventually cracked, [two-factor authentication](/two-factor-authentication/) is your safety net. Enable 2FA on every account that supports it, prioritizing Tier 1 and Tier 2 accounts. Use hardware security keys or authenticator apps rather than SMS.

### 5. Rotate Sensitive Non-Password Data

If your vault contained more than just passwords, address those items too:

- **Credit card numbers**: Request new card numbers from your issuers
- **Bank account numbers**: Contact your bank to discuss options
- **API keys and tokens**: Regenerate them in the respective developer consoles
- **Secure notes**: If you stored Social Security numbers, driver's license numbers, or other government IDs, consider [freezing your credit](/data-breaches/freeze-credit/) and monitoring for [identity theft](/data-breaches/identity-theft-recovery/)
- **Recovery codes**: Regenerate 2FA recovery codes for all services

## Evaluating Your Password Manager Architecture

A breach should trigger a fundamental reassessment of your password management approach. The key architectural question is: who has copies of your encrypted vault?

### Cloud-Based Managers

Password managers like LastPass, 1Password, Bitwarden, and Dashlane store encrypted copies of your vault on their servers. The advantages are obvious: seamless sync, no file management, easy onboarding. The disadvantage is that a breach of the vendor's infrastructure puts every user's encrypted vault in attacker hands simultaneously.

The security model requires you to trust:
1. The vendor's infrastructure security (to prevent breaches)
2. The encryption implementation (to resist cracking if a breach occurs)
3. The vendor's incident response (to detect and disclose breaches promptly)

The LastPass breach demonstrated that failure at point 1 can expose every user, and that point 3 may involve months of delay.

### Local-First Managers

Password managers built on the [KeePass format](/keepass/) -- such as PanicVault, KeePassXC, and Strongbox -- take a fundamentally different approach. Your encrypted database file is a file you control. It lives on your device, on your iCloud Drive, on a USB drive, wherever you choose to store it. There is no vendor server holding a copy of every user's vault.

This architecture eliminates the specific attack vector that made the LastPass breach so devastating. An attacker would need to breach your personal device or your personal cloud storage to obtain your vault file -- a targeted attack against an individual rather than a mass harvest from a central server.

PanicVault, for example, stores your database in the standard KDBX format on your Apple devices or iCloud Drive. If PanicVault as a company disappeared tomorrow, your data remains accessible through any [KeePass-compatible application](/keepass/). There is no vendor dependency beyond the app itself, and no centralized target for attackers.

### Self-Hosted Managers

Bitwarden offers a self-hosted option where you run your own server. This gives you the sync convenience of a cloud manager with the control of a local manager, but you assume responsibility for server security, maintenance, backups, and patching. This is appropriate for technically sophisticated users and small organizations with IT resources.

## Switching Password Managers

If a breach has eroded your trust in your current provider, switching is a reasonable response. Here is how to do it safely:

### 1. Export Your Current Vault

Before changing your master password or closing your account, export your vault data. Most managers export to CSV or their own proprietary format. CSV is universally importable but stores your passwords in plaintext -- treat the export file with extreme care and delete it securely after import.

### 2. Import into the New Manager

Import the exported data into your new password manager. Verify that all entries transferred correctly, paying attention to:

- Custom fields and notes
- TOTP/2FA seeds
- Folder/group structure
- Shared vault entries

### 3. Verify and Clean Up

Spend time verifying that your most critical credentials work correctly in the new manager. Test autofill, search, and any workflows you use daily. Once confirmed, delete the plaintext export file using secure deletion (not just moving to trash).

### 4. Delete Your Old Account

After confirming that all data has been migrated successfully, close your account with the old provider. This does not affect vault copies that were already stolen in a breach, but it stops new data from accumulating on a platform you no longer trust.

## Long-Term Considerations

### Master Password Strength

A breach should permanently raise your standard for master password strength. For a vault that might be cracked offline, your master password needs to resist GPU-accelerated attacks over a period of years. A randomly generated passphrase of 5-6 words (or 20+ random characters) provides sufficient entropy.

### Regular Password Rotation

After the initial mass rotation, adopt a practice of rotating your most sensitive passwords periodically -- financial accounts, primary email, and work accounts. A [password manager](/password-managers/) makes this practical rather than burdensome.

### Zero-Knowledge Architecture

Whatever manager you choose going forward, verify that it uses zero-knowledge architecture -- meaning the vendor cannot decrypt your vault even if they wanted to. The encryption and decryption must happen entirely on your device, with only the encrypted blob ever touching the vendor's servers (if applicable).

### Key Derivation Settings

Check your new manager's key derivation settings. If it uses PBKDF2, ensure the iteration count is set to at least 600,000 (OWASP recommendation). If it supports Argon2, use it -- Argon2 is specifically designed to resist the GPU-based attacks used in offline cracking. The [KeePass format](/keepass/) supports Argon2d natively, which is one of the reasons the format remains a strong choice for security-conscious users.

## Related Articles

- [The LastPass Breach: Lessons for Password Security](/data-breaches/lastpass-breach-lessons/)
- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [How Data Breaches Happen: Anatomy of an Incident](/data-breaches/how-breaches-happen/)
- [How to Freeze Your Credit After a Data Breach](/data-breaches/freeze-credit/)
