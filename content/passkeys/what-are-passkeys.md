---
title: "What Are Passkeys? Complete Guide for 2026"
description: "Learn what passkeys are, how they replace passwords with public-key cryptography, and why they represent the biggest shift in authentication technology in decades."
date: 2026-02-14
lastmod: 2026-10-21
draft: false
silo: "Passkeys & Passwordless"
aliases:
  - /passkeys/how-passkeys-work/
  - /passkeys/vs-passwords/
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

A passkey is a cryptographic credential based on public-key cryptography. Instead of a shared secret (like a password), it uses a key pair: a private key that stays with you -- on your device or in your credential manager -- and a public key that the website stores.

Here is how it works in practice:

### Registration (Creating a Passkey)

When you create a passkey for a website:

1. The website sends a challenge to your device -- essentially a random number.
2. Your device generates a new key pair specific to that website. The private key is saved in your credential manager -- iCloud Keychain on Apple devices, Google Password Manager on Android, Windows Hello on a PC, or a third-party password manager -- or on a hardware security key.
3. Your device signs the challenge with the private key and sends the signature along with the public key back to the website.
4. The website stores the public key associated with your account.

At no point does a secret travel over the network that could be used to impersonate you. The private key is never sent to the website. (A synced passkey does travel between your own devices, but end-to-end encrypted -- see below.) The public key, even if stolen from the website's database, is useless for authentication.

### Authentication (Using a Passkey)

When you log in with a passkey:

1. The website sends a new challenge to your device.
2. Your device asks you to verify your identity -- typically through Face ID, Touch ID, a fingerprint sensor, or a device PIN.
3. Once verified, your device signs the challenge with the private key and sends the signature to the website.
4. The website verifies the signature using the stored public key. If it matches, you are authenticated.

The entire process takes a few seconds. There is nothing to type, nothing to remember, and -- critically -- nothing that can be phished. Your device will only respond to challenges from the legitimate website because the passkey is cryptographically bound to that specific domain.

### Under the Hood: FIDO2, WebAuthn and CTAP

Passkeys are FIDO credentials, built on open standards from the FIDO Alliance and the World Wide Web Consortium (W3C):

- **WebAuthn** (Web Authentication) is the W3C standard that browsers implement. A website calls `navigator.credentials.create()` to register a passkey and `navigator.credentials.get()` to sign in; the browser hands the request to an authenticator and returns the signed result.
- **CTAP** (Client to Authenticator Protocol) defines how a browser or operating system talks to an external authenticator over USB, NFC or Bluetooth -- including the "hybrid" flow that lets your phone sign you in on a nearby computer after you scan a QR code.
- **FIDO2** is the umbrella name for WebAuthn plus CTAP.

**Authenticators** come in two kinds. A *platform authenticator* is built into the device you are using: iCloud Keychain on an iPhone or Mac, Google Password Manager on Android, Windows Hello on a PC, or a third-party password manager registered with the operating system. A *roaming authenticator* is a separate device, such as a YubiKey or Google Titan key, connected by USB, NFC or Bluetooth; it holds device-bound passkeys that never leave the key.

**Attestation** is an optional signed statement an authenticator can attach at registration to say what kind of authenticator it is. Most consumer websites do not ask for it; enterprise and government services sometimes require it so that only approved hardware can register.

Whatever the authenticator, the browser and operating system handle the prompts and key storage. That is why the same passkey works whether a site is opened in Safari, Chrome, Edge or Firefox.

## How Passkeys Differ from Passwords

The differences go beyond just "no typing required." Here is a systematic comparison, including the places where passwords still win:

| Characteristic | Passwords | Passkeys |
|---|---|---|
| What is stored on the server | Password hash | Public key |
| What the user provides | A secret (the password) | Biometric or PIN to unlock the passkey |
| Phishing | Can be typed into a fake site | Resistant -- only offered on the domain it was created for |
| Reuse across sites | Yes (and often is) | No -- unique per site by design |
| If the site's database leaks | Hashes can be cracked | Public keys are useless to an attacker |
| Requires memorization | Yes | No |
| Login speed | Slow (type + possible MFA) | Fast (biometric confirmation only) |
| Works on every site | Yes | Only sites that have added support |
| Signing in on someone else's computer | Type it anywhere | Scan a QR code with your phone, which must be nearby |
| Account recovery | Email reset | Synced copy on your other devices, or the site's fallback |
| Sharing with family or a team | Easy | Only in managers that share passkeys |

### Where Passkeys Still Fall Short

**Recoverability.** Password recovery is familiar: you click an email link and set a new one. Passkey recovery depends on where the passkey lives. A synced passkey survives a lost phone because it is still on your other devices, but losing access to the account that syncs it (your Apple Account, Google account or password manager account) loses every copy, and a passkey on a lost hardware key is simply gone. That is why most sites keep a password or another fallback -- and why attackers target that fallback, as explained in [can passkeys be hacked?](/passkeys/can-passkeys-be-hacked/).

**Shared and enterprise accounts.** A password can be handed to a family member or colleague. A passkey can only be shared inside a credential manager that supports it -- for example, a shared group in Apple's Passwords app or a shared vault in 1Password -- and a passkey on a hardware security key cannot be shared at all. Team service accounts often still depend on a shared password for this reason.

## How Passkeys Differ from Two-Factor Authentication

You might wonder how passkeys relate to [two-factor authentication](/two-factor-authentication/) methods like TOTP codes, SMS codes, or hardware security keys.

Traditional two-factor authentication adds a second step to password-based login. You enter your password (something you know), then provide a second factor (something you have, like a phone or hardware key). This layered approach improves security, but the password remains a vulnerability. If the password is phished, the attacker often has time windows or social engineering techniques to bypass the second factor.

Passkeys are inherently multi-factor. The private key is something you have (stored on your device). Unlocking it requires something you are (biometric) or something you know (PIN). Both factors are satisfied in a single gesture. This is why passkeys are considered stronger than most traditional two-factor setups while being faster and simpler.

Hardware security keys like YubiKey are the closest predecessor to passkeys. In fact, passkeys are built on the same FIDO2 standard that hardware security keys use. The difference is that passkeys can be synced across devices (what the FIDO Alliance calls "multi-device credentials"), while hardware security keys are bound to a single physical device.

## Synced Passkeys vs. Device-Bound Passkeys

This distinction matters for understanding how passkeys work in practice.

**Synced passkeys** (also called multi-device credentials) are stored in a cloud-synced credential manager like iCloud Keychain, Google Password Manager, or a third-party [password manager](/password-managers/). When you create a passkey on your iPhone, it automatically becomes available on your iPad and Mac through iCloud Keychain. If you lose your phone, your passkeys are not lost -- they are recoverable through your cloud account. Apple and Google both sync passkeys end-to-end encrypted, so neither company can read them.

**Device-bound passkeys** are stored on a single device and cannot be exported or synced. Hardware security keys create device-bound passkeys. Some enterprise security policies require device-bound passkeys for higher assurance.

Most consumer passkey implementations in 2026 use synced passkeys, which provides a better user experience. The trade-off is that the security of your passkeys depends partly on the security of your cloud account, which is why protecting your Apple ID, Google account, or password manager with strong credentials and two-factor authentication remains important.

For details on how syncing works on each platform, see our comparison of [Google, Apple and Microsoft passkeys](/passkeys/google-apple-microsoft/).

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

For KeePass users, passkeys already fit in the KDBX file: KeePassXC stores each passkey in the entry's custom fields (prefixed `KPEX_PASSKEY_`), and other KeePass-compatible apps such as PanicVault read the same format, so passwords and passkeys sit in one portable, encrypted database within the [Apple ecosystem](/apple/) and beyond. Our article on [passkeys and your KeePass database](/passkeys/keepass-and-passkeys/) covers this in detail.

To see which password managers support passkeys today, see [managing passwords and passkeys together](/passkeys/managing-both/).

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

- [How to Set Up Passkeys on Apple Devices](/passkeys/setup-apple/)
- [Can Passkeys Be Hacked? Security Model Explained](/passkeys/can-passkeys-be-hacked/)
- [The Transition: Managing Passwords and Passkeys Together](/passkeys/managing-both/)
- [Google, Apple, Microsoft Passkey Implementations Compared](/passkeys/google-apple-microsoft/)
- [Passkeys and Your KeePass Database](/passkeys/keepass-and-passkeys/)
