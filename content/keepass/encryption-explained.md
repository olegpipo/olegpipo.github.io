---
title: "How KeePass Encryption Works: AES-256, Twofish, and ChaCha20"
description: "Deep dive into KeePass encryption algorithms, key derivation with Argon2d and AES-KDF, transform rounds, and inner random stream protection."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

The [KeePass ecosystem](/keepass/) has earned its reputation as one of the most trusted open-source password management platforms, and the encryption architecture is the reason why. Unlike cloud-based password managers that ask you to trust a company's infrastructure, KeePass puts the cryptography front and center -- every design decision is documented, every algorithm is a published standard, and every implementation can be independently verified. This article explains exactly how KeePass encrypts your password database, from the moment you type your master passphrase to the final encrypted bytes stored on disk.

Understanding the encryption pipeline matters even if you never plan to audit the source code yourself. Knowing what protects your data helps you make informed decisions about algorithm choices, key derivation settings, and how much trust to place in your vault's security.

## The Encryption Pipeline Overview

When you save a KeePass database, several layers of cryptographic operations work together:

1. **Key composition** -- Your master passphrase (and optionally a [key file](/keepass/key-files/)) are combined into a composite key.
2. **Key derivation** -- The composite key is processed through a deliberately slow key derivation function (Argon2d or AES-KDF) to produce a derived key.
3. **Outer encryption** -- The derived key encrypts the entire database payload using a symmetric cipher (AES-256, ChaCha20, or Twofish).
4. **Inner random stream** -- Individual protected fields within the database (like passwords) receive an additional layer of encryption using an inner random stream cipher.
5. **Integrity verification** -- HMAC-SHA-256 authenticates the encrypted data to detect tampering.

Each layer addresses a different threat. Key derivation slows brute-force attacks. Outer encryption protects the database at rest. Inner stream protection guards sensitive fields even during database processing. Integrity verification ensures no one has modified the encrypted file.

## Symmetric Encryption Algorithms

KeePass supports three symmetric encryption algorithms for the outer cipher. The choice is stored in the [KDBX file header](/keepass/kdbx-format-guide/), so compatible applications know which algorithm to use when decrypting.

### AES-256 (Rijndael)

AES-256 is the default encryption algorithm in KeePass and the most widely used symmetric cipher in the world. Selected by NIST in 2001 after a rigorous multi-year competition, AES has withstood over two decades of cryptanalysis by the world's leading researchers.

Key properties of AES-256 in the KeePass context:

- **Key size**: 256 bits, providing a theoretical security level of 2^256 possible keys. For context, if every atom in the observable universe were a computer performing a trillion key guesses per second, the age of the universe would not be enough time to try even a negligible fraction of the key space.
- **Block size**: 128 bits. Data is encrypted in 128-bit (16-byte) blocks.
- **Mode of operation**: KeePass uses AES in CBC (Cipher Block Chaining) mode, where each plaintext block is XORed with the previous ciphertext block before encryption. This ensures that identical plaintext blocks produce different ciphertext, preventing pattern analysis.
- **Initialization vector (IV)**: A random 128-bit IV is generated for each save operation and stored in the database header. The IV ensures that saving the same database twice produces different ciphertext.

AES-256 in CBC mode is a well-understood, battle-tested configuration. Hardware acceleration (AES-NI instructions) is available on virtually all modern CPUs, making encryption and decryption fast despite the strong security level.

### ChaCha20

ChaCha20 is a modern stream cipher designed by Daniel J. Bernstein. It became available as an alternative outer cipher in KDBX 4.0 and represents a fundamentally different approach to encryption than AES.

Where AES is a block cipher that processes data in fixed-size chunks, ChaCha20 generates a keystream that is XORed with the plaintext. Key advantages include:

- **No padding required**: Because it is a stream cipher, ChaCha20 does not need to pad data to a block boundary. This eliminates padding oracle attacks entirely -- a class of vulnerability that has historically affected block ciphers in CBC mode.
- **Constant-time operation**: ChaCha20 uses only add, rotate, and XOR operations (the ARX design). These operations execute in constant time on all hardware, making the algorithm inherently resistant to timing side-channel attacks. AES implementations that lack hardware acceleration can leak timing information through cache access patterns.
- **Software performance**: On systems without AES-NI hardware acceleration (some ARM processors, older CPUs, embedded devices), ChaCha20 often outperforms AES in pure software implementations.
- **Nonce-based**: ChaCha20 uses a 96-bit nonce (number used once) and a 256-bit key. KeePass generates a fresh random nonce for each save operation.

ChaCha20 is paired with Poly1305 for authentication in many protocols (the ChaCha20-Poly1305 AEAD construction used in TLS 1.3 and WireGuard). In KeePass, integrity verification is handled separately by HMAC-SHA-256.

For most users, ChaCha20 is an excellent choice, particularly if you use your database on devices that may lack AES hardware acceleration. Its security margin is considered at least as strong as AES-256.

### Twofish

Twofish was a finalist in the AES competition, designed by Bruce Schneier and a team of cryptographers. While it did not win the competition (Rijndael was selected as AES), Twofish remains a respected cipher with no known practical attacks.

Key characteristics:

- **Key size**: 256 bits
- **Block size**: 128 bits
- **Design philosophy**: Twofish uses a more conservative design with wider security margins than AES, at the cost of somewhat lower performance.
- **Availability**: Supported in KeePass 2.x and many compatible applications, though not universally supported across the ecosystem.

Twofish is a solid choice for users who want algorithm diversity -- using a different cipher than AES as a hedge against the (extremely unlikely) possibility that a practical attack against AES is discovered. However, [compatibility](/keepass/compatibility-guide/) should be checked when sharing databases across different applications, as not all KeePass-compatible apps support Twofish.

## Key Derivation: Turning Your Passphrase Into a Key

Your master passphrase might be a memorable sentence or a randomly generated string, but either way it is not suitable as a direct encryption key. Key derivation functions transform your passphrase into a fixed-length cryptographic key while adding deliberate computational cost that slows brute-force attacks.

KeePass supports two key derivation functions: Argon2d (the modern default) and AES-KDF (the legacy option).

### Argon2d

Argon2 won the Password Hashing Competition in 2015 and is widely considered the state of the art for password-based key derivation. KeePass uses the Argon2d variant specifically, which is optimized for resistance against GPU and ASIC-based cracking attacks.

Argon2d has three independently configurable parameters:

**Memory cost** -- The amount of RAM the function requires during computation. A typical setting is 64 MB. This is the parameter that makes Argon2d "memory-hard." GPUs have enormous computational throughput but relatively little memory per core. Requiring 64 MB of RAM per computation means a GPU with 8 GB of VRAM can only run about 125 parallel instances, rather than the thousands or millions of parallel computations it could perform with a memory-light algorithm.

**Iterations (time cost)** -- The number of passes the algorithm makes over the memory. More iterations mean more computation time. A setting of 3 iterations with 64 MB of memory might take 500 milliseconds on a modern laptop -- imperceptible when unlocking your vault, but devastating to an attacker who needs to try millions of candidate passphrases.

**Parallelism** -- The number of threads used during computation. This parameter controls how the algorithm can take advantage of multi-core processors during legitimate use while not providing a proportional advantage to attackers.

The interplay between these parameters is what makes Argon2d powerful. An attacker cannot trade memory for time or vice versa -- the algorithm is designed to require both simultaneously. This is a fundamental improvement over older KDFs that are only computationally hard, not memory-hard.

To understand why this matters for password security, see our explanation of [password entropy](/password-security/password-entropy/) and how key derivation amplifies the effective strength of your passphrase. The relationship between [password salting](/password-security/password-salt-explained/) and key derivation is also critical: the salt stored in the KDBX header ensures that the same passphrase produces different derived keys for different databases.

### AES-KDF (Legacy)

The older key derivation method in KeePass applies AES encryption iteratively to derive the key. The primary configurable parameter is the number of **transform rounds** -- how many times AES is applied.

A typical setting might be 60,000 rounds or more. Each round applies AES encryption to the intermediate key material, so more rounds mean more computation per passphrase guess. You can benchmark your hardware within KeePass to find a round count that produces an acceptable delay (usually targeting around one second).

AES-KDF has a significant limitation compared to Argon2d: it is not memory-hard. GPU-based attackers can run AES-KDF computations efficiently because AES acceleration is widely available in hardware and the algorithm requires negligible memory. This means that while AES-KDF with a high round count provides decent protection, it is fundamentally less resistant to hardware-accelerated attacks than Argon2d.

**Recommendation**: Use Argon2d for all new databases. AES-KDF exists primarily for backward compatibility with KDBX 3.1 databases and older applications that do not support KDBX 4.0.

### Choosing Key Derivation Parameters

The goal is to make each passphrase guess as expensive as possible for an attacker without making your own vault-opening experience unpleasant. Practical guidelines:

- **Target unlock time**: 0.5 to 2 seconds on your slowest device. If you open your vault on a phone, benchmark there, not on your desktop.
- **Memory for Argon2d**: Start at 64 MB. If your device has ample RAM, increase to 128 MB or 256 MB. Each doubling of memory roughly doubles the difficulty for memory-constrained attackers.
- **Iterations for Argon2d**: 2-4 iterations is typical. More iterations increase CPU cost linearly.
- **Parallelism for Argon2d**: Match the number of cores on your slowest device. Setting parallelism to 4 is a reasonable default.

Remember that these settings are stored in the database header and apply to anyone who opens the database. If you share your vault across devices, the parameters must be practical for the least powerful device.

## Inner Random Stream Protection

Beyond the outer encryption that protects the entire database, KeePass adds a second encryption layer for individual sensitive fields -- passwords, TOTP secrets, and any field marked as "protected" in the database schema.

This inner stream encryption serves a specific purpose: protecting sensitive data during database processing. When the database is decrypted and loaded into memory, all the metadata (titles, URLs, notes) exists in plaintext in RAM. Protected fields, however, remain encrypted with the inner random stream cipher and are only decrypted on demand -- for example, when you copy a password to the clipboard or autofill a login form.

### ChaCha20 Inner Stream (KDBX 4.x)

In KDBX 4.0 and later, the inner random stream uses ChaCha20. A 256-bit key for the inner stream is derived from the database's master seed, independent of the outer encryption key. This means that even if an attacker could somehow observe the decrypted database in memory, protected fields would still appear as encrypted bytes until individually accessed.

### Salsa20 Inner Stream (KDBX 3.x)

Older KDBX 3.1 databases use Salsa20, another stream cipher by Daniel Bernstein and the predecessor to ChaCha20. Salsa20 remains secure, but ChaCha20 offers improved diffusion per round and is the recommended choice for new databases.

### Why Inner Stream Protection Matters

Consider a scenario where malware is monitoring a process's memory. Without inner stream protection, once the vault is unlocked, every password sits in plaintext in RAM. With inner stream protection, the malware would need to identify and intercept the specific moment a password is decrypted for use. This significantly raises the bar for memory-scraping attacks.

This layered approach is characteristic of the defense-in-depth philosophy in [database encryption](/keepass/database-encryption/) and is one reason the KeePass format is considered the [gold standard](/keepass/gold-standard/) for offline password management.

## Integrity Verification

Encryption alone does not protect against tampering. An attacker who cannot decrypt your database might still modify the encrypted bytes to corrupt it or, worse, manipulate it in predictable ways. KeePass addresses this with HMAC-SHA-256 authentication.

### How HMAC-SHA-256 Works in KDBX 4.x

KDBX 4.0 divides the encrypted payload into blocks. Each block has an associated HMAC-SHA-256 tag computed from:

- The block's ciphertext
- The block index
- A key derived from the master key

When the database is opened, KeePass verifies the HMAC tag for each block before decryption. If any block has been modified -- even a single bit -- the HMAC check fails and the database refuses to open. This prevents both accidental corruption and deliberate tampering.

### Header Authentication

The KDBX 4.0 format also authenticates the database header itself. Because the header contains critical parameters (which cipher to use, which KDF, the KDF parameters, the initialization vector), tampering with the header could be used to weaken the encryption. Header authentication ensures that an attacker cannot, for example, downgrade the KDF parameters to make brute-forcing easier.

This is a significant improvement over KDBX 3.1, where the header was protected only by a SHA-256 hash rather than a keyed HMAC. The unkeyed hash could verify accidental corruption but provided weaker protection against deliberate modification by a sophisticated attacker.

## Putting It All Together: The Full Encryption Flow

Here is the complete sequence when you save a KeePass database with KDBX 4.0 defaults:

1. **Composite key assembly**: Your master passphrase is hashed with SHA-256. If a key file is used, its content is hashed and combined. The result is the composite key.

2. **Key derivation**: The composite key is fed into Argon2d along with a random salt (stored in the header). Argon2d processes the key using the configured memory, iteration, and parallelism parameters, producing a 256-bit derived key.

3. **Master seed mixing**: The derived key is combined with a random master seed (also stored in the header) and hashed again to produce the final encryption key and the HMAC key.

4. **Inner stream key generation**: A separate key for the ChaCha20 inner random stream is derived from the master seed.

5. **Protected field encryption**: All fields marked as protected are encrypted with ChaCha20 using the inner stream key.

6. **Payload compression**: The XML database payload (with protected fields already encrypted) is optionally compressed with GZip.

7. **Outer encryption**: The compressed payload is encrypted with the chosen algorithm (AES-256-CBC, ChaCha20, or Twofish) using the final encryption key.

8. **Block HMAC computation**: HMAC-SHA-256 tags are computed for each encrypted block.

9. **Header writing and authentication**: The complete header is written, followed by an HMAC-SHA-256 tag authenticating the header.

10. **File output**: The header, header HMAC, encrypted blocks, and block HMACs are written to the .kdbx file.

Decryption reverses this process: verify header HMAC, derive keys, verify block HMACs, decrypt outer cipher, decompress, and finally decrypt inner stream fields on demand.

## How This Compares to Cloud Password Managers

Cloud-based password managers like 1Password, Bitwarden, and Dashlane also use strong encryption -- typically AES-256 with PBKDF2 or Argon2. The fundamental difference is not the algorithms but the trust model.

With a cloud manager, your encrypted vault is stored on someone else's servers. Even with [zero-knowledge encryption](/password-managers/zero-knowledge-encryption/), you are trusting that the client software correctly implements the cryptography and does not leak your key. You are trusting that the server infrastructure is secure. You are trusting that no future software update will weaken the encryption.

With KeePass, the encrypted database file is a local file under your control. The format is an open standard, and multiple independent implementations exist -- from KeePassXC on the desktop to mobile apps like KeePassDX, Strongbox, and [PanicVault](https://panicvault.com) on Apple platforms. You can verify the encryption yourself, choose your own storage location, and control exactly which devices have access. This transparency is a core part of why [open standards matter for password security](/keepass/open-source-security/).

## Practical Security Implications

Understanding the encryption architecture leads to concrete decisions:

**Choose ChaCha20 or AES-256 as your outer cipher.** Both are excellent. ChaCha20 is marginally better on devices without AES-NI, and its stream cipher design eliminates padding-related attack surfaces. AES-256 is the default and has the broadest compatibility.

**Use Argon2d for key derivation.** There is no compelling reason to use AES-KDF for new databases. Argon2d's memory-hardness provides a qualitative advantage against GPU-based attacks that AES-KDF cannot match.

**Set aggressive but practical KDF parameters.** Every doubling of memory cost or iteration count doubles the work for an attacker. Benchmark on your slowest device and set parameters as high as you can tolerate.

**Pair strong encryption with a strong passphrase.** The encryption is only as strong as the key, and the key is derived from your passphrase. A weak passphrase with perfect encryption is still vulnerable. Aim for a passphrase with at least 60-80 bits of [entropy](/password-security/password-entropy/).

**Keep your database format current.** KDBX 4.0 offers meaningful security improvements over KDBX 3.1, including Argon2d support, ChaCha20 inner stream, and header HMAC authentication. Check the [compatibility guide](/keepass/compatibility-guide/) to ensure your applications support it, then upgrade.

The KeePass encryption architecture is not security by obscurity. Every algorithm is a published standard. Every parameter is configurable. Every implementation can be audited. That transparency is the foundation of trust -- and it is why the format has remained a trusted choice for security-conscious users for over two decades.
