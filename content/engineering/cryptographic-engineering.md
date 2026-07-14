---
title: "Cryptographic Engineering: How We Handle Keys and Secrets"
description: "AES-256 vs ChaCha20, Argon2 parameters under RFC 9106, key zeroization, constant-time comparison, the Secure Enclave, and why PanicVault implements no custom cryptography."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "Engineering & Security"
---

Cryptography almost never fails because someone broke the mathematics. AES has stood for over two decades of concentrated public cryptanalysis without a practical break. What fails is everything *around* the mathematics: a nonce reused, a key that outlived its scope, a MAC checked after the plaintext was already handed to the parser, a comparison that returned early and leaked timing, a parameter quietly lowered to make a progress spinner feel snappier.

This article is about that surrounding layer -- the engineering, not the algorithms. It is where a password manager is actually won or lost.

## The First Rule: We Implement No Custom Cryptography

Not a cipher. Not a key derivation function. Not a MAC. Not a random number generator. Not a "small improvement" to any of them.

This rule exists because cryptographic primitives are the one part of software where being *nearly* right is indistinguishable, from the outside, from being right -- and catastrophically different in fact. Wrong code usually crashes. Wrong cryptography produces beautiful, plausible, decryptable ciphertext. There is no test that a naive implementation fails and a correct one passes, which is why this is the area where reviewing your own work is least reliable and standing on vetted implementations is most valuable. It is also NIST SSDF practice PW.4: *reuse existing, well-secured software*.

One honest caveat, because the rule is often stated too broadly. We do implement the **KDBX 4 container format** -- the framing, the header, the ordering of operations, the composition of the primitives. That is not designing cryptography, but it is not nothing either: composition is exactly where implementations go wrong, and it is why the format code carries the heaviest test and review burden in the codebase.

## AES-256 and ChaCha20: A Real Tradeoff

PanicVault supports both ciphers, because [KDBX 4](/keepass/kdbx-format-guide/) supports both and because they fail in different ways.

**AES-256** is a block cipher with a 256-bit key, standardized by NIST in 2001 and used by essentially every government and bank on earth. Its most relevant engineering property in 2026 is that it is implemented *in hardware* on every device we ship to: Apple silicon and A-series chips carry the ARMv8 cryptographic extensions, which execute AES rounds as single instructions. That matters for more than speed. A hardware AES instruction is **constant-time by construction** -- it does not perform data-dependent table lookups, so it cannot leak the key through cache-timing side channels. Software AES implementations built on lookup tables historically could, and did.

**ChaCha20** is a stream cipher designed by Daniel J. Bernstein, built from additions, rotations, and XORs (an "ARX" design). It has no lookup tables at all, which means it is constant-time on *any* CPU, with or without hardware acceleration. On a device without AES instructions, ChaCha20 is both faster and safer than a software AES; on Apple hardware, AES has the edge on throughput. Its structural virtue is diversity: ChaCha20's design shares essentially nothing with AES's, so a hypothetical cryptanalytic advance against one has no bearing on the other.

Neither cipher provides *integrity* on its own -- and this is the point people miss. Encryption without authentication lets an attacker flip bits in your ciphertext and see what happens to your plaintext. KDBX 4 authenticates the vault with **HMAC-SHA-256**, computed over the header and over the encrypted payload in blocks, with a per-block key. The engineering rule that follows is absolute and is enforced by tests that assert on refusal:

> **Verify the MAC before you parse anything.** Not after. Not "in parallel." A vault whose HMAC does not verify is not a damaged vault to be salvaged -- it is a hostile input, and it is rejected before a single entry is touched.

This is encrypt-then-MAC discipline, and it is the difference between a corrupted file and an attack.

## Argon2: Making Guesses Expensive

Your master password is not your encryption key. It is stretched into one by a **key derivation function**, and the KDF is the only thing standing between an attacker who has stolen your vault file and every credential in it. This is the most consequential parameter choice in the entire product.

PanicVault uses **Argon2**, winner of the 2015 Password Hashing Competition and specified in **RFC 9106**. It takes three parameters:

| Parameter | What it controls | Why an attacker hates it |
|---|---|---|
| **Memory cost (m)** | RAM required per guess | Silicon area is expensive; RAM cannot be parallelized away |
| **Time cost (t)** | Number of passes over that memory | Linear cost multiplier per guess |
| **Parallelism (p)** | Lanes computed in parallel | Uses the defender's cores; does not help the attacker's economics |

### Why memory-hardness defeats GPUs and ASICs

A GPU is a machine with thousands of tiny cores and comparatively little fast memory per core. An ASIC is the same bargain taken to its extreme: enormous compute, purchased by stripping out everything general-purpose. Both are devastating against a *fast* hash -- a modern GPU computes billions of SHA-256 hashes per second, which is why any password protected by a bare hash is already lost, as we describe in [password cracking explained](/password-security/password-cracking-explained/).

Argon2 changes the resource being consumed. If a single guess requires 64 MiB of memory that must be filled, read, and rewritten in a data-dependent pattern, then an attacker wanting a thousand parallel guesses needs 64 GiB of *fast* memory -- and memory is the one component you cannot shrink by building a custom chip. Memory-hardness converts the attacker's advantage (raw parallel compute) into their bottleneck (memory bandwidth and area). RFC 9106 exists precisely to codify this.

### Argon2d, Argon2i, Argon2id -- and why the default is what it is

- **Argon2d** uses *data-dependent* memory access. Maximum resistance to GPU cracking, but its memory access pattern depends on the secret, which means it is theoretically vulnerable to an attacker who can *observe memory access on the machine doing the derivation* (a side-channel adversary).
- **Argon2i** uses *data-independent* access: side-channel resistant, but weaker against time-memory tradeoff attacks.
- **Argon2id** is the hybrid -- data-independent for the first half-pass, data-dependent thereafter -- and is what RFC 9106 recommends as the default choice when you are unsure.

PanicVault supports **Argon2d and Argon2id**, matching the KDBX 4 format. The nuance worth stating plainly: in the *local vault file* threat model, the attacker who has your `.kdbx` is running the derivation on their own hardware and has no side channel into yours, which is why Argon2d is a defensible default for KDBX and why KeePass chose it. If you are worried about a hostile process observing your device while you unlock, Argon2id is the right selection -- and it is available in settings. Both are exercised by tests on every build, against the test vectors published in RFC 9106.

### Parameters

RFC 9106 gives two recommended profiles: a high-memory option (2 GiB, t=1, p=4) and a lower-memory option (64 MiB, t=3, p=4) for constrained environments. A mobile password manager lives inside a real constraint here that a server does not: iOS will terminate an app that requests too much memory, and the derivation must complete on the oldest device we support without the OS killing the process mid-unlock.

So we do the unglamorous thing: we default to parameters at the strong end of what every supported device can complete reliably, we expose them so you can raise them, and we write down *why* -- because a vendor that quietly ships a 1-iteration, 16 MiB KDF while advertising "Argon2" has technically told the truth and practically given your vault away. Parameter choice is not a detail. It *is* the security of a stolen vault, and a commit that changes it is treated as a cryptographic change, reviewed as such by [Fable 5](/engineering/ai-code-audit-fable-5/), and tested as such.

Your master password still has to carry its side of the bargain. Argon2 multiplies the cost of each guess; it cannot multiply zero. See [password entropy](/password-security/password-entropy/) for how much entropy your passphrase actually needs, and [password salting](/password-security/password-salt-explained/) for why the random salt in the KDBX header means no precomputed table can ever help an attacker.

## Key Material: Lifetime and Zeroization

Once derived, the key exists in RAM for as long as your vault is unlocked. Three rules govern it.

**Rule 1: Keys never touch types that copy silently.** A Swift `String` is immutable and copy-on-write; you cannot reliably find and overwrite every copy the runtime made. Secrets live in contiguous byte buffers we own, never in `String`, never in a type that might be interned, boxed, or logged.

**Rule 2: Buffers are zeroed deterministically.** A `defer` block wipes the buffer on every exit path, including the throwing ones. And here is the subtlety that separates people who have thought about this from people who have not: **a compiler is entitled to delete a memset whose result is never read.** "Zero this buffer and then never use it again" is, to an optimizer, dead code. This is why zeroization must use a routine the compiler is not permitted to elide (the `memset_s` family and its equivalents) rather than a hand-written loop that a release build will cheerfully optimize away. A wipe that does not happen is worse than no wipe, because you believed it did.

**Rule 3: We are honest that zeroization is best-effort.** In any managed runtime, on any modern OS, you cannot prove no copy of a secret exists anywhere. The memory manager may have moved it. macOS has swap (encrypted, by default, which is exactly why that matters). Memory compression exists. A crash reporter may snapshot the process. What we can do -- and do -- is minimize the *window*: derive late, hold briefly, wipe on lock, wipe on background, wipe on error, and never, under any circumstances, allow key material or a decrypted credential into a log, an analytics event, or a crash report. PanicVault sends no telemetry at all, which conveniently means there is no pipeline for a secret to accidentally escape through.

## Constant-Time Comparison

When PanicVault compares an authentication tag, it does not use `==`.

A normal byte-array comparison returns as soon as it finds a difference. That means it takes measurably longer to reject a tag whose first byte is correct than one whose first byte is wrong. An attacker who can time your rejections can therefore *learn the tag one byte at a time*, turning an infeasible 2^256 search into a few thousand attempts. This is not theoretical; it is one of the best-documented practical attacks on otherwise-correct implementations.

The fix is to compare in constant time: XOR every byte pair, accumulate the differences into a single value, and check that value once at the end. Same result, no early exit, no timing signal. This is not optional and it is not clever; it is table stakes, and it is exactly the kind of thing that a code review looking for "does this compile" will wave through and an [adversarial reviewer](/engineering/ai-code-audit-fable-5/) will catch.

## Randomness: CSPRNG and the Modulo Trap

Every password PanicVault generates, every salt, every nonce comes from the platform's cryptographically secure random number generator -- `SecRandomCopyBytes` on Apple platforms, seeded and maintained by the kernel and, on modern Apple hardware, ultimately fed by the true random number generator inside the Secure Enclave. Never `rand()`. Never a seeded PRNG. Never "random enough."

And then there is the trap that catches so many generators: **modulo bias**. If you want a character from a 62-character alphabet and you take a random byte modulo 62, values 0 through 7 come up slightly more often than the rest, because 256 is not a multiple of 62. The password *looks* random. Its entropy is measurably lower than advertised, and it is skewed in a direction an attacker can exploit. The correct approach is rejection sampling -- discard the values that would bias the result and draw again -- which costs nothing and is trivially unit-testable against a uniformity check. Our [generator](/password-managers/how-generators-work/) does the correct thing, and there is a test that fails if anyone ever changes it to the fast, wrong thing.

## The Secure Enclave: What Biometric Unlock Actually Does

The most persistent misconception about biometric unlock is that your face or fingerprint *decrypts* the vault. It does not, and it cannot -- biometrics are not secrets and they are not stable enough to be keys.

Here is what actually happens. The **Secure Enclave** is a separate coprocessor with its own boot ROM, its own encrypted memory, its own AES engine, and its own true random number generator. It is isolated from the main application processor by design: code running in iOS or macOS -- including ours, including malware -- cannot read what is inside it.

When you enable biometric unlock:

1. The key that protects your vault is stored in the Keychain, wrapped by keys entangled with the Secure Enclave and your device passcode.
2. The item is created with an access control policy requiring biometric authentication, and with a device-only accessibility class -- meaning it never leaves this device, never syncs to iCloud Keychain, and never appears in a backup.
3. When you unlock, Face ID or Touch ID performs the match **inside the Secure Enclave**. The biometric data never leaves it, and PanicVault never sees it. Our app receives one bit of information: authenticated, or not.
4. On success, the Enclave authorizes the *release* of the stored key. The key is what decrypts the vault.

So: **the biometric releases a key; it does not become one.** And your master password is never stored on the device in recoverable form, never transmitted anywhere, and never involved in the biometric path at all.

One more detail that matters and is usually omitted: the access control policy is bound to the *current set* of enrolled biometrics. If someone adds a new fingerprint or re-enrolls a face on your device, the stored key is invalidated by the operating system and the master password is required again. An attacker who compels or coerces an enrollment change gains nothing. This is a genuinely strong property, and it is the reason biometric convenience does not have to mean weaker security -- a tradeoff we examine further in [biometric vault protection](/biometrics/biometric-vault-protection/) and in the deeper dive on [the Secure Enclave](/apple/secure-enclave/).

## Everything Above Is Only as Good as the Code Around It

Choosing AES-256 is easy. Choosing Argon2 is easy. Getting the ordering, the lifetimes, the comparisons, the parameters, the wiping, and the error paths right -- and *keeping* them right across hundreds of commits by people under deadline -- is the actual job. That is why the cryptographic core of PanicVault sits under a [blocking static analysis gate](/engineering/static-analysis-sonarqube/), [100% branch coverage](/engineering/hundred-percent-test-coverage/) with known-answer vectors from the standards themselves, and an [adversarial AI reviewer on every diff](/engineering/ai-code-audit-fable-5/) whose specific job is to notice when one of the rules on this page has quietly stopped being true.

Back to [Engineering and Security Assurance](/engineering/), or read how the whole [secure development lifecycle](/engineering/secure-development-lifecycle/) fits together.
