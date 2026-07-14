---
title: "Why We Hold 100% Test Coverage -- and What It Really Proves"
description: "PanicVault enforces 100% test coverage as a merge requirement. An honest account of what line and branch coverage prove, what they do not, and why the metric is still a serious security control."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "Engineering & Security"
---

PanicVault enforces **100% test coverage as a merge requirement**. Code that is not covered does not ship, and there is no exception process.

Now the part that most vendors leave out: **100% coverage does not mean the code is correct.** It means every line of it was executed at least once while the tests were running. Those are radically different claims, and anyone who tells you otherwise is either confused or selling something.

We hold the metric anyway -- not despite that limitation, but with a clear understanding of it. This article explains what coverage actually measures, why the honest version of the claim is still a powerful security control for a password manager specifically, and how we think about the gap that coverage cannot close.

## What Coverage Measures

### Line coverage

The simplest form. Did this line of code execute during the test run? Instrument the binary, run the suite, count the lines that were hit. 100% line coverage means no line went unexecuted.

It is also the weakest form, and it flatters you. Consider:

```swift
func unlock(with key: SymmetricKey) -> Bool {
    guard verifyHMAC(key) else { return false }
    state = .unlocked
    return true
}
```

A single test that calls `unlock` with a valid key executes every line except the `return false`. Depending on how the instrumentation attributes that early return, you can end up at or near 100% line coverage having never once tested what happens when the HMAC fails -- which is, of course, the only case an attacker cares about.

### Branch coverage

Branch coverage asks the sharper question: for every decision point, was each outcome taken? Every `if` must go both ways. Every `guard` must both pass and fail. Every `switch` case must be entered. Every `try` must both succeed and throw.

This is where the metric starts to earn its keep, because **branch coverage forces you to write the failure tests.** You cannot reach 100% branch coverage on the function above without a test that supplies a key which fails HMAC verification. You cannot reach it on a parser without feeding it malformed input. You cannot reach it on a KDF configuration path without exercising every algorithm option in [the KDBX format](/keepass/kdbx-format-guide/), including the ones nobody uses.

When we say 100% coverage, we mean line *and* branch. Line-only coverage at 100% is a number you can achieve while testing almost nothing that matters.

### Condition coverage and MC-DC

Above branch coverage sit stricter criteria. Condition coverage requires each boolean sub-expression in a compound condition (`if a && b`) to take both values. MC-DC -- modified condition/decision coverage, the criterion the avionics standard DO-178C mandates for life-critical software -- additionally requires demonstrating that each condition *independently* affects the outcome.

We do not claim MC-DC. We name it because it marks where the ladder goes: coverage is not one thing, it is a hierarchy of increasingly demanding questions, and being precise about which rung you are standing on is the difference between an engineering claim and a marketing one.

## What 100% Coverage Does Not Prove

Here is the failure mode, in four lines:

```swift
func testDerivation() throws {
    let key = try deriveKey(password: "hunter2", salt: salt)
    XCTAssertNotNil(key)   // executes everything, proves nothing
}
```

That test runs the entire key derivation path. It contributes to coverage. And it would pass if `deriveKey` returned the SHA-1 of the password, or the password itself, or thirty-two zero bytes. **Coverage measures execution, not assertion.** A test suite of 100% coverage and no meaningful assertions is a suite that proves your code does not crash.

The metric is therefore vulnerable to Goodhart's law -- the moment it becomes a target, you can hit it without achieving the thing it was proxying for. Any honest discussion of coverage has to start by conceding this. Ours does.

## Why We Hold It Anyway

If coverage is that gameable, why enforce it at 100%? Because for a password manager, the *specific* thing it guarantees is unusually valuable.

### There is no unexercised error path

Reread the [threat model](/engineering/secure-development-lifecycle/) and notice where the dangerous code lives. It is not the happy path. Nobody ships a password manager that fails to decrypt a valid vault -- that bug is caught in the first five minutes of use. The bugs that survive to production live in the paths that almost never run: the corrupted vault, the interrupted write, the failed biometric prompt, the sync conflict at 2am, the out-of-memory condition during Argon2, the entry with a malformed attachment.

Those paths are precisely the ones that a 90% coverage target leaves uncovered, because the uncovered 10% is never randomly distributed -- **it is always the hard, scary, awkward-to-test code.** That is the same code where a `catch` block returns `true`, where a fallback silently downgrades a security parameter, where an error message contains a secret. A coverage floor of 100% is a mechanical guarantee that somebody, at some point, wrote a test that made each of those branches run and looked at what happened.

That is the honest claim, and it is worth a great deal: *no error path in PanicVault has ever executed for the first time on a user's device.*

### There is no dead crypto branch

The KDBX 4 format supports multiple ciphers (AES-256, ChaCha20) and multiple key derivation functions (Argon2d, Argon2id, AES-KDF). That is a matrix of configurations, most of which the average user will never select -- and untested configuration branches are how a "compatible" implementation quietly produces a file that another KeePass client cannot open, or worse, produces one that decrypts under weaker parameters than the header advertises. Full branch coverage means every cipher, every KDF, every parameter path in [our encryption implementation](/keepass/database-encryption/) is exercised on every single build.

### Dead code has to die

You cannot reach 100% coverage while carrying unreachable code. So unreachable code gets deleted, permanently, on the day it becomes unreachable. This sounds like housekeeping. It is a security control: dead code is code that nobody tests, nobody reviews attentively, and everyone assumes is doing something. It is also code that can be resurrected by a future refactor into a live path that was never designed for it.

### Refactoring becomes safe, so crypto agility becomes possible

A password manager must be able to change its cryptographic posture -- raise Argon2 memory parameters as devices get faster, add a cipher, adjust a lock state machine -- without fear. Without comprehensive tests, every change to the crypto core is a gamble, so teams stop making them, and the code ossifies at whatever was true in the year it was written. **The test suite is what buys us the freedom to keep the cryptography current.** That is not a testing benefit; it is a long-run security benefit.

### The gate holds the line

Coverage is enforced at the [SonarQube quality gate](/engineering/static-analysis-sonarqube/), on new code, as a blocking condition. A target of 90% erodes -- there is always a reason this one file is special. A floor of 100% cannot erode, because there is no room below it. The bright line is doing real work: the argument "can we skip tests for this bit" has no place to land.

## Thinking Like a Mutation Tester

The intellectually honest way to close the gap between "executed" and "verified" is to ask a mutation tester's question, whether or not a tool is asking it for you:

> If I quietly changed this line, would any test fail?

Flip a `>` to a `>=`. Replace a return value with a constant. Delete the HMAC verification entirely. Halve the Argon2 memory parameter. Remove the `defer` that zeroes the buffer. Return `true` from the failure branch.

If the suite still goes green, the test that "covers" that line is decorative. Coverage told you the line ran; the mutation question tells you whether anything was *watching* while it ran.

So we write tests as if a mutation tester were reading them:

- **Assert on values, not on non-nilness.** A derived key is checked against a published test vector, not against `XCTAssertNotNil`.
- **Known-answer tests from the standards themselves.** RFC 9106 publishes Argon2 test vectors. RFC 6238 publishes TOTP test vectors. AES has NIST known-answer vectors. If our implementation produces the standard's output for the standard's input, we have tested for *correctness*, not merely for execution -- and we have simultaneously tested for interoperability, which is what makes your vault openable by KeePassXC tomorrow.
- **Round-trip and property tests.** Encrypt then decrypt yields the original. Write then read yields the same entries. Any KDBX file we write, we can read; any file KeePassXC writes, we can read.
- **Negative tests as first-class citizens.** A vault with a flipped byte must *fail to open*. A truncated file must fail. A vault with a valid header and a corrupted HMAC must fail before a single entry is parsed. These tests assert on refusal, and refusal is a security property.
- **Every bug becomes a test that fails first.** Reproduce, watch it go red, fix, watch it go green. The regression can never come back silently.

## What Coverage Is, Placed Honestly

Coverage is a **necessary condition, not a sufficient one.** It is a floor, not a ceiling. It proves that every line and every branch of PanicVault has been executed under test -- which is exactly the guarantee that stops an error path from running for the first time on your phone, and exactly the guarantee that makes it safe for us to keep changing the cryptography as the threat landscape moves.

It does not prove the code is correct. Nothing short of formal verification does, and we are not going to pretend otherwise to sell an app. What it does is remove an entire category of excuse, and combine with the other three controls -- [static analysis](/engineering/static-analysis-sonarqube/), [adversarial AI review](/engineering/ai-code-audit-fable-5/), and human judgement -- to make the code that guards your [vault](/keepass/) as boringly, verifiably trustworthy as we know how to make it.

We would rather tell you the true version of what our metrics prove than the flattering one. If you are evaluating a password manager, the vendor's willingness to describe the limits of their own assurances is a signal worth more than most of the numbers on the marketing page -- a theme we return to in [trusting a password manager with your passwords](/password-managers/trust-with-passwords/).

Back to [Engineering and Security Assurance](/engineering/).
