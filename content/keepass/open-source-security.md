---
title: "Is KeePass Open Source? Licences and Audits for Every KeePass App"
description: "Yes: KeePass is open source under the GPL. Here is the licence of every major KeePass app, what has been audited, and why the open .kdbx format matters even when an app is closed."
date: 2026-02-13
lastmod: 2026-10-21
draft: false
silo: "KeePass & Open Standards"
aliases:
  - /keepass/open-source-vs-proprietary/
faq:
  - q: "Is KeePass open source?"
    a: "Yes. KeePass Password Safe, the original Windows program by Dominik Reichl, is distributed under the GNU General Public License version 2 or later, and its source code can be downloaded from keepass.info. It is also free."
  - q: "Is KeePassXC open source?"
    a: "Yes. KeePassXC is a separate project from KeePass, licensed under the GNU GPL version 2 or 3. Its releases are signed with OpenPGP and published with SHA-256 digests so you can check a download."
  - q: "Are Strongbox and KeePassium open source?"
    a: "Both publish their source code, Strongbox under the AGPL-3.0 and KeePassium under the GPLv3. But iPhone apps come from the App Store, and there is no way to verify that the build you install was compiled from that published code."
  - q: "Is PanicVault open source?"
    a: "No. PanicVault is closed source. It stores your passwords in the open KDBX 4 format, so the same file opens in KeePassXC or any other KDBX app, and every commit is adversarially reviewed in CI by Fable, Anthropic's most advanced model for cybersecurity reasoning."
  - q: "Has KeePass been audited?"
    a: "The EU-FOSSA project audited KeePass 1.31 in 2016 and found no critical or high-severity issues. A later EU-FOSSA bug bounty covering KeePass 2.x found a few minor issues, which were fixed. KeePassXC had an independent audit in 2023 and received the French ANSSI's CSPN certification in 2025."
  - q: "Does KeePass connect to the internet?"
    a: "Only if you let it. On first start KeePass asks whether to enable automatic update checks, and it can open or save a database at a URL (FTP, HTTP, HTTPS or WebDAV) if you choose to. Otherwise it works with a local file."
---

Yes, KeePass is open source. KeePass Password Safe, the Windows program Dominik Reichl has maintained since 2003, is released under the GNU General Public License, and anyone can download, read and build its source code. But "KeePass" also names a whole family of apps that open the same `.kdbx` files, and not all of them are open. Some publish their code under open licences, some publish code you cannot match to the app you install, and some are closed.

This page lists the licence of each major KeePass app, what has actually been audited, and why the open file format matters even when the app you use is closed.

> **Quick answer**: **KeePass 2.x** (GPL v2 or later), **KeePassXC** (GPL v2 or v3), **KeePassDX** and **Keepass2Android** on Android, and **MacPass** on Mac are open source. **Strongbox** and **KeePassium** publish their source code, but their App Store builds can't be verified against it. **[PanicVault](https://apps.apple.com/app/id6759188575)** is closed source. All of them read and write the same open KDBX format, so your passwords are never tied to one app.

## Is KeePass Open Source?

KeePass 2.x is [distributed under the GNU General Public License version 2 or later](https://keepass.info/help/v2/license.html). You can read the code, build the program yourself, change it, and share your changes under the same licence. It is also free: there is no paid edition.

KeePass also created the `.kdbx` file format. The format is documented by that open source code and has been implemented independently by dozens of other apps, which is why a database made in KeePass opens in KeePassXC, KeePassDX or an iPhone app. Our [KDBX format guide](/keepass/kdbx-format-guide/) walks through how it works.

## Which KeePass Apps Are Open Source?

| App | Platforms | Licence | What you can verify |
|---|---|---|---|
| KeePass 2.x | Windows (Linux, macOS via Mono) | GPL v2 or later | Source on keepass.info; build it yourself |
| KeePassXC | Windows, Mac, Linux | GPL v2 or v3 | Releases [signed with OpenPGP](https://keepassxc.org/verifying-signatures/) and published with SHA-256 digests |
| KeePassDX | Android | GPL v3 or later | Source on GitHub |
| Keepass2Android | Android | GPL v3 | Source on GitHub |
| MacPass | Mac | GPL v3 | Source on GitHub |
| Strongbox | iPhone, iPad, Mac | AGPL-3.0 (source published) | Source on GitHub; App Store build can't be matched to it |
| KeePassium | iPhone, iPad, Mac | GPL v3 (source published) | Source on GitHub; App Store build can't be matched to it |
| PanicVault | iPhone, iPad, Mac | Closed source | The KDBX 4 files it writes open in any other KDBX app |

On desktop and Android, "open source" means what it says: you can compile the app yourself, or check that a download is the one the developers signed. On iPhone and iPad it means less. Every app comes through the App Store, and there is no way to confirm that the build you install was compiled from the code a developer published. Published source still has value -- anyone can review it and report bugs -- but in practice, on iOS you are trusting the developer's build whichever app you choose. What you can check is the developer's track record, any published audits, and the format your data is stored in.

## Open Format vs. Open Code

In 1883 Auguste Kerckhoffs argued that a cryptographic system should stay secure even if everything about it except the key is public. KDBX follows that principle. The ciphers (AES-256 or ChaCha20), the key derivation function (Argon2 or AES-KDF) and its settings are all standard, and they are written into the file's header for anyone to read. The security of the file rests on your master password, key file or YubiKey, not on any secret about how the app works.

That is why an open format matters even when the app is closed:

- **You can always leave.** Any KDBX app opens your file. If a closed app is abandoned, changes direction or loses your trust, you open the same file somewhere else, with no export. Our [data portability guide](/keepass/data-portability/) covers this in depth.
- **You can check the app's output.** Open a database a closed app has saved in KeePassXC. If it opens with your password and shows your entries, the app wrote standard KDBX, encrypted with the cipher and key derivation settings shown in the database settings.
- **You cannot check everything.** A second app confirms the file, not what the first app does in memory, with your clipboard, or over the network. For that you rely on the developer's practices and on audits.

PanicVault is closed source, and this is the trade it makes. Your data stays in an open format you can take anywhere, and instead of publishing its code it relies on a continuous audit: every commit and pull request is reviewed in CI by Fable, Anthropic's most advanced model for cybersecurity reasoning, which reads each change the way an attacker would ([how the continuous audit works](/engineering/ai-code-audit-fable-5/)). That is a different kind of assurance from code you can read yourself, and it is fair to weigh it that way.

## Audits and Vulnerability History

Open source makes review possible; it does not mean review has happened. These are the published audits and notable vulnerabilities for the main KeePass apps.

### KeePass

- **EU-FOSSA audit, 2016.** The European Commission's Free and Open Source Software Auditing project reviewed **KeePass 1.31**, the classic 1.x edition, in August and September 2016. Its [summary](https://interoperable-europe.ec.europa.eu/sites/default/files/inline-files/DLV%20WP6%20-02-%20Summary%20of%20the%20evaluation%20of%20results%20_KeePass_published.pdf) reports no critical or high-severity findings (five medium, three low) and calls KeePass mature. Note that it covered 1.x, not the KeePass 2.x most people use today.
- **EU-FOSSA 2 bug bounty, 2019-2020.** KeePass 2.x was part of the EU's follow-up bug bounty; according to [keepass.info](https://keepass.info/ratings.html), "a few minor issues were found and fixed."
- **[CVE-2023-32784](https://nvd.nist.gov/vuln/detail/CVE-2023-32784).** In KeePass 2.x before 2.54, all but the first character of the master password could be recovered from a memory dump. Version 2.54 added mitigations, so make sure you run 2.54 or later.
- **[CVE-2023-24055](https://nvd.nist.gov/vuln/detail/CVE-2023-24055).** Someone with write access to KeePass's XML configuration file could add an export trigger that writes your passwords out in cleartext. The CVE is disputed: the developer's position is that KeePass is not meant to resist an attacker who already has that level of access to your PC.

### KeePassXC

- **Independent audit, 2023.** Security consultant Zaur Molotnikov audited KeePassXC 2.7.4 free of charge and, according to the [published report](https://keepassxc.org/blog/2023-04-15-audit-report/), found no major problems.
- **ANSSI CSPN certification, 2025.** France's national cybersecurity agency certified KeePassXC 2.7.9 on Windows 10 under its CSPN scheme (ANSSI-CSPN-2025/16); see KeePassXC's [audits page](https://keepassxc.org/audits/).

### iPhone and iPad Apps

KeePassium's App Store listing says it has been independently audited by Cure53. PanicVault's continuous Fable audit is described above. Whichever app you use, keep it updated: on iOS, fixes reach you only through App Store updates.

## Does KeePass Connect to the Internet?

Only if you let it. According to [KeePass's technical FAQ](https://keepass.info/help/base/faq_tech.html), on first start it asks whether to enable automatic update checks, which send no personal information and never download or install anything by themselves. KeePass can also [open and save a database at a URL](https://keepass.info/help/v2/ioconnect.html) -- FTP, HTTP, HTTPS or WebDAV -- if you choose to, and plugins can add network features of their own. Otherwise it works with a file on your disk, which makes its network behaviour easy to watch with a firewall.

## How to Verify Security Claims Yourself

You do not need to be a cryptographer to check the basics:

1. **Look at the source repository.** Regular commits, several active contributors, and a security policy (often a SECURITY.md file) explaining how to report vulnerabilities are good signs.
2. **Read the audit reports, and note what they covered.** Check the version and scope. The 2016 EU-FOSSA audit of KeePass, for example, covered 1.31, not 2.x.
3. **Search the National Vulnerability Database.** Look the app up at [nvd.nist.gov](https://nvd.nist.gov/) and see how serious its CVEs were and how quickly they were fixed. A few well-handled CVEs are a healthier sign than none and no sign of review.
4. **Verify your download.** On desktop, check the signature or hash the developers publish; KeePassXC explains [how to verify its releases](https://keepassxc.org/verifying-signatures/).
5. **Build from source.** For the highest assurance on desktop or Android, compile the app yourself from the published code.
6. **Open your database in a second app.** If another KDBX app opens it, your data is in the standard format and not dependent on the app that wrote it.

## What Open Source Does Not Guarantee

Open source is a strong property, but not a complete one:

- **Published is not the same as reviewed.** Code that nobody reads is no safer than closed code. Look for audits and an active community, not just a licence.
- **Supply-chain attacks bypass source review.** A compromised dependency or build system can ship malicious code that is not in the project's own source. The 2024 XZ Utils backdoor attempt showed how patient these attacks can be.
- **Store builds can't be matched to source.** As above, on iOS you trust the developer's build either way.
- **Your own setup still matters.** No licence protects a weak master password, an unbacked-up database, or a phishing page you type it into. Our guide to [KeePass encryption](/keepass/encryption-explained/) explains what the master password protects.

The practical answer is to use a KeePass app whose development you can check in the ways that matter to you, and to keep your passwords in the open KDBX format, so that choice is never permanent. Our list of [KeePass apps for every platform](/keepass/compatible-apps/) covers the options, and our look at the [KeePass approach](/keepass/gold-standard/) explains why the format matters as much as the app.
