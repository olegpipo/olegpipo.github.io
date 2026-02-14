---
title: "How to Generate and Store Strong Passwords"
description: "Learn how to use your password manager's generator for truly strong passwords. Covers configuration, site-specific requirements, and storage best practices."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

The most common mistake in password management is trying to invent passwords yourself. Humans are predictably bad at randomness -- we choose dictionary words, follow patterns, reuse favorites, and make substitutions that attackers have already cataloged. Your password manager's generator solves this completely by producing truly random credentials that no human would create and no attacker can guess. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, shows you how to use your generator effectively and handle the edge cases that trip people up.

## Why Generated Passwords Beat Human Passwords

A human-created password like `Sunshine2024!` feels secure. It has uppercase, lowercase, numbers, and a symbol. It meets most website requirements. But an attacker running a dictionary-based cracking tool would find it in seconds because:

- "Sunshine" is a top-100 password base word
- Appending the current year is the most common pattern
- Adding an exclamation mark at the end is the most common symbol placement
- The total search space, accounting for these patterns, is tiny

A generated password like `k7#mQ9xL4&nPw2$tR8` has no patterns, no dictionary words, and no predictable structure. Every character is independently random. Cracking this password through brute force with current hardware would take longer than the age of the universe.

The key insight: you do not need to remember these passwords. Your password manager remembers them. You authenticate with your [master password](/guides/master-password/) or [Face ID/Touch ID](/apple/face-id-touch-id-setup/), and [AutoFill](/guides/autofill-setup/) handles the rest. There is zero benefit to making your individual account passwords human-readable.

## Configuring Your Password Generator

### PanicVault

1. Open PanicVault and create a new entry (or edit an existing one)
2. Tap the password generator icon (usually a dice or gear icon near the password field)
3. Configure the generator settings:
   - **Length**: Set to 20-24 characters (the default is usually sufficient)
   - **Character types**: Enable uppercase, lowercase, digits, and symbols
   - **Exclude ambiguous characters**: Optional -- removes characters like `l`, `1`, `I`, `O`, `0` that look similar. Useful if you ever need to read the password aloud
4. Generate a password and tap to accept it
5. The password is automatically saved in the entry

### KeePassXC

1. Open KeePassXC and click the password generator (dice icon in the toolbar or within an entry)
2. Set the character length to 20 or more
3. Select character groups: A-Z, a-z, 0-9, special characters
4. Optionally enable "Extended ASCII" for even more character options
5. Click Generate and copy or apply the result

### 1Password and Bitwarden

Both offer inline generators when creating or editing entries. Settings include length, character types, and the option to generate passphrases (multiple random words) instead of random characters.

## What Length Should You Use?

### The Short Answer

20 characters for most accounts. 16 characters as a minimum. 24+ characters when a site allows it and you want extra margin.

### The Math

Password entropy (randomness) scales with length. For a character set of 95 printable ASCII characters:

- 8 characters: ~52 bits of entropy (crackable)
- 12 characters: ~79 bits (strong for now)
- 16 characters: ~105 bits (very strong)
- 20 characters: ~131 bits (far beyond what any current or foreseeable technology can crack)
- 24 characters: ~157 bits (absurdly strong)

There is no practical difference in security between 20 and 24 characters -- both are effectively uncrackable. But longer costs nothing (your password manager fills it automatically), so there is no reason to be conservative.

### When Shorter Is Necessary

Some sites impose maximum length limits. Common caps:

- 16 characters: Many banks and financial institutions
- 20 characters: Some older systems
- 128 characters: Enterprise platforms

When a site caps your length, use the maximum it allows. Add a note to the vault entry recording the restriction so you know why this password is shorter than your standard.

## Character Types: What to Include

### The Ideal Password Includes

- **Uppercase letters** (A-Z): 26 characters
- **Lowercase letters** (a-z): 26 characters
- **Digits** (0-9): 10 characters
- **Special characters** (!@#$%^&*): 20-30 characters depending on which set

Together, these give you 90+ possible characters per position, maximizing entropy per character.

### When to Exclude Character Types

Some sites have frustrating restrictions:

- **"No special characters"**: Generate using only letters and digits. Compensate by increasing length to 24+
- **"Only these special characters"**: Customize your generator to use only the allowed symbols
- **"Must include at least one of each type"**: Most generators produce at least one of each naturally, but check. If your generator creates a password without a digit, regenerate until the requirement is met
- **"No spaces"**: Most generators do not include spaces by default, but check if yours does

### Passphrases vs. Random Characters

Your password manager may offer both:

- **Random characters**: `k7#mQ9xL4&nPw2$t` -- Maximum entropy per character. Ideal for all machine-filled passwords.
- **Passphrases**: `marble-kitchen-voltage-planet-anchor` -- Lower entropy per character but much easier to type manually. Ideal for your [master password](/guides/master-password/) and for the rare cases where you must type a password by hand.

For accounts where AutoFill handles entry, always choose random characters. For your master password and any credential you might need to type on a device without your password manager, use a passphrase.

## Generating Passwords for Specific Scenarios

### Banking and Financial Sites

Banks often have the most restrictive password policies. Common constraints:

- Maximum 16-20 characters
- Limited special character set (often only `!@#$%`)
- Case-insensitive (treating `A` and `a` as the same)
- No spaces

Generate within their constraints and compensate with maximum allowed length. Always enable [2FA](/guides/setup-2fa/) on financial accounts -- the password is only one layer.

### Wi-Fi Networks

Your home Wi-Fi password should be generated and strong (20+ characters), but you will need to type it when connecting new devices. Options:

- Generate a passphrase (4-5 random words, easy to type)
- Store it in your vault and copy it when needed
- Use your phone to display the password from your vault while typing it on the new device

### App-Specific Passwords

Some services (notably Apple) create app-specific passwords for third-party email clients and other tools. These are usually generated by the service itself and should be stored in your vault under the main account entry (in the notes field or as a separate entry linked to the main one).

### Temporary and Disposable Passwords

For throwaway accounts (one-time registrations, free trial signups), still use generated passwords. It costs nothing, and you avoid accidentally creating a credential that links to a real account via password reuse.

## Storing Generated Passwords

### Let AutoFill Capture Them

When you create a new account:

1. Navigate to the signup page
2. Fill in your username/email
3. Use your password manager's generator to create the password
4. The manager creates a new vault entry automatically
5. Complete the registration

This is the ideal flow. The password goes directly from the generator into your vault and into the signup form. You never see it, never type it, never need to remember it.

### When Manual Storage Is Needed

Sometimes AutoFill does not trigger (unusual signup flows, native apps, etc.):

1. Open PanicVault and create a new entry manually
2. Use the built-in generator for the password
3. Copy the password and paste it into the signup form
4. Verify the entry is saved with the correct URL, username, and password

### Do Not Store Passwords Elsewhere

Once your password manager is set up, it should be the single source of truth for all credentials. Do not also save passwords in:

- Browser password managers (disable browser save prompts -- see our [import guide](/guides/import-from-browser/))
- Text files or documents
- Email drafts
- Notes apps
- Physical notebooks (except your [master password](/guides/master-password/) emergency backup)

Multiple storage locations create sync problems and increase the attack surface.

## Handling Password Changes

### When Sites Force a Change

Some sites require periodic password changes. When prompted:

1. Use your password manager's generator for the new password
2. Do not iterate on the old password (e.g., changing `Password1` to `Password2`) -- generate a completely new random string
3. Save the new password in your vault, replacing the old one
4. Verify the new password works by logging out and back in

### When You Voluntarily Change a Password

During a [password audit](/guides/audit-passwords/), you will change weak or reused passwords:

1. Log into the account
2. Navigate to the password change page
3. Enter the old password (let AutoFill handle this)
4. Generate a new password with your manager
5. Save the update
6. Your vault entry is updated automatically (or update it manually)

### Password History

PanicVault and KeePassXC maintain password history for each entry within the [KDBX format](/keepass/). If a password change goes wrong and you need to revert, you can find the previous password in the entry's history. This is a safety net, not a daily feature.

## Troubleshooting Generator Issues

### "The Generated Password Was Rejected by the Site"

The site likely has a restriction your generator did not account for. Common fixes:

- Reduce length to the site's maximum
- Remove special characters or limit them to the site's allowed set
- Ensure at least one uppercase, one lowercase, one digit, and one symbol are included
- Remove spaces if the site does not allow them

### "I Generated a Password But Forgot to Save It"

If you used the generated password to create an account but did not save it in your vault:

1. Check if AutoFill captured it anyway (open your vault and search for the site)
2. If not, use the site's password reset flow to create a new password
3. This time, make sure the new password is saved in your vault

### "AutoFill Is Suggesting Old Passwords After a Change"

Your vault may still have the old password. Open the entry and verify the password matches the current one. If you see the old password, update it manually. Also check if the old password is saved in your browser -- disable browser password saving to prevent this.

## Best Practices Summary

1. **Always use the generator** -- Never create passwords from your imagination
2. **Default to 20+ characters** -- Longer costs nothing and provides margin
3. **Include all character types** -- Unless the site prohibits some
4. **Use passphrases for passwords you must type** -- Master password, Wi-Fi, etc.
5. **Let AutoFill handle entry and retrieval** -- You should rarely see your passwords
6. **Store everything in one place** -- Your password manager is the single source of truth
7. **Enable 2FA where possible** -- Even the strongest password benefits from a second factor

Your password manager's generator is not just a convenience feature -- it is the foundation of your security. Every password it creates is one that no attacker will ever guess.

## Related Articles

- [How to Create a Secure Master Password You'll Remember](/guides/master-password/)
- [How to Audit Your Existing Passwords](/guides/audit-passwords/)
- [How to Use AutoFill on iPhone/iPad With a Password Manager](/guides/autofill-setup/)
- [How to Organize Your Password Vault](/guides/organize-vault/)
- [KeePass Encryption Explained](/keepass/encryption-explained/)
