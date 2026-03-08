---
title: "Change Your X / Twitter Password"
description: "Step-by-step guide to changing your X (formerly Twitter) password on web and mobile. Includes 2FA setup tips and what to do if your account is compromised."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Guides & Tutorials"
faq:
  - q: "How do I change my password on X (Twitter)?"
    a: "On the web, go to Settings and Privacy, then Your Account, then Change Your Password. Enter your current password and your new password twice, then click Save. On mobile, the path is the same through the app's Settings menu."
  - q: "Does X still support SMS two-factor authentication?"
    a: "SMS-based 2FA on X is restricted to X Premium (formerly Twitter Blue) subscribers. Free accounts should use a TOTP authenticator app or a password manager like PanicVault that can generate TOTP codes. This is actually more secure than SMS."
  - q: "What happens if I forgot my X password?"
    a: "On the X login screen, tap Forgot password and enter your email address or phone number. X will send a reset code. Enter the code, create a new password, and save it in your password manager immediately."
  - q: "Can someone hack my X account if they know my email?"
    a: "Knowing your email alone is not enough, but it is the first step. If your password is weak, reused from another breached service, or guessable, an attacker who knows your email can compromise your account. Use a unique, randomly generated password and enable 2FA."
  - q: "Should I change my X password after a data breach?"
    a: "Yes. If X announces a breach or your credentials appear in a breach database, change your X password immediately. Also change the password on any other service where you used the same credentials, and enable two-factor authentication."
---

Your X (formerly Twitter) account is a public-facing identity tied to your name, opinions, professional brand, and direct messages. A compromised X account can be used to impersonate you, send phishing DMs to your followers, or access private conversations you assumed were secure. Whether you are responding to a security alert, cleaning up after a breach, or simply replacing a weak password, changing your X password takes less than two minutes. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, walks you through the process on both web and mobile, plus the critical step of enabling two-factor authentication.

## When and Why to Change Your X Password

Several situations call for an immediate password change on X:

- **Suspicious account activity.** Tweets you did not post, DMs you did not send, followers you did not add, or settings changes you did not make all indicate someone else has access to your account.
- **A data breach involving X or another service.** X has experienced data exposures in the past. Additionally, if any other service where you used the same password has been breached, your X account is vulnerable. Learn more about [password reuse risks](/password-security/password-reuse-dangers/).
- **You are still using a weak or memorable password.** If your X password is something you can type from memory, it is probably not strong enough. Human-memorable passwords follow patterns that attackers exploit.
- **Someone who knew your password no longer should.** After sharing access with a social media manager, colleague, or partner, revoke that access by changing the password.
- **You logged in on a public or shared device.** Hotel computers, library workstations, and borrowed phones may have keyloggers or cached sessions. Change your password from a trusted device afterward.

X accounts are frequently targeted because they provide a trusted platform for social engineering. An attacker controlling a verified or well-followed account can spread phishing links to thousands of people who trust the account owner.

## Before You Start

Prepare the following before changing your X password:

1. **Your current password.** X requires your existing password to set a new one. If you have forgotten it, see the password reset section below.
2. **Your password manager.** Open PanicVault or your preferred manager so you can [generate a strong replacement](/guides/generate-strong-passwords/) and save it immediately.
3. **Your recovery email and phone number.** Verify these are current in your X settings. You will need them if X prompts for verification or if you ever need to reset your password in the future.
4. **A plan for 2FA.** X restricts SMS-based two-factor authentication to premium subscribers, so free users should set up TOTP (time-based one-time password) authentication. PanicVault and most password managers can generate TOTP codes, making this easy to configure during the same session.

## How to Change Your X Password on Desktop (Web)

### Step 1: Open X settings

Go to [x.com](https://x.com) and sign in. Click **More** (the three-dot icon) in the left sidebar, then click **Settings and Support**, followed by **Settings and privacy**.

### Step 2: Navigate to Your Account

In the settings menu, click **Your account**. This section contains your account information, password settings, and deactivation options.

### Step 3: Select Change your password

Click **Change your password**. X displays a form with three fields.

### Step 4: Enter your current and new password

Fill in the fields:
- **Current password**: Your existing X password.
- **New password**: A randomly generated password from your password manager. Aim for at least 20 characters with a mix of uppercase, lowercase, numbers, and symbols.
- **Confirm new password**: Enter the new password again.

### Step 5: Save the change

Click **Save**. X confirms the password has been updated. You may be signed out of other active sessions depending on your security settings.

### Step 6: Update your password manager

Immediately update the X entry in PanicVault or your password manager with the new password. Verify that the URL field contains `x.com` (and optionally `twitter.com` as a secondary URL) so [AutoFill](/guides/autofill-setup/) works correctly on both domains.

## How to Change Your X Password on Mobile App

### Step 1: Open the X app settings

Launch the X app on your iPhone or Android device. Tap your **profile icon** in the top-left corner, then tap **Settings and Support**, followed by **Settings and privacy**.

### Step 2: Navigate to Your Account

Tap **Your account** in the settings menu.

### Step 3: Tap Change your password

Tap **Change your password**. The app presents the same three-field form as the web version.

### Step 4: Enter your passwords

Enter your current password, then enter and confirm your new password. If you have PanicVault installed on your device, you can use the password generator directly and paste the result into the new password fields. On iOS, the AutoFill suggestion bar above the keyboard may offer to save the new password automatically.

### Step 5: Save and sync

Tap **Save** (or the checkmark icon). Update the entry in your mobile password manager. If your password manager syncs via [cloud storage](/cloud-sync/), the change propagates to all your devices automatically.

## Enable Two-Factor Authentication (TOTP)

Changing your password is only half the security equation. Two-factor authentication ensures that even if someone steals your new password, they cannot access your account without a second verification code.

X offers three 2FA methods, but only one is available to all users for free:

- **TOTP authenticator app** (free, recommended): Works with any TOTP app or password manager that supports TOTP codes, including PanicVault.
- **SMS text message** (X Premium only): Restricted to paid subscribers since 2023. Even if available, SMS is the weakest 2FA method due to SIM-swapping attacks.
- **Security key** (free): Physical hardware keys like YubiKey. Excellent security but requires carrying the key.

### To set up TOTP on X:

1. Go to **Settings and privacy** → **Security and account access** → **Security** → **Two-factor authentication**.
2. Select **Authentication app**.
3. X displays a QR code. Open PanicVault (or your TOTP app), scan the QR code, and the app generates a six-digit code.
4. Enter the code on X to confirm the setup.
5. X provides **backup codes**. Save these in your password manager as a secure note. They are your recovery path if you lose access to your authenticator.

For more details on configuring 2FA across all your accounts, see our guide on [setting up 2FA on every service](/two-factor-authentication/setup-on-every-service/).

## What Makes a Strong X Password

Your replacement password should meet these criteria:

- **At least 20 characters.** X allows long passwords. Since your password manager types it for you, length costs nothing.
- **Randomly generated.** Use the password generator in PanicVault or your preferred manager. Do not try to create a "random-looking" password yourself -- humans are terrible at randomness. See our [strong password guide](/password-security/strong-password-guide/) for the math behind this.
- **Unique to X.** Never reuse your X password on any other service. If it matches your [Microsoft password](/guides/change-password-microsoft/) or [LinkedIn password](/guides/change-password-linkedin/), a breach on one platform compromises both.
- **No personal information.** Your X handle, display name, bio keywords, birth year, and any other publicly visible information should never appear in your password.

## Store It in a Password Manager

The strongest password in the world is useless if you lose it or fall back to a weaker one because you cannot remember it. Here is how to store your new X password properly:

1. **Open PanicVault** or your preferred password manager and find your X / Twitter entry. If you do not have one, create a new entry.
2. **Update the password** field with the new credential. If you generated the password within the manager, it may already be saved.
3. **Set the URL** to `https://x.com`. Consider adding `https://twitter.com` as a secondary URL since some sign-in flows still use the old domain.
4. **Store your TOTP secret** in the same entry if your password manager supports it. PanicVault handles TOTP codes natively, keeping everything in one place.
5. **Save your backup codes** as a secure note within the entry or in a separate secure note in your vault.
6. **Add a date note** recording when you changed the password. This helps during future [password audits](/guides/audit-passwords/).

If you have not set up a password manager yet, our [first-time setup guide](/guides/first-time-setup/) takes about 30 minutes and is worth every second.

## What to Do If You Forgot Your X Password

If you cannot remember your current X password:

1. **Go to the X login page** at [x.com](https://x.com) or open the X app.
2. **Tap "Forgot password?"** below the sign-in form.
3. **Enter your email, phone number, or username.** X uses this to locate your account.
4. **Choose a verification method.** X sends a reset code to your email or phone number on file.
5. **Enter the verification code.** Check your email or SMS for the code and enter it on the reset page.
6. **Create a new password.** Use your password manager's generator to create a strong, random password. Save it in your manager immediately.
7. **Enable 2FA.** Once you are back in your account, set up TOTP authentication to prevent future unauthorized access.

If you no longer have access to your recovery email or phone number, X's account recovery process may require additional identity verification. This can take several days, so keeping your recovery information current is essential.

After regaining access, check your account for unauthorized changes. Review your profile information, connected apps (Settings → Security and account access → Apps and sessions), email address, phone number, and recent DMs. Revoke access for any apps you do not recognize.

## Related Articles

- [How to Generate and Store Strong Passwords](/guides/generate-strong-passwords/)
- [The Dangers of Password Reuse](/password-security/password-reuse-dangers/)
- [How to Set Up 2FA on Every Service](/two-factor-authentication/setup-on-every-service/)
- [What to Do After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [How to Audit Your Existing Passwords](/guides/audit-passwords/)
