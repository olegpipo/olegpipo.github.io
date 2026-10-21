---
title: "Set Up 2FA on Instagram and Change Your Password (2026)"
description: "Step-by-step guide to enabling two-factor authentication on Instagram with an authenticator app, text message, or WhatsApp, changing your Instagram password in Accounts Center, and getting back in if you are locked out."
date: 2026-03-08
lastmod: 2026-10-21
draft: false
silo: "Two-Factor Authentication"
aliases:
  - /guides/change-password-instagram/
faq:
  - q: "Does Instagram support authenticator apps for 2FA?"
    a: "Yes. Instagram supports standard TOTP from any authenticator app or password manager with TOTP support, and recommends it over text messages or WhatsApp. You can only turn the authentication app method on from the Instagram app for iPhone or Android, not from the website."
  - q: "Can I use WhatsApp for Instagram 2FA?"
    a: "Yes, as an additional method. Instagram can send codes to your WhatsApp number, but you have to turn on text message 2FA first. Like SMS, it depends on your phone number, so an authentication app is the stronger choice."
  - q: "How do I change my Instagram password?"
    a: "In the app, go to your profile, tap the menu, then Accounts Center (or Meta Account settings) > Password and security > Change password. Pick your Instagram account, enter your current password and the new one twice, and tap Change password."
  - q: "Does changing my Instagram password change my Facebook password?"
    a: "No. Even when your Instagram and Facebook accounts are linked in Accounts Center, each account keeps its own password. Changing one does not change the other, so give each a unique password."
  - q: "What if I get locked out of Instagram after enabling 2FA?"
    a: "Use one of your saved backup codes to sign in. If you have none and cannot reach your email or phone, choose 'I can't access this email or phone number' in the password reset flow. For accounts with photos of you, Instagram may ask for a video selfie to confirm your identity."
  - q: "Is Instagram 2FA the same as Facebook 2FA?"
    a: "Instagram 2FA is managed through Meta's Accounts Center, which is shared with Facebook. However, each account has its own independent 2FA settings. Enabling 2FA on Facebook does not automatically enable it on Instagram."
  - q: "Can someone hack my Instagram even with 2FA enabled?"
    a: "2FA makes unauthorized access much harder, but sophisticated phishing attacks can still capture both your password and verification code in real time. Use a unique password, enable 2FA, and never enter your credentials on suspicious links."
---

Instagram accounts are prime targets for attackers, and the threat extends well beyond personal embarrassment. A hijacked Instagram account can be used to scam your followers, promote fraudulent products under your identity, extort you for the return of your account, or serve as a stepping stone to compromise your other Meta accounts. For creators and businesses, a compromised account can mean lost revenue, damaged reputation, and the erosion of an audience built over years. Enabling [two-factor authentication](/two-factor-authentication/) on Instagram, together with a strong, unique password, is one of the simplest and most effective steps you can take to prevent account takeover.

Instagram's security settings live in Meta's Accounts Center, which it shares with Facebook. Meta is gradually moving people to "Meta Accounts," so you may see **Meta Account settings** where this guide says **Accounts Center**; the options inside are the same. Each account still has its own password and its own 2FA settings.

## 2FA Options Available on Instagram

Instagram offers three methods for two-factor authentication:

**Authentication app (TOTP)** is the strongest option and the one Instagram recommends. Any standard authenticator app or password manager works. A new six-digit code is generated every thirty seconds, and you enter it when signing in from an unrecognized device. This method works offline and is immune to SIM swapping. Instagram only lets you turn it on from the Instagram app for iPhone or Android.

**Text message** sends a six-digit code to your registered phone number each time you sign in from a new device. While better than no 2FA, SMS is vulnerable to [SIM swapping](/two-factor-authentication/sms-being-phased-out/) and interception.

**WhatsApp** can deliver the same codes to your WhatsApp number. It is an add-on: you need text message 2FA turned on first. Delivery can be more reliable than SMS in some countries, but it carries similar limitations, since it is still tied to your phone number.

For the strongest protection, use an authentication app. For a detailed comparison, see our guide on [SMS codes vs. authenticator apps](/two-factor-authentication/sms-being-phased-out/).

## Step-by-Step Setup in the Instagram App

Because the authentication app method can only be turned on in the mobile app, start there even if you mostly use Instagram on a computer. (On the web, the same screen is under **More** > **Settings** > **See more in Accounts Center** > **Password and security** > **Two-factor authentication**, where you can manage text message and WhatsApp codes.)

### On iPhone

1. Open the **Instagram** app.
2. Go to your profile by tapping your profile picture in the bottom-right.
3. Tap the **menu icon** (three horizontal lines) in the top-right.
4. Tap **Accounts Center** (or **Meta Account settings**).
5. Tap **Password and security**.
6. Tap **Two-factor authentication**.
7. Select your Instagram account.
8. Tap **Authentication app**.
9. Instagram may offer to automatically configure a specific authenticator app. To use your own app or password manager, look for the option to set it up manually or copy the key to get the TOTP secret.
10. Copy the setup key, switch to your authenticator app or password manager, and add a new entry with this key.
11. Return to Instagram and enter the six-digit code your authenticator is now generating.
12. Tap **Next** to confirm.
13. Save your backup codes (see below).

### On Android

1. Open the **Instagram** app.
2. Tap your profile picture in the bottom-right, then tap the **menu icon** (three horizontal lines).
3. Tap **Accounts Center** > **Password and security** > **Two-factor authentication**.
4. Select your Instagram account and choose **Authentication app**.
5. Follow the same process: get the setup key, enter it in your authenticator, enter the verification code, and save your backup codes.

### Adding WhatsApp as a 2FA Method

If WhatsApp is available to you:

1. Make sure **Text message** is already turned on in Two-factor authentication.
2. Add **WhatsApp** as a method. Instagram checks that your registered phone number is linked to a WhatsApp account.
3. A verification code is sent to your WhatsApp. Enter it to confirm.

For the strongest security, use an authentication app as your primary method, with WhatsApp or text messages only as a fallback.

## Choosing TOTP Over SMS and WhatsApp

Instagram account takeovers are common, particularly for accounts with large followings or business accounts. A frequent attack pattern combines credential phishing with SIM swapping:

1. The attacker sends a phishing message (often disguised as an Instagram security alert or brand collaboration offer) to capture your password.
2. The attacker contacts your mobile carrier, impersonates you, and transfers your phone number to their SIM card.
3. They sign into your Instagram account with your stolen password and receive the SMS verification code on their device.

TOTP eliminates step 3 entirely. Your verification codes are generated by your authenticator app using a secret stored locally on your device. There is no phone number to swap, no SMS to intercept, and no carrier representative to social-engineer.

WhatsApp offers marginal improvement over SMS because it uses encrypted messaging, but the code is still tied to your phone number. If your number is ported via SIM swap, the attacker can try to register WhatsApp on the new SIM and receive the code.

## Saving Your Backup Codes

Instagram provides backup codes that let you sign in when your authenticator is unavailable:

1. Go to **Accounts Center** > **Password and security** > **Two-factor authentication** and select your account.
2. Tap **Additional methods** > **Backup codes**.
3. **Save them immediately:**
   - In your Instagram entry in your password manager
   - In an encrypted document stored outside of Instagram's ecosystem
   - On printed paper in a physically secure location
4. Do not save backup codes in Instagram DMs, in a note app synced to an account that depends on Instagram, or in a screenshot sitting unencrypted in your photo library.

Each code is single-use. Tapping **Get new codes** gives you a fresh set and cancels the old one, so do it after you have used a few. For more on storing them, see our guide to [backing up 2FA and recovery codes](/two-factor-authentication/backup-totp-codes/).

## Change Your Instagram Password

Change your password straight away if you notice posts, messages, follows, or profile changes you did not make, if you get a login alert you do not recognize, if the password appears in a data breach or is [reused on another site](/password-security/password-reuse-dangers/), or if someone who no longer needs access (a former social media manager, an ex-partner) knows it.

### In the iPhone or Android App

1. Go to your profile and tap the **menu icon** (three horizontal lines).
2. Tap **Accounts Center** (or **Meta Account settings**) > **Password and security** > **Change password**.
3. Select your **Instagram account**.
4. Enter your current password, then enter the new password twice.
5. Tap **Change password**.

### On the Web

1. Sign in at [instagram.com](https://www.instagram.com) and click **More** > **Settings**.
2. Click **Accounts Center** > **Password and security** > **Change password**.
3. Select your Instagram account, enter your current password and the new one twice, and confirm.

Generate the new password with your password manager rather than inventing one: at least 16 random characters, used nowhere else. Then update the Instagram entry in PanicVault or your password manager straight away, before you close the settings screen. Because your Instagram and Facebook accounts keep separate passwords even when linked, change each one on its own.

## Forgot Your Password or Locked Out?

### If You Forgot Your Password

1. On the login screen, tap **Forgot password?**
2. Enter the email address, phone number, or username on the account.
3. Tap **Send login link** (on the web) or **Continue** (on iPhone). Instagram sends a link to your email or phone.
4. Follow the link, set a new password from your password manager's generator, and save it in your vault immediately.

### If You Cannot Access Your Email or Phone

1. In the reset flow, tap **Can't reset your password?** (on Android, start with **Get help logging in**).
2. Choose your email or phone, tap **Send security code**, then tap **I can't access this email or phone number**.
3. Give Instagram a secure email address that only you can access.
4. If your account has photos of you, Instagram may ask for a **video selfie** turning your head in different directions. Meta says it is never shown on Instagram and is deleted within 30 days. If you pass, Instagram emails you a reset link. Accounts without photos of you get an email asking for the email or phone number you signed up with and the type of device you used.

If an attacker changed the email on your account, look for the message from **security@mail.instagram.com** about the change: its **secure my account** link may let you reverse it. Instagram's starting point for hacked accounts is [instagram.com/hacked](https://www.instagram.com/hacked/).

## Using a Password Manager for TOTP

The most streamlined way to handle Instagram 2FA is to store your TOTP secret directly in your password manager alongside your Instagram password. This eliminates the need for a separate authenticator app and ensures your 2FA secrets are automatically backed up with your password vault.

[PanicVault](https://apps.apple.com/app/id6759188575) supports this workflow natively on iPhone, iPad, and Mac. During Instagram's 2FA setup, copy the setup key, edit your Instagram entry in PanicVault, and paste the key into the **One-Time Password** section. PanicVault stores the secret as a standard `otpauth://` URI inside your encrypted `.kdbx` database and shows the six-digit code with a countdown, refreshing every thirty seconds.

The benefits of this approach are significant:

**Automatic backup.** Your TOTP secret is part of your encrypted password database. Back up your vault, and your Instagram 2FA is backed up too. No separate backup process for your authenticator app.

**Cross-device access.** Because PanicVault uses the open KeePass format, you can access the same database from KeePassXC on a desktop computer or KeePassDX on Android. Your Instagram TOTP code is available wherever you have access to your vault.

**Single workflow.** When you need to sign into Instagram on a new device, your password manager provides both the password and the TOTP code. No app switching, no fumbling with a separate authenticator.

**Backup code storage.** Store your Instagram backup codes in the same entry. Everything you need for Instagram access lives in one encrypted location.

For more on this approach, read our comparison of [Google Authenticator vs. password manager TOTP](/two-factor-authentication/google-authenticator-vs-builtin/) and our walkthrough for [moving existing authenticator codes into a password manager](/two-factor-authentication/move-codes-to-password-manager/).

## Protecting Your Instagram From Common Attacks

2FA is a critical layer of defense, but it works best as part of a broader security posture:

**Use a unique, strong password.** Your Instagram password should be generated by your password manager and used nowhere else. Password reuse is one of the most common ways accounts are taken over.

**Be skeptical of DMs.** Instagram phishing attacks frequently arrive as direct messages claiming your account has been flagged, offering brand deals, or threatening account suspension. Instagram will never ask for your password or verification code via DM. Our guide to [Instagram phishing](/phishing/instagram-phishing/) shows what these messages look like.

**Review connected apps.** On the web, go to **Settings** > **Website permissions** > **Apps and websites** and remove access for any third-party apps you no longer use.

**Check login activity.** In **Accounts Center** > **Password and security** > **Where you're logged in**, review all active sessions, select any device you do not recognize, and log it out.

**Keep your contact details current.** Make sure only your own email addresses and phone numbers are on the account. Attackers sometimes add their own so they can reset your password later.

These steps, combined with TOTP-based 2FA, make your Instagram account a much harder target for attackers.

## Related Articles

- [The Complete Guide to Two-Factor Authentication](/two-factor-authentication/) -- The fundamentals of 2FA and how it protects your accounts.
- [SMS 2FA vs. Authenticator Apps: Why SMS Is Being Phased Out](/two-factor-authentication/sms-being-phased-out/) -- Why TOTP beats SMS for security.
- [Set Up 2FA on Facebook](/two-factor-authentication/setup-2fa-facebook/) -- Protect your linked Facebook account through the same Accounts Center.
- [The Best Authenticator Apps in 2026](/two-factor-authentication/best-authenticator-apps/) -- Compare authenticator options for Instagram and other services.
- [How to Back Up 2FA: TOTP Secrets and Recovery Codes](/two-factor-authentication/backup-totp-codes/) -- Ensure you never lose access to your 2FA secrets.
