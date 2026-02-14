---
title: "KeePass vs. Proprietary Formats: Who Owns Your Data?"
description: "Compare open KeePass KDBX format against proprietary password manager formats on data portability, vendor lock-in, and long-term data ownership."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

Every password manager stores your credentials in some kind of database format. The question most people never think to ask is: **who controls that format?** When you entrust hundreds of passwords, secure notes, and authentication secrets to a tool, the format those secrets are stored in determines whether you truly own your data or merely rent access to it. The difference between the open [KeePass KDBX format](/keepass/) and the proprietary formats used by commercial password managers is not just a technical detail -- it is a question of ownership, autonomy, and long-term security.

This article examines what happens when you store your most sensitive data in a format controlled by a corporation versus an open standard maintained by a global community.

## What Makes a Format "Open" vs. "Proprietary"

An **open format** has a publicly documented specification that anyone can read, implement, and build upon. The KDBX format used by KeePass and its ecosystem of [compatible applications](/keepass/compatible-apps/) is open in this sense: the file structure, encryption scheme, key derivation process, and XML data model are fully described, and dozens of independent applications have implemented readers and writers. No single entity controls the format, and no permission is needed to create software that works with it.

A **proprietary format** is controlled by a single company. The specification may be partially documented, entirely undocumented, or intentionally obfuscated. Only the company's own software can fully read and write the format. Third-party access, if it exists at all, is limited to what the company chooses to expose through APIs or export functions.

Most commercial password managers use proprietary formats. 1Password, LastPass, Dashlane, and Bitwarden (despite being open-source on the client side) each store credentials in formats that are either fully proprietary or tightly coupled to their own infrastructure. When you use these tools, your data exists in a format that the company designed, the company controls, and the company can change at any time.

This distinction matters far more than most users realize.

## The Vendor Lock-In Problem

Vendor lock-in occurs when switching away from a product is made artificially difficult or costly. In password management, lock-in manifests in several ways:

### Export Limitations

Every commercial password manager offers some form of data export -- typically as a CSV or JSON file. On the surface, this seems adequate. But the reality is more complicated:

**CSV exports strip critical data.** A CSV file can contain usernames, passwords, and URLs, but it typically cannot represent custom fields, file attachments, TOTP secrets, secure notes with formatting, folder hierarchies, or entry-level metadata like creation dates and modification history. If you have spent years building a carefully organized vault with attachments and custom fields, a CSV export gives you back a fraction of your data.

**JSON exports are vendor-specific.** Some managers export to a proprietary JSON schema that only their own import tool can fully interpret. Fields may use internal identifiers that have no meaning outside the application. While a developer could write a conversion tool, non-technical users are stuck with whatever the official import/export path provides.

**Export features are sometimes deliberately limited.** Vendors have strong financial incentives to make leaving difficult. Some limit export to paid tiers. Some add friction to the export process (requiring desktop access when the user primarily uses mobile, for example). Some simply do not prioritize maintaining export quality because it serves the business goal of retention rather than acquisition.

**Exports create security risks.** The moment your passwords exist in a plaintext CSV file on your filesystem, they are vulnerable to any malware, backup process, or accidental sharing that touches that file. Users who export for migration may forget to securely delete the plaintext file afterward. The need to create an unencrypted export at all is a consequence of the proprietary format -- a problem that does not exist when your data is already in an open format like KDBX.

### The KDBX Difference

With a KDBX file, there is no export step needed to switch applications. Your database file is already in a format that every KeePass-compatible application can read natively. Switching from KeePassXC to Strongbox, or from KeePassDX to PanicVault, means pointing the new application at the same file. No conversion, no data loss, no plaintext intermediary. Every custom field, every attachment, every piece of metadata comes along intact.

This is [data portability](/keepass/data-portability/) in its truest form: your data moves freely because the format belongs to you, not to a vendor.

## What Happens When the Company Disappears

Software companies do not last forever. They get acquired, go bankrupt, pivot to different markets, or simply shut down. When a password manager company ceases operations, users face an urgent question: can I still access my data?

### Real-World Precedents

The history of digital services is littered with examples of sudden shutdowns. While major password managers have not (yet) vanished overnight, the pattern is well-established in related categories:

- **Acquisitions that kill products.** When a larger company acquires a smaller one, the acquired product is frequently discontinued. Users are given a migration window -- sometimes generous, sometimes not -- and then the old service goes dark. If the data format is proprietary and the migration window passes, access to historical data may be lost.

- **Pricing changes that force migration.** LastPass's 2021 decision to restrict its free tier forced millions of users to choose between paying or leaving. For those who left, the export process was the only way out -- and as discussed above, exports are lossy.

- **Infrastructure dependencies.** Some proprietary managers require authentication against the company's servers to decrypt the local vault. If those servers go offline, the vault becomes inaccessible even though the encrypted data is on the user's device. This is an architectural choice that prioritizes the company's control over the user's autonomy.

### How Open Formats Provide Insurance

A KDBX file has no infrastructure dependency. It is a self-contained encrypted file that can be decrypted with the correct master credentials and any compatible application. The cryptographic algorithms it uses -- AES-256, ChaCha20, Argon2 -- are international standards with implementations in every major programming language. Even if every current KeePass-compatible application were abandoned simultaneously, the format is well-documented enough that a new reader could be built from the specification.

This is not a hypothetical benefit. The KDBX format has been continuously readable for over fifteen years across application changes, platform migrations, and operating system upgrades. Users who created KeePass databases in 2010 can still open them today in any modern client. Try saying the same about a proprietary format from a company that no longer exists.

## Community Control vs. Corporate Control

The development trajectory of an open-source project is governed by its community. Anyone can propose changes, report issues, review code, and fork the project if they disagree with its direction. The KDBX format evolves through consensus: when KeePass moved from KDBX 3.1 to 4.0, the changes (Argon2 support, HMAC-authenticated blocks, inner header encryption) were driven by genuine security improvements, debated publicly, and implemented transparently. See our [KDBX format guide](/keepass/kdbx-format-guide/) for the technical details of that evolution.

Corporate-controlled formats evolve based on business priorities. A company might add features that increase user engagement but also increase complexity and attack surface. It might change the format in ways that break backward compatibility with older clients to force upgrades. It might introduce server-side components that make the format dependent on proprietary infrastructure. These decisions are made in boardrooms, not in public, and users learn about them after the fact.

This is not to say that all corporate decisions are bad or that all community decisions are good. But the accountability structures are fundamentally different. When a community project makes a controversial change, it can be forked -- the entire codebase and format specification can be taken in a different direction by anyone who disagrees. When a corporation makes a controversial change to a proprietary format, users can either accept it or leave (taking only what the export function provides).

The ability to fork is the ultimate check on power in open-source software, and it is a check that proprietary formats inherently lack.

## Interoperability: The Practical Test

Interoperability measures how well software works with other software. For password managers, the practical test is simple: can you use your data across different devices, operating systems, and applications without losing information?

### Proprietary Managers

Most proprietary password managers solve interoperability by building their own client for every platform: Windows, macOS, Linux, iOS, Android, and browser extensions. This works as long as the company continues to maintain all those clients. If it drops support for a platform (as some have done with Linux), users on that platform are stranded.

Cross-application interoperability is essentially nonexistent. You cannot open a 1Password vault in Dashlane, or a LastPass export in Bitwarden, without a conversion process that inevitably loses some data. Each application is an island, and moving between islands requires getting wet.

### The KeePass Ecosystem

The KDBX format supports a fundamentally different model. Because the format is open, independent developers on every platform can build applications that read and write the same files. The result is an ecosystem where:

- **Desktop users** can choose between KeePassXC, KeePass 2.x, KeePassX, or KeeWeb
- **Apple users** can use PanicVault, a native macOS and iOS app, or Strongbox
- **Android users** can choose KeePassDX, KeePass2Android, or KeepShare
- **iOS users** can also choose KeePassium or AuthPass
- **Web users** can use KeeWeb directly in the browser

All of these applications operate on the same KDBX file. A user can create a database in KeePassXC on their Linux workstation, sync it via Dropbox, and access it through Strongbox on their iPhone -- with full fidelity, including custom fields, attachments, and folder structure.

This is interoperability through an open standard rather than through vendor uniformity. It is more resilient because it does not depend on any single organization's continued commitment to a platform.

## The Security Angle

The choice between open and proprietary formats has direct security implications beyond the trust issues covered in our guide on [who to trust with your passwords](/password-managers/trust-with-passwords/).

### Auditability

Open formats can be independently audited. Security researchers can examine the KDBX specification, identify potential weaknesses, and verify that implementations handle encryption correctly. This has happened repeatedly -- the [KeePass ecosystem](/keepass/gold-standard/) has been reviewed by EU-funded security audits, independent researchers, and the broader cryptography community.

Proprietary formats, by definition, resist independent auditing. You cannot verify how a proprietary format encrypts data unless the company discloses its implementation -- and even then, you are relying on the company's description matching reality. History has shown that companies sometimes overstate or misrepresent their security properties. When LastPass was breached in 2022, the specifics of how vault data was encrypted (and which metadata was not encrypted) became a matter of intense scrutiny -- scrutiny that would have been possible before the breach if the format had been open.

### Attack Surface

Proprietary cloud-based managers introduce server-side attack surface that open, local-first formats simply do not have. When your encrypted vault sits on a vendor's server, it can be exfiltrated in a breach. Even if the encryption is strong, the attacker now has unlimited time and resources to attempt to crack it. Our analysis of [what happens when password managers get hacked](/password-managers/what-if-hacked/) explores these scenarios in detail.

With a KDBX file stored locally or on your own cloud storage, the attack surface is limited to your own devices and accounts. There is no centralized target that, if breached, exposes millions of users' vaults simultaneously.

### Cryptographic Transparency

The KDBX format uses well-understood, standardized cryptographic primitives: AES-256 or ChaCha20 for encryption, SHA-256 and HMAC-SHA-256 for integrity, and Argon2 for key derivation. These are the same algorithms used by the world's most security-critical systems, and their security properties are extensively studied.

Proprietary formats may use the same underlying algorithms, but without access to the implementation, you cannot verify how they are applied. Are IVs generated correctly? Is the key derivation parameterized adequately? Is sensitive metadata encrypted or left in plaintext? These are questions that can only be answered definitively when the format is open.

## The Cost of "Free" Proprietary Services

Many proprietary password managers offer a free tier. This can seem like the best of both worlds: professional polish, cloud synchronization, and zero cost. But the free tier serves a specific business function -- it is a funnel to paid plans, and the dynamics of that funnel shape the product in ways that are not always aligned with user interests.

Free tiers are typically limited: fewer devices, no sharing, no advanced features. The full product costs $36 to $60 per year. Over a decade, that is $360 to $600 -- for software that performs a function achievable with free, open-source tools using openly auditable cryptography.

More importantly, the free tier still locks your data in a proprietary format. You are not paying money, but you are paying with control. The switching cost accumulates silently as you add entries, and by the time you consider leaving, the friction of export and migration serves as an effective retention mechanism.

KeePass-compatible applications, by contrast, are genuinely free. KeePassXC, KeePassDX, and KeeWeb are open-source and community-funded. Strongbox and KeePassium offer optional premium tiers for convenience features, but the core password management functionality -- and crucially, full KDBX format compatibility -- is available without payment.

## Making the Decision

Choosing between open and proprietary formats is not just a technical decision. It is a decision about:

- **Who controls your data** -- You or a company?
- **How long your data remains accessible** -- As long as open standards exist, or as long as a company remains in business?
- **How verifiable your security is** -- Independently auditable, or trust-the-vendor?
- **How portable your data is** -- Natively interoperable, or dependent on export functions?
- **What you pay** -- Nothing, or recurring subscriptions?

For users who prioritize security, autonomy, and long-term data ownership, the KDBX format and the KeePass ecosystem offer a combination that proprietary alternatives cannot match. Your passwords are too important to store in a format that someone else controls. The open standard exists, it is proven, and it is free. The only question is whether you choose to use it.
