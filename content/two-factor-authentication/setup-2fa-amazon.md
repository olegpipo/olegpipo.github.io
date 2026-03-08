---
title: "Set Up 2FA on Amazon (2026)"
description: "Step-by-step guide to enabling two-factor authentication on your Amazon account using an authenticator app or SMS to protect your financial data."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Two-Factor Authentication"
faq:
  - q: "Does Amazon support authenticator apps for 2FA?"
    a: "Yes. Amazon supports TOTP-based authenticator apps such as Google Authenticator, Microsoft Authenticator, Authy, and password managers with built-in TOTP like PanicVault. TOTP is the recommended option over SMS."
  - q: "What happens if I lose my phone with Amazon 2FA enabled?"
    a: "Amazon allows you to register a backup phone number during 2FA setup. You can also use recovery codes if you saved them. If you stored your TOTP secret in a password manager like PanicVault, you can access your codes from another device."
  - q: "Can I use SMS for Amazon two-step verification?"
    a: "Yes, Amazon supports SMS as a 2FA method. However, SMS is vulnerable to SIM swapping attacks and is less secure than using a TOTP authenticator app. We recommend using an authenticator app as your primary method."
  - q: "Does Amazon 2FA protect my saved credit cards?"
    a: "Two-step verification prevents unauthorized logins, which protects access to your saved payment methods, order history, and shipping addresses. However, Amazon may still allow some purchases without re-authentication on trusted devices."
  - q: "How do I disable 2FA on Amazon if I need to?"
    a: "Go to Account → Login & Security → Two-Step Verification → Manage → Disable. You will need to verify your identity first. We strongly recommend keeping 2FA enabled and storing your TOTP codes in a password manager instead of disabling it."
---

Your Amazon account is more than a shopping profile. It stores your credit and debit card numbers, your home and work addresses, your complete purchase history, and in many cases your Prime Video watch history, Kindle library, and Alexa voice recordings. A compromised Amazon account gives an attacker the ability to place fraudulent orders, change your shipping addresses, access your payment methods, and harvest personal data that fuels further identity theft. Enabling two-factor authentication is the single most effective step you can take to prevent unauthorized access. This guide walks you through setting it up. For the broader picture on why 2FA matters and how it works, see our [complete guide to two-factor authentication](/two-factor-authentication/).

## Why Your Amazon Account Needs 2FA

Amazon accounts are high-value targets for attackers. Unlike a compromised social media profile, a breached Amazon account has immediate financial consequences. An attacker can:

- **Place orders using your saved payment methods** and ship them to a different address
- **Access your full order history**, revealing personal details about your life, habits, and purchases
- **View and modify your saved addresses**, including home and work locations
- **Access linked services** including Prime Video, Kindle, Audible, and Alexa-enabled devices
- **Change your account email and password**, locking you out entirely

Credential stuffing attacks -- where attackers use email and password combinations leaked from other breaches -- are the most common way Amazon accounts are compromised. If you have ever reused a password across services, your Amazon account is at risk. Two-step verification ensures that even a stolen password is not enough to gain access.

## 2FA Options Available on Amazon

Amazon offers two methods for two-step verification:

**Authenticator app (TOTP)** -- This is the recommended method. An authenticator app generates a time-based one-time password that changes every 30 seconds. The code is generated locally on your device and never travels over a network, making it immune to interception. For a detailed explanation of how this technology works, see our article on [what 2FA is and why you need it](/two-factor-authentication/what-is-2fa/).

**SMS text messages** -- Amazon can send a six-digit code to your phone number via text message. While this is better than no 2FA at all, SMS is vulnerable to SIM swapping and interception attacks. Our comparison of [TOTP vs. SMS authentication](/two-factor-authentication/totp-vs-sms/) explains why TOTP is the stronger choice.

Amazon requires you to set up a primary method and allows you to add a backup method. The ideal configuration is an authenticator app as your primary method with SMS as a backup for emergencies.

## Step-by-Step Setup on the Web

Setting up two-step verification on Amazon through a web browser takes about three minutes.

**Step 1: Navigate to Login & Security.** Go to [amazon.com](https://www.amazon.com) and sign in. Click your name or "Account & Lists" in the top-right corner, then select "Account." Under the "Login & Security" section, click "Edit" or navigate directly to the Login & Security page.

**Step 2: Find Two-Step Verification.** On the Login & Security page, scroll down to the "Two-Step Verification (2SV) Settings" section. Click "Get Started" or "Edit" if you have previously configured it.

**Step 3: Choose your preferred method.** Amazon will present the option to use an authenticator app. Select "Authenticator App" as your method.

**Step 4: Scan the QR code.** Amazon will display a QR code on screen. Open your authenticator app (or password manager with TOTP support) and scan the code. Your app will begin generating six-digit codes that refresh every 30 seconds. If you cannot scan the QR code, Amazon provides a text-based secret key you can enter manually.

**Step 5: Enter the verification code.** Type the current six-digit code from your authenticator app into Amazon's verification field and click "Verify OTP and continue."

**Step 6: Add a backup method.** Amazon will prompt you to add a backup phone number for SMS verification. This is a safety net in case you lose access to your authenticator app. Enter a phone number you control and verify it with the SMS code Amazon sends.

**Step 7: Confirm and save.** Review your settings and click "Got it. Turn on Two-Step Verification." Amazon will confirm that 2SV is now active on your account.

## Step-by-Step Setup on the Mobile App

The process on the Amazon mobile app is similar but navigated differently.

**Step 1: Open account settings.** Tap the hamburger menu (three horizontal lines) or your profile icon, then tap "Your Account."

**Step 2: Go to Login & Security.** Tap "Login & Security." You may be asked to re-enter your password.

**Step 3: Find Two-Step Verification.** Scroll to "Two-Step Verification (2SV) Settings" and tap "Get Started" or "Manage."

**Step 4: Choose Authenticator App.** Select the authenticator app option. The app will display a QR code. If you are setting up on the same phone where your authenticator app lives, tap the option to copy the secret key manually instead, then paste it into your authenticator app.

**Step 5: Verify and enable.** Enter the six-digit code from your authenticator app to verify the connection. Add a backup phone number when prompted. Confirm to enable two-step verification.

Once enabled, Amazon will require a verification code during login on new devices and browsers. You can mark trusted devices to reduce how often you are prompted on your regular devices.

## Why You Should Choose TOTP Over SMS

Amazon supports both authenticator apps and SMS, but they are not equally secure. The difference matters.

SMS codes travel through the telecommunications network, which was not designed with security in mind. [SIM swapping attacks](/two-factor-authentication/sim-swapping/) allow criminals to hijack your phone number by convincing your carrier to transfer it to a new SIM card. Once they control your number, they receive your SMS verification codes. This attack requires no technical sophistication -- it is a social engineering attack against a customer service representative.

TOTP codes, by contrast, are generated entirely on your device. There is no phone number to hijack, no message to intercept, and no carrier employee to deceive. The shared secret lives only on your device and Amazon's servers. An attacker would need physical access to your device -- or access to your authenticator app's backup -- to obtain your codes.

For a deeper analysis of why the security community recommends TOTP over SMS, read our full comparison of [TOTP vs. SMS](/two-factor-authentication/totp-vs-sms/).

## Saving Your Recovery Codes

When you enable two-step verification, Amazon may provide recovery options or allow you to generate backup codes. These are one-time-use codes that let you log in if you lose access to your authenticator app and your backup phone number simultaneously.

Save your recovery codes immediately. Do not skip this step. Store them in a secure location separate from your authenticator app -- a password manager is ideal because the codes are encrypted alongside your other credentials.

If Amazon does not explicitly provide downloadable recovery codes during setup, your backup phone number serves as the recovery path. Make sure the backup number is current and belongs to a phone you will have access to in an emergency. For comprehensive guidance on managing recovery codes, see our [recovery codes guide](/two-factor-authentication/recovery-codes/).

## Using a Password Manager for TOTP Codes

A dedicated authenticator app works well, but there is a more streamlined approach: storing your TOTP codes directly in your password manager alongside your Amazon credentials.

Password managers like PanicVault support TOTP natively. When Amazon displays the QR code during 2FA setup, you scan it with your password manager instead of a separate authenticator app. From that point forward, your password manager generates the six-digit codes and can auto-fill them during login. Your Amazon password and your 2FA code live in the same encrypted entry, protected by the same master password and end-to-end encryption.

This approach has several advantages:

- **No separate app to manage.** You already use a password manager for your credentials. Adding TOTP codes keeps everything in one encrypted vault.
- **Automatic backup and sync.** When your password manager syncs across devices, your TOTP codes sync with it. Lose your phone, and your codes are still accessible on your other devices.
- **Reduced lockout risk.** The most common reason people get locked out of accounts is losing access to a standalone authenticator app that was not backed up. A password manager with cloud sync eliminates this scenario.
- **Encrypted storage.** Your TOTP secrets are encrypted at rest with the same strong encryption protecting your passwords. A standalone authenticator app may or may not encrypt its secret storage.

Some security purists argue that storing passwords and TOTP codes together weakens the "two-factor" principle because both factors are in the same place. In theory, this is true. In practice, the threat model for most people involves remote attackers who have stolen a password from a data breach -- not attackers who have compromised your encrypted password manager vault. The practical security improvement of having reliable, backed-up TOTP codes far outweighs the theoretical risk for the vast majority of users.

For a full discussion of this trade-off and how to set it up, see our guide on [using your password manager as an authenticator](/two-factor-authentication/password-manager-as-authenticator/).

## Related Articles

- [What Is Two-Factor Authentication and Why You Need It](/two-factor-authentication/what-is-2fa/)
- [TOTP vs. SMS: Which Two-Factor Method Is More Secure?](/two-factor-authentication/totp-vs-sms/)
- [How to Use Your Password Manager as an Authenticator](/two-factor-authentication/password-manager-as-authenticator/)
- [Understanding Recovery Codes: Your 2FA Safety Net](/two-factor-authentication/recovery-codes/)
- [How to Set Up 2FA on Every Account That Supports It](/two-factor-authentication/setup-on-every-service/)
