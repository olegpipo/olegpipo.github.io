---
title: "What Are Passkeys? Complete Guide for 2026"
description: "Learn what passkeys are, how they replace passwords with public-key cryptography, and why they represent the biggest shift in authentication technology in decades."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Passkeys & Passwordless"
---

Passkeys are the most significant advancement in authentication technology since passwords were first introduced in the 1960s. If you have been following the security landscape, you have likely heard the term used by Apple, Google, and Microsoft -- but the details often get lost in marketing language. This guide, part of our comprehensive [passkeys and passwordless authentication](/passkeys/) series, explains what passkeys actually are, how they differ from everything that came before, and what they mean for your daily digital life.

## The Problem Passkeys Solve

To understand passkeys, you first need to understand why passwords fail. A password is a shared secret. When you create an account, you choose a password, and the website stores a version of it (ideally a cryptographic hash, though not all services follow best practices). When you log in, you type the password, the site checks it against the stored version, and you are in.

This model has several structural weaknesses that no amount of password complexity can fix:

**Passwords can be stolen in transit.** Even with HTTPS, passwords travel from your device to the server. Man-in-the-middle attacks, compromised TLS certificates, and malicious proxies can intercept them.

**Passwords can be phished.** If someone builds a convincing replica of your bank's login page, nothing in the password protocol prevents you from typing your real password into the fake site. With 3.4 billion phishing emails sent daily, this is not a theoretical concern.

**Passwords can be breached at rest.** When a service is hacked, the stored password hashes can be extracted. Weak hashing algorithms or poor implementation can allow attackers to recover the original passwords. Even strong hashes can be brute-forced with modern hardware.

**Passwords are reused.** The average person manages approximately 250 passwords, and research consistently shows that 94 percent of passwords are reused or duplicated across services. A breach at one site effectively compromises dozens of others.

**Passwords are a user experience burden.** Remembering, typing, resetting, and managing passwords is friction. That friction pushes people toward weak passwords, password reuse, and disabling security features that add even more friction, like [two-factor authentication](/two-factor-authentication/).

## What a Passkey Actually Is

A passkey is a cryptographic credential based on public-key cryptography. Instead of a shared secret (like a password), it uses a key pair: a private key that stays on your device and a public key that the website stores.

Here is how it works in practice:

### Registration (Creating a Passkey)

When you create a passkey for a website:

1. The website sends a challenge to your device -- essentially a random number.
2. Your device generates a new key pair specific to that website. The private key is stored securely on your device, protected by your device's security hardware (the Secure Enclave on Apple devices, TPM on Windows, Titan chip on Pixel phones).
3. Your device signs the challenge with the private key and sends the signature along with the public key back to the website.
4. The website stores the public key associated with your account.

At no point does a secret travel over the network that could be used to impersonate you. The private key never leaves your device. The public key, even if stolen from the website's database, is useless for authentication.

### Authentication (Using a Passkey)

When you log in with a passkey:

1. The website sends a new challenge to your device.
2. Your device asks you to verify your identity -- typically through Face ID, Touch ID, a fingerprint sensor, or a device PIN.
3. Once verified, your device signs the challenge with the private key and sends the signature to the website.
4. The website verifies the signature using the stored public key. If it matches, you are authenticated.

The entire process takes a few seconds. There is nothing to type, nothing to remember, and -- critically -- nothing that can be phished. Your device will only respond to challenges from the legitimate website because the passkey is cryptographically bound to that specific domain.

For a deeper technical dive into the protocols that make this work, see our article on [how passkeys work: FIDO2 and WebAuthn explained](/passkeys/how-passkeys-work/).

## How Passkeys Differ from Passwords

The differences go beyond just "no typing required." Here is a systematic comparison:

| Characteristic | Passwords | Passkeys |
|---|---|---|
| What is stored on the server | Password hash | Public key |
| What the user provides | A secret (the password) | Biometric or PIN to unlock a device key |
| Can be phished | Yes | No -- domain-bound |
| Can be reused across sites | Yes (and often is) | No -- unique per site by design |
| Can be brute-forced | Yes, if hash is leaked | No -- private key never exposed |
| Requires memorization | Yes | No |
| Login speed | Slow (type + possible MFA) | Fast (biometric confirmation only) |

For a thorough comparison of these approaches including practical trade-offs, read our [passkeys vs. passwords](/passkeys/vs-passwords/) analysis.

## How Passkeys Differ from Two-Factor Authentication

You might wonder how passkeys relate to [two-factor authentication](/two-factor-authentication/) methods like TOTP codes, SMS codes, or hardware security keys.

Traditional two-factor authentication adds a second step to password-based login. You enter your password (something you know), then provide a second factor (something you have, like a phone or hardware key). This layered approach improves security, but the password remains a vulnerability. If the password is phished, the attacker often has time windows or social engineering techniques to bypass the second factor.

Passkeys are inherently multi-factor. The private key is something you have (stored on your device). Unlocking it requires something you are (biometric) or something you know (PIN). Both factors are satisfied in a single gesture. This is why passkeys are considered stronger than most traditional two-factor setups while being faster and simpler.

Hardware security keys like YubiKey are the closest predecessor to passkeys. In fact, passkeys are built on the same FIDO2 standard that hardware security keys use. The difference is that passkeys can be synced across devices (what the FIDO Alliance calls "multi-device credentials"), while hardware security keys are bound to a single physical device.

## Synced Passkeys vs. Device-Bound Passkeys

This distinction matters for understanding how passkeys work in practice.

**Synced passkeys** (also called multi-device credentials) are stored in a cloud-synced credential manager like iCloud Keychain, Google Password Manager, or a third-party [password manager](/password-managers/). When you create a passkey on your iPhone, it automatically becomes available on your iPad and Mac through iCloud Keychain. If you lose your phone, your passkeys are not lost -- they are recoverable through your cloud account.

**Device-bound passkeys** are stored on a single device and cannot be exported or synced. Hardware security keys create device-bound passkeys. Some enterprise security policies require device-bound passkeys for higher assurance.

Most consumer passkey implementations in 2026 use synced passkeys, which provides a better user experience. The trade-off is that the security of your passkeys depends partly on the security of your cloud account, which is why protecting your Apple ID, Google account, or password manager with strong credentials and two-factor authentication remains important.

For details on how syncing works across platforms, see our guide to [syncing passkeys across devices](/passkeys/sync-across-devices/).

## Where You Can Use Passkeys Today

Passkey adoption has accelerated significantly since Google, Apple, and Microsoft began supporting them in their platforms. As of 2026, major services that support passkey login include:

- Google (all services)
- Apple ID
- Microsoft accounts
- Amazon
- PayPal
- eBay
- GitHub
- WhatsApp
- LinkedIn
- Best Buy
- Kayak
- Shopify stores

The list grows monthly. Our regularly updated directory of [websites that support passkeys in 2026](/passkeys/supported-sites/) provides comprehensive coverage including setup instructions for each service.

Not every site that supports passkeys requires them. Most currently offer passkeys as an optional alternative to passwords, which means you need to actively set them up. Over time, more services will nudge users toward passkeys as the default, but we are still in the early adoption phase.

## What Happens If You Lose Your Device

This is the question that makes most people hesitate about passkeys. With passwords, you can always do a password reset through email. What happens if you lose the phone that holds your passkeys?

The answer depends on whether you use synced or device-bound passkeys:

**With synced passkeys** (the common case), losing a device does not mean losing your passkeys. They are synced to your cloud account and will appear on any new device you sign into. If you lose your iPhone, your passkeys are still accessible on your iPad, Mac, or a new iPhone once you sign into iCloud.

**With device-bound passkeys**, losing the device means losing access. This is why device-bound passkeys are typically used alongside account recovery mechanisms -- backup codes, recovery keys, or alternative authentication methods.

Most services that support passkeys also maintain password-based login as a fallback, at least for now. This means the worst case for losing a device is typically falling back to your password plus any two-factor authentication you have configured.

## Passkeys and Password Managers

A common misconception is that passkeys make password managers obsolete. In reality, the relationship is more nuanced, and password managers are evolving to become passkey managers too.

Here is why password managers remain essential even as passkeys gain adoption:

1. **Not all sites support passkeys yet.** You will have password-based accounts for years to come.
2. **Password managers can store passkeys.** 1Password, Bitwarden, Dashlane, and others now support passkey storage, giving you a single credential manager.
3. **Password managers handle more than passwords.** Secure notes, documents, credit cards, identities -- these features are not replaced by passkeys.

For KeePass users, the situation is particularly interesting. The KDBX format is being extended to support passkey storage, and KeePass-compatible applications like PanicVault are in a strong position to offer unified credential management within the [Apple ecosystem](/apple/). Our article on [passkeys and your KeePass database](/passkeys/keepass-and-passkeys/) covers this in detail.

For the broader picture of how the password manager industry is responding, see [how password managers are adapting to passkeys](/passkeys/password-managers-adapting/).

## Getting Started with Passkeys

If you are ready to try passkeys, the process is straightforward on modern devices:

1. **Check your device.** You need iOS 16 or later, macOS Ventura or later, Android 9 or later, or Windows 10 or later with a compatible browser.
2. **Pick a site.** Start with a service you use frequently that supports passkeys, like Google or Amazon.
3. **Find the passkey option.** Look in the site's security or account settings for "Passkey," "Sign in with a passkey," or similar wording.
4. **Create the passkey.** Follow the prompts. Your device will ask for biometric confirmation.
5. **Test it.** Sign out and sign back in using the passkey to confirm it works.

For Apple-specific instructions, our step-by-step guide to [setting up passkeys on Apple devices](/passkeys/setup-apple/) walks through the process on iPhone, iPad, and Mac.

## The Bottom Line

Passkeys are not a gimmick or a marginal improvement. They represent a fundamental architectural shift from shared secrets to public-key cryptography, eliminating entire categories of attacks that have plagued passwords for decades. They are faster, more secure, and easier to use than passwords -- a rare trifecta in security technology.

The transition will take time. You will manage both passwords and passkeys for the foreseeable future, which means your [password manager](/password-managers/) is more important than ever. But every account you upgrade to passkeys is one less password that can be phished, breached, or forgotten.

Passkeys are not the future of authentication. They are the present. The only question is how quickly you adopt them.

## Related Articles

- [Passkeys vs. Passwords: Why the Industry Is Moving On](/passkeys/vs-passwords/)
- [How Passkeys Work: FIDO2 and WebAuthn Explained](/passkeys/how-passkeys-work/)
- [How to Set Up Passkeys on Apple Devices](/passkeys/setup-apple/)
- [Why Passkeys Are Phishing-Resistant](/passkeys/phishing-resistant/)
- [Why You Still Need a Password Manager in a Passkey World](/passkeys/still-need-password-manager/)
