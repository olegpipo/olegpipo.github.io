---
title: "Set Up 2FA on Reddit and Change Your Password (2026)"
description: "Step-by-step guide to enabling two-factor authentication on Reddit with a TOTP authenticator app (Reddit has no SMS option), saving your backup codes, changing or setting your Reddit password, and Google or Apple sign-in accounts."
date: 2026-03-08
lastmod: 2026-10-21
draft: false
silo: "Two-Factor Authentication"
aliases:
  - /guides/change-password-reddit/
faq:
  - q: "Does Reddit support SMS-based 2FA?"
    a: "No. Reddit only supports TOTP-based authenticator apps for two-factor authentication. There is no SMS option. This is actually more secure, since TOTP is immune to SIM swapping attacks that plague SMS-based verification."
  - q: "What authenticator apps work with Reddit?"
    a: "Any app that supports the TOTP standard works with Reddit, including Google Authenticator, Microsoft Authenticator, and password managers with built-in TOTP support like PanicVault."
  - q: "Can I set up Reddit 2FA on mobile?"
    a: "Not in the Reddit app. Reddit says you can only turn on two-factor authentication by logging in to Reddit in a web browser on a computer. Your authenticator can still be on your phone: scan the QR code shown on the computer screen with it."
  - q: "What happens if I lose my Reddit 2FA access?"
    a: "Use one of the ten backup codes Reddit gives you. Without your authenticator or a backup code, getting back into the account can be very difficult, so keep the TOTP secret and the backup codes somewhere other than the phone you use for Reddit, such as your password manager."
  - q: "I signed up with Google or Apple. Do I have a Reddit password?"
    a: "Possibly not. Reddit's two-factor authentication only applies when you log in with a Reddit password; if you use Google or Apple sign-in, protect that account with its own 2FA. To create a Reddit password, disconnect Google or Apple under Settings > Account authorization, and Reddit asks you to create one."
  - q: "How do I change my Reddit password?"
    a: "On reddit.com, open Settings from your profile menu and look in the Account settings for the password option; on old.reddit.com it is under preferences > password/email. If you have forgotten it, use Forgot password on the login screen and Reddit emails you a reset link."
  - q: "Does Reddit 2FA protect my moderated subreddits?"
    a: "Yes. 2FA protects your entire Reddit account, including any subreddits you moderate. If an attacker cannot log in to your account, they cannot abuse your moderator privileges to alter subreddit settings, ban users, or delete content."
---

Reddit is one of the largest community platforms on the internet, and its accounts carry more value than most users realize. A Reddit account tied to moderated communities, years of post history, and accumulated karma is a meaningful target for attackers. Compromised Reddit accounts are used to spread misinformation, promote scams in trusted subreddits, conduct social engineering, and sell access on underground markets. Reddit's approach to 2FA is notably security-conscious: it supports only authenticator app-based TOTP, with no SMS option. This guide walks you through enabling it, saving your backup codes, and changing or setting your Reddit password. For the complete picture on why 2FA matters, see our [complete guide to two-factor authentication](/two-factor-authentication/).

## Why Your Reddit Account Needs 2FA

Reddit accounts may not seem as sensitive as banking or email accounts, but their compromise can have outsized consequences:

- **Moderator account takeovers** allow attackers to seize control of subreddits, alter rules, remove other moderators, and redirect communities for spam, scams, or political manipulation
- **Karma and account age** give compromised accounts an appearance of legitimacy, making them effective tools for astroturfing, disinformation, and social engineering
- **Post and comment history** can reveal personal information, opinions, and details about your life that you may not want exposed
- **Direct messages** may contain private conversations, shared links, or personal exchanges
- **Connected accounts** such as linked email addresses and any verified identity information become accessible

Reddit itself has been targeted. In 2023, Reddit disclosed a security incident where attackers used a fake version of its intranet login page to phish an employee's credentials and 2FA code and reach internal systems. If Reddit's own employees are targeted, individual accounts with default security settings are certainly at risk.

## 2FA Options Available on Reddit

Reddit takes a streamlined approach to 2FA:

**Authenticator app (TOTP)** -- This is the only 2FA method Reddit supports. Any TOTP-compatible app works, including Google Authenticator, Microsoft Authenticator, and password managers like PanicVault that generate TOTP codes. For help choosing, see our [best authenticator apps guide](/two-factor-authentication/best-authenticator-apps/).

**No SMS option** -- Reddit does not offer SMS-based verification. This is a more secure design choice: by skipping SMS entirely, Reddit avoids the [SIM swapping vulnerabilities](/two-factor-authentication/sms-being-phased-out/) that plague SMS-based 2FA on other platforms.

**Passkeys** -- Reddit also lets you sign in with a passkey, managed under **Settings** > **Account authorization** > **Passkeys**. An account cannot rely on passkeys alone.

Reddit's 2FA only applies when you log in with your Reddit password. If you sign in with Google or Apple, you are protected by that account's 2FA instead (see [accounts without a password](#accounts-without-a-password-google-or-apple-sign-in) below).

## Step-by-Step Setup

Reddit only lets you turn on two-factor authentication from a web browser on a computer, not from the Reddit app. Your authenticator can still be on your phone.

**Step 1: Open your account settings.** Sign in at [reddit.com](https://www.reddit.com) on your computer. Click your profile avatar or username, then select **Settings**.

**Step 2: Go to Account authorization.** Find the **Account authorization** section and select **Two-factor authentication**.

**Step 3: Confirm your password.** Enter your Reddit password and select **Confirm**.

**Step 4: Scan the QR code.** Reddit displays a QR code and a text key. Scan the QR code with your authenticator app or password manager on your phone. If your authenticator is on the same computer, copy the text key instead.

**Step 5: Enter the verification code.** Type the six-digit code currently shown in your authenticator into Reddit to finish setup.

**Step 6: Save your backup codes.** Generate your backup codes right away (see below) and store them in your password manager.

On old.reddit.com, the same option is under **preferences** > **password/email**, where you can choose to enable two-factor authentication.

### If Your Authenticator Is PanicVault

On iPhone or iPad, open your Reddit entry in PanicVault, tap **Edit**, and in the **One-Time Password** section tap **Scan QR Code**, then point the camera at the QR code on your computer screen. On a Mac, copy Reddit's text key and paste it into the same section. Either way, the code appears in the entry with a countdown; tap it to copy, and enter it on Reddit.

## Why Reddit's TOTP-Only Approach Is a Good Thing

Some users are frustrated when a service does not offer SMS as a 2FA option, viewing it as inconvenient. In reality, Reddit's TOTP-only approach is a security advantage -- and Reddit learned why the hard way. In 2018, attackers intercepted the SMS codes protecting several Reddit employees' accounts at its cloud and source-code providers, and got away with an old backup of user data. Reddit's advice afterward was to move to token-based 2FA.

SMS-based verification has well-documented weaknesses. [SIM swapping attacks](/two-factor-authentication/sms-being-phased-out/) allow criminals to hijack phone numbers by social-engineering carrier support representatives. Once they control your number, they receive your SMS codes. Telecom networks also have structural vulnerabilities (SS7 protocol flaws) that can be exploited to intercept text messages.

TOTP avoids all of these attack vectors. The codes are generated locally on your device using a shared secret that never travels again after initial setup. There is no phone number to hijack, no message to intercept, and no carrier to deceive. Reddit's decision to support only TOTP means that every Reddit user with 2FA enabled has the more secure option, with no possibility of falling back to the weaker SMS method.

For a thorough comparison of the two approaches, see our analysis of [SMS codes vs. authenticator apps](/two-factor-authentication/sms-being-phased-out/).

## Saving Your Backup Codes

Reddit's backup codes are your way back in if you lose access to your authenticator app. Reddit has no SMS fallback, so store them carefully.

To get them, go to **Settings** > **Account authorization** > **Access your backup codes** on reddit.com (on a computer), enter your password, and select **Continue**. Reddit gives you ten single-use codes. Generating a new set invalidates the old one.

- **Store them in your password manager** alongside your Reddit credentials. This ensures they are encrypted, backed up across devices, and available when you need them.
- **Do not store them only on the same device** as your authenticator app. If you lose that device, you lose both your TOTP codes and your backup codes simultaneously.
- **Do not post them anywhere online**, even in "private" locations. Backup codes stay valid until used or replaced.
- **Generate a fresh set** after you have used a few.

For more on storing recovery codes, see our guide to [backing up 2FA and recovery codes](/two-factor-authentication/backup-totp-codes/).

## Change Your Reddit Password First

If you are tightening up your account, start with the password. Change it if you have reused it anywhere else, if you see posts, comments, messages, or settings changes you did not make, or if someone else (a co-moderator, a former partner) knows it.

- **On reddit.com:** open **Settings** from your profile menu and look in the **Account** settings for the password option. Reddit moves these labels between redesigns, so if you cannot find it, the reset flow below changes your password just as well.
- **On old.reddit.com:** go to **preferences** > **password/email**.

Generate the new password with your password manager -- at least 20 random characters, used nowhere else -- and save it in your Reddit entry straight away. If you also use old.reddit.com, add it as a second URL on the entry so AutoFill offers the login there too.

### If You Forgot Your Password

1. On the login screen, select **Forgot password?**
2. Enter your username or email address and select **Reset Password**.
3. Reddit emails you a **Reset Password** link. It expires after a while, so use it promptly.
4. Set a new password from your password manager's generator and save it in your vault.

Resetting your password logs you out of Reddit on all your devices. If you forgot your username, run the same reset with your email address: the email lists usernames associated with that address. If there is no email address on your account, Reddit cannot send a reset link, so add one now while you can still sign in.

## Accounts Without a Password (Google or Apple Sign-In)

If you created your Reddit account with Google or Apple sign-in, you may not have a Reddit password at all. In that case Reddit's own 2FA does not apply to your logins -- protect the Google account or Apple Account you sign in with by turning on its two-factor authentication.

To give your Reddit account its own password (useful as a backup login, and required before Reddit's 2FA can protect it):

1. Go to **Settings** > **Account authorization** on reddit.com.
2. Select **disconnect** next to Google or Apple.
3. If you do not have a password yet, Reddit asks you to create one. Use your password manager's generator and save it immediately.

Accounts created with a phone number need an email address added before you can set a password.

## Using a Password Manager for TOTP Codes

The most practical way to handle Reddit's TOTP requirement is to store the TOTP secret in your password manager. Password managers like PanicVault support TOTP natively -- you add Reddit's key to your Reddit entry, and the manager generates your six-digit codes alongside your stored password.

This approach solves the biggest problem with standalone authenticator apps: backup and recovery. When your authenticator app lives on a single phone with no backup, losing that phone means losing access to every account protected by that app. When your TOTP codes live in a password manager that syncs across devices, a lost phone is an inconvenience, not a crisis.

The practical benefits for Reddit specifically:

- **Login efficiency.** Your password manager fills your Reddit password, and the current code is in the same entry, one tap away.
- **Backup and sync.** Your Reddit TOTP secret is backed up and synced alongside all your other credentials. Device loss does not mean account loss.
- **Encrypted storage.** The TOTP secret is encrypted at rest with the same strong encryption protecting your passwords.
- **Migration simplicity.** When you upgrade your phone, everything transfers with your password vault. No need to disable Reddit 2FA, set it up again on the new device, and save new backup codes.

Since Reddit only supports TOTP (no SMS backup), having your codes in a reliable, synced password manager is especially important. If your standalone authenticator app fails and you have lost your backup codes, recovering a Reddit account can be extremely difficult.

For the trade-offs of keeping passwords and codes together, see our comparison of [Google Authenticator vs. password manager TOTP](/two-factor-authentication/google-authenticator-vs-builtin/).

## Related Articles

- [The Complete Guide to Two-Factor Authentication](/two-factor-authentication/)
- [SMS 2FA vs. Authenticator Apps: Why SMS Is Being Phased Out](/two-factor-authentication/sms-being-phased-out/)
- [Google Authenticator vs. Password Manager TOTP](/two-factor-authentication/google-authenticator-vs-builtin/)
- [How to Back Up 2FA: TOTP Secrets and Recovery Codes](/two-factor-authentication/backup-totp-codes/)
- [How to Move Your TOTP Codes to a Password Manager](/two-factor-authentication/move-codes-to-password-manager/)
