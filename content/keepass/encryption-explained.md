---
title: "How KeePass Encryption Works: AES-256, Twofish, and ChaCha20"
description: "Deep dive into KeePass encryption algorithms, key derivation with Argon2d and AES-KDF, transform rounds, and inner random stream protection."
date: 2026-02-13
lastmod: 2026-09-02
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "What encryption does KeePass use?"
    a: "KeePass encrypts the whole .kdbx payload with a 256-bit symmetric cipher. KeePass 2.x ships AES-256 in CBC mode and ChaCha20 built in; Twofish, Serpent and GOST come from plugins, though some compatible apps such as KeePassXC implement Twofish natively. The master key is stretched first by a key derivation function -- AES-KDF or Argon2 -- and KDBX 4 files authenticate the header and every data block with HMAC-SHA-256."
  - q: "Is KeePass AES-256 encrypted?"
    a: "Yes. AES-256 (Rijndael) is the default database cipher in KeePass, used in CBC mode with a fresh random initialization vector on every save. But AES-256 is not what resists password guessing -- the key derivation function does that. A .kdbx file encrypted with AES-256 behind a weak master passphrase and low KDF settings is still a weak database."
  - q: "Should I use Argon2 or AES-KDF in KeePass?"
    a: "Use Argon2 unless you need to stay on KDBX 3.1, which only supports AES-KDF. Argon2 is memory-hard, so it forces an attacker to commit RAM to every guess and blunts GPU and ASIC cracking rigs; AES-KDF is CPU-only and hardware-accelerated almost everywhere. KeePass offers two Argon2 variants, Argon2d and Argon2id, and recommends Argon2d for database files on personal devices."
  - q: "ChaCha20 vs AES in KeePass: which should I pick?"
    a: "Either is safe. AES-256 has the broadest compatibility and is very fast wherever AES-NI hardware acceleration exists, which is nearly every modern CPU including Apple silicon. ChaCha20 is a stream cipher, so it needs no padding and runs in constant time even in pure software. One practical note: from KeePass 2.44 onward, choosing ChaCha20 forces the file to be saved as KDBX 4."
  - q: "Is KeePass encryption still secure in 2026?"
    a: "Yes. Nothing in the KDBX 4 stack has been broken: AES-256, ChaCha20, Argon2 and HMAC-SHA-256 all remain standard, heavily reviewed primitives, and the current KeePass 2.6x line -- 2.61 in March 2026 and 2.61.1 in May 2026 -- shipped no cryptographic changes. The realistic weak points are your master passphrase, KDF settings left too low, and the device you unlock the vault on."
---

The [KeePass ecosystem](/keepass/) has earned its reputation as one of the most trusted open-source password management platforms, and the encryption architecture is the reason why. Unlike cloud-based password managers that ask you to trust a company's infrastructure, KeePass puts the cryptography front and center -- every design decision is documented, every algorithm is a published standard, and every implementation can be independently verified. This article explains exactly how KeePass encrypts your password database, from the moment you type your master passphrase to the final encrypted bytes stored on disk.

Understanding the encryption pipeline matters even if you never plan to audit the source code yourself. Knowing what protects your data helps you make informed decisions about algorithm choices, key derivation settings, and how much trust to place in your vault's security.

> **Quick answer**: A .kdbx database is encrypted as a whole with a 256-bit cipher -- AES-256 in CBC mode by default, with ChaCha20 as the other option built into KeePass 2.x. Your passphrase never becomes the key directly: a key derivation function, AES-KDF or Argon2, stretches it first, and that is what makes guessing expensive. Pick AES-256 or ChaCha20 with Argon2, tuned so that unlocking takes about a second on your slowest device.

## The Encryption Pipeline Overview

When you save a KeePass database, several layers of cryptographic operations work together:

1. **Key composition** -- Your master passphrase (and optionally a [key file](/keepass/key-files/)) are combined into a composite key.
2. **Key derivation** -- The composite key is processed through a deliberately slow key derivation function (AES-KDF or Argon2) to produce a derived key.
3. **Outer encryption** -- The derived key encrypts the entire database payload using a symmetric cipher (AES-256, ChaCha20, or Twofish).
4. **Inner random stream** -- Individual protected fields within the database (like passwords) receive an additional layer of encryption using an inner random stream cipher.
5. **Integrity verification** -- In KDBX 4, HMAC-SHA-256 authenticates the header and every encrypted data block to detect tampering.

Each layer addresses a different threat. Key derivation slows brute-force attacks. Outer encryption protects the database at rest. Inner stream protection guards sensitive fields even during database processing. Integrity verification ensures no one has modified the encrypted file.

## Symmetric Encryption Algorithms

Three symmetric algorithms turn up as outer ciphers in the KeePass world, but they are not on equal footing. KeePass 2.x has exactly two built in -- AES-256 and ChaCha20 -- and reaches Twofish (along with Serpent and GOST) only through plugins, while several compatible applications such as KeePassXC implement Twofish natively. The choice is stored in the [KDBX file header](/keepass/kdbx-format-guide/), so compatible applications know which algorithm to use when decrypting. None of this changed in the current KeePass 2.6x release line: 2.61 (March 2026) and 2.61.1 (May 2026) were interface, integration and bug-fix releases rather than cryptographic ones.

### AES-256 (Rijndael)

AES-256 is the default encryption algorithm in KeePass and the most widely used symmetric cipher in the world. Rijndael won NIST's multi-year public competition in 2000 and was published as the AES standard (FIPS 197) in 2001, and it has withstood over two decades of cryptanalysis by the world's leading researchers.

Key properties of AES-256 in the KeePass context:

- **Key size**: 256 bits, providing a theoretical security level of 2^256 possible keys. For context, if every atom in the observable universe were a computer performing a trillion key guesses per second, the age of the universe would not be enough time to try even a negligible fraction of the key space.
- **Block size**: 128 bits. Data is encrypted in 128-bit (16-byte) blocks.
- **Mode of operation**: KeePass uses AES in CBC (Cipher Block Chaining) mode, where each plaintext block is XORed with the previous ciphertext block before encryption. This ensures that identical plaintext blocks produce different ciphertext, preventing pattern analysis.
- **Initialization vector (IV)**: A random 128-bit IV is generated for each save operation and stored in the database header. The IV ensures that saving the same database twice produces different ciphertext.

AES-256 in CBC mode is a well-understood, battle-tested configuration. Hardware acceleration (AES-NI instructions) is available on virtually all modern CPUs, making encryption and decryption fast despite the strong security level.

### ChaCha20

ChaCha20 is a modern stream cipher designed by Daniel J. Bernstein. KeePass 2.35 added it as an alternative outer cipher alongside the KDBX 4 format, and since KeePass 2.44 selecting ChaCha20 also forces the database to be saved as KDBX 4. It represents a fundamentally different approach to encryption than AES.

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
- **Availability**: Not built into KeePass 2.x. KeePass's own documentation lists Twofish -- with Serpent and GOST -- among the algorithms supplied by plugins; Twofish was a built-in option in KeePass 1.x for the older .kdb format. Several KDBX applications, KeePassXC among them, implement it natively.

Twofish appeals to users who want algorithm diversity -- a different cipher than AES as a hedge against the (extremely unlikely) possibility that a practical attack against AES is discovered. The trade-off is reach: [compatibility](/keepass/compatibility-guide/) has to be checked before you commit, because KeePass itself needs a plugin and not every KeePass-compatible app reads Twofish databases.

## Key Derivation: Turning Your Passphrase Into a Key

Your master passphrase might be a memorable sentence or a randomly generated string, but either way it is not suitable as a direct encryption key. Key derivation functions transform your passphrase into a fixed-length cryptographic key while adding deliberate computational cost that slows brute-force attacks.

KDBX supports two key derivation functions: AES-KDF, the original, and Argon2, added with KDBX 4. Argon2 is specified in three variants; KeePass offers two of them, Argon2d and Argon2id, and leaves out Argon2i as the least suitable for a database file.

### Argon2 (Argon2d and Argon2id)

Argon2 won the Password Hashing Competition in 2015 and is widely considered the state of the art for password-based key derivation. Argon2d gives the strongest resistance to GPU- and ASIC-based cracking, which is why KeePass recommends it for database files. Argon2id trades a little of that resistance for slightly better protection against certain side-channel attacks -- a sensible trade on a server, less relevant on a personal device where the database file simply sits on local storage.

Argon2 exposes three parameters you can configure in KeePass:

**Memory cost** -- The amount of RAM the function requires during computation. A typical setting is 64 MB. This is the parameter that makes Argon2d "memory-hard." GPUs have enormous computational throughput but relatively little memory per core. Requiring 64 MB of RAM per computation means a GPU with 8 GB of VRAM can only run about 125 parallel instances, rather than the thousands or millions of parallel computations it could perform with a memory-light algorithm.

**Iterations (time cost)** -- The number of passes the algorithm makes over the memory. More iterations mean more computation time. A setting of 3 iterations with 64 MB of memory might take 500 milliseconds on a modern laptop -- imperceptible when unlocking your vault, but devastating to an attacker who needs to try millions of candidate passphrases.

**Parallelism** -- The number of threads used during computation. This parameter controls how the algorithm can take advantage of multi-core processors during legitimate use while not providing a proportional advantage to attackers.

The interplay between these parameters is what makes Argon2d powerful. An attacker cannot trade memory for time or vice versa -- the algorithm is designed to require both simultaneously. This is a fundamental improvement over older KDFs that are only computationally hard, not memory-hard.

To understand why this matters for password security, see our explanation of [password entropy](/password-security/password-entropy/) and how key derivation amplifies the effective strength of your passphrase. The relationship between [password salting](/password-security/password-salt-explained/) and key derivation is also critical: the salt stored in the KDBX header ensures that the same passphrase produces different derived keys for different databases.

### AES-KDF (Legacy)

The older key derivation method in KeePass applies AES encryption iteratively to derive the key. The primary configurable parameter is the number of **transform rounds** -- how many times AES is applied.

A typical setting might be 60,000 rounds or more. Each round applies AES encryption to the intermediate key material, so more rounds mean more computation per passphrase guess. You can benchmark your hardware within KeePass to find a round count that produces an acceptable delay (usually targeting around one second).

AES-KDF has a significant limitation compared to Argon2d: it is not memory-hard. GPU-based attackers can run AES-KDF computations efficiently because AES acceleration is widely available in hardware and the algorithm requires negligible memory. This means that while AES-KDF with a high round count provides decent protection, it is fundamentally less resistant to hardware-accelerated attacks than Argon2d.

**Recommendation**: Use Argon2d for all new databases. AES-KDF exists primarily for backward compatibility: KDBX 3.1 supports no other KDF, so choosing anything but AES-KDF is itself what pushes a KeePass database into the KDBX 4 format.

### Choosing Key Derivation Parameters

The goal is to make each passphrase guess as expensive as possible for an attacker without making your own vault-opening experience unpleasant. Practical guidelines:

- **Target unlock time**: about one second on your slowest device. KeePass's own tuning procedure says to reduce the parameters if key transformation takes longer than you are willing to wait when opening the file. If you open your vault on a phone, benchmark there, not on your desktop.
- **Memory for Argon2**: KeePass's general advice is half the RAM of your smallest device, capped at 1 GB. On iOS and iPadOS, do not follow that: KeePass explicitly recommends 64 MB or less there, because an app that allocates a lot of RAM can stop AutoFill from working. Pair the lower memory with a higher iteration count.
- **Iterations for Argon2**: KeePass starts its procedure at 2 and raises the count when the transformation finishes too quickly. Iteration cost scales linearly with the count.
- **Parallelism for Argon2**: set it to the smallest number of logical processors among the devices that open the database.

Remember that these settings are stored in the database header and apply to anyone who opens the database. If you share your vault across devices, the parameters must be practical for the least powerful device.

## Inner Random Stream Protection

Beyond the outer encryption that protects the entire database, KeePass adds a second encryption layer for individual sensitive fields -- passwords, TOTP secrets, and any field marked as "protected" in the database schema.

This inner stream encryption serves a specific purpose: protecting sensitive data during database processing. When the database is decrypted and loaded into memory, all the metadata (titles, URLs, notes) exists in plaintext in RAM. Protected fields, however, remain encrypted with the inner random stream cipher and are only decrypted on demand -- for example, when you copy a password to the clipboard or autofill a login form.

### ChaCha20 Inner Stream (KDBX 4.x)

In KDBX 4.0 and later, the inner random stream uses ChaCha20, which supersedes Salsa20 as the default for this layer. The stream is keyed by a dedicated inner random stream key, generated at random and stored in the KDBX 4 *inner* header -- inside the encrypted payload, rather than in the plaintext outer header where KDBX 3.1 kept it. That key is independent of the outer encryption key, so even if an attacker could somehow observe the decrypted database in memory, protected fields would still appear as encrypted bytes until individually accessed.

### Salsa20 Inner Stream (KDBX 3.x)

KDBX 3.1 files written by KeePass use Salsa20, another stream cipher by Daniel Bernstein and the predecessor to ChaCha20, and they store the inner stream ID and key in the unencrypted outer header. Salsa20 remains unbroken, but ChaCha20 offers improved diffusion per round and is what KDBX 4 uses.

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

When the database is opened, KeePass verifies the HMAC tag for each block before decryption. If any block has been modified -- even a single bit -- the HMAC check fails and the database refuses to open. This prevents both accidental corruption and deliberate tampering. Because the tag covers the ciphertext rather than the plaintext, KDBX 4 is an encrypt-then-MAC scheme; KDBX 3.1 hashed each block's plaintext and encrypted the hash along with it, which is why only KDBX 4 can reject a tampered block without decrypting it first.

### Header Authentication

The KDBX 4.0 format also authenticates the database header itself. Because the header contains critical parameters (which cipher to use, which KDF, the KDF parameters, the initialization vector), tampering with the header could be used to weaken the encryption. Header authentication ensures that an attacker cannot, for example, downgrade the KDF parameters to make brute-forcing easier.

This is a meaningful improvement over KDBX 3.1, where the header was authenticated by a SHA-256 hash stored inside the encrypted part of the file -- so it could only be checked after decryption had already been attempted. A KDBX 4 file stores an unencrypted SHA-256 hash of the header, which lets any reader detect accidental corruption without the master key, followed by the HMAC-SHA-256 value that proves the header has not been altered by someone without it.

## Putting It All Together: The Full Encryption Flow

Here is the complete sequence when you save a KeePass database with KDBX 4.0 defaults:

1. **Composite key assembly**: Your master passphrase is hashed with SHA-256. If a key file is used, its content is hashed and combined. The result is the composite key.

2. **Key derivation**: The composite key is fed into Argon2d along with a random salt (stored in the header). Argon2d processes the key using the configured memory, iteration, and parallelism parameters, producing a 256-bit derived key.

3. **Master seed mixing**: The derived key is combined with a random master seed (also stored in the header) and hashed again to produce the final encryption key and the HMAC key.

4. **Inner stream key generation**: A separate random key for the ChaCha20 inner random stream is generated and written into the inner header, which sits inside the encrypted payload.

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

With KeePass, the encrypted database file is a local file under your control. The format is an open standard, and multiple independent implementations exist -- from KeePassXC on the desktop to mobile apps like KeePassDX, Strongbox, and [PanicVault](https://apps.apple.com/app/id6759188575) on Apple platforms. You can verify the encryption yourself, choose your own storage location, and control exactly which devices have access. This transparency is a core part of why [open standards matter for password security](/keepass/open-source-security/).

## Practical Security Implications

Understanding the encryption architecture leads to concrete decisions:

**Choose ChaCha20 or AES-256 as your outer cipher.** Both are excellent. ChaCha20 is marginally better on devices without AES-NI, and its stream cipher design eliminates padding-related attack surfaces. AES-256 is the default and has the broadest compatibility.

**Use Argon2d for key derivation.** There is no compelling reason to use AES-KDF for a new database unless you must stay on KDBX 3.1 for an application that cannot read KDBX 4. Argon2d's memory-hardness provides a qualitative advantage against GPU-based attacks that AES-KDF cannot match.

**Set aggressive but practical KDF parameters.** Every doubling of memory cost or iteration count doubles the work for an attacker. Benchmark on your slowest device and set parameters as high as you can tolerate.

**Pair strong encryption with a strong passphrase.** The encryption is only as strong as the key, and the key is derived from your passphrase. A weak passphrase with perfect encryption is still vulnerable. Aim for a passphrase with at least 60-80 bits of [entropy](/password-security/password-entropy/).

**Keep your database format current.** KDBX 4 offers meaningful security improvements over KDBX 3.1, including Argon2 support (Argon2d and Argon2id), the ChaCha20 inner stream moved into the encrypted inner header, encrypt-then-MAC block authentication, and header HMAC authentication. Check the [compatibility guide](/keepass/compatibility-guide/) to ensure your applications support it, then upgrade.

The KeePass encryption architecture is not security by obscurity. Every algorithm is a published standard. Every parameter is configurable. Every implementation can be audited. That transparency is the foundation of trust -- and it is why the format has remained a trusted choice for security-conscious users for over two decades.
