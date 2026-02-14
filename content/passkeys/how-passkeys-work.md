---
title: "How Passkeys Work: FIDO2 and WebAuthn Explained"
description: "Technical explainer of how passkeys work under the hood. Covers the FIDO2 framework, WebAuthn API, registration and authentication flows, and authenticator types."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Passkeys & Passwordless"
---

Passkeys are often described as "passwordless login" or "the replacement for passwords," which is accurate but incomplete. Understanding how passkeys actually work at a technical level helps you evaluate their security properties, troubleshoot issues, and make informed decisions about where and how to use them. This guide, part of our [passkeys and passwordless authentication](/passkeys/) resource, explains the protocols, cryptography, and architecture behind passkeys without requiring a computer science degree.

## The Standards Behind Passkeys

Passkeys are built on two open standards developed by the FIDO Alliance and the World Wide Web Consortium (W3C):

**FIDO2** is the overarching framework for passwordless authentication. It defines the architecture, security model, and requirements for the entire ecosystem. FIDO stands for Fast Identity Online.

**WebAuthn** (Web Authentication API) is the specific web standard within FIDO2 that defines how browsers and websites communicate during passkey creation and authentication. It is a W3C recommendation, meaning it is an official web standard implemented by all major browsers.

**CTAP2** (Client to Authenticator Protocol 2) is the companion protocol that defines how the browser communicates with the authenticator -- the component that stores and uses the private keys. The authenticator might be your phone's Secure Enclave, a hardware security key like a YubiKey, or a platform credential manager like iCloud Keychain.

Together, these standards create an end-to-end authentication system that eliminates passwords while maintaining interoperability across browsers, platforms, and devices.

## Public-Key Cryptography: The Foundation

To understand passkeys, you need a basic mental model of public-key cryptography. If you already know how this works, skip ahead.

Public-key cryptography uses pairs of mathematically related keys:

- **Private key**: Kept secret. Only you (or your device) have it.
- **Public key**: Shared openly. Anyone can have it.

The relationship between the keys has a crucial property: data encrypted with the public key can only be decrypted with the private key, and data signed with the private key can be verified with the public key. Critically, knowing the public key does not allow you to derive the private key. This mathematical asymmetry is the foundation of passkey security.

With passwords, both you and the server know the secret (the password). With passkeys, only your device knows the secret (the private key), and the server only has the public key, which is useless for impersonation.

## The Registration Flow (Creating a Passkey)

When you create a passkey for a website, the following happens:

### Step 1: The Server Sends a Challenge

The website (called the "relying party" in the specification) generates a random challenge -- a large, unpredictable number -- and sends it to your browser along with parameters that describe what kind of credential it wants:

- The relying party ID (typically the website's domain, like `example.com`)
- The user's account identifier
- Supported cryptographic algorithms (usually ES256 or RS256)
- Optional parameters like whether to require user verification (biometrics/PIN)

This information is passed to the browser through the WebAuthn API's `navigator.credentials.create()` function.

### Step 2: The Browser Talks to the Authenticator

Your browser passes the challenge to the authenticator. On an iPhone, the authenticator is the Secure Enclave chip that is hardware-isolated from the main processor. On a Mac, it is the T2 or Apple Silicon security chip. On a Windows PC, it is the TPM (Trusted Platform Module).

The authenticator:

1. Prompts you for user verification -- Face ID, Touch ID, fingerprint, or device PIN.
2. Once verified, generates a new key pair (private and public) specific to this website.
3. Stores the private key securely, associated with the relying party ID.
4. Creates an "attestation object" containing the public key, a credential ID, and optionally information about the authenticator itself.
5. Signs the challenge and the attestation object with the new private key.

### Step 3: The Response Goes Back to the Server

The browser sends the signed attestation object back to the website. The website:

1. Verifies the signature using the public key.
2. Stores the public key and credential ID associated with the user's account.
3. Confirms the registration.

At no point does the private key leave the authenticator. The website never sees it, the browser never sees it, and no network observer can intercept it.

## The Authentication Flow (Signing In)

When you use a passkey to log in, the flow is similar but simpler:

### Step 1: The Server Sends a New Challenge

The website generates a fresh random challenge and sends it to the browser through `navigator.credentials.get()`. It includes the relying party ID and optionally a list of credential IDs it knows about for the user.

### Step 2: The Authenticator Signs the Challenge

Your browser passes the challenge to the authenticator, which:

1. Looks up the private key associated with the relying party ID.
2. Prompts you for user verification (Face ID, Touch ID, etc.).
3. Signs the challenge and additional authentication data (like a counter value) with the private key.
4. Returns the signed assertion to the browser.

### Step 3: The Server Verifies the Signature

The website uses the stored public key to verify the signature on the assertion. If the signature is valid and the challenge matches, the user is authenticated.

The entire process takes one to three seconds from the user's perspective. Behind the scenes, the cryptographic operations happen in milliseconds.

## Why This Architecture Defeats Common Attacks

Understanding the flow makes it clear why passkeys are resistant to attacks that plague passwords:

### Phishing Resistance

The relying party ID is cryptographically bound into the credential. When your authenticator stores a passkey for `bank.com`, it will only use that passkey for challenges from `bank.com`. If a phishing site at `bank-secure.com` or `bank.com.evil.site` requests authentication, the authenticator has no matching passkey and will not respond.

This is enforced at the protocol level, not the user level. Even the most sophisticated phishing attack -- a pixel-perfect copy of the real site -- fails because the domain does not match. For a deeper analysis, see [why passkeys are phishing-resistant](/passkeys/phishing-resistant/).

### Server Breach Resistance

If an attacker breaches the server and steals the stored public keys and credential IDs, they cannot use them to authenticate. Public keys, by definition, cannot generate valid signatures. There is no equivalent of "cracking a password hash" with passkeys.

### Replay Attack Resistance

Each authentication uses a fresh, random challenge from the server. Even if an attacker intercepted a signed assertion, it would be useless for future authentication because the challenge would be different. Additionally, authenticators maintain a signature counter that increments with each use, allowing servers to detect cloned credentials.

### Man-in-the-Middle Resistance

The assertion includes the origin (the website's URL) and is bound to the TLS channel. A man-in-the-middle attacker would need to modify the assertion, which would invalidate the cryptographic signature.

## Authenticator Types

The FIDO2 specification supports two types of authenticators:

### Platform Authenticators

These are built into your device. On an iPhone, it is the [Secure Enclave](/apple/secure-enclave/). On a Mac with Apple Silicon, it is the integrated security chip. On a Windows PC, it is the TPM.

Platform authenticators are the most convenient because they are always present. When you create a passkey on your iPhone and authenticate with Face ID, you are using a platform authenticator.

### Roaming Authenticators

These are external devices like hardware security keys (YubiKey, Google Titan Key). They connect via USB, NFC, or Bluetooth and can be used across multiple devices.

Roaming authenticators are often used in enterprise environments where higher assurance is needed. They create device-bound passkeys that cannot be synced or exported, providing stronger guarantees about where the private key exists.

## Synced Credentials vs. Device-Bound Credentials

One of the most significant developments in the passkey ecosystem is the distinction between synced and device-bound credentials.

### Synced Passkeys (Multi-Device Credentials)

When Apple, Google, or a third-party [password manager](/password-managers/) syncs your passkeys across devices, the private key is encrypted and replicated through a cloud service. Apple uses iCloud Keychain. Google uses Google Password Manager. Third-party managers use their own sync infrastructure.

The private key is still protected by end-to-end encryption -- Apple, for example, cannot read your passkey private keys even though they transit Apple's servers. But the key does exist on multiple devices, which changes the security model compared to a hardware security key where the key exists on exactly one device.

For most consumers, synced passkeys are the right trade-off. They provide excellent security while solving the practical problem of device loss and multi-device access. For details on how this works across platforms, see [how to sync passkeys across devices](/passkeys/sync-across-devices/).

### Device-Bound Passkeys

Hardware security keys and some enterprise configurations create passkeys that exist on exactly one device. If that device is lost, the passkey is gone. This is more secure against certain threats (a compromised cloud account cannot be used to export your keys) but less convenient.

## The Role of Attestation

During registration, the authenticator can optionally provide attestation -- a signed statement about itself. This tells the relying party what kind of authenticator was used (hardware key, platform authenticator, software-based) and provides cryptographic proof.

In practice, most consumer-facing websites do not check attestation. Enterprise and government applications are more likely to require it, ensuring that only approved hardware or platforms are used for authentication.

## The WebAuthn API in Practice

For developers, the WebAuthn API is relatively straightforward. The two core functions are:

**`navigator.credentials.create()`** -- Used during registration. Takes a configuration object specifying the relying party, user information, supported algorithms, and challenge. Returns the attestation object containing the public key.

**`navigator.credentials.get()`** -- Used during authentication. Takes a challenge and optional credential ID hints. Returns the signed assertion.

The browser handles all communication with the authenticator, and the operating system manages biometric prompts and secure key storage. This abstraction is what makes passkeys work consistently across different browsers and platforms.

## How This Connects to Your Password Manager

If you use a password manager that supports passkeys, the password manager registers itself as a credential provider with the operating system. When a website calls `navigator.credentials.create()`, the operating system can route the request to your password manager instead of (or in addition to) the platform's built-in credential store.

This is how tools like 1Password, Bitwarden, and KeePass-compatible applications like PanicVault can store passkeys alongside your traditional passwords. On Apple devices, this integration happens through the [credential provider extension framework](/apple/credential-provider-extensions/). The result is a unified experience where your password manager handles both passwords and passkeys through the same interface.

For the broader picture of how the password management industry is incorporating passkeys, see [how password managers are adapting to passkeys](/passkeys/password-managers-adapting/).

## Practical Implications

Understanding the technical architecture leads to several practical conclusions:

1. **Passkeys are as secure as the device they are stored on.** The private key's security depends on the authenticator. Apple's [Secure Enclave](/apple/secure-enclave/) is hardware-isolated and well-audited. A software-based authenticator on an unpatched device is weaker. Keep your devices updated.

2. **The domain binding is the anti-phishing mechanism.** You do not need to check URLs or look for padlock icons. The protocol does it for you. This is why passkeys are described as [phishing-resistant by design](/passkeys/phishing-resistant/).

3. **Synced passkeys are protected by your cloud account.** If you use iCloud Keychain, your Apple ID becomes a critical security boundary. Protect it with a strong password and [two-factor authentication](/two-factor-authentication/).

4. **Passkeys do not protect the account recovery process.** Most sites still offer password-based fallback and email-based recovery. An attacker who compromises your email may still be able to access your accounts. See [can passkeys be hacked?](/passkeys/can-passkeys-be-hacked/) for a thorough threat analysis.

5. **You need both passkeys and passwords for now.** The transition is ongoing. A [password manager](/password-managers/) that handles both gives you the most practical and secure setup during this [hybrid period](/passkeys/managing-both/).

The technology behind passkeys is elegant, well-standardized, and backed by the strongest players in the technology industry. Understanding how it works is not necessary for using it, but it builds justified confidence that passkeys are not just a convenience feature -- they are a fundamental improvement in authentication security.

## Related Articles

- [What Are Passkeys? Complete Guide for 2026](/passkeys/what-are-passkeys/)
- [Can Passkeys Be Hacked? Security Model Explained](/passkeys/can-passkeys-be-hacked/)
- [Why Passkeys Are Phishing-Resistant](/passkeys/phishing-resistant/)
- [How Password Managers Are Adapting to Passkeys](/passkeys/password-managers-adapting/)
- [Apple Secure Enclave Explained](/apple/secure-enclave/)
