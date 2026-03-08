---
title: "23andMe Data Breach: What to Know"
description: "Analysis of the 2023 23andMe breach that exposed genetic data for 6.9 million users, the bankruptcy that followed, and what it means for DNA privacy."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Data Breaches & Identity"
faq:
  - question: "What data was stolen in the 23andMe breach?"
    answer: "Attackers accessed profile information for approximately 6.9 million users, including names, birth years, ancestry reports, and DNA Relatives matches. For about 1.4 million users, Family Tree profile data was also exposed. The underlying raw genetic data (DNA sequencing files) was not directly accessed in the breach."
  - question: "How did the 23andMe breach happen?"
    answer: "Attackers used credential stuffing -- testing username and password combinations stolen from other breaches -- to access approximately 14,000 user accounts. They then exploited the DNA Relatives feature, which shares data between opted-in users, to scrape profile information for 6.9 million connected accounts."
  - question: "Can I change my DNA after the 23andMe breach?"
    answer: "No. Unlike a password or credit card number, your genetic information is permanent and immutable. This makes genetic data breaches uniquely concerning -- the exposed information can never be rotated, reset, or revoked."
  - question: "What happened to 23andMe after the breach?"
    answer: "23andMe filed for Chapter 11 bankruptcy in March 2024, raising critical questions about who would gain custody of the genetic data of its approximately 15 million users. Privacy advocates urged users to delete their data before an acquisition could transfer it to new ownership."
  - question: "Should I delete my 23andMe data?"
    answer: "Many privacy experts recommend deleting your 23andMe data, especially following the bankruptcy filing. You can request deletion of your account and genetic data through the 23andMe settings. Be aware that data already exposed in the breach cannot be recalled."
---

The 2023 23andMe data breach stands apart from other security incidents for a reason that strikes at something deeply personal: the exposed data included genetic information -- the biological blueprint that defines who you are, your ancestry, and your predisposition to certain health conditions. Unlike a stolen password or credit card number, your DNA cannot be changed. The breach, which affected 6.9 million users, was followed by 23andMe's bankruptcy filing, raising urgent questions about the custody and fate of genetic data for millions of customers. As part of our [Data Breaches & Identity Protection guide](/data-breaches/), this article examines what happened, why genetic data breaches are uniquely dangerous, and what affected users should do.

## What Happened: Timeline

### October 2023: The Initial Disclosure

On October 6, 2023, 23andMe confirmed that user data had been compromised and was being offered for sale on hacking forums. The stolen data had initially appeared on the BreachForums dark web marketplace in August 2023, where a user posted samples claiming to have data on millions of 23andMe users, with some posts specifically targeting users of Ashkenazi Jewish and Chinese descent.

23andMe's initial disclosure characterized the incident as limited, attributing it to [credential stuffing](/data-breaches/credential-stuffing/) attacks against individual user accounts.

### December 2023: The Full Scope Revealed

On December 1, 2023, 23andMe revised its disclosure significantly upward. While approximately 14,000 accounts were directly compromised through credential stuffing, the attackers had exploited the DNA Relatives feature to access profile information for 6.9 million additional users -- roughly half of 23andMe's entire customer base.

The DNA Relatives feature is an opt-in tool that allows users to discover and connect with genetic relatives in 23andMe's database. When an attacker gained access to one account, they could scrape the profile information of every other user connected through DNA Relatives matches. A relatively small number of compromised accounts cascaded into a massive data exposure.

### January 2024: Blame and Backlash

In January 2024, 23andMe drew sharp criticism when it sent letters to breach victims stating that the incident was caused by users who "negligently recycled and failed to update their passwords." The company attempted to shift responsibility to users for reusing passwords across multiple services. This framing was widely condemned by security experts and lawyers, who noted that 23andMe's own platform design -- specifically the DNA Relatives feature's data-sharing model -- was the primary amplification factor.

### March 2024: Bankruptcy Filing

On March 24, 2024, 23andMe filed for Chapter 11 bankruptcy protection. The company's stock price had plummeted from its peak of over $6 per share to under $1. The breach, combined with declining consumer interest and mounting legal liabilities, left the company financially unviable.

The bankruptcy raised an existential question for the genetic testing industry: what happens to millions of people's DNA data when the company holding it ceases to exist? Privacy advocates, state attorneys general, and federal regulators all urged 23andMe users to delete their data before any acquisition could transfer it to new ownership with unknown privacy practices.

## What Was Exposed

### Profile and Ancestry Data

For approximately 6.9 million users whose data was scraped through DNA Relatives:

- **Display names and profile photos**
- **Birth years and self-reported locations**
- **Ancestry composition results** (ethnicity percentage breakdowns)
- **DNA Relatives match lists** (revealing biological family connections)
- **Haplogroup information** (maternal and paternal genetic lineage)

### Family Tree Data

For approximately 1.4 million users who had opted into the Family Tree feature:

- **Family relationship labels** (parent, sibling, cousin)
- **Birth years and self-reported locations** of family members
- **Relationship connection maps**

### What Was Not Directly Accessed

23andMe stated that raw genotype data files (the actual DNA sequencing results) were not accessed in this breach. However, the ancestry composition results and haplogroup data that were exposed are derived from genetic analysis and reveal significant biological information.

## How It Happened

### The Credential Stuffing Vector

The initial entry point was [credential stuffing](/data-breaches/credential-stuffing/) -- the automated testing of username/password combinations previously stolen from other services. Users who reused passwords across multiple websites were vulnerable. The attackers used credentials from previous, unrelated data breaches to log into approximately 14,000 23andMe accounts.

This is the same attack vector seen in countless breaches, and it underscores the [danger of password reuse](/password-security/password-reuse-dangers/). A single password used across multiple services creates a chain of vulnerability that extends far beyond the originally breached service.

### The DNA Relatives Amplification

What made this breach exceptional was the amplification effect of the DNA Relatives feature. Each compromised account gave the attackers access to the profile information of potentially hundreds of genetic matches. The social graph of genetic relationships served as a force multiplier, turning 14,000 compromised accounts into 6.9 million exposed profiles.

This architectural vulnerability is inherent to any platform that shares data between users. The DNA Relatives feature was functioning as designed -- it was meant to connect genetic relatives. But this same design meant that each compromised account was a window into a vast network of connected users.

### No Multi-Factor Authentication Requirement

At the time of the breach, 23andMe offered but did not require multi-factor authentication. Given the extraordinary sensitivity of genetic data, this was a significant security gap. Following the breach, 23andMe mandated two-factor authentication for all users.

## Impact

### The Uniqueness of Genetic Data Exposure

Every other type of personal data can be changed after a breach. You can get a new credit card number, change your passwords, freeze your credit, and even, in extreme cases, get a new Social Security number. You cannot change your DNA.

The exposed genetic data reveals:

- **Ethnic and ancestral heritage** -- information that in some contexts carries discrimination risk
- **Biological family relationships** -- potentially revealing previously unknown relatives, adoption details, or family secrets
- **Genetic predispositions** -- ancestry data can, in some cases, correlate with health-related genetic markers

The permanence of this exposure is the defining characteristic of genetic data breaches. The information exposed in 2023 will remain accurate and sensitive for the lifetime of every affected individual and, in fact, for the lifetimes of their biological descendants.

### The Bankruptcy Data Custody Crisis

23andMe's bankruptcy filing created a novel and alarming scenario. The company held raw genetic data for approximately 15 million users. In bankruptcy proceedings, this data is an asset that could be sold to the highest bidder. A buyer might have entirely different privacy practices, data monetization strategies, or security standards.

Multiple state attorneys general issued public statements urging 23andMe users to delete their data before any acquisition. California's Attorney General explicitly warned that the privacy protections in 23andMe's original terms of service might not survive a bankruptcy sale.

### Legal Fallout

Multiple class action lawsuits were filed against 23andMe. The company's attempt to blame users for password reuse was widely viewed as both legally and ethically problematic, particularly given that the DNA Relatives feature -- a platform design decision -- was the primary amplification factor.

## Lessons for Users

### Lesson 1: Genetic Data Requires Extraordinary Caution

Before sharing your DNA with any company, consider what happens if that company is breached, goes bankrupt, changes ownership, or changes its privacy policy. Genetic data is the most sensitive personal information you can share, and it is the only type that is truly permanent and immutable.

### Lesson 2: Credential Stuffing Is Preventable

The entire 23andMe breach began with [credential stuffing](/data-breaches/credential-stuffing/) -- an attack that is entirely preventable with two simple measures: unique passwords for every account and multi-factor authentication. If the 14,000 initially compromised users had used unique passwords, the breach would not have occurred.

### Lesson 3: Social Features Create Cascading Risk

Any platform feature that shares your data with other users creates an expanded attack surface. On 23andMe, opting into DNA Relatives meant your data could be exposed through the compromise of any other user you were matched with. Consider carefully before opting into social or sharing features, especially on platforms holding sensitive data.

### Lesson 4: Company Survival Is Not Guaranteed

When you entrust data to a company, you are implicitly betting on that company's continued existence and commitment to its privacy policies. 23andMe's bankruptcy demonstrated that companies can fail, and when they do, your data becomes an asset on a balance sheet. Consider this risk before sharing data that cannot be revoked.

## How to Protect Yourself

### If You Are a 23andMe User

1. **Consider deleting your 23andMe data**. Log into your account, go to Settings, and use the account deletion option. Request deletion of your genetic data as well. Note that this does not recover data already exposed in the breach.

2. **Download your data first** if you want to retain a personal copy before deletion.

3. **Disable DNA Relatives** and any other data-sharing features if you choose to keep your account.

4. **Change your 23andMe password** to a unique, randomly generated password. Better yet, use a password manager like PanicVault to generate and store unique passwords for every service. PanicVault uses the KeePass format and stores your vault locally on your Apple devices, ensuring your credentials are not held on another company's servers.

5. **Enable multi-factor authentication** on your 23andMe account and every other account you use.

### General Protective Measures

6. **Stop reusing passwords immediately**. The 23andMe breach began because users reused passwords from other services. A password manager eliminates this risk entirely by generating and remembering unique passwords for every site. The [dangers of password reuse](/password-security/password-reuse-dangers/) cannot be overstated.

7. **[Check whether your email has been compromised](/data-breaches/check-email-compromised/)** in other breaches using [Have I Been Pwned](/data-breaches/have-i-been-pwned/). If your credentials appeared in previous breaches, they were likely used in credential stuffing attacks against 23andMe and other services.

8. **[Monitor your identity](/data-breaches/dark-web-monitoring/)** for signs that your personal information is being misused. While your genetic data itself is unlikely to be used for financial fraud, the associated personal information (name, birth year, location) adds to your overall exposure profile.

9. **[Freeze your credit](/data-breaches/freeze-credit/)** if you have not already done so. While the 23andMe breach did not expose financial data, the personal information exposed (name, birth year, location) combined with data from other breaches may be sufficient for identity theft.

10. **Be skeptical of future genetic testing services**. Before submitting DNA to any company, review their privacy policy, data retention practices, security measures, and what happens to your data if the company is acquired or goes bankrupt. Consider whether the benefits of the service outweigh the permanent, irrevocable nature of genetic data sharing.

The 23andMe breach forces a reckoning with a question that the technology industry has largely avoided: are some types of data too sensitive to entrust to any company, regardless of its security measures? Your DNA is the most personal data you possess. Once shared, it can never be fully recovered. Every future decision about genetic data sharing should be made with the full understanding of this reality.

## Related Articles

- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [The Dangers of Password Reuse](/password-security/password-reuse-dangers/)
- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [Check If Your Email Has Been Compromised](/data-breaches/check-email-compromised/)
- [The Biggest Data Breaches of 2025-2026](/data-breaches/biggest-breaches/)
