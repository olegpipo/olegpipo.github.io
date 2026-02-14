---
title: "The California DELETE Act: What It Means"
description: "How the California DELETE Act changes data privacy for consumers, its implications for personal security and password management, and what you should do to take advantage of your new rights."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Trends & Future"
---

The California Delete Act (SB 362), signed into law in October 2023 with full implementation rolling out through 2026, represents one of the most significant shifts in consumer data privacy in the United States. By creating a single mechanism for consumers to request deletion of their personal information from all registered data brokers, the law fundamentally changes the economics of personal data collection. For anyone thinking about [password security and authentication trends](/trends/), the implications are substantial and direct.

This is not just a privacy law. It is a security tool.

## What the DELETE Act Does

### The Data Broker Problem

Data brokers are companies that collect, aggregate, and sell personal information about consumers. They compile data from public records, commercial transactions, social media, and other sources to create detailed profiles that include:

- Full name, aliases, and maiden names
- Home addresses (current and historical)
- Phone numbers and email addresses
- Family relationships and household composition
- Employment history and estimated income
- Property ownership and vehicle registration
- Social media profiles and online behavior
- Consumer preferences and purchase history

This information is sold to marketers, background check services, people-search websites, and anyone willing to pay. Before the DELETE Act, requesting deletion of your information from data brokers required individually contacting each broker -- a process so tedious that few consumers attempted it and fewer succeeded.

### The Single Deletion Mechanism

The DELETE Act's central innovation is the creation of a single, free mechanism through which California residents can request deletion of their personal information from all registered data brokers simultaneously. Rather than contacting hundreds of brokers individually, consumers submit a single request through a centralized system. All registered data brokers must honor the request within a specified timeframe.

The California Privacy Protection Agency (CPPA) is responsible for implementing and maintaining the deletion mechanism. Data brokers must register with the state and participate in the centralized system. Non-compliance carries significant penalties.

### Ongoing Obligations

The DELETE Act goes beyond one-time deletion. Data brokers who receive a deletion request must also refrain from selling or sharing the consumer's personal information going forward. This is a meaningful difference from a simple data purge -- it creates an ongoing obligation that limits future data collection and sale.

## Why This Matters for Security

### Reducing Your Attack Surface

Personal data in data broker databases is a direct enabler of [AI-powered attacks](/trends/ai-and-passwords/). The more information available about you, the more effective an attacker's social engineering, password prediction, and [phishing personalization](/trends/ai-phishing-effectiveness/).

When a data broker profile links your name to your address, phone number, family members, employer, and online accounts, it provides the raw material for:

- **Targeted phishing**: AI can craft messages that reference your real life circumstances, making them dramatically more convincing.
- **Password prediction**: Names of family members, pets, addresses, and dates that appear in data broker profiles are among the most common elements in human-created passwords.
- **Security question bypass**: Mother's maiden name, first car, childhood street -- all commonly available through data brokers and public records.
- **SIM swapping**: Phone numbers and associated personal details help attackers convince mobile carriers to port your number, enabling interception of [SMS OTP codes](/trends/sms-otp-ban/).
- **[Deepfake targeting](/trends/deepfake-as-a-service/)**: Personal information helps attackers identify valuable targets and craft convincing impersonation scenarios.

Removing your information from data broker databases directly reduces the effectiveness of these attack vectors. The DELETE Act makes this removal practical for the first time.

### The Phone Number Problem

Your phone number is one of the most sensitive pieces of information in the modern security landscape. It is used for:

- SMS-based two-factor authentication
- Account recovery for most online services
- Identity verification for financial services
- Communication that establishes trust (you recognize calls from known numbers)

Data brokers make phone numbers widely available. Anyone can search for your number on people-search websites, find it in data broker databases, and use it to target you. The DELETE Act helps by removing your phone number from these databases, reducing (though not eliminating) its exposure.

### Identity Theft Prevention

Comprehensive personal information is the raw material for identity theft. With enough data from data broker profiles, an attacker can:

- Open financial accounts in your name
- File fraudulent tax returns
- Obtain credit cards and loans
- Create synthetic identities combining your real information with fabricated elements

The DELETE Act's deletion mechanism reduces the availability of this information, making identity theft more difficult for attackers who rely on commercially available data.

## How to Use the DELETE Act

### Who Is Eligible

The DELETE Act applies to California residents. However, some data brokers honor deletion requests from residents of other states as well, partly because managing state-by-state compliance is more complex than applying a uniform standard. The law is also influencing similar legislation in other states.

### The Deletion Process

1. **Access the deletion mechanism**: The CPPA's centralized system is accessible online. You provide basic identifying information (name, email, phone number) to generate deletion requests.

2. **Submit your request**: A single submission triggers deletion requests to all registered data brokers.

3. **Wait for processing**: Data brokers have a specified timeframe to process deletion requests. The timeline varies but is typically 30-45 days.

4. **Verify deletion**: After the processing period, check major people-search websites to verify that your information has been removed. Some degree of re-accumulation is inevitable, so periodic re-submission may be necessary.

### Supplementary Tools

The DELETE Act is powerful but not comprehensive. Supplement it with:

- **Commercial deletion services**: Companies like DeleteMe, Privacy Duck, and Kanary specialize in data broker removal and provide ongoing monitoring. They handle brokers that may not be covered by the DELETE Act.
- **Direct opt-out requests**: Some data sources (voter registration, property records) are public records not covered by data broker regulation. Opt-out procedures vary by jurisdiction.
- **Social media privacy settings**: Review and restrict what is publicly visible on all social media platforms. Data brokers scrape public social media profiles.
- **Email aliases**: Use unique email addresses for different services to limit cross-reference capability. Apple's Hide My Email is a convenient tool for this on Apple devices.

## The Broader Privacy Landscape

### Similar Legislation

The DELETE Act is part of a broader trend toward consumer data protection:

- **GDPR** (EU): The right to erasure under GDPR predated the DELETE Act and provides similar (in some ways stronger) protections for EU residents.
- **CCPA/CPRA** (California): The DELETE Act builds on the existing California Consumer Privacy Act, which established data access and deletion rights.
- **State privacy laws**: Connecticut, Virginia, Colorado, and other states have enacted privacy laws with varying deletion rights.
- **Federal proposals**: Multiple federal privacy bills have been proposed, though none has been enacted as of 2026.

### Limitations

The DELETE Act is not a complete solution:

- It applies only to registered data brokers. Data held by companies that are not classified as data brokers (social media platforms, retailers, service providers) is not covered.
- Public records remain accessible. Government databases (property records, court records, voter registration) are generally exempt.
- Data re-accumulation occurs. Even after deletion, data brokers may re-acquire your information from other sources. Periodic re-submission of deletion requests is necessary.
- Enforcement is dependent on regulatory resources. The CPPA must monitor compliance across hundreds of data brokers.

## The Connection to Password Management

The DELETE Act's privacy protections complement good [password management](/password-managers/) practices. Together, they create a layered defense:

**Layer 1: Data minimization (DELETE Act)** -- Remove your personal information from data broker databases, reducing the raw material available for attacks.

**Layer 2: Strong credential management** -- Use a password manager with randomly generated, unique passwords for every account. The less personal information available to attackers, the less effective password prediction becomes -- but random passwords are the ultimate defense regardless.

**Layer 3: Phishing-resistant authentication** -- [Passkeys](/passkeys/) and hardware security keys prevent credential theft even if an attacker successfully crafts a convincing phishing message using whatever personal data they have.

**Layer 4: Data portability** -- Use credential storage that you control. The [KeePass KDBX format](/keepass/) used by PanicVault keeps your passwords in an encrypted file on your own device. No cloud service has access to your credentials, and no data broker can sell information about your password management habits.

This layered approach embodies the [zero trust principle](/trends/zero-trust-individuals/): do not trust that any single defense is sufficient. Privacy protection, strong credentials, phishing-resistant authentication, and data ownership each provide value independently, and together they create a security posture that is resilient against the evolving [threat landscape](/trends/state-of-password-security/).

## Practical Recommendations

### Immediate Actions

1. **Submit a DELETE Act request** through the CPPA's centralized system if you are a California resident.
2. **Search for yourself** on major people-search websites (Spokeo, BeenVerified, WhitePages, Intelius) to understand your current data exposure.
3. **Review and restrict** your social media privacy settings across all platforms.
4. **Enable Hide My Email** or use email aliases for new account registrations.

### Ongoing Practices

1. **Re-submit deletion requests** quarterly. Data re-accumulation is ongoing.
2. **Monitor data broker listings** periodically to verify deletion.
3. **Minimize new data exposure** by being deliberate about what information you share online and with services.
4. **Use a password manager** that generates random passwords, eliminating the connection between your personal information and your credentials.

### For Non-California Residents

Even if you are not a California resident:
- Many data brokers honor deletion requests regardless of state
- Check if your state has privacy legislation with deletion rights
- Use commercial deletion services that operate nationally
- Apply the same data minimization principles proactively

The DELETE Act represents a shift in the balance of power between consumers and the data economy. For security-conscious individuals, it is a tool that directly reduces attack surface. Combined with strong credential management through tools like PanicVault and the [KeePass ecosystem](/keepass/), it contributes to a security posture that is both private and resilient.

## Related Articles

- [Privacy in the Age of AI](/trends/privacy-age-of-ai/)
- [How AI Makes Phishing 400% More Effective](/trends/ai-phishing-effectiveness/)
- [Zero Trust Security for Individuals](/trends/zero-trust-individuals/)
- [The State of Password Security in 2026](/trends/state-of-password-security/)
- [Deepfake-as-a-Service: What It Means for Security](/trends/deepfake-as-a-service/)
