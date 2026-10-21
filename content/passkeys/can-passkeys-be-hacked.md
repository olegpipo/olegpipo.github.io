---
title: "Can Passkeys Be Hacked? Security Model Explained"
description: "Honest analysis of passkey security: why passkeys resist phishing, what threats remain (account recovery, password fallback, cloud accounts), and how safe a passkey stored in a KeePass database is."
date: 2026-02-14
lastmod: 2026-10-21
draft: false
silo: "Passkeys & Passwordless"
aliases:
  - /passkeys/phishing-resistant/
---

Passkeys are widely described as unhackable, phishing-proof, and more secure than any password-based system. Those descriptions are mostly accurate, but "mostly" is not the same as "entirely." If you are considering adopting passkeys -- or have already started -- you deserve a clear-eyed analysis of what passkeys protect against, where vulnerabilities remain, and what realistic threats look like. This article, part of our [passkeys and passwordless authentication](/passkeys/) guide, provides that analysis.

## What Passkeys Definitively Prevent

Before examining potential weaknesses, it is important to establish the attacks that passkeys genuinely eliminate. These are not incremental improvements -- they are entire categories of attack that become structurally impossible.

### Phishing

With passwords, a convincing fake website can trick you into entering your credentials. With passkeys, authentication is cryptographically bound to the legitimate website's domain. Your device will not respond to an authentication challenge from a spoofed domain, period. No amount of social engineering can change this because the check happens at the protocol level, not the human level.

The check works in three places, none of which depends on you reading the address bar:

1. **The browser** only lets a page request a passkey for its own domain (the "relying party ID"). A page on `bank-secure.com` cannot ask for the `bank.com` passkey, so none is offered.
2. **The signed data** includes the page's real origin (in WebAuthn's `clientDataJSON`) and a hash of the relying party ID, both filled in by the browser and authenticator rather than by the website.
3. **The real server** rejects any signature made for a different origin or relying party, even if the signature itself is valid.

This alone is transformative. With 3.4 billion phishing emails sent daily, phishing is the single largest vector for credential theft, and passkeys take the stolen-password half of it off the table.

### How It Plays Out Against Real Phishing

- **Lookalike domain.** An email links to `bank-verify.com`, a pixel-perfect copy of your bank. With a password, you type it in and it is gone. With a passkey, the fake site cannot request your `bank.com` credential, so your device offers nothing to approve.
- **Homograph domain.** An attacker registers `bаnk.com` with a Cyrillic "а" that looks identical in the address bar. To the browser it is a different domain, so no passkey matches.
- **Real-time phishing proxy.** A phishing kit relays the real site's pages through the attacker's server, capturing passwords and one-time codes as you type them -- one of the most effective attacks against password-plus-2FA. A passkey ceremony through the proxy is either refused or signed for the proxy's domain, which the real server rejects.

What these scenarios have in common is that the passkey is never offered to the wrong site. The weak points are elsewhere: the password you still have on the account, and the account recovery process (see below).

### Credential Stuffing

When passwords leak from one service, attackers try them on other services. Since 94 percent of passwords are reused, these attacks succeed at alarming rates. Passkeys are unique per website by cryptographic design -- there is no credential to stuff.

### Brute Force and Dictionary Attacks

Password hashes can be cracked offline using GPU-accelerated tools. Passkeys do not store anything on the server that can be cracked. The server holds only the public key, which cannot be used to derive the private key with any computationally feasible method.

### Server-Side Breaches (of Authentication Data)

When a service is breached and password hashes are stolen, it is a crisis. When a service is breached and passkey public keys are stolen, it is a non-event. Public keys are, by definition, not secret. An attacker with your public key cannot authenticate as you.

### Keylogging

Traditional keyloggers capture passwords as you type them. Passkeys involve no typing. The private key is released by a biometric check or device PIN handled by the secure hardware on your device, not by keyboard input that can be intercepted by malware running in the operating system layer.

## Where Vulnerabilities Remain

Passkeys are not magic. They shift the security boundary from "the user must protect a shared secret" to "the user must protect their device and cloud account." That shift eliminates many attacks but introduces a different set of considerations.

### Device Compromise

If an attacker gains physical access to your unlocked device, they have access to your passkeys. This is true of any authentication method stored on a device, including passwords in a [password manager](/password-managers/). The mitigating factor is that passkeys require user verification (Face ID, Touch ID, or device PIN) for each use, so a device must be both unlocked and in the attacker's physical presence during the authentication attempt.

The more serious scenario is malware with elevated privileges on your device. If malware gains root or kernel-level access, it could theoretically interact with the operating system's credential APIs. Copying your passkeys out is much harder: on Apple devices, passkeys are stored in iCloud Keychain, whose encryption keys are protected by the [Secure Enclave](/apple/secure-enclave/) -- a separate processor with its own security boundary -- and each use requires Face ID, Touch ID or your device passcode. A passkey on a hardware security key goes further: the private key never leaves the key at all.

### Cloud Account Compromise

Synced passkeys (the default on Apple, Google, and most third-party managers) are stored in a cloud-synced credential manager. If an attacker compromises your Apple ID, they could potentially access your passkeys on a new device. The same applies to passkeys synced through Chrome -- see [is Google Password Manager safe](/password-managers/is-chrome-passwords-safe/) for how that sync model works and what 2026 research found about it.

Apple mitigates this through several mechanisms:
- End-to-end encryption means Apple cannot read your passkey data.
- Reading your keychain on a new device can require the passcode of one of your other devices.
- [Two-factor authentication](/two-factor-authentication/) on your Apple ID is mandatory for passkey sync.
- iCloud Keychain recovery requires knowledge of your device passcode and multiple verification steps.

The practical risk is low, but it makes protecting your Apple Account (or Google account) critically important. A strong, unique password and two-factor authentication on your cloud account are non-negotiable.

### Passkeys Stored in a KeePass Database

Where the private key lives decides the risk, and a KeePass database is a different place again. KeePassXC stores each passkey, private key included, in the entry's custom fields (prefixed `KPEX_PASSKEY_`) inside your encrypted `.kdbx` file, and other KeePass-compatible apps such as PanicVault use the same format. That means a passkey in your vault is exactly as safe as two things:

- **The vault's own protection** -- your master password, plus a key file or YubiKey if you use one. Anyone who has the file and can unlock it has your passkeys.
- **Wherever the `.kdbx` file is stored and synced** -- iCloud Drive, Google Drive, Dropbox or a USB stick. The file is encrypted, so a copy on its own is not enough, but every copy is one more place an attacker can try to guess your master password offline.

The trade-off is control: no Apple Account or Google account can be hijacked to reach these passkeys, and you can back them up and move them like any other entry. In return, the strength of your master password carries the whole load. See [passkeys and your KeePass database](/passkeys/keepass-and-passkeys/) for which KeePass apps support passkeys today.

### Account Recovery Attacks

This is arguably the weakest link in the passkey security chain, and it has nothing to do with passkeys themselves. Most websites that support passkeys also maintain alternative authentication methods: password-based login, email-based password reset, security questions, or customer support-based recovery.

An attacker who cannot compromise your passkey might instead target the recovery process. If they can reset your password through email, or convince customer support to bypass authentication, the passkey is irrelevant.

The same goes for the password you keep as a fallback. Phishing protection only applies when you actually sign in with the passkey: if you type the account's password on a device without your passkeys, that sign-in is as phishable as ever. Attackers can also try to push you there on purpose. In August 2025, Proofpoint researchers demonstrated a [FIDO authentication downgrade](https://www.proofpoint.com/us/blog/threat-insight/dont-phish-let-me-down-fido-authentication-downgrade) in which an adversary-in-the-middle phishing page makes passkey sign-in fail and steers the victim to a less secure method it can intercept. Proofpoint had not seen it used in the wild, but the lesson holds: if a site you normally open with a passkey suddenly asks for your password or a code, treat that as a warning sign, not a glitch.

This is an industry-wide challenge. As passkeys become more common, services will need to strengthen their recovery processes to match the security level of passkey authentication. Until then, your passkey-protected accounts are only as strong as their weakest authentication method.

### Social Engineering (Non-Phishing)

Passkeys prevent phishing -- tricking you into authenticating on a fake website. They do not prevent all forms of social engineering. An attacker could still:

- Convince you to add their device to your cloud account.
- Trick you into approving an authentication request you did not initiate.
- Social-engineer customer support into resetting your account.

These attacks are harder to execute than phishing but not impossible. The defense is awareness and ensuring your cloud account recovery processes are locked down.

### SIM Swapping (Indirect)

Passkeys themselves are not vulnerable to SIM swapping. However, if your cloud account recovery process involves SMS verification, a SIM swap could allow an attacker to compromise your cloud account and gain access to synced passkeys. This is another argument for using app-based or hardware-based [two-factor authentication](/two-factor-authentication/) rather than SMS.

### Theoretical Cryptographic Attacks

The cryptographic algorithms used by passkeys (ECDSA with P-256, or RSA) are considered secure by current standards. However, quantum computing poses a theoretical long-term threat to public-key cryptography. A sufficiently powerful quantum computer could derive private keys from public keys.

This is not a near-term concern. Current quantum computers are far from being able to break the algorithms used by passkeys. The FIDO Alliance is actively working on post-quantum cryptographic migration paths. By the time quantum computers pose a real threat, the standards will have evolved to use quantum-resistant algorithms.

## Realistic Threat Assessment

For the average consumer, the realistic threats to passkey-protected accounts are:

1. **Account recovery process exploitation** -- the most likely attack vector, and it targets the website's recovery mechanisms, not the passkey itself.
2. **Cloud account compromise** -- mitigated by strong cloud account security.
3. **Physical device theft with PIN knowledge** -- limited scope, requires both the device and knowledge of the unlock PIN.
4. **Advanced persistent threats with device malware** -- relevant for high-value targets (journalists, executives, activists), and made expensive on Apple devices by the hardware-protected keychain and the biometric or passcode check on every use.

For comparison, the realistic threats to password-protected accounts include all of the above plus phishing, credential stuffing, brute force attacks, server-side breaches, and keylogging. The threat surface with passkeys is dramatically smaller.

## How to Maximize Passkey Security

Given the actual threat landscape, here are concrete steps to make your passkey usage as secure as possible:

### Protect Your Cloud Account

Your Apple ID (or Google account, or password manager account) is the key to your synced passkeys. Treat it accordingly:
- Use a strong, unique password.
- Enable hardware key-based [two-factor authentication](/two-factor-authentication/) if available.
- Review trusted devices regularly and remove old ones.
- Use an app-based authenticator rather than SMS for any secondary verification.

### Use Strong Device Security

- Set a strong device passcode (six digits minimum, alphanumeric preferred).
- Enable [Face ID or Touch ID](/apple/face-id-touch-id-setup/) for biometric authentication.
- Keep your operating system updated to receive security patches.
- Enable remote wipe capability (Find My iPhone / Find My Mac) in case of device theft.

### Harden Account Recovery

Where possible, review and strengthen the recovery options on your most important accounts:
- Disable SMS-based recovery if better options are available.
- Set up backup authentication methods like hardware security keys.
- Store recovery codes securely (in your [password manager](/password-managers/) or a physical safe).

### Keep Passwords as Backup -- Securely

Most services maintain password-based login as a fallback for passkeys. These fallback passwords should still be strong and unique, stored in a password manager. A weak fallback password undermines the security of a passkey-protected account.

If you use a KeePass-compatible tool like PanicVault, you can store both your passkeys and your fallback passwords in the same encrypted [KDBX database](/keepass/), keeping everything organized and portable.

### Monitor for Unauthorized Access

Check your account activity logs regularly. If someone bypasses your passkey through an alternative authentication method, the activity log may show the anomaly before further damage occurs.

## Passkeys vs. Other Authentication Methods: Security Comparison

| Attack Vector | Password Only | Password + MFA | Passkey | Hardware Security Key |
|---|---|---|---|---|
| Phishing | Vulnerable | Partially vulnerable | Resistant (passkey itself) | Resistant |
| Credential stuffing | Vulnerable | Vulnerable (password layer) | Immune | Immune |
| Server breach | Vulnerable (hash cracking) | Vulnerable (password layer) | Immune | Immune |
| Keylogging | Vulnerable | Partially vulnerable | Immune | Immune |
| Device theft (unlocked) | N/A | Vulnerable | Vulnerable | Immune (key needed) |
| Cloud account compromise | N/A | N/A | Vulnerable (synced keys) | Immune (device-bound) |
| Account recovery attack | Vulnerable | Vulnerable | Vulnerable | Vulnerable |
| SIM swap | N/A | Vulnerable (if SMS MFA) | Indirect risk | Immune |

## The Bottom Line

Can passkeys be hacked? In the traditional sense of stealing credentials through phishing, brute force, or server breaches -- no. Those attacks are structurally prevented by the cryptographic architecture.

Can accounts protected by passkeys be compromised? Yes, through cloud account compromise, account recovery exploitation, or device-level attacks. But these attack vectors are harder to exploit, more expensive for attackers, and affect far fewer people than the mass-scale attacks that passkeys eliminate.

Passkeys do not provide perfect security. Nothing does. What they provide is a massive reduction in attack surface compared to passwords, with the remaining risks being manageable through standard device and account security practices. For most people, passkeys represent the most significant practical improvement in personal security available today.

The question is not whether passkeys are hackable in theory. The question is whether they are more secure than what you are using now. The answer, for almost everyone, is decisively yes.

## Related Articles

- [What Are Passkeys? Complete Guide](/passkeys/what-are-passkeys/)
- [Passkeys and Your KeePass Database](/passkeys/keepass-and-passkeys/)
- [The Transition: Managing Passwords and Passkeys Together](/passkeys/managing-both/)
- [Apple Secure Enclave Explained](/apple/secure-enclave/)
