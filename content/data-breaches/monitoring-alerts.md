---
title: "How to Set Up Identity Theft Monitoring"
description: "Practical guide to setting up identity theft monitoring -- free and paid options, what to monitor, how to configure alerts, and how to respond when they fire."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Data Breaches & Identity"
---

Identity theft monitoring is the practice of systematically watching for signs that your personal information is being misused. It ranges from free email breach notifications to comprehensive paid services that monitor credit bureaus, dark web marketplaces, and public records. The goal is early detection -- catching unauthorized use of your identity before it causes serious damage. This guide, part of our [Data Breaches & Identity Protection](/data-breaches/) resource center, walks through every monitoring layer available to you, from free essentials to premium services, and helps you build a monitoring setup that matches your risk level.

## The Monitoring Layers

Effective identity theft monitoring is not a single service -- it is a combination of tools that cover different threat vectors. Think of it as concentric rings of detection, each catching a different type of abuse.

### Layer 1: Breach Monitoring (Free)

The foundation. This layer alerts you when your credentials appear in known data breaches.

**Have I Been Pwned (HIBP)**

Register every email address you use at haveibeenpwned.com/NotifyMe. When your email appears in a newly cataloged breach, you receive an automatic notification. This is the single highest-value free security tool available. For a complete walkthrough, see our [HIBP guide](/data-breaches/have-i-been-pwned/).

**Password Manager Breach Monitoring**

Most modern [password managers](/password-managers/) include features that check your stored credentials against known breach databases:

- **1Password**: Watchtower scans your vault against HIBP and alerts you to compromised, reused, and weak passwords.
- **Bitwarden**: Vault Health Reports identify compromised passwords, reused passwords, and weak passwords.
- **PanicVault**: Works within the [Apple ecosystem's](/apple/) security monitoring to flag compromised credentials stored in your [KeePass](/keepass/) database. Because PanicVault stores your vault locally on your Apple devices or iCloud Drive rather than on a cloud server, the monitoring happens without your credential vault ever being transmitted to a third party.
- **KeePassXC**: Supports HIBP integration for checking stored passwords against breach databases.

Run these audits monthly or whenever you learn about a new major breach.

**Browser-Based Monitoring**

Firefox Monitor, Google Password Checkup, and Safari's built-in Security Recommendations all check saved passwords against breach databases. Enable whichever is relevant to your browser.

### Layer 2: Credit Monitoring (Free or Paid)

Credit monitoring watches for changes to your credit report -- new accounts, hard inquiries, address changes, and other activity that could indicate identity theft.

**Free Options**

- **AnnualCreditReport.com**: You are entitled to free credit reports from all three bureaus (Equifax, Experian, TransUnion). Request them on a rotating schedule -- one bureau every four months -- for year-round coverage.
- **Experian Free Credit Monitoring**: Experian offers free basic monitoring of your Experian credit report.
- **Credit Karma**: Free monitoring of TransUnion and Equifax reports with alerts for new accounts, inquiries, and score changes.
- **Breach notification offers**: After a major breach, affected companies often provide 1-2 years of free credit monitoring. Accept these offers -- they are typically from reputable providers like Experian IdentityWorks or AllClear ID.

**Paid Options**

Premium credit monitoring services ($10-30/month) offer:
- Real-time monitoring of all three bureaus (rather than one or two)
- Faster alerts (same-day rather than monthly)
- Score tracking and simulations
- Integration with identity theft recovery services

**Setting Up Credit Alerts**

Regardless of which monitoring service you use, configure alerts for:
- New account openings
- Hard credit inquiries
- Address changes on your credit file
- Public records (judgments, liens, bankruptcies)
- Significant balance changes on existing accounts

### Layer 3: Financial Transaction Monitoring (Free)

Your bank and credit card providers are your first line of defense against financial fraud.

**Transaction Alerts**

Set up real-time alerts on every financial account:
- All transactions above $0 (or whatever threshold makes sense for your daily spending)
- All ATM withdrawals
- All wire transfers and ACH debits
- International transactions
- Online transactions
- Card-not-present transactions

Most banks and credit card issuers offer these alerts through their mobile apps at no additional cost. Enable push notifications for the fastest response time.

**Statement Review**

Beyond automated alerts, review your full statements monthly. Look for small, unfamiliar charges -- attackers often make test transactions of $1-5 before attempting larger fraud.

### Layer 4: Government Identity Monitoring (Free)

**IRS Identity Protection PIN**

Request an IP PIN from the IRS (irs.gov/identity-theft-fraud-scams/get-an-identity-protection-pin). This six-digit PIN is required to file your tax return, preventing someone else from filing fraudulently under your SSN. It is renewed annually.

**Social Security Administration**

Create an account at ssa.gov to monitor your Social Security Statement for unauthorized earnings reported under your SSN. If someone is working using your SSN, the earnings will appear on your statement.

**USPS Informed Delivery**

Sign up for Informed Delivery at informeddelivery.usps.com. You receive daily email previews of incoming mail, which helps you detect:
- Mail you expected but did not receive (possible mail theft or address change fraud)
- Mail from institutions you have no relationship with (possible new account fraud)
- Change-of-address confirmations you did not initiate

### Layer 5: Dark Web and Comprehensive Monitoring (Paid)

[Dark web monitoring](/data-breaches/dark-web-monitoring/) services scan underground marketplaces, forums, and data dumps for your personal information. Comprehensive identity protection suites combine dark web monitoring with credit monitoring, financial monitoring, and identity theft recovery services.

**Major Providers**

- **Norton LifeLock**: Credit monitoring, dark web monitoring, SSN alerts, stolen wallet assistance, identity recovery. $12-35/month.
- **Aura**: Credit and financial monitoring, dark web monitoring, antivirus, VPN, parental controls. $12-37/month.
- **Identity Guard**: Credit monitoring, dark web monitoring, social media monitoring, recovery services. $8-25/month.
- **Experian IdentityWorks**: Credit and dark web monitoring from one of the three major bureaus. $10-25/month.

**When Paid Monitoring Makes Sense**

Paid monitoring services are most valuable when:
- Your SSN has been exposed in a breach (SSN monitoring is not available for free)
- You have been a victim of identity theft and need to watch for recurrence
- You want consolidated monitoring with a single dashboard and unified alerts
- You want identity theft insurance and recovery assistance included
- You prefer hands-off monitoring over managing multiple free services

For most people, the free layers (HIBP, credit monitoring, transaction alerts, IRS PIN) provide strong coverage. Add paid services when your risk level justifies the cost -- particularly after a breach that [exposed sensitive personal data](/data-breaches/what-hackers-steal/).

## Building Your Monitoring Stack

### Minimum Setup (Free, 30 Minutes)

This baseline protects against the most common threats:

1. Register all email addresses with [Have I Been Pwned](/data-breaches/have-i-been-pwned/) notifications
2. Enable breach monitoring in your [password manager](/password-managers/)
3. Set up transaction alerts on all bank accounts and credit cards
4. Request your free annual credit reports and review them
5. Request an IRS IP PIN

### Enhanced Setup (Free to Low Cost, 1 Hour)

Add these layers for broader coverage:

6. Sign up for Experian free credit monitoring or Credit Karma
7. Sign up for USPS Informed Delivery
8. Create a Social Security Administration online account
9. Enable login notifications on email, financial, and social media accounts
10. [Freeze your credit](/data-breaches/freeze-credit/) at all three bureaus (this is preventive, not monitoring, but it complements monitoring perfectly)

### Comprehensive Setup (Paid, 1-2 Hours)

For maximum coverage, add:

11. Subscribe to a comprehensive identity protection service
12. Enable three-bureau real-time credit monitoring
13. Set up dark web monitoring for SSN and financial account numbers
14. Consider identity theft insurance coverage

## Responding to Monitoring Alerts

Monitoring is only useful if you respond to alerts promptly and appropriately. Here is a framework for triage:

### High Priority (Respond Within Hours)

- New credit account you did not open
- Transaction you did not make
- Password breach at a service where you store financial data
- Login notification from an unrecognized device or location
- IRS notice about a tax return you did not file

**Action**: Follow the [immediate breach response checklist](/data-breaches/what-to-do-after-breach/). Contact the relevant institution directly. Document everything.

### Medium Priority (Respond Within 24-48 Hours)

- Hard credit inquiry you do not recognize
- Password breach at a non-financial service
- Dark web alert showing your email address
- Address change on your credit file you did not initiate

**Action**: Investigate the source. Change affected passwords. If the inquiry or address change is fraudulent, contact the bureau and the creditor.

### Low Priority (Respond Within a Week)

- Password breach showing only email exposure (no password data)
- Pre-approved credit offers from unfamiliar lenders (could indicate your data is circulating)
- Reused password flagged by your password manager

**Action**: Update affected passwords. Set up 2FA if not already enabled. Adjust monitoring settings if needed.

## Monitoring for Families

Identity theft affects all ages. Children and elderly family members are particularly vulnerable:

### Children

- [Freeze children's credit](/data-breaches/freeze-credit/) proactively (identity thieves target children because fraud can go undetected for years)
- Monitor for unexpected mail addressed to children from financial institutions
- Check children's SSNs against credit bureau records annually

### Elderly Family Members

- Help set up basic monitoring (transaction alerts, credit monitoring)
- Enable login notifications on their accounts
- Consider adding yourself as an authorized contact for fraud alerts
- Educate about [phishing](/phishing/) and phone scam tactics

## The Cost of Not Monitoring

The average [identity theft recovery](/data-breaches/identity-theft-recovery/) process takes between 100 and 200 hours of a victim's time, with some cases extending to [months or years](/data-breaches/recovery-timeline/). Financial losses can range from hundreds to tens of thousands of dollars, even when ultimately resolved. The emotional toll -- stress, anxiety, loss of trust -- is harder to quantify but very real.

Monitoring does not prevent breaches. No tool can. But it dramatically reduces the window between a breach and your response, and that window is what determines whether a breach becomes an inconvenience or a catastrophe.

## Related Articles

- [Have I Been Pwned? Using Free Breach-Checking Tools](/data-breaches/have-i-been-pwned/)
- [Dark Web Monitoring: What It Is and Do You Need It?](/data-breaches/dark-web-monitoring/)
- [How to Freeze Your Credit After a Data Breach](/data-breaches/freeze-credit/)
- [Identity Theft Recovery: Step-by-Step Guide](/data-breaches/identity-theft-recovery/)
- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
