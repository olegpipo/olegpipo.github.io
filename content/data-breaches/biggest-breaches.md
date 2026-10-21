---
title: "The Biggest Data Breaches of 2024-2026"
description: "The breaches behind today's scams: the Snowflake campaign (AT&T, Ticketmaster), Change Healthcare, PowerSchool, Coinbase, the 2025 Salesforce attacks and Canvas -- what leaked and what to do."
date: 2026-02-14
lastmod: 2026-10-21
draft: false
silo: "Data Breaches & Identity"
aliases:
  - /data-breaches/att-data-breach/
  - /data-breaches/ticketmaster-data-breach/
  - /data-breaches/marriott-data-breach/
---

Some years are defined by one enormous breach, others by a pattern. 2024 produced the mega-breaches whose data still circulates today. 2025 had fewer giant incidents but more incidents overall, and a clear shift in method: attackers who talked their way in -- through help desks, bribed insiders and connected apps -- instead of breaking in. This article catalogs the incidents that matter most for ordinary people, what each one exposed, and the practical lesson for your own [data breach](/data-breaches/) defenses.

These are not just news stories. Each breach represents millions of people asking the same questions: "Was I affected?" and "What do I do now?" If you find yourself asking those questions, our [breach response guide](/data-breaches/what-to-do-after-breach/) provides your action plan.

## The Scale of the Problem

Before examining individual incidents, the numbers deserve context:

- The Identity Theft Resource Center counted a record [3,300-plus publicly reported data compromises](https://www.infosecurity-magazine.com/news/us-data-breaches-record-high/) in the US in 2025. Yet victim notices fell to about 279 million, from roughly 1.4 billion in 2024, because 2025 had no single breach on the scale of 2024's biggest.
- Verizon's [2026 Data Breach Investigations Report](https://www.verizon.com/business/resources/reports/dbir/), covering incidents from November 2024 to October 2025, found that exploiting software vulnerabilities (31% of breaches) had overtaken stolen passwords as the most common way in, and that ransomware was involved in 48% of breaches.
- IBM's [2026 Cost of a Data Breach Report](https://www.ibm.com/reports/data-breach) puts the global average cost of a breach at a record $4.99 million.

These figures come with a caveat: they reflect only breaches that were detected and reported. The true number is certainly higher.

## The 2024 Mega-Breaches (Still in Circulation)

### National Public Data

**When**: Breached around late 2023; the data was offered for sale in April 2024 and leaked for free in August 2024

**Scale**: The seller claimed 2.9 billion records. Many people appear several times, with different addresses from different years.

**What was exposed**: Names, Social Security numbers, mailing addresses going back decades, phone numbers, and email addresses

**Why it matters**: National Public Data was a data broker -- a company that aggregates and sells personal information about people who never dealt with it. Once the full dataset was posted for free, Social Security numbers and address histories were available to anyone. See our [National Public Data breach analysis](/data-breaches/national-public-data-breach/) for the full story.

**Lesson**: Data brokers hold enormous amounts of personal information, often without your knowledge or consent. [Freezing your credit](/data-breaches/freeze-credit/) is one of the few proactive defenses against the downstream effects, and [removing yourself from data brokers](/digital-privacy/remove-personal-info/) shrinks what the next one can leak.

### Change Healthcare

**When**: February 2024

**Scale**: Approximately 190 million people

**What was exposed**: Health insurance information, medical records, billing data, Social Security numbers, payment information

**Why it matters**: Change Healthcare processes a significant portion of US healthcare transactions. The attackers used stolen credentials to log into a Citrix remote-access portal that lacked multi-factor authentication -- a basic security control. UnitedHealth Group, Change Healthcare's parent company, paid a $22 million ransom, and the incident's total cost exceeded $2 billion. More in our [Change Healthcare breach analysis](/data-breaches/change-healthcare-breach/).

**Lesson**: Critical infrastructure often has basic security gaps. MFA is not optional. The [two-factor authentication](/two-factor-authentication/) that could have prevented this breach costs virtually nothing to implement.

### The Snowflake Campaign: AT&T, Ticketmaster and About 165 Organizations

In spring 2024, a financially motivated group that Mandiant tracks as UNC5537 logged into the Snowflake cloud data accounts of about 165 organizations using passwords stolen by infostealer malware -- some harvested as far back as 2020. Snowflake's platform itself was not breached. According to [Mandiant's investigation](https://cloud.google.com/blog/topics/threat-intelligence/unc5537-snowflake-data-theft-extortion), three things made it possible: the accounts had no multi-factor authentication, the stolen passwords had never been changed, and nothing restricted logins to trusted networks.

The pipeline is worth understanding, because it applies far beyond Snowflake:

1. **Infostealer malware** on an employee's or contractor's computer, often a personal machine also used for work, harvests saved passwords.
2. **The credentials are sold or shared** in criminal markets, sometimes for years.
3. **Attackers try them** against cloud login pages.
4. **Accounts without MFA** open with the username and password alone.
5. **Data is exported in bulk**, and the company is extorted.

Snowflake has since moved to make MFA mandatory and phase out password-only sign-ins.

#### AT&T: Two Separate Incidents

- **March 2024 (not Snowflake)**: AT&T confirmed that a dataset circulating on the dark web, dating from 2019 or earlier, held information including Social Security numbers and account passcodes for about 7.6 million current and 65.4 million former account holders. It could not say whether the data came from its own systems or a vendor's, and it reset the affected passcodes. A hacker had claimed to hold AT&T customer data back in 2021, which AT&T denied at the time.
- **July 2024 (Snowflake)**: AT&T disclosed that records of calls and texts made by nearly all of its wireless customers between roughly May 1 and October 31, 2022 (and on January 2, 2023 for some) had been downloaded from its Snowflake workspace -- about 109 million customer accounts, as widely reported. According to its [SEC filing](https://www.sec.gov/Archives/edgar/data/732717/000073271724000046/t-20240506.htm), the records show which numbers each customer interacted with, how many times, and the total call time per day or month, plus cell site IDs for some records -- but not the content of calls or texts, names, or Social Security numbers. AT&T learned of it on April 19, 2024; the Justice Department twice decided public disclosure should be delayed.
- **Settlement**: AT&T agreed to a $177 million class settlement covering both incidents (up to $149 million for the first and $28 million for the second), which a federal judge gave final approval in 2026.

**Lesson: metadata is more revealing than it sounds.** Who you call, how often, for how long, and for some records which cell tower was nearby, maps your relationships, your doctor, your lawyer and your routine without a single word of content. And the first dataset paired phone numbers with Social Security numbers and carrier passcodes -- exactly what a SIM swapper needs. Change your carrier passcode and move important accounts from SMS codes to an authenticator app or security key.

#### Ticketmaster

Live Nation, Ticketmaster's parent company, told the SEC it detected unauthorized activity in a third-party cloud database on May 20, 2024, and that on May 27 a criminal offered what it alleged was company user data for sale on the dark web. The seller, ShinyHunters, claimed 560 million customer records and asked $500,000; the company never confirmed that number. Ticketmaster's notices to customers said the data, taken between April 2 and May 18, 2024, could include names, contact details, and payment card details such as the last four digits and expiration dates.

**Lesson: purchase history is a phishing kit.** Knowing which concerts and games you bought tickets for lets an attacker write "There's a problem with your tickets for [the real event]" -- far more convincing than a generic lure. Check any ticket "problem" in the official app, never through the email's link.

### Dell

**When**: May 2024

**Scale**: The seller claimed 49 million customer records

**What was exposed**: According to Dell's notice, names, physical addresses, and order details (service tags, item descriptions, order dates, warranty information) -- not payment information, email addresses, or phone numbers

**Why it matters**: The exposed information was enough for highly targeted phishing and support scams. An attacker who knows exactly which Dell computer you bought, and when, can craft a very convincing "warranty" or "tech support" message.

**Lesson**: Non-financial data has more value than people realize. See [what attackers do with stolen data](/data-breaches/what-to-do-after-breach/) for how seemingly harmless details enable downstream attacks.

### A Historic Mega-Breach: Marriott and Starwood

Some older breaches still teach the clearest lessons. Attackers were inside the Starwood hotel reservation system from 2014 until the intrusion was discovered in September 2018 -- right through Marriott's 2016 acquisition of Starwood. About 383 million guest records were affected, including roughly 5.25 million unencrypted passport numbers. In October 2024 the FTC ordered Marriott and Starwood to overhaul their security over [three breaches between 2014 and 2020 affecting more than 344 million customers](https://www.ftc.gov/news-events/news/press-releases/2024/10/ftc-takes-action-against-marriott-starwood-over-multiple-data-breaches), and Marriott agreed to a separate $52 million penalty with 49 states and the District of Columbia.

**Lesson**: When a company you use is acquired, its old systems -- and whoever is already inside them -- can come along. And a passport number cannot be changed as easily as a password.

## Major Breaches of 2025

### PowerSchool

**When**: Disclosed January 2025; data stolen in late December 2024

**Scale**: About 60 million students and 10 million teachers, according to federal prosecutors

**How it happened**: The attacker logged in with a PowerSchool contractor's stolen credentials. PowerSchool, whose software many US school districts use for student records, paid a ransom worth nearly $2.9 million, yet school districts still received follow-on extortion demands. The Massachusetts man behind the attack, Matthew Lane, pleaded guilty and was [sentenced to four years in prison](https://cyberscoop.com/powerschool-hacker-matthew-lane-sentenced/) in October 2025.

**Lesson**: Paying a ransom does not make stolen data safe. Children's records are especially valuable because nobody checks a child's credit for years; parents can freeze a child's credit at the three bureaus, the same way they [freeze their own](/data-breaches/freeze-credit/).

### Coinbase

**When**: May 2025

**Scale**: 69,461 customers notified, according to Coinbase's filing with Maine's attorney general

**What was exposed**: According to Coinbase's SEC filing ([reported by BleepingComputer](https://www.bleepingcomputer.com/news/security/coinbase-discloses-breach-faces-up-to-400-million-in-losses/)), names, addresses, phone numbers and email addresses; the last four digits of Social Security numbers; masked bank account numbers; images of government IDs; and balance snapshots and transaction history. No passwords, private keys or funds were exposed.

**How it happened**: Criminals paid contractors or support staff outside the US to pull customer data from internal support tools. Coinbase refused a $20 million extortion demand, offered a $20 million reward for information instead, and estimated the incident's cost, including reimbursing customers, at $180 million to $400 million.

**Lesson**: The data was made for convincing phone scams. A caller who knows your balance and the last four digits of your Social Security number sounds exactly like the real support team. Hang up and contact the company through its app; no legitimate support agent will ask you to move funds to a "safe" wallet.

### The Salesforce Campaigns

Two related waves in 2025 went after companies' Salesforce data -- not by attacking Salesforce itself, but through the people and apps connected to it:

- **Voice phishing**: A group Google tracks as UNC6040 phoned employees while posing as IT support and talked them into connecting a modified Data Loader app to their company's Salesforce, then stole customer records for extortion by a group claiming to be ShinyHunters. Google's own Salesforce instance, which held basic business contact details, was hit in June 2025 ([Google Threat Intelligence](https://cloud.google.com/blog/topics/threat-intelligence/voice-phishing-data-extortion)).
- **Stolen app tokens**: Between August 8 and at least August 18, 2025, a group tracked as UNC6395 used OAuth tokens stolen from the Salesloft Drift chat integration to export data from numerous companies' Salesforce instances, then searched it for passwords and cloud access keys ([Google Threat Intelligence](https://cloud.google.com/blog/topics/threat-intelligence/data-theft-salesforce-instances-via-salesloft-drift)).

**Lesson**: No password was cracked and no software flaw was exploited -- a phone call and a connected app were enough. The companies you deal with can lose your contact details even if they do everything else right, and the follow-up will be phishing. For your own accounts, review the third-party apps connected to your Google, Microsoft and Apple accounts and remove the ones you no longer use.

## 2026 So Far

### Canvas (Instructure)

In May 2026, Instructure, maker of the Canvas learning platform used by schools and universities, said attackers had stolen names, email addresses, student ID numbers, and messages between users; it found no evidence that passwords, dates of birth, government IDs or financial information were taken. The extortion group ShinyHunters claimed data on 275 million students and staff at nearly 9,000 institutions, an unverified figure. After the group defaced Canvas login pages, Instructure briefly took the platform offline, and on May 11 said it had paid the extortionists and that the data had been returned ([Krebs on Security](https://www.krebsonsecurity.com/2026/05/canvas-breach-disrupts-schools-colleges-nationwide/)).

**Lesson**: There is no way to verify that stolen data was really deleted. If your school uses Canvas, expect phishing that quotes your real courses or messages, and sign in only through your school's usual link.

## Patterns Across the Biggest Breaches

Several common threads connect these incidents:

### Missing Multi-Factor Authentication

A striking number of major breaches succeeded because MFA was not enabled on critical systems. The Change Healthcare and Snowflake breaches both exploited exactly that gap. [Two-factor authentication](/two-factor-authentication/) is the single most effective technical control for preventing credential-based breaches.

### People Were the Way In

Coinbase's attackers bribed support staff; the Salesforce attackers phoned employees and asked. No amount of encryption helps when someone with legitimate access is persuaded to use it for the attacker. The same tactics are aimed at you: [social engineering](/phishing/social-engineering-guide/) works on customers as well as staff.

### Third-Party and Supply Chain Exposure

Snowflake accounts, a Salesloft Drift integration, and a PowerSchool contractor's login: many of these breaches started not at the company in the headlines but at a vendor, a contractor, or a connected app. Your data's security depends on every organization in the chain.

### Cloud Misconfigurations and Weak Access Controls

The data in most of these incidents lived in well-built cloud platforms. What failed was access: password-only logins, credentials never rotated, overly broad app permissions. As detailed in our guide to [how breaches happen](/data-breaches/how-breaches-happen/), these gaps are persistent and preventable.

### Delayed Detection

Some of the Snowflake credentials had been stolen as early as 2020, and a hacker claimed AT&T's older dataset in 2021, three years before AT&T acknowledged it. By the time a [breach notification letter](/data-breaches/notification-letters/) reaches you, the breach may have happened months or years earlier.

### Data Broker Risk

The National Public Data breach highlighted the unique risk posed by data brokers -- companies that aggregate your personal information from public records, commercial transactions, and other sources. You may have no direct relationship with the breached company and no way to have "opted out" of the data collection.

## What You Can Do

The scale of modern breaches can feel overwhelming, but effective personal defenses exist:

### 1. Accept That Your Data Is Likely Already Exposed

If you have been active online for more than a few years, some of your personal information is almost certainly in the hands of attackers. The question is not whether you have been breached but how well you have limited the usefulness of the stolen data.

### 2. Make Credential Stuffing Impossible

Use a [password manager](/password-managers/) to generate unique, strong passwords for every account. When credentials from one breach cannot be reused at other services, the cascade stops. With dozens or hundreds of accounts, a password manager is the only practical way to maintain unique passwords at scale.

Consider a password manager that does not create a centralized target. Cloud-based managers store encrypted vaults on vendor servers -- and as the [LastPass breach](/data-breaches/lastpass-breach-lessons/) demonstrated, those servers can be breached. Password managers using the [KeePass format](/keepass/), like PanicVault, store your encrypted database on your own devices or your own iCloud Drive. There is no PanicVault server for attackers to target. If PanicVault ceased to exist, your data remains accessible through any KeePass-compatible app.

### 3. Enable Two-Factor Authentication Everywhere

Use passkeys, hardware security keys or authenticator apps -- not SMS -- for your most important accounts.

### 4. Freeze Your Credit

Unless you are actively applying for new credit, keep your credit [frozen at all three bureaus](/data-breaches/freeze-credit/). It is free, takes minutes, and prevents the most damaging form of identity theft.

### 5. Monitor Your Exposure

Register all your email addresses with [Have I Been Pwned](/data-breaches/have-i-been-pwned/) for automatic breach notifications. Use your password manager's breach monitoring features. Set up [identity theft monitoring](/data-breaches/monitoring-alerts/) appropriate to your risk level.

### 6. Expect the Follow-Up Scam

Breached data is mostly used to make phishing believable. Treat any email, text or call that mentions a breach, a refund, a settlement or a problem with your account as suspect, and [verify it through the official app or website](/phishing/recognize-phishing/) instead.

### 7. Minimize Your Data Footprint

Every service that holds your data is a potential breach source. Use guest checkout, decline to provide optional information, delete accounts you no longer use, and request data deletion where legally supported.

## Related Articles

- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [How Data Breaches Happen: Anatomy of an Incident](/data-breaches/how-breaches-happen/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [How to Freeze Your Credit After a Data Breach](/data-breaches/freeze-credit/)
- [Have I Been Pwned? Using Free Breach-Checking Tools](/data-breaches/have-i-been-pwned/)
