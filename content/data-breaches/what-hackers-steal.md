---
title: "What Information Hackers Steal in a Breach"
description: "Understanding what data hackers target in breaches -- from emails and passwords to SSNs and medical records -- and what they do with each type once stolen."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Data Breaches & Identity"
---

Not all data breaches are equal. A breach that exposes your email address and a hashed password is a fundamentally different event from one that exposes your Social Security number, medical history, or biometric data. The type of information stolen determines the severity of the breach, the urgency of your response, and the long-term risk you face. This guide, part of our [Data Breaches & Identity Protection](/data-breaches/) resource center, catalogs the categories of data that hackers target, explains what attackers do with each type, and helps you assess your actual risk when you receive a [breach notification](/data-breaches/notification-letters/).

## The Hierarchy of Stolen Data

Stolen data has a well-defined value hierarchy in criminal markets. Understanding this hierarchy helps you prioritize your response when a breach occurs.

### Tier 1: Email Addresses

**Dark web value**: $0.50-$5 per record

Email addresses are the most commonly exposed data type in breaches. On their own, they are the least damaging -- but they are never truly "on their own." An email address is the starting point for:

- **Phishing attacks**: Knowing your email and that you have an account at a specific service enables targeted [phishing](/phishing/) campaigns.
- **Spam**: Mass-market phishing, scam, and malware distribution.
- **Account enumeration**: Attackers can test whether your email is registered at other services, building a profile of your online presence.
- **Social engineering**: Your email address may reveal your real name, employer, or other details useful for crafting convincing pretext scenarios.

**Your response**: Be vigilant about phishing emails. No immediate action required beyond heightened awareness, but use this as a prompt to check whether you have reused passwords across services.

### Tier 2: Usernames and Passwords

**Dark web value**: $1-$15 per credential pair

Credentials are the bread and butter of data breaches. Twenty-two percent of all breaches involve [credential stuffing](/data-breaches/credential-stuffing/) -- the automated reuse of stolen credentials at other services. With 94% of passwords reused or duplicated, a single stolen credential can unlock access to many accounts.

**How passwords are typically exposed**:

- **Plaintext**: The worst case. The service stored passwords without any hashing or encryption. The passwords are immediately usable.
- **Hashed without salt**: Passwords were hashed but not salted, meaning precomputed rainbow tables can be used to reverse the hashes quickly.
- **Hashed with salt (weak algorithm)**: Passwords were hashed with a salt using an outdated algorithm like MD5 or SHA-1. These can be cracked with GPU hardware.
- **Hashed with salt (strong algorithm)**: Passwords were hashed using bcrypt, scrypt, or Argon2. These are computationally expensive to crack, protecting most passwords -- though weak passwords (short, common, predictable) will still fall.

**What attackers do**: Run the credentials through automated tools that attempt to log in at hundreds of popular services: email providers, banks, social media, cloud storage, cryptocurrency exchanges. Successful logins are sold or used directly.

**Your response**: Change the breached password immediately, and change it at every other service where you used it. This is the scenario where a [password manager](/password-managers/) proves its value -- if every password is unique, a credential breach at one service cannot cascade to others.

### Tier 3: Phone Numbers

**Dark web value**: $5-$20 per record (higher when paired with other data)

Phone numbers are increasingly valuable because they are used for SMS-based [two-factor authentication](/two-factor-authentication/). An attacker with your phone number, email, and password may be able to:

- **SIM-swap**: Convince your carrier to transfer your phone number to their SIM card, intercepting any SMS messages -- including 2FA codes.
- **Vishing**: Call you with a convincing pretext, impersonating your bank, the IRS, or tech support.
- **Smishing**: Send text message phishing attacks.

**Your response**: Set up a PIN or passcode with your mobile carrier to prevent unauthorized SIM swaps. Switch from SMS-based 2FA to authenticator apps or hardware security keys for critical accounts.

### Tier 4: Physical Addresses and Dates of Birth

**Dark web value**: $10-$40 per record (as part of a "fullz" package)

Physical addresses and dates of birth are identity verification data. They do not enable direct account access, but they are used in:

- **Identity verification bypass**: Many financial institutions use address and date of birth as verification questions. An attacker with these details can pass identity checks over the phone.
- **Synthetic identity creation**: Combining real personal details with fabricated information to create new identities for fraud.
- **Targeted mail fraud**: Opening new financial accounts with your identity and routing correspondence to an address the attacker controls.

**Your response**: [Freeze your credit](/data-breaches/freeze-credit/) to prevent new accounts from being opened. Monitor your credit reports for unfamiliar inquiries or accounts.

### Tier 5: Social Security Numbers

**Dark web value**: $30-$100 per record

A Social Security number is the master key to financial identity in the United States. With a SSN and supporting personal details, an attacker can:

- **Open new credit accounts**: Credit cards, personal loans, auto loans, mortgages
- **File fraudulent tax returns**: Claiming your tax refund before you file
- **Apply for government benefits**: Unemployment, Social Security benefits, Medicare
- **Obtain employment**: Working under your SSN, creating tax complications
- **Create synthetic identities**: Combining your SSN with other fabricated details

SSNs cannot be changed in most circumstances, making their exposure a permanent risk factor.

**Your response**: [Freeze your credit immediately](/data-breaches/freeze-credit/) at all three bureaus plus ChexSystems and NCTUE. File an IRS Identity Protection PIN request. Consider filing an FTC Identity Theft Report at IdentityTheft.gov. Set up comprehensive [identity theft monitoring](/data-breaches/monitoring-alerts/).

### Tier 6: Financial Account Numbers

**Dark web value**: $50-$200 per account (credit cards); $200-$1,000+ per account (bank accounts)

Credit card numbers, bank account and routing numbers, and other financial account data enable direct financial theft:

- **Unauthorized purchases**: Using stolen credit card data for online shopping
- **Wire transfers**: Initiating unauthorized bank transfers
- **ACH fraud**: Setting up unauthorized debit transactions against your bank account
- **Account takeover**: Using account details to pass verification and take control of the account

**Your response**: Contact your financial institutions immediately. Request new account numbers. Review recent transactions. File fraud claims for any unauthorized activity.

### Tier 7: Medical Records and Health Insurance Information

**Dark web value**: $250-$1,000+ per record

Medical records are among the most valuable stolen data types, and medical identity theft is among the hardest to recover from:

- **Insurance fraud**: Obtaining medical care, prescriptions, or medical devices under your insurance
- **Prescription fraud**: Using your insurance to obtain controlled substances
- **Medical records contamination**: Incorrect information in your medical file that could affect your future care
- **Billing fraud**: Filing false insurance claims using your identity

**Your response**: Contact your health insurance provider. Request an accounting of all claims filed under your insurance. Review your medical records for treatments you did not receive. See the medical identity theft section in our [identity theft recovery guide](/data-breaches/identity-theft-recovery/).

### Tier 8: Biometric Data

**Dark web value**: Not widely traded yet, but growing in value

Fingerprints, facial recognition data, voiceprints, and other biometric identifiers present a unique problem: they cannot be changed. A compromised password can be replaced. A compromised fingerprint is permanent.

Currently, biometric data exposure is most concerning when it enables:

- **Biometric authentication bypass**: Accessing systems that use biometric login
- **Deepfake creation**: Using facial data to create convincing deepfake videos or voice clones for social engineering

**Your response**: If biometric data is exposed, disable biometric authentication on affected accounts where possible, or add additional authentication factors. Monitor for account access using compromised biometrics.

## How Stolen Data Is Used

### Credential Stuffing

The most immediate and automated use of stolen credentials. Bots attempt to log in to hundreds of services using stolen email-password pairs. Because 94% of passwords are reused, this is devastatingly effective. Our [credential stuffing guide](/data-breaches/credential-stuffing/) explains the mechanics in detail.

### Identity Theft

Stolen personal details -- SSN, date of birth, address, financial information -- are assembled into "fullz" packages and used to open new accounts, file fraudulent tax returns, or obtain medical care. The [identity theft recovery process](/data-breaches/identity-theft-recovery/) can take [months to years](/data-breaches/recovery-timeline/).

### Targeted Phishing and Social Engineering

Detailed personal information makes [phishing](/phishing/) attacks far more convincing. An attacker who knows your bank, your employer, your recent purchases, and your physical address can craft messages that are nearly indistinguishable from legitimate communications.

### Account Takeover

With sufficient personal information, attackers can pass identity verification at banks, telcos, and other institutions -- resetting passwords, changing contact information, and taking full control of accounts.

### Dark Web Trading

Stolen data is sold on underground marketplaces, often in bulk. Prices depend on the freshness, completeness, and type of data. Complete identity packages (fullz) command the highest prices. Old data that has been widely circulated sells for less but remains useful.

## Protecting the Most Sensitive Data

The hierarchy of stolen data maps directly to a hierarchy of protective measures:

| Data Type | Primary Defense |
|---|---|
| Passwords | Unique passwords via a [password manager](/password-managers/) |
| Email + Password | Password manager + [2FA](/two-factor-authentication/) |
| Phone numbers | Carrier PIN + authenticator apps instead of SMS |
| SSN + Personal details | [Credit freeze](/data-breaches/freeze-credit/) + monitoring |
| Financial accounts | Transaction alerts + rapid response |
| Medical records | Insurance monitoring + records review |
| Biometric data | Multi-factor authentication beyond biometrics |

For password storage specifically, the architecture of your password manager determines how much data is at risk if the manager itself is breached. Cloud-based managers store every user's encrypted vault on their servers. The [LastPass breach](/data-breaches/lastpass-breach-lessons/) exposed 33 million encrypted vaults simultaneously. Managers using the [KeePass format](/keepass/), like PanicVault, store your encrypted database locally on your devices or iCloud Drive -- no centralized server of vaults to target. Your credential data's exposure is limited to the security of your own devices and your own cloud storage.

## Related Articles

- [How Data Breaches Happen: Anatomy of an Incident](/data-breaches/how-breaches-happen/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [Data Breach Notification Letters: How to Read Them](/data-breaches/notification-letters/)
- [The Biggest Data Breaches of 2025-2026](/data-breaches/biggest-breaches/)
