---
title: "The Biggest Data Breaches of 2025-2026"
description: "Catalog of the most significant data breaches of 2025-2026 -- scale, data exposed, downstream impact, and lessons for personal security from each incident."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Data Breaches & Identity"
---

Every year, data breaches grow larger in scale, more sophisticated in execution, and more consequential for affected individuals. The [data breach landscape](/data-breaches/) of 2025 and early 2026 continued this trajectory, with several incidents ranking among the largest ever recorded. The average cost of a data breach in the United States reached $10.22 million in 2025, and the human cost -- measured in compromised identities, drained accounts, and years of recovery -- was incalculable.

This article catalogs the most significant breaches of the period, examines what made each one notable, and extracts practical lessons for protecting yourself. These are not just news stories. Each breach represents millions of people asking the same questions: "Was I affected?" and "What do I do now?" If you find yourself asking those questions, our [breach response guide](/data-breaches/what-to-do-after-breach/) provides your action plan.

## The Scale of the Problem

Before examining individual incidents, the numbers deserve context. In 2025:

- More than 3,200 publicly reported data breaches occurred in the United States alone
- Over 1.5 billion individual records were exposed
- The average time to identify and contain a breach was 258 days
- Twenty-two percent of breaches involved [credential stuffing](/data-breaches/credential-stuffing/) -- automated attacks using previously stolen passwords
- The healthcare, financial, and technology sectors were the most frequently targeted

These figures come with a caveat: they reflect only publicly reported breaches. The true number is certainly higher, as many breaches go undetected or unreported.

## Major Breaches of 2025

### National Public Data Breach (Fallout Continues)

**When**: Originally breached in late 2023, with ongoing data circulation through 2025

**Scale**: 2.9 billion records containing personal information for approximately 170 million individuals

**What was exposed**: Full names, Social Security numbers, dates of birth, physical addresses spanning decades, phone numbers

**Why it matters**: National Public Data was a data broker -- a company that aggregates and sells personal information. The breach was notable not just for its massive scale but for the type of data exposed. Social Security numbers and comprehensive address histories provide everything needed for identity theft. The breached data continued to circulate on dark web markets throughout 2025, making this a persistent rather than point-in-time threat.

**Lesson**: Data brokers hold enormous amounts of personal information, often without your knowledge or explicit consent. This data is a high-value target. [Freezing your credit](/data-breaches/freeze-credit/) is one of the few proactive defenses against the downstream effects of such breaches.

### Change Healthcare

**When**: February 2024, with full scope and impact unfolding through 2025

**Scale**: Approximately 190 million individuals

**What was exposed**: Health insurance information, medical records, billing data, Social Security numbers, payment information

**Why it matters**: Change Healthcare processes a significant portion of US healthcare transactions. The breach affected patients, healthcare providers, pharmacies, and insurers across the country. The attackers used stolen credentials to access a Citrix portal that lacked multi-factor authentication -- a basic security control. UnitedHealth Group, Change Healthcare's parent company, paid a $22 million ransom, and the incident's total cost exceeded $2 billion.

**Lesson**: Critical infrastructure often has basic security gaps. MFA is not optional. The [two-factor authentication](/two-factor-authentication/) that could have prevented this breach costs virtually nothing to implement.

### AT&T Customer Records

**When**: Disclosed in 2024, with ongoing impact through 2025

**Scale**: 73 million current and former customers

**What was exposed**: Social Security numbers, account numbers, phone numbers, addresses. A separate incident exposed call and text metadata for nearly all AT&T wireless customers.

**Why it matters**: The combination of SSNs and phone numbers is particularly dangerous. Phone numbers are increasingly used as a second authentication factor (via SMS), and attackers can use SIM-swapping to intercept those codes. SSN exposure enables new account fraud.

**Lesson**: SMS-based [two-factor authentication](/two-factor-authentication/) is vulnerable when phone numbers and carrier account details are breached. Use authenticator apps or hardware security keys instead of SMS wherever possible.

### Ticketmaster/Live Nation

**When**: May-June 2024, with data trading continuing through 2025

**Scale**: Over 560 million customer records

**What was exposed**: Names, email addresses, phone numbers, partial payment card data, order history

**Why it matters**: The breach occurred through a compromised Snowflake cloud data warehouse account -- part of a broader campaign targeting Snowflake customers who had not enabled MFA. The breach illustrated how a single compromised credential for a cloud platform can cascade into massive data exposure.

**Lesson**: Cloud platforms multiply both convenience and risk. A single set of credentials can unlock enormous amounts of data, making strong, unique passwords and mandatory MFA essential.

### Dell Technologies

**When**: May 2024, ongoing impact through 2025

**Scale**: 49 million customer records

**What was exposed**: Customer names, physical addresses, Dell order information (product details, order dates, warranty information)

**Why it matters**: While the breach did not include financial data, the exposed information was sufficient for highly targeted phishing and social engineering attacks. An attacker who knows what Dell products you purchased and when can craft extremely convincing messages.

**Lesson**: Non-financial data has more value than people realize. [What hackers steal](/data-breaches/what-hackers-steal/) explains how seemingly innocuous data enables downstream attacks.

## Breaches Shaping Early 2026

### Healthcare Sector Continues to be Targeted

The healthcare sector remained the most expensive industry for data breaches, with average costs exceeding $10 million per incident. Multiple regional health systems and health insurance providers reported breaches exposing patient records, insurance data, and SSNs.

### Education Sector Surge

Universities and school districts experienced a significant increase in breaches, driven by ransomware attacks targeting institutions with limited IT security budgets. Student records, financial aid information, and research data were primary targets.

### AI-Related Data Exposures

As organizations rapidly adopted AI tools, several breaches involved training data, customer data processed by AI systems, and misconfigurations in AI platform integrations. The intersection of AI adoption and data security is an emerging concern.

## Patterns Across the Biggest Breaches

Several common threads connect these incidents:

### Missing Multi-Factor Authentication

A striking number of major breaches succeeded because MFA was not enabled on critical systems. The Change Healthcare and Snowflake-related breaches both exploited the absence of mandatory MFA. [Two-factor authentication](/two-factor-authentication/) is the single most effective technical control for preventing credential-based breaches.

### Third-Party and Supply Chain Exposure

Many 2025 breaches originated not at the primary company but at a third-party service provider, data processor, or cloud platform. The interconnected nature of modern IT infrastructure means that your data's security depends on the security practices of every organization in the chain.

### Cloud Misconfigurations

The migration to cloud computing continues to produce data exposures through misconfigured storage and access controls. As detailed in our guide to [how breaches happen](/data-breaches/how-breaches-happen/), cloud misconfigurations are a persistent and often preventable breach vector.

### Delayed Detection

The average time to identify a breach remained well over 200 days. During this window, attackers had unfettered access to data. By the time a [breach notification letter](/data-breaches/notification-letters/) reaches you, the breach may have occurred months earlier.

### Data Broker Risk

The National Public Data breach highlighted the unique risk posed by data brokers -- companies that aggregate your personal information from public records, commercial transactions, and other sources. You may have no direct relationship with the breached company and no way to have "opted out" of the data collection.

## What You Can Do

The scale of modern breaches can feel overwhelming, but effective personal defenses exist:

### 1. Accept That Your Data Is Likely Already Exposed

If you have been active online for more than a few years, some of your personal information is almost certainly in the hands of attackers. The question is not whether you have been breached but how well you have limited the usefulness of the stolen data.

### 2. Make Credential Stuffing Impossible

Use a [password manager](/password-managers/) to generate unique, strong passwords for every account. When credentials from one breach cannot be reused at other services, the cascade stops. With the average person managing roughly 250 passwords, a password manager is the only practical way to maintain unique passwords at scale.

Consider a password manager that does not create a centralized target. Cloud-based managers store encrypted vaults on vendor servers -- and as the [LastPass breach](/data-breaches/lastpass-breach-lessons/) demonstrated, those servers can be breached. Password managers using the [KeePass format](/keepass/), like PanicVault, store your encrypted database on your own devices or your own iCloud Drive. There is no PanicVault server for attackers to target. If PanicVault ceased to exist, your data remains accessible through any KeePass-compatible app.

### 3. Enable Two-Factor Authentication Everywhere

Use hardware security keys or authenticator apps -- not SMS -- for your most important accounts.

### 4. Freeze Your Credit

Unless you are actively applying for new credit, keep your credit [frozen at all three bureaus](/data-breaches/freeze-credit/). It is free, takes minutes, and prevents the most damaging form of identity theft.

### 5. Monitor Your Exposure

Register all your email addresses with [Have I Been Pwned](/data-breaches/have-i-been-pwned/) for automatic breach notifications. Use your password manager's breach monitoring features. Set up [identity theft monitoring](/data-breaches/monitoring-alerts/) appropriate to your risk level.

### 6. Minimize Your Data Footprint

Every service that holds your data is a potential breach source. Use guest checkout, decline to provide optional information, delete accounts you no longer use, and request data deletion where legally supported.

## Related Articles

- [How Data Breaches Happen: Anatomy of an Incident](/data-breaches/how-breaches-happen/)
- [What Information Hackers Steal in a Breach](/data-breaches/what-hackers-steal/)
- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [How to Freeze Your Credit After a Data Breach](/data-breaches/freeze-credit/)
