---
title: "KDBX File Format Compatibility Guide"
description: "Complete guide to KDBX 3.1 vs 4.0 compatibility across KeePass apps, covering encryption, KDF support, and feature differences."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

One of the greatest strengths of the [KeePass ecosystem](/keepass/) is that your password database is not locked to a single application. The KDBX file format is an open standard, and dozens of applications across every major platform can read and write it. But not every application supports every feature -- and when you open a database in an app that does not fully support its format version, you can encounter anything from missing features to outright failure to decrypt.

This guide covers everything you need to know about KDBX compatibility: what changed between format versions, which applications support which features, and how to avoid problems when using your database across multiple devices and platforms.

## KDBX Format Versions: 3.1 vs 4.0

The KDBX format has evolved through several versions. The two you will encounter in practice are KDBX 3.1 and KDBX 4.0 (sometimes referred to as KDBX 4.x to include minor revisions). Understanding their differences is essential for making compatibility decisions.

### KDBX 3.1: The Established Standard

KDBX 3.1 has been the workhorse of the KeePass ecosystem for years. Its features are well-understood, and support is essentially universal across compatible applications.

Key characteristics:

- **Outer encryption**: AES-256 in CBC mode (Twofish also supported in KeePass 2.x)
- **Key derivation**: AES-KDF with configurable transform rounds
- **Inner random stream**: Salsa20 for protecting individual password fields in memory
- **Header integrity**: SHA-256 hash of the header (unkeyed)
- **Payload structure**: The entire database is encrypted as a single stream after an optional GZip compression step
- **XML format**: Database contents are stored as XML with Base64-encoded protected fields

KDBX 3.1 is the safe choice when maximum compatibility is the priority. Every KeePass-compatible application in active development supports it.

### KDBX 4.0: The Modern Standard

KDBX 4.0 introduced significant improvements to the security architecture. If you are starting fresh or can ensure all your applications support it, 4.0 is the better choice.

Key improvements over 3.1:

- **Argon2d key derivation**: Memory-hard KDF that is dramatically more resistant to GPU and ASIC attacks than AES-KDF. This is the single most important security improvement. See our detailed explanation of [KeePass encryption](/keepass/encryption-explained/) for why memory-hardness matters.
- **ChaCha20 outer cipher**: A modern stream cipher alternative to AES-256, offering resistance to padding oracle attacks and constant-time execution without hardware acceleration.
- **ChaCha20 inner random stream**: Replaces Salsa20 for inner field protection, with improved per-round diffusion.
- **HMAC-SHA-256 header authentication**: The header is now authenticated with a keyed HMAC rather than an unkeyed hash. This prevents an attacker from tampering with header parameters (such as downgrading KDF settings) without detection.
- **Block-level HMAC**: The encrypted payload is divided into blocks, each individually authenticated. This allows detection of partial file corruption or tampering.
- **Header field extensibility**: The format supports custom header fields, allowing future additions without breaking backward compatibility.

### What Actually Changed in the Header

The differences between 3.1 and 4.0 are concentrated in three areas:

**Key derivation parameters**: In 3.1, the header contains a transform seed and a round count for AES-KDF. In 4.0, the header contains a serialized dictionary of KDF parameters that can represent either AES-KDF (for backward compatibility) or Argon2d (with memory, iterations, parallelism, and salt).

**Integrity protection**: In 3.1, the header ends with a StreamStartBytes field -- a random 32-byte value stored in plaintext that is also stored encrypted at the beginning of the payload. After decryption, the application checks that the decrypted start bytes match the header value to verify the key is correct. In 4.0, this mechanism is replaced by HMAC-SHA-256 authentication of both the header and each payload block.

**Inner header**: KDBX 4.0 introduces an inner header that is encrypted along with the payload. This inner header contains the inner random stream ID and key, which in 3.1 were stored in the outer (unencrypted) header. Moving these to the inner header means they are protected by the outer encryption, adding another layer of security.

## Application Compatibility Matrix

The following matrix covers the most widely used [KeePass-compatible applications](/keepass/compatible-apps/) and their format support. This information reflects the state of each application as of early 2026.

### Desktop Applications

| Application | Platform | KDBX 3.1 | KDBX 4.0 | AES-256 | ChaCha20 | Twofish | Argon2d | AES-KDF |
|---|---|---|---|---|---|---|---|---|
| KeePass 2.x | Windows | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| KeePassXC | Win/Mac/Linux | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| PanicVault | macOS | Yes | Yes | Yes | Yes | No | Yes | Yes |
| MacPass | macOS | Yes | Yes | Yes | Yes | No | Yes | Yes |
| KeePassDX | Android | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| KeeWeb | Web/Desktop | Yes | Yes | Yes | Yes | No | Yes | Yes |

### Mobile Applications

| Application | Platform | KDBX 3.1 | KDBX 4.0 | AES-256 | ChaCha20 | Twofish | Argon2d | AES-KDF |
|---|---|---|---|---|---|---|---|---|
| KeePassDX | Android | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| KeePass2Android | Android | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Strongbox | iOS | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| KeePassium | iOS | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| PanicVault | iOS/iPadOS | Yes | Yes | Yes | Yes | No | Yes | Yes |
| AuthPass | iOS/Android | Yes | Yes | Yes | Yes | No | Yes | Yes |

### Key Observations

**KDBX 4.0 support is now widespread.** The major applications across all platforms support 4.0. The days when 3.1 was necessary for compatibility are largely over, though you should verify your specific combination of tools.

**Twofish support varies.** If you use Twofish as your outer cipher, some applications (notably KeeWeb, MacPass, and AuthPass) will not be able to open your database. AES-256 and ChaCha20 have the broadest support.

**Argon2d is broadly supported in 4.0-capable apps.** Any application that supports KDBX 4.0 also supports Argon2d, since it is the primary new KDF in that format version.

## Encryption Algorithm Support in Detail

### AES-256: Universal Compatibility

AES-256 is supported by every KeePass-compatible application without exception. If you need to share a database across the widest possible range of tools, AES-256 is the safe choice.

In KDBX 3.1, AES-256-CBC is the only standard outer cipher (though KeePass 2.x adds Twofish via its plugin-like architecture). In KDBX 4.0, AES-256-CBC remains available alongside ChaCha20.

### ChaCha20: Modern and Well-Supported

ChaCha20 is available only in KDBX 4.0 databases. Among applications that support KDBX 4.0, ChaCha20 support is universal -- the algorithm is part of the 4.0 specification, so any compliant implementation must support it.

ChaCha20 is a particularly good choice for users who access their database on mobile devices or lower-power hardware, where AES hardware acceleration may be absent or less effective.

### Twofish: Check Before Using

Twofish support is the most variable. While KeePass 2.x, KeePassXC, and the major mobile apps support it, several web-based and lighter-weight applications do not. If you want to use Twofish, verify that every application in your workflow supports it before converting your database.

## Feature Compatibility Beyond Encryption

Format version affects more than just cryptographic algorithms. Several database features are tied to the KDBX version.

### Entry History

Both KDBX 3.1 and 4.0 support entry history -- maintaining previous versions of entries so you can recover an old password. The implementation is compatible across versions, and applications generally handle history entries correctly regardless of format version.

### Custom Fields and Icons

Custom entry fields and custom icons are supported in both format versions. However, the encoding and storage details differ slightly between 3.1 and 4.0, which can occasionally cause display issues when an application reads a database written by a different application in a different format version.

### File Attachments (Binaries)

Both versions support file attachments, but KDBX 4.0 stores them more efficiently. In 3.1, binaries are stored inline in the XML with Base64 encoding. In 4.0, they are stored in a more structured inner header format. This difference is handled transparently by well-implemented applications, but poorly maintained tools may struggle with large attachments in one format or the other.

### Groups and Tags

Group structures (folders for organizing entries) work identically across versions. Tags were introduced later and are supported in both 3.1 and 4.0, though some older applications may not display them.

### TOTP and OTP Support

One-time password (TOTP/HOTP) storage is not part of the KDBX specification itself -- it is handled through custom fields or entry string conventions. Compatibility depends on the application, not the format version. KeePassXC, KeePassDX, and Strongbox all support TOTP through their own conventions, but the exact field names and formats may differ. When sharing a database across applications, verify that TOTP entries work correctly in each.

## Practical Compatibility Scenarios

### Scenario 1: Desktop and Phone Sync

You use KeePassXC on your laptop and KeePassDX on your Android phone, syncing the database through a cloud storage provider.

**Recommended configuration**: KDBX 4.0 with ChaCha20 and Argon2d. Both applications fully support this combination. ChaCha20 will perform well on your phone, and Argon2d provides the strongest available protection against brute-force attacks. Set memory parameters with your phone's capability in mind -- 64 MB is a safe starting point that most modern phones handle comfortably.

### Scenario 2: Shared Family Database

Your family members use different applications: KeePassXC on desktop, Strongbox on iPhone, KeePass2Android on Android.

**Recommended configuration**: KDBX 4.0 with AES-256 and Argon2d. All three applications support this combination. AES-256 offers the most predictable behavior across implementations. Set Argon2d parameters conservatively since you need to accommodate the least powerful device in the family.

### Scenario 3: Maximum Compatibility Needed

You need to occasionally open your database in KeeWeb or another browser-based tool, and you also use it on desktop and mobile.

**Recommended configuration**: KDBX 4.0 with AES-256 and Argon2d. KeeWeb supports KDBX 4.0, AES-256, and Argon2d. Avoid Twofish in this scenario.

### Scenario 4: Legacy Application Required

You must use an older application that only supports KDBX 3.1.

**Recommended configuration**: KDBX 3.1 with AES-256 and AES-KDF. Set the AES-KDF transform rounds as high as your slowest device can tolerate (aim for a 1-second unlock time). Consider migrating to a modern application and KDBX 4.0 when possible, since the security improvements -- especially Argon2d -- are substantial.

## What to Check When Sharing Databases

When you share a KDBX database file with others or use it across multiple applications, run through this checklist:

1. **Verify format version support.** Open the database in every application before committing to a format. A silent failure to open is better than data corruption from a partial read.

2. **Confirm cipher support.** Check that your chosen outer cipher (AES-256, ChaCha20, or Twofish) is supported by all target applications.

3. **Test KDF compatibility.** Open and close the database in each application to verify that key derivation works correctly. Pay attention to unlock time -- if one application is dramatically slower than another with the same parameters, there may be an implementation difference worth investigating.

4. **Check feature fidelity.** After opening the database in a secondary application, verify that entries, custom fields, attachments, groups, and TOTP codes are all intact and functional.

5. **Watch for format migration prompts.** Some applications may offer to upgrade a KDBX 3.1 database to 4.0 when saving. If you need to maintain 3.1 compatibility, decline this offer or verify that it does not happen automatically.

6. **Test conflict resolution.** If you sync the database via cloud storage and edit on multiple devices, understand how each application handles file conflicts. Most KeePass applications do not merge changes -- the most recent save wins, and the other version is lost unless your sync tool preserves conflict copies.

## Migrating Between Format Versions

### Upgrading from KDBX 3.1 to 4.0

Most modern applications make this straightforward:

1. **In KeePassXC**: Go to Database > Database Settings > Security. Under Encryption, change the KDF to Argon2d and optionally change the cipher to ChaCha20. Save the database, and it will be written in KDBX 4.0 format.

2. **In KeePass 2.x**: Go to File > Database Settings > Security tab. Change the KDF to Argon2d. Save the database.

3. **Before migrating**: Ensure all applications you use support KDBX 4.0. Create a backup of your 3.1 database before converting.

### Downgrading from KDBX 4.0 to 3.1

Downgrading is sometimes necessary for compatibility:

1. Change the KDF back to AES-KDF.
2. Change the outer cipher to AES-256 (if using ChaCha20).
3. Save the database.

Note that downgrading loses the security benefits of Argon2d, ChaCha20 inner stream, and HMAC header authentication. Only downgrade if you have a genuine compatibility requirement.

## Understanding the KDBX File Structure

For readers interested in the technical details of the format, the [KDBX format guide](/keepass/kdbx-format-guide/) provides a byte-level walkthrough. Understanding the structure helps when troubleshooting compatibility issues, as most problems trace back to specific header fields or format-version-dependent features.

The [data portability](/keepass/data-portability/) implications of using an open format are significant. Because the KDBX specification is documented and multiple independent implementations exist, your passwords are never trapped in a proprietary silo. If your current application is abandoned or changes direction, you can switch to another compatible application without losing anything.

This stands in stark contrast to proprietary password managers, where your data's accessibility depends entirely on the continued operation and goodwill of a single company. For a broader perspective on [what password managers do](/password-managers/what-is-a-password-manager/) and why format openness matters, our password manager overview covers the landscape.

## Staying Compatible Going Forward

The KDBX format continues to evolve, but the KeePass community prioritizes backward compatibility. Future format revisions will likely add new capabilities (such as additional cipher options or KDF algorithms) while maintaining the ability to read older databases.

To keep your setup running smoothly:

- **Update your applications regularly.** Format support is added through software updates. Running the latest stable version of your KeePass-compatible apps ensures you have the broadest compatibility.
- **Standardize on KDBX 4.0 with AES-256 or ChaCha20 and Argon2d.** This combination is supported by every major application and provides the strongest available security.
- **Keep a backup in the current format.** Before any format migration or application switch, back up your database. A backup takes seconds and prevents data loss.
- **Test after any application update.** Occasionally, updates change default settings or format handling. A quick open-and-verify after updating confirms everything still works.

The KeePass ecosystem's commitment to open standards and compatibility is one of its defining strengths. With a clear understanding of format versions and application support, you can confidently use your password database across any combination of devices and platforms without compromising security or losing access to your data.
