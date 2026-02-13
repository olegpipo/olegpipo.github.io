---
title: "Why Password Expiration Policies Are Being Abandoned"
description: "Mandatory password rotation creates weaker passwords. Learn why NIST, Microsoft, and the UK NCSC now recommend against forced password expiration policies."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Password Security"
---

For decades, the 90-day password reset was gospel in corporate IT. Every quarter, employees would see the dreaded prompt -- "Your password will expire in 3 days" -- and dutifully change `Summer2024!` to `Fall2024!`. The ritual felt secure. It was anything but. Today, every major [password security](/password-security/) authority has reversed course on mandatory password rotation, and the evidence behind that reversal is overwhelming.

This article examines how password expiration policies became standard practice, why the research shows they actively weaken security, and what organizations and individuals should do instead.

## The Origin of the 90-Day Rule

The concept of regular password rotation dates back to the 1980s and early 1990s, when computing environments were fundamentally different. Passwords were stored as unsalted hashes or, in some cases, in plaintext. Brute-force attacks were slow but steady. In that context, the logic held: if an attacker obtained a password hash, it might take weeks or months to crack. Rotating passwords every 90 days meant that by the time an attacker succeeded, the password would already be obsolete.

This reasoning was codified into compliance frameworks. The Department of Defense's "Rainbow Series" publications recommended periodic password changes. NIST's earlier guidelines reinforced the practice. PCI DSS required password changes every 90 days for systems handling payment card data. HIPAA auditors expected rotation policies in healthcare settings.

By the early 2000s, the 90-day password change had become so deeply embedded in IT policy that questioning it was almost heretical. Security teams enforced it not because they had evidence it worked, but because every compliance framework demanded it and every auditor checked for it.

## The Research That Changed Everything

### UNC Chapel Hill: Predictability of New Passwords

The most cited study on the futility of forced password changes comes from researchers at the University of North Carolina at Chapel Hill. In 2010, they analyzed over 51,000 accounts with access to more than 7,700 historical passwords. Their findings were damning:

- **17% of new passwords** could be guessed within five attempts if the attacker knew the old password
- **41% of new passwords** could be cracked offline within three seconds given the previous password hash
- Users followed predictable transformation patterns: incrementing a number, changing a season or month, shifting a special character, or toggling capitalization

The transformations were so formulaic that the researchers built an algorithm to predict new passwords from old ones. The "security" gained by forcing a password change was largely illusory -- an attacker who had already compromised one password could trivially guess the next.

> "Mandatory password expiration does not prevent compromise. It encourages users to create passwords that follow predictable patterns, which makes the attacker's job easier, not harder."

### Carleton University: The Cost-Benefit Analysis

A 2010 paper by Cormac Herley at Microsoft Research and a subsequent 2016 analysis by researchers at Carleton University formalized what security practitioners had long suspected. They modeled the security gain from password expiration against the usability cost and concluded that:

- Forced rotation provides minimal benefit against online attacks (which are rate-limited anyway)
- Against offline attacks, rotation only helps if the attacker's cracking speed is slower than the rotation interval -- an increasingly unlikely scenario with modern GPUs
- The usability cost (weaker passwords, increased helpdesk calls, written-down credentials) far exceeds the marginal security benefit

### Real-World Helpdesk Data

Beyond academic research, the operational costs tell their own story. Gartner has estimated that **20 to 50 percent of all helpdesk calls** are password-related, with a significant portion driven by expiration-forced resets. Each call costs an organization between $15 and $70 to resolve. For a company with 10,000 employees rotating passwords quarterly, that translates to tens or hundreds of thousands of dollars annually -- spent making security worse.

## What the Authorities Now Say

### NIST SP 800-63B

In 2017, NIST published Special Publication 800-63B, "Digital Identity Guidelines," which marked a historic reversal. The key recommendation:

**"Verifiers SHOULD NOT require memorized secrets to be changed arbitrarily (e.g., periodically)."**

NIST specifically noted that forced rotation leads to weaker passwords and that passwords should only be changed when there is evidence of compromise. The guidelines also recommended:

- Allowing passwords up to at least 64 characters
- Accepting spaces and all printable ASCII characters
- Screening passwords against known breach dictionaries
- Eliminating composition rules (mandatory uppercase, numbers, symbols)

These guidelines have been updated and reaffirmed in subsequent revisions, and they now serve as the foundation for federal authentication policy.

### Microsoft's Policy Reversal

In 2019, Microsoft dropped password expiration from its Windows security baseline recommendations. Aaron Margosis of Microsoft wrote in the announcement:

> "Periodic password expiration is an ancient and obsolete mitigation of very low value."

Microsoft's reasoning mirrored the academic research: when humans are forced to change passwords frequently, they make small, predictable modifications. The company now recommends enforcing banned password lists and multi-factor authentication instead.

This was a significant moment. Microsoft's security baselines influence millions of organizations worldwide. When the company that makes the operating system running most enterprise desktops says forced rotation is counterproductive, the message is hard to ignore.

### UK NCSC Guidance

The UK's National Cyber Security Centre (NCSC) has been equally direct. Their guidance states:

> "Regular password changing harms rather than improves security. Many systems will force users to change their password at regular intervals, typically every 30, 60, or 90 days. This imposes burdens on the user and there are costs associated with managing this. Forcing password expiry carries no real benefits."

The NCSC recommends that organizations focus on detecting compromised credentials through monitoring and breach checking rather than relying on calendar-driven rotation.

### Other Authorities

The chorus is broad:

- **FTC (Federal Trade Commission)**: Chief Technologist Lorrie Cranor published a blog post in 2016 explicitly discouraging mandatory password changes
- **SANS Institute**: Updated training materials to reflect the research and de-emphasize rotation
- **ISO 27001/27002 (2022 revision)**: No longer specifically mandates periodic password changes, instead emphasizing risk-based approaches
- **PCI DSS 4.0**: While still referencing periodic changes, now allows alternative controls that demonstrate equivalent security

## Why People Create Weaker Passwords Under Rotation Policies

Understanding the psychology helps explain the research results. When forced to create a new password every 90 days, people face a cognitive problem: they need something they can remember, that meets complexity requirements, and that is different from their last password.

The path of least resistance is to make a minimal change. Research on [password psychology](/password-security/psychology-of-passwords/) confirms that users follow consistent, predictable strategies:

- **Incrementing numbers**: `Autumn2024!` becomes `Autumn2025!`
- **Rotating seasons or months**: `Winter2024$` becomes `Spring2024$`
- **Shifting characters**: `Pa$$word1` becomes `Pa$$word2`
- **Toggling capitalization**: `SecureLogin` becomes `sECURELOGIN`
- **Appending or prepending**: `MyPassword` becomes `MyPassword!` becomes `MyPassword!!`

These patterns are so well-documented that password cracking tools include transformation rules specifically designed to exploit them. An attacker who captures a hash from January can generate likely candidates for the April password in seconds.

The irony is inescapable: a policy designed to improve security systematically trains users to create passwords that are easier to guess.

## What to Do Instead

If forced rotation is out, what should replace it? The answer is a layered approach that addresses the actual threats passwords face.

### Change Passwords Only After a Known or Suspected Breach

The single most important policy change is this: stop rotating passwords on a schedule. Instead, require a password change only when there is evidence that the credential may have been compromised. This includes:

- Notification from a breach monitoring service
- Suspicious login activity on the account
- Malware detected on a device where the password was used
- A colleague's account in the same system has been compromised

PanicVault's built-in breach monitoring checks your stored credentials against known compromise databases, alerting you when a password change is actually warranted rather than on an arbitrary schedule.

### Use Strong, Unique Passwords for Every Account

When passwords are not being churned every 90 days, users and organizations can invest in doing it right once. A [strong, unique password](/password-security/strong-password-guide/) -- or better, a randomly generated one stored in a [password manager](/password-managers/) -- provides far more protection than a rotating series of predictable variations.

The key principles of [good password hygiene](/password-security/password-hygiene/) are straightforward:

- Generate random passwords of 16+ characters for each account
- Never reuse passwords across services -- the [dangers of password reuse](/password-security/password-reuse-dangers/) are well-documented
- Use a password manager to store and autofill credentials
- Reserve your memorization effort for your master passphrase

### Enable Multi-Factor Authentication

[Two-factor authentication](/two-factor-authentication/) (2FA) provides a fundamentally stronger defense than any password rotation policy ever could. Even if a password is compromised, a second factor -- a hardware key, authenticator app, or push notification -- blocks unauthorized access.

Organizations that implement 2FA across their systems effectively neutralize the threat model that password rotation was originally designed to address. The combination of a strong, stable password plus a second factor is superior to a weak, frequently changed password with no second factor.

### Screen Passwords Against Breach Databases

Rather than forcing changes on a timer, check passwords against databases of known compromised credentials at the time of creation and periodically thereafter. If a password appears in a breach, require a change immediately. If it does not, leave it alone.

NIST specifically recommends this approach. Services like Have I Been Pwned provide APIs for organizations to integrate breach checking directly into their authentication systems.

## When Rotation Still Makes Sense

Abandoning forced expiration does not mean passwords should never change. There are specific scenarios where rotation remains appropriate:

### Shared and Service Accounts

When multiple people share access to an account -- a social media login, an admin console, a vendor portal -- passwords should be rotated when any person with access leaves the organization or changes roles. The concern here is not password aging but access control: someone who should no longer have access still knows the credential.

For [business password policies](/business/password-policy/), managing shared accounts is one of the most challenging aspects of credential security. A password manager with sharing features can streamline this by allowing access to be revoked centrally.

### Privileged Access Accounts

Highly privileged accounts (root, domain admin, database admin) present a higher-risk target. Some organizations rotate these credentials more frequently or use privileged access management (PAM) systems that issue temporary, one-time-use credentials. This is a different problem from general user password expiration and involves different tools and processes.

### Post-Incident Response

After any security incident -- confirmed breach, suspected intrusion, insider threat investigation -- affected passwords should be changed immediately. This is event-driven rotation, not calendar-driven, and it aligns perfectly with current best practices.

## How to Transition Away from Forced Expiration

For organizations still enforcing 90-day rotation, the shift requires both a technical change and a communication strategy:

1. **Audit your current policy**: Document what your rotation interval is, which compliance frameworks you are subject to, and what compensating controls you have in place
2. **Implement breach checking**: Integrate a compromised-credential check into your authentication flow before removing rotation requirements
3. **Deploy multi-factor authentication**: Roll out 2FA to all users, starting with privileged accounts and expanding from there
4. **Strengthen password requirements**: Increase minimum length to 12-16 characters, allow passphrases, and drop arbitrary complexity rules
5. **Update the policy**: Remove calendar-based rotation and replace it with event-based triggers
6. **Communicate the change**: Explain to users why the old policy was counterproductive and what is expected of them now
7. **Monitor and adjust**: Track helpdesk call volume, password strength metrics, and account compromise rates to measure the impact

## Understanding Password Change Frequency

The question of [how often to change passwords](/password-security/password-change-frequency/) has a clear answer in 2026: only when there is a reason to. Calendar-driven rotation is a relic of a different computing era, kept alive by compliance inertia long after the evidence turned against it.

The organizations that have moved to event-driven password changes, strong unique credentials, and multi-factor authentication report lower helpdesk costs, stronger actual password quality, and equivalent or better security outcomes.

## Summary

The 90-day password expiration policy had a logical foundation in the 1980s when password cracking was slow and breach detection was nonexistent. That foundation crumbled under the weight of research showing that forced rotation produces predictable, weaker passwords while imposing significant cost and friction.

NIST, Microsoft, the UK NCSC, and virtually every modern security authority now recommends against mandatory password rotation for standard user accounts. The replacement strategy is straightforward:

- **Create strong, unique passwords** and do not change them on a schedule
- **Use a password manager** like PanicVault to generate and store credentials securely
- **Enable two-factor authentication** on every account that supports it
- **Change passwords immediately** when there is evidence of compromise
- **Reserve rotation** for shared accounts, privileged access, and incident response

The best password is not the one you changed last week. It is the one that was strong enough that it never needed changing in the first place.
