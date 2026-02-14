---
title: "What to Do Immediately After a Data Breach"
description: "Step-by-step action plan for the critical first 48 hours after learning your data has been exposed in a breach. Prioritized checklist to limit damage fast."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Data Breaches & Identity"
---

Learning that your personal information has been exposed in a data breach can trigger a wave of anxiety, but the actions you take in the first 48 hours determine how much damage the breach ultimately causes. This guide, part of our [Data Breaches & Identity Protection](/data-breaches/) resource center, provides a prioritized, step-by-step response plan you can follow immediately -- whether the breach exposed your email and password, your financial details, or your Social Security number.

## Assess What Was Exposed

Before you act, understand the scope. Not all breaches are equal, and the severity of your response should match the severity of the exposure.

### Tier 1: Email and Password

This is the most common type of breach exposure. An online service was hacked, and your email address and hashed (or in the worst case, plaintext) password were taken. The primary risk is [credential stuffing](/data-breaches/credential-stuffing/) -- attackers using that email-password combination to try logging into your other accounts.

**Urgency**: High, but manageable if you use unique passwords. If you reuse the breached password anywhere, it becomes critical.

### Tier 2: Financial Information

Credit card numbers, bank account details, or payment history were exposed. The risk is direct financial fraud -- unauthorized charges, wire transfers, or new accounts opened in your name.

**Urgency**: Critical. Contact your financial institutions immediately.

### Tier 3: Government-Issued Identifiers

Social Security number, driver's license number, passport number, or tax identification number. These are the keys to identity theft -- opening new credit lines, filing fraudulent tax returns, or obtaining medical services in your name.

**Urgency**: Maximum. Act within hours, not days.

### Tier 4: Medical Records

Health insurance information, medical history, or prescription data. Medical identity theft is among the hardest to detect and the most difficult to resolve.

**Urgency**: Maximum, with the added complexity that medical records cannot be "changed" the way a password can.

## The First-Hour Checklist

Work through this list in order. Each step builds on the previous one.

### 1. Change the Breached Password

Log into the compromised service and change your password immediately. Use a [password manager](/password-managers/) to generate a strong, random password of at least 16 characters. If you cannot log in -- if the attacker has already changed your password -- use the service's account recovery process.

If you have been reusing the breached password on other accounts, change it everywhere. This is why credential stuffing is so effective: 94% of passwords are reused or duplicated, meaning one breach can cascade across dozens of accounts. A password manager that generates unique credentials for every account eliminates this cascade entirely.

### 2. Enable Two-Factor Authentication

If the breached service supports [two-factor authentication](/two-factor-authentication/) and you had not yet enabled it, do so now. Use an authenticator app or hardware security key rather than SMS-based 2FA, which is vulnerable to SIM-swapping attacks. Enable 2FA on every account that supports it, starting with:

- Email (this is the master key to your other accounts via password resets)
- Banking and financial services
- Cloud storage (Google Drive, iCloud, Dropbox)
- Social media
- Your password manager (if it is cloud-based)

### 3. Check for Unauthorized Access

Review the breached account for signs that someone has already used your credentials:

- **Login history**: Most services show recent login activity, including IP addresses and locations. Look for logins you do not recognize.
- **Connected devices**: Remove any devices you do not own.
- **Account settings**: Check for changes to recovery email, phone number, or security questions. Attackers often change these to maintain access even after you change your password.
- **Forwarding rules**: In email accounts specifically, check for auto-forwarding rules that silently copy your incoming mail to another address. This is a common persistence technique.

### 4. Review Financial Statements

If financial data was exposed -- or even if you are unsure -- review recent statements from your bank accounts and credit cards. Look for charges you do not recognize, even small ones. Attackers often make small "test" charges before attempting larger fraudulent transactions.

Set up transaction alerts on all financial accounts if you have not already. Most banks and credit card issuers offer real-time notifications for any charge above a threshold you set. A $0 threshold means you are notified of every transaction.

### 5. Document Everything

Start a record of your response. This is important both for your own reference and for any future disputes, insurance claims, or law enforcement reports. Document:

- The date and time you learned about the breach
- The notification you received (save the email or letter)
- What data was reportedly exposed
- Every action you take in response, with dates and times
- Names and reference numbers from any customer service interactions
- Screenshots of unauthorized activity

## If Financial Information Was Exposed

Beyond the first-hour checklist, financial exposure requires additional immediate action.

### Contact Your Financial Institutions

Call your bank and credit card issuers directly -- use the phone number on your card or statement, not any number provided in the breach notification. Report the breach and ask about:

- Issuing new card numbers
- Placing fraud alerts on your accounts
- Reviewing recent transactions for fraud
- Temporarily increasing account monitoring

### Place a Fraud Alert

Contact one of the three major credit bureaus (Equifax, Experian, or TransUnion) to place an initial fraud alert on your credit file. The bureau you contact is required to notify the other two. An initial fraud alert lasts one year and requires creditors to verify your identity before opening new accounts.

### Consider a Credit Freeze

A [credit freeze](/data-breaches/freeze-credit/) is stronger than a fraud alert. It prevents anyone -- including you -- from opening new credit accounts until you lift the freeze. If your Social Security number was exposed, a freeze should be your default action. Unlike a fraud alert, you must contact each bureau individually to place and lift freezes.

## If Government IDs Were Exposed

Social Security number exposure is the most serious category because SSNs cannot be changed in most circumstances.

### Freeze Your Credit at All Three Bureaus

This is no longer optional -- it is essential. See our detailed guide to [freezing your credit after a data breach](/data-breaches/freeze-credit/).

### File an Identity Theft Report

If you see any evidence that your identity is being misused, file a report at IdentityTheft.gov (the FTC's identity theft resource). This generates an official Identity Theft Report that gives you specific legal rights, including the ability to:

- Block fraudulent information from appearing on your credit reports
- Prevent companies from collecting debts that resulted from identity theft
- Place an extended fraud alert lasting seven years

### Monitor for Tax Fraud

If the breach occurred between October and April (tax season), be especially vigilant for tax-related identity theft. File your tax return as early as possible -- if a fraudulent return is filed under your SSN first, your legitimate return will be rejected. Consider filing Form 14039 (Identity Theft Affidavit) with the IRS.

### Request a Credit Report

Pull your credit reports from all three bureaus at AnnualCreditReport.com. Review them for accounts you did not open, inquiries you did not authorize, and addresses where you have never lived. Dispute any inaccuracies immediately.

## The Password Manager Question

A data breach often triggers a broader reassessment of security practices. If you are not using a password manager, a breach is compelling evidence that you need one -- managing unique passwords for 250+ accounts is not feasible without one. If you are already using a password manager, verify that the breached password was not reused elsewhere. Your manager's audit feature (sometimes called a "security checkup" or "vault health report") can identify reused passwords across all your stored credentials.

If your password manager itself was breached -- a scenario with its own specific response plan covered in [What to Do If Your Password Manager Is Breached](/data-breaches/password-manager-breached/) -- the calculus changes significantly. The [LastPass breach](/data-breaches/lastpass-breach-lessons/) demonstrated that cloud-based password managers create a centralized target: breach the vendor, and you potentially get copies of every user's encrypted vault.

Password managers that store your encrypted database locally -- such as those using the [KeePass format](/keepass/) like PanicVault -- avoid this specific risk. Your vault file lives on your devices and your cloud storage (such as iCloud Drive), not on the password manager vendor's servers. There is no central repository of user vaults to breach.

## Long-Term Actions

After the immediate crisis, shift to building defenses that limit the damage of future breaches.

### Audit Your Accounts

Use this breach as motivation to do a comprehensive security audit. Review every account in your password manager for:

- Reused passwords (change them all to unique ones)
- Missing two-factor authentication (enable it everywhere possible)
- Outdated accounts you no longer use (close them or at minimum, change the password to something unique)
- Accounts using the breached email as their login

### Set Up Ongoing Monitoring

Register your email addresses with [Have I Been Pwned](/data-breaches/have-i-been-pwned/) to receive automatic notifications when they appear in future breaches. Consider whether [dark web monitoring](/data-breaches/dark-web-monitoring/) is appropriate for your risk level.

### Review Breach Notification Rights

Know your rights under your state's data breach notification law and, if applicable, regulations like GDPR or CCPA. Companies that suffered the breach may owe you free credit monitoring, identity theft protection services, or other remediation. The breach notification letter itself is a legal document worth reading carefully -- our guide to [understanding notification letters](/data-breaches/notification-letters/) explains what to look for.

## When to Seek Professional Help

Consider engaging a professional identity theft recovery service or attorney if:

- You discover accounts opened in your name that you did not authorize
- You are denied credit, employment, or housing because of identity theft damage
- The breach exposed medical records and you suspect medical identity theft
- You are spending more than 10-15 hours per week on recovery and it is affecting your work or mental health
- The recovery timeline has extended beyond six months without resolution

The [identity theft recovery process](/data-breaches/identity-theft-recovery/) can take anywhere from a few weeks to several years depending on the severity. Understanding what to expect -- including realistic [recovery timelines](/data-breaches/recovery-timeline/) -- helps you pace yourself and make informed decisions about when self-management is sufficient and when professional help is worth the cost.

## Related Articles

- [How to Check If Your Email Has Been Compromised](/data-breaches/check-email-compromised/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [How to Freeze Your Credit After a Data Breach](/data-breaches/freeze-credit/)
- [Identity Theft Recovery: Step-by-Step Guide](/data-breaches/identity-theft-recovery/)
- [The LastPass Breach: Lessons for Password Security](/data-breaches/lastpass-breach-lessons/)
