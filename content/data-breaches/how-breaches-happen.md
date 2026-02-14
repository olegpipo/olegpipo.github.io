---
title: "How Data Breaches Happen: Anatomy of an Incident"
description: "Technical breakdown of how data breaches happen -- common attack vectors, real-world examples, and what each method means for your personal data security."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Data Breaches & Identity"
---

Data breaches do not happen in a vacuum. Every breach follows a chain of events -- an initial compromise, lateral movement, data discovery, and exfiltration -- that can take anywhere from minutes to months. Understanding these patterns is not just academic curiosity. When you know how breaches happen, you can assess your own exposure more accurately, evaluate the security claims of services you use, and make informed decisions about which defenses actually matter. This article, part of our [Data Breaches & Identity Protection](/data-breaches/) resource center, breaks down the most common attack vectors with real-world examples.

## The Anatomy of a Breach

Most data breaches follow a recognizable lifecycle:

### 1. Initial Access

The attacker gains a foothold in the target's systems. This is the entry point -- the first door that opens.

### 2. Persistence

Once inside, the attacker establishes mechanisms to maintain access even if the initial vulnerability is patched or credentials are changed.

### 3. Lateral Movement

The attacker moves from the initially compromised system to other systems within the network, escalating privileges and seeking access to valuable data.

### 4. Data Discovery

The attacker identifies where the target's most valuable data is stored -- customer databases, credential stores, financial records, intellectual property.

### 5. Exfiltration

The attacker copies the data out of the network, often compressing and encrypting it to avoid detection by data loss prevention tools.

### 6. Monetization or Publication

Stolen data is sold on dark web marketplaces, used for [credential stuffing](/data-breaches/credential-stuffing/), leveraged for extortion (ransomware), or published for ideological purposes.

The time between step 1 and step 6 averages approximately 277 days for detection and containment, according to IBM's Cost of a Data Breach Report. During this window, the attacker operates undetected.

## Attack Vector 1: Phishing and Social Engineering

[Phishing](/phishing/) remains the most common initial access vector for data breaches. It succeeds because it targets people rather than technology, and people are reliably fallible under pressure.

### How It Works

An attacker sends an email, text message, or voice call designed to trick the recipient into:

- **Clicking a malicious link** that installs malware or leads to a fake login page
- **Opening a malicious attachment** that executes code on the recipient's device
- **Providing credentials** directly in response to a convincing pretext

Spear phishing targets specific individuals with personalized messages. Business email compromise (BEC) impersonates executives or trusted partners to authorize wire transfers or data access. Both are devastatingly effective.

### Real-World Example

The 2020 Twitter breach started with phone-based social engineering targeting Twitter employees. The attackers convinced support staff to reset credentials, gaining access to internal admin tools. They then took over high-profile accounts (Barack Obama, Elon Musk, Apple) to run a cryptocurrency scam. The technical sophistication was minimal -- the social engineering was the entire attack.

### What This Means for You

You cannot control whether a company you do business with falls to a phishing attack. But you can limit the blast radius:

- Use a unique password for every account so that [credential stuffing](/data-breaches/credential-stuffing/) from one breach cannot cascade to others
- Enable [two-factor authentication](/two-factor-authentication/) so that a stolen password alone is insufficient for access
- Be skeptical of unexpected emails requesting action, even from known contacts

## Attack Vector 2: Credential Compromise

Stolen, leaked, or weak credentials are the second most common breach vector. This includes:

- **Brute force attacks**: Trying common passwords against login pages
- **Credential stuffing**: Using email-password pairs stolen from other breaches to log into unrelated services. With 94% of passwords reused or duplicated, this works at alarming scale.
- **Purchased credentials**: Buying login credentials from dark web marketplaces

### Real-World Example

The 2024 Snowflake incidents illustrated credential compromise at scale. Attackers used credentials stolen from earlier breaches to access Snowflake cloud data warehouse accounts that lacked multi-factor authentication. The result was a cascade of breaches affecting major companies -- Ticketmaster, AT&T, Santander, and others -- through a single platform. The root cause was not a vulnerability in Snowflake's software but compromised customer credentials combined with the absence of mandatory MFA.

### What This Means for You

Your credentials are only as secure as the weakest service where you use them. If you reuse a password and any of those services is breached, every account sharing that password is compromised. A [password manager](/password-managers/) that generates unique passwords for every account is the definitive defense against credential compromise as a breach vector.

## Attack Vector 3: Software Vulnerabilities

Unpatched software vulnerabilities give attackers direct technical access to systems. These include:

- **Known vulnerabilities**: Published security flaws (CVEs) that have patches available but have not been applied
- **Zero-day vulnerabilities**: Previously unknown flaws that have no patch at the time of exploitation
- **Misconfigurations**: Default settings, exposed admin panels, and improperly secured APIs

### Real-World Example

The 2023 MOVEit breach exploited a zero-day SQL injection vulnerability in Progress Software's MOVEit Transfer file-sharing application. The Cl0p ransomware group used the vulnerability to access MOVEit servers worldwide, stealing data from over 2,600 organizations and affecting more than 77 million individuals. The breach was notable for its scope -- because MOVEit was used as a third-party tool by thousands of organizations, a single vulnerability created a mass casualty event.

### What This Means for You

Keep your software updated. Enable automatic updates where possible. When a critical security patch is released, apply it promptly. For the services you use, you are dependent on their patching practices -- a risk factor you cannot directly control but should be aware of when choosing which services to trust with your data.

## Attack Vector 4: Third-Party and Supply Chain Attacks

Organizations increasingly rely on third-party vendors, libraries, and services. Compromising a trusted third party can provide access to all of that party's customers simultaneously.

### Real-World Example

The [LastPass breach](/data-breaches/lastpass-breach-lessons/) followed a supply chain pattern. Attackers first compromised LastPass's development environment (August 2022), then used stolen credentials and keys to access their cloud storage environment (November 2022), ultimately obtaining encrypted vault data for 33 million users. The attack on the production environment was enabled by compromising a personal computer belonging to a DevOps engineer -- a third-party vector (the employee's personal device) leading to access to production infrastructure.

### What This Means for You

The security of any service is only as strong as its supply chain. When evaluating services -- particularly those that store sensitive data like [password managers](/password-managers/) -- consider:

- How many third parties have access to your data?
- How much of the infrastructure is vendor-controlled?
- What happens to your data if the vendor's supply chain is compromised?

Services that minimize third-party dependencies and keep your data under your control reduce supply chain risk. The [KeePass format](/keepass/) exemplifies this: your encrypted database file is under your control, and the encryption happens entirely on your device. An app like PanicVault stores your vault on your Apple devices or iCloud Drive -- there are no PanicVault servers in the supply chain that could be compromised.

## Attack Vector 5: Insider Threats

Not all breaches come from outside the organization. Insiders -- employees, contractors, or business partners with legitimate access -- can steal data intentionally or expose it accidentally.

### Intentional Insider Threats

Disgruntled employees, financially motivated insiders, or individuals recruited by external attackers can exfiltrate data they have legitimate access to. This is particularly difficult to detect because the access patterns may look normal.

### Accidental Insider Threats

Misconfigured cloud storage buckets, accidentally published databases, emails sent to the wrong recipient, and lost devices account for a significant percentage of data exposures. These are breaches caused by human error rather than malicious intent, but the impact on affected individuals is identical.

### Real-World Example

The 2019 Capital One breach was caused by a former AWS employee who exploited a misconfigured web application firewall to access Capital One's cloud storage, exposing personal information of over 100 million customers. The breach combined elements of insider knowledge (familiarity with AWS infrastructure) with a technical misconfiguration.

### What This Means for You

You cannot control insider threats at organizations that hold your data. What you can control is the scope of what any single organization holds. Minimize the sensitive information you share with any service. Use guest checkout when possible. Do not store information that is not required.

## Attack Vector 6: Misconfigured Cloud Storage

The migration to cloud computing has created a new category of breach: data exposed through misconfigured cloud storage. Publicly accessible S3 buckets, unsecured Azure Blob Storage containers, and exposed Elasticsearch instances have been responsible for some of the largest data exposures in history.

### How It Happens

Cloud storage defaults and permission models are complex. A single misconfigured permission can expose millions of records to anyone who knows -- or can guess -- the URL. Automated scanning tools continuously probe for open cloud storage, meaning misconfigurations are typically discovered by both security researchers and attackers within hours of being created.

### What This Means for You

When a service you use stores your data in the cloud, you are trusting their infrastructure team to configure storage correctly. Major cloud providers (AWS, Azure, Google Cloud) have implemented increasingly aggressive defaults and warnings to prevent misconfigurations, but human error persists. Breaches from misconfigured cloud storage tend to expose large volumes of data with no encryption -- everything is in plaintext because the storage was meant to be private.

## Attack Vector 7: Ransomware with Data Exfiltration

Modern ransomware attacks have evolved from simple encryption-for-ransom to "double extortion" -- encrypting systems AND stealing data. If the victim does not pay the ransom, the attackers publish the stolen data.

This evolution means that ransomware attacks are now data breaches by default. Even if the organization recovers its systems from backups without paying the ransom, the stolen data is already in attacker hands.

### What This Means for You

Ransomware-driven breaches tend to expose whatever data the attacker could access during their time in the network, which often includes customer databases, employee records, and financial information. The [notification process](/data-breaches/notification-letters/) for ransomware-driven breaches can be particularly slow because the organization is simultaneously dealing with operational recovery.

## Reducing Your Exposure

You cannot prevent breaches at organizations that hold your data. But you can limit the damage when breaches occur:

1. **Use unique passwords everywhere**: A [password manager](/password-managers/) makes this practical. When one service is breached, the damage stops there.
2. **Enable two-factor authentication**: [2FA](/two-factor-authentication/) ensures that stolen credentials alone cannot access your accounts.
3. **Minimize data sharing**: Only provide the information that is strictly required. Use guest checkout. Skip optional fields.
4. **Monitor for breaches**: Register with [Have I Been Pwned](/data-breaches/have-i-been-pwned/) and enable your password manager's breach monitoring.
5. **Freeze your credit**: A [credit freeze](/data-breaches/freeze-credit/) prevents identity thieves from leveraging stolen personal information.
6. **Choose services carefully**: Evaluate the security practices and architecture of services you trust with sensitive data. Services with minimal data collection, zero-knowledge encryption, and local-first storage inherently limit breach exposure.

## Related Articles

- [The Biggest Data Breaches of 2025-2026](/data-breaches/biggest-breaches/)
- [What Information Hackers Steal in a Breach](/data-breaches/what-hackers-steal/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [The LastPass Breach: Lessons for Password Security](/data-breaches/lastpass-breach-lessons/)
- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
