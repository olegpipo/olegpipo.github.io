---
title: "Marriott Data Breach: Lessons"
description: "Analysis of Marriott's data breaches from 2014 to 2022 -- 500 million Starwood records, passport numbers exposed, and a pattern of security failures."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Data Breaches & Identity"
faq:
  - question: "How many people were affected by the Marriott data breach?"
    answer: "The initial 2018 disclosure reported up to 500 million Starwood guest records compromised. This was later revised to approximately 383 million unique records. Subsequent breaches in 2020 and 2022 affected additional guests, though at smaller scale."
  - question: "What data was stolen in the Marriott breach?"
    answer: "The primary breach exposed names, passport numbers, email and mailing addresses, phone numbers, dates of birth, Starwood Preferred Guest account numbers, arrival and departure dates, reservation details, and some encrypted payment card numbers. The breadth of data was unusually comprehensive."
  - question: "How long was Marriott breached before detection?"
    answer: "The breach of Starwood's reservation system began in 2014 and was not detected until September 2018 -- approximately four years of unauthorized access. This remains one of the longest undetected breaches in corporate history."
  - question: "Were passport numbers really stolen in the Marriott breach?"
    answer: "Yes. Approximately 5.25 million unencrypted passport numbers and approximately 20.3 million encrypted passport numbers were compromised. Passport numbers are particularly valuable for identity theft, fraud, and potentially state-sponsored intelligence gathering."
  - question: "Has Marriott been breached more than once?"
    answer: "Yes. In addition to the massive 2014-2018 Starwood breach, Marriott disclosed breaches in January 2020 (5.2 million guest records accessed through compromised employee credentials) and in mid-2022 (approximately 20 GB of data stolen through social engineering of a hotel employee)."
---

The Marriott data breach saga is a case study in how acquisition blind spots, prolonged undetected intrusions, and repeated security failures can compound into a crisis affecting hundreds of millions of people. The primary breach -- which began in the Starwood hotel reservation system in 2014 and went undetected for four years -- exposed approximately 383 million guest records, including passport numbers and travel histories. Subsequent breaches in 2020 and 2022 demonstrated that Marriott had not resolved its systemic security problems even after the first catastrophic incident. As part of our [Data Breaches & Identity Protection guide](/data-breaches/), this article examines the full scope of Marriott's security failures and what travelers should learn from them.

## What Happened: Timeline

### 2014: The Breach Begins

In 2014, attackers compromised the Starwood Hotels reservation database. Starwood, which operated brands including W Hotels, Sheraton, Westin, St. Regis, and Le Meridien, maintained a centralized guest reservation system that stored detailed records for millions of travelers worldwide.

The attackers installed a Remote Access Trojan (RAT) and a tool called Mimikatz (used to harvest credentials from memory) on Starwood's systems. These tools gave the attackers persistent, deep access to the reservation database and the ability to extract data over an extended period.

### September 2016: Marriott Acquires Starwood

In September 2016, Marriott International completed its $13.6 billion acquisition of Starwood Hotels & Resorts, creating the world's largest hotel company. The acquisition brought Starwood's brands, properties, loyalty program, and technology infrastructure -- including the compromised reservation system -- under Marriott's umbrella.

Marriott's pre-acquisition due diligence did not detect the ongoing breach. The attackers continued to operate within the Starwood systems throughout the acquisition process and for two more years afterward.

### September 8, 2018: Detection

On September 8, 2018, Marriott's internal security tool flagged an alert related to an attempt to access the Starwood guest reservation database. Investigation of this alert led to the discovery of the four-year-old breach.

The discovery was triggered not by sophisticated threat hunting but by a routine security alert. The fact that attackers had operated within the system for four years without detection underscores the inadequacy of Starwood's and subsequently Marriott's security monitoring.

### November 30, 2018: Public Disclosure

On November 30, 2018, Marriott publicly disclosed the breach, initially reporting that up to 500 million guest records from the Starwood reservation system had been compromised. The number was later revised to approximately 383 million unique records.

### January 2020: Second Breach

In January 2020, Marriott disclosed a second, unrelated breach. Attackers had used the login credentials of two employees at a franchise property to access approximately 5.2 million guest records. The compromised data included names, addresses, phone numbers, loyalty account numbers, dates of birth, and travel preferences.

This breach was smaller in scale but significant in what it revealed: Marriott's security improvements following the 2018 disclosure were insufficient to prevent a straightforward credential-based attack at a franchise property.

### June 2022: Third Breach

In mid-2022, a threat group used social engineering to trick an employee at the BWI Airport Marriott in Maryland into providing access to internal systems. The attackers obtained approximately 20 GB of data, including credit card information, internal business documents, and guest information.

The group behind the attack was identified as being connected to the broader wave of social engineering attacks targeting hospitality and technology companies during this period.

## What Was Exposed

### The Primary Breach (2014-2018)

The Starwood reservation database contained extraordinarily detailed guest information:

- **Names and contact information**: Mailing addresses, phone numbers, email addresses
- **Passport numbers**: Approximately 5.25 million unencrypted and 20.3 million encrypted passport numbers
- **Dates of birth**
- **Starwood Preferred Guest (SPG) account information**: Account numbers, points balances, earning and spending history
- **Reservation details**: Arrival and departure dates, room types, special requests, travel companion information
- **Payment card information**: Encrypted credit card numbers and expiration dates (Marriott stated that the encryption keys may also have been compromised)
- **Communication preferences and affiliated companies**

### Why Travel Data Is Uniquely Sensitive

Hotel reservation data reveals patterns of movement, travel companions, and personal habits. For business travelers, it exposes corporate travel patterns, meeting locations, and client relationships. For government officials and diplomats, it reveals travel schedules and locations that are inherently sensitive from a national security perspective.

The exposure of passport numbers was particularly alarming. Passport numbers, combined with names and dates of birth, can be used to:

- Create forged travel documents
- Commit identity fraud in international transactions
- Track individuals' international travel (in conjunction with other intelligence)
- Obtain visa and travel permissions fraudulently

The breach was widely attributed to Chinese state-sponsored hackers, though Marriott and official sources were cautious about formal attribution. If accurate, the intelligence value of detailed travel records and passport numbers for hundreds of millions of international travelers would be enormous.

## How It Happened

### The Pre-Acquisition Blind Spot

The most significant systemic failure was the lack of thorough security assessment during Marriott's acquisition of Starwood. A comprehensive security audit of Starwood's systems would likely have detected the RAT and Mimikatz tools that had been present since 2014. Instead, Marriott absorbed the compromised infrastructure into its operations.

This is not just a Marriott-specific problem. Mergers and acquisitions frequently involve inheriting the target company's security vulnerabilities along with its assets. The Marriott case is the most dramatic example of this risk, but it occurs across industries.

### Four Years Without Detection

The attackers operated within Starwood's systems from 2014 to 2018 without triggering alerts. This extended dwell time points to multiple failures:

- **Insufficient monitoring** of database access patterns
- **Lack of data loss prevention** tools that would detect large-scale data exfiltration
- **Inadequate endpoint detection** that should have identified the RAT and Mimikatz tools
- **Poor network segmentation** that allowed persistent lateral movement

### Franchise Model Weaknesses

The 2020 breach exploited a weakness inherent in Marriott's franchise model. Franchise properties operate semi-independently, with their own staff and, in many cases, their own IT infrastructure. Employee credentials at a franchise property provided access to the central guest database -- a security architecture that created thousands of potential entry points.

## Impact

### Regulatory Penalties

In October 2020, the UK's Information Commissioner's Office (ICO) fined Marriott approximately $23.8 million (18.4 million GBP) under GDPR for the breach. The fine was originally proposed at $123 million but was reduced due to Marriott's cooperation and the economic impact of COVID-19.

US state attorneys general reached a $52 million settlement with Marriott in 2024, covering data protection claims from all 50 states.

### Guest Impact

For the hundreds of millions of affected guests:

- **Passport holders** faced the need to determine whether their passport numbers were in the compromised set and potentially renew passports early
- **Loyalty program members** had to secure their SPG/Marriott Bonvoy accounts against unauthorized access
- **Business travelers** had their corporate travel patterns exposed
- **All affected guests** faced ongoing identity theft risk from the combination of personal data, payment information, and identification numbers

### Industry Impact

The Marriott breach raised awareness of cybersecurity risk in mergers and acquisitions. Security due diligence during acquisitions, previously an afterthought, became a more prominent part of deal evaluation across industries. The concept of "inheriting a breach" entered the mainstream vocabulary of corporate risk management.

## Lessons for Users

### Lesson 1: Hotels Know Everything About You

Hotel reservation systems store an extraordinarily detailed picture of your life: where you travel, when, with whom, your preferences, your payment methods, and your identification documents. This data persists in hotel systems for years and, as the Marriott case showed, may be silently accessed by attackers for extended periods.

### Lesson 2: Passport Number Exposure Is Serious

If your passport number was exposed, consider whether to renew your passport early. While passport numbers alone are insufficient for most types of fraud, combined with other personal information (name, date of birth, nationality), they increase the risk of identity fraud in international contexts.

### Lesson 3: Loyalty Programs Expand Your Attack Surface

Travel loyalty programs connect your identity, travel patterns, payment methods, and personal preferences in a single account. Securing these accounts with unique passwords and MFA is essential. A compromised loyalty account reveals not just points balances but detailed behavioral profiles.

### Lesson 4: Acquisitions Create Security Gaps

When companies merge, their security postures do not automatically align. The Marriott-Starwood case is an extreme example, but security integration challenges are common in acquisitions. As a customer, you have no visibility into these transitions, which is why personal security measures remain essential regardless of the companies you patronize.

## How to Protect Yourself

If you stayed at a Starwood or Marriott property between 2014 and 2018, or were affected by the 2020 or 2022 breaches:

1. **Change your Marriott Bonvoy password** to a unique, randomly generated password. Use a password manager like PanicVault to generate and store strong passwords for every travel and hospitality account. PanicVault uses the KeePass format and stores your vault locally on your Apple devices -- your hotel and travel credentials never reside on a company's servers.

2. **Enable MFA on your Marriott Bonvoy account** and any other hotel loyalty programs you use.

3. **Check if your passport number was exposed** through Marriott's breach notification tools. If it was, consider applying for a new passport, especially if you travel internationally frequently.

4. **[Freeze your credit](/data-breaches/freeze-credit/)** at all three major bureaus if you have not already, particularly if the breach exposed your name, date of birth, and address.

5. **Monitor your payment cards** that were used at Starwood or Marriott properties during the breach period. Consider requesting new card numbers from your bank.

6. **[Check your breach exposure](/data-breaches/check-email-compromised/)** using [Have I Been Pwned](/data-breaches/have-i-been-pwned/) to understand the full scope of your personal data in circulation.

7. **Be cautious with hotel booking emails**. Attackers with your travel history can send convincing phishing emails referencing past stays or upcoming reservations. Always verify communications by logging into the hotel's official website directly.

8. **Minimize the personal data you share** with hotel loyalty programs. Consider whether the benefits of a loyalty program justify the amount of personal information you provide.

9. **[Set up dark web monitoring](/data-breaches/dark-web-monitoring/)** for your email addresses, passport numbers, and other personal identifiers.

10. **Use unique passwords for every travel service** -- airlines, hotels, car rental, and booking platforms. The [dangers of password reuse](/password-security/password-reuse-dangers/) are amplified when travel services hold such comprehensive personal profiles.

The Marriott breach demonstrates that even after a company knows it has been breached, subsequent incidents can follow. The 2020 and 2022 breaches proved that the $23.8 million fine and $500+ million in breach-related costs were insufficient to prevent further security failures. For travelers, the lesson is clear: protect yourself as if every company you share data with will eventually be breached, because the historical record suggests that many of them will be.

## Related Articles

- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [Dark Web Monitoring: Is Your Data for Sale?](/data-breaches/dark-web-monitoring/)
- [How to Freeze Your Credit (and Why You Should)](/data-breaches/freeze-credit/)
- [The Dangers of Password Reuse](/password-security/password-reuse-dangers/)
- [The Biggest Data Breaches of 2025-2026](/data-breaches/biggest-breaches/)
