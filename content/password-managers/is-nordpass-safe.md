---
title: "Is NordPass Safe? (2026)"
description: "Security analysis of NordPass: XChaCha20 encryption, zero-knowledge design, Cure53 audits, Nord Security backing, and the NordVPN breach context."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Password Managers"
faq:
  - q: "Has NordPass ever been hacked?"
    a: "NordPass itself has not been breached. However, its parent company Nord Security experienced a server breach in 2019 affecting NordVPN (not NordPass). NordPass was launched after that incident and has maintained a clean security record since its launch."
  - q: "What encryption does NordPass use?"
    a: "NordPass uses XChaCha20 encryption, a modern cipher designed by Daniel J. Bernstein. Unlike AES-256 used by most competitors, XChaCha20 is natively fast in software, resistant to timing attacks, and uses a 256-bit key with a 192-bit nonce for strong security without hardware acceleration."
  - q: "Is NordPass safer than Bitwarden?"
    a: "Both are secure with different strengths. NordPass uses a more modern cipher (XChaCha20) and has been audited by Cure53. Bitwarden is open source, allowing public code verification. NordPass is closed source. Both use zero-knowledge architecture and have clean breach records."
  - q: "Can NordPass see my passwords?"
    a: "No. NordPass uses zero-knowledge encryption. Your vault is encrypted on your device using keys derived from your master password. NordPass's servers store only encrypted data and the company cannot access your plaintext passwords."
  - q: "Is NordPass owned by NordVPN?"
    a: "Both NordPass and NordVPN are products of Nord Security, a cybersecurity company based in Panama and Lithuania. They share a parent company but are separate products with separate infrastructure and security teams."
---

NordPass is the password manager from Nord Security, the company behind NordVPN. Launched in 2019, it is one of the newer entrants in the password management space, but it backs its offering with a distinctive technical choice: XChaCha20 encryption instead of the AES-256 that virtually every competitor uses. Whether NordPass is safe depends on the strength of that encryption, the integrity of its zero-knowledge architecture, and the broader security track record of its parent organization. For background on how password managers protect your data, see our [password managers guide](/password-managers/).

## The Short Answer

NordPass is safe. It uses XChaCha20 encryption -- a modern, well-respected cipher -- implements zero-knowledge architecture, has been audited by Cure53, and has not been breached since its launch. The security concerns relate to its relative youth as a product, its closed-source code, and the shadow cast by the 2019 NordVPN server breach (which affected NordVPN, not NordPass).

For users who want a modern encryption approach backed by a well-funded cybersecurity company, NordPass is a legitimate option. For users who prioritize longevity and open-source transparency, more established alternatives may offer greater confidence.

## Security Architecture

NordPass uses a zero-knowledge architecture where all encryption and decryption occurs on the user's device. Your master password never leaves your device, and NordPass's servers store only encrypted ciphertext.

The authentication flow uses SRP (Secure Remote Password protocol), which allows the client to prove knowledge of the master password without transmitting it or any derived hash to the server. This is the same authentication protocol used by 1Password and is considered a best practice for password manager authentication.

NordPass generates a random encryption key for the vault, which is then protected by a key derived from your master password. The vault key encrypts individual items, and the master password-derived key encrypts the vault key. This hierarchical key structure means that changing your master password re-wraps the vault key without requiring re-encryption of every individual item.

NordPass also implements biometric unlock on supported devices, using the platform's secure enclave or keystore to protect the vault key when biometric authentication is used in place of the master password.

## Encryption Details

NordPass's most notable technical decision is its choice of **XChaCha20-Poly1305** for encryption. This is worth understanding because it differs from the AES-256 used by nearly every other password manager.

**XChaCha20** is an extended-nonce variant of the ChaCha20 stream cipher, designed by cryptographer Daniel J. Bernstein. Poly1305 is a message authentication code (MAC) that provides integrity verification. Together, XChaCha20-Poly1305 is an authenticated encryption with associated data (AEAD) scheme.

Why XChaCha20 instead of AES-256? Several reasons make it an interesting choice:

- **Software performance.** ChaCha20 is designed to be fast in pure software implementations without requiring hardware acceleration. AES relies on dedicated CPU instructions (AES-NI) for optimal performance. On devices without AES-NI hardware support, ChaCha20 can be significantly faster.
- **Timing attack resistance.** ChaCha20's design uses only constant-time operations (additions, XORs, and rotations), making it inherently resistant to timing side-channel attacks. AES implementations without hardware acceleration can be vulnerable to cache-timing attacks.
- **Nonce size.** XChaCha20 uses a 192-bit nonce, compared to AES-GCM's 96-bit nonce. This larger nonce virtually eliminates the risk of nonce reuse (a catastrophic failure mode for stream ciphers), even when generating nonces randomly for large numbers of items.
- **Proven lineage.** ChaCha20 is used in TLS 1.3 (the protocol securing web traffic), WireGuard (the modern VPN protocol), and has been endorsed by major standards bodies. It is not an obscure or experimental cipher.

Both XChaCha20 and AES-256 provide 256-bit security. Neither has known practical attacks. The choice between them is more about implementation philosophy than cryptographic strength. NordPass's choice of XChaCha20 is defensible and arguably forward-looking.

For key derivation, NordPass uses **Argon2id** -- the recommended variant of the Argon2 family that combines resistance to both GPU attacks and side-channel attacks. The specific parameters (memory, iterations, parallelism) are not publicly documented, but the use of Argon2id itself is a positive signal, as it represents the current state of the art for password hashing.

## Breach History

NordPass itself has not been breached. Since its launch in 2019, there have been no reported incidents of unauthorized access to NordPass's servers, vault data exposure, or source code compromise.

However, the NordVPN breach of 2019 is relevant context. In March 2018 (disclosed publicly in October 2019), an attacker gained access to a NordVPN data center server in Finland through an insecure remote management system left by the hosting provider. The attacker obtained an expired TLS certificate and some configuration files. No user credentials, browsing data, or NordVPN account information was exposed, but the incident raised questions about Nord Security's vendor management and server hardening practices.

Key context:
- The breach affected NordVPN infrastructure, not NordPass (which launched after the breach).
- NordVPN's response included transitioning to diskless RAM-only servers, conducting independent infrastructure audits, and implementing a bug bounty program.
- The incident prompted Nord Security to invest more heavily in security infrastructure, which arguably benefited NordPass's design from the start.

The NordVPN incident does not directly affect NordPass's security, but it is part of the trust calculus for the parent organization. Nord Security's response to the incident -- transparency, infrastructure improvements, and ongoing third-party audits -- suggests the company takes security lessons seriously.

## Independent Audits

NordPass has been audited by **Cure53**, one of the most respected independent security audit firms:

- **Cure53 (2020)**: Initial security audit of NordPass's applications and infrastructure. The audit examined the cryptographic implementation, zero-knowledge architecture, and client-side security.
- **Cure53 (2022)**: Follow-up audit covering updates and new features.
- **Cure53 (2024)**: Additional assessment confirming continued adherence to security best practices.

These audits by a firm of Cure53's reputation are a strong positive signal. Cure53 has also audited Bitwarden and 1Password, so the same firm can provide comparative assurance across products.

NordPass also benefits from Nord Security's broader security infrastructure, including the company's bug bounty program and security operations center.

## Known Vulnerabilities and Concerns

**Relatively new product.** NordPass launched in 2019, making it significantly younger than 1Password (2005), LastPass (2008), and Dashlane (2012). A shorter track record means fewer years of real-world testing, fewer edge cases discovered, and less time for the security community to scrutinize the product deeply.

**Closed-source code.** NordPass is not open source. The encryption implementation, key management, and zero-knowledge claims cannot be independently verified through public code review. Users must rely on Cure53's audits and Nord Security's representations. This is the same limitation shared by 1Password, Dashlane, and Keeper, but it contrasts with Bitwarden's open-source approach.

**Parent company reputation.** The NordVPN breach, while not affecting NordPass, demonstrated vulnerabilities in Nord Security's infrastructure management at the time. The company has since taken significant steps to address these issues, but the incident remains part of the trust conversation.

**Marketing-heavy approach.** Nord Security invests heavily in marketing and affiliate programs, which can create a perception gap between marketing claims and technical reality. This is a brand concern rather than a security one, but it sometimes leads to skepticism from the security community, which generally values understated technical communication.

**Limited enterprise features.** Compared to 1Password or Keeper, NordPass's enterprise offering is less mature. This is relevant for business users who need advanced admin controls, compliance features, and integration capabilities.

## What Could Go Wrong

The realistic risk scenarios for NordPass users:

1. **Weak master password.** As with any password manager, a weak master password is the most likely vulnerability. Argon2id provides strong brute-force resistance, but cannot fully compensate for a password with low entropy. Choose a random passphrase of at least four words.

2. **Device compromise.** Malware on your device could capture your master password or read decrypted vault data. This is universal to all password managers.

3. **Infrastructure attack.** A successful attack on NordPass's infrastructure would expose encrypted vault data. The zero-knowledge design means this data would be useless without individual master passwords, but the [handling breaches](/password-managers/handling-breaches/) scenario would still require users to take precautionary steps.

4. **Supply chain attack.** Compromise of NordPass's build or distribution pipeline could push malicious updates. Closed-source code makes detection harder than with open-source alternatives.

For more on these scenarios, see our guide on [what happens if a password manager gets hacked](/password-managers/what-if-hacked/).

## The Offline Alternative

Users who prefer to avoid trusting any company's cloud infrastructure entirely can use offline password managers. The KeePass format, supported by tools like PanicVault, keeps your encrypted vault on your own devices with no cloud dependency. PanicVault provides a native Apple experience with KeePass-format vaults, combining the security of local-first storage with modern usability. No subscription, no cloud servers, and an open standard format that prevents vendor lock-in.

## Verdict

NordPass is a safe, technically sound password manager. Its use of XChaCha20 encryption is genuinely forward-thinking, the Cure53 audits provide credible independent assurance, and the zero-knowledge architecture is implemented according to current best practices. The clean breach record since launch is a positive sign.

The reservations are about maturity and transparency. NordPass is younger than its main competitors, closed-source, and carries the indirect reputational weight of the NordVPN breach. None of these are disqualifying -- they simply mean that users who prioritize a longer track record or open-source verifiability have other options.

For users already in the Nord ecosystem, NordPass is a strong choice. For users choosing a password manager fresh, it is worth comparing against [Bitwarden](/password-managers/is-bitwarden-safe/) (open source, free tier) and [1Password](/password-managers/is-1password-safe/) (Secret Key, longest track record) to see which trust model and feature set best matches your needs. For a broader look at [whether password managers are safe](/password-managers/are-password-managers-safe/), see our comprehensive guide.

## Related Articles

- [Are Password Managers Safe?](/password-managers/are-password-managers-safe/)
- [Zero-Knowledge Encryption Explained](/password-managers/zero-knowledge-encryption/)
- [What Happens If a Password Manager Gets Hacked?](/password-managers/what-if-hacked/)
- [Password Manager Pricing Comparison](/compare/pricing-comparison/)
- [Handling Password Manager Breaches](/password-managers/handling-breaches/)
