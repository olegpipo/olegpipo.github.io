---
title: "What Is the KeePass (.kdbx) Format? Complete Technical Guide"
description: "A deep technical guide to the KDBX file format covering header structure, encryption layers, compression, XML payload, and version differences."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

The KeePass database format -- commonly known by its `.kdbx` file extension -- is the open standard that underpins one of the most trusted password management ecosystems in the world. If you use any [KeePass-compatible application](/keepass/), you are trusting this format with your most sensitive credentials. Understanding how the format actually works, from the binary header bytes to the encrypted XML payload, gives you the knowledge to evaluate that trust for yourself.

This guide walks through the full anatomy of a KDBX file: how it is structured, how it protects your data, and how the format has evolved across its major versions.

## A Brief History of the KeePass File Format

The original KeePass application, created by Dominik Reichl in 2003, used a format with the `.kdb` extension (KDB 1.x). It was functional but limited: the database structure was flat, custom fields were not supported, and the encryption pipeline was simpler than what modern security standards demand.

In 2010, KeePass 2.x introduced the KDBX format. This was a ground-up redesign that brought hierarchical groups, an extensible XML data model, pluggable key derivation, and stronger encryption. KDBX has gone through several sub-versions, with the most significant transition being from KDBX 3.1 to KDBX 4.0 (released in 2017) and later KDBX 4.1. Each version refined the security model and added capabilities while maintaining backward compatibility where possible.

Today, virtually every KeePass-compatible application -- including KeePassXC, KeePassDX, Strongbox, KeeWeb, and PanicVault -- reads and writes the KDBX format. This interoperability is one of the core advantages of the [KeePass ecosystem](/keepass/compatible-apps/).

## High-Level File Structure

A KDBX file consists of three major sections, arranged sequentially in the binary file:

1. **Outer Header** -- Unencrypted metadata that tells the application how to decrypt the rest of the file
2. **Encrypted Payload** -- The actual database contents, encrypted with a key derived from your master credentials
3. **HMAC Blocks (KDBX 4.x)** -- Integrity verification data that ensures no byte has been tampered with

In KDBX 3.1, the structure is slightly different: the payload uses a stream of encrypted bytes with a stream start marker, and integrity is verified via a hash rather than HMAC blocks. KDBX 4.x moved to a more robust authenticated encryption scheme.

## The Outer Header in Detail

The outer header is the only part of a KDBX file that can be read without knowing the master key. It begins with a **signature** that identifies the file as a KeePass database:

```
Bytes 0-3:   0x03D9A29A  (KeePass signature 1)
Bytes 4-7:   0x67FB4BB5  (KeePass signature 2)
Bytes 8-9:   Minor version number
Bytes 10-11: Major version number
```

The dual signature allows applications to quickly identify a file as KDBX and determine whether they support its version. A KDBX 4.0 file has major version `0x0004` and minor version `0x0000`.

Following the signature, the header contains a series of **type-length-value (TLV) fields**. Each field has a one-byte type identifier, a length indicator, and the field data. The key header fields include:

### Cipher ID

A UUID identifying the encryption algorithm used for the payload. The two standard options are:

- **AES-256-CBC** (`31C1F2E6-BF71-4350-BE58-05216AFC5AFF`) -- The default in older databases
- **ChaCha20** (`D6038A2B-8B6F-4CB5-A524-339A31DBB59A`) -- Available in KDBX 3.1+ and the default in many modern implementations

ChaCha20 is a stream cipher that offers excellent performance on devices without hardware AES acceleration and provides authenticated encryption when paired with Poly1305. Both options deliver strong security, but ChaCha20 is increasingly preferred for new databases. For a deeper comparison of these ciphers, see our [KeePass encryption explained](/keepass/encryption-explained/) guide.

### Compression Flags

The payload can optionally be compressed with GZip before encryption. Compression reduces file size and, when applied before encryption, does not leak information about the plaintext structure because the compressed output is subsequently encrypted. Most KDBX files use GZip compression by default.

### Master Seed

A 32-byte random value generated each time the database is saved. The master seed is combined with the output of the key derivation function to produce the final encryption key. Because it changes on every save, even if you never change your master password, the actual encryption key differs between saves. This limits the amount of ciphertext an attacker can collect that was encrypted under the same key.

### Key Derivation Function Parameters

In KDBX 3.1, the key derivation function is always AES-KDF: the composite key is encrypted repeatedly under a random transform seed for a configurable number of rounds (typically 60,000 to 600,000). The transform seed and round count are stored in dedicated header fields.

KDBX 4.0 introduced a **KDF parameters** field that stores a VariantDictionary -- a flexible key-value structure that can describe any key derivation function. This is how KDBX 4.0 supports Argon2d and Argon2id alongside AES-KDF. The dictionary stores the algorithm UUID plus its specific parameters (memory cost, iteration count, parallelism, salt).

The move to Argon2 was significant. AES-KDF is CPU-bound and can be accelerated with GPUs and custom hardware. Argon2 is memory-hard, meaning it requires substantial RAM per computation, which dramatically increases the cost of parallel brute-force attacks. This is the same principle discussed in our guide on [password salting](/password-security/password-salt-explained/).

### Encryption IV

The initialization vector (or nonce, for ChaCha20) used with the cipher. This is randomly generated for each save and ensures that encrypting the same plaintext twice produces different ciphertext.

### Inner Random Stream ID and Key (KDBX 3.1)

In KDBX 3.1, certain sensitive fields within the XML payload (specifically, password values) are individually encrypted using an **inner random stream** -- either Salsa20 or ChaCha20. The inner stream ID and key are stored in the outer header. This provides a second layer of encryption: even after decrypting the main payload, password values remain encrypted under a separate key stream.

In KDBX 4.x, the inner random stream parameters moved inside the encrypted payload (into an "inner header"), so they are no longer exposed in the unencrypted outer header. This is a security improvement because it means an attacker cannot learn which inner stream cipher is used without first decrypting the outer layer.

### End of Header

A sentinel field marks the end of the header. Everything after this point is encrypted (or, in KDBX 4.x, is part of the HMAC-authenticated and encrypted data blocks).

## The Key Derivation Pipeline

Understanding how your master credentials become an encryption key is central to evaluating the format's security.

### Step 1: Composite Key

KeePass supports multiple credential types that are combined into a **composite key**:

- **Master password** -- Hashed with SHA-256
- **Key file** -- The raw bytes (or a hash of the file contents, depending on key file version)
- **Windows User Account** (KeePass on Windows only)

If multiple credential types are used, their individual hashes are concatenated and hashed again with SHA-256 to produce a single 32-byte composite key. This means a key file and password together are stronger than either alone.

### Step 2: Key Derivation

The composite key is passed through the configured KDF:

- **AES-KDF**: The composite key is encrypted under the transform seed for N rounds, then hashed with SHA-256
- **Argon2d/Argon2id**: The composite key is processed with the configured memory, iteration, and parallelism parameters plus a random salt

The output is a 32-byte derived key.

### Step 3: Final Key Generation

The derived key is concatenated with the master seed from the header and hashed with SHA-256 to produce the **final encryption key**. This key is used directly with AES-256 or ChaCha20 to decrypt the payload.

In KDBX 4.x, an additional HMAC key is derived by hashing the derived key concatenated with the master seed and the byte `0x01`. This HMAC key is used to verify the integrity of every data block.

## The Encrypted Payload

### KDBX 3.1 Payload Structure

In KDBX 3.1, the encrypted payload is a single contiguous block. After decryption:

1. The first 32 bytes are compared against a **stream start bytes** value from the header to verify correct decryption
2. The remaining data is organized as a series of **hashed blocks** -- each block contains its data plus a SHA-256 hash for integrity verification
3. After reassembling and optionally decompressing the blocks, you get the XML payload

### KDBX 4.x Payload Structure

KDBX 4.x replaced the hashed-block scheme with **HMAC-SHA-256 authenticated blocks**. Each block is individually authenticated with an HMAC derived from the block index and the HMAC key. This provides stronger integrity guarantees because HMAC is a cryptographic authentication code rather than a simple hash, and it prevents block reordering or substitution attacks.

After decryption and optional decompression, the payload begins with an **inner header** containing the inner random stream parameters, followed by the XML data.

## The XML Data Model

The core of every KDBX database is an XML document with a well-defined schema. The top-level structure looks like this:

```xml
<?xml version="1.0" encoding="utf-8"?>
<KeePassFile>
    <Meta>
        <Generator>KeePassXC</Generator>
        <DatabaseName>My Passwords</DatabaseName>
        <DefaultUserName/>
        <MemoryProtection>
            <ProtectPassword>True</ProtectPassword>
            <ProtectURL>False</ProtectURL>
        </MemoryProtection>
        <CustomIcons>...</CustomIcons>
        <CustomData>...</CustomData>
    </Meta>
    <Root>
        <Group>
            <Name>Root</Name>
            <UUID>...</UUID>
            <Group>
                <Name>Internet</Name>
                <Entry>
                    <UUID>...</UUID>
                    <String>
                        <Key>Title</Key>
                        <Value>Example Login</Value>
                    </String>
                    <String>
                        <Key>Password</Key>
                        <Value Protected="True">...</Value>
                    </String>
                    ...
                </Entry>
            </Group>
        </Group>
    </Root>
</KeePassFile>
```

### Groups and Entries

The database is a tree of **Groups**, each of which can contain sub-groups and **Entries**. An entry represents a single credential and holds its data as key-value **String** pairs. Standard keys include Title, UserName, Password, URL, and Notes, but applications can add arbitrary custom string fields -- a feature that makes the format flexible enough to store SSH keys, API tokens, TOTP seeds, and any other structured secret.

### Protected Values

Fields marked with `Protected="True"` have their values encrypted with the inner random stream cipher. When the XML is in memory, these values appear as Base64-encoded ciphertext. They are only decrypted on demand when the user requests them. This minimizes the time sensitive data spends in plaintext in process memory.

### Custom Data

Both the `Meta` section and individual entries support a `CustomData` element -- a key-value store for application-specific metadata. This allows KeePass-compatible apps to store settings, sync state, or plugin data without breaking compatibility with other applications that simply ignore keys they do not recognize.

### Attachments

Binary attachments (files stored within entries) are handled differently across versions. In KDBX 3.1, binaries are stored in a `Binaries` pool in the `Meta` section, referenced by index from entries. In KDBX 4.x, binaries are stored in the inner header as dedicated binary records, which means they benefit from the same HMAC integrity protection as the rest of the payload.

## KDBX 3.1 vs. KDBX 4.x: Key Differences

| Feature | KDBX 3.1 | KDBX 4.0 / 4.1 |
|---|---|---|
| Key derivation | AES-KDF only | AES-KDF, Argon2d, Argon2id |
| Payload integrity | SHA-256 hashed blocks | HMAC-SHA-256 authenticated blocks |
| Inner stream parameters | In outer header (unencrypted) | In inner header (encrypted) |
| Binary attachments | In XML Meta section | In inner header |
| Header integrity | SHA-256 hash appended after header | HMAC-SHA-256 of header |
| Custom KDF support | No | Yes (VariantDictionary) |

The move from KDBX 3.1 to 4.x was driven by genuine security improvements. HMAC authentication prevents tampering that simple hash verification cannot detect. Moving the inner stream parameters inside the encrypted payload reduces information leakage. And Argon2 support makes brute-force attacks orders of magnitude more expensive.

Most modern applications default to KDBX 4.x when creating new databases. If you are working with an older database in KDBX 3.1 format, consider migrating to 4.x for the improved security properties. Our [compatibility guide](/keepass/compatibility-guide/) covers which applications support which versions.

## Security Properties of the Format

The KDBX format provides several layers of defense in depth:

**Confidentiality.** The entire payload is encrypted with AES-256 or ChaCha20. Without the correct master credentials, the data is computationally indistinguishable from random bytes.

**Integrity.** In KDBX 4.x, every data block is individually authenticated with HMAC-SHA-256. Any modification -- even a single flipped bit -- is detected before the data is used.

**Key derivation resistance.** Argon2 with appropriate parameters (e.g., 64 MB memory, 3 iterations) ensures that brute-forcing the master password requires enormous per-guess resources, as explored in our discussion of [zero-knowledge encryption](/password-managers/zero-knowledge-encryption/).

**Forward secrecy of encryption keys.** The master seed changes on every save, so even if a previous encryption key were somehow compromised, it would not decrypt future versions of the database.

**Memory protection.** The inner random stream encrypts sensitive values within the XML, reducing the window during which passwords exist in plaintext in process memory.

## Data Portability and the Open Standard

One of the most important properties of the KDBX format is that it is **fully documented and open**. The source code of KeePass serves as the reference implementation, and the format specification has been independently implemented by dozens of applications across every major platform.

This openness means your data is never locked into a single vendor's ecosystem. You can create a database in KeePassXC on Linux, open it in Strongbox on iOS, edit it in KeePassDX on Android, and manage it through PanicVault on the web -- all without any conversion or data loss. This level of [data portability](/keepass/data-portability/) is unmatched by proprietary password managers, which typically use closed formats that only their own applications can read.

The format's openness also means its security is publicly auditable. Any researcher can examine exactly how encryption is applied, how keys are derived, and where potential weaknesses might exist. Cryptographic formats that rely on secrecy for their security -- so-called "security through obscurity" -- have a long history of catastrophic failures. The KDBX format takes the opposite approach: its security rests entirely on the strength of its cryptographic primitives and the correctness of their application, both of which are open to scrutiny.

## Practical Implications for Users

You do not need to understand every byte of the KDBX header to use a KeePass-compatible application safely. But knowing the format's architecture helps you make informed decisions:

- **Choose KDBX 4.x with Argon2** when creating a new database. The security improvements over KDBX 3.1 are substantial.
- **Use a strong master passphrase.** The format's encryption is only as strong as the key protecting it. Argon2 makes brute force expensive, but a weak password is still a weak password.
- **Keep backups.** Because the KDBX file is a single encrypted blob, corruption of even a few bytes can make the entire database unreadable. Regular backups to independent storage locations protect against hardware failure and accidental deletion.
- **Verify application compatibility.** Not every application supports every KDBX feature. If you use custom fields, attachments, or Argon2id, confirm that all your applications handle them correctly. Our [compatibility guide](/keepass/compatibility-guide/) provides a detailed matrix.

The KDBX format has earned its position as the most widely supported open password database standard through two decades of careful engineering, community scrutiny, and iterative improvement. It is a format designed by people who understand that the security of your passwords depends on getting every cryptographic detail right -- and who made sure anyone could verify that they did.
