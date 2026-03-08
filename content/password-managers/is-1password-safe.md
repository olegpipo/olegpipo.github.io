---
title: "Is 1Password Safe? (2026)"
description: "Security deep-dive into 1Password: Secret Key architecture, AES-256-GCM encryption, Cure53 audits, zero-knowledge design, and breach history."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Password Managers"
faq:
  - q: "Has 1Password ever been breached?"
    a: "No. As of 2026, 1Password has never suffered a data breach resulting in exposure of customer vault data. In October 2023, 1Password detected suspicious activity related to their Okta instance following the Okta support breach, but confirmed no user data or systems were compromised."
  - q: "What is the 1Password Secret Key?"
    a: "The Secret Key is a 128-bit randomly generated value created when you set up your 1Password account. It is combined with your master password during key derivation, adding 128 bits of entropy that an attacker must possess in addition to your master password to decrypt your vault. It is stored on your devices but never sent to 1Password's servers."
  - q: "Can 1Password see my passwords?"
    a: "No. 1Password uses zero-knowledge encryption. Your vault is encrypted on your device using keys derived from your master password and Secret Key. 1Password's servers store only encrypted data and never have access to your plaintext passwords or your Secret Key."
  - q: "Is 1Password safer than Bitwarden?"
    a: "Both are highly secure. 1Password's Secret Key provides an additional layer of protection against offline brute-force attacks that Bitwarden lacks. Bitwarden's advantage is open-source transparency. For most users with strong master passwords, both provide excellent security."
  - q: "What happens if I lose my 1Password Secret Key?"
    a: "You need both your master password and Secret Key to access your vault. 1Password provides an Emergency Kit (a PDF containing your Secret Key) that you should store securely offline. Without both credentials, your vault data cannot be recovered -- this is a feature of the zero-knowledge design, not a flaw."
---

1Password has positioned itself as the premium choice in password management, trusted by over 150,000 businesses and millions of individuals. Its marketing emphasizes security, and its pricing reflects a confidence that users will pay more for a tool they trust with everything. But does the security architecture justify that confidence? Here is a thorough examination of what makes 1Password safe, where the concerns lie, and what you should understand before entrusting it with your credentials. For context on how password managers protect data in general, see our [password managers guide](/password-managers/).

## The Short Answer

1Password is one of the safest password managers available. Its dual-key architecture (master password plus Secret Key) provides a level of protection against offline brute-force attacks that most competitors do not match. It uses AES-256-GCM encryption, undergoes regular third-party audits by Cure53, implements zero-knowledge architecture, and has never been breached. The primary concern is that it is entirely proprietary -- you cannot independently verify its code the way you can with open-source alternatives.

## Security Architecture

1Password's architecture centers on a concept the company calls the "two-secret key derivation" model. Unlike password managers that derive encryption keys solely from a master password, 1Password combines two independent secrets:

**Master Password**: The passphrase you memorize and type to unlock your vault. You choose this, and its strength depends on your choices.

**Secret Key**: A 128-bit randomly generated string (formatted as something like `A3-XXXXXX-XXXXXX-XXXXX-XXXXX-XXXXX-XXXXX`) created automatically when you set up your account. This key is stored on your devices but never transmitted to 1Password's servers.

During key derivation, both values are combined using SRP (Secure Remote Password) protocol for authentication and HKDF (HMAC-based Key Derivation Function) to produce the final encryption keys. The master password is first processed through PBKDF2 with 650,000 iterations, then combined with the Secret Key.

This dual-key approach is 1Password's most significant security differentiator. Here is why it matters: if an attacker somehow obtains your encrypted vault from 1Password's servers, they need both your master password and your Secret Key to decrypt it. The Secret Key adds 128 bits of entropy -- a number so large that brute-forcing it is computationally impossible regardless of hardware advances. Even if your master password were "password123," the Secret Key alone would make offline decryption infeasible.

Compare this to LastPass, where the master password alone (plus KDF iterations) protects the vault. When LastPass's encrypted vaults were stolen in 2022, users with weak master passwords became vulnerable. Under 1Password's model, the same breach scenario would not result in decryptable vaults because attackers would lack each user's Secret Key.

The tradeoff is complexity. You must store your Secret Key somewhere safe. If you lose both your devices and your Secret Key, your vault is unrecoverable. 1Password mitigates this with the Emergency Kit -- a printable PDF containing your Secret Key and account details, designed to be stored in a physical safe or secure location.

## Encryption Details

1Password encrypts vault data using **AES-256-GCM** (Galois/Counter Mode). GCM is an authenticated encryption mode that provides both confidentiality and integrity in a single operation, which is slightly more efficient and modern than the CBC + HMAC approach used by some competitors. GCM is widely regarded as the current best practice for symmetric authenticated encryption.

The key derivation pipeline works as follows:

1. Your master password is processed through **PBKDF2-SHA256** with 650,000 iterations and a random salt.
2. The resulting key is combined with your **Secret Key** using HKDF.
3. The final derived key is used to decrypt your account's master unlock key (MUK).
4. The MUK decrypts individual vault keys, which in turn decrypt individual vault items.

This multi-layered key hierarchy means that each vault can have its own encryption key, and shared vaults between family or team members use separate key exchange mechanisms. Changing your master password re-wraps the key hierarchy without re-encrypting every individual item.

All vault item fields are encrypted, including URLs, usernames, passwords, notes, and metadata. This stands in contrast to implementations where URLs or other metadata are stored unencrypted.

1Password uses **SRP (Secure Remote Password protocol)** for authentication. SRP allows the client to prove knowledge of the password without transmitting it or its hash. The server verifies the proof without ever possessing the password -- a significant improvement over traditional authentication where a password hash might be sent over the wire.

## Breach History

1Password has never suffered a data breach resulting in customer vault data exposure.

In **October 2023**, following the broad Okta support system breach, 1Password detected suspicious activity in their Okta instance used for employee-facing applications. The company's security team identified the intrusion quickly, investigated thoroughly, and concluded that no user data, no vault data, and no production systems were affected. The attacker accessed an Okta environment used for internal management only. 1Password published a detailed incident report and confirmed that the security boundary between internal tools and customer data held.

This incident actually served as a positive signal -- it demonstrated that 1Password's defense-in-depth approach and security monitoring worked as designed, catching and containing an intrusion before it reached sensitive systems.

Prior to that, 1Password has had no known security incidents affecting customer data since the company was founded in 2005 (originally as Agile Bits). This is one of the cleanest track records in the industry.

## Independent Audits

1Password invests heavily in third-party security assessments:

- **Cure53**: Has conducted multiple audits of 1Password's client applications and infrastructure. Cure53 is one of the most respected security audit firms in the industry, known for thorough assessments of security-critical software.
- **ISE (Independent Security Evaluators)**: Conducted a security assessment of 1Password's architecture and implementations.
- **SOC 2 Type 2**: 1Password maintains SOC 2 compliance, independently verified.
- **Bug bounty program**: 1Password runs a bug bounty program through Bugcrowd, inviting security researchers to find and report vulnerabilities.

1Password publishes summaries of audit findings and has a history of transparent communication about security assessments. However, it does not publish full audit reports the way Bitwarden does, and the source code is not publicly available for independent review.

## Known Vulnerabilities and Concerns

Despite its strong security posture, 1Password has areas worth scrutinizing:

**Proprietary code.** 1Password is closed-source. You cannot inspect the code to verify that the encryption is implemented correctly, that there are no backdoors, or that the zero-knowledge claims hold true. You must trust 1Password's representations and the third-party auditors who have reviewed the code. This is a meaningful difference from open-source alternatives like [Bitwarden](/password-managers/is-bitwarden-safe/) where anyone can verify the cryptographic implementation.

1Password has published a detailed [security white paper](https://1passwordstatic.com/files/security/1password-white-paper.pdf) describing its architecture, and the audit results from reputable firms provide some assurance. But "trust us and our auditors" is a fundamentally different trust model than "verify it yourself."

**Single company dependency.** Your vault is tied to 1Password's infrastructure and proprietary format. If 1Password were to cease operations, undergo an unfavorable acquisition, or make problematic policy changes, migrating away involves exporting to a generic format and importing elsewhere. The lack of an open standard for the vault format creates lock-in.

**Secret Key management burden.** The Secret Key is a powerful security feature, but it shifts responsibility to the user. If you lose your Secret Key and all authorized devices, your vault is permanently inaccessible. Users who do not understand this and fail to store their Emergency Kit securely could lose access to all their credentials.

**Subscription-only model.** 1Password has moved entirely to a subscription model -- there is no perpetual license or one-time purchase option. If you stop paying, you lose access to your vault through 1Password's apps (though you can export data before your subscription lapses). This is a business model concern rather than a security concern, but it affects the long-term trust calculation.

**Watchtower data.** 1Password's Watchtower feature checks your passwords against breach databases and identifies weak or reused credentials. This requires some analysis of your vault contents, though 1Password states this analysis happens locally. The feature can be disabled.

## What Could Go Wrong

Even with 1Password's strong architecture, realistic risk scenarios exist:

1. **Master password compromise without 2FA.** If someone obtains your master password (through shoulder surfing, social engineering, or keylogging) and has access to a device where your Secret Key is stored, they can access your vault. Enabling two-factor authentication adds another barrier.

2. **Device compromise.** Malware on your device could capture your master password as you type it or read decrypted vault contents from memory while the vault is unlocked. No password manager can fully protect against a compromised device. The Secret Key does not help here because it is already present on the compromised device.

3. **Supply chain attack.** A compromise of 1Password's update mechanism or build pipeline could theoretically distribute a malicious version of the application. Closed-source software makes this harder to detect than open-source software where builds can be independently verified.

4. **Emergency Kit exposure.** If your printed Emergency Kit (containing your Secret Key) is found by an adversary, and they also know or can guess your master password, they can access your vault from any device. Store the Emergency Kit in a physically secure location.

Reviewing how [zero-knowledge encryption](/password-managers/zero-knowledge-encryption/) works helps understand why server-side breaches are the one scenario where 1Password's architecture truly excels compared to simpler designs.

## The Offline Alternative

For users who want the peace of mind of keeping encrypted vault data entirely under their own control, offline password managers using the KeePass format offer an alternative approach. PanicVault, for example, provides a native Apple experience with the KeePass format -- your encrypted vault stays on your device and syncs only through mechanisms you choose (such as iCloud Drive or a local file). There is no company server to breach, no subscription to maintain, and the open KeePass format ensures you are never locked into a single vendor.

## Verdict

1Password is among the most secure password managers on the market. The Secret Key architecture is genuinely innovative and provides protection against offline brute-force attacks that most competitors cannot match. The clean breach history, regular Cure53 audits, and transparent communication during the 2023 Okta-adjacent incident all build confidence.

The main reservation is the closed-source nature of the code. You are trusting 1Password and its auditors rather than being able to verify the implementation yourself. For many users, the combination of strong architecture, reputable audits, and a long track record makes this an acceptable tradeoff. For users who prioritize verifiability above all else, open-source options like Bitwarden offer a different trust model.

If you choose 1Password, use a strong master password (a random passphrase of four to six words), store your Emergency Kit in a secure physical location, and enable two-factor authentication. With these measures, your vault is protected against every realistic threat scenario. For more on how password managers are designed to withstand attacks, see our guide on [handling breaches](/password-managers/handling-breaches/).

## Related Articles

- [Are Password Managers Safe?](/password-managers/are-password-managers-safe/)
- [1Password vs Bitwarden: Full Comparison](/compare/1password-vs-bitwarden/)
- [Zero-Knowledge Encryption Explained](/password-managers/zero-knowledge-encryption/)
- [What Happens If a Password Manager Gets Hacked?](/password-managers/what-if-hacked/)
- [Password Manager Pricing Comparison](/compare/pricing-comparison/)
