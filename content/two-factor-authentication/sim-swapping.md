---
title: "How SIM Swapping Bypasses SMS 2FA"
description: "Learn how SIM swapping attacks work, why SMS-based two-factor authentication is vulnerable, real-world cases, carrier protections, and how to defend your accounts with TOTP."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Two-Factor Authentication"
---

SMS-based two-factor authentication was a significant improvement when it was introduced. Adding any second factor makes account compromise harder. But as we explain in our [guide to two-factor authentication](/two-factor-authentication/), not all second factors are created equal -- and SMS has a fundamental vulnerability that attackers exploit routinely. SIM swapping is that exploit, and understanding how it works is essential to protecting your accounts.

A SIM swap attack transfers your phone number to an attacker's SIM card. Once they control your number, they receive every SMS sent to it, including two-factor authentication codes. The attack does not require any technical sophistication on the attacker's part -- it exploits the weakest link in the security chain: human beings working at mobile carrier stores.

## How SIM Swapping Works

The attack follows a predictable sequence:

### Step 1: Target Selection and Research

The attacker identifies a target, typically someone with valuable accounts -- cryptocurrency holdings, a large social media following, access to corporate systems, or simply a bank account worth draining. They gather personal information through:

- **Social media profiles** -- Birthdates, pet names, schools, employers, and other details commonly used in security questions.
- **Data breaches** -- Leaked databases containing email addresses, phone numbers, partial SSNs, and account details. Breach data from past incidents is widely available on dark web marketplaces and is a primary vector for [identity theft](/data-breaches/).
- **Public records** -- Property records, voter registration, court documents, and other publicly accessible information.
- **Phishing** -- Targeted emails or messages designed to extract specific personal details. Understanding [how phishing attacks work](/phishing/) helps you recognize when you are being targeted for information gathering that precedes a SIM swap.

### Step 2: Contacting the Carrier

Armed with personal information, the attacker contacts the target's mobile carrier. This can happen through several channels:

**In-store visits**: The attacker walks into a carrier retail store claiming to be the account holder. They present a fake ID or simply provide enough personal information to pass identity verification. Retail employees are trained to be helpful, and the identity verification process at most carrier stores is not designed to withstand a determined social engineer.

**Phone calls**: The attacker calls customer support and requests a SIM swap, claiming a lost or damaged phone. They answer security questions using the researched information. If one representative is suspicious, the attacker hangs up and calls again, hoping for a less vigilant agent.

**Online account portals**: Some carriers allow SIM changes through their website or app. If the attacker has compromised the carrier account credentials (through phishing or credential stuffing from breach data), they can initiate the swap without human interaction.

**Insider collusion**: In some documented cases, attackers have bribed or coerced carrier employees to perform unauthorized SIM swaps. A carrier employee with system access can override normal verification procedures.

### Step 3: The Swap

The carrier transfers the target's phone number to a new SIM card controlled by the attacker. This happens quickly -- usually within minutes. The target's phone immediately loses cellular service. Calls and texts stop arriving. The phone shows "No Service" or "Emergency Calls Only."

### Step 4: Account Takeover

With the phone number under their control, the attacker moves fast:

1. They initiate password resets on the target's accounts. Many services send a reset code via SMS.
2. They receive the SMS codes on their device.
3. They reset passwords and lock the legitimate owner out.
4. If the service uses SMS-based 2FA, they receive the authentication codes directly.
5. They drain accounts, steal data, or take over identities -- all before the target realizes what happened.

The entire attack, from SIM swap to account compromise, can take less than 30 minutes.

## Real-World SIM Swapping Cases

SIM swapping is not theoretical. It has affected thousands of individuals and resulted in significant financial losses:

**Michael Terpin (2018)** -- An early cryptocurrency investor lost approximately $24 million in a SIM swap attack. The attacker, a teenager named Joel Ortiz, worked with associates to swap Terpin's phone number and gain access to cryptocurrency accounts. Terpin later sued AT&T for $224 million, alleging negligence in allowing the swap.

**Twitter CEO Jack Dorsey (2019)** -- Dorsey's Twitter account was compromised through a SIM swap. The attackers used Dorsey's phone number to post offensive tweets via Cloudhopper, a service that allowed tweeting by SMS. While the damage was reputational rather than financial, it demonstrated that even prominent tech figures are vulnerable.

**The SEC Hack (2024)** -- The US Securities and Exchange Commission's official X/Twitter account was compromised via a SIM swap, leading to a fraudulent post about Bitcoin ETF approval that briefly moved cryptocurrency markets. The incident highlighted how SIM swap attacks can have consequences far beyond the individual victim.

**Princeton University Study (2020)** -- Researchers tested five major US carriers by attempting SIM swaps using readily available information. They found that all five carriers used authentication procedures vulnerable to SIM swapping. In many cases, the researchers were able to complete swaps even when they could not answer the standard security questions, because customer service representatives offered alternative verification methods that were equally weak.

## Why SMS 2FA Is Fundamentally Vulnerable

The problem with SMS-based 2FA is not a bug in a specific implementation -- it is an architectural flaw. SMS was designed in the 1980s as a convenience feature for mobile networks. It was never intended to be a secure authentication channel.

**The phone number is not an identity.** A phone number is a routing address controlled by your carrier. When you "authenticate" with an SMS code, you are actually proving that your carrier is currently routing messages to a SIM card you possess. The carrier can change that routing at any time, as SIM swaps demonstrate.

**SS7 vulnerabilities.** The Signaling System 7 (SS7) protocol that routes SMS messages between carriers has known security flaws that allow interception of messages. State-level actors and sophisticated criminal groups have exploited SS7 to intercept SMS messages without needing a SIM swap at all.

**No encryption.** SMS messages are transmitted in plaintext across carrier networks. While the radio link between your phone and the cell tower may be encrypted, the message traverses carrier infrastructure without end-to-end protection.

**Carrier employees are a vulnerability.** Any system that depends on a minimum-wage retail employee correctly verifying identity has a fundamental weakness. Social engineering exploits human trust, helpfulness, and decision fatigue -- qualities that are difficult to eliminate through training alone.

This is why the industry is [phasing out SMS-based 2FA](/two-factor-authentication/sms-being-phased-out/) in favor of more secure alternatives. For a detailed comparison of TOTP and SMS, see our analysis of [TOTP vs. SMS authentication](/two-factor-authentication/totp-vs-sms/).

## How to Protect Yourself Against SIM Swapping

### Switch to TOTP or Hardware Keys

The most effective protection is to stop using SMS as a second factor entirely. TOTP authenticator apps generate codes locally on your device. The shared secret never traverses a cellular network, and your carrier has no role in the authentication process. A SIM swap gives the attacker your phone number, but it does not give them your TOTP secrets.

Hardware security keys go further by providing phishing-resistant authentication that is bound to a physical device. Neither SIM swaps nor TOTP code phishing can compromise a hardware key.

### Add a Carrier PIN or Account Lock

Most major carriers now offer security features specifically designed to prevent unauthorized SIM swaps:

- **T-Mobile**: Account Takeover Protection (enabled in the T-Mobile app or in-store)
- **AT&T**: Extra Security passcode (set through your account profile)
- **Verizon**: Number Lock (enabled in the My Verizon app)
- **Visible/MVNO carriers**: Check with your specific provider for SIM lock options

These PINs add a layer of verification that an attacker must bypass before the carrier will process a SIM swap. They are not foolproof -- an insider with system access may be able to override them -- but they significantly raise the difficulty of a standard social engineering attack.

### Reduce Your Digital Footprint

The less personal information available about you, the harder it is for an attacker to pass carrier identity verification:

- Remove your phone number from public social media profiles.
- Opt out of data broker listings (services like DeleteMe can automate this).
- Use unique, random answers for security questions rather than truthful answers. Store these in your password manager.
- Use a separate phone number for critical accounts if possible. A Google Voice number, for example, cannot be SIM-swapped through a carrier store.

### Monitor for Warning Signs

A SIM swap produces immediate, recognizable symptoms:

- Your phone suddenly shows "No Service" when it should have signal.
- You receive unexpected "Welcome to [carrier]" or SIM activation messages.
- You cannot make or receive calls or texts.
- You receive emails about password resets you did not initiate.

If you notice these signs, act immediately: contact your carrier from a different phone, lock your accounts, and change passwords on your most critical services. Time is critical -- attackers move within minutes.

### Prioritize Your Most Important Accounts

Not all accounts need the same level of protection. Focus on the accounts that, if compromised, would cause the most damage or enable cascading compromises. Your email account is the highest priority because it is the recovery mechanism for almost everything else. See our guide to [setting up 2FA on your most important accounts](/two-factor-authentication/priority-accounts/) for a systematic approach.

## Why TOTP Is Immune to SIM Swapping

TOTP authentication removes the carrier from the security equation entirely. Store your TOTP secrets in a trusted password manager -- Apple users can use [PanicVault](https://panicvault.com), a native macOS/iOS app that keeps passwords and TOTP codes together in an encrypted KeePass KDBX vault. Here is why TOTP is immune:

1. **The secret stays on your device.** When you set up TOTP, the shared secret is stored in your authenticator app. It never passes through your carrier's network, is never associated with your phone number, and cannot be intercepted via SS7 or redirected via SIM swap.

2. **Code generation is local.** Your authenticator app computes the current code using the stored secret and the current time. No network communication is required. You can generate valid codes in airplane mode.

3. **No human intermediary.** SIM swapping exploits carrier employees. TOTP has no equivalent vulnerability because there is no third party involved in code generation.

4. **No routing dependency.** SMS codes must be routed from the service through carrier infrastructure to your device. Each hop is a potential point of interception or redirection. TOTP eliminates the entire routing chain.

The only way to compromise TOTP is to obtain the shared secret itself -- by compromising the device where it is stored, intercepting it during initial setup, or extracting it from the service's database. These attacks are possible but far more difficult than a SIM swap, requiring either malware on your specific device or a server-side breach.

## What About eSIM?

eSIM (embedded SIM) technology does not fundamentally solve the SIM swapping problem. While eSIM eliminates the physical SIM card, the underlying process of transferring a phone number between devices still exists. An attacker who successfully social-engineers a carrier can transfer a number to a new eSIM just as they could to a physical SIM card.

eSIM does make some attack vectors slightly harder -- the attacker cannot simply insert a SIM card into a phone at a carrier store -- but the core vulnerability remains: the carrier controls phone number assignment, and carrier employees can be deceived.

## The Broader Lesson

SIM swapping is a case study in why security cannot depend on trust in intermediaries. Any authentication mechanism that routes through a third party -- whether a mobile carrier, an email provider, or a cloud service -- inherits the security weaknesses of that third party.

The most secure authentication methods are those where the cryptographic material never leaves your control. TOTP keeps the secret on your device. Hardware keys keep the private key in tamper-resistant hardware. [Passkeys](/passkeys/) store credentials in platform secure enclaves. Each of these approaches eliminates the carrier as a point of failure.

Understanding [what 2FA is and why it matters](/two-factor-authentication/what-is-2fa/) is the first step. Understanding which 2FA methods are actually secure is the second. SIM swapping makes the case clearly: SMS-based 2FA is better than no 2FA, but it is the weakest form of two-factor authentication in common use, and for anyone with accounts worth protecting, it should be replaced with TOTP or hardware keys as soon as possible.
