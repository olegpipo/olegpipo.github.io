---
title: "How TOTP Works: A Technical Explainer"
description: "Understand how Time-Based One-Time Passwords (TOTP) work under the hood, including RFC 6238, HMAC-SHA1, shared secrets, time steps, and the code generation algorithm."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Two-Factor Authentication"
---

Time-Based One-Time Passwords are one of the most widely deployed [two-factor authentication](/two-factor-authentication/) methods in the world. Every 30 seconds, your authenticator app generates a new six-digit code without contacting any server. The service you are logging into independently computes the same code and checks for a match. This article explains exactly how that process works, from the cryptographic primitives to the final digit extraction.

Understanding TOTP at a technical level is not just an academic exercise. It helps you evaluate the security of different [authenticator apps](/two-factor-authentication/best-authenticator-apps/), understand why backup matters, and make informed decisions about using TOTP in a [password manager](/two-factor-authentication/password-manager-as-authenticator/).

## The Standards: RFC 4226 and RFC 6238

TOTP is built on two IETF standards that define the algorithm precisely enough for any compliant implementation to generate identical codes.

**RFC 4226 -- HOTP: An HMAC-Based One-Time Password Algorithm** (2005) defines the foundation. HOTP generates a one-time password from a shared secret and a counter value. Each time you use a code, the counter increments. The security relies on the HMAC (Hash-based Message Authentication Code) construction and the assumption that the counter stays synchronized between client and server.

**RFC 6238 -- TOTP: Time-Based One-Time Password Algorithm** (2011) extends HOTP by replacing the counter with a value derived from the current time. Instead of incrementing a counter manually, TOTP divides the current Unix timestamp by a time step (default: 30 seconds) to produce a counter value. This eliminates the synchronization problem of HOTP -- both parties compute the counter from their clocks, which are kept in sync via NTP.

The relationship is simple: TOTP is HOTP where the counter is `floor(current_unix_time / time_step)`.

## The Shared Secret

Every TOTP setup begins with a shared secret -- a random byte string that both the server and your authenticator app know. This secret is the cryptographic key that makes the system work.

### Secret Generation

The server generates the shared secret when you enable 2FA on your account. RFC 4226 recommends a minimum secret length of 128 bits (16 bytes), but most implementations use 160 bits (20 bytes) to match the output length of SHA-1, the default hash algorithm. Some services use longer secrets when paired with SHA-256 (32 bytes) or SHA-512 (64 bytes).

The secret must be generated using a cryptographically secure random number generator. If the secret is predictable or has insufficient entropy, the entire system collapses -- an attacker who can guess or derive the secret can generate valid codes indefinitely.

### Secret Exchange

The shared secret is communicated to your authenticator app exactly once, during initial setup. The most common method is a QR code that encodes a URI in the `otpauth://` format:

```
otpauth://totp/ExampleService:user@example.com?secret=JBSWY3DPEHPK3PXP&issuer=ExampleService&algorithm=SHA1&digits=6&period=30
```

The components of this URI:

- **Type**: `totp` (as opposed to `hotp`)
- **Label**: The service name and account identifier
- **secret**: The shared secret encoded in Base32
- **issuer**: The service name (for display purposes)
- **algorithm**: The HMAC hash function (SHA1, SHA256, or SHA512)
- **digits**: The length of the generated code (6 or 8)
- **period**: The time step in seconds (almost always 30)

The QR code is simply this URI rendered as a 2D barcode. Scanning it with your authenticator app extracts the parameters and stores them.

### Secret Storage

Once exchanged, the shared secret must be stored securely by both parties.

**Server-side**: The server stores the secret in its database, typically encrypted at rest. Unlike password hashes, the TOTP secret must be stored in a recoverable form (not hashed) because the server needs the original secret to compute codes. This means a server database breach can expose TOTP secrets. This is a fundamental limitation of TOTP's symmetric-key design, and one reason why FIDO2 hardware keys (which use asymmetric cryptography) are considered more secure.

**Client-side**: Your authenticator app stores the secret in device storage. Standalone apps may rely on the operating system's keychain or encrypted storage. Password managers like PanicVault store TOTP secrets in the encrypted KeePass database alongside your passwords, meaning they are protected by the same [encryption architecture](/keepass/encryption-explained/) -- AES-256 or ChaCha20, with Argon2d key derivation. This approach ensures that TOTP secrets receive the same level of cryptographic protection as your credentials.

## The TOTP Algorithm Step by Step

With the shared secret established, here is how a TOTP code is generated each time you need one.

### Step 1: Compute the Time Counter

The current Unix timestamp (seconds since January 1, 1970, 00:00:00 UTC) is divided by the time step to produce an integer counter value:

```
T = floor(unix_timestamp / time_step)
```

For the default 30-second time step, at Unix timestamp 1707840000 (February 13, 2024, 16:00:00 UTC):

```
T = floor(1707840000 / 30) = 56928000
```

This counter value changes every 30 seconds, which is why the generated code changes at the same interval.

The counter is then encoded as an 8-byte big-endian integer. For our example:

```
T_bytes = 0x0000000003652E80
```

### Step 2: Compute HMAC

The time counter (as bytes) is fed into HMAC along with the shared secret:

```
hmac_result = HMAC-SHA1(secret, T_bytes)
```

HMAC is a construction that turns a hash function into a keyed message authentication code. It computes:

```
HMAC(K, m) = H((K' XOR opad) || H((K' XOR ipad) || m))
```

Where:
- **K'** is the key (shared secret), padded to the hash function's block size
- **opad** is the byte 0x5C repeated to fill the block size
- **ipad** is the byte 0x36 repeated to fill the block size
- **H** is the hash function (SHA-1 by default)
- **||** denotes concatenation

The result of HMAC-SHA1 is a 20-byte (160-bit) value. This is far too long and complex to type as a login code, so the next step extracts a human-friendly number.

### Step 3: Dynamic Truncation

The 20-byte HMAC output is reduced to a 4-byte (31-bit) value through a process called dynamic truncation:

1. Take the last nibble (4 bits) of the HMAC output. This value (0-15) serves as an offset.
2. Starting at that offset, extract 4 bytes from the HMAC output.
3. Mask the most significant bit (to avoid signed integer issues), producing a 31-bit unsigned integer.

In pseudocode:

```
offset = hmac_result[19] & 0x0F
code = ((hmac_result[offset] & 0x7F) << 24)
     | ((hmac_result[offset + 1] & 0xFF) << 16)
     | ((hmac_result[offset + 2] & 0xFF) << 8)
     | (hmac_result[offset + 3] & 0xFF)
```

The dynamic truncation ensures that the extracted value depends on the entire HMAC output (because the offset itself is derived from the output), making it harder to predict or manipulate.

### Step 4: Reduce to the Final Code

The 31-bit integer is reduced to the desired number of digits (typically 6) using modular arithmetic:

```
otp = code % 10^digits
```

For a 6-digit code:

```
otp = code % 1000000
```

The result is zero-padded if necessary. If the computation produces `42367`, the displayed code is `042367`.

### Complete Example

Let us trace through a concrete example:

- **Shared secret** (Base32): `JBSWY3DPEHPK3PXP`
- **Shared secret** (decoded): `Hello!` (0x48656C6C6F21) -- used here for illustration; real secrets are random
- **Unix time**: 1707840059
- **Time step**: 30 seconds
- **T**: floor(1707840059 / 30) = 56928001
- **T as 8 bytes**: 0x0000000003652E81

Computing HMAC-SHA1 of T_bytes using the secret as key produces a 20-byte result. Dynamic truncation extracts 4 bytes, modular arithmetic reduces to 6 digits, and you get your code.

Both your authenticator app and the server perform this identical computation. When the codes match, authentication succeeds.

## Why Codes Expire

TOTP codes change every 30 seconds by design. This expiration serves several security purposes.

**Replay prevention**: A code observed by an attacker (over the shoulder, via a keylogger, through phishing) is only useful for a very narrow window. With [SMS codes that remain valid for 5-10 minutes](/two-factor-authentication/totp-vs-sms/), an attacker has a much wider window to exploit a captured code.

**Statelessness**: Because the code is derived from the current time, neither the client nor the server needs to track which codes have been used. This simplifies implementation and eliminates synchronization issues that plague counter-based HOTP systems.

**Bounded exposure**: Even if an attacker obtains the code through real-time phishing, they must use it within the current (or perhaps the next) time step. Delays in the attack pipeline -- even seconds -- can cause the code to expire.

### Clock Drift and Validation Windows

In practice, clocks are not perfectly synchronized. Your phone's clock might be a few seconds ahead or behind the server's clock. To accommodate this, most server implementations accept codes from a small window of adjacent time steps.

A typical server accepts:

- The current time step (T)
- One step before (T - 1)
- One step after (T + 1)

This means a code is effectively valid for roughly 90 seconds (the current 30-second window plus one on each side), though the exact window depends on where within the current step you generate and submit the code.

Some implementations use a wider window (T +/- 2 or more) at the cost of reduced security. Google's implementation, for example, uses a window of T +/- 1 with an additional resynchronization mechanism that detects and compensates for persistent clock drift.

If your device's clock is significantly wrong (more than a few minutes off), TOTP will fail entirely. Modern devices sync their clocks via NTP (Network Time Protocol) and rarely drift significantly, but this can be an issue on devices with disabled network time synchronization.

## Hash Algorithm Variants

While SHA-1 is the default hash algorithm for TOTP (and the one used by the vast majority of services), RFC 6238 supports SHA-256 and SHA-512 as alternatives.

**SHA-1**: Produces a 160-bit (20-byte) HMAC output. SHA-1 has known collision vulnerabilities for general hashing, but these do not affect HMAC-SHA1. The HMAC construction's security depends on the hash function's pseudorandomness, not its collision resistance. HMAC-SHA1 remains secure for TOTP purposes.

**SHA-256**: Produces a 256-bit (32-byte) HMAC output, truncated through the same dynamic truncation process. Some financial institutions and government systems mandate SHA-256 for its larger security margin.

**SHA-512**: Produces a 512-bit (64-byte) HMAC output. Rarely used in practice but supported by the standard.

For most users, the hash algorithm is not a practical concern -- the service dictates which algorithm to use, and the authenticator app handles it automatically. When choosing a [password manager or authenticator app](/two-factor-authentication/best-authenticator-apps/), verify that it supports all three hash algorithms to ensure compatibility with all services.

## The Security Model

TOTP's security rests on several assumptions:

**The shared secret remains secret.** If an attacker obtains the shared secret, they can generate valid codes indefinitely. Unlike a password, the shared secret cannot be easily changed without re-enrolling 2FA. This is why server-side storage of TOTP secrets is a critical security consideration, and why encrypting your client-side secrets (in a password manager or secure keychain) matters.

**The hash function is a secure PRF.** The HMAC construction requires the underlying hash function to behave as a pseudorandom function. As discussed, HMAC-SHA1 meets this requirement despite SHA-1's collision weaknesses.

**Clocks are reasonably synchronized.** The time-based counter depends on both parties agreeing on the current time. NTP handles this in practice, but a compromised NTP source could theoretically manipulate time to force reuse of codes.

**The code has enough entropy.** A 6-digit code provides roughly 20 bits of entropy (10^6 = 1,048,576 possible values, approximately 2^20). This is not strong enough to resist offline attacks, but TOTP is designed for online verification where the server limits attempts. Most services lock accounts after a small number of failed 2FA attempts.

### What TOTP Does Not Protect Against

TOTP is not a silver bullet. Understanding its limitations matters as much as understanding its strengths.

**Real-time phishing**: An attacker operating a reverse proxy phishing site can capture and relay your TOTP code to the real service before it expires. TOTP raises the bar significantly compared to password-only authentication, but it does not provide cryptographic phishing resistance. Only FIDO2/WebAuthn achieves that.

**Malware on the device**: If malware on your phone can read the authenticator app's storage, it can extract the shared secret and generate codes. Device-level security (OS updates, app sandboxing, avoiding sideloaded software) is the defense here.

**Server compromise**: If the server's database of TOTP secrets is breached, every user's second factor is compromised. Unlike password databases where proper hashing provides significant protection even after a breach, TOTP secrets must be stored reversibly and are immediately usable by an attacker.

## TOTP in Password Managers

A growing number of users store their TOTP secrets alongside their passwords in a password manager. This is convenient -- you copy the code from the same app that autofills your password -- and it provides automatic encrypted backup of your TOTP secrets.

The security tradeoff is worth understanding. When TOTP secrets and passwords are in the same vault, compromising the vault compromises both factors simultaneously. The "two" in two-factor authentication becomes more like "one and a half" from a theoretical perspective.

In practice, the threat model makes this acceptable for most people. The password database is protected by strong [encryption](/keepass/encryption-explained/) and a master passphrase. If that encryption is broken (which requires either cracking the passphrase or finding a flaw in AES-256/ChaCha20), the attacker has access to everything regardless. Meanwhile, the convenience means users actually enable TOTP on every account rather than just a handful, which is a substantial net security improvement.

For high-value accounts where you want maximum factor separation, use a dedicated hardware security key. For everything else, TOTP in your password manager is a pragmatic and effective choice. PanicVault, for example, stores TOTP secrets in standard KeePass OTP fields within the encrypted database, so they are backed up and synchronized across devices automatically through your normal [database management](/keepass/data-portability/) workflow.

## The Bigger Picture

TOTP is a pragmatic, well-designed protocol that provides strong second-factor authentication for the vast majority of use cases. Its reliance on symmetric cryptography (shared secrets) means it is not as theoretically robust as asymmetric approaches like FIDO2, but its simplicity, wide compatibility, and offline operation make it the most practical 2FA method for most people.

The key takeaways for users:

- Your TOTP secrets are as sensitive as your passwords. Protect them accordingly.
- Back up your secrets. Losing access to your authenticator without backup codes is a serious problem. Using a password manager that stores TOTP secrets provides automatic encrypted backup.
- TOTP is vastly superior to [SMS-based 2FA](/two-factor-authentication/totp-vs-sms/), but it is not phishing-proof. For your most critical accounts, consider hardware security keys.
- The 30-second code rotation is a feature, not an inconvenience. It bounds the window of vulnerability for any intercepted code.

The fact that TOTP works the same way everywhere -- from Google to your bank to a self-hosted Nextcloud instance -- is a testament to the power of open standards. RFC 6238 gave the world a common, interoperable, and secure second-factor protocol, and it continues to serve that role well.
