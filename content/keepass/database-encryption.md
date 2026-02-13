---
title: "Understanding Password Database Encryption: A Deep Dive"
description: "Deep dive into how password databases encrypt your data, covering AES-256, key derivation, salting, Argon2, and protection against GPU attacks."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

When you store passwords in a manager like [KeePass](/keepass/), you are trusting that the encryption protecting your vault is genuinely unbreakable. That trust should not be blind. Understanding how password database encryption works -- from the moment you type your master passphrase to the point where your data becomes indistinguishable from random noise -- lets you evaluate whether that trust is justified. This guide walks through every layer of the encryption pipeline used in modern password databases, with a focus on the KDBX format that underpins the KeePass ecosystem.

## How Password Databases Store Data

A password database is, at its most basic level, a structured file containing your credentials, notes, URLs, and metadata. Before encryption, this data exists as organized records: username fields, password fields, group hierarchies, timestamps, and attachments.

The encryption process transforms this structured, readable data into ciphertext that is computationally indistinguishable from random bytes. Without the correct decryption key, no amount of analysis can recover the original content. The file could contain your bank credentials or a stream of random numbers -- an attacker cannot tell the difference.

The KDBX format stores everything in a single file with two main sections:

- **The header** -- Contains metadata needed for decryption: the encryption algorithm identifier, the key derivation function parameters, the master seed, the encryption IV (initialization vector), and integrity check values. The header is not encrypted but is authenticated, meaning any tampering is detectable.
- **The payload** -- Contains the actual password entries, groups, and attachments. This section is fully encrypted.

This design means an attacker who obtains your vault file knows which algorithms were used and what parameters were chosen. That information is intentionally public. Security depends entirely on the strength of your master passphrase and the mathematical properties of the cryptographic primitives -- a principle known as Kerckhoffs' principle.

## Symmetric vs. Asymmetric Encryption

Encryption algorithms fall into two broad categories, and password databases use one of them almost exclusively.

**Asymmetric encryption** (public-key cryptography) uses a pair of keys: a public key for encryption and a private key for decryption. This is what secures HTTPS connections, email encryption (PGP), and digital signatures. It is powerful for communication between parties who have not shared a secret in advance, but it is relatively slow and is not designed for encrypting large volumes of data at rest.

**Symmetric encryption** uses a single key for both encryption and decryption. It is fast, efficient, and well-suited to encrypting files. If you and the decryption process share the same key, symmetric encryption provides extremely strong protection.

Password databases use symmetric encryption because the use case is inherently symmetric: you encrypt the database with a key derived from your master passphrase, and you decrypt it with the same key. There is no second party involved, no need for key exchange, and no reason to pay the performance cost of asymmetric algorithms.

The two symmetric ciphers used in modern KDBX databases are **AES-256** and **ChaCha20**.

## AES-256: The Workhorse

AES (Advanced Encryption Standard) with a 256-bit key is the most widely deployed symmetric cipher in the world. Selected by NIST in 2001 after a multi-year international competition, AES has been subjected to more cryptanalytic scrutiny than perhaps any other cipher in history. No practical attack against properly implemented AES-256 has ever been demonstrated.

AES operates on fixed-size blocks of 16 bytes (128 bits). To encrypt data larger than 16 bytes -- which is virtually always the case -- you need a **block cipher mode of operation** that defines how successive blocks are processed.

## Block Cipher Modes

The choice of block cipher mode is a critical but often overlooked aspect of encryption security.

### ECB (Electronic Codebook) -- The Wrong Choice

ECB encrypts each 16-byte block independently. Identical plaintext blocks produce identical ciphertext blocks, which leaks information about patterns in the data. ECB is never used for password databases and is mentioned here only to explain why other modes exist.

### CBC (Cipher Block Chaining)

CBC was the default mode in earlier KDBX versions. Each plaintext block is XORed with the previous ciphertext block before encryption, creating a chain where every block depends on all preceding blocks. This eliminates the pattern leakage of ECB.

CBC requires an **initialization vector** (IV) -- a random value used for the first block (since there is no "previous ciphertext" to start the chain). The IV is stored in the database header and does not need to be secret; it must only be unique for each encryption operation.

CBC has a known weakness: it is vulnerable to **padding oracle attacks** if the implementation leaks information about whether decrypted padding is valid. In the context of a local file (rather than a network protocol), this is less of a concern, but it motivated the move to more modern modes.

### CTR (Counter Mode) with HMAC

Counter mode transforms AES into a stream cipher: it encrypts a counter value for each block and XORs the result with the plaintext. This eliminates padding entirely and supports parallel encryption. When combined with HMAC (Hash-based Message Authentication Code) for integrity verification, CTR provides both confidentiality and authenticity.

### ChaCha20-Poly1305

The KDBX 4.x format added support for **ChaCha20-Poly1305**, a modern authenticated encryption scheme. ChaCha20 is a stream cipher designed by Daniel Bernstein that operates differently from AES: instead of encrypting fixed-size blocks, it generates a keystream that is XORed with the plaintext. Poly1305 is a message authentication code that provides integrity and authenticity in a single pass.

ChaCha20-Poly1305 has several advantages over AES-CBC:

- **No padding** -- Stream ciphers do not require padding, eliminating an entire class of vulnerabilities
- **Built-in authentication** -- Integrity is verified as part of decryption, not as a separate step
- **Performance on devices without AES hardware** -- ChaCha20 is fast in pure software, while AES performance depends heavily on hardware acceleration (AES-NI instructions)

Both AES-256 and ChaCha20-Poly1305 are considered highly secure for password database encryption. The choice between them is a matter of preference and hardware characteristics, not a significant security difference.

## Key Derivation: From Passphrase to Encryption Key

Your master passphrase might be something like "correct horse battery staple" -- a human-readable string of variable length. The encryption algorithm needs a fixed-length, high-entropy key (256 bits for AES-256). The process of transforming a passphrase into a suitable encryption key is called **key derivation**, and it is arguably the most security-critical step in the entire pipeline.

A naive approach -- simply hashing the passphrase with SHA-256 to produce a 256-bit key -- would be catastrophically insecure. SHA-256 is fast by design: a modern GPU can compute billions of SHA-256 hashes per second. An attacker who obtains your vault file could try billions of passphrase guesses per second.

Key derivation functions solve this by making each guess deliberately expensive.

### The Role of Salt

Before key derivation begins, a [random salt](/password-security/password-salt-explained/) is generated and stored in the database header. The salt is combined with your passphrase as input to the KDF. This serves two purposes:

1. **Prevents precomputation** -- Without a salt, an attacker could build a lookup table mapping common passphrases to their derived keys. The salt makes every database unique, even if two users choose the same passphrase.
2. **Forces per-database attacks** -- Each database has a different salt, so an attacker cracking multiple databases gains no efficiency from having cracked one.

The KDBX format uses a 256-bit (32-byte) cryptographically random salt, providing an astronomically large space that makes precomputation impossible.

### Iteration Counts and Time Cost

All key derivation functions include a parameter that controls how many times the core operation is repeated. This is called the **iteration count** (in PBKDF2 and AES-KDF) or the **time cost** (in Argon2).

Higher iteration counts mean more computation per guess, which directly translates to slower cracking speed. The goal is to find a balance: slow enough that an attacker trying millions of guesses faces weeks or months of computation, but fast enough that you experience only a brief delay (typically 0.5 to 2 seconds) when opening your vault.

The older AES-KDF used in KDBX 3.x achieved this by running AES encryption in a loop for a configurable number of rounds. A typical setting was 6,000,000 iterations, producing roughly a one-second delay on consumer hardware.

### Memory-Hard Algorithms: Defeating GPU Attacks

Iteration count alone has a limitation: GPUs are extremely efficient at repetitive computation. A high-end GPU in 2026 has thousands of cores that can each compute hash iterations in parallel. Simply increasing iterations shifts the advantage toward attackers with GPU farms.

**Memory-hard algorithms** address this by requiring each derivation to consume a large amount of RAM. GPUs have limited memory per core -- typically a few kilobytes of fast local memory per thread, with global memory shared across thousands of threads. An algorithm that requires 64 MB of RAM per derivation limits each GPU core to sequential execution, neutralizing the parallelism advantage.

This is the key innovation of Argon2 and scrypt, and it is why KDBX 4.x defaults to Argon2 for key derivation.

## Argon2 in Detail

Argon2, winner of the 2015 Password Hashing Competition, is the state of the art for key derivation. The KDBX 4.x format uses **Argon2d**, optimized for resistance against GPU-based attacks.

Argon2 accepts three configurable parameters:

- **Time cost (t)** -- The number of iterations over the memory. Higher values increase computation time.
- **Memory cost (m)** -- The amount of RAM required, in kilobytes. This is the memory-hardness parameter.
- **Parallelism (p)** -- The number of independent threads used during derivation. This parameter primarily affects legitimate users' performance on multi-core hardware.

A typical KDBX 4.x configuration uses:

```
Time cost:    3 iterations
Memory cost:  65536 KB (64 MB)
Parallelism:  4 threads
```

### How Argon2 Uses Memory

Argon2 allocates a large block of memory and fills it with data derived from the passphrase and salt. It then makes multiple passes over this memory, mixing blocks in a pattern that depends on previous blocks. This creates a chain of dependencies that cannot be shortcut: you must have the full memory allocated to compute the final key.

An attacker attempting to use less memory faces a steep penalty: reducing memory by a factor of _k_ increases computation time by a factor of roughly _k squared_. This makes time-memory trade-offs impractical. You either allocate the full memory or you pay an enormous computational penalty.

### Protecting Against GPU and ASIC Attacks

The memory hardness of Argon2 provides strong protection against GPU attacks because:

1. **Memory bandwidth is the bottleneck** -- GPUs have high computational throughput but limited memory bandwidth per core. Argon2's memory access pattern saturates this bandwidth, preventing cores from running at full speed.
2. **Memory allocation limits parallelism** -- A GPU with 24 GB of memory can run at most 375 parallel Argon2 instances at 64 MB each. Compare this to billions of parallel SHA-256 computations. The ratio of cracking speed to legitimate use speed collapses.
3. **Custom hardware (ASICs) face similar constraints** -- Building a custom chip for Argon2 requires large amounts of fast memory, which is expensive and difficult to scale.

Against a well-configured Argon2 setup with a passphrase that has reasonable [entropy](/password-security/password-entropy/), even a well-funded attacker faces months or years of computation to test a dictionary of common passphrases -- let alone an exhaustive brute-force search.

## Choosing KDF Parameters

The right KDF parameters depend on your hardware and your tolerance for unlock delay. Here are practical guidelines:

**Memory cost**: Use the highest value your least powerful device can handle comfortably. If you only access your vault on a modern laptop, 64 MB or even 256 MB is reasonable. If you also use a low-end Android phone, 32 MB may be the practical maximum. More memory means stronger protection against [GPU-based cracking](/password-security/password-cracking-explained/).

**Time cost**: Start with 3 iterations and adjust upward until the unlock time reaches 1-2 seconds on your slowest device. Going above 2 seconds per unlock is unnecessary for most threat models and will cause frustration.

**Parallelism**: Match this to the number of CPU cores on your primary device. 4 is a reasonable default. This parameter does not significantly affect security; it primarily determines how efficiently the derivation uses multi-core hardware.

### Testing and Benchmarking

KeePassXC and KeePass both provide benchmarking tools that measure how long key derivation takes on your hardware. Use them. Set parameters that produce roughly one second of delay, and re-evaluate when you upgrade hardware. The [KDBX format guide](/keepass/kdbx-format-guide/) includes specific configuration steps.

## The Complete Encryption Pipeline

Putting it all together, here is what happens when you save a KDBX 4.x database:

1. **Generate random values** -- The system generates a fresh random master seed (32 bytes) and encryption IV. A new HMAC key is also generated.

2. **Derive the composite key** -- Your master passphrase (and optionally a [key file](/keepass/key-files/)) is processed to create a composite key. If a key file is used, its contents are combined with the passphrase hash.

3. **Run Argon2** -- The composite key is processed through Argon2d with the stored salt and configured parameters (time, memory, parallelism). This produces the derived key.

4. **Derive final keys** -- The derived key is combined with the master seed using SHA-256 to produce the final encryption key and the HMAC key.

5. **Encrypt the payload** -- The database content (entries, groups, metadata) is serialized, compressed (optionally, using GZip), and encrypted using AES-256-CBC or ChaCha20-Poly1305 with the derived encryption key.

6. **Compute integrity HMAC** -- An HMAC-SHA-256 is computed over the encrypted payload and the header data, using the HMAC key. This ensures that any tampering with either the header or the encrypted content is detectable.

7. **Write the file** -- The header (algorithm identifiers, KDF parameters, salt, IV, HMAC) and the encrypted payload are written as a single KDBX file.

When you open the database, the process runs in reverse: read the header, derive the key from your passphrase and the stored salt, verify the HMAC, decrypt the payload, decompress, and present your credentials.

## Defense in Depth

The security of a KDBX database does not rest on any single mechanism. It is a layered defense:

- **Argon2 key derivation** makes brute-forcing the master passphrase computationally expensive and memory-intensive
- **Random salting** prevents precomputed attacks and ensures each database is unique
- **AES-256 or ChaCha20** encryption makes the payload unreadable without the derived key
- **HMAC integrity verification** detects any tampering with the encrypted file
- **Header authentication** in KDBX 4.x prevents attackers from modifying encryption parameters (e.g., downgrading the KDF to weaker settings)

Breaking any one layer does not compromise the others. An attacker would need to simultaneously defeat the key derivation (to get the key), the encryption (to read the data), and the integrity checks (to avoid detection). This layered approach, combined with the [open-source transparency](/keepass/open-source-security/) that allows independent verification of each layer, is what makes properly configured KDBX databases among the most secure credential storage formats available.

## Practical Implications

Understanding database encryption is not just academic. It informs practical decisions:

**Your master passphrase is the weakest link.** No amount of Argon2 tuning compensates for a weak passphrase. If your passphrase is a common phrase or a short string, the KDF slows the attacker down but does not stop them. Aim for at least 80 bits of entropy -- roughly a five-word random passphrase or a 14-character random string.

**KDF parameters should match your threat model.** If you are protecting personal accounts, default parameters are sufficient. If you face targeted attacks from well-resourced adversaries, increase memory cost to 256 MB or higher and accept a longer unlock time.

**Keep your software updated.** Encryption implementations are occasionally found to have bugs. The KeePass ecosystem's open-source nature means patches are transparent and verifiable, but they only protect you if you apply them.

**Backups inherit the encryption.** A copy of your KDBX file is exactly as secure as the original. Back up freely to cloud storage, USB drives, or remote servers. Without your master passphrase, the backup is useless to an attacker. This is the practical benefit of strong database encryption -- it liberates your backup strategy from security concerns.

The mathematics of modern encryption, properly implemented and parameterized, provide a level of security that is genuinely beyond the reach of any known attack. When you understand how your password database encryption works, you can use it with confidence rather than hope.
