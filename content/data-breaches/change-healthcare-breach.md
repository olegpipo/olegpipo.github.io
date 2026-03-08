---
title: "Change Healthcare Breach: Lessons"
description: "Analysis of the 2024 Change Healthcare breach -- the largest healthcare data breach in US history, affecting 100 million people."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Data Breaches & Identity"
faq:
  - question: "How many people were affected by the Change Healthcare breach?"
    answer: "Approximately 100 million people were affected, making it the largest healthcare data breach in US history. The final number may be higher as UnitedHealth Group, Change Healthcare's parent company, continued to assess the breach's scope into 2025."
  - question: "What data was stolen in the Change Healthcare breach?"
    answer: "Stolen data included health insurance information, medical records, billing and claims data, Social Security numbers, and payment information. The exact data varied by individual depending on what Change Healthcare processed for their healthcare provider."
  - question: "Did Change Healthcare pay a ransom?"
    answer: "Yes. UnitedHealth Group confirmed paying approximately $22 million in Bitcoin to the ALPHV/BlackCat ransomware group. Despite paying the ransom, the attackers' affiliates later attempted additional extortion, and there is no guarantee the stolen data was destroyed."
  - question: "How did the Change Healthcare breach happen?"
    answer: "Attackers used stolen credentials to access a Citrix remote access portal that did not have multi-factor authentication enabled. From there, they deployed ALPHV/BlackCat ransomware and exfiltrated data over approximately nine days before encrypting systems."
  - question: "How did the Change Healthcare breach affect patients?"
    answer: "The breach disrupted healthcare operations nationwide for weeks. Pharmacies could not process prescriptions, providers could not verify insurance, and claims processing halted. Some patients were unable to access medications, and healthcare providers faced severe cash flow disruptions."
---

The Change Healthcare breach of February 2024 was the largest healthcare data breach in United States history. Approximately 100 million people had their medical records, insurance information, and personal data stolen. But the breach was more than a data theft -- it was a systemic disruption that paralyzed healthcare operations across the country, preventing pharmacies from processing prescriptions, providers from verifying insurance, and hospitals from submitting claims. As part of our [Data Breaches & Identity Protection guide](/data-breaches/), this article examines how a single missing security control led to a catastrophe that affected one in three Americans.

## What Happened: Timeline

### February 21, 2024: The Attack Begins

On February 21, 2024, the ALPHV/BlackCat ransomware group gained access to Change Healthcare's network. The initial entry point was a Citrix remote access portal -- a tool used by employees for remote work -- that was protected only by a username and password. Multi-factor authentication was not enabled on this portal.

The attackers used stolen credentials to log in, then spent approximately nine days moving through Change Healthcare's network, identifying valuable data, and exfiltrating it before deploying ransomware to encrypt systems.

### February 21, 2024: Systems Go Dark

When the ransomware deployed, Change Healthcare's systems went offline almost immediately. As one of the largest healthcare technology companies in the United States, Change Healthcare processes approximately 15 billion healthcare transactions annually -- roughly one-third of all US healthcare claims. The impact was instantaneous and widespread.

### February-March 2024: National Healthcare Disruption

The shutdown of Change Healthcare's systems created a cascading crisis across the US healthcare system:

- **Pharmacies** could not process insurance claims or verify patient coverage. Some patients could not obtain medications, particularly those requiring prior authorization.
- **Hospitals and clinics** could not submit claims to insurance companies, creating severe cash flow problems. Some smaller providers reported being unable to make payroll.
- **Insurance verification** systems went offline, forcing healthcare providers to operate without knowing whether patients had valid coverage.
- **Prior authorization** processes halted, delaying access to medications and procedures.

The American Hospital Association described the incident as "the most significant and consequential incident of its kind against the US health care system in history."

### March 2024: Ransom Payment

UnitedHealth Group, Change Healthcare's parent company, confirmed paying approximately $22 million in Bitcoin to the ALPHV/BlackCat ransomware group. The payment was intended to prevent the release of stolen data and obtain a decryption key.

In a twist that illustrated the unreliability of ransomware negotiations, the ALPHV/BlackCat group appeared to conduct an exit scam against its own affiliate who carried out the attack. The affiliate, who did not receive their share of the ransom, subsequently threatened additional extortion against UnitedHealth Group, claiming they still possessed the stolen data.

### October 2024: Scope Confirmed

On October 24, 2024, UnitedHealth Group confirmed that approximately 100 million people were affected -- making it the largest healthcare data breach in US history by a significant margin.

## What Was Exposed

The stolen data encompassed a broad range of healthcare and personal information:

- **Health insurance information**: Insurance member IDs, plan details, Medicaid and Medicare data
- **Medical records**: Diagnoses, medications, test results, treatment plans, medical images
- **Billing and claims data**: Claim numbers, billing codes, payment information
- **Personal identifiers**: Social Security numbers, driver's license numbers, passport numbers
- **Financial information**: Banking details used for claims payments, payment card data

The scope of exposed medical information is particularly concerning. Medical records reveal some of the most intimate details of a person's life -- mental health diagnoses, substance abuse treatment, reproductive health decisions, chronic conditions, and prescribed medications. Unlike financial data, medical information cannot be "frozen" or easily monitored for misuse.

## How It Happened

### The Missing MFA

The breach's root cause was strikingly simple: a remote access portal without multi-factor authentication. UnitedHealth Group CEO Andrew Witty confirmed this in testimony before Congress in May 2024, stating that the Citrix portal lacked MFA -- a basic security control that costs virtually nothing to implement and would have prevented the attack.

The attacker used valid credentials (likely obtained through phishing or credential markets) to log into the portal. Without MFA, the stolen username and password were sufficient for full access.

### Post-Exploitation and Lateral Movement

Once inside the network, the attackers demonstrated sophisticated tradecraft:

- They conducted reconnaissance to map Change Healthcare's network architecture
- They identified and accessed databases containing patient records, insurance data, and financial information
- They exfiltrated terabytes of data over approximately nine days
- They deployed ALPHV/BlackCat ransomware to encrypt systems and maximize pressure for payment

### ALPHV/BlackCat: A Ransomware-as-a-Service Operation

ALPHV/BlackCat operated as a ransomware-as-a-service (RaaS) operation, where the core group develops the ransomware tools and infrastructure, then recruits affiliates to carry out individual attacks. The affiliates perform the actual intrusions and negotiate ransoms, paying a percentage to the core group.

This business model has been one of the driving forces behind the ransomware epidemic. It lowers the barrier to entry for attackers and creates a scalable, specialized criminal enterprise.

## Impact

### Healthcare System Disruption

The operational impact of the breach extended far beyond data theft:

- **Pharmacy disruptions** lasted for weeks, with some patients unable to fill prescriptions
- **Provider revenue shortfalls** reached billions of dollars as claims processing halted
- **UnitedHealth Group advanced over $6 billion** to healthcare providers to keep them operational during the outage
- **System restoration** took months, with some services not fully restored until late 2024

### Financial Cost

UnitedHealth Group estimated the total cost of the breach at $2.45 billion for 2024 alone, encompassing:

- Remediation and system restoration
- The $22 million ransom payment
- Advance funding to affected providers
- Legal costs and regulatory fines
- Customer notification and credit monitoring

### Regulatory Response

The breach triggered intense congressional scrutiny. UnitedHealth Group CEO Andrew Witty testified before both the Senate Finance Committee and the House Energy and Commerce Subcommittee. Lawmakers questioned how a company of UnitedHealth's size and resources could fail to implement basic MFA on a critical access portal.

The Department of Health and Human Services (HHS) launched an investigation into HIPAA compliance. The incident renewed calls for stronger cybersecurity regulations in the healthcare sector, including mandatory minimum security standards.

## What Change Healthcare Did in Response

- **Paid the $22 million ransom** (a decision criticized by many security experts)
- **Advanced over $6 billion** to healthcare providers affected by the operational disruption
- **Accelerated MFA deployment** across all systems
- **Engaged multiple cybersecurity firms** for forensic analysis and system hardening
- **Provided credit monitoring and identity protection** services to affected individuals
- **Established a dedicated support line** for breach victims

## Lessons for Users

### Lesson 1: Healthcare Data Is Uniquely Sensitive

Medical records contain information that cannot be changed and that many people consider more private than financial data. Diagnoses, medications, mental health treatment, and reproductive health decisions are deeply personal. Unlike a credit card, medical information cannot be reissued or frozen.

### Lesson 2: You May Not Know Who Processes Your Healthcare Data

Most people had never heard of Change Healthcare before the breach, yet the company processed their insurance claims and medical data. The healthcare system is built on a complex web of intermediaries, and your data passes through many hands between your doctor's office and your insurance company. You have limited visibility into or control over this data flow.

### Lesson 3: Basic Security Failures Have Massive Consequences

The breach was caused by the absence of multi-factor authentication -- a security control that has been standard practice for years. The disproportion between the simplicity of the vulnerability and the scale of the impact (100 million people, $2.45 billion in costs, nationwide healthcare disruption) is a stark reminder that security basics matter more than advanced technologies.

### Lesson 4: Paying Ransoms Does Not Guarantee Safety

UnitedHealth Group paid $22 million and still could not guarantee that the stolen data was deleted. The group's internal dispute with its affiliate demonstrated the inherent unreliability of criminal negotiations. Paying a ransom funds criminal enterprises and provides no assurance of data destruction.

## How to Protect Yourself

If you received a notification from Change Healthcare or UnitedHealth Group, or if you used healthcare services in the US in 2022-2024, your data may have been affected. Take these steps:

1. **Enroll in the free credit monitoring and identity protection** offered by UnitedHealth Group to affected individuals. Check the official Change Healthcare breach notification website for eligibility.

2. **[Freeze your credit](/data-breaches/freeze-credit/)** at all three major bureaus. If your SSN was exposed, a credit freeze prevents criminals from opening accounts in your name.

3. **Monitor your healthcare accounts** for unfamiliar claims, prescriptions, or medical services. Medical identity theft -- where someone uses your insurance to obtain healthcare -- can affect your medical records and future treatment.

4. **Review your Explanation of Benefits (EOB)** statements from your insurance company. Flag any services or providers you do not recognize.

5. **Use unique passwords for all healthcare portals** -- patient portals, insurance accounts, and pharmacy apps. Store these in a password manager like PanicVault, which keeps your credentials in an encrypted local vault on your Apple devices rather than on cloud servers vulnerable to breaches like this one.

6. **Enable MFA on every account that offers it**. If the Change Healthcare breach taught one lesson above all others, it is that multi-factor authentication is not optional.

7. **[Check your overall breach exposure](/data-breaches/check-email-compromised/)** using [Have I Been Pwned](/data-breaches/have-i-been-pwned/) and similar services.

8. **[Set up dark web monitoring](/data-breaches/dark-web-monitoring/)** to receive alerts if your personal or medical information appears in criminal markets.

9. **Be alert for medical identity theft**. If you receive bills for services you did not receive, EOB statements for unknown visits, or if your insurance company contacts you about claims you did not make, report it immediately to your insurer and file a report with the FTC at IdentityTheft.gov.

10. **File an [identity theft report](/data-breaches/identity-theft-recovery/)** if you discover any misuse of your personal or medical information.

The Change Healthcare breach is a reminder that the institutions we rely on for healthcare are also custodians of our most sensitive data. A single missing security control -- MFA on one remote access portal -- compromised the medical information of 100 million Americans. While you cannot control the security practices of healthcare intermediaries, you can take defensive measures that limit the damage when their defenses fail.

## Related Articles

- [What to Do Immediately After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [How to Freeze Your Credit (and Why You Should)](/data-breaches/freeze-credit/)
- [Identity Theft Recovery: A Step-by-Step Guide](/data-breaches/identity-theft-recovery/)
- [Dark Web Monitoring: Is Your Data for Sale?](/data-breaches/dark-web-monitoring/)
- [The Biggest Data Breaches of 2025-2026](/data-breaches/biggest-breaches/)
