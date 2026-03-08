---
title: "National Public Data Breach: Lessons"
description: "Analysis of the 2024 National Public Data breach that exposed 2.9 billion records including SSNs for most Americans from a data broker."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Data Breaches & Identity"
faq:
  - question: "How many records were exposed in the National Public Data breach?"
    answer: "The threat actor claimed to have 2.9 billion records containing personal information for approximately 170 million unique individuals. The dataset included current and historical records, meaning some people appeared multiple times with different addresses spanning decades."
  - question: "What data was in the National Public Data breach?"
    answer: "The exposed data included full names, Social Security numbers, dates of birth, current and historical home addresses (spanning decades), phone numbers, and in some cases email addresses. This comprehensive dataset could fuel identity theft for years."
  - question: "What is National Public Data?"
    answer: "National Public Data (also known as Jerico Pictures) was a data broker that compiled and sold background check information. It aggregated public records, court records, and other data sources to build detailed profiles on hundreds of millions of Americans."
  - question: "Did I know National Public Data had my data?"
    answer: "Almost certainly not. Data brokers like National Public Data compile information from public records, court filings, and other sources without directly notifying the individuals in their databases. Most people affected by this breach had never heard of the company."
  - question: "What happened to National Public Data after the breach?"
    answer: "National Public Data filed for Chapter 11 bankruptcy in October 2024, citing the financial burden of the breach, class action lawsuits, and state regulatory investigations. The company had estimated annual revenue of only about $75,000, making it unable to handle the costs of breach response."
---

The National Public Data breach of 2024 exposed a hidden reality of the digital economy: a small data broker that most people had never heard of held detailed personal information -- including Social Security numbers -- for the majority of Americans. When that data broker was breached and 2.9 billion records were leaked, the incident laid bare the shadow data industry where companies compile, buy, sell, and sometimes lose the personal details of hundreds of millions of people without their knowledge or meaningful consent. As part of our [Data Breaches & Identity Protection guide](/data-breaches/), this article examines what happened, why it matters, and what you should do to protect yourself.

## What Happened: Timeline

### April 2024: Data Appears for Sale

In April 2024, a threat actor using the handle "USDoD" posted a listing on the BreachForums dark web marketplace claiming to possess a database of 2.9 billion records from "National Public Data" (also known as Jerico Pictures, Inc.), a Florida-based data broker specializing in background checks. The asking price was $3.5 million for the complete dataset.

### June 2024: Class Action Filed

On June 11, 2024, a class action lawsuit was filed against Jerico Pictures (doing business as National Public Data) in US District Court for the Southern District of Florida. The plaintiff, a California resident, alleged that he had received an alert from an identity monitoring service indicating that his personal information had been found on the dark web as part of the National Public Data breach. He had never heard of the company and had never knowingly provided it with his information.

### August 2024: Full Dataset Leaked Free

On August 6, 2024, a different threat actor posted the complete National Public Data dataset for free download on BreachForums. The free release of 2.9 billion records meant that the information was now available to anyone -- not just well-funded criminal organizations willing to pay millions, but any individual with basic technical ability.

Analysis by security researchers confirmed the dataset contained:

- Full names
- Social Security numbers
- Dates of birth
- Current and historical addresses (some individuals had address records spanning 30+ years)
- Phone numbers
- In some cases, email addresses

### October 2024: Bankruptcy

On October 2, 2024, Jerico Pictures filed for Chapter 11 bankruptcy protection. In its filing, the company disclosed annual revenue of approximately $75,000 -- a staggering figure given that it held personal data on hundreds of millions of Americans. The company stated it could not afford the costs of breach notification, legal defense, or remediation.

## What Was Exposed

### The Scale

The 2.9-billion-record claim requires context. The dataset included historical records, meaning a single person might appear multiple times with different addresses from different periods of their life. Security researchers estimated that the dataset contained information on approximately 170 million unique individuals -- roughly half the US population. Some analyses suggested the number could be higher, as the database also included records for Canadian and British individuals.

### The Data Fields

For each record:

- **Full legal name** (including middle names and historical name variants)
- **Social Security number**
- **Date of birth**
- **Home address** (current and historical, with some records showing address histories spanning decades)
- **Phone numbers** (current and historical)
- **Email addresses** (for a subset of records)
- **Relatives and associates** (linked records for family members and known associates)

### Why This Data Is Especially Dangerous

The combination of SSN, date of birth, full name, and address is the core identity package used by financial institutions, government agencies, and healthcare providers for identity verification. This dataset provides everything needed to:

- Open fraudulent credit accounts
- File fraudulent tax returns
- Obtain government benefits fraudulently
- Pass identity verification checks at banks and financial institutions
- Take over existing accounts through social engineering

The inclusion of historical address data adds another dimension of risk. Knowledge questions used for identity verification ("What address did you live at in 2015?") become useless when the attacker has a complete address history.

## How It Happened

### The Data Broker Business Model

National Public Data was a small operation that compiled background check data by aggregating public records, court records, voter registration files, and other data sources. It sold access to this information to businesses, landlords, and other parties conducting background checks.

The company's security practices appear to have been commensurate with its $75,000 annual revenue -- grossly inadequate for the sensitivity and volume of data it held. The exact technical details of the breach have not been fully disclosed, but the combination of a small company, minimal security investment, and hundreds of millions of sensitive records created an inevitable target.

### The Data Broker Ecosystem

National Public Data was not unique. Thousands of data brokers operate in the United States, aggregating and selling personal information with minimal regulatory oversight. Many of these companies are small operations with limited security budgets but massive data holdings. The National Public Data breach simply made visible what security researchers had warned about for years: the data broker ecosystem is a systemic vulnerability in American data security.

### No Direct Relationship with Victims

Perhaps the most troubling aspect of this breach is that the vast majority of affected individuals never consented to National Public Data having their information. They never created an account, never agreed to terms of service, and never knew the company existed. Their data was compiled from public sources and aggregated into a comprehensive database without their direct involvement.

This distinguishes the National Public Data breach from breaches at companies like [T-Mobile](/data-breaches/tmobile-data-breach/) or [Ticketmaster](/data-breaches/ticketmaster-data-breach/), where affected individuals at least had a customer relationship with the breached entity. Here, the victims had no relationship with the company and no ability to proactively protect their information.

## Impact

### Universal SSN Exposure

Security experts had long warned that, between the [Equifax breach](/data-breaches/equifax-breach-lessons/) (147 million SSNs), various healthcare breaches, and smaller incidents, most Americans should assume their SSN was already compromised. The National Public Data breach essentially confirmed this assumption for everyone who had not already been affected.

The practical implication: Social Security numbers should be treated as public information for security purposes. Any system that relies on SSN knowledge as proof of identity is fundamentally broken.

### Identity Theft at Scale

The free availability of the complete dataset lowered the barrier for identity theft to essentially zero. Previously, buying large databases required operating in specialized criminal markets and paying significant sums. After August 2024, anyone could download comprehensive identity data for 170 million Americans at no cost.

### Bankruptcy and Accountability Gaps

National Public Data's bankruptcy filing exposed a troubling gap in accountability. A company with $75,000 in annual revenue held data on 170 million people and, when that data was breached, had no resources to notify victims, provide remediation, or compensate for harm. The class action lawsuit faces the challenge of collecting from a bankrupt entity with minimal assets.

This pattern of small data brokers holding massive datasets with inadequate resources for breach response represents a systemic risk that current regulations are not designed to address.

## Lessons for Users

### Lesson 1: Companies You Have Never Heard of Hold Your Data

The data broker ecosystem means your personal information exists in databases you never agreed to and companies you have never heard of. You cannot control this through careful online behavior or privacy settings -- the data is compiled from public records and other sources regardless of your actions.

### Lesson 2: SSNs Are No Longer Secret

Between the Equifax breach, the National Public Data breach, and numerous other incidents, Social Security numbers for the majority of Americans are in criminal circulation. Any security system that relies on SSN knowledge for verification is essentially using a compromised credential. Credit freezes are the primary defense against this reality.

### Lesson 3: Data Minimization Matters

The National Public Data breach illustrates why data minimization (limiting the amount of personal information collected and retained) is a fundamental security principle. A company that holds data on 170 million people should have security proportional to that responsibility. When it does not, the consequences are borne by the individuals whose data is exposed.

### Lesson 4: Proactive Monitoring Is Essential

Because you cannot know which companies hold your data or when they might be breached, proactive monitoring is essential. [Breach notification services](/data-breaches/have-i-been-pwned/), [dark web monitoring](/data-breaches/dark-web-monitoring/), and credit monitoring provide the earliest possible warning of data misuse.

## How to Protect Yourself

Given the scale of this breach, every American should take protective measures whether or not they were specifically notified:

1. **[Freeze your credit immediately](/data-breaches/freeze-credit/)** at all three major bureaus: Equifax, Experian, and TransUnion. Also freeze at Innovis, NCTUE, and ChexSystems. A credit freeze is the single most effective defense against identity theft using stolen SSNs.

2. **Set up an IRS Identity Protection PIN** to prevent fraudulent tax filings. Visit irs.gov/ippin to enroll.

3. **Use unique, strong passwords for every account**. With your personal details in wide circulation, [credential stuffing](/data-breaches/credential-stuffing/) and social engineering attacks become more dangerous. A password manager like PanicVault generates unique passwords for every site and stores them in an encrypted local vault on your Apple devices using the KeePass format. Your passwords never reside on a third-party server.

4. **Enable multi-factor authentication** on all accounts, prioritizing financial accounts, email, and government services.

5. **[Check your breach exposure](/data-breaches/check-email-compromised/)** using [Have I Been Pwned](/data-breaches/have-i-been-pwned/) and the National Public Data breach checker tools that security researchers have published.

6. **Monitor all financial accounts** with transaction alerts. Set up notifications for any new account openings.

7. **Request your free annual credit report** from AnnualCreditReport.com and review it for unfamiliar accounts or inquiries.

8. **[Set up dark web monitoring](/data-breaches/dark-web-monitoring/)** for your SSN, email address, and phone number.

9. **File taxes early** each year to prevent criminals from filing fraudulent returns using your SSN.

10. **Opt out of data brokers** where possible. Services like DeleteMe and Privacy Duck can help remove your information from data broker databases, reducing future exposure. While this does not recall already-breached data, it limits ongoing collection.

11. **Be vigilant about social engineering**. With complete address histories, phone numbers, and family connections available, attackers can craft highly convincing impersonation attempts. Verify the identity of anyone who contacts you claiming to be from a bank, government agency, or other institution.

The National Public Data breach is a milestone in the erosion of personal data privacy in America. When a company most people never knew existed can lose the Social Security numbers of 170 million people and then go bankrupt without providing meaningful remediation, the system has failed. The only reliable defense is the one you build yourself: credit freezes, unique passwords, MFA, and constant vigilance.

## Related Articles

- [How to Freeze Your Credit (and Why You Should)](/data-breaches/freeze-credit/)
- [Equifax Breach: Lasting Lessons](/data-breaches/equifax-breach-lessons/)
- [Identity Theft Recovery: A Step-by-Step Guide](/data-breaches/identity-theft-recovery/)
- [Check If Your Email Has Been Compromised](/data-breaches/check-email-compromised/)
- [The Biggest Data Breaches of 2025-2026](/data-breaches/biggest-breaches/)
