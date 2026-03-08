---
title: "Is Keeper Safe? (2026)"
description: "Security deep-dive into Keeper: AES-256 encryption, PBKDF2 key derivation, SOC 2 Type 2 compliance, zero-knowledge design, and breach history."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Password Managers"
faq:
  - q: "Has Keeper ever been hacked?"
    a: "No. As of 2026, Keeper has never suffered a data breach resulting in exposure of customer vault data. The company maintains SOC 2 Type 2, ISO 27001, and FedRAMP authorization, all of which require ongoing third-party verification of security controls."
  - q: "Is Keeper safe for enterprise use?"
    a: "Yes. Keeper is widely deployed in enterprise environments and holds SOC 2 Type 2, ISO 27001, and FedRAMP certifications. It offers role-based access controls, SCIM provisioning, SSO integration, event logging, and admin policy enforcement designed for regulated industries."
  - q: "Can Keeper employees see my passwords?"
    a: "No. Keeper uses zero-knowledge encryption. Your vault is encrypted on your device, and Keeper's servers only store encrypted data. Keeper does not have access to your master password, encryption keys, or plaintext vault contents."
  - q: "Why is Keeper more expensive with add-ons?"
    a: "Keeper uses modular pricing. The base plan covers core password management, but features like dark web monitoring (BreachWatch), secure file storage, and the private messaging feature (KeeperChat) are paid add-ons. The total cost with all add-ons can exceed $60/year."
  - q: "Does Keeper support hardware security keys?"
    a: "Yes. Keeper supports FIDO2/WebAuthn hardware security keys (such as YubiKey) as a two-factor authentication method. It also supports TOTP authenticator apps, SMS codes, and Duo Security for 2FA."
---

Keeper Security markets itself as the enterprise-grade password manager -- the one you deploy across a 10,000-person organization with compliance requirements and regulatory audits. It holds SOC 2 Type 2, ISO 27001, and FedRAMP certifications, runs annual penetration tests, and has maintained a clean breach record since its founding in 2011. But certifications and enterprise sales are different from cryptographic security. Here is what you need to know about whether Keeper is actually safe to trust with your credentials. For the broader picture on password manager security, see our [password managers guide](/password-managers/).

## The Short Answer

Keeper is safe. It uses AES-256 encryption with PBKDF2 key derivation, implements zero-knowledge architecture, holds multiple compliance certifications, undergoes annual penetration tests, and has never been breached. Its security is enterprise-grade in the literal sense -- regulated organizations trust it with their credentials, and compliance auditors have verified its controls.

The concerns center on transparency (proprietary code, no published audit reports) and pricing (add-on modules that fragment the value proposition). The cryptographic fundamentals are sound.

## Security Architecture

Keeper's architecture follows the standard zero-knowledge model: all encryption and decryption happens on the user's device, and Keeper's servers store only encrypted data.

When you create a Keeper account, the client generates a 256-bit AES encryption key (called the "data key") randomly. This data key is what encrypts your vault contents. The data key itself is encrypted using a key derived from your master password through PBKDF2, and the encrypted data key is stored on Keeper's servers.

This means decrypting your vault requires: (1) your master password to derive the key derivation key, (2) the key derivation key to decrypt the data key, and (3) the data key to decrypt vault items. An attacker who obtains only the encrypted vault from the server faces the full strength of the KDF and master password before reaching the data key, and the full strength of AES-256 before reaching vault contents.

Keeper also implements a **record-level encryption** model. Each vault record (password entry, secure note, file) is encrypted with its own individual record key, and these record keys are encrypted with the data key. This granular encryption supports Keeper's sharing features -- when you share a record with another user, only that record's key is re-encrypted with the recipient's public key, without exposing your data key or other records.

For team and enterprise deployments, Keeper uses an **Elliptic Curve (EC) key pair** (specifically NIST P-256) for each user. The EC key pair enables secure key exchange for shared folders and records. The private key is encrypted with the user's data key and stored on the server. The public key is available for key exchange.

## Encryption Details

Keeper uses **AES-256-GCM** (transitioning from AES-256-CBC in earlier versions) for encrypting vault data. GCM provides authenticated encryption, ensuring both confidentiality and integrity in a single operation.

For key derivation, Keeper uses **PBKDF2-SHA512** with a minimum of 1,000,000 iterations (as of recent updates). The high iteration count makes brute-force attacks against the master password computationally expensive. At 1,000,000 iterations, even a high-end GPU cluster would be limited to hundreds of guesses per second -- far too slow to crack a strong passphrase.

Unlike 1Password, Keeper does not use a Secret Key model. The master password alone (processed through the KDF) protects the data key. This means the security of the vault hinges on the strength of the master password plus the KDF settings.

Unlike some competitors, Keeper does not yet offer Argon2 as a KDF option. PBKDF2 with high iterations remains secure for strong passwords but is theoretically more susceptible to GPU-based attacks than Argon2's memory-hard approach. For users with strong master passwords, this distinction is unlikely to matter in practice. For users with weaker passwords, Argon2 would provide an additional margin of safety.

All vault fields are encrypted, including record titles, usernames, passwords, URLs, notes, and custom fields. File attachments stored in Keeper are also encrypted with individual file-level keys.

## Breach History

Keeper has never been breached. Since its founding in 2011, there have been no reported incidents of server compromise, vault data theft, or source code exposure.

The company's compliance certifications require ongoing monitoring and incident reporting, adding an additional layer of accountability. A breach affecting a SOC 2-certified organization would trigger audit and disclosure requirements, making concealment difficult.

One incident worth noting is a **2017 vulnerability** discovered by security researcher Tavis Ormandy (Google Project Zero) in Keeper's browser extension. The vulnerability could have allowed a malicious website to steal passwords from the browser extension. Keeper patched the issue within 24 hours of disclosure. This was a software vulnerability, not a server breach, and it was handled responsibly with a rapid fix. However, Keeper's initial legal response -- threatening the researcher who disclosed the vulnerability -- drew criticism from the security community before the company changed course.

This episode highlights the tension between compliance-oriented security culture and the open vulnerability disclosure culture that the security research community values. Keeper's technical response (fast patch) was good; the initial communication response was poor.

## Independent Audits

Keeper maintains multiple compliance certifications that require independent auditing:

- **SOC 2 Type 2**: Verified by independent auditors, covering security, availability, processing integrity, confidentiality, and privacy controls. SOC 2 Type 2 requires evidence of controls operating effectively over time, not just at a point in time.
- **ISO 27001**: International standard for information security management systems, independently certified.
- **FedRAMP Authorization**: Federal Risk and Authorization Management Program certification, required for cloud services used by U.S. government agencies. FedRAMP involves rigorous security assessment, authorization, and continuous monitoring.
- **Annual penetration testing**: Keeper engages third-party firms for annual penetration tests of its infrastructure and applications.

These certifications represent genuine security verification, particularly FedRAMP, which has some of the strictest security requirements of any certification framework. However, compliance certifications assess operational security controls -- server hardening, access management, incident response -- rather than deep cryptographic code review.

Keeper does not publish full penetration test or audit reports publicly. The certifications confirm that independent auditors have reviewed the system and found it compliant, but the details of their findings are not available for public scrutiny.

## Known Vulnerabilities and Concerns

**Proprietary and closed-source.** Keeper's entire codebase is proprietary. The encryption implementation cannot be independently verified by the security community at large. Trust is derived from compliance certifications and NDA-bound auditors rather than public code review.

**No Argon2 support.** Keeper relies on PBKDF2-SHA512 for key derivation. While the iteration count is high, PBKDF2 is not memory-hard, meaning it is more amenable to GPU-based cracking than Argon2. For users with strong master passwords, this is a theoretical concern. For the broader user base, Argon2 would provide better protection against weak password choices.

**No Secret Key.** Like Bitwarden and LastPass, Keeper does not use a Secret Key model. The master password alone (plus KDF iterations) protects the vault. 1Password's Secret Key approach provides stronger protection against offline brute-force attacks.

**Add-on pricing model.** Keeper's base plan is $34.99/year (individual), but essential features are paid add-ons: BreachWatch (dark web monitoring) is $19.99/year, secure file storage is $9.99/year, and KeeperChat is additional. The total cost with all features approaches or exceeds $65/year, making it one of the most expensive options. This pricing model creates frustration and can lead users to skip security-relevant features (like BreachWatch) to save money.

**2017 researcher response.** The initial legal threat against Tavis Ormandy raised concerns about Keeper's openness to external security research. The company has since adopted a more standard approach to vulnerability disclosure, but the incident left a mark on community perception.

**Enterprise focus.** Keeper's individual consumer product, while functional, is clearly secondary to the enterprise business. Features, documentation, and support are heavily oriented toward team and business deployments. Individual users may find the interface more complex than necessary.

## What Could Go Wrong

The realistic threat scenarios for Keeper users:

1. **Weak master password.** Without a Secret Key and without Argon2, a weak master password is the most significant vulnerability. PBKDF2 at 1,000,000 iterations provides good protection, but a short or predictable password could still be vulnerable to a well-funded attacker with GPU resources.

2. **Browser extension vulnerabilities.** The 2017 Tavis Ormandy vulnerability demonstrated that browser extensions are a meaningful attack surface. While that specific issue was patched, browser extensions operate in an inherently complex environment where new vulnerabilities can emerge.

3. **Device compromise.** Malware on a user's device can capture the master password or read decrypted vault contents from memory. This is universal to all password managers.

4. **Supply chain attack.** Proprietary code means that a compromised build pipeline would be harder for the public to detect compared to open-source alternatives where builds can be independently verified.

Understanding [what happens if a password manager is hacked](/password-managers/what-if-hacked/) provides useful context for evaluating these risks against Keeper's zero-knowledge design.

## The Offline Alternative

For users who prefer compliance-level security without cloud dependency, the KeePass format offers an offline alternative. PanicVault brings the KeePass format to Apple devices with a native, modern interface. Your encrypted vault stays on your devices, synchronized only through mechanisms you control. There is no server to audit, no subscription to maintain, and the open KeePass format is supported by a broad ecosystem of compatible tools across every platform.

## Verdict

Keeper is a safe, enterprise-oriented password manager with a clean breach record and strong compliance credentials. SOC 2 Type 2, ISO 27001, and FedRAMP certifications provide genuine assurance that independent auditors have verified its security controls. The encryption fundamentals are sound, the zero-knowledge architecture works as expected, and the record-level encryption model is well-designed for sharing scenarios.

The concerns are about modernization (no Argon2, no Secret Key), transparency (closed source, no public audit reports), and pricing (add-on fragmentation). For enterprise deployments in regulated industries, Keeper's compliance portfolio makes it a natural fit. For individual users, the value proposition is less clear given that competitors offer comparable or superior security at lower prices.

If you choose Keeper, use a strong master password, enable two-factor authentication with a hardware key, and consider adding BreachWatch for dark web monitoring. For more on [how password managers handle security](/password-managers/are-password-managers-safe/), see our comprehensive guide.

## Related Articles

- [Are Password Managers Safe?](/password-managers/are-password-managers-safe/)
- [Zero-Knowledge Encryption Explained](/password-managers/zero-knowledge-encryption/)
- [What Happens If a Password Manager Gets Hacked?](/password-managers/what-if-hacked/)
- [Bitwarden vs Keeper: Full Comparison](/compare/bitwarden-vs-keeper/)
- [Password Manager Pricing Comparison](/compare/pricing-comparison/)
