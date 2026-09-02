---
title: "Apple Passwords in iOS 27: Automatic Password Changes Explained"
description: "iOS 27's Passwords app can change weak and breached passwords for you. How it works, which iPhones get it, and whether it replaces a password manager."
date: 2026-09-02
lastmod: 2026-09-02
draft: false
silo: "Apple Ecosystem"
faq:
  - q: "Can the iOS 27 Passwords app change my passwords automatically?"
    a: "Yes. Apple says the Passwords app alerts you to weak or compromised passwords and can update them on your behalf. One tap hands the job to Apple Intelligence and Safari, which open the site, sign in with your saved credentials, work through the password-change flow, generate a strong password, and save it. It needs an Apple Intelligence-capable device and a site the automation can navigate."
  - q: "Which iPhones get automatic password changes in iOS 27?"
    a: "The feature is part of Apple Intelligence, so it needs an Apple Intelligence-capable device. Apple's compatibility footnote lists iPhone 15 Pro, iPhone 15 Pro Max, and all iPhone 16 models and later. Older iPhones can install iOS 27 but do not get Apple Intelligence features. Apple lists the same Passwords capability on its iPadOS 27 and macOS 27 pages."
  - q: "Does the iOS 27 Passwords app replace a password manager?"
    a: "For an all-Apple household with straightforward needs, it closes the biggest gap in Apple's password story: people who see the security warnings and never act on them. It does not add folders, tags, custom fields, secure notes, an encrypted export format, or Windows and Android apps. If you needed a dedicated manager before iOS 27, you still do."
  - q: "Will iOS 27 turn my passwords into passkeys?"
    a: "Apple has not said that. Apple's own description of the feature says Passwords upgrades accounts to strong passwords, not to passkeys, and no published Apple material describes the automatic flow creating a passkey on your behalf. The Passwords app does store and sync passkeys, so you can still create one manually on any site that offers the option."
  - q: "Is it safe to let Apple change my passwords for me?"
    a: "The design is conservative. Apple says the models behind it run on device and on servers using Private Cloud Compute, where personal data is not stored nor made accessible to Apple or anyone else, and the new password lands in end-to-end encrypted iCloud Keychain. The realistic risks are operational -- a change that half-completes on an uncooperative site -- rather than cryptographic."
---

Apple's Passwords app has been able to tell you that a password is weak, reused, or turned up in a data breach since it arrived as a standalone app in iOS 18. What it could never do was fix one. Acting on a warning meant tapping through to the site yourself, hunting for the account settings, and typing a new password -- once for every flagged entry. Most people opened the Security list, saw thirty items, and closed it again.

iOS 27 changes that. At WWDC on June 8, 2026, Apple announced that the Passwords app can now change flagged passwords on your behalf, using Apple Intelligence and Safari to sign in and work through each site's password-change flow. It is the most consequential change to Apple's password manager since it got a home screen icon. It is also, as of early September 2026, not yet something you can actually use, and the details below come from Apple's own WWDC announcement and product pages plus beta reporting rather than from a shipping release.

> **Quick answer**: In iOS 27, iPadOS 27, and macOS 27, the Passwords app can update a weak or compromised password for you -- one tap hands the job to Apple Intelligence and Safari, which open the site, sign in with your saved credentials, run the site's password-change flow, and save the new strong password to iCloud Keychain. It requires an Apple Intelligence-capable device (on iPhone, that means iPhone 15 Pro, iPhone 15 Pro Max, or iPhone 16 and later) and a website the automation can navigate. As of early September 2026 iOS 27 has not shipped publicly, and [9to5Mac](https://9to5mac.com/2026/08/27/ios-27s-passwords-app-can-change-your-passwords-for-you-automatically/) reports the feature has appeared inconsistently across the betas, so it may land in a 27.x update rather than on day one.

## What's New in the iOS 27 Passwords App

Two earlier releases set the stage. iOS 18 pulled password management out of Settings and gave it a standalone app -- the change that made most people realize Apple had been saving their credentials all along. iOS 26 added version history, so a login that has been changed keeps a record of its previous passwords instead of silently overwriting them. Neither release changed what the Security section could do about a bad password: it could point, and nothing more.

The iOS 27 addition is the pointing plus the fixing. On its [iOS 27 page](https://www.apple.com/os/ios/), under the heading "Fix passwords with a tap," Apple describes it in one sentence: "The Passwords app alerts you to weak or compromised passwords and can update them on your behalf without the hassle." The identical sentence appears on Apple's [iPadOS 27](https://www.apple.com/os/ipados/) and [macOS 27](https://www.apple.com/os/macos/) pages, so this is not an iPhone-only feature.

Apple's [WWDC announcement](https://www.apple.com/newsroom/2026/06/apple-intelligence-brings-powerful-ai-capabilities-into-everyday-experiences/) is a little more specific: "Building on its ability to alert users about weak and compromised passwords, Passwords can now automatically fix these for users with just a tap." Apple describes the mechanism as Apple Intelligence and Safari taking action on your behalf -- navigating through websites to sign in and upgrade accounts to strong passwords.

Beyond this, Apple has not announced other changes to the Passwords app for iOS 27. The app's structure, its categories, and its storage model all appear to be unchanged from the version described in our guide to [how the Apple Passwords app works](/apple/how-apple-passwords-works/).

## How Automatic Password Changes Work

The flow starts where it always did: the Security section of the Passwords app, where weak, reused, and compromised credentials are listed. Instead of a link that dumps you on the website, iOS 27 offers to handle the change itself.

From Apple's description and the beta coverage, a single change runs roughly like this. Apple Intelligence opens the site in Safari, signs in using the credentials already stored in iCloud Keychain, finds and completes the site's password-change form, generates a new strong password, and writes it back to your keychain so it syncs to your other devices and autofills as normal. Apple frames the whole thing as an agentic action -- you approve it, and the system does the clicking.

Two details from beta reporting are worth knowing. [MacRumors](https://www.macrumors.com/2026/06/08/apple-passwords-can-now-automatically-fix-passwords-with-agentic-ai/) reports that the process surfaces as a Live Activity while it runs, so the work is visible rather than happening invisibly in the background. And [9to5Mac](https://9to5mac.com/2026/06/11/security-bite-apples-most-impressive-agentic-ai-feature-yet-is-hiding-in-the-passwords-app/), testing the developer beta, reports that the app asks permission to temporarily read one-time verification codes from Messages or Mail when an account has two-factor authentication switched on -- which means the automation can get past an SMS or emailed code, but has nothing to work with on an account whose second factor lives in an authenticator app.

On passkeys, it is worth being precise, because it is easy to assume more than Apple has claimed. Apple's wording is that Passwords upgrades accounts "to strong passwords." Apple has not said that the automatic flow creates a passkey when a site offers one, and no Apple material published so far describes that behavior. The Passwords app stores and syncs passkeys perfectly well, and you can still create one yourself on any site that supports them -- see our guide to [setting up passkeys on Apple devices](/passkeys/setup-apple/) -- but treat "it will convert my logins to passkeys" as an assumption rather than a documented feature.

## Requirements

**iOS 27, iPadOS 27, or macOS 27.** Apple lists the feature on all three product pages. It is not coming to iOS 26.

**An Apple Intelligence-capable device.** The feature sits under "Apple Intelligence in apps" on Apple's pages, and Apple's newsroom post says the capability is powered by Apple Foundation Models running on device and on servers using Private Cloud Compute. Apple's compatibility footnote for Apple Intelligence on iOS 27, iPadOS 27, and macOS 27 covers all iPhone 16 models and later, iPhone 15 Pro and iPhone 15 Pro Max, iPad mini (A17 Pro) and iPad models with M1 and later, and Mac models with M1 and later. An iPhone 14 can run iOS 27; it will not get this.

**A supported device language.** Apple's same footnote requires Siri and device language to be set to one of a specific list -- Chinese (Simplified or Traditional), Danish, Dutch, English, French, German, Italian, Japanese, Korean, Norwegian, Portuguese, Spanish, Swedish, Turkish, or Vietnamese -- and adds that some features may not be available in all regions or languages. Apple has not published a separate availability list for the Passwords feature specifically.

**A site the automation can handle.** Apple has not published a list of supported websites, and its own phrasing is careful about which accounts qualify. Assume good coverage on large, well-maintained services and gaps everywhere else.

## What It Cannot Do

The feature is genuinely useful and genuinely narrow. Several limits follow directly from what it is.

**It only works where the automation can navigate.** A password change requires finding a login form, a settings page, and a change-password form, in that order, on a site that does not object. Older portals, unusual account flows, and aggressive bot detection are the obvious hard cases, and Apple has not committed to any coverage figure.

**Interruptions still exist.** Two-factor prompts that do not arrive by SMS or email, CAPTCHAs, and re-authentication challenges all sit in the middle of the exact path the automation has to walk. 9to5Mac's beta testing already flags authenticator-app 2FA as a case the agent cannot complete.

**It does not widen Apple's ecosystem.** This is still the Apple Passwords app. There is no Android app and no web vault; Windows access remains the limited iCloud Passwords browser extension. If your passwords need to work on a work laptop running Windows or a Linux machine, iOS 27 does not change that -- the reasoning is set out in [why iCloud Keychain is not enough](/apple/icloud-keychain-not-enough/).

**It does not give you a portable file.** The Passwords app still exports to plaintext CSV and nothing else. There is no encrypted export and no export to the KDBX format used by KeePass-compatible apps, so your credentials are easier to fix than they are to move.

**It does not add organization.** No folders, no tags, no custom fields, no standalone secure notes, no file attachments, and no vault lock separate from your device passcode. Every limitation documented in [how the Apple Passwords app works](/apple/how-apple-passwords-works/) survives iOS 27 untouched. Automatic changes make a flat list of two hundred entries healthier; they do not make it navigable.

## Does It Replace a Password Manager?

For a household that lives entirely on Apple hardware, this is the most valuable thing Apple could have shipped. The single biggest failure mode in consumer password security is not that people lack a manager -- it is that they have one, it tells them eleven of their passwords are compromised, and they do nothing. Removing the work from that step is worth more in practice than most feature checkboxes. If Apple Passwords was already enough for you, iOS 27 makes it meaningfully better.

For everyone else, the calculus is unchanged, because the feature does not touch the reasons people leave. Cross-platform access, an encrypted file you own rather than a service you rent, folders and custom fields for a vault that has outgrown a flat list, secure notes and attachments, and a master password independent of your device passcode are all still outside what Apple offers. Our [Apple Passwords versus third-party managers comparison](/apple/apple-passwords-app-comparison/) and the [Bitwarden versus Apple Passwords breakdown](/compare/bitwarden-vs-apple-passwords/) go through those trade-offs in detail.

The two also coexist more comfortably than the framing usually suggests. A common arrangement is a KeePass-format vault as the primary store -- PanicVault is built for exactly this on iPhone, iPad, and Mac, keeping your credentials in a .kdbx file you own while still using Face ID and system-wide AutoFill -- with Apple Passwords kept for the handful of logins that benefit from OS-level integration, or the other way round. iOS 27 makes the Apple side of that arrangement more capable without making the other side unnecessary.

The honest summary: a real improvement to a tool that was already good at the things it is good at, arriving with the same boundaries it always had.

## Related Articles

- [How Apple Passwords App Works](/apple/how-apple-passwords-works/) -- Storage, AutoFill, sync, and the app's limits
- [Is Apple Passwords App Safe?](/apple/is-apple-passwords-safe/) -- The security architecture, examined
- [Apple Passwords vs. Third-Party Managers](/apple/apple-passwords-app-comparison/) -- Where the built-in app falls short
- [Why iCloud Keychain Isn't Enough](/apple/icloud-keychain-not-enough/) -- The cross-platform and portability gaps
- [Setting Up Passkeys on Apple Devices](/passkeys/setup-apple/) -- Creating passkeys yourself, site by site
- [Do Passwords Transfer to a New iPhone?](/apple/new-iphone-upgrade/) -- What moves when you upgrade to an iOS 27 iPhone
