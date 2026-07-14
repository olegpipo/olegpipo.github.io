---
title: "How PanicVault Is Built: Our Secure Development Lifecycle"
description: "The threat model behind a password manager and how every phase of PanicVault's development -- design, code, review, test, build, release -- maps to the NIST Secure Software Development Framework."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "Engineering & Security"
---

Most security marketing starts with the algorithm. "We use AES-256." That sentence is true of PanicVault, and it is almost meaningless on its own. AES-256 has never been broken in practice. Password managers, on the other hand, have failed repeatedly -- not because the cipher was weak, but because a key was written somewhere it should not have been, a clipboard was never cleared, an error path returned success, or a vault file was parsed by code that trusted its input.

Security is not a property of the cipher. It is a property of the process that produces the code around the cipher. This article describes that process at PanicVault: the threat model we design against, and how each phase of our development lifecycle maps to the practices in the NIST Secure Software Development Framework (SSDF, SP 800-218).

## What a Threat Model Actually Is

If you have never seen one, a threat model sounds more mysterious than it is. A threat model is a written answer to four questions:

1. **What are we protecting?** (the assets)
2. **Who wants it, and what can they do?** (the adversaries and their capabilities)
3. **Where can they touch our system?** (the entry points and trust boundaries)
4. **What could go wrong at each of those points, and what stops it?** (the threats and mitigations)

That is the whole idea. It is a structured way of being pessimistic on purpose, before you write the code rather than after someone else finds the flaw. A common technique for step four is **STRIDE**, a checklist that prompts you to consider six categories of threat at every boundary: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege.

The important word is *boundary*. A trust boundary is any place where data or control crosses from something you trust into something you do not -- or the reverse. A file you read from disk crosses a boundary. A string handed to you by another app crosses a boundary. The clipboard is a boundary. So is the moment your app goes into the background and the operating system takes a screenshot of it.

Threat modelling comes first at PanicVault because it is the only step that determines what all the later steps are even for. It is also the practice NIST places at the head of the software production group: **PW.1, "design software to meet security requirements and mitigate security risks."**

## The PanicVault Threat Model

A password manager is an unusually clean thing to threat model, because the asset list is short and an attacker's goals are obvious. Here is what an adversary actually wants from PanicVault.

### Asset 1: The vault file at rest

The `.kdbx` file is the crown jewel. It contains every credential you own, and unlike a server-side database it is a *portable* artifact -- it can be copied to a USB stick, pulled out of a backup, or downloaded from a compromised cloud account.

We therefore assume, as a baseline, that **the attacker already has your vault file.** Not as a worst case, but as the default case. Everything else follows from that assumption. It is why the file is encrypted with AES-256 or ChaCha20 in the [KDBX 4 format](/keepass/kdbx-format-guide/), why the master password is stretched with a memory-hard KDF rather than a fast hash, and why the file is authenticated with an HMAC so that a tampered vault is rejected rather than partially decrypted. If the attacker has the file, the only thing standing between them and your credentials is the cost of guessing your master password. We design for that fight, and we lose it only if your master password is weak -- which is why the [master password guide](/password-managers/master-password-guide/) is the most important thing we ask of you.

### Asset 2: The master key in memory

While your vault is unlocked, the derived encryption key exists in RAM. This is the single most sensitive window in the product's entire lifetime. An attacker who can read the process's memory -- through a debugger on a compromised machine, a crash dump, an over-eager logging call, or swap written to disk -- does not need to crack anything.

The mitigations here are unglamorous and entirely about discipline: minimize how long key material lives, keep it out of Swift types that copy silently, zero the buffers deterministically when done, and never allow a secret to reach a log, an error message, or a crash report. We cover the mechanics in [cryptographic engineering](/engineering/cryptographic-engineering/).

### Asset 3: The clipboard

The clipboard is the least respected attack surface in the entire category. When you copy a password, that password leaves your app's sandbox and is placed in a system-wide buffer that -- historically, on both iOS and macOS -- any other running application could read. Universal Clipboard can even push it to another device over the network.

The clipboard is a deliberate trust boundary crossing, made by the user, and it needs explicit expiry, not good intentions. See [platform hardening](/engineering/ios-app-hardening/) for how we bound it.

### Asset 4: The AutoFill surface

The credential provider extension is the part of PanicVault that talks to the rest of the world. It receives a service identifier -- a domain, an app bundle ID -- from the system and decides which credentials to offer. Get the matching logic wrong and you have built a phishing amplifier: a manager that helpfully offers your bank password to `bank-secure-login[.]com`.

Correct AutoFill is a *security* feature, not a convenience feature, and it lives in a separate process with a separate lock state. Our [AutoFill guide](/apple/autofill-iphone-guide/) covers the user-facing behaviour; the isolation model is in the platform hardening article.

### Asset 5: The sync path

PanicVault is offline-first: there is no PanicVault account and no PanicVault server. But your vault file can still travel through iCloud Drive, Dropbox, or a file server, which means the sync path is part of the threat model even though we do not operate it.

The adversary here is not only "someone who steals the file from the cloud" (see Asset 1 -- we already assume that). It is the subtler one: an adversary who can *modify* or *roll back* the file. A silently truncated write, a stale replica that resurrects a password you rotated, a conflict resolved by picking the wrong side. This is why every write is atomic, every read verifies the HMAC before a single entry is parsed, and conflicts are surfaced to you rather than resolved by a coin flip. [Cloud sync](/cloud-sync/) is an integrity problem more than a confidentiality problem, because encryption already handles confidentiality.

### The adversaries

- **The opportunistic thief** who has your locked or unlocked device. Mitigated by auto-lock, biometric gating, and the platform's own data protection.
- **The remote attacker** holding a copy of your vault file. Mitigated by encryption and the KDF -- and by nothing else, which is why the KDF parameters matter so much.
- **A malicious or compromised app on the same device.** Mostly contained by the OS sandbox, but the clipboard and the pasteboard are the leaks it will look for.
- **A compromised dependency or build system.** The subject of [supply chain security](/engineering/supply-chain-security/).
- **Us.** A vendor that receives telemetry can leak telemetry. A vendor with an account system has a database to breach. Our answer is structural rather than promissory: PanicVault has no account, no server, and no analytics, so there is no vendor-side asset to compromise. This is the same reasoning behind [zero-knowledge encryption](/password-managers/zero-knowledge-encryption/), taken one step further -- we do not hold ciphertext either.

## Mapping the Lifecycle to NIST SSDF

The SSDF (NIST SP 800-218) is not a certification and we make no claim of one. It is a vocabulary: a set of practices grouped into four families -- Prepare the Organization (PO), Protect the Software (PS), Produce Well-Secured Software (PW), and Respond to Vulnerabilities (RV). Its usefulness is that it forces you to name where each of your controls sits, and to notice the gaps. Here is how our lifecycle maps onto it.

### Design (PO.1, PW.1, PW.2)

Every feature that touches a secret starts with a written note answering the four threat-model questions above for that feature specifically. Adding TOTP? Then the shared secret becomes an asset, and the fact that it now lives in the same vault as the password is a threat-model change worth stating out loud -- which we do, honestly, in our discussion of [using a password manager as your authenticator](/two-factor-authentication/password-manager-as-authenticator/).

Two design rules are absolute:

- **We implement no custom cryptography.** Not a cipher, not a KDF, not a MAC. We compose vetted, standard primitives.
- **Defaults are the secure setting** (SSDF PW.9). A user who never opens Settings must still get memory-hard key derivation, a short auto-lock, and clipboard expiry.

Design intent is checked against the **OWASP Mobile Application Security Verification Standard (MASVS)**, using the MASTG as the testing companion. MASVS gives us a per-feature checklist across storage, cryptography, authentication, platform interaction, code quality, and resilience. We use it as a design and verification checklist -- alignment, not certification.

### Implementation (PW.4, PW.5, PW.6)

PanicVault is written in Swift, which gives us memory safety by default: no buffer overruns, no use-after-free, no dangling pointers in ordinary code. That default is a genuine, categorical elimination of an entire vulnerability class -- and it is exactly why the places where we *leave* the default matter so much. Cryptographic code touches raw byte buffers. Format parsing touches raw byte buffers. Those are the regions where `Unsafe` pointers appear, and those are the regions that get the most review attention, because Swift's guarantees stop at that boundary.

PW.4 -- "reuse existing, well-secured software" -- is the practice that a password manager is most tempted to violate, because everyone wants to hand-roll their crypto. We do not.

### Review (PW.7)

PW.7 asks you to review and analyze human-readable code to find vulnerabilities and verify compliance. We do this three ways on every single pull request, because each catches a different class of defect:

- **[SonarQube static analysis](/engineering/static-analysis-sonarqube/)** with a blocking quality gate -- deterministic, syntactic, taint-aware, tireless, and unable to understand intent.
- **[Adversarial AI review by Fable 5](/engineering/ai-code-audit-fable-5/)** -- semantic, adversarial, high-recall, reads the diff asking "how would I break this," and catches logic and state-machine flaws that no linter can express.
- **Human review** -- the only one of the three that knows what we *meant*.

### Testing (PW.8)

PW.8 is "test executable code to identify vulnerabilities and verify compliance." Our floor is **100% test coverage, enforced as a merge requirement** -- not a target, a gate. The crypto core is additionally checked against published known-answer vectors (the Argon2 vectors in RFC 9106, the TOTP vectors in RFC 6238), and the KDBX parser is exercised against malformed and hostile inputs, because a vault file is untrusted input by definition.

We are precise about what coverage does and does not prove, and we think that precision is the point: see [why we hold 100% coverage](/engineering/hundred-percent-test-coverage/).

### Build and release (PS.1, PS.2, PS.3, PW.6)

Dependencies are pinned by lockfile. The toolchain version is pinned. The build is produced by CI, not by a laptop. Releases are code-signed and notarized by Apple, giving you a verifiable chain from our build to the binary on your device. This is the Protect the Software family, and it is covered in [supply chain security](/engineering/supply-chain-security/).

### Respond (RV.1, RV.2, RV.3)

Every defect with a security dimension -- whether we found it, a tool found it, or a user reported it -- follows the same path: reproduce it with a **test that fails first**, fix it, watch the test go green, and then ask RV.3's question, "what class of bug is this, and where else could it exist?" A fix that only fixes the one instance is an incomplete fix. That is how a bug becomes a permanently closed door instead of a temporarily patched one.

## Why the Process Is the Product

You cannot inspect our engineering culture from the App Store page, and you should be skeptical of any vendor asking you to take security on faith. That skepticism is precisely why we build on an [open format](/keepass/) rather than a proprietary one: even if you distrust every word on this page, your vault is a standard KDBX 4 file that you can open with KeePassXC, verify independently, and take with you the day we disappoint you.

The lifecycle described here exists to make the *code* worthy of the *format*. The format guarantees you can leave. The process is how we try to make sure you never need to.

Continue with the [Engineering and Security Assurance overview](/engineering/), or go deeper on [how we handle keys and secrets](/engineering/cryptographic-engineering/).
