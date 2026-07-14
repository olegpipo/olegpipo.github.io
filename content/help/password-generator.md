---
title: "Password Generator"
description: "Generate strong random passwords or EFF wordlist passphrases in PanicVault, check their strength, and use them directly in your entries."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Passwords & Entries"
weight: 80
---

PanicVault includes a built-in password generator that creates strong, random passwords using a cryptographically secure random number generator. This page covers the two generation modes, the strength meter, and how to put a generated password to work in an entry.

You can access the generator from:

- The toolbar in the entry list (key icon, or **Cmd+G** on Mac)
- The dice icon in the password field when creating or editing an entry

## Character-Based Passwords

Generate passwords made of random characters. You can configure:

- **Length** -- from 8 to 128 characters (default: 20)
- **Character sets** -- toggle any combination of:
  - Uppercase letters (A-Z)
  - Lowercase letters (a-z)
  - Digits (0-9)
  - Symbols (!@#$%^&* and more)

At least one character set must be enabled.

## Passphrase Generation

Generate passwords made of random words from the EFF wordlist (a curated list of common English words). Passphrases are easier to remember while still being very secure.

You can configure:

- **Word count** -- from 3 to 10 words (default: 5)
- **Delimiter** -- the separator between words:
  - Hyphen (-)
  - Space
  - Dot (.)
  - Underscore (_)

{{< callout type="tip" >}}
A 5-word passphrase with the EFF wordlist provides approximately 64 bits of entropy -- equivalent to a random 12-character password with mixed character types.
{{< /callout >}}

## Password Strength Meter

Every generated password (and every password you type in an entry form) shows a strength meter with four levels:

- **Weak** -- less than 40 bits of entropy
- **Fair** -- 40 to 59 bits of entropy
- **Strong** -- 60 to 79 bits of entropy
- **Excellent** -- 80 or more bits of entropy

## Copying and Using Generated Passwords

- Tap **Copy** to copy the password to your clipboard
- Tap **Regenerate** to create a new password with the same settings
- When accessed from an entry form, tap **Use Password** to fill the password field

The generator keeps a history of your last 10 generated passwords so you can go back and copy a previous one if needed.

For how the password field fits into the rest of an entry, see [Entries (Passwords)](/help/entries/). Clipboard behavior after copying is covered in [Security & Settings](/help/security-and-settings/).
