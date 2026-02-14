---
title: "Which Websites Support Passkeys in 2026?"
description: "Regularly updated directory of major websites and services supporting passkey authentication in 2026, organized by category with setup instructions."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Passkeys & Passwordless"
---

One of the most practical questions about passkeys is where you can actually use them. While the technology is mature and supported by every major platform, individual website and service adoption varies significantly. This regularly updated directory, part of our [passkeys and passwordless authentication](/passkeys/) resource, tracks which services support passkey login in 2026 and provides guidance on setting them up.

## The Current State of Passkey Support

Passkey adoption has reached a tipping point. The largest consumer platforms -- Google, Apple, Microsoft, Amazon -- all support passkeys. Major financial services, social media platforms, and e-commerce sites have followed. However, the long tail of smaller websites, enterprise applications, and regional services is still catching up.

As of early 2026, an estimated 20-25 percent of the top 1,000 websites support passkey authentication. That number is growing rapidly, driven by consumer demand, regulatory pressure, and the clear security benefits that passkeys provide. For the latest numbers, see our [passkey adoption statistics](/passkeys/adoption-statistics/).

## Major Services with Passkey Support

### Technology and Cloud Platforms

| Service | Passkey Since | Notes |
|---|---|---|
| **Google** (all services) | 2023 | Full passkey support for login. Works across Gmail, Drive, YouTube, Cloud. |
| **Apple ID** | 2022 | Integrated into iCloud Keychain. Used for App Store, iCloud, and all Apple services. |
| **Microsoft** (personal accounts) | 2023 | Windows Hello integration. Works with Outlook, OneDrive, Xbox. |
| **GitHub** | 2023 | Strong recommendation for developers. Supports device-bound and synced passkeys. |
| **1Password** | 2023 | Uses passkeys for vault unlock in addition to storing them. |
| **Bitwarden** | 2024 | Supports passkey login and passkey storage. |
| **Cloudflare** | 2023 | Dashboard login with passkey support. |
| **Nvidia** | 2024 | Account login for GeForce Experience, cloud gaming. |

### E-Commerce and Retail

| Service | Passkey Since | Notes |
|---|---|---|
| **Amazon** | 2023 | Available in account security settings. Works for Amazon.com and regional variants. |
| **eBay** | 2023 | Early adopter. Passkeys available in account settings. |
| **Best Buy** | 2024 | Online account authentication. |
| **Shopify** (merchant accounts) | 2024 | Admin login for store owners. Customer-facing support varies by store. |
| **Target** | 2024 | Account login for Target.com and the Target app. |
| **Walmart** | 2025 | Added in mid-2025 for online accounts. |

### Financial Services

| Service | Passkey Since | Notes |
|---|---|---|
| **PayPal** | 2023 | One of the earliest adopters. Full passkey login support. |
| **Coinbase** | 2024 | Cryptocurrency exchange with strong passkey integration. |
| **Robinhood** | 2024 | Mobile and web passkey support. |
| **Stripe** (dashboard) | 2024 | For merchant and developer accounts. |

Financial services adoption has been measured because of regulatory requirements around strong customer authentication. Many banks are piloting passkey support internally before rolling out to customers. If your bank does not support passkeys yet, continuing to use a strong password with [two-factor authentication](/two-factor-authentication/) remains the best practice.

### Social Media and Communication

| Service | Passkey Since | Notes |
|---|---|---|
| **WhatsApp** | 2024 | Passkey for app login. |
| **LinkedIn** | 2024 | Professional network passkey login. |
| **X (Twitter)** | 2024 | Account login with passkey. |
| **TikTok** | 2024 | Mobile-first passkey support. |
| **Discord** | 2024 | Desktop and mobile passkey support. |
| **Uber** | 2024 | Account authentication. |

### Travel and Hospitality

| Service | Passkey Since | Notes |
|---|---|---|
| **Kayak** | 2023 | Early passkey adopter. |
| **Booking.com** | 2025 | Account login. |
| **Air France/KLM** | 2025 | Loyalty account login. |
| **Hilton** | 2025 | Hilton Honors account authentication. |

### Productivity and Business

| Service | Passkey Since | Notes |
|---|---|---|
| **Adobe** | 2024 | Creative Cloud and Document Cloud accounts. |
| **Canva** | 2025 | Design platform login. |
| **Notion** | 2025 | Workspace login. |
| **Vercel** | 2024 | Developer platform. |
| **Figma** | 2025 | Design tool authentication. |

### Gaming

| Service | Passkey Since | Notes |
|---|---|---|
| **PlayStation Network** | 2025 | PSN account login. |
| **Nintendo** | 2024 | Nintendo Account login. |
| **Roblox** | 2024 | Account authentication. |

## How to Check If a Site Supports Passkeys

Not every service prominently advertises passkey support. Here are ways to find out:

1. **Check account security settings.** Sign into the service and navigate to Settings > Security or Account > Authentication. Look for terms like "Passkey," "Security key," "Passwordless," or "Sign in with biometrics."

2. **Look for the FIDO/passkey icon.** Some login pages display a passkey icon (a key symbol) alongside the password field.

3. **Use the FIDO Alliance's passkey directory.** The FIDO Alliance maintains a directory of passkey-enabled services at passkeys.directory, which is updated by the community.

4. **Try creating one.** On sites where you suspect support, look in the security settings for an "Add passkey" or "Set up passkey" option.

## Setting Up Passkeys: General Process

While the exact steps differ by service, the general flow is consistent:

1. **Sign in** to the service using your existing password.
2. **Navigate to security settings** (usually under Account > Security or similar).
3. **Find the passkey option** and click "Add passkey" or "Create passkey."
4. **Authenticate** with your device biometrics (Face ID, Touch ID, fingerprint, or device PIN).
5. **Confirm** the passkey creation.

On Apple devices, the passkey is automatically stored in iCloud Keychain and synced to all your devices. For step-by-step instructions specific to iPhone, iPad, and Mac, see our detailed guide to [setting up passkeys on Apple devices](/passkeys/setup-apple/).

## Which Accounts to Prioritize

You do not need to set up passkeys for everything at once. Prioritize based on risk:

**High priority -- set up passkeys immediately:**
- Email (Google, Apple ID, Microsoft) -- your email is the recovery mechanism for almost every other account
- Banking and financial services
- Cloud storage (iCloud, Google Drive, Dropbox)
- Password manager account

**Medium priority -- set up when convenient:**
- Social media accounts
- Shopping sites where you have stored payment information
- Work and productivity tools

**Lower priority -- set up as part of regular maintenance:**
- Entertainment and streaming services
- Forum and community accounts
- Gaming platforms

The principle is simple: the accounts where a breach would cause the most damage should get passkeys first. For a structured approach to organizing your credentials during this transition, see our guide to [managing passwords and passkeys together](/passkeys/managing-both/).

## Notable Services That Do Not Support Passkeys Yet

As of early 2026, several major services still lack passkey support:

- **Most traditional banks** (though many are piloting)
- **Netflix** (passwordless via email link only)
- **Spotify** (no passkey support yet)
- **Many government services** (adoption varies by country)
- **Most healthcare portals**
- **Many small and medium business tools**

The absence of passkey support on these services does not mean you cannot protect them. Strong, unique passwords stored in a [password manager](/password-managers/) combined with [two-factor authentication](/two-factor-authentication/) where available provides solid protection. If you use a KeePass-compatible tool like PanicVault, your passwords are stored in an encrypted, portable [KDBX database](/keepass/) that remains under your control regardless of which authentication method the service supports.

## The Platform Implementation Factor

Where your passkey is stored matters. When you create a passkey on an Apple device, the default storage is iCloud Keychain. On Android, it is Google Password Manager. On Windows, it is Windows Hello.

If you use devices across these platforms, you have several options:

1. **Platform-native storage.** Let each platform store passkeys in its own credential manager. Simple but creates silos.
2. **Third-party password manager.** Use a password manager like 1Password, Bitwarden, or Dashlane that stores passkeys across platforms. More flexible but adds a dependency.
3. **Platform-native with cross-device authentication.** Store passkeys in iCloud Keychain but use cross-device QR code authentication when needed on non-Apple devices.

For a detailed comparison of how each platform handles passkeys, see [Google, Apple, Microsoft passkey implementations compared](/passkeys/google-apple-microsoft/). For practical cross-platform strategies, see [how to sync passkeys across devices](/passkeys/sync-across-devices/).

## What to Expect Going Forward

Passkey adoption follows a predictable pattern. The largest, most technically sophisticated services adopt first. Then mid-size services follow as libraries and frameworks make implementation easier. Finally, small businesses adopt as passkey support becomes standard in off-the-shelf web frameworks and CMS platforms.

Industry analysts project that by the end of 2027, a majority of the top 10,000 websites will support passkeys. For consumers, the practical implication is clear: start using passkeys where you can, keep your password manager for everything else, and check back regularly as support expands.

The [password manager industry is adapting](/passkeys/password-managers-adapting/) to this reality by adding passkey management alongside traditional password storage. Whether you use iCloud Keychain, a third-party manager, or a KeePass-compatible tool, the goal is the same: a unified view of all your credentials, both passwords and passkeys, managed securely from a single interface.

## Related Articles

- [How to Set Up Passkeys on Apple Devices](/passkeys/setup-apple/)
- [Passkey Adoption Statistics: How Fast Is It Moving?](/passkeys/adoption-statistics/)
- [Why You Still Need a Password Manager in a Passkey World](/passkeys/still-need-password-manager/)
- [How to Sync Passkeys Across Devices](/passkeys/sync-across-devices/)
- [Google, Apple, Microsoft Passkey Implementations Compared](/passkeys/google-apple-microsoft/)
