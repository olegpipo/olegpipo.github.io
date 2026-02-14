---
title: "CEO Fraud and Business Email Compromise"
description: "Business email compromise (BEC) caused $2.9B in losses in 2023. Learn how CEO fraud works, why it succeeds, and how to protect your organization."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Phishing & Social Engineering"
---

Business email compromise (BEC) is the most financially devastating form of cybercrime. According to the FBI's Internet Crime Complaint Center, BEC attacks caused over $2.9 billion in reported losses in 2023 alone -- and the actual figure is likely much higher because many incidents go unreported. What makes BEC particularly dangerous is what it does not involve: no malware, no malicious attachments, no suspicious links. Just a carefully crafted email from a trusted authority figure, asking you to do something that seems perfectly reasonable. This article is part of our [Phishing & Social Engineering](/phishing/) guide.

## What Is Business Email Compromise?

BEC is a targeted [social engineering attack](/phishing/social-engineering-guide/) in which an attacker impersonates a trusted business contact -- typically an executive, vendor, lawyer, or partner -- to trick employees into transferring money, changing payment details, or sharing sensitive information.

The attacks are devastatingly simple:

1. The attacker identifies a target organization and researches its structure, key personnel, vendors, and financial processes.
2. The attacker either compromises a legitimate email account or creates a convincing lookalike address.
3. The attacker sends an email that appears to come from a trusted authority figure.
4. The recipient complies because the request seems legitimate and comes from a recognized authority.

There is nothing technically sophisticated about most BEC attacks. They succeed through psychology, not technology. The authority of the supposed sender, the reasonableness of the request, and the urgency of the timeline combine to override the skepticism that might otherwise trigger verification.

## Common BEC Attack Types

### CEO Fraud

The most recognized form. An attacker impersonates the CEO or another senior executive and sends an email to an employee in finance or accounting:

*"I need you to process a wire transfer of $47,500 to this account. It's for a confidential acquisition we're closing today. Please handle this quietly and urgently -- I'll explain in our meeting tomorrow."*

The email exploits authority (it comes from the CEO), urgency (closing today), and secrecy (handle quietly -- discouraging the employee from verifying with colleagues).

### Vendor Invoice Fraud

The attacker impersonates a vendor and sends a modified invoice with updated bank account details:

*"Please note our banking details have changed effective immediately. All future payments should be directed to the following account..."*

The invoice looks identical to previous legitimate invoices. The only change is the bank account number. Payments are redirected to the attacker's account, often for months before the fraud is discovered.

### Attorney Impersonation

The attacker poses as a lawyer handling a confidential legal matter:

*"I represent [Law Firm Name]. We are handling a time-sensitive acquisition on behalf of your CEO. I need you to process the following payment today under NDA. Your CEO has authorized this -- please do not discuss it with colleagues."*

The legal context adds gravity and the NDA request prevents the employee from seeking verification.

### Payroll Diversion

The attacker impersonates an employee and requests a change to their direct deposit information:

*"Hi [HR], I've recently changed banks. Can you update my direct deposit to route to the following account starting this pay period?"*

This redirects the employee's salary to the attacker's account. The real employee does not notice until their expected pay fails to arrive.

### Data Theft

Instead of requesting money, the attacker requests sensitive data:

*"Please send me the W-2 forms for all employees. I need them for the annual tax filing review."*

Employee tax information enables identity theft on a massive scale. These attacks typically occur during tax season.

## Why BEC Succeeds

### Authority Bias

When a request appears to come from the CEO, the CFO, or a senior partner, employees default to compliance. Questioning authority feels uncomfortable, especially in hierarchical organizations. The psychological pressure to obey is powerful -- it is the same principle that drives [social engineering](/phishing/social-engineering-guide/) across all contexts.

### Plausible Requests

BEC attacks do not ask for anything unusual in isolation. Wire transfers, invoice payments, payroll changes, and data requests are all part of normal business operations. The attacker simply inserts themselves into an existing process.

### Urgency and Confidentiality

The combination of urgency ("process today") and confidentiality ("don't discuss with anyone") is devastating. Urgency prevents the employee from taking time to verify. Confidentiality prevents them from asking a colleague who might spot the fraud.

### Compromised Accounts

In sophisticated BEC attacks, the attacker has actually compromised the executive's real email account -- through [phishing](/phishing/recognize-phishing/), [credential theft from data breaches](/data-breaches/), or other means. When the email comes from the executive's real address, it passes all the usual checks. The email thread is consistent. The writing style matches. The request arrives in the context of a genuine ongoing conversation.

### AI Enhancement

[AI-powered tools](/phishing/ai-powered-phishing/) allow attackers to mimic an executive's writing style, reference real business activities, and create contextually accurate messages. Combined with [voice cloning](/phishing/deepfake-voice-scams/), attackers can follow up a BEC email with a phone call from what sounds like the executive's own voice, confirming the request.

## Real-World BEC Examples

### Ubiquiti Networks ($46.7 Million)

In 2015, Ubiquiti Networks disclosed that it lost $46.7 million through a BEC attack. Attackers impersonated company executives and targeted employees at the company's finance department, requesting wire transfers to overseas accounts.

### Crelan Bank ($75 Million)

Belgian bank Crelan lost approximately $75 million in a BEC attack where fraudsters impersonated a senior executive and convinced employees to transfer funds over an extended period.

### Toyota Boshoku ($37 Million)

In 2019, a Toyota subsidiary was defrauded of $37 million when attackers impersonated a business partner and convinced a finance executive to change bank account information for a wire transfer.

These are not small companies with lax security. They are large, sophisticated organizations with existing security controls. BEC attacks succeed because they target human psychology, not technical vulnerabilities.

## How to Protect Your Organization

### Verification Procedures

The single most effective defense against BEC is a mandatory verification procedure for financial transactions:

- **Out-of-band verification**: Any request for wire transfers, bank account changes, or payments above a threshold must be verified through a communication channel different from the one the request arrived on. If the request came by email, verify by phone. If it came by phone, verify by email or in person.
- **Call-back verification**: Call the requester using a phone number from your organization's directory -- not a number provided in the email.
- **Multi-person approval**: Require two or more people to approve financial transactions above a certain amount.
- **No exception for authority**: The verification procedure applies to everyone, including the CEO. If the CEO wants a wire transfer, the finance team verifies it just as they would for anyone else. A CEO who objects to this policy is undermining the organization's security.

### Email Authentication

Implement email authentication protocols to prevent domain spoofing:

- **SPF (Sender Policy Framework)**: Specifies which mail servers are authorized to send email on behalf of your domain.
- **DKIM (DomainKeys Identified Mail)**: Adds a digital signature to outgoing emails that verifies they have not been altered.
- **DMARC (Domain-based Message Authentication, Reporting, and Conformance)**: Tells receiving mail servers what to do when SPF or DKIM checks fail -- typically reject or quarantine the email.

These protocols prevent attackers from spoofing your exact domain. They do not prevent lookalike domains (e.g., "company-inc.com" vs. "companyinc.com"), so employee awareness remains essential.

### Password Security

Compromised email accounts are a primary enabler of BEC. Protect executive and finance team email accounts with:

- **[Password managers](/password-managers/)** for strong, unique passwords on every account. Deploying a password manager organization-wide -- such as PanicVault for Apple-equipped teams -- ensures that no employee uses a weak or reused password that could be compromised through a [data breach](/data-breaches/) or [fake login page](/phishing/fake-login-pages/).
- **[Two-factor authentication](/two-factor-authentication/)** on all email accounts, with hardware security keys or [passkeys](/passkeys/) preferred over SMS-based 2FA.
- **[Strong password policies](/password-security/)** that require sufficient length and complexity.

### Security Awareness Training

Regular training that includes BEC scenarios:

- **Simulated BEC exercises**: Send simulated BEC emails to employees and measure response rates. This is not about catching people doing wrong -- it is about building recognition habits.
- **Real-world case studies**: Share examples of BEC attacks, including the ones that affected major companies. Abstract warnings are less effective than concrete stories.
- **Procedure reinforcement**: Regularly remind employees of verification procedures and make it clear that following the procedure is always correct, even when it slows things down.

### Technical Controls

- **Email flagging**: Configure email systems to flag messages from external senders, especially those with display names matching internal employees. A warning banner like "This email is from an external sender" on messages that display an executive's name but originate from outside the organization is a simple and effective control.
- **Domain monitoring**: Monitor for newly registered domains that are similar to your company's domain. Attackers often register lookalike domains in advance of a BEC campaign.
- **Account monitoring**: Monitor executive email accounts for unusual activity -- unexpected forwarding rules, login from unfamiliar locations, mass data access.

### Incident Response

Have a documented plan for when a BEC attack is detected or suspected:

1. **Stop the transfer**: Contact the bank immediately to freeze or reverse the wire transfer. Speed is critical -- once funds are transferred internationally, recovery becomes extremely difficult.
2. **Preserve evidence**: Save the fraudulent email, including full headers. Do not delete anything.
3. **Notify law enforcement**: Report to the FBI's IC3 at ic3.gov and local law enforcement.
4. **Investigate the compromise**: Determine whether an email account was compromised and how. Change passwords, review forwarding rules, and audit recent account activity.
5. **Communicate**: Notify affected parties (employees, vendors, customers) as appropriate.
6. **Learn**: Update procedures and training based on how the attack succeeded.

## BEC for Small Businesses

Small businesses are not immune to BEC -- they are often more vulnerable because they lack the security infrastructure and formal procedures of large organizations. A small business where the owner verbally approves payments without formal verification is an easy target.

Even small organizations should implement:

- **Written verification procedures** for any transaction above a reasonable threshold.
- **[Password managers](/password-managers/)** for all employees.
- **Two-factor authentication** on all email and financial accounts.
- **Regular discussions** about BEC tactics so employees recognize attempts.

The cost of these measures is minimal compared to the potential loss from a single successful BEC attack.

## The Human Element

BEC is ultimately a human problem. The technology is just the delivery mechanism. The attack succeeds because someone in your organization trusts an email enough to act on it without verification. The defense is building a culture where verification is not seen as distrustful or slow -- it is seen as professional and responsible.

When employees feel safe saying "I need to verify this before I process it," even to the CEO, your organization is protected. When employees feel pressured to comply without questioning, your organization is vulnerable.

Security culture starts at the top. Executives who submit to the same verification procedures they expect of their teams demonstrate that security is a shared responsibility, not an obstacle to productivity.

## Related Articles

- [What Is Social Engineering? Comprehensive Guide](/phishing/social-engineering-guide/)
- [AI-Powered Phishing in 2026: Harder to Spot](/phishing/ai-powered-phishing/)
- [Deepfake Voice Cloning Scams: How They Work](/phishing/deepfake-voice-scams/)
- [How to Recognize a Phishing Email: 10 Red Flags](/phishing/recognize-phishing/)
- [How to Report a Phishing Attempt](/phishing/report-phishing/)
