---
title: "Engineering & Security Assurance: How PanicVault Is Built"
description: "How PanicVault is engineered and verified: adversarial AI review of every commit by Fable 5, a blocking SonarQube quality gate, 100% test coverage, and the cryptographic and platform engineering behind an offline-first password manager."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "Engineering & Security"
sitemap_priority: 0.8
sitemap_changefreq: monthly
---

Every password manager on the market claims to use AES-256. It is a true statement, it costs nothing to say, and it tells you almost nothing about whether the app is safe to trust with your life's credentials.

The cipher has never been the weak point. AES has survived two decades of the most concentrated public cryptanalysis in history without a practical break. Password managers, on the other hand, have failed repeatedly -- and they have failed because a key outlived its scope, because an error path returned success, because a clipboard was never cleared, because a vault file was parsed before its integrity was checked, because a parameter was quietly lowered to make an animation feel faster.

In other words: **the security of a password manager is a property of the engineering process that produces the code, not of the algorithm named on the marketing page.** This section documents ours -- in detail, with the limitations stated openly, so you can judge it rather than take it on faith.

## The Four Controls on Every Change

Nothing merges into PanicVault without passing through all four of the following. They are here because each one is blind to what the others catch.

**1. Adversarial AI security review of every diff.** Every commit and pull request is audited in CI by **Fable 5**, Anthropic's most advanced model for cybersecurity reasoning, instructed to read the change the way an attacker would. It catches the class of defect that no rule engine can express: logic flaws, unsafe state transitions, key-material lifetime bugs, time-of-check-to-time-of-use races, semantically incorrect use of correct cryptography, and error paths that leak. Read the full account -- including a frank section on what AI review is *not* -- in [Continuous AI Security Audit](/engineering/ai-code-audit-fable-5/).

**2. Static analysis with a blocking quality gate.** SonarQube runs SAST on every build. Zero new bugs, zero new vulnerabilities, every security hotspot reviewed, ratings of A. If the gate fails, the build fails and the merge is refused. There is no override button, and [we explain why a gate that can be overridden is not a gate](/engineering/static-analysis-sonarqube/).

**3. 100% test coverage, enforced as a merge requirement.** Line and branch. Not a target -- a floor. We are also precise about what it proves (every line and branch *executes* under test) and what it does not (that the code is *correct*), because [that honesty is the whole point of the metric](/engineering/hundred-percent-test-coverage/).

**4. Human review.** The only one of the four that knows what we meant to build.

## Start Here: The Threat Model

Everything above exists to serve a threat model, and the threat model is the only place a security programme can honestly begin. An attacker coming for a password manager wants five things: **the vault file**, **the master key while it sits in memory**, **the clipboard**, **the AutoFill surface**, and **the sync path**.

We assume from the outset that the attacker already has your vault file -- not as a worst case, but as the default case -- and design backwards from there.

> **[How PanicVault Is Built: Our Secure Development Lifecycle](/engineering/secure-development-lifecycle/)**
> The full threat model in plain language, an explanation of what a threat model even *is*, and how each phase of our lifecycle maps onto the NIST Secure Software Development Framework (SP 800-218).

## The Engineering Deep Dives

### Review and verification

- **[Continuous AI Security Audit: Every Commit Reviewed by Fable 5](/engineering/ai-code-audit-fable-5/)** -- what an adversarial AI reviewer catches that linters and tired humans miss, why "on every commit" beats "once a year," and an honest account of the limits: it is a high-recall reviewer that never gets tired, not a proof and not a substitute for design review.
- **[Static Analysis and the Quality Gate: SonarQube on Every Build](/engineering/static-analysis-sonarqube/)** -- SAST versus DAST, taint analysis from source to sink (the vault file *is* untrusted input), bugs versus vulnerabilities versus security hotspots versus code smells, the technical debt ratio, and what a blocking gate actually means.
- **[Why We Hold 100% Test Coverage -- and What It Really Proves](/engineering/hundred-percent-test-coverage/)** -- line coverage, branch coverage, MC-DC, the reason a 90% target always leaves the *scariest* 10% untested, known-answer vectors from the standards, and how to think like a mutation tester.

### Cryptography and platform

- **[Cryptographic Engineering: How We Handle Keys and Secrets](/engineering/cryptographic-engineering/)** -- AES-256 versus ChaCha20 as a real tradeoff, Argon2d and Argon2id parameters under RFC 9106, why memory-hard key derivation defeats GPUs and ASICs, key lifetime and why a compiler is allowed to delete your zeroization, constant-time comparison, the Secure Enclave and what biometric unlock *actually* does, and the rule that we implement no custom cryptography.
- **[Supply Chain Security: Trusting the Code We Did Not Write](/engineering/supply-chain-security/)** -- a minimal dependency footprint as the primary control, pinned lockfiles, where reproducible builds honestly end on a signed Apple platform, the SLSA build model, code signing and notarization, and why an app with no network egress has a smaller blast radius.
- **[Platform Hardening on iOS and macOS](/engineering/ios-app-hardening/)** -- Data Protection classes and keychain accessibility, the app sandbox and what it does *not* isolate, the backgrounded-app screenshot nobody thinks about, clipboard expiry, real auto-lock (the key is wiped, not the view), AutoFill extension isolation, and a candid section on why jailbreak detection is a speed bump rather than a wall.

## Standards We Align With

We map our practices to public frameworks because a shared vocabulary is how you find your own gaps. These are **alignments, not certifications** -- no external body has audited or certified PanicVault, and we will not imply otherwise:

- **NIST SSDF (SP 800-218)** -- the lifecycle structure: Prepare the Organization, Protect the Software, Produce Well-Secured Software, Respond to Vulnerabilities.
- **OWASP MASVS and MASTG** -- the mobile security verification standard and its testing guide, used as our design and verification checklist for storage, crypto, authentication, platform interaction, code quality, and resilience.
- **OWASP ASVS** and the **CWE Top 25** -- the vulnerability taxonomy our static analysis rules map onto.
- **SLSA** -- the build provenance model our CI pipeline is built around.
- **RFC 9106** (Argon2), **RFC 6238** (TOTP), and **W3C WebAuthn** (passkeys) -- the specifications we implement against, with their published test vectors used as known-answer tests.
- **NIST SP 800-63B** -- the digital identity guidelines that inform how we think about [password entropy](/password-security/password-entropy/) and authentication.

## What We Do Not Claim

A security page is judged as much by what it refuses to say as by what it asserts. So, plainly: PanicVault has no SOC 2 report, no ISO 27001 certificate, no FIPS validation, no third-party penetration test, and no bug bounty programme. We have not commissioned an external audit firm. If you see a password manager claiming those things, ask to read the actual report -- and note the date on it, because a point-in-time audit describes a snapshot of a codebase that stopped existing the moment the next commit merged.

What we have instead is a process that runs on **every single change**: an adversarial security review of every diff, a static analysis gate that cannot be overridden, and a test suite that covers every line and every branch. And what we have that no certificate can give you is the **[open KDBX format](/keepass/)** -- your vault is a standard file that KeePassXC and a dozen independent implementations can open, which means your security does not ultimately rest on trusting us at all. You can verify, and you can leave.

That is the deal we think a password manager should offer.

## Where to Go Next

If you want the product's security properties from the user's side rather than the engineer's, start with [zero-knowledge encryption](/password-managers/zero-knowledge-encryption/), [how KeePass database encryption works](/keepass/database-encryption/), or [the Secure Enclave](/apple/secure-enclave/). If you are weighing whether to trust any password manager at all, [that question deserves a direct answer](/password-managers/are-password-managers-safe/) -- and the honest one starts with knowing how the software was built.
