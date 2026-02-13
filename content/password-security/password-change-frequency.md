---
title: "How Often Should You Change Your Passwords?"
description: "Discover how often you should really change your passwords. Learn why NIST dropped the 90-day rule and when changing passwords actually matters."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Password Security"
---

For decades, the standard advice was simple: change your passwords every 60 to 90 days. IT departments enforced it. Corporate compliance required it. Security training repeated it like a mantra. But in recent years, the world's leading cybersecurity authorities have reversed course entirely. The modern consensus, backed by research and real-world data, is that **routine password rotation does more harm than good**. The answer to how often you should change your passwords is nuanced, and understanding it is a key part of solid [password security](/password-security/).

This article breaks down why the old advice changed, what the current recommendations are, when you genuinely need to change a password, and how to build a practical strategy that keeps your accounts safe without driving you mad.

## The Old Rule: Change Every 90 Days

The 90-day password rotation policy became ubiquitous in the early 2000s. It made intuitive sense at the time. If an attacker somehow obtained your password, forcing a change every three months would limit how long they could use it. Government agencies, banks, hospitals, and universities all adopted the practice as a baseline security measure.

The logic was rooted in the computational limits of older hardware. In the 1980s and 1990s, it might take an attacker weeks or months to crack a hashed password through brute force. A 90-day window seemed like a reasonable safety net -- by the time the password was cracked, you would have already moved on to a new one.

But two things changed:

1. **Password cracking became exponentially faster.** Modern GPUs can test billions of password candidates per second. A weak password does not survive 90 days -- it falls in minutes.
2. **Researchers discovered that forced rotation made passwords weaker, not stronger.**

The 90-day rule was a relic of a slower era, and continuing to follow it blindly was actively undermining security.

## What NIST Actually Recommends Now

In 2017, the National Institute of Standards and Technology (NIST) published a landmark revision to its digital identity guidelines (SP 800-63B). Among the most significant changes was a direct statement that **password expiration policies should not be imposed** unless there is evidence of compromise.

The key NIST recommendations include:

- **Do not require periodic password changes.** Forced rotation leads to predictable patterns.
- **Screen passwords against known breach databases.** Block passwords that have appeared in previous data breaches.
- **Enforce a minimum length of 8 characters**, with a strong recommendation for longer passwords and passphrases.
- **Do not impose arbitrary complexity rules** (such as requiring uppercase, lowercase, numbers, and symbols).
- **Allow all printable characters**, including spaces, to encourage passphrases.

Microsoft followed suit in 2019 by removing password expiration policies from its Windows 10 security baseline. The Federal Trade Commission (FTC) and the UK's National Cyber Security Centre (NCSC) have published similar guidance. The consensus is clear: **routine forced rotation is an outdated practice**.

## The UNC Chapel Hill Study: Evidence That Rotation Backfires

One of the most cited pieces of evidence against forced password changes comes from a 2010 study conducted by researchers at the University of North Carolina at Chapel Hill. The team analyzed over 10,000 expired password hashes from university accounts that had been subject to mandatory rotation every three months.

Their findings were striking:

- **17% of new passwords could be cracked within 5 guesses** if the attacker knew the previous password.
- Users overwhelmingly used **predictable transformation patterns**: incrementing a number (`Summer2025` becomes `Summer2026`), moving a special character (`!Password` becomes `Password!`), or toggling capitalization.
- For 41% of accounts, the researchers could crack the new password **within 3 seconds** using the old password as a starting point.

The study demonstrated a fundamental flaw in rotation policies: when people are forced to change passwords frequently, they do not create entirely new, random passwords. They make minimal, predictable modifications to their existing ones. An attacker who has captured one password can often predict the next.

This is the central paradox of forced rotation. The policy exists to limit damage from compromised credentials, but it produces credentials that are easier to compromise in the first place.

## When You SHOULD Change Your Password

Abandoning routine rotation does not mean you should set a password once and never think about it again. There are specific situations where changing a password immediately is both necessary and urgent:

### After a Confirmed Data Breach

If a service you use suffers a data breach and your credentials may have been exposed, change your password on that service immediately. Equally important, change it on **any other service where you used the same password**. This is one of the primary reasons [password reuse is so dangerous](/password-security/password-reuse-dangers/) -- a single breach can cascade across every account sharing those credentials.

PanicVault's breach monitoring features help here by alerting you when your stored accounts appear in known breach databases, so you can act quickly rather than discovering the exposure months later. For a detailed response plan, see our guide on [what to do after a data breach](/data-breaches/what-to-do-after-breach/).

### If You Suspect Unauthorized Access

If you notice unfamiliar login activity, receive unexpected password reset emails, or see changes to your account that you did not make, treat it as an active compromise. Change the password, enable [two-factor authentication](/two-factor-authentication/) if it is not already active, and review connected devices and sessions.

### After Sharing a Password

Sometimes you share a streaming or utility account password with someone -- a roommate, a family member, a contractor. When that sharing arrangement ends, change the password. People do not always have malicious intent, but ex-roommates and former employees should not retain access to your accounts indefinitely.

### When a Password Is Weak or Reused

If you audit your passwords and discover that some are short, based on dictionary words, follow common patterns, or are reused across multiple sites, change them. This is not routine rotation -- it is remediation. A [password manager](/password-managers/) makes this process manageable by generating [strong, unique passwords](/password-security/strong-password-guide/) for each account and storing them for you.

### After Malware or Phishing Exposure

If your device was infected with a keylogger or infostealer, or if you entered credentials on a phishing page, you must assume those passwords are in an attacker's hands. Change them immediately, starting with your email and financial accounts, then working outward. Understanding [how hackers steal passwords](/password-security/how-hackers-steal-passwords/) can help you recognize these scenarios before they escalate.

## The Problem with Forced Rotation in Organizations

Many organizations still enforce periodic password changes despite the updated guidance. If you work in an environment with mandatory rotation policies, it is worth understanding why these policies persist and what you can do within them.

### Why Companies Still Enforce It

- **Regulatory compliance.** Some industries (healthcare, finance, government contracting) operate under regulations that were written before the NIST update and have not caught up. PCI DSS, for example, historically required 90-day rotation, though recent versions have begun to soften this language.
- **Institutional inertia.** Changing security policies requires review, approval, and often retraining. It is easier to keep the existing policy than to justify removing it.
- **Liability concerns.** If a breach occurs and the organization had no rotation policy, it can be perceived as negligent -- even if the policy would not have prevented the breach.

Understanding the nuances of [password expiration policies](/password-security/password-expiration-policies/) can help security teams make the case for modern approaches that actually reduce risk.

### How to Cope with Forced Rotation

If you are stuck with a 90-day rotation policy, resist the temptation to use predictable patterns. Instead:

1. **Use a password manager** to generate a completely new random password each time.
2. **Do not increment numbers or shift characters.** Each new password should bear no resemblance to the previous one.
3. **Use a passphrase** if the system allows sufficient length. A new set of random words every cycle is easier to type than a random string.
4. **Never write passwords on sticky notes** attached to your monitor. If you must write one down, lock it in a drawer until you have committed it to memory, then destroy it.

## A Practical Modern Password Strategy

Given everything above, here is a practical framework for managing password changes in your personal life:

### Set Strong Passwords Once

For each account, generate a long, random password or passphrase. Aim for at least 16 characters for standard accounts and 20+ characters (or 5+ random words) for high-value accounts like email, banking, and your password manager's master password. Store everything in an encrypted vault. PanicVault makes it easy to generate, store, and autofill these passwords across all your devices.

### Enable Two-Factor Authentication Everywhere

A [strong second factor](/two-factor-authentication/) means that even if a password is compromised, the attacker still cannot access your account without your phone or security key. This dramatically reduces the urgency of password rotation because a stolen password alone is no longer sufficient.

### Monitor for Breaches Continuously

Rather than changing passwords on a fixed schedule, **change them in response to events**. Subscribe to breach notification services. Use a password manager with built-in breach monitoring. When an alert fires, act on it promptly. This event-driven approach targets the actual risk rather than wasting effort on arbitrary calendar dates.

### Audit Periodically, Not Rotate

Once or twice a year, review your password vault. Look for:

- **Reused passwords** that need to be made unique
- **Short or weak passwords** that predate your current practices
- **Accounts you no longer use** that should be closed or have their passwords randomized
- **Accounts lacking two-factor authentication** that should have it enabled

This kind of [password hygiene](/password-security/password-hygiene/) audit is far more effective than changing everything on a timer. It addresses real weaknesses instead of creating the illusion of security through rotation.

### Treat Your Email as the Crown Jewel

Your primary email account is the skeleton key to your digital life. It is the recovery address for almost every other account you own. If an attacker controls your email, they can reset passwords elsewhere at will. Make sure your email password is exceptionally strong, unique, and protected by the strongest available second factor (a hardware security key, if possible). If there is one password you should occasionally evaluate and strengthen, it is this one.

## What About Password Managers Themselves?

Your password manager's master password is the one password you must actually remember. It should be a long, random passphrase that you have never used anywhere else. Should you change it periodically?

The practical answer is: **only if you have reason to believe it has been compromised.** If you entered it on a device that might have been infected, if someone observed you typing it, or if you suspect the manager's encrypted vault file was accessed by an unauthorized party, change it immediately.

Otherwise, a strong, unique master passphrase that is not reused anywhere does not benefit from rotation. The same principles apply to it as to any other password -- change it in response to events, not on a calendar.

## The Bottom Line

The old advice to change your passwords every 90 days is not just outdated -- it is counterproductive. Decades of research and the combined guidance of NIST, Microsoft, the FTC, and the NCSC all point to the same conclusion: **create strong, unique passwords, store them in a password manager, enable two-factor authentication, and change passwords only when there is a specific reason to do so.**

The triggers for a password change are clear:

- A breach affecting a service you use
- Evidence of unauthorized access to your account
- Discovery that a password is weak, reused, or shared
- Exposure to malware or phishing

Everything else is noise. Stop rotating passwords on a schedule. Start building passwords that do not need to be rotated.

PanicVault supports this approach by giving you a secure, local vault for generating and storing strong passwords, monitoring for breaches, and making it simple to update credentials when a real threat demands it -- no subscription fees, no cloud dependency, just practical security under your control.
