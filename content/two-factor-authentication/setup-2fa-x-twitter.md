---
title: "Set Up 2FA on X / Twitter (2026)"
description: "Step-by-step guide to enabling two-factor authentication on X (Twitter) using an authenticator app or security key after SMS was removed from free accounts."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Two-Factor Authentication"
faq:
  - q: "Did Twitter remove SMS 2FA?"
    a: "Yes. In February 2023, X (then Twitter) removed SMS-based 2FA for free accounts. Only X Premium (formerly Twitter Blue) subscribers can use SMS as a second factor. Free users must use an authenticator app or security key."
  - q: "What is the best 2FA method for X?"
    a: "An authenticator app using TOTP is the best option for most users. It is free, works offline, and is more secure than SMS. Security keys offer even stronger protection but require a physical device."
  - q: "Can I use Google Authenticator with X?"
    a: "Yes. X supports standard TOTP, so any authenticator app works, including Google Authenticator, Microsoft Authenticator, Authy, and password managers like PanicVault that have built-in TOTP support."
  - q: "What happens if I lose my authenticator app for X?"
    a: "Use the single-use backup code that X provides during 2FA setup. If you don't have the backup code, you will need to go through X's account recovery process, which can be difficult and slow."
  - q: "Is 2FA on X free?"
    a: "Authenticator app and security key 2FA are free for all X users. SMS-based 2FA requires an X Premium subscription."
---

X (formerly Twitter) occupies a unique position in the 2FA landscape. In February 2023, the platform made the controversial decision to remove SMS-based two-factor authentication from free accounts, restricting it to X Premium subscribers only. This left millions of users who had relied on SMS as their only second factor suddenly unprotected -- and forced anyone who wants 2FA on X to use an authenticator app or a security key.

The silver lining of this policy change is that it pushed users toward stronger authentication methods. SMS was always the weakest form of 2FA, vulnerable to SIM swapping and interception. By making TOTP the default free option, X inadvertently improved the security posture of users who bothered to re-enable 2FA after the change. If you have not yet set up app-based 2FA on your X account, this guide walks through the process step by step, as described in our [complete guide to two-factor authentication](/two-factor-authentication/).

## 2FA Options Available on X

X currently offers these second-factor methods:

**Authenticator app (TOTP)** is available to all users for free. X supports standard TOTP, so any compatible authenticator app or password manager works. This is the recommended method for the vast majority of users.

**Security keys** are also available to all users for free. X supports FIDO2/WebAuthn hardware security keys like YubiKey and Google Titan. Security keys provide the strongest phishing resistance because they cryptographically verify the website's identity during authentication. For a detailed comparison, see our guide on [hardware keys vs. TOTP](/two-factor-authentication/hardware-keys-vs-totp/).

**SMS text messages** are restricted to X Premium subscribers. Even if you pay for Premium, SMS is still the weakest 2FA method due to [SIM swapping vulnerabilities](/two-factor-authentication/sms-being-phased-out/). If you are a Premium subscriber, use an authenticator app instead.

The absence of SMS for free users is actually a security advantage -- it removes the temptation to use the weakest option and encourages adoption of TOTP or security keys.

## Step-by-Step Setup on the Web

To enable TOTP-based 2FA on X using a desktop browser:

1. Open [x.com](https://x.com) in your browser and sign in.
2. Click **More** in the left sidebar (the three-dot icon), then click **Settings and Support** > **Settings and privacy**.
3. Click **Security and account access** in the left sidebar.
4. Click **Security**.
5. Click **Two-factor authentication**.
6. You will see three toggle options: Text message, Authentication app, and Security key.
7. Toggle on **Authentication app**.
8. X will ask you to enter your password to confirm your identity.
9. X displays a QR code on screen. Open your authenticator app or password manager and scan this QR code. If you cannot scan, click the link to view the secret key as text and enter it manually.
10. Enter the six-digit verification code that your authenticator is now generating.
11. Click **Confirm**.
12. X displays a single backup code. **This is your only recovery code -- save it immediately.** Unlike services that provide ten codes, X gives you just one. Store it in your password manager or another secure location.

After enabling 2FA, X may prompt you to verify your second factor the next time you sign in from a new device or browser. Test this immediately by signing out and signing back in.

## Step-by-Step Setup on the Mobile App

### On iPhone

1. Open the **X** app.
2. Tap your profile picture in the top-left corner to open the navigation drawer.
3. Tap **Settings and Support** > **Settings and privacy**.
4. Tap **Security and account access** > **Security** > **Two-factor authentication**.
5. Toggle on **Authentication app**.
6. Enter your account password when prompted.
7. X shows a QR code and a "Link app" option. If you are using a password manager on the same device, tap **Link app** and choose your authenticator, or tap **Can't link?** to see the secret key for manual entry.
8. Copy the secret key, switch to your password manager or authenticator app, and add a new entry with this key.
9. Return to X and enter the six-digit code your authenticator generates.
10. Tap **Confirm**.
11. Save the backup code X provides.

### On Android

1. Open the **X** app.
2. Tap your profile picture in the top-left corner.
3. Tap **Settings and Support** > **Settings and privacy**.
4. Tap **Security and account access** > **Security** > **Two-factor authentication**.
5. Toggle on **Authentication app**.
6. Follow the same flow: enter your password, get the setup key, add it to your authenticator, enter the verification code, and save your backup code.

### Adding a Security Key on Mobile

To use a hardware security key with X on your phone:

1. Follow the 2FA path above and toggle on **Security key**.
2. When prompted, insert your USB-C security key into your phone or tap your NFC-enabled key against the back of your device.
3. X registers the key. You can add multiple keys for redundancy.
4. Security keys on mobile work alongside or instead of an authenticator app -- you can have both enabled simultaneously.

## The SMS Removal: What Happened and Why It Matters

In February 2023, X announced that SMS 2FA would be removed for non-paying users within 30 days. The stated rationale was the cost of SMS delivery, but the practical effect was significant:

- Users who had SMS as their only 2FA method had their second factor disabled entirely when the deadline passed.
- Many users did not see the warning or did not act on it, leaving their accounts unprotected.
- The change disproportionately affected less technical users who had been told SMS 2FA was "good enough."

If your X account previously had SMS 2FA and you did not switch to an authenticator app, **your account currently has no second factor.** Check your settings immediately and enable TOTP.

The broader lesson is important: [SMS 2FA is being phased out](/two-factor-authentication/sms-being-phased-out/) across the industry. X was one of the first major platforms to take this step, but others are likely to follow. Switching to TOTP now protects you against both current SMS vulnerabilities and future platform policy changes.

## Choosing TOTP Over SMS (Even for Premium Users)

If you are an X Premium subscriber, you have the option to use SMS for 2FA. Do not use it. Here is why:

**SIM swapping is a real threat on X.** High-profile X accounts -- verified accounts, accounts with large followings, accounts associated with cryptocurrency -- are frequent targets of SIM swapping attacks. An attacker calls your carrier, convinces a representative to transfer your number, and immediately uses it to receive your SMS codes and take over your account.

**TOTP works offline.** Your authenticator generates codes using a stored secret and the current time, with no network dependency. SMS requires cellular service, which can fail during travel, carrier outages, or number changes.

**Portability.** Your TOTP secret can be stored in any compatible authenticator app or password manager. It is not tied to your phone number, your carrier, or X's platform decisions.

Even services that still offer SMS as an option are increasingly recommending against it. For more on why TOTP is the better choice, see our detailed comparison of [TOTP vs. SMS](/two-factor-authentication/totp-vs-sms/).

## Saving Your Backup Code

X provides only a single backup code during 2FA setup, which makes protecting it especially important:

1. When X displays your backup code after enabling 2FA, copy it immediately.
2. Store the code in the notes field of your X account entry in your password manager.
3. Consider also printing it and storing the printed copy in a physically secure location.
4. If you need a new backup code later, go to **Settings** > **Security and account access** > **Security** > **Two-factor authentication** > **Backup code** and generate a fresh one. The old code is invalidated.

Because X gives you only one code (not ten like most services), losing it means your only fallback is X's account recovery process -- which has been notoriously slow and unreliable. Treat this single code as critically important.

For broader advice on managing recovery codes across all your accounts, see our [recovery codes guide](/two-factor-authentication/recovery-codes/).

## Using a Password Manager for TOTP

Storing your X 2FA secret in a password manager is the most practical approach for several reasons:

**Your backup code is safe.** With the secret stored in your password manager, losing your phone does not mean losing access. Your TOTP secret lives in your encrypted vault, accessible from any device where your vault is available.

**One fewer app.** Instead of maintaining a separate authenticator app just for X (and every other TOTP-enabled service), your password manager handles both credential storage and code generation.

**Seamless sign-in.** When you need to sign into X on a new device, your password manager provides your password, TOTP code, and backup code from a single entry.

[PanicVault](https://panicvault.com) is a KeePass-compatible password manager for Apple devices that handles TOTP natively. During X's 2FA setup, scan the QR code or enter the secret key into the OTP field of your X entry in PanicVault. The app stores the secret in the standard KeePass OTP field within your encrypted `.kdbx` database, generates codes automatically, and backs up the secret as part of your regular vault backup.

Because PanicVault uses the open KeePass format, your X TOTP secret is portable. You can access the same database from [KeePassXC on a desktop](/two-factor-authentication/best-authenticator-apps/) or KeePassDX on Android. No vendor lock-in, no proprietary format, no risk of losing your codes if an app shuts down.

For a complete guide to this workflow, see our articles on [using a password manager as your authenticator](/two-factor-authentication/password-manager-as-authenticator/) and [moving existing codes to a password manager](/two-factor-authentication/move-codes-to-password-manager/).

## Additional X Security Recommendations

Beyond 2FA, these settings strengthen your X account security:

**Use a strong, unique password.** Generate a random password with your password manager and do not reuse it on any other service.

**Review connected apps.** Go to **Settings** > **Security and account access** > **Apps and sessions** > **Connected apps** and revoke access for any third-party apps you no longer use. Each connected app is a potential entry point.

**Check active sessions.** Under **Apps and sessions** > **Sessions**, review all devices currently signed into your account. Log out of any you do not recognize.

**Disable password reset by email alone.** Under **Security**, ensure that additional verification is required for password resets. This prevents an attacker who has compromised your email from easily resetting your X password.

These measures, combined with TOTP-based 2FA, create layered security that makes your X account resilient to the most common attack patterns.

## Related Articles

- [What Is Two-Factor Authentication?](/two-factor-authentication/what-is-2fa/) -- Understand the fundamentals of 2FA and why every account needs it.
- [SMS 2FA Is Being Phased Out](/two-factor-authentication/sms-being-phased-out/) -- Why platforms like X are moving away from text message verification.
- [TOTP vs. SMS: Which 2FA Method Is Safer?](/two-factor-authentication/totp-vs-sms/) -- The security comparison that explains X's decision.
- [Using a Password Manager as Your Authenticator](/two-factor-authentication/password-manager-as-authenticator/) -- The simplest way to manage all your TOTP codes.
- [How to Set Up 2FA on Every Major Service](/two-factor-authentication/setup-on-every-service/) -- Enable 2FA on all your important accounts in one session.
