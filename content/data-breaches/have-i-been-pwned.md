---
title: "Have I Been Pwned? Using Free Breach-Checking Tools"
description: "Complete guide to Have I Been Pwned and other free breach-checking tools -- how to check your exposure, interpret results, and set up ongoing monitoring."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Data Breaches & Identity"
---

When a [data breach](/data-breaches/) exposes millions of records, the affected individuals need a way to find out whether they are among the victims. Have I Been Pwned (HIBP) has become the definitive answer to that question. Created in 2013 by Australian security researcher Troy Hunt, the free service aggregates data from known breaches and lets anyone search by email address to see if their credentials have been exposed. But HIBP is not the only tool available, and knowing how to use these services effectively -- including understanding their limitations -- is an essential part of your security practice.

## What Is Have I Been Pwned?

HIBP is a free, independently operated website (haveibeenpwned.com) that catalogs data breaches. As of early 2026, the service contains records from over 800 breached websites representing more than 14 billion compromised accounts. When a breach is publicly disclosed or breach data is discovered being traded on underground forums, Troy Hunt works to verify the data and load it into HIBP's database.

The service answers a simple question: "Has my email address appeared in a known data breach?" But the way it answers that question -- and the additional tools it provides -- makes it far more useful than a simple yes-or-no lookup.

### How HIBP Gets Its Data

Breach data reaches HIBP through several channels:

- **Public disclosures**: When companies report breaches, the data often eventually becomes publicly available.
- **Security researchers**: Researchers who discover breach data in the wild share it with Hunt for inclusion.
- **Law enforcement**: Agencies like the FBI have collaborated with HIBP to load seized breach databases, such as data from the Emotet botnet takedown.
- **Underground marketplaces**: Data being sold or freely shared on dark web forums is obtained and verified.

Hunt verifies the authenticity of breach data before loading it into HIBP. This verification process is critical -- false breach reports would undermine the service's trustworthiness. He has documented his verification methodology extensively.

## Using HIBP: A Complete Walkthrough

### Email Search

Navigate to haveibeenpwned.com and enter your email address. The results page shows every known breach that includes that email address.

Each breach listing provides:

- **The name of the breached service**: Which company or website was compromised
- **The breach date**: When the breach occurred (which may be months or years before it was discovered)
- **The date it was added to HIBP**: When the data was loaded into the database
- **The number of compromised accounts**: The total scope of the breach
- **Compromised data types**: Exactly what categories of information were exposed -- email addresses, passwords, usernames, IP addresses, phone numbers, dates of birth, physical addresses, or other fields

Pay close attention to the "compromised data" field. A breach that exposed only email addresses is far less severe than one that exposed passwords, security questions, or financial information.

### Pwned Passwords

The Pwned Passwords tool (haveibeenpwned.com/Passwords) lets you check whether a specific password appears in any known breach database. The database contains over 900 million unique passwords collected from breaches.

**Security architecture**: HIBP uses a privacy-preserving k-anonymity model for password checks. Your password is hashed using SHA-1 on your device. Only the first five characters of the hash are sent to the server. The server returns all hash suffixes that match those five characters, and the comparison happens locally in your browser. Your full password never leaves your device.

This is safe to use, and you should check every password you currently use. If a password appears in the Pwned Passwords database, it is actively used in credential stuffing dictionaries and should be changed immediately.

### API Access

HIBP offers a free API for individual use and a commercial API for organizations. The API enables:

- **Automated breach checks**: Integrate breach checking into your own applications or scripts
- **Password checking at scale**: Organizations can check employee passwords against the Pwned Passwords database during password changes
- **Notification subscriptions**: Programmatically subscribe email addresses for breach notifications

Many [password managers](/password-managers/) integrate with the HIBP API to automatically flag compromised passwords in your vault. This is one of the most practical applications of the service -- passive monitoring that alerts you without requiring manual checks.

### Domain Search

If you own a domain, HIBP's domain search lets you see all breaches affecting any email address at that domain. This is primarily useful for businesses and organizations monitoring their employees' exposure, but it also works for personal domains.

## Other Free Breach-Checking Tools

HIBP is the most comprehensive service, but several alternatives offer additional capabilities or different perspectives on breach data.

### Mozilla Monitor

Mozilla Monitor (monitor.mozilla.org) uses HIBP's database but wraps it in a more guided experience. It integrates with your Firefox account to provide:

- Automatic monitoring of your email addresses
- Step-by-step resolution guidance when breaches are found
- Prioritized action items based on the severity of exposed data
- Integration with the Firefox browser for real-time alerts

Mozilla Monitor is particularly useful for less technical users who want actionable guidance alongside breach data.

### Google Password Checkup

Built into Google Chrome and Google accounts, Password Checkup automatically scans your saved passwords against Google's own database of known compromised credentials. If you use Chrome as your browser and Google as your password store, this monitoring happens automatically.

The Google Security Checkup (myaccount.google.com/security-checkup) provides a broader assessment that includes breach checks alongside other security settings review.

### Apple Security Recommendations

Apple's built-in password monitoring (available in iOS Settings > Passwords > Security Recommendations and in macOS System Settings > Passwords) checks your saved passwords against known breach databases. It also flags reused passwords and passwords that are too simple. If you use the Apple Passwords app or iCloud Keychain, this monitoring is automatic and persistent.

Password managers like PanicVault that integrate with [Apple's credential provider framework](/apple/credential-provider-extensions/) can also surface these security recommendations for passwords stored in your [KeePass](/keepass/) database.

### Dehashed and Intelligence X

These are more advanced tools aimed at security professionals and investigators. They index a broader range of data sources, including paste sites, dark web forums, and data dumps. They are less user-friendly than HIBP but can surface data that HIBP has not yet cataloged.

## Interpreting Results: What to Do

### No Breaches Found

Good news, but do not assume permanent safety. This means your email does not appear in currently cataloged breaches. New breaches are discovered regularly, and some are never publicly disclosed.

**Action**: Set up HIBP email notifications (see below) and continue practicing good password hygiene with a [password manager](/password-managers/) and [two-factor authentication](/two-factor-authentication/).

### Breaches Found with Password Data

This is the most actionable result. If a breach exposed your password -- whether hashed or plaintext -- that password is compromised everywhere you use it.

**Immediate actions**:
1. Change the password at the breached service
2. Change it at every other service where you used the same password
3. Enable two-factor authentication at all affected services
4. Check for unauthorized access at [what to do after a breach](/data-breaches/what-to-do-after-breach/)

### Breaches Found without Password Data

If only your email, username, or other non-credential data was exposed, the primary risk is phishing and social engineering rather than direct account compromise.

**Actions**:
1. Be vigilant about [phishing](/phishing/) emails referencing the breached service
2. Review the breached account's security settings
3. Consider whether other data types exposed (phone numbers, addresses) increase your social engineering risk

### Paste Appearances

HIBP also tracks "pastes" -- instances where email addresses appear in text pasted to public paste sites (like Pastebin). Pastes often contain preliminary breach data or credential lists being shared among attackers. A paste appearance may indicate a breach that has not yet been formally cataloged.

**Action**: Treat paste appearances with the same seriousness as breach appearances. Check and change your passwords for services associated with the exposed email.

## Setting Up Ongoing Monitoring

### HIBP Email Notifications

Visit haveibeenpwned.com/NotifyMe and enter your email address. You will receive a verification email -- click the link to confirm. From that point on, you will be automatically notified whenever your email appears in a newly loaded breach.

This is free, requires no account creation, and is one of the highest-value security measures available for zero ongoing effort. Register every email address you use.

### Organizational Monitoring

For businesses, HIBP's domain search and API enable monitoring of all email addresses under your domain. This can be integrated into security operations to provide early warning when employee credentials appear in breaches.

### Browser-Based Monitoring

Firefox Monitor and Chrome's Password Checkup provide passive monitoring within your browser. If you use either browser as your primary, enabling this feature means breach checks happen continuously in the background as you browse and log into services.

## Limitations to Understand

No breach-checking service is perfect, and understanding the limitations helps you use these tools appropriately.

### Data Lag

There is always a delay between a breach occurring and the data appearing in HIBP or other services. Some breaches are not discovered for months. Even after discovery, data may take weeks to be verified and loaded. Your email could be compromised right now in a breach that has not yet been publicly reported.

### Incomplete Coverage

HIBP does not have data from every breach that has ever occurred. Private breaches, nation-state operations, and data that is tightly held among criminal groups may never appear in any public breach-checking service.

### False Sense of Security

A clean result can lead to complacency. "I checked and I'm fine" is true only for the breaches that are currently known. The correct interpretation is "I have no known exposure as of today." Continue practicing security fundamentals regardless of your results.

### Not All Data Is Created Equal

Breach data ages. A password exposed in a 2019 breach and changed that same year is less concerning than a password exposed last month. But your email address and other personal details from old breaches remain useful to attackers for phishing and social engineering indefinitely.

## Connecting Breach Checks to Password Management

The most practical way to use breach-checking tools is in conjunction with a password manager. A manager that integrates with HIBP's Pwned Passwords database can automatically flag compromised passwords across your entire vault, turning what would be a manual, password-by-password check into an automatic scan.

The [KeePass ecosystem](/keepass/) supports HIBP integration in several clients. KeePassXC includes a built-in HIBP check in its database tools. PanicVault, as a native Apple app, works within the [Apple ecosystem's](/apple/) security monitoring infrastructure while storing your credentials in the portable KeePass format -- meaning your vault file remains entirely under your control, stored locally or on iCloud Drive rather than on a vendor's cloud servers. This architecture matters because it means that even if PanicVault were to experience a security incident, there is no centralized database of user vaults to be exposed -- a critical distinction highlighted by the [LastPass breach](/data-breaches/lastpass-breach-lessons/).

## Related Articles

- [How to Check If Your Email Has Been Compromised](/data-breaches/check-email-compromised/)
- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [Dark Web Monitoring: What It Is and Do You Need It?](/data-breaches/dark-web-monitoring/)
- [How to Set Up Identity Theft Monitoring](/data-breaches/monitoring-alerts/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
