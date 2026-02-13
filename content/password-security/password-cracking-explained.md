---
title: "How Password Cracking Works: Brute Force, Dictionary, and Rainbow Tables"
description: "Learn how attackers crack passwords using brute force, dictionary attacks, and rainbow tables, plus the defenses that stop them cold."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Password Security"
---

Every password you create will eventually face an adversary. Whether it is a targeted attacker going after your accounts or an automated script chewing through a leaked database, the question is never _if_ your password will be tested -- it is _how long it will hold_. Understanding the methods attackers use to crack passwords is the first step toward building defenses that actually work. If you are looking for a broader foundation, start with our [Password Security](/password-security/) pillar page, which covers the full landscape of protecting your credentials.

This guide walks through the major password cracking techniques, how modern hardware has changed the math, and what defenders -- including tools like PanicVault -- do to neutralize each method.

## What Attackers Are Really Cracking

Before diving into techniques, it helps to understand what attackers work with. Reputable services never store your password in plain text. Instead, they store a **hash** -- the output of a one-way mathematical function. When you type your password, the system hashes your input and compares it to the stored hash. If they match, you are in.

When a [data breach](/data-breaches/) exposes a database, attackers get these hashes. Their job is to find the original password that produces each hash. They do this by trying candidate passwords, hashing each one, and checking for matches. The speed at which they can do this depends on the hashing algorithm, the hardware, and the cracking technique.

## Brute Force Attacks

Brute force is the most straightforward method: try every possible combination of characters until one produces the correct hash. Start with `a`, then `b`, then `c`, all the way through every character in the set. Then move to `aa`, `ab`, `ac`, and so on.

The math is simple. If your password uses lowercase letters only (26 characters), the number of possible passwords of length _n_ is 26^n. Add uppercase, digits, and symbols, and the character set grows to roughly 95 printable ASCII characters. Now you are looking at 95^n possibilities.

### Modern Cracking Speeds

This is where theory meets reality. A single modern GPU can compute billions of hashes per second against fast algorithms like MD5 or SHA-1. A dedicated cracking rig with multiple GPUs pushes that into the tens or hundreds of billions. Here is what that means in practice:

| Password Length | Character Set | Possible Combinations | MD5 Crack Time (10B hashes/sec) | SHA-256 Crack Time (5B hashes/sec) |
|---|---|---|---|---|
| 6 characters | Lowercase (26) | 309 million | < 1 second | < 1 second |
| 6 characters | Full ASCII (95) | 735 billion | ~1 minute | ~2.5 minutes |
| 8 characters | Lowercase (26) | 209 billion | ~21 seconds | ~42 seconds |
| 8 characters | Full ASCII (95) | 6.6 quadrillion | ~7.6 days | ~15.3 days |
| 10 characters | Lowercase (26) | 141 trillion | ~3.9 hours | ~7.8 hours |
| 10 characters | Full ASCII (95) | 59.9 quintillion | ~190 years | ~380 years |
| 12 characters | Full ASCII (95) | 540 sextillion | ~1.7 million years | ~3.4 million years |
| 16 characters | Full ASCII (95) | 4.4 x 10^31 | ~140 trillion years | ~280 trillion years |

The takeaway is stark. Short passwords -- anything under 10 characters using a limited character set -- fall in minutes to hours. This is why [password length](/password-security/password-length/) matters more than almost any other factor. Each additional character multiplies the work an attacker must do exponentially.

But pure brute force is also the least efficient method. Attackers almost always start with smarter approaches.

## Dictionary Attacks

A dictionary attack uses a precompiled list of likely passwords instead of trying every possible combination. These lists are not just English dictionaries. They include:

- **Common passwords**: The millions of passwords exposed in previous breaches (123456, password, qwerty, letmein)
- **Leaked credential databases**: Entire dumps from major breaches, containing real passwords real people chose
- **Language-specific wordlists**: Words from every major language
- **Cultural and pop-culture terms**: TV shows, sports teams, band names, game characters

A well-maintained wordlist might contain hundreds of millions of entries. Against fast hashing algorithms, an attacker can test every entry in seconds. If your password is a single common word, a name, or any password that has ever appeared in a breach, it will be found almost instantly.

This is why the advice to create a [strong password](/password-security/strong-password-guide/) emphasizes randomness. Human-chosen passwords are predictable. We pick words that mean something to us, and attackers know it.

## Hybrid and Rule-Based Attacks

Pure dictionary attacks find the low-hanging fruit. Hybrid attacks go further by applying transformation rules to dictionary words:

- **Capitalization**: `password` becomes `Password`, `PASSWORD`, `pAssword`
- **Leet speak substitutions**: `password` becomes `p@ssw0rd`, `p4$$w0rd`
- **Appended numbers**: `password1`, `password123`, `password2026`
- **Prepended or appended symbols**: `!password`, `password!`, `#password#`
- **Reversed strings**: `drowssap`
- **Concatenation**: Two dictionary words joined together, like `soccermonkey`

Tools like Hashcat and John the Ripper ship with sophisticated rule engines that can generate thousands of variants from each base word. A dictionary of 10 million words with 1,000 rules produces 10 billion candidates -- still trivially fast against a weak hash.

This is also why [password complexity rules](/password-security/password-complexity-rules/) that merely require "one uppercase, one number, one symbol" provide less protection than people assume. Attackers have encoded exactly those patterns into their rules. The substitution of `@` for `a` or `3` for `e` adds almost no entropy because it is a predictable transformation.

True [password entropy](/password-security/password-entropy/) comes from genuine randomness, not from human-predictable complexity.

## Rainbow Tables

Rainbow tables represent a different philosophy: **precompute now, crack instantly later**.

A rainbow table is a massive lookup structure that maps hash values back to their original inputs. Instead of hashing candidates during an attack, you build the table once -- spending days or weeks of compute time -- and then every future crack against the same algorithm is essentially a table lookup, taking seconds.

### How Rainbow Tables Work

A full table storing every hash and its corresponding input would require absurd amounts of storage. Rainbow tables use a clever trick called **reduction functions** to compress the data. They store chains of alternating hash and reduction steps. To crack a hash, you apply the reduction functions to see if the hash appears in any chain, then reconstruct the original password from the chain's starting point.

For unsalted MD5, rainbow tables covering all 8-character alphanumeric passwords fit in a few hundred gigabytes. That is well within reach of a consumer hard drive.

### How Salting Defeats Rainbow Tables

A **salt** is a random value added to each password before hashing. Instead of computing `hash(password)`, the system computes `hash(salt + password)`. The salt is stored alongside the hash in the database.

Salting makes rainbow tables useless. A rainbow table built for unsalted hashes cannot match salted hashes because the input is different for every user, even if two users share the same password. An attacker would need to build a separate rainbow table for every possible salt value, which is computationally infeasible.

For a deeper explanation of this defense, see our guide on [password salting](/password-security/password-salt-explained/). Every modern password storage system uses salting. If a service is breached and the hashes are unsalted, that is a sign of negligent security practices.

## GPU-Accelerated Cracking

The shift from CPU-based cracking to GPU-accelerated cracking changed the landscape permanently. GPUs excel at the kind of parallel, repetitive computation that password hashing demands. A single high-end GPU in 2026 can perform:

- **MD5**: ~50 billion hashes per second
- **SHA-1**: ~15 billion hashes per second
- **SHA-256**: ~5 billion hashes per second
- **NTLM (Windows)**: ~100 billion hashes per second

A purpose-built cracking rig with eight GPUs multiplies those numbers accordingly. Cloud computing makes this even more accessible -- an attacker can rent GPU clusters by the hour without any upfront hardware investment.

This raw speed is what makes fast hash algorithms like MD5 and SHA-1 completely unsuitable for password storage. They were designed to be fast, which is exactly the wrong property when you want to slow attackers down.

## Key Derivation Functions: The Real Defense

The answer to GPU-accelerated cracking is **key derivation functions** (KDFs) -- algorithms specifically designed to be slow and resource-intensive. Unlike general-purpose hash functions, KDFs are tuned to make each guess expensive.

### PBKDF2

PBKDF2 (Password-Based Key Derivation Function 2) works by iterating a hash function thousands or hundreds of thousands of times. If each hash takes a fraction of a microsecond but you perform 600,000 iterations, a single guess now takes measurable time. An attacker doing billions of fast hashes per second might only manage a few thousand PBKDF2 guesses per second.

### bcrypt

bcrypt incorporates a cost factor that controls how much computation each hash requires. It also has built-in salting. The cost factor can be increased over time as hardware gets faster, keeping the defense current.

### Argon2

Argon2 is the current gold standard, winner of the Password Hashing Competition in 2015. It is designed to be:

- **CPU-hard**: Requires significant computation
- **Memory-hard**: Requires large amounts of RAM, which neutralizes GPU advantages since GPUs have limited memory per core
- **Parallelism-resistant**: Can be tuned to resist attacks using many cores simultaneously

Argon2 has three variants: Argon2d (data-dependent, maximizes resistance to GPU attacks), Argon2i (data-independent, resistant to side-channel attacks), and Argon2id (a hybrid that provides both protections).

PanicVault uses Argon2 for deriving the encryption key from your master passphrase. This means even if an attacker obtained your encrypted vault file, each guess at your master passphrase would require significant time and memory. Combined with a strong master passphrase, this makes brute-forcing the vault computationally impractical. You can learn more about how this encryption pipeline works in our [KeePass encryption explained](/keepass/encryption-explained/) guide.

## How Real-World Attacks Unfold

In practice, attackers do not choose a single method. They layer techniques in order of efficiency:

1. **Credential stuffing first**: Try username/password pairs from other breaches. No cracking needed -- just reuse.
2. **Dictionary attack**: Run the top million passwords. This catches a surprising percentage of users.
3. **Rule-based hybrid**: Apply common transformation rules to the dictionary. Catches users who think `P@ssw0rd!` is clever.
4. **Targeted brute force**: For high-value targets, attempt brute force on shorter password lengths or specific character sets.
5. **Full brute force**: Only for short passwords or when the target justifies the compute cost.

The first three steps happen quickly -- often in minutes. This is why most password breaches report that a large percentage of hashes are cracked within hours. The passwords that survive are the long, truly random ones.

## What This Means for You

Understanding how password cracking works leads to clear, actionable conclusions:

**Length is your primary defense.** Every character you add to a password exponentially increases the brute force search space. Aim for 16 characters minimum, or use a passphrase of 5 or more random words. Our guide on [password length](/password-security/password-length/) explains the math in detail.

**Randomness defeats dictionary attacks.** If a human brain chose the password, it is probably in a dictionary. Let a password generator create your passwords. PanicVault includes a configurable generator that produces both random strings and diceware-style passphrases.

**Unique passwords prevent credential stuffing.** If every account has a different password, a breach on one site cannot cascade to others. A [password manager](/password-managers/) makes this practical by storing and filling hundreds of unique passwords so you do not have to remember them.

**Modern hashing algorithms buy time.** When services use Argon2, bcrypt, or PBKDF2 with strong parameters, even short passwords survive much longer against cracking attempts. But you should not rely on the service doing the right thing -- many still use fast hashes. Your password strength is the only factor you fully control.

**Salting is non-negotiable.** Any properly implemented system salts its hashes, making precomputed rainbow table attacks worthless. PanicVault's vault files use unique salts for key derivation, ensuring that even identical master passphrases produce different encryption keys.

## The Arms Race Continues

Password cracking is an arms race between attackers and defenders. Hardware gets faster every year. New techniques emerge. But the fundamental math has not changed: a sufficiently long, random password combined with a strong key derivation function remains uncrackable within any practical timeframe.

The tools exist to protect yourself. Use a password manager to generate and store unique, high-entropy passwords for every account. Choose a strong master passphrase. Let the math work in your favor -- because attackers are certainly using math to work against you.
