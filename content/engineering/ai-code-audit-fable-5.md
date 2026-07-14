---
title: "Continuous AI Security Audit: Every Commit Reviewed by Fable 5"
description: "Every PanicVault commit is adversarially reviewed in CI by Fable 5, Anthropic's most advanced model for cybersecurity reasoning. What an AI reviewer catches that linters and humans miss -- and what it honestly does not."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "Engineering & Security"
---

The traditional way to get a security review of a password manager is to hire a firm once a year. They spend two weeks with a snapshot of your code, write a report, and leave. Then you merge four hundred commits over the following twelve months, none of which anyone with a security specialism has looked at closely, and you tell users you have been "security reviewed."

We do something different. **Every commit and every pull request in PanicVault is audited in CI by Fable 5 -- Anthropic's most advanced model for cybersecurity reasoning -- acting as an adversarial reviewer of the diff.** Not a linter pass. A reviewer whose instruction is to read the change the way an attacker would and answer one question: *how do I break this?*

This article explains what that catches, why the cadence matters more than the depth of any single review, and -- because credibility here depends entirely on candour -- exactly what it does not do.

## What "Adversarial Review of the Diff" Means

Fable 5 receives the change under review together with the surrounding code it touches, plus the standing context of what PanicVault is: an offline password manager whose assets are a vault file, a master key in memory, a clipboard, an AutoFill surface, and a sync path. That context is the whole trick. A general-purpose reviewer sees a function that returns a `Bool`. A reviewer that knows the [threat model](/engineering/secure-development-lifecycle/) sees a function that returns a `Bool` *which decides whether a vault is considered unlocked*, and immediately asks what happens when the function throws instead of returning.

It is not summarizing the diff. It is attacking it.

## What an Adversarial AI Reviewer Actually Catches

Static analyzers are pattern matchers over syntax and data flow. They are superb at what they can express and blind to what they cannot. The defects below are the ones that live in the blind spot -- they are all perfectly legal, idiomatic, well-formatted code.

### Logic flaws

A change makes the auto-lock timer reset on "any user interaction." A linter sees a timer being reset. An adversarial reviewer asks which interactions, and notices that a background refresh triggered by the file coordinator counts as an interaction -- so a vault sitting untouched on a synced folder now never locks. The code is correct; the *logic* is wrong. There is no rule in any SAST engine that expresses "this timer can be reset by a non-user event."

### Unsafe state transitions

Password managers are state machines with two states that matter enormously: locked and unlocked. The bugs live in the transitions. A reviewer looks for orderings like: the UI flips to the unlocked state *before* the HMAC over the vault file has been verified; a failed biometric attempt leaves a partially populated in-memory model; a lock triggered during an in-flight save leaves the key alive in a closure that outlives the lock. These are ordering bugs. They cannot be found by looking at any single line, only by reasoning about sequences -- which is exactly what a language model is good at and what a rule engine is not.

### Key-material lifetime bugs

The most valuable finding class in this product. A derived key gets captured by an escaping closure and now outlives the lock event. A `Data` holding key bytes is converted to a Swift `String` for a convenience log line, and Swift strings are immutable and copy-on-write, so the bytes are now somewhere you can no longer reach to zero them. A new error path returns early -- *before* the `defer` block that was supposed to wipe the buffer, because someone moved the `defer` below the guard. Each of these is a two-line diff that a tired human reads straight past. See [cryptographic engineering](/engineering/cryptographic-engineering/) for why these matter so much.

### TOCTOU (time-of-check to time-of-use)

Check that the vault file has the right data-protection attributes; then open it. Between the check and the open, the file can change. Check that a sync replica is newer; then merge it. Check free disk space; then write. TOCTOU windows are invisible unless you are specifically hunting for the gap between a check and the action it authorizes -- and "specifically hunting for it" is a *prompt*, not a rule.

### Incorrect cryptographic usage

Not "you used a broken cipher" -- SonarQube catches that, and we would never ship it. The subtle version: the right primitive, used wrongly. A nonce derived from a counter that resets when the app restarts. A MAC verified *after* the plaintext has already been handed to the parser. A comparison of two authentication tags with `==`, which short-circuits on the first differing byte and therefore leaks timing information. An Argon2 memory parameter that a "performance" commit quietly halves. All of these are semantic misuse of a correct algorithm, and semantic misuse is where real-world crypto fails -- as we explain in the context of [password cracking](/password-security/password-cracking-explained/), the attacker's job is to find the cheapest path, and a downgraded KDF parameter is the cheapest path there is.

### Error paths that leak

This is the classic. The happy path gets all the design attention and all the tests; the error path gets written in thirty seconds at the end of the afternoon. So the error path is where the entry title ends up in an `os_log` string, where the failure message includes the full vault path, where a `catch` block returns `true` because the compiler wanted a value, and where a fallback silently downgrades to a weaker setting instead of refusing to proceed. **Fail closed, never fail open** is easy to say and easy to violate in a one-line `catch`.

## Why "On Every Commit" Beats "Once a Year"

Two arguments, one about coverage and one about cost.

**Coverage.** A point-in-time audit reviews a snapshot. The moment the next commit merges, the audited artifact no longer exists. An annual review, however excellent, examines a fraction of the code that will ever ship and none of the code written after it. Continuous review inverts this: every line that has ever been merged has been read adversarially, in context, at the moment it was introduced. There is no unreviewed remainder.

**Cost.** The defect-cost curve is one of the oldest findings in software engineering: a flaw caught while the author still has the design in their head costs a conversation; the same flaw caught after release costs an incident. Reviewing at merge time is the cheapest possible moment to catch anything -- and, crucially, the author is still there to explain what they were trying to do.

There is a third argument, and it is about human beings. Reviewer attention is a depleting resource. Recall on a 40-file diff at the end of a long day is not the same as recall on a 3-file diff on a Monday morning, and everybody who has ever reviewed code knows it. An automated reviewer has no bad days, no deadline pressure, and no social reluctance to leave the eleventh comment on a colleague's pull request. **Its recall is constant.** That is the actual value proposition -- not that it is smarter than our engineers, but that it is *never tired*, and vulnerabilities are found in exactly the places where tired reviewers stop looking.

## What AI Review Is Not

If this section were absent, you should not believe the rest of the article.

**It is not a proof.** A model reasoning about code is producing a very well-informed argument, not a mathematical guarantee. Formal verification proves properties. AI review finds problems. Those are different activities, and the second one can never be complete: absence of findings is not evidence of absence of flaws.

**It is not deterministic.** Run it twice and the wording changes. It can raise a finding on one pass and not the next. This is why the *blocking* gates in our pipeline are the deterministic ones -- the [SonarQube quality gate](/engineering/static-analysis-sonarqube/) and [100% test coverage](/engineering/hundred-percent-test-coverage/) -- and why Fable 5's findings must be **dispositioned**: fixed, or answered in writing in the pull request with a rationale that a human signs. A finding that is silently ignored is a process failure, and a reviewer whose findings can be silently ignored is decoration.

**It produces false positives.** Of course it does. A reviewer that never raised a false positive would be a reviewer with terrible recall, because the two trade off. We would rather triage a wrong finding than miss a right one, and we tune the process rather than the sensitivity.

**It does not replace design review.** Fable 5 sees a diff. It does not sit in the room when we decide whether a feature should exist at all -- whether to add a sharing mechanism, whether to touch the network, whether a convenience is worth an attack surface. The most consequential security decisions in PanicVault are decisions *not* to build things, and no diff-level reviewer can make them for you. That is threat modelling, and it is human work.

**It does not replace human review.** The model can tell you the code does something dangerous. It cannot tell you the code does something you did not intend, because it does not know what you intended.

## How It Layers With Everything Else

The point of having four reviewers is that they fail differently:

| Control | What it reasons about | Blind to |
|---|---|---|
| SonarQube SAST | Syntax, data flow, taint paths | Intent and multi-step logic |
| Fable 5 adversarial review | Semantics, state, attacker goals | Runtime behaviour; is non-deterministic |
| 100% test coverage | What the code actually *does* when executed | Whether what it does is what you wanted |
| Human review | Intent and design fit | Fatigue, volume, the eleventh comment |

No single one of these is sufficient. A logic flaw slips past the linter; a taint path slips past a tired human; an untested error branch slips past everyone until it runs in production. The overlap is the product.

## Why This Matters More for a Password Manager

Most software fails safely. A bug in a photo app shows the wrong thumbnail. A bug in a password manager can expose every credential you own, and it can do so silently -- there is no error message, no crash, no symptom. The failure mode is *undetectable by the user*, which means the burden of catching it falls entirely on the process that produced the code.

That asymmetry is why we spend a disproportionate amount of engineering effort on review rather than on features, and why an AI reviewer that reads every diff with an attacker's mindset is, in our judgement, one of the highest-leverage security investments available in 2026. It is not magic and it is not a certificate. It is a very good reviewer who reads absolutely everything.

Read next: [Static analysis and the quality gate](/engineering/static-analysis-sonarqube/), [why we hold 100% coverage](/engineering/hundred-percent-test-coverage/), or the full [secure development lifecycle](/engineering/secure-development-lifecycle/). For the broader question of whether password managers deserve your trust at all, see [are password managers safe](/password-managers/are-password-managers-safe/).

Back to [Engineering and Security Assurance](/engineering/).
