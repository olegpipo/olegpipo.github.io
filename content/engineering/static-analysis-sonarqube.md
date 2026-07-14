---
title: "Static Analysis and the Quality Gate: SonarQube on Every Build"
description: "SonarQube SAST runs on every PanicVault build with a blocking quality gate. What static analysis catches, how taint tracking works, and why a gate that can be overridden is not a gate."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "Engineering & Security"
---

There is a version of "we run static analysis" that means almost nothing. A tool runs, it produces a report, the report goes into a dashboard, and the dashboard is opened twice a year by someone preparing a slide. The findings accumulate. The number goes up. Nobody is accountable for it, and the build ships regardless.

That is not what happens at PanicVault. **SonarQube runs on every build, and its quality gate is blocking: if the gate fails, the build fails, and the code cannot be merged.** Not a warning. Not a dashboard. A closed door.

This article explains what static analysis actually does, which classes of vulnerability it catches in a codebase like ours, and why the *blocking* part of that sentence is the only part that matters.

## SAST, DAST, and Why the Distinction Matters Here

**SAST** -- static application security testing -- analyzes source code without running it. It parses the code into a syntax tree, builds a control-flow graph and a data-flow graph, and reasons about every path the program could take, including the ones your tests never exercise. Its superpower is coverage of *paths*: it does not care whether you ever executed that error branch, because it can see the branch.

**DAST** -- dynamic application security testing -- probes a *running* application from the outside, throwing malformed input at it and watching what comes back. Its natural home is a web application with HTTP endpoints to poke.

Here is the honest observation about a product like ours: **PanicVault has almost no DAST surface.** There is no server, no API, no login endpoint, no session to hijack. That is not a boast about our testing; it is a consequence of the architecture. An [offline-first password manager](/cloud-sync/offline-vs-cloud/) has no network attack surface to scan, because it does not talk to a network. What it has instead is a *parser* -- and the input to that parser is a file that an attacker may have written. So the dynamic testing that matters for us is not endpoint scanning; it is hostile-input testing of the KDBX parser inside our own test suite, plus the platform's runtime sanitizers (Address Sanitizer, Thread Sanitizer) which catch memory and concurrency faults at execution time.

SAST, meanwhile, does something no test suite can: it reasons about paths nobody thought to test.

## Taint Analysis: The Interesting Part

The single most valuable thing a modern SAST engine does is **taint tracking**. The model is simple:

- A **source** is any point where untrusted data enters the program.
- A **sink** is any point where data does something dangerous.
- A **sanitizer** is a function that makes tainted data safe.
- The engine follows data from every source, through every assignment, function call, and struct field, and reports any path that reaches a sink without passing through a sanitizer.

The classic textbook example is user input reaching a SQL query. But the interesting question for a password manager is: *what are our sources?* People assume an offline app has no untrusted input. It has plenty:

- **The vault file itself.** A `.kdbx` file is bytes from disk. It may have been written by us, by KeePassXC, by a broken sync client -- or by an attacker who handed you a "shared vault." Every field in it is untrusted until the HMAC verifies, and the *structure* is untrusted even then.
- **The XML inside the vault.** KDBX 4 stores its entries as XML inside the encrypted payload. XML parsers are a notorious source of vulnerabilities (XML External Entity attacks, billion-laughs entity expansion), and "the XML is inside an encrypted file" is not a defence when the threat is a vault someone sent you.
- **Attachment filenames.** A KDBX entry can carry a file attachment with an arbitrary name. If that name reaches a filesystem path without sanitization, you have a path traversal: an attachment named `../../../../Library/Preferences/something.plist` writing outside the sandbox on export. This is a real, historically exploited class of bug in file-format handlers, and it is exactly the kind of source-to-sink path taint analysis exists to find.
- **Imported CSV** from another password manager.
- **URL schemes and deep links** -- data handed to us by another app on the device.
- **AutoFill service identifiers** -- the domain or bundle ID the system asks us to match against.
- **The clipboard**, when reading.

Each one of those is a taint source. The engine follows them all, on every build, down every path -- including the paths our tests do not reach and the paths the author did not consider.

## What SonarQube Flags in a Swift Codebase

Beyond taint paths, SonarQube's rule set covers vulnerability classes mapped to public taxonomies -- the **CWE Top 25** and the OWASP catalogues. The ones that bite in a Swift/Objective-C client:

- **Hardcoded secrets and credentials.** Keys, tokens, or test passwords committed to source. Trivially caught, catastrophically bad, and the reason this rule exists at severity "blocker."
- **Weak or obsolete cryptography.** MD5 or SHA-1 used for anything security-relevant, ECB mode, predictable IVs, or a non-cryptographic random number generator (`rand()`, `random()`) used where `SecRandomCopyBytes` is required. The distinction between a *fast* RNG and a *cryptographically secure* one is exactly the kind of thing an engine can enforce mechanically and a human forgets at 6pm.
- **Insecure file handling.** Predictable temp file names, world-readable permissions, missing data-protection attributes.
- **XXE and unsafe deserialization.** External entity resolution left enabled on an XML parser.
- **Path traversal.** As described above.
- **Insecure transport configuration.** App Transport Security exceptions, disabled certificate validation. (We have no network layer to misconfigure -- but a rule that fires the day someone *adds* one is worth having in place before that day.)
- **Unhandled errors and ignored return values.** The birthplace of fail-open behaviour.
- **Dead code and unreachable branches.** Not glamorous, but dead code is an audit liability: it is code nobody tests, nobody reviews, and everybody assumes is doing something.

## Bugs, Vulnerabilities, Hotspots, and Code Smells

SonarQube's taxonomy is worth understanding because people conflate the categories and then dismiss the tool.

- A **bug** is code that is demonstrably wrong -- it will misbehave at runtime. A null dereference. A condition that is always false.
- A **vulnerability** is code that is exploitable -- an attacker can use it. A taint path to a sink.
- A **security hotspot** is *security-sensitive code that requires a human decision*. It is not an assertion that something is wrong; it is the engine saying "this is the kind of code where mistakes are catastrophic -- someone must look at it and confirm." Writing to a temp file is a hotspot. Using a cryptographic API is a hotspot. Hotspots do not get auto-fixed; they get **reviewed**, and the review is recorded.
- A **code smell** is a maintainability problem: a 400-line function, a cyclomatic complexity of 40, a duplicated block. It is not a security finding, and yet it is: complexity is where bugs hide, and a function nobody can hold in their head is a function nobody can review. The correlation between complexity and defect density is one of the most consistently reproduced results in software engineering.

The **technical debt ratio** aggregates the maintainability findings into a single number: the estimated cost to fix everything, divided by the estimated cost of having written the code in the first place. A ratio at or below 5% earns a maintainability rating of A. We hold the gate at A. Not because tidiness is a security control in itself, but because **reviewability is** -- and reviewability is what our [adversarial AI review](/engineering/ai-code-audit-fable-5/) and our human reviewers both depend on.

## What a Blocking Quality Gate Actually Means

A quality gate is a set of pass/fail conditions evaluated on the code you just changed. Ours, applied to new code on every pull request:

- **Zero new bugs. Zero new vulnerabilities.** Not "few." Zero.
- **100% of new security hotspots reviewed.** Every one has a human decision attached.
- **100% coverage on new code.** The [coverage requirement](/engineering/hundred-percent-test-coverage/) is enforced here, at the gate, and it is why it holds.
- **Reliability, security, and maintainability ratings of A.**
- **Duplication below threshold.**

If any condition fails, the CI job exits non-zero. The pull request shows a red check. Branch protection refuses the merge. There is no button that says "merge anyway."

This is the "clean as you code" model, and it is the only version of static analysis that survives contact with a real backlog. Legacy findings in old code are a project you schedule. New findings in new code are a defect you fix *now*, while the author is still holding the context, before the code has ever run on a user's device.

## Why a Gate That Can Be Overridden Is Not a Gate

This is the whole argument, so let us make it plainly.

If a failing gate can be dismissed by a person under deadline pressure, then the gate's real strength is not the strength of its rules. It is the strength of the weakest person's willingness to say no on the worst day of the quarter. That is not a security control. That is a suggestion with a red icon.

Every escape hatch, in practice, becomes the default path. A "temporary" bypass flag gets copied into the next pull request because it worked last time. A rule exclusion added to unblock a release stays in the config for three years. A dashboard nobody is blocked by is a dashboard nobody reads.

So there is no bypass. What there *is* -- and this matters, because a gate with no relief valve gets sabotaged instead of respected -- is a legitimate, visible path for the rare true false positive: **you change the rule configuration, in a commit, in a pull request, reviewed by humans and by Fable 5, permanently visible in the git history.** The waiver becomes part of the diff. It gets argued about. It gets a rationale written next to it.

The difference is not bureaucratic; it is structural. An override is invisible and individual. A configuration change is visible and collective. One decays silently; the other has to be defended.

## The Limits of Static Analysis

Being honest about the ceiling is what makes the claim credible.

SAST does not understand intent. It cannot tell you that the vault should have locked before this line, only that this line dereferences a possibly-nil value. It generates false positives, sometimes tediously. It cannot reason about behaviour that emerges across process boundaries -- and PanicVault has a real one, between the main app and the AutoFill extension. It cannot find a design flaw. It will never tell you that a feature should not exist.

Which is exactly why it is one of four controls and not the only one. SonarQube gives us mechanical, deterministic, unmissable enforcement of the things that *can* be expressed as rules. [Fable 5](/engineering/ai-code-audit-fable-5/) reasons about the things that cannot. [Tests](/engineering/hundred-percent-test-coverage/) prove the code actually runs the way we claim. Humans decide what any of it is for. Each covers the others' blind spot, and the [lifecycle](/engineering/secure-development-lifecycle/) is what holds them together.

The result you get is a vault file in an [open, verifiable format](/keepass/kdbx-format-guide/) -- and code behind it that no engineer, however senior and however rushed, can merge past a red gate.

Back to [Engineering and Security Assurance](/engineering/).
