---
title: "How to Use AutoFill on iPhone/iPad With a Password Manager"
description: "Set up AutoFill on iOS and iPadOS with PanicVault or any password manager. Step-by-step configuration, troubleshooting, and tips for reliable autofill."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

AutoFill is what makes a password manager practical. Without it, you are opening an app, searching for a credential, copying the password, switching back to the login screen, and pasting -- a process so tedious that you will abandon it within a week. With AutoFill properly configured, your password manager offers the right credential the moment you tap a login field, and [Face ID or Touch ID](/apple/face-id-touch-id-setup/) fills it in with a glance or a fingerprint. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, shows you exactly how to set this up on iPhone and iPad.

## How AutoFill Works on iOS

Apple's iOS provides a system-level AutoFill framework that password managers plug into via [Credential Provider Extensions](/apple/credential-provider-extensions/). When you tap on a username or password field in Safari, any app, or even system dialogs, iOS asks your configured password manager for matching credentials. The manager checks the URL or app identifier, finds matching entries in your vault, and presents them for you to select.

This is a system-level integration -- it works everywhere, not just in Safari. Any app that uses standard text input fields for login will trigger AutoFill suggestions. Banking apps, social media apps, streaming services, email clients -- they all work.

## Setting Up AutoFill With PanicVault

### Step 1: Install and Configure PanicVault

If you have not already set up PanicVault, see our [first-time setup guide](/guides/first-time-setup/). You need a vault with at least a few entries before AutoFill has anything to offer.

### Step 2: Enable AutoFill in iOS Settings

1. Open the **Settings** app on your iPhone or iPad
2. Scroll down and tap **Passwords**
3. Tap **Password Options**
4. Toggle on **AutoFill Passwords and Passkeys**
5. Under "Use Passwords and Passkeys From," select **PanicVault**
6. You may also see iCloud Keychain and other managers listed -- you can enable multiple providers, but this can cause confusion about which one fills. For the cleanest experience, enable only PanicVault

### Step 3: Verify Face ID / Touch ID Is Enabled

AutoFill uses biometric authentication to unlock your vault when a credential is needed:

1. In PanicVault, go to Settings
2. Ensure Face ID (or Touch ID on older devices) is enabled
3. Test it by closing and reopening PanicVault -- it should prompt for biometric unlock

### Step 4: Test AutoFill

1. Open Safari and navigate to a site where you have a saved login (e.g., amazon.com)
2. Tap the username or email field
3. You should see a suggestion bar above the keyboard showing your PanicVault credential
4. Tap the credential to fill both the username and password fields
5. Face ID or Touch ID will authenticate you before filling

If it works, you are done. If not, see the troubleshooting section below.

## Setting Up AutoFill With Other Password Managers

The process is similar for all password managers that support iOS AutoFill:

### 1Password

1. Settings > Passwords > Password Options > AutoFill Passwords
2. Select 1Password from the provider list
3. Open 1Password and ensure Face ID is enabled in its settings

### Bitwarden

1. Settings > Passwords > Password Options > AutoFill Passwords
2. Select Bitwarden from the provider list
3. Open Bitwarden and enable "Unlock with Face ID" in Settings

### KeePassXC (via Strongbox or Other iOS KeePass Client)

KeePassXC itself is desktop-only. On iOS, you need a KeePass-compatible app like Strongbox or KeePassium that supports the [KDBX format](/keepass/):

1. Install your chosen KeePass-compatible iOS app
2. Open your KDBX database in the app
3. Settings > Passwords > Password Options > AutoFill Passwords
4. Select the app from the provider list

## How AutoFill Matches Credentials to Sites and Apps

Understanding the matching mechanism helps you troubleshoot when AutoFill does not work as expected.

### URL Matching in Safari

When you visit a website in Safari, AutoFill looks at the domain (e.g., `amazon.com`) and searches your vault for entries with matching URLs. This is why the URL field in your password entries matters -- if it is empty or wrong, AutoFill cannot find the right credential.

PanicVault and most managers match on the base domain. So `https://www.amazon.com/gp/sign-in` matches an entry with the URL `https://amazon.com`. Subdomains usually match too -- `login.amazon.com` matches `amazon.com`.

### App Matching

For native apps, iOS uses the app's associated domains. Well-built apps register their domain with Apple's associated domains system, so AutoFill knows that the Amazon app should offer credentials for `amazon.com`. If an app does not implement this correctly, AutoFill may not trigger -- this is the app developer's limitation, not your password manager's.

### Manual Search

When automatic matching fails, you can manually search your vault from the AutoFill interface:

1. Tap the username or password field
2. Tap the key icon in the suggestion bar (or above the keyboard)
3. Select your password manager
4. Search for the entry by name or URL
5. Select the matching entry

## Optimizing Your AutoFill Experience

### Fill the URL Field in Every Entry

Go through your vault and ensure every entry has a URL. AutoFill relies on this for matching. No URL means no automatic suggestion. See our [vault organization guide](/guides/organize-vault/) for best practices on URL formatting.

### Handle Multiple Accounts Per Site

If you have both personal and work accounts for the same site (e.g., two Google accounts), AutoFill will show all matching credentials. You pick the right one from the list. Make sure your entry titles are descriptive enough to tell them apart:

- `Google -- Personal (john@gmail.com)`
- `Google -- Work (john@company.com)`

### Use Strong, Generated Passwords

Since AutoFill fills passwords for you, there is zero benefit to making passwords short or memorable. Use your password manager's generator to create long, random passwords. You will never type them manually. See our guide on [generating strong passwords](/guides/generate-strong-passwords/).

### Keep Your Vault Unlocked (Selectively)

PanicVault can keep your vault unlocked for a configurable period. A 5-minute timeout means you authenticate once and AutoFill works without re-prompting for 5 minutes. Too long a timeout is a security risk if you lose your phone. Too short means constant biometric prompts. Find your comfort level.

## AutoFill for Two-Factor Authentication

PanicVault supports TOTP (Time-based One-Time Password) codes. If you store [2FA codes](/guides/setup-2fa/) in your vault alongside the login credential, AutoFill can fill both the password and the verification code in sequence.

### How It Works

1. AutoFill fills your username and password
2. The site prompts for a verification code
3. iOS detects the verification code field and suggests the TOTP code from PanicVault
4. Tap to fill the code

This eliminates the need for a separate authenticator app for most sites. For a full walkthrough, see our [2FA setup guide](/guides/setup-2fa/).

## Troubleshooting AutoFill Issues

### AutoFill Does Not Appear at All

**Check that AutoFill is enabled:**
Settings > Passwords > Password Options > AutoFill Passwords must be toggled on, and PanicVault must be selected as a provider.

**Check that PanicVault has entries:**
If your vault is empty, there is nothing to suggest. Import your passwords first -- see our [import guide](/guides/import-from-browser/).

**Restart your device:**
Sometimes the credential provider extension needs a restart to register. Power off your iPhone or iPad and turn it back on.

**Reinstall if necessary:**
Rarely, the credential provider extension fails to register properly. Deleting and reinstalling PanicVault can fix this.

### AutoFill Shows But Offers the Wrong Credential

**Check the URL field:**
Open the entry in PanicVault and verify the URL matches the site you are visiting. A common issue is having `http://` when the site uses `https://`, or having an old URL that the site has since changed.

**Check for duplicate entries:**
You may have imported the same credential multiple times. Delete duplicates and keep the most complete entry.

### AutoFill Works in Safari But Not in Apps

**The app may not support AutoFill:**
Some apps, particularly older ones, use custom login screens that do not trigger the AutoFill system. There is no workaround except to copy-paste from your password manager or to contact the app developer.

**Try the manual search method:**
Tap the key icon above the keyboard and manually search for the credential.

### AutoFill Prompt Disappears Too Quickly

This can happen if the app quickly changes focus to another field. Tap back on the username or password field to re-trigger the suggestion. If the problem persists, use the manual search method.

### "No Passwords Available" Message

**Your vault may be locked:**
Open PanicVault and confirm it is unlocked. If it timed out, Face ID or Touch ID should re-authenticate when AutoFill triggers, but sometimes you need to manually open the app first.

**The entry may be missing the URL:**
AutoFill cannot match an entry to a site if there is no URL stored. Open your vault and add the URL.

### AutoFill Fills the Username But Not the Password

This usually happens when the login form has the username and password on separate pages (common on Google, Microsoft, and banking sites). After the username is filled and you advance to the password page, AutoFill should trigger again with the password. If it does not, tap the password field to trigger the suggestion.

## AutoFill on iPad With External Keyboard

When using an iPad with an external keyboard, AutoFill suggestions appear slightly differently:

- Suggestions may appear in a floating window near the text field rather than above the on-screen keyboard
- Keyboard shortcuts may be available (varies by password manager)
- The experience is generally the same, but the visual presentation differs

## Security Considerations

### Is AutoFill Secure?

Yes, when implemented through Apple's credential provider framework, AutoFill is secure:

- Your vault remains encrypted until you authenticate with biometrics
- Credentials are passed directly from the password manager to the text field -- they do not go through the clipboard (which other apps could read)
- The URL matching provides phishing protection -- if you are on a fake site, AutoFill will not suggest credentials for the real one

### Multiple AutoFill Providers

You can enable multiple providers (e.g., PanicVault and iCloud Keychain), but this can cause confusion:

- Both may offer credentials for the same site
- You might save new credentials to the wrong manager
- Keeping track of where each credential lives becomes difficult

For a cleaner experience, choose one primary provider. If you are transitioning from iCloud Keychain to PanicVault, keep both enabled during the migration, then disable iCloud Keychain once all your credentials are in PanicVault.

## Related Articles

- [How to Set Up a Password Manager for the First Time](/guides/first-time-setup/)
- [How to Set Up 2FA Using Your Password Manager](/guides/setup-2fa/)
- [Credential Provider Extensions on Apple Devices](/apple/credential-provider-extensions/)
- [Face ID and Touch ID Setup for Password Managers](/apple/face-id-touch-id-setup/)
- [AutoFill iPhone Guide](/apple/autofill-iphone-guide/)
