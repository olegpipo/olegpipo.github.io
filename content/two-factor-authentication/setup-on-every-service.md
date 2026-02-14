---
title: "How to Set Up 2FA on Every Major Service"
description: "Step-by-step guide to enabling two-factor authentication on Google, Apple, Microsoft, Amazon, social media, banking, and email services."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Two-Factor Authentication"
---

Enabling [two-factor authentication](/two-factor-authentication/) is the single most impactful thing you can do to protect your online accounts, yet most people only enable it on one or two services -- if they enable it at all. The reason is not apathy. It is that every service hides 2FA settings in a different place, uses different terminology, and presents a different enrollment flow. This guide walks through enabling 2FA on every major service you are likely to use, with a consistent approach that makes the process manageable even if you have dozens of accounts.

Before you begin, choose your authenticator method. If you are unsure, read our comparison of the [best authenticator apps](/two-factor-authentication/best-authenticator-apps/) and consider whether a [password manager with built-in TOTP](/two-factor-authentication/password-manager-as-authenticator/) might simplify your workflow. Whichever method you choose, have it ready before you start enrolling services.

## Before You Start: The Preparation Checklist

Rushing through 2FA setup is how people lock themselves out of accounts. Take ten minutes to prepare:

1. **Choose your authenticator.** A password manager with TOTP support, a standalone app, or a hardware security key. Stick with one primary method for consistency. For Apple users, [PanicVault](https://panicvault.com) is a native macOS/iOS app that handles both passwords and TOTP codes in a single KeePass KDBX vault.
2. **Have backup storage ready.** Every service will offer recovery codes during setup. You need a secure place to store them -- your password manager's notes field, an encrypted document, or a printed sheet in a safe. Never skip this step.
3. **Identify your [priority accounts](/two-factor-authentication/priority-accounts/).** Email first, then financial services, then cloud storage, then social media. If an attacker controls your email, they can reset passwords on everything else.
4. **Set aside uninterrupted time.** Enable 2FA on your critical accounts in a single session. Doing it piecemeal over weeks means you will forget which accounts are protected and which are not.
5. **Save your recovery codes.** After each enrollment, store the [recovery codes](/two-factor-authentication/recovery-codes/) immediately. Do not tell yourself you will do it later.

## Email Services

Your email account is the master key to your digital life. Password reset links go to your email. Account verification goes to your email. Compromise your email, and an attacker can cascade into every other account. Secure email first.

### Gmail / Google Account

Google offers multiple 2FA methods, but TOTP is the most portable:

1. Go to [myaccount.google.com](https://myaccount.google.com) and sign in.
2. Navigate to **Security** in the left sidebar.
3. Under "How you sign in to Google," find **2-Step Verification** and click the arrow.
4. Google may first prompt you to set up phone-based verification. You can add this and then also add an authenticator app.
5. Click **Authenticator app** and then **Set up authenticator**.
6. Google displays a QR code. Scan it with your authenticator app or password manager.
7. Enter the six-digit code your authenticator generates to confirm.
8. Google will provide backup codes. **Save all of them immediately.** Store them in your password manager or another secure location.

Google also supports passkeys and hardware security keys. Adding a physical key as a second method provides the highest level of protection for your Google account.

### Outlook / Microsoft Account

1. Sign in at [account.microsoft.com](https://account.microsoft.com).
2. Go to **Security** and then **Advanced security options**.
3. Under "Additional security," find **Two-step verification** and click **Turn on**.
4. Microsoft walks through a wizard. Choose **An app** when asked how you want to verify.
5. If prompted to use Microsoft Authenticator, look for the option that says "I want to use a different authenticator app."
6. Scan the QR code with your authenticator.
7. Enter the verification code.
8. Microsoft provides a recovery code. Save it.

Microsoft aggressively promotes its own Authenticator app. You are not required to use it -- any TOTP-compatible app or password manager works.

### Apple ID (iCloud)

Apple uses its own 2FA system rather than standard TOTP. It sends verification codes to trusted Apple devices:

1. On an iPhone or iPad, go to **Settings** > your name > **Sign-In & Security** > **Two-Factor Authentication**.
2. On a Mac, go to **System Settings** > your name > **Sign-In & Security** > **Two-Factor Authentication**.
3. Follow the prompts. Apple will ask for a trusted phone number to receive verification codes via SMS as a fallback.
4. Once enabled, any sign-in on a new device sends a six-digit code to your existing trusted devices.

Apple's 2FA is not TOTP-based and cannot be added to a third-party authenticator. The trusted device model works well within the Apple ecosystem but means you need at least one Apple device to receive codes. Make sure your trusted phone number is current.

### ProtonMail

1. Sign in to ProtonMail and go to **Settings** > **Account and Password** > **Two-factor authentication**.
2. Click **Enable** next to "Authenticator app."
3. Scan the QR code.
4. Enter the verification code.
5. ProtonMail displays recovery codes. Save them securely.

ProtonMail also supports hardware security keys (U2F/FIDO2) as a second method, which is recommended for high-security email.

## Cloud Storage and Productivity

### Dropbox

1. Sign in to dropbox.com and go to **Settings** > **Security**.
2. Under "Two-step verification," click **Enable**.
3. Choose **Use a mobile app** (this means any TOTP authenticator, not just a phone app).
4. Scan the QR code and enter the verification code.
5. Dropbox provides a backup phone number option and recovery codes. Save the codes.

### iCloud (see Apple ID above)

iCloud security is tied to your Apple ID. Enabling 2FA on your Apple ID automatically protects iCloud.

## Social Media

Social media accounts are frequent targets for takeover, both for identity theft and for using your account to scam your contacts.

### Facebook / Meta

1. Go to **Settings & Privacy** > **Settings** > **Accounts Center** > **Password and security**.
2. Select **Two-factor authentication** and choose your account.
3. Choose **Authentication app**.
4. Scan the QR code.
5. Enter the verification code.
6. Facebook provides recovery codes. Save them.

Facebook also supports hardware security keys. If you have a U2F key, add it as an additional method.

### Instagram

Instagram's 2FA is managed through the Meta Accounts Center (same as Facebook) or directly in the app:

1. Go to your profile > menu > **Settings and privacy** > **Accounts Center** > **Password and security** > **Two-factor authentication**.
2. Choose **Authentication app**.
3. Instagram may offer to auto-set-up with a specific app. Look for the manual setup option to get a key you can enter in any authenticator.
4. Enter the verification code.
5. Save the recovery codes.

### X (formerly Twitter)

1. Go to **Settings and Support** > **Settings and privacy** > **Security and account access** > **Security** > **Two-factor authentication**.
2. Select **Authentication app**.
3. Scan the QR code or enter the secret manually.
4. Enter the verification code.
5. Save the backup code displayed.

Note: X removed free SMS-based 2FA for non-premium users, making app-based TOTP the standard free option. This is actually better for security, since SMS is vulnerable to SIM-swapping attacks.

### LinkedIn

1. Go to **Settings & Privacy** > **Sign in & security** > **Two-step verification**.
2. Click **Turn on** and choose **Authenticator app**.
3. Scan the QR code.
4. Enter the verification code.
5. LinkedIn provides recovery codes via phone number. Ensure your phone number is current.

## Financial Services

### Amazon

1. Go to **Account** > **Login & security**.
2. Next to "Two-Step Verification," click **Edit** > **Get Started**.
3. Choose **Authenticator app**.
4. Scan the QR code.
5. Enter the verification code.
6. Amazon requires a backup method (phone number). Add one.
7. Save any recovery information provided.

### PayPal

1. Go to **Settings** (gear icon) > **Security** > **2-step verification**.
2. Click **Set up**.
3. Choose **Use an authenticator app**.
4. Scan the QR code.
5. Enter the verification code.
6. PayPal enables a backup SMS method automatically.

### Banking

Banks vary widely in their 2FA implementations. Many use proprietary systems rather than standard TOTP. Common patterns:

- **Major banks** (Chase, Bank of America, Wells Fargo, Citi) typically offer SMS-based 2FA or push notifications through their own apps. Few support standard TOTP.
- **Online-first banks** (Ally, Marcus, Capital One) are more likely to support app-based 2FA.
- **Investment platforms** (Fidelity, Vanguard, Schwab) increasingly support TOTP. Check your brokerage's security settings.

For banks that only offer SMS-based 2FA, enable it anyway. SMS 2FA is weaker than TOTP but dramatically stronger than no 2FA at all. The threat of SIM swapping is real but primarily targets high-value individuals. For most people, SMS 2FA is a meaningful improvement.

## Developer and Technical Services

### GitHub

1. Go to **Settings** > **Password and authentication** > **Two-factor authentication**.
2. Click **Enable two-factor authentication**.
3. Choose **Set up using an app**.
4. Scan the QR code.
5. Enter the verification code.
6. GitHub displays recovery codes. **These are critical** -- save them immediately. GitHub account recovery without codes is extremely difficult.

GitHub also supports passkeys and hardware security keys. For developers, a hardware key is highly recommended.

### AWS (Amazon Web Services)

1. Sign in to the AWS Console and go to **IAM** > **Security credentials**.
2. Under "Multi-factor authentication (MFA)," click **Assign MFA device**.
3. Choose **Authenticator app** (or "Virtual MFA device").
4. Scan the QR code.
5. Enter two consecutive verification codes (AWS requires two to confirm synchronization).

AWS account security is paramount. A compromised AWS root account can result in enormous financial damage from unauthorized resource usage. Enable MFA on the root account and every IAM user.

### npm

1. Sign in to npmjs.com and go to your profile > **Account** > **Two Factor Authentication**.
2. Click **Enable 2FA**.
3. Scan the QR code.
4. Enter the verification code.
5. Save recovery codes.

For package maintainers, npm 2FA prevents supply-chain attacks where an attacker publishes malicious code under your package name.

## Common Pitfalls and How to Avoid Them

### Not Saving Recovery Codes

This is the number one cause of account lockouts. Every service provides recovery codes during 2FA setup. These are your lifeline if you [lose your 2FA device](/two-factor-authentication/lost-2fa-device/). Save them immediately, in your password manager or another secure location. Never assume you will remember to do it later.

### Using Only SMS-Based 2FA

SMS 2FA is better than nothing, but it is vulnerable to SIM swapping, SS7 network attacks, and social engineering of carrier support staff. Use TOTP or hardware keys whenever a service supports them. Fall back to SMS only when it is the only option.

### Enabling 2FA Without Testing

After enabling 2FA on a service, sign out and sign back in immediately to verify everything works. Discovering that your authenticator has the wrong code -- or no code at all -- is much better to discover now than during a critical moment weeks later.

### Setting Up 2FA on a Device You Might Lose

If your only authenticator is the phone that you might drop, break, or have stolen, you have a single point of failure. Ensure your TOTP secrets are backed up. Using a password manager that syncs across devices solves this problem, because losing one device does not mean losing your codes. See our guide on [backing up TOTP codes](/two-factor-authentication/backup-totp-codes/) for detailed strategies.

### Forgetting Which Accounts Have 2FA

After a large enrollment session, it is easy to lose track. Maintain a list (in your password manager) of which accounts have 2FA enabled and which method each uses. When you add a new account, add 2FA as part of the initial setup rather than as a separate task you will "do later."

## The Priority Order

If you cannot enable 2FA everywhere in one session, prioritize in this order:

1. **Primary email** -- The account that receives password reset links for everything else.
2. **Secondary email** -- Any backup email used for account recovery.
3. **Password manager** (if cloud-based) -- The vault that holds everything.
4. **Financial services** -- Bank accounts, investment platforms, payment services.
5. **Cloud storage** -- Dropbox, Google Drive, iCloud, OneDrive.
6. **Social media** -- Facebook, Instagram, X, LinkedIn.
7. **Shopping** -- Amazon, other sites with saved payment methods.
8. **Developer tools** -- GitHub, AWS, npm, hosting providers.
9. **Everything else** -- Any remaining account that supports 2FA.

This order reflects the cascading damage potential: compromising your email lets an attacker reach everything downstream. Securing the top of the chain protects the entire structure.

## After Setup: Maintaining Your 2FA

Enabling 2FA is not a one-time task. Maintenance keeps your protection current:

- **Review quarterly.** Check your accounts for new 2FA options. Services frequently upgrade from SMS-only to TOTP or passkey support.
- **Verify backups.** Confirm that your recovery codes are still accessible and that your [TOTP backup strategy](/two-factor-authentication/backup-totp-codes/) is working.
- **Update after device changes.** When you get a new phone, transfer your authenticator data before wiping the old device. Better yet, use a password manager that syncs TOTP codes automatically.
- **Audit your recovery phone numbers.** If you changed your phone number, update the backup numbers on all services that use them.

Two-factor authentication is the highest-leverage security investment you can make. The setup process takes an afternoon. The protection lasts indefinitely. Start with your email, work down the priority list, save every recovery code, and do not stop until every account that supports 2FA has it enabled.
