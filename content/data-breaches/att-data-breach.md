---
title: "AT&T Data Breach: What to Know"
description: "Analysis of the 2024 AT&T data breaches that exposed 73 million customer records and call metadata for 110 million subscribers."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Data Breaches & Identity"
faq:
  - question: "How many people were affected by the AT&T data breach?"
    answer: "AT&T disclosed two major breaches in 2024. The first exposed personal data for approximately 73 million current and former customers. The second exposed call and text metadata for roughly 110 million wireless subscribers."
  - question: "What data was exposed in the AT&T breach?"
    answer: "The first breach exposed Social Security numbers, account numbers, passcodes, names, addresses, dates of birth, and email addresses. The second breach exposed call and text metadata including phone numbers called, call durations, and timestamps."
  - question: "How did the AT&T data breach happen?"
    answer: "The first breach involved data from 2019 or earlier that surfaced on the dark web. The second breach resulted from unauthorized access to AT&T's Snowflake cloud data platform account, part of a broader campaign targeting multiple Snowflake customers."
  - question: "Is my data from AT&T on the dark web?"
    answer: "If you were an AT&T customer before 2021, your data may have been exposed. AT&T offered credit monitoring to affected customers. You can check your exposure using breach notification tools like Have I Been Pwned."
  - question: "What should AT&T customers do after the breach?"
    answer: "Change your AT&T account password and passcode, enable multi-factor authentication, freeze your credit at all three bureaus, monitor financial accounts for suspicious activity, and watch for phishing attempts using your exposed information."
---

The AT&T data breaches of 2024 represent one of the most significant telecommunications security failures in recent history. Across two separate incidents, personal data for approximately 73 million customers and call metadata for roughly 110 million subscribers were compromised -- exposing Social Security numbers, account details, and intimate records of who called whom and when. As part of our [Data Breaches & Identity Protection guide](/data-breaches/), this article examines what happened, what was exposed, and what AT&T customers should do to protect themselves.

## What Happened: Timeline of the AT&T Breaches

### March 2024: 73 Million Customer Records Surface

On March 30, 2024, AT&T confirmed that a dataset containing personal information for approximately 73 million current and former customers had been published on the dark web. The data appeared to originate from 2019 or earlier, though AT&T initially struggled to determine whether the information was extracted directly from AT&T systems or from a third-party vendor.

The existence of this data had been rumored since 2021, when a threat actor known as ShinyHunters first claimed to possess AT&T customer records. AT&T denied any breach at the time. Three years later, the data was posted publicly, forcing AT&T to acknowledge the exposure and begin notifying affected customers.

### July 2024: Call Metadata for 110 Million Customers

On July 12, 2024, AT&T disclosed a second, entirely separate breach. Attackers had accessed AT&T's account on the Snowflake cloud data platform and downloaded call and text message metadata for nearly all AT&T wireless customers -- approximately 110 million people. The stolen data covered a period from May 1 to October 31, 2022, with a smaller subset from January 2, 2023.

This breach was part of a broader campaign targeting Snowflake customers. The attackers used stolen credentials to access Snowflake accounts that lacked multi-factor authentication. AT&T was one of dozens of companies affected, alongside [Ticketmaster](/data-breaches/ticketmaster-data-breach/) and others.

AT&T reportedly paid a member of the hacking group approximately $370,000 in Bitcoin to delete the stolen data, though security experts noted that there is no reliable way to verify deletion of digital information.

### Ongoing Legal Fallout

Multiple class action lawsuits were filed against AT&T following both disclosures. The Federal Communications Commission opened an investigation into the company's data security practices. State attorneys general launched their own inquiries. The financial and reputational costs continued to mount through 2025 and into 2026.

## What Was Exposed

### First Breach: Personal Identification Data

The March 2024 dataset included:

- **Social Security numbers** for approximately 7.6 million current customers and 65.4 million former customers
- **AT&T account numbers and passcodes** (numeric PINs used for account security)
- **Full names, email addresses, and mailing addresses**
- **Dates of birth and phone numbers**

The combination of Social Security numbers with names, dates of birth, and addresses is particularly dangerous. This is the precise set of information needed to open fraudulent accounts, file fraudulent tax returns, and commit [identity theft](/data-breaches/identity-theft-recovery/).

### Second Breach: Communications Metadata

The July 2024 breach exposed:

- **Phone numbers of calls made and received** by AT&T wireless customers
- **Phone numbers of text messages sent and received**
- **Call durations and timestamps**
- **Cell site identification numbers** (which can approximate a user's location)

While the actual content of calls and texts was not exposed, metadata is extraordinarily revealing. It shows who you communicate with, how often, for how long, and from where. This information can reveal personal relationships, business dealings, medical consultations, political affiliations, and daily movement patterns.

## How It Happened

### The Dark Web Dataset

The origin of the first breach remains partially unclear. AT&T stated that the data appeared to come from 2019 or earlier but could not definitively confirm whether it was extracted from their own systems or from a vendor. The three-year gap between the data's first appearance in hacking forums (2021) and AT&T's public acknowledgment (2024) raised serious questions about the company's breach detection and disclosure practices.

### The Snowflake Campaign

The second breach had a clearer attack chain. A group of hackers, subsequently identified and partially apprehended by law enforcement, targeted companies that stored data on Snowflake's cloud data platform. The attackers obtained credentials -- in many cases through [credential stuffing](/data-breaches/credential-stuffing/) or infostealer malware on employee machines -- and used them to access Snowflake accounts that had not enabled multi-factor authentication.

Snowflake itself was not breached. Rather, individual customer accounts were compromised because they relied solely on username-and-password authentication. AT&T's Snowflake account was one of approximately 165 accounts accessed by the attackers.

This attack pattern highlights a recurring theme in modern breaches: the compromise of cloud platforms through stolen credentials and absent MFA. The data may reside in sophisticated cloud infrastructure, but access is only as secure as the authentication protecting it.

## Impact on Customers

### Identity Theft Risk

For the 73 million customers whose Social Security numbers were exposed, the risk of identity theft is long-term and serious. SSNs cannot be changed in most circumstances. The exposed data provides everything a criminal needs to open credit cards, take out loans, or file fraudulent tax returns in a victim's name.

### Targeted Phishing and Social Engineering

With detailed personal information and communication patterns available, affected customers face elevated risk of sophisticated phishing attacks. An attacker who knows your phone number, address, who you call regularly, and your AT&T account details can craft highly convincing social engineering attempts.

### Privacy Implications of Metadata

The call and text metadata exposure affected a far larger group. Journalists, activists, domestic violence survivors, business executives, healthcare providers, and ordinary citizens all had their communication patterns exposed. For certain populations, the revelation of who they communicate with could have serious personal or professional consequences.

## What AT&T Did in Response

AT&T took several steps following the disclosures:

- **Reset passcodes** for 7.6 million affected current customers
- **Offered credit monitoring** through Experian for affected individuals
- **Notified affected customers** via email, mail, and account notifications
- **Enhanced security** on its Snowflake and other cloud platform accounts, including implementing MFA
- **Cooperated with law enforcement**, leading to arrests of individuals connected to the Snowflake campaign

Critics noted that AT&T's response to the first breach was delayed by years and that the company's initial denial in 2021 prevented customers from taking protective steps sooner. The second breach was also reported with a significant delay -- AT&T learned of it in April 2024 but did not disclose it publicly until July, after obtaining a delay from the Department of Justice related to national security concerns.

## Lessons for Users

### Lesson 1: Telecom Data Is a High-Value Target

Telecommunications companies hold extraordinary volumes of sensitive data. Beyond basic personal information, they possess records of every call and text, location data, billing information, and account credentials. This makes them prime targets for sophisticated attackers.

### Lesson 2: Cloud Security Depends on Access Controls

The Snowflake-linked breach was not caused by a vulnerability in the cloud platform itself but by weak access controls on AT&T's account. Multi-factor authentication would have blocked the attack entirely. This pattern appears repeatedly across major breaches, including the [Change Healthcare incident](/data-breaches/change-healthcare-breach/).

### Lesson 3: Metadata Is More Revealing Than People Think

Many people dismissing the call metadata breach as less serious than the SSN breach underestimated the sensitivity of communications metadata. Intelligence agencies consider metadata analysis one of their most powerful tools for a reason -- it reveals the structure of your entire life without needing to hear a single word.

### Lesson 4: Corporate Denial Delays Your Response

AT&T's denial of the first breach in 2021 meant that affected customers went three years without taking protective action. When a company claims "no evidence of breach" while your data circulates in hacking forums, you lose valuable time to freeze credit, change passwords, and monitor accounts.

## How to Protect Yourself

If you are or were an AT&T customer, take these steps:

1. **[Freeze your credit](/data-breaches/freeze-credit/)** at Equifax, Experian, and TransUnion. A credit freeze is the single most effective defense against identity theft using stolen SSNs. It is free and does not affect your credit score.

2. **Change your AT&T account password and passcode** immediately. Use a unique, randomly generated password stored in a password manager like PanicVault. Never reuse passwords across services -- the [dangers of password reuse](/password-security/password-reuse-dangers/) are well documented.

3. **Enable multi-factor authentication** on your AT&T account and every other account that supports it. Use an authenticator app or hardware key rather than SMS-based verification, especially given that your phone number may have been compromised.

4. **[Check whether your email has been compromised](/data-breaches/check-email-compromised/)** in this or other breaches using services like [Have I Been Pwned](/data-breaches/have-i-been-pwned/).

5. **Monitor your financial accounts** for unauthorized transactions. Set up alerts for new account openings through your bank and credit monitoring services.

6. **Watch for phishing attempts** that reference your AT&T account, personal details, or recent communications. Attackers will use the stolen data to craft convincing scams.

7. **Use a password manager** to generate and store unique passwords for every account. PanicVault uses the open KeePass format and stores your vault locally on your Apple devices -- never on a third-party server that could be breached. This local-first approach means that even if PanicVault's company were compromised, your passwords would remain secure on your own devices.

8. **Set up [dark web monitoring](/data-breaches/dark-web-monitoring/)** to receive alerts if your personal information appears in new data dumps.

The AT&T breaches illustrate a difficult truth: even as a customer, you cannot control how companies store and protect your data. What you can control is your response -- freezing credit, using unique passwords, enabling MFA, and monitoring for misuse. Taking these steps will not undo the breach, but they significantly reduce the likelihood that exposed data translates into real harm.

## Related Articles

- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [Ticketmaster Data Breach: What Happened and What to Do](/data-breaches/ticketmaster-data-breach/)
- [How to Freeze Your Credit (and Why You Should)](/data-breaches/freeze-credit/)
- [Credential Stuffing: How One Password Compromises All](/data-breaches/credential-stuffing/)
- [The Biggest Data Breaches of 2025-2026](/data-breaches/biggest-breaches/)
