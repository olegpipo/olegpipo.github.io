---
title: "Data Portability: Why Your Password Manager Should Never Lock You In"
description: "Understand why data portability matters for password managers, how open standards like KDBX prevent vendor lock-in, and what to look for before trusting a vault."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

Your passwords are yours. That statement sounds obvious, but the reality of how most password managers operate tells a different story. When you store credentials in a proprietary vault, you are trusting not only that the vendor will keep your data secure, but that they will let you leave with it when you want to. Many will not -- at least not easily. Export tools are limited, formats are undocumented, and the switching costs are designed, whether intentionally or not, to keep you paying month after month. This is vendor lock-in, and it has no place in the management of your most sensitive personal data.

The [KeePass](/keepass/) ecosystem takes a fundamentally different approach. Your vault is stored in the KDBX format -- an open, documented standard that any developer can implement. You can move your database between applications, platforms, and operating systems without conversion, without data loss, and without asking permission. This article examines what data portability means for password management, why it matters more than most people realize, and how the choice between open and proprietary formats shapes your security and autonomy for years to come.

## What Data Portability Actually Means

Data portability is the ability to move your data from one service, application, or platform to another without significant loss of information, functionality, or access. In the context of password management, it means:

- You can export your credentials in a format that other password managers can read.
- You can import credentials from other sources without manual re-entry.
- Your vault file is not tied to a specific application -- multiple programs can open and edit it.
- If your current password manager is discontinued, acquired, breached, or simply falls out of favor, you can migrate to an alternative without starting from scratch.

True portability is more than a one-time export function buried in a settings menu. It means your data lives in a format that is understood by multiple independent implementations, documented publicly, and not controlled by any single entity.

### The Spectrum of Portability

Not all password managers offer the same level of portability, and the differences are significant:

**Fully portable (open format):** Your vault is a file in a documented, open format that multiple independent applications support. You can open it in any compatible app without conversion. The KeePass KDBX format sits at this end of the spectrum.

**Export-portable:** The vault is stored in a proprietary format, but the application provides export functionality to CSV, JSON, or other common formats. You can get your data out, but the process is manual, may lose metadata (like TOTP secrets, attachments, or custom fields), and the exported file is typically unencrypted -- creating a serious security risk during the migration.

**Minimally portable:** The vault is proprietary and the export options are limited or nonexistent. You can view your passwords in the application, but extracting them in bulk requires third-party tools, screen scraping, or manual copy-paste.

**Locked in:** The vault exists only on the vendor's servers. There is no local copy, no export function, and no way to access your data outside the vendor's application. If the vendor shuts down, raises prices beyond what you will pay, or suffers a catastrophic breach, you lose access.

## Open Standards vs. Walled Gardens

The distinction between open standards and proprietary walled gardens is central to understanding data portability.

### Open Standards: The KDBX Model

The KDBX format -- used by KeePass, KeePassXC, KeePassDX, Strongbox, KeeWeb, and dozens of other applications -- is an open standard. Its structure is documented, its encryption algorithms are well-known (AES-256, ChaCha20, Argon2), and anyone can build software that reads and writes KDBX files.

This openness produces several concrete benefits:

**No single point of failure.** If the original KeePass application were abandoned tomorrow, your data would remain accessible through KeePassXC, Strongbox, KeePassDX, and every other compatible implementation. The [ecosystem of compatible apps](/keepass/compatible-apps/) ensures continuity.

**Independent security auditing.** Because the format is open, security researchers can examine exactly how your data is encrypted, how keys are derived, and whether the implementation matches the specification. Proprietary formats cannot be audited this way -- you are trusting the vendor's assurances rather than verifiable code. This transparency is part of what makes the KeePass approach the [gold standard](/keepass/gold-standard/) for password security.

**Competition on quality.** When multiple applications support the same format, they compete on user experience, features, performance, and platform support rather than on data lock-in. KeePassXC exists because developers saw an opportunity to build a better cross-platform experience on top of the KDBX format. Strongbox exists because iOS users wanted a native, polished vault app. The open format enabled both without requiring users to migrate their data.

**Long-term archival safety.** A KDBX file created in 2010 can still be opened in 2026 by any compatible application. The format has evolved (from KDB to KDBX 3.1 to KDBX 4.0/4.1), but backward compatibility has been maintained. Your data does not depend on any company remaining in business or any subscription remaining active.

For a detailed look at the format itself, see our [KDBX format guide](/keepass/kdbx-format-guide/).

### Walled Gardens: The Proprietary Model

Proprietary password managers store your vault in a format that only their software can read natively. The encryption may be strong, the user experience may be excellent, and the service may have a good track record -- but your data is fundamentally tied to their ecosystem.

The risks are concrete:

**Vendor discontinuation.** Companies fail, get acquired, or pivot to different business models. If your password manager shuts down, your access to your own data depends entirely on whatever export tools they built (if any) and whatever migration path they provide (if any). History is full of examples: password managers have been discontinued, acquired and sunsetted, or changed their pricing models dramatically, leaving users scrambling.

**Price increases.** When your data is locked in a proprietary format, the vendor's leverage in pricing discussions is significant. Switching costs -- the time and effort to export, find an alternative, import, verify, and rebuild integrations -- serve as a de facto price floor. You will pay more than you want to before you will endure the pain of migration.

**Feature removal or degradation.** Vendors can remove features, change sync behavior, drop platform support, or alter security practices. When you are locked in, your options are to accept the changes or begin a painful migration. When your data is in an open format, you switch applications and keep working.

**Forced trust.** With a proprietary format, you cannot independently verify how your data is encrypted, how keys are managed, or what data the vendor can access. You trust their documentation, their marketing, and their reputation. With an open format, you trust the mathematics and the publicly auditable code. For more on the trust dynamics of password management, see our discussion of [trusting a company with your passwords](/password-managers/trust-with-passwords/).

## How KDBX Enables True Portability

The KDBX format is the technical foundation of KeePass data portability. Understanding what it stores and how it stores it explains why the portability is so comprehensive.

### What KDBX Contains

A KDBX file is a self-contained, encrypted database that stores:

- **Entries:** Each entry holds a title, username, password, URL, notes, and an arbitrary number of custom fields.
- **Groups:** Entries are organized into a hierarchical group structure (folders and subfolders).
- **Metadata:** Database name, description, default username, recycle bin settings, custom icons, and color labels.
- **History:** Previous versions of each entry, allowing you to see when a password was changed and revert if needed.
- **Attachments:** Binary files (documents, certificates, key files) stored within entries.
- **TOTP configuration:** Time-based one-time password secrets for two-factor authentication.
- **Custom data:** Application-specific settings stored within the file (KeePassXC uses this for browser integration state, for example).

All of this is encrypted with AES-256 or ChaCha20 and protected by your master password (and optionally a key file) through Argon2 or AES-KDF key derivation.

### Moving Between Applications

Because the format is standardized, you can open the same .kdbx file in:

- **KeePassXC** on Windows, macOS, or Linux
- **KeePassDX** on Android
- **Strongbox** or **KeePassium** on iOS
- **KeeWeb** in a web browser
- **The original KeePass 2.x** on Windows (via .NET or Mono)

No conversion is needed. You open the file, enter your master password, and your complete vault is there -- entries, groups, history, attachments, and all. This is not an import/export workflow. It is the same file being read natively by different software.

### Import and Export Capabilities

Beyond native KDBX support, KeePass-compatible applications provide import and export paths for migration:

**Importing from other password managers:** KeePassXC and KeePass 2.x can import from 1Password (1PIF/1PUX), LastPass (CSV), Bitwarden (JSON), Dashlane (CSV), Chrome (CSV), Firefox, and many others. The import translates the foreign format into KDBX entries, preserving as much metadata as the source format provides.

**Exporting to common formats:** If you ever need to leave the KeePass ecosystem (though the open format makes this far less likely), you can export to CSV, XML, or HTML. Be aware that these exports are unencrypted -- handle them with extreme care and securely delete them immediately after use.

The import capability means that migrating to the KeePass ecosystem from a proprietary manager is straightforward. The open format means that once you are in the ecosystem, you never need to migrate again -- only switch between compatible applications.

## Switching Costs: The Hidden Tax of Proprietary Formats

Switching costs are the time, effort, risk, and frustration involved in migrating from one password manager to another. They are the primary mechanism of vendor lock-in, and they are deliberately or incidentally high for proprietary managers.

### The Components of Switching Cost

**Export difficulty.** Some managers bury the export function, limit what can be exported, or require you to export in batches. A few require you to be on a paid tier to export your own data.

**Data loss during migration.** CSV exports typically lose TOTP secrets, file attachments, entry history, custom fields, and group structure. You get usernames, passwords, URLs, and maybe notes. Everything else is gone.

**Verification burden.** After importing into a new manager, you need to verify that every entry transferred correctly. With hundreds of entries, this is tedious and error-prone. A single missing or corrupted entry might not be discovered until you need that specific password -- at which point recovery may be difficult.

**Integration rebuilding.** Browser extensions, auto-fill configurations, mobile app settings, and SSH agent integrations all need to be reconfigured. Some integrations store state in the vault file (KeePassXC does this well); proprietary managers may store it server-side where it cannot be exported.

**Habit disruption.** Keyboard shortcuts, workflows, and muscle memory all change. This is a real cost, even though it is not a data cost.

### The Open Format Advantage

With KDBX, switching costs are minimal:

- Switch from KeePassXC to Strongbox? Open the same file.
- Switch from KeePass 2.x to KeePassXC? Open the same file.
- Switch from desktop to mobile? Open the same file.

There is no export, no import, no verification, no data loss. The file is the vault, and any compatible application can use it. This is what genuine data portability looks like.

## The Regulatory Landscape: Data Portability as a Right

Data portability is not just a technical preference -- it is increasingly a legal right.

### GDPR (European Union)

The General Data Protection Regulation, in effect since May 2018, includes Article 20: the right to data portability. This gives EU residents the right to receive their personal data in a "structured, commonly used and machine-readable format" and to transmit that data to another controller without hindrance.

For password managers, this means that EU-based users have a legal right to export their data in a usable format. Whether the proprietary manager's CSV export satisfies the "commonly used and machine-readable" standard is debatable -- a format that loses most metadata and requires manual reconstruction is arguably not meeting the spirit of the regulation.

### CCPA (California)

The California Consumer Privacy Act provides similar data portability rights for California residents. The right to know and the right to data portability give consumers the ability to obtain their data in a readily usable format.

### Digital Markets Act (European Union)

The EU's Digital Markets Act, which came into full effect in 2024, goes further by targeting "gatekeeper" platforms and requiring interoperability and data portability provisions. While current password managers may not qualify as gatekeepers, the regulatory direction is clear: locked-in data is increasingly viewed as anti-competitive.

### The Practical Implication

Regulations provide a backstop, but they are a poor substitute for choosing a portable format from the start. Exercising your legal right to data portability from a proprietary manager involves filing requests, waiting for responses, receiving limited exports, and dealing with data loss. Choosing an open format means you never need to exercise that right because the portability is built into the technology itself.

## Future-Proofing Your Credentials

Your passwords are not a short-term concern. You will need them for years, likely decades. The password manager you choose today needs to work for you in five, ten, or twenty years. Future-proofing requires thinking about what could change and whether your data will survive those changes.

### Scenarios to Consider

**Your password manager company is acquired.** Acquisitions are common in the security industry. The acquiring company may discontinue the product, merge it into a different platform, change the pricing, or alter the security model. With an open format, none of this affects your data.

**Your password manager raises prices significantly.** Subscription models mean you are always one billing cycle away from losing access -- or at least losing the motivation to pay. A local KDBX file costs nothing to maintain.

**A critical vulnerability is discovered.** If a serious flaw is found in your password manager, you want the ability to switch immediately -- not after a multi-day migration process. With KDBX, you can switch applications in minutes.

**Technology platforms shift.** You might move from Windows to macOS, from Android to iOS, from desktop to a platform that does not yet exist. An open, well-documented format is far more likely to be supported on whatever platform comes next than a proprietary format tied to one vendor's roadmap.

**Your needs change.** Today you might be fine with a simple vault. In five years, you might need SSH key management, TOTP integration, or team sharing features. An open format lets you choose the application that best fits your evolving needs without migrating your data.

### The Test of Time

Consider how many software products from ten years ago are still available and unchanged. Now consider which file formats from ten years ago are still readable. Formats outlast applications. Open formats outlast proprietary ones. The KDBX format has been readable across dozens of applications since its introduction, and its open nature ensures that even if every current application were abandoned, new ones could be built to read it.

## What to Look for in a Portable Password Manager

If data portability is important to you (and it should be), evaluate password managers against these criteria:

1. **Open file format.** Can multiple independent applications read your vault file natively, without import/export?
2. **Full-fidelity export.** If export is required, does it preserve all data -- entries, groups, history, attachments, TOTP secrets, custom fields -- or only a subset?
3. **Import from competitors.** Can the manager import data from the tools you might be migrating from?
4. **Local file access.** Do you have direct access to the encrypted vault file, or does it exist only on the vendor's servers?
5. **No subscription gate on data access.** Can you access your data if you stop paying? Some managers lock you out of your vault or limit you to read-only access on the free tier.
6. **Open-source implementation.** Can you verify the code that handles your data? Open source is not a guarantee of security, but it enables independent auditing that proprietary software does not.

The KeePass ecosystem scores well on every criterion. Your vault is a local KDBX file that you control. Multiple open-source applications support it natively. Full import and export capabilities exist. There is no subscription, no server dependency, and no vendor controlling access to your own data.

For a broader comparison of how the KeePass approach differs from proprietary alternatives, see our article on [KeePass vs. proprietary managers](/keepass/vs-proprietary/). And for a critical look at common misconceptions about password management tools, our piece on [password manager myths debunked](/password-managers/myths-debunked/) addresses several portability-related claims.

## The Cost of Ignoring Portability

It is easy to dismiss portability as a theoretical concern. Your password manager works fine. You like the interface. You are not planning to switch. Why worry about it?

Because the situations that make portability critical are, by definition, ones you did not plan for:

- The company behind your password manager announces it is shutting down. You have 30 days to export your data.
- A breach exposes that the vendor's encryption was weaker than advertised. You need to move immediately.
- Your subscription triples in price overnight. You want to leave but dread the migration.
- A platform you depend on drops support for the manager's app.

In each of these scenarios, the user with an open-format vault is inconvenienced for minutes. The user with a proprietary vault is disrupted for days or weeks, with real risk of data loss along the way.

Portability is insurance. It costs nothing when you choose an open format from the start, and it pays off enormously when circumstances force a change you did not anticipate.

## Conclusion

Data portability is not a feature. It is a principle. Your credentials are the keys to your digital life, and you should never cede control of those keys to any single vendor, application, or service. The choice between an open format and a proprietary one is the choice between owning your data and renting access to it.

The KDBX format, supported by the KeePass ecosystem, delivers genuine portability: a single encrypted file that works across dozens of applications, platforms, and operating systems. No export required. No data loss. No switching cost. No vendor lock-in. If you change your mind about which application to use, you take your vault and go.

Choose a password manager that respects your autonomy. Choose one that stores your data in a format you can read with any compatible tool, back up with any method, and keep for as long as you need. Choose portability, because the future is too unpredictable to lock your passwords behind a single vendor's key.
