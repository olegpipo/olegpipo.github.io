---
title: "Ticketmaster Breach: Lessons"
description: "Analysis of the 2024 Ticketmaster breach that exposed 560 million customer records through a compromised Snowflake cloud account."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Data Breaches & Identity"
faq:
  - question: "How many people were affected by the Ticketmaster data breach?"
    answer: "Approximately 560 million customer records were compromised, making it one of the largest data breaches of 2024. The breach included customers of Ticketmaster and its parent company Live Nation across multiple countries."
  - question: "What data was stolen from Ticketmaster?"
    answer: "The stolen data included full names, email addresses, phone numbers, home addresses, partial payment card data (last four digits and expiration dates), order history and ticket purchase details, and account information."
  - question: "How did the Ticketmaster breach happen?"
    answer: "Attackers compromised Ticketmaster's Snowflake cloud data account using stolen credentials. The account did not have multi-factor authentication enabled. This attack was part of a broader campaign targeting approximately 165 Snowflake customer accounts."
  - question: "Is the Ticketmaster breach related to other 2024 breaches?"
    answer: "Yes. The Ticketmaster breach was part of a broader campaign by the same threat group that targeted multiple Snowflake customers, including AT&T and other major companies. The attackers systematically accessed Snowflake accounts that lacked multi-factor authentication."
  - question: "What should Ticketmaster customers do after the breach?"
    answer: "Change your Ticketmaster and Live Nation passwords immediately, monitor your payment cards for unauthorized charges, enable MFA where available, watch for phishing emails referencing past ticket purchases, and check your breach exposure at Have I Been Pwned."
---

The 2024 Ticketmaster data breach exposed approximately 560 million customer records -- names, contact information, partial payment data, and detailed purchase histories. The breach was notable not just for its scale but for its method: attackers accessed Ticketmaster's data through a compromised Snowflake cloud account, part of a broader campaign that targeted dozens of companies storing data on the same platform. The incident demonstrated how cloud service supply chains create interconnected risk, where a vulnerability in one provider's access controls can cascade across an entire ecosystem of customers. As part of our [Data Breaches & Identity Protection guide](/data-breaches/), this article examines what happened, what was exposed, and what Ticketmaster customers should do.

## What Happened: Timeline

### April-May 2024: The Snowflake Campaign

In early 2024, a group of hackers began systematically targeting companies that used Snowflake, a popular cloud data warehousing platform. The attackers obtained credentials for Snowflake customer accounts -- primarily through infostealer malware that had previously infected employees' computers and harvested login credentials. They then tested these credentials against Snowflake accounts that did not require multi-factor authentication.

Snowflake itself was not breached. Rather, individual customer accounts were compromised because they relied solely on username-and-password authentication. The campaign ultimately affected approximately 165 Snowflake customer accounts, including Ticketmaster, [AT&T](/data-breaches/att-data-breach/), Advance Auto Parts, and others.

### May 2024: Ticketmaster's Data Accessed

In late May 2024, Ticketmaster's parent company Live Nation detected unauthorized activity in a third-party cloud database environment. The attackers had accessed Ticketmaster's Snowflake account and downloaded a massive dataset containing customer records.

On May 28, 2024, a threat group known as ShinyHunters posted the stolen data for sale on a hacking forum, claiming to have 560 million customer records and demanding $500,000 for the dataset.

### May 31, 2024: SEC Filing

Live Nation filed an 8-K report with the Securities and Exchange Commission on May 31, 2024, acknowledging that "a criminal threat actor offered what it alleged to be Company user data for sale via the dark web."

### June-July 2024: Notifications Begin

Ticketmaster began notifying affected customers in June and July 2024. The company offered affected users one year of free identity monitoring through a third-party service.

## What Was Exposed

The 560-million-record dataset included:

### Personal Information
- **Full names**
- **Email addresses**
- **Phone numbers**
- **Home addresses**

### Financial Data
- **Partial payment card data** (last four digits and expiration dates of credit and debit cards)
- **Payment card types** used for purchases
- **Some encrypted credit card information**

### Account and Purchase Data
- **Ticketmaster account IDs**
- **Order history and ticket purchase details** (events attended, dates, venues, ticket quantities)
- **Customer service interaction records**

### Why Purchase History Matters

While the financial data was partial (last four digits only), the purchase history is a rich source of information for social engineering. An attacker who knows which concerts you attended, which sporting events you bought tickets for, and which venues you frequent can craft highly personalized phishing emails. "We noticed an issue with your tickets for [specific event]" is far more convincing than a generic phishing message.

## How It Happened

### The Infostealer-to-Snowflake Pipeline

The attack chain illustrates a growing pattern in modern breaches:

1. **Infostealer malware** infected employee computers (often personal machines used for work), harvesting stored credentials, session tokens, and browser data
2. **Stolen credentials** were sold or shared in underground markets
3. **Attackers tested credentials** against Snowflake customer login portals
4. **Accounts without MFA** were accessed using only the stolen username and password
5. **Data was exfiltrated** in bulk from the cloud data warehouse

This pipeline is particularly insidious because the initial infection may have occurred months or years before the breach. An employee who visited a compromised website or downloaded malicious software in 2022 could have had their Snowflake credentials harvested then, with those credentials sitting in criminal markets until the 2024 campaign.

### Shared Responsibility in Cloud Security

The Ticketmaster breach highlighted a critical tension in cloud security: the shared responsibility model. Snowflake provides the platform and the tools for securing it (including MFA). The customer is responsible for configuring those tools. When Ticketmaster failed to enable MFA on its Snowflake account, it assumed a risk that materialized in a 560-million-record breach.

Snowflake subsequently announced that it would begin requiring MFA for all accounts, acknowledging that optional security controls are insufficient when the consequences of not using them affect millions of people.

### The Scale of the Snowflake Campaign

Ticketmaster was one of approximately 165 companies affected by the same campaign. This concentration of attacks against a single platform's customers illustrates how cloud service providers become high-value targets -- not because their platforms are insecure, but because they aggregate access to many companies' data. Compromise the access controls for one platform, and you potentially gain entry to dozens of customers' data stores.

## Impact

### Consumer Impact

For 560 million Ticketmaster customers, the breach exposed personal contact information, partial financial data, and detailed records of entertainment preferences and spending. The primary risks include:

- **Targeted phishing** using purchase history and event details
- **Payment card monitoring** needs, even though only partial card data was exposed (partial data can be combined with information from other breaches)
- **Credential stuffing** if Ticketmaster passwords were reused on other services
- **Identity correlation** -- combining Ticketmaster data with other breach data to build comprehensive identity profiles

### Corporate Impact

Live Nation, already facing federal antitrust action over its dominant market position in live entertainment, faced additional scrutiny over its data security practices. The breach compounded the company's legal and reputational challenges during a period of intense regulatory attention.

### Industry Impact

The broader Snowflake campaign prompted a reassessment of cloud security practices across industries. Companies that stored data on Snowflake and other cloud platforms were forced to audit their access controls, implement MFA, and review their credential management practices.

## What Ticketmaster Did in Response

- **Notified affected customers** via email beginning in June 2024
- **Offered one year of free identity monitoring** through a third-party provider
- **Implemented MFA** on its Snowflake and other cloud platform accounts
- **Rotated credentials** for all cloud service accounts
- **Engaged cybersecurity firms** for forensic investigation and remediation
- **Filed SEC disclosure** as required for material cybersecurity incidents

## Lessons for Users

### Lesson 1: Cloud Supply Chains Create Hidden Risk

Your data is only as secure as the weakest link in the chain of companies that handle it. Ticketmaster stored data on Snowflake, and the breach occurred through Snowflake's access portal. As a Ticketmaster customer, you had no visibility into this third-party relationship or its security posture. This is a reality of modern digital services: your data traverses and resides in systems you may never know about.

### Lesson 2: MFA Is the Single Most Important Security Control

The entire Snowflake campaign -- affecting Ticketmaster, [AT&T](/data-breaches/att-data-breach/), and dozens of other companies -- was enabled by the absence of multi-factor authentication. Every compromised account could have been protected by MFA. This single control would have prevented hundreds of millions of records from being exposed.

### Lesson 3: Your Purchase History Is Valuable to Attackers

People tend to think of financial data (credit card numbers, SSNs) as the most dangerous type of exposed information. But purchase history and behavioral data are extremely valuable for social engineering. Knowing what events you attend, where you travel, and how you spend your money allows attackers to craft personalized attacks that are far more likely to succeed.

### Lesson 4: Infostealer Malware Is a Growing Threat

The credentials used to breach Ticketmaster's Snowflake account were likely stolen by infostealer malware running on an employee's computer. This type of malware is increasingly common and is often distributed through seemingly legitimate software downloads, browser extensions, or compromised websites. Keeping your devices clean and avoiding untrusted software is essential.

## How to Protect Yourself

If you have a Ticketmaster or Live Nation account, take these steps:

1. **Change your Ticketmaster password immediately**. Use a unique, randomly generated password. A password manager like PanicVault generates strong passwords and stores them in an encrypted vault on your Apple devices, eliminating the need to remember or reuse passwords across services.

2. **Enable multi-factor authentication** on your Ticketmaster account and every other online account that supports it.

3. **Monitor your payment cards** for unauthorized charges. Even though only partial card data was exposed, request new card numbers from your bank if you used a card on Ticketmaster.

4. **Watch for phishing emails** referencing past events, ticket purchases, or Ticketmaster account issues. Verify any communication by going directly to Ticketmaster.com rather than clicking links in emails.

5. **Do not reuse your Ticketmaster password** anywhere else. If you used the same password on other sites, change those passwords immediately. The [dangers of password reuse](/password-security/password-reuse-dangers/) are well documented, and [credential stuffing attacks](/data-breaches/credential-stuffing/) specifically exploit this vulnerability.

6. **[Check your email for breach exposure](/data-breaches/check-email-compromised/)** using [Have I Been Pwned](/data-breaches/have-i-been-pwned/) to understand the full scope of your data in criminal circulation.

7. **Enroll in the free identity monitoring** offered by Ticketmaster to affected customers.

8. **[Set up dark web monitoring](/data-breaches/dark-web-monitoring/)** for ongoing alerts about your personal information appearing in data dumps or criminal markets.

9. **Keep your devices clean**. Install software only from trusted sources, keep your operating system and browser updated, and consider using endpoint protection software. Infostealer malware was the root cause of the credentials theft that enabled this breach.

The Ticketmaster breach is a textbook example of how modern data breaches often exploit the gaps between companies rather than the companies themselves. Snowflake was not breached. Ticketmaster's own systems were not directly compromised. The vulnerability was in the authentication of the connection between the two. For users, the takeaway is consistent: use unique passwords, enable MFA everywhere, and monitor your accounts -- because you cannot control the security practices of the companies that hold your data or the platforms they depend on.

## Related Articles

- [AT&T Data Breach: What You Need to Know](/data-breaches/att-data-breach/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [Dark Web Monitoring: Is Your Data for Sale?](/data-breaches/dark-web-monitoring/)
- [The Biggest Data Breaches of 2025-2026](/data-breaches/biggest-breaches/)
