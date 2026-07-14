---
title: "Supply Chain Security: Trusting the Code We Did Not Write"
description: "A minimal dependency footprint, pinned lockfiles, verifiable builds, SLSA-aligned provenance, and Apple code signing and notarization -- how PanicVault limits the blast radius of code it did not write."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "Engineering & Security"
---

You can write flawless code and still ship a compromised application. Every third-party library you link runs *inside your process*, with your permissions, in your address space, next to your keys. It is not a guest in a sandbox. It is you.

For most software this is an acceptable risk, quietly accepted a hundred times over in a typical `package.json`. For a password manager it is close to an existential one: a single malicious dependency does not need to break the encryption, because it is already standing on the other side of it, holding the plaintext.

This article is about how PanicVault handles the code we did not write.

## The Primary Control Is Not Having the Dependency

Every serious supply chain mitigation -- pinning, scanning, provenance, signing -- is a way of managing risk you have already accepted. There is exactly one control that *eliminates* it, and it is refusing to take on the dependency in the first place.

So the first question for any proposed library is not "is it well maintained?" It is: **can we not?** A dependency has to earn its place against the cost of auditing it forever. That means:

- **No analytics SDK.** PanicVault collects no telemetry, so there is no analytics library in the binary. This is normally framed as a privacy decision; it is equally a supply chain decision. Analytics SDKs are large, obfuscated, network-connected, and they update on someone else's schedule. Every one you omit is an entire foreign codebase that is not running next to your master key.
- **No crash reporting SDK.** Third-party crash reporters read process memory by design. That is their job. In a password manager, process memory is the vault.
- **No advertising, attribution, or A/B testing frameworks.** None of them exist in a product with no account and no server.
- **No networking stack**, because there is nothing to talk to. An offline-first application does not need an HTTP client, which means it does not need the transitive tree beneath one.

What remains is a deliberately small set of well-scoped, widely reviewed libraries plus the platform's own cryptographic frameworks -- which are, notably, code Apple already ships and already signs, on a device that already runs it.

A useful way to see this: most of the CVEs that hit mobile apps in any given year land in dependencies the app's authors never read. **The cheapest vulnerability to patch is the one you never imported.**

## Pinning: Lockfiles and the Meaning of "Reproducible"

Every dependency PanicVault does use is **pinned to an exact resolved revision, recorded in a lockfile that is committed to the repository.** Not a version range. Not "^2.1.0", which is an instruction to your build system to run whatever the maintainer publishes next.

The distinction matters more than it sounds. A range means the code you tested and the code you ship can differ, and the difference arrives without a commit, without a review, and without anyone noticing. Pinning makes a dependency change what it should always have been: **a diff.** A visible, reviewable line in a pull request, read by a human and adversarially reviewed by [Fable 5](/engineering/ai-code-audit-fable-5/) like any other change. Dependency bumps are treated as code changes because they are code changes.

An important nuance most write-ups skip: a package manifest is itself *executable code*. Swift Package Manager compiles and runs `Package.swift` to resolve the graph. It sandboxes that evaluation, but the correct posture is to treat manifest execution and build plugins as part of the attack surface, not as configuration. We do not use build plugins that require network or arbitrary filesystem permissions.

## Verifiable Builds and Where Reproducibility Actually Ends

A **reproducible build** means anyone with the same source and toolchain can produce a bit-for-bit identical binary. It is the gold standard, because it lets a third party verify that a shipped binary corresponds to the published source -- that nothing was inserted between the two.

Here is where we have to be honest rather than aspirational, because plenty of vendors claim "reproducible builds" on Apple platforms and the claim does not survive scrutiny. **A signed, notarized iOS or macOS app cannot be bit-for-bit reproduced by a third party**, because signing injects a signature produced with a private key that -- necessarily -- nobody else has, App Store distribution involves re-signing by Apple, and embedded provenance carries timestamps. Anyone telling you otherwise is describing something else.

What is achievable, and what we do:

- **Pin the toolchain.** The Xcode and Swift versions are fixed; a build is not a function of what happened to be installed on someone's laptop.
- **Build only in CI.** Release artifacts are produced by the pipeline from a tagged commit, in a clean environment, never on a developer machine. This is NIST SSDF's PS family -- protect the software, and provide a mechanism for verifying release integrity.
- **Deterministic inputs.** The dependency graph is pinned; the build flags are in source control; the build is a function of the commit.
- **Provenance.** Every release artifact is traceable to the exact commit, the exact toolchain, and the exact dependency set that produced it.

That last bullet is the substance of the **SLSA** framework (Supply-chain Levels for Software Artifacts). SLSA v1.0's Build track defines escalating levels: Level 1 means provenance exists and describes how the artifact was built; Level 2 adds a hosted build platform and signed provenance, so the provenance is authenticated rather than merely asserted; Level 3 adds a hardened build platform where the provenance is resistant to forgery by the build itself. We describe our pipeline as **aligned with the SLSA build model** -- CI-only builds, tagged commits, signed artifacts, recorded provenance. Alignment, not certification: SLSA is a framework we map our practices onto, not a badge anyone has issued us.

## Apple Code Signing and Notarization

The last mile of the supply chain is the one between our build and your device, and on Apple platforms that link is unusually strong -- which is a real advantage of shipping to a curated platform.

**Code signing** binds the binary to our developer identity with a cryptographic signature over its contents. Any modification -- a single flipped byte, an injected dylib, a patched function -- invalidates the signature, and the operating system refuses to run it. The signature is checked at launch, every launch, by code you do not have to trust us about, because it is the OS's.

**Notarization** submits the build to Apple's automated analysis service, which scans it for malicious content and issues a ticket that is stapled to the artifact. Gatekeeper on macOS checks that ticket before first run. Notarization is a malware scan, not a security audit, and we will not dress it up as one -- but it is a real, independent check that we do not control the outcome of.

**Hardened runtime and entitlements** complete the picture: the app declares exactly which capabilities it needs, the declaration is signed, and the kernel enforces it. Entitlements PanicVault does not request are capabilities PanicVault cannot use, even if it is compromised. The full picture of that enforcement is in [platform hardening](/engineering/ios-app-hardening/).

The practical result for you: the binary running on your device is verifiably the one we built, from the commit we tagged, containing the dependencies we pinned -- and the chain from our CI to your home screen is checked by the operating system, not asserted by our marketing.

## Why an Offline App Has a Smaller Blast Radius

Blast radius is the right way to think about supply chain risk. Assume, for the sake of argument, that a dependency in PanicVault is compromised tomorrow. What can it actually accomplish?

It runs in our process, so it can read memory. That is bad -- and it is *why the dependency count is the primary control*, because no amount of sandboxing isolates a library from the process that linked it. This is the part that other vendors' supply chain pages tend to fudge, and we will not: in-process code is inside the trust boundary. Full stop.

But look at what it then has to do with what it stole. To exfiltrate anything, it needs a network egress. PanicVault has **no networking code, no analytics endpoint, no crash reporter, no account server, and no telemetry pipeline** -- so there is no existing, legitimate, expected network traffic for malicious traffic to hide inside. A compromised dependency in a cloud password manager can send your vault to an attacker's server inside a stream of perfectly normal-looking sync and telemetry requests. In an offline app, any network activity at all is anomalous by construction: it would require the app to declare capabilities it does not have, in a signed entitlement set the operating system enforces.

That is the structural argument for [offline-first](/cloud-sync/offline-vs-cloud/), and it is not a slogan. **Architecture that removes a capability beats a policy that promises not to use it.** A promise can be broken by a library you did not write. A missing entitlement cannot.

## Dependency Review in CI

Concretely, on every build:

- The lockfile is verified; an unpinned or drifted dependency fails the build.
- Dependency changes appear in the diff and are reviewed by humans and by Fable 5 like any other change.
- Known-vulnerability data is checked against the resolved dependency set, and a new advisory is a build-breaking finding, not an email.
- [SonarQube's quality gate](/engineering/static-analysis-sonarqube/) blocks the merge on any new security finding in our own code.
- The artifact is built, signed, and its provenance recorded, only from CI, only from a tagged commit.

## And Then the Format Saves You Anyway

Here is the argument that outlives every control on this page.

Suppose all of it fails. Suppose we are compromised, or negligent, or acquired by someone with different values. What is your exposure? Your vault is a **standard KDBX 4 file**, sitting in your own storage, encrypted with standard algorithms, readable by KeePassXC, KeePassDX, and a dozen other independent implementations written by people who have never met us. You are not locked in. You never were.

That is the deepest supply chain control we can offer you, and it is the one that does not depend on you believing anything we say: [the open format](/keepass/) means your data's security does not ultimately rest on our integrity. Every other vendor asks you to trust their process. We ask you to check ours -- and then hand you the door key regardless, which is the whole point of [open standards over proprietary lock-in](/keepass/open-source-vs-proprietary/).

Read next: [platform hardening on iOS and macOS](/engineering/ios-app-hardening/), [cryptographic engineering](/engineering/cryptographic-engineering/), or the [secure development lifecycle](/engineering/secure-development-lifecycle/).

Back to [Engineering and Security Assurance](/engineering/).
