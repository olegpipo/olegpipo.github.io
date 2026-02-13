---
title: "Why SMS 2FA Is Being Phased Out"
description: "Learn why organizations are abandoning SMS-based two-factor authentication. Covers NIST guidelines, SS7 vulnerabilities, SIM swapping attacks, and what's replacing SMS 2FA."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Two-Factor Authentication"
---

SMS-based two-factor authentication was once considered good enough. You log in with your password, receive a text message with a six-digit code, type it in, and you are verified. For years, this was the default [two-factor authentication](/two-factor-authentication/) method offered by banks, email providers, and social media platforms. It was simple, it required no additional software, and it was a genuine improvement over passwords alone.

That era is ending. Major organizations, security standards bodies, and governments are actively moving away from SMS as a second factor. Not because SMS 2FA is worse than no 2FA -- it is not -- but because its vulnerabilities have been documented, exploited at scale, and demonstrated to be fundamentally unfixable. Understanding why SMS is being abandoned helps you make informed decisions about your own accounts and prepare for the transition.

## The NIST Turning Point

The most influential signal came from the National Institute of Standards and Technology (NIST). In 2016, NIST Special Publication 800-63B -- the federal standard for digital identity guidelines -- deprecated SMS as an out-of-band authentication method. The language was carefully chosen: SMS was described as a "restricted" authenticator, meaning agencies should use it only when no alternative is available and should plan to migrate away from it.

NIST's reasoning was straightforward. SMS messages are delivered through the public switched telephone network (PSTN), which was designed for voice communication, not secure data transmission. The protocols underlying SMS were built decades before authentication was a consideration, and they carry inherent vulnerabilities that cannot be patched without replacing the entire infrastructure.

The NIST deprecation was not a ban. It was a formal acknowledgment that the security community's concerns about SMS had reached a threshold where continued reliance on it was irresponsible for high-assurance systems. The private sector took notice: companies that previously viewed SMS 2FA as adequate began evaluating alternatives.

Subsequent revisions of NIST 800-63B have maintained and strengthened this position. The message is clear -- SMS 2FA is a transitional technology, not a long-term solution.

## SS7: The Protocol That Cannot Be Secured

To understand why SMS is vulnerable at its core, you need to understand Signaling System 7 (SS7), the protocol suite that underlies the global telephone network.

### What SS7 Does

SS7 is a set of protocols developed in the 1970s and 1980s to enable telephone networks to communicate with each other. When you send an SMS, it travels through SS7 signaling to reach the recipient's carrier and ultimately their phone. SS7 handles call routing, number portability, roaming, and SMS delivery.

### Why SS7 Is Vulnerable

SS7 was designed in an era when access to the telephone network was limited to a small number of trusted carriers. There was no authentication between SS7 nodes -- any node on the network was assumed to be legitimate. This trust model made sense when there were a handful of national telephone companies.

Today, hundreds of carriers, mobile virtual network operators (MVNOs), and interconnect providers have SS7 access. The barrier to entry has lowered dramatically. Security researchers have demonstrated that an attacker with access to an SS7 node -- through a compromised carrier, a rogue provider, or a purchased connection -- can:

**Intercept SMS messages.** By sending SS7 commands that redirect a target's messages to an attacker-controlled device, the attacker receives the authentication code instead of the legitimate user. This is not theoretical: it has been demonstrated in controlled research and exploited in real attacks.

**Track location.** SS7 allows querying which cell tower a phone is connected to, enabling real-time location tracking of any phone number.

**Redirect calls.** Calls can be silently forwarded through attacker infrastructure, enabling eavesdropping.

### Why SS7 Cannot Be Fixed

The fundamental problem is architectural. SS7 was not designed with authentication or encryption. Retrofitting security into the protocol would require coordinating changes across thousands of carriers in hundreds of countries, many of which run decades-old switching equipment. The economic incentive to make this investment is low, because carriers are moving toward newer protocols (Diameter, for 4G/5G networks) rather than securing the legacy infrastructure.

Several proposals for SS7 security improvements exist (including SMS firewalls and filtering), and some carriers have implemented them. But these are mitigations, not solutions. As long as any carrier on the global network has weak SS7 security, the entire network is exposed to interception at the signaling level.

For authentication purposes, this means: any SMS message can potentially be intercepted by a determined attacker with modest resources. The cost of SS7 exploitation has been estimated at a few thousand dollars for a single interception -- well within reach for targeted attacks on high-value accounts.

## SIM Swapping: The Low-Tech Attack

While SS7 exploitation requires technical sophistication, SIM swapping requires only social engineering -- and it has become one of the most common attack vectors against SMS-based 2FA.

### How SIM Swapping Works

1. **Research the target.** The attacker gathers personal information about the victim: name, phone number, address, last four digits of their SSN, and other data often available from data breaches or social media.

2. **Contact the carrier.** The attacker calls the victim's mobile carrier (or visits a store) and impersonates the victim. They claim to have lost their phone or SIM card and request that the phone number be transferred to a new SIM.

3. **Bypass verification.** Carrier employees ask security questions. The attacker provides the researched information. In many cases, this is sufficient. In others, the attacker may bribe or coerce a carrier employee (known as an "inside job").

4. **Receive the victim's messages.** Once the SIM swap is complete, all SMS messages and calls to the victim's number are routed to the attacker's device. The victim's phone loses service.

5. **Intercept authentication codes.** The attacker initiates password resets or login attempts on the victim's accounts, receives the SMS codes on their device, and takes over the accounts.

### The Scale of the Problem

SIM swapping is not rare. The FBI's Internet Crime Complaint Center (IC3) reported that SIM swapping complaints increased dramatically year over year, with losses in the hundreds of millions of dollars. Cryptocurrency holders have been particularly targeted because blockchain transactions are irreversible -- once funds are transferred, they are gone.

High-profile incidents include:

- **Twitter CEO Jack Dorsey's account** was hijacked via SIM swap in 2019, with the attackers posting messages from his account
- **Numerous cryptocurrency investors** have lost millions of dollars through SIM swap attacks that bypassed SMS-based 2FA on exchange accounts
- **Journalists and activists** have been targeted by state-sponsored attackers using SIM swapping to access their communications

### Why Carriers Cannot Fully Prevent It

Carriers face a tension between security and customer service. Customers who legitimately lose their phones need to transfer their numbers to new SIMs quickly. Every added verification step slows down legitimate requests and generates customer complaints. Carriers have implemented PIN codes, multi-step verification, and employee training, but social engineering remains effective because the human element cannot be fully eliminated.

Some carriers now offer account locks, port-out protections, and enhanced verification for high-risk changes. These are improvements, but they are opt-in and inconsistently applied. The fundamental problem remains: your phone number is controlled by a third party (the carrier), and that third party can be manipulated.

## Real-Time Phishing: SMS's Hidden Weakness

Even without SIM swapping or SS7 exploitation, SMS codes are vulnerable to real-time phishing attacks.

In a real-time phishing attack, the attacker creates a convincing fake login page for a target service. When the victim enters their username and password on the fake page, the attacker immediately uses those credentials on the real service. The real service sends an SMS code to the victim. The victim, still on the fake page, is prompted to enter the SMS code. The victim enters it, the attacker receives it, and enters it on the real service -- all within the 30-second validity window.

This attack works because SMS codes are not cryptographically bound to the login session. The code is valid regardless of where it is entered. This is a fundamental limitation shared with [TOTP codes](/two-factor-authentication/totp-vs-sms/), though TOTP at least eliminates the network interception vectors.

By contrast, [passkeys](/passkeys/) and hardware security keys use cryptographic challenge-response protocols that are bound to the specific origin (domain), making phishing mathematically impossible even in real time.

## What Is Replacing SMS 2FA

The shift away from SMS is not happening in a vacuum. Several stronger alternatives have matured to the point of practical deployment.

### TOTP (Time-Based One-Time Passwords)

TOTP codes generated by authenticator apps or [password managers](/password-managers/) eliminate the network transport vulnerability entirely. The shared secret never leaves your device. There is no SMS to intercept, no SIM to swap, no carrier to social-engineer. The code is generated locally using a cryptographic algorithm.

TOTP is the most practical immediate replacement for SMS 2FA. Setup requires scanning a QR code, and code generation works offline. The [best authenticator apps](/two-factor-authentication/best-authenticator-apps/) make this process straightforward.

### Hardware Security Keys

FIDO U2F and FIDO2 hardware keys (such as YubiKey) provide the strongest form of 2FA currently available. The authentication is based on public-key cryptography, bound to the specific website origin, and requires physical interaction with the key. It is resistant to phishing, interception, and replay attacks.

The tradeoff is cost (keys must be purchased) and convenience (you must carry the physical key). For high-value accounts, [hardware keys are worth evaluating](/two-factor-authentication/hardware-keys-vs-totp/) as either a primary or backup second factor.

### Passkeys

[Passkeys](/passkeys/) represent the next evolution: FIDO2 credentials stored on your device (or synced across devices) that replace both the password and the second factor. Passkeys use public-key cryptography, are phishing-resistant by design, and do not require carrying a separate device.

Major platforms (Apple, Google, Microsoft) have implemented passkey support, and adoption is accelerating. Passkeys are widely considered the long-term replacement for the password-plus-SMS model.

### Push-Based Authentication

Services like Duo Push and Microsoft Authenticator push notifications send an authentication prompt to a registered device. The user approves or denies the login attempt with a tap. Some implementations include number matching (the user must select the correct number shown on the login screen) to prevent prompt-bombing attacks.

Push-based authentication is not phishing-resistant in the same way as FIDO2/passkeys, but it is significantly stronger than SMS because it requires access to a specific registered device rather than just a phone number.

## The Transition: Where Things Stand

The migration away from SMS 2FA is well underway, but it is uneven.

### Organizations That Have Moved

- **Google** has pushed users toward Google Prompts and passkeys, with SMS as a fallback that is increasingly de-emphasized
- **Twitter/X** removed SMS 2FA for non-paying users in 2023, requiring authenticator apps or hardware keys
- **Major banks** in Europe and Australia have largely transitioned to app-based authentication, driven by regulatory requirements (PSD2 in Europe)
- **GitHub** requires authenticator apps or hardware keys for developer accounts; SMS is not offered
- **Cloudflare, Dropbox, and other tech companies** have made hardware keys their primary 2FA method internally

### Organizations Still Using SMS

- **Many US banks** still rely primarily on SMS, though this is changing gradually
- **Government services** in some countries still offer only SMS 2FA
- **Smaller services** that lack the engineering resources to implement TOTP or FIDO2
- **Telecom providers** ironically still use SMS for their own account security in many cases

### The Long Tail

SMS 2FA will not disappear overnight. It will persist for years in legacy systems, in services that prioritize simplicity over security, and in regions where smartphone penetration is lower. But the direction is clear, and the pace is accelerating.

## What You Should Do Now

### Audit Your Accounts

Identify every account where you use SMS as your second factor. Prioritize them by importance: email, financial services, cloud storage, and social media first.

### Switch to TOTP Where Possible

For each account that supports it, switch from SMS to TOTP. Most services offer this in their security settings under "authenticator app" or "authentication app." The process typically takes a few minutes per account. Store your TOTP secrets in your password manager or a dedicated authenticator app.

### Enable Stronger Methods Where Available

If a service supports hardware keys or passkeys, consider using them -- especially for your most critical accounts (email, financial, cloud infrastructure). Even if you keep TOTP as a backup, a hardware key as the primary factor provides the strongest protection.

### Set Up SIM Swap Protection

Until you have eliminated SMS 2FA entirely, protect your phone number:

- Set a PIN or passcode on your carrier account
- Enable port-out protection if your carrier offers it
- Use a carrier that supports advanced security features
- Consider a secondary phone number (Google Voice, VoIP) for 2FA on less critical accounts, though this introduces its own set of tradeoffs

### Do Not Remove SMS 2FA Without Replacing It

This point deserves emphasis. SMS 2FA, with all its flaws, is still far better than no 2FA. If a service only supports SMS as a second factor, keep it enabled. The vulnerabilities described in this article require a targeted attack against you specifically. A password alone is vulnerable to every automated credential-stuffing botnet on the internet.

The goal is to replace SMS with something stronger, not to remove it and go back to passwords only. Even Google and NIST acknowledge that SMS 2FA has value -- they just want you to move to something better as soon as practically possible.

## The Bigger Picture

The decline of SMS 2FA is part of a broader shift in authentication philosophy. The old model -- something you know (password) plus something delivered to you (SMS code) -- relied on the security of a delivery channel that turned out to be fundamentally insecure. The new model -- something you know plus something you possess (hardware key, authenticator app, passkey) -- eliminates the delivery channel entirely.

This shift aligns with the broader trend toward [the future of multi-factor authentication](/two-factor-authentication/future-of-mfa/): phishing-resistant, cryptographically bound, and independent of third-party infrastructure like telephone carriers. Passkeys, hardware keys, and TOTP all share this property to varying degrees.

SMS 2FA was a necessary step in the evolution of online security. It normalized the idea that a password alone is not enough. It trained billions of users to expect a second verification step. That cultural shift is permanent and valuable. But the technology itself has served its purpose, and it is time to move on.

The transition does not have to happen all at once. Start with your [priority accounts](/two-factor-authentication/setup-on-every-service/), switch to TOTP or passkeys, and work your way through the rest of your accounts over time. Every account you move away from SMS is one less account vulnerable to SIM swapping, SS7 interception, and real-time phishing. The path forward is clear -- and the tools to walk it are already available.
