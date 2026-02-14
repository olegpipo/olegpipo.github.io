---
title: "How to Audit Your Existing Passwords"
description: "Systematic guide to auditing your password vault. Identify weak, reused, and compromised passwords, then fix them in priority order."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

You probably have weak, reused, or compromised passwords in your vault right now. That is not a personal failing -- it is the reality for nearly everyone. Studies show that 94% of passwords are reused or duplicated across services. The average person has 250 accounts, many created years ago when "password123" felt adequate. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, walks you through a systematic audit that identifies the worst problems first and fixes them in order of risk.

## Why Audit Your Passwords

A password audit is a security checkup for your digital life. It answers three critical questions:

1. **Which passwords are weak?** Short passwords, dictionary words, common patterns, and simple substitutions can be cracked in seconds to hours by modern hardware.

2. **Which passwords are reused?** When you use the same password on multiple sites, a breach at any one of them compromises all the others. This is the single most dangerous password habit.

3. **Which passwords are compromised?** Your email and password combinations may already be circulating in breach databases. Attackers use automated tools to try known credentials across thousands of sites.

Finding and fixing these problems does not require a single evening of suffering. You can work through them methodically over a week, focusing on the highest-risk accounts first.

## Before You Start

### Get All Your Passwords in One Place

If your passwords are scattered across browser saves, sticky notes, and memory, consolidate them into your password manager first. See our guides for [importing from browsers](/guides/import-from-browser/) and [first-time setup](/guides/first-time-setup/).

An audit is only as good as the data it covers. If half your passwords are not in your vault, you are only auditing half your exposure.

### Set Aside Time

A thorough audit of a typical vault (100-250 entries) takes 1-3 hours if you fix problems as you find them. You do not need to do it all at once. The triage phase (identifying problems) takes about 30 minutes. Fixing individual passwords takes 2-5 minutes each, and you can do a few per day.

## Phase 1: Automated Scanning

Most password managers have built-in audit tools. Use them first -- they catch the obvious problems quickly.

### PanicVault Audit

PanicVault can flag entries with weak or duplicate passwords:

1. Open your vault in PanicVault
2. Look for the audit or security report feature
3. Review the flagged entries, which typically include:
   - Passwords below a minimum strength threshold
   - Passwords reused across multiple entries
   - Entries with empty or very short passwords

### KeePassXC Audit

KeePassXC has a built-in health check:

1. Open your database in KeePassXC
2. Go to **Database > Database Reports** (or the equivalent in your version)
3. Review the health report, which shows:
   - Password strength scores for each entry
   - Entries with expired passwords
   - Entries with known weak passwords
   - Duplicate passwords across entries

### 1Password Watchtower

1Password's Watchtower feature provides the most comprehensive automated audit:

1. Open 1Password and look for the Watchtower section
2. It checks for weak passwords, reused passwords, passwords found in data breaches, and sites where you have not enabled two-factor authentication
3. Work through the recommendations in priority order

### Bitwarden Vault Health Reports

Bitwarden (premium) offers vault health reports:

1. Log into the Bitwarden web vault
2. Go to Tools > Reports
3. Run the following reports: Exposed Passwords, Reused Passwords, Weak Passwords, Unsecured Websites, Inactive 2FA

## Phase 2: Manual Triage

Automated tools catch the obvious problems. Manual review catches the nuanced ones.

### Check Your Most Critical Accounts First

Regardless of what the automated scan says, manually verify the password strength on your most important accounts:

**Tier 1 -- Highest Priority:**
- Primary email (if this is compromised, attackers can reset passwords everywhere)
- Banking and financial accounts
- Apple ID / Google Account (controls access to your devices and cloud data)
- Password manager itself (your [master password](/guides/master-password/))

**Tier 2 -- High Priority:**
- Secondary email accounts
- Social media (used for identity verification on other services)
- Cloud storage (iCloud, Google Drive, Dropbox)
- Mobile carrier account (SIM swap attacks)
- Health insurance and medical portals

**Tier 3 -- Medium Priority:**
- Shopping accounts with saved payment methods
- Subscription services
- Professional/work accounts (unless employer manages these)
- Government and tax accounts

**Tier 4 -- Lower Priority:**
- Forums and community sites
- Newsletters and marketing accounts
- One-time use accounts
- Free services without saved payment information

### What to Look For

For each entry, check:

- **Length**: Is the password at least 16 characters? 12 is the minimum acceptable. Anything shorter should be changed.
- **Randomness**: Does it look like a password manager generated it (e.g., `k7#mQ9xL4&nPw2$t`), or does it look like a human created it (e.g., `MyDog2019!`)? Human-created passwords are almost always weaker than they appear.
- **Uniqueness**: Is this password used anywhere else in your vault? Even one duplicate is one too many.
- **Age**: When was this password last changed? Passwords for critical accounts that have not been updated in years should be regenerated, especially if those services have experienced breaches.

## Phase 3: Check for Breached Credentials

Your email address and passwords may already appear in known data breaches. Checking is straightforward and important.

### Have I Been Pwned

Visit haveibeenpwned.com and enter each email address you use for online accounts. The site will tell you which breaches your email appeared in and what data was exposed.

If an email appears in a breach:
1. Change the password on the breached service immediately
2. Change the password on any other service where you used the same password
3. Enable [two-factor authentication](/guides/setup-2fa/) on the breached service if available
4. Monitor the account for suspicious activity

### Password Breach Check

Some password managers (1Password Watchtower, Bitwarden Exposed Passwords report) check your actual passwords against breach databases using a privacy-preserving technique called k-anonymity. Your password is never sent to the service -- only a partial hash is transmitted, and the matching happens locally.

If a password appears in a breach database, change it immediately, regardless of which account it is on.

## Phase 4: Fix the Problems

Now you know what is broken. Here is how to fix it efficiently.

### Batch Processing Strategy

Trying to fix all 250 passwords at once leads to burnout and abandonment. Instead:

**Day 1**: Fix Tier 1 accounts (email, banking, Apple ID). This might be 5-10 passwords. Time: 30-60 minutes.

**Day 2-3**: Fix Tier 2 accounts (secondary email, social media, cloud storage, carrier). Another 10-15 passwords. Time: 30-60 minutes per session.

**Week 2**: Work through Tier 3 accounts at a pace of 5-10 per day.

**Ongoing**: Fix Tier 4 accounts as you encounter them during normal use.

### How to Change a Password Properly

For each password that needs changing:

1. Open the account's website or app
2. Navigate to Settings > Security > Change Password (the exact path varies)
3. Use your password manager to [generate a new strong password](/guides/generate-strong-passwords/) -- at least 16 characters, fully random
4. Enter the old password and the new generated password
5. Save the new password in your vault
6. Verify the change by logging out and back in

### Handling Sites With Frustrating Password Requirements

Some sites impose counterproductive requirements: maximum length limits, no special characters, or only specific character sets. When you encounter these:

- Generate a password that meets their requirements (adjust your generator settings)
- Use the maximum length they allow
- Add a note to the vault entry about the site's password restrictions
- Accept that this password will be slightly weaker than your standard -- it is still vastly better than a reused or human-created password

### What to Do About Accounts You No Longer Use

During your audit, you will find accounts you forgot about. For each:

1. **If the account has personal data**: Log in, delete or minimize your personal information, then close/delete the account if possible
2. **If you might need it again**: Change the password to a strong, unique one and leave it
3. **If it is truly dead**: Try to close the account. If you cannot, change the password to a strong, unique one and [archive the entry](/guides/organize-vault/) in your vault

## Phase 5: Enable Two-Factor Authentication

Changing passwords is half the battle. Enabling [two-factor authentication](/two-factor-authentication/) on critical accounts is the other half. A strong, unique password plus 2FA makes an account extremely difficult to compromise.

Focus 2FA on your Tier 1 and Tier 2 accounts. See our [2FA setup guide](/guides/setup-2fa/) for detailed instructions on setting up TOTP codes in your password manager.

## Maintaining Good Password Health

An audit is not a one-time event. Build these habits:

### Ongoing

- Always use your password manager's generator for new accounts
- Never reuse passwords
- Enable 2FA whenever a new service offers it
- Save every new credential in your vault immediately

### Quarterly

- Run your password manager's automated audit tool
- Check haveibeenpwned.com for new breaches
- Review and delete any accounts you no longer use

### Annually

- Do a full manual review of Tier 1 and Tier 2 account passwords
- Regenerate passwords on your most critical accounts
- Review your [emergency access setup](/guides/emergency-access/)
- Update your [vault backup](/guides/backup-vault/)

## The 80/20 of Password Auditing

If you only have 30 minutes and want maximum impact:

1. Change your email password to a strong, unique, generated one (5 min)
2. Change your banking password (5 min)
3. Enable 2FA on your email account (5 min)
4. Check your email on haveibeenpwned.com and change passwords on any breached services (10 min)
5. Delete or change the single most-reused password in your vault (5 min)

These five actions eliminate the majority of your password risk. Everything else is important but less urgent.

## Related Articles

- [How to Generate and Store Strong Passwords](/guides/generate-strong-passwords/)
- [How to Set Up 2FA Using Your Password Manager](/guides/setup-2fa/)
- [How to Create a Secure Master Password You'll Remember](/guides/master-password/)
- [How to Organize Your Password Vault](/guides/organize-vault/)
- [Two-Factor Authentication Overview](/two-factor-authentication/)
