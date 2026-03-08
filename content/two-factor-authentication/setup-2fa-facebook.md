---
title: "Set Up 2FA on Facebook (2026)"
description: "Step-by-step guide to enabling two-factor authentication on Facebook using an authenticator app, SMS, or security key for stronger account protection."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Two-Factor Authentication"
faq:
  - q: "Does Facebook support authenticator apps for 2FA?"
    a: "Yes. Facebook supports standard TOTP from any authenticator app, including Google Authenticator, Microsoft Authenticator, and password managers like PanicVault that have built-in TOTP support."
  - q: "Is Facebook 2FA free?"
    a: "Yes. All 2FA methods on Facebook — authenticator app, SMS, and security keys — are free. There is no premium tier required."
  - q: "What happens if I lose my phone with Facebook 2FA enabled?"
    a: "Use one of your saved recovery codes to sign in. If you don't have recovery codes, Facebook offers an identity verification process that may require uploading a government-issued ID."
  - q: "Can I use 2FA on Facebook without a phone number?"
    a: "Yes. You can use an authenticator app or a security key for Facebook 2FA without providing a phone number. Only SMS-based 2FA requires a phone number."
  - q: "Does Facebook 2FA protect against all hacking?"
    a: "2FA dramatically reduces the risk of account takeover, but it does not protect against every threat. Phishing attacks that capture both your password and TOTP code in real time can still succeed. Use unique passwords and be cautious of suspicious links."
---

Facebook accounts are among the most frequently targeted by attackers, and the consequences of a compromised account go beyond losing access to your profile. An attacker with control of your Facebook account can impersonate you to friends and family, run scam advertisements using your identity, access Messenger conversations containing private information, and pivot to other accounts linked through Facebook Login. With nearly three billion monthly active users, Facebook is a massive target, and accounts without [two-factor authentication](/two-factor-authentication/) are the lowest-hanging fruit.

The good news is that Facebook offers robust 2FA options, including full support for standard TOTP from any authenticator app. Setting it up takes less than five minutes, and the protection it provides is immediate and substantial.

## 2FA Options Available on Facebook

Facebook provides three second-factor methods:

**Authenticator app (TOTP)** is the recommended option. Facebook supports standard TOTP, which means any compatible authenticator app or password manager works -- you are not limited to Facebook's own suggestions. The app generates a new six-digit code every thirty seconds, and the code is required in addition to your password when you sign in from an unrecognized device or browser.

**SMS text messages** send a six-digit code to your registered phone number. This method is widely available but weaker than TOTP because SMS messages can be intercepted through [SIM swapping attacks](/two-factor-authentication/sms-being-phased-out/) or social engineering of mobile carrier support staff. Use SMS only if you cannot use an authenticator app.

**Security keys** are physical hardware devices (like YubiKey) that provide the strongest protection. When you sign in, you plug in or tap your security key to verify your identity. Security keys are phishing-resistant because they verify the legitimacy of the website cryptographically. For a comparison of security keys and TOTP, see our guide on [hardware keys vs. TOTP](/two-factor-authentication/hardware-keys-vs-totp/).

## Step-by-Step Setup on the Web

To enable TOTP-based 2FA on Facebook using a desktop browser:

1. Open Facebook in your browser and sign in.
2. Click your profile picture in the top-right corner and select **Settings & Privacy**, then **Settings**.
3. In the left sidebar, click **Accounts Center** (Meta Accounts Center).
4. Click **Password and security**.
5. Click **Two-factor authentication**.
6. Select the Facebook account you want to protect (if you have multiple accounts linked in Accounts Center).
7. Choose **Authentication app** as your preferred method.
8. Facebook displays a QR code and a text-based secret key. Open your authenticator app or password manager and scan the QR code. If you cannot scan, manually enter the secret key.
9. Your authenticator will begin generating six-digit codes. Enter the current code in the confirmation field on Facebook.
10. Click **Continue** or **Confirm** to complete the setup.
11. Facebook will offer to generate **Recovery codes**. Click **Get Codes** and save all ten codes immediately. These are single-use codes that let you sign in if you lose access to your authenticator.

After enabling the authenticator app, Facebook may still have SMS enabled as a backup method. You can manage this in the same Two-factor authentication settings -- consider whether you want SMS as a fallback (convenient but weaker) or whether you prefer to rely solely on your authenticator app and recovery codes.

## Step-by-Step Setup on the Mobile App

To enable 2FA from the Facebook mobile app on iPhone or Android:

### On iPhone

1. Open the **Facebook** app.
2. Tap the **menu icon** (three horizontal lines) in the bottom-right corner.
3. Scroll down and tap **Settings & Privacy**, then **Settings**.
4. Tap **Accounts Center** under the Meta section.
5. Tap **Password and security**.
6. Tap **Two-factor authentication** and select your Facebook account.
7. Choose **Authentication app**.
8. Facebook shows a QR code and a setup key. If you are using a password manager on the same device, you may need to copy the setup key manually rather than scanning the QR code.
9. Switch to your authenticator app, add a new account, and paste or enter the setup key.
10. Return to Facebook and enter the six-digit code generated by your authenticator.
11. Tap **Continue** to confirm.
12. Generate and save your recovery codes.

### On Android

1. Open the **Facebook** app.
2. Tap the **menu icon** (three horizontal lines) in the top-right corner.
3. Tap **Settings & Privacy** > **Settings**.
4. Tap **Accounts Center** > **Password and security**.
5. Tap **Two-factor authentication**, select your account, and follow the same steps as iPhone: choose authenticator app, scan or enter the setup key, enter the verification code, and save your recovery codes.

## Choosing TOTP Over SMS

If you are deciding between an authenticator app and SMS for Facebook 2FA, TOTP wins on every security dimension:

**SIM swapping risk.** Facebook accounts are high-value targets for SIM swapping attacks, where an attacker convinces your mobile carrier to transfer your phone number to their SIM card. Once they have your number, they receive your SMS verification codes. TOTP codes are generated locally on your device and cannot be intercepted this way.

**No carrier dependency.** SMS delivery depends on your cellular carrier's infrastructure. In areas with poor reception, or if your carrier has an outage, you may not receive SMS codes promptly. TOTP works entirely offline -- your authenticator generates codes using a stored secret and the current time, with no network required.

**International travel.** If you travel internationally and do not have a local SIM or roaming enabled, SMS codes may not reach you. TOTP codes continue to generate normally regardless of your location or network status.

**Account takeover patterns.** Real-world Facebook account compromises frequently involve [phishing attacks](/two-factor-authentication/what-is-2fa/) combined with SIM swapping. Attackers phish your password, then swap your SIM to receive the SMS code. TOTP eliminates the SIM component of this attack chain.

For all these reasons, the security community overwhelmingly recommends TOTP over SMS. Facebook makes it easy to use either one, so there is no reason not to choose the stronger option.

## Saving Your Recovery Codes

Facebook provides ten recovery codes during 2FA setup. Each code can be used exactly once as a substitute for your authenticator code:

1. After enabling 2FA, navigate back to **Password and security** > **Two-factor authentication** in Accounts Center.
2. Select **Recovery codes**.
3. Facebook displays ten eight-digit codes.
4. **Save all of them immediately.** Store them in:
   - The notes field of your Facebook entry in your password manager
   - An encrypted document separate from your primary device
   - A printed copy in a physically secure location

5. Do not store recovery codes in Facebook Messenger or in a note on a device that depends on your Facebook account for access.

When you have used most of your codes, return to the recovery codes section and generate a fresh set. The old unused codes are invalidated when new ones are generated.

For a comprehensive discussion of recovery code management across all services, see our [recovery codes guide](/two-factor-authentication/recovery-codes/).

## Using a Password Manager for TOTP

Managing Facebook 2FA with a password manager streamlines both the setup and the day-to-day experience. Instead of switching to a separate authenticator app every time you sign into Facebook on a new device, your password manager stores the TOTP secret alongside your Facebook password and generates the verification code automatically.

[PanicVault](https://panicvault.com) makes this particularly convenient for Apple users. When you scan Facebook's QR code during 2FA setup, PanicVault stores the TOTP secret in the standard KeePass OTP field within your encrypted `.kdbx` database. The six-digit code appears directly in your Facebook entry, refreshing every thirty seconds. Your Facebook password, TOTP code, and recovery codes are all in one secure, encrypted entry.

This approach also solves the backup problem. Your TOTP secret is part of your encrypted password database, which is backed up through your regular vault backup process. Lose your phone? Your TOTP secrets are in your vault, accessible from any device where you have PanicVault (or KeePassXC, or any other KeePass-compatible app). No panicked search for recovery codes, no account recovery process.

The [password manager as authenticator](/two-factor-authentication/password-manager-as-authenticator/) approach works for Facebook and for virtually every other service that supports standard TOTP. If you are currently using a standalone authenticator app, see our guide on [moving your codes to a password manager](/two-factor-authentication/move-codes-to-password-manager/).

## Additional Facebook Security Settings

While you are in Facebook's security settings, consider these additional protections:

**Recognized devices.** Review the list of devices that are currently signed into your account. Remove any you do not recognize or no longer use.

**Login alerts.** Enable notifications for unrecognized logins so you are immediately aware of any unauthorized access attempts.

**App passwords.** If you use Facebook Login with third-party apps, review which apps have access and revoke permissions for any you no longer use. Each connected app is a potential attack surface.

**Trusted contacts.** Facebook allows you to designate friends as trusted contacts who can help you recover your account. This is a social recovery mechanism -- useful but dependent on your friends' security practices.

These settings, combined with TOTP-based 2FA, create a layered defense that makes your Facebook account significantly harder to compromise.

## Related Articles

- [What Is Two-Factor Authentication?](/two-factor-authentication/what-is-2fa/) -- Understand how 2FA protects your accounts.
- [TOTP vs. SMS: Which 2FA Method Is Safer?](/two-factor-authentication/totp-vs-sms/) -- Why app-based codes beat text messages for security.
- [Using a Password Manager as Your Authenticator](/two-factor-authentication/password-manager-as-authenticator/) -- Simplify 2FA by storing TOTP codes in your vault.
- [How to Save and Manage Recovery Codes](/two-factor-authentication/recovery-codes/) -- Never get locked out of your accounts.
- [Set Up 2FA on Instagram](/two-factor-authentication/setup-2fa-instagram/) -- Protect your linked Instagram account with the same approach.
