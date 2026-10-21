---
title: "Change Your LinkedIn Password and Turn On 2FA (2026)"
description: "Step-by-step guide to changing your LinkedIn password on desktop and mobile, then turning on two-factor authentication with an authenticator app. Current menu paths, lockout recovery, and passkeys."
date: 2026-03-08
lastmod: 2026-10-21
draft: false
silo: "Guides & Tutorials"
aliases:
  - /two-factor-authentication/setup-2fa-linkedin/
faq:
  - q: "How do I change my LinkedIn password?"
    a: "Sign in to LinkedIn, click the Me icon, go to Settings & Privacy, then Sign in & security, and select Change password. Enter your current password, enter and retype a new password, then select Save password. In the app, tap your profile picture and follow the same Settings & Privacy > Sign in & security path."
  - q: "Why is my LinkedIn account a target for hackers?"
    a: "LinkedIn accounts contain professional information including your employer, title, connections, and email address. Attackers use compromised LinkedIn accounts for targeted phishing, recruitment scams, business email compromise, and social engineering attacks against your employer."
  - q: "Does LinkedIn support two-factor authentication?"
    a: "Yes. LinkedIn calls it two-factor authentication (older pages say two-step verification). Go to Settings & Privacy, then Sign in & security, then Two-factor authentication, and choose Authenticator App or Phone Number (SMS). LinkedIn recommends the authenticator app, and a password manager like PanicVault that generates TOTP codes works as one."
  - q: "What happens to my LinkedIn sessions when I change my password?"
    a: "That depends on a checkbox. When you change your password, LinkedIn offers 'Require all devices to sign in with new password'. If you select it, every other session is signed out and has to sign in again with the new password. If you suspect someone else has been in your account, select it."
  - q: "Does LinkedIn give you 2FA recovery codes?"
    a: "LinkedIn's help center does not describe backup or recovery codes for two-factor authentication. If you lose your authenticator and are not signed in anywhere, LinkedIn asks you to verify your identity with a photo of a government-issued ID. Keep the TOTP secret itself backed up, for example in your password manager."
  - q: "Does LinkedIn support passkeys or security keys?"
    a: "LinkedIn supports passkeys for signing in (Settings & Privacy > Sign in & security > Passkeys, up to five per account), although the option does not appear on every device yet. LinkedIn's help pages do not list hardware security keys as a two-factor method; the options are an authenticator app or SMS."
  - q: "How do I know if my LinkedIn account has been hacked?"
    a: "Signs include connection requests or messages you did not send, profile changes you did not make, login notifications from unfamiliar locations, or being unable to sign in. If you notice any of these, change your password immediately and review your account activity."
---

LinkedIn is the world's largest professional network, and that makes it one of the most valuable targets for attackers. A compromised LinkedIn account gives criminals access to your professional identity, your connections' contact information, and a trusted platform for launching phishing attacks disguised as job offers, business proposals, or recruitment outreach. LinkedIn's 2012 breach eventually leaked about 117 million email and password pairs, and the platform remains a top target for credential stuffing and social engineering. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, walks you through changing your LinkedIn password on desktop and mobile, turning on two-factor authentication, and hardening your account against the threats that specifically target professional networks.

## When and Why to Change Your LinkedIn Password

LinkedIn accounts are prime targets for several reasons that make password hygiene especially important:

- **Professional phishing.** Attackers use compromised LinkedIn accounts to send convincing job offers, partnership proposals, and recruitment messages. Because LinkedIn is inherently a platform for connecting with strangers professionally, recipients are less suspicious of messages from unknown accounts than they would be on other platforms.
- **Business email compromise.** A compromised LinkedIn account reveals your employer, title, colleagues, and business relationships -- exactly the information needed to craft targeted phishing emails to your coworkers or clients.
- **Credential stuffing from past breaches.** LinkedIn's 2012 breach and later data scraping incidents mean that old LinkedIn credentials are widely available in breach databases. If you have not changed your password since then, or if you reused that password elsewhere, you are exposed.
- **Recruitment and job scams.** Fake recruiters using stolen accounts lure victims with lucrative job postings, then collect personal information (Social Security numbers, banking details) under the guise of "onboarding."

Change your LinkedIn password immediately if you notice suspicious activity, receive a breach notification, suspect [password reuse](/password-security/password-reuse-dangers/) with another compromised service, or have not updated it in over a year.

## Before You Start

Prepare before making the change:

1. **Your current LinkedIn password.** Required for the standard password change process. If you have forgotten it, see the reset section below.
2. **Your password manager.** Open PanicVault or your preferred manager to [generate a strong replacement](/password-managers/how-generators-work/) and save it immediately.
3. **Your recovery email and phone number.** Verify these are current in your LinkedIn settings. Go to Settings & Privacy → Sign in & security → Email addresses and Phone numbers to confirm.
4. **A decision about other sessions.** LinkedIn lets you sign out every other device when you change your password. If you choose that, expect to sign in again on your phone, tablet, and any other device where you use LinkedIn.

## How to Change Your LinkedIn Password on Desktop (Web)

### Step 1: Go to LinkedIn settings

Open [linkedin.com](https://www.linkedin.com) in your browser and sign in. Click the **Me** icon (your photo) in the top navigation bar, then select **Settings & Privacy** from the dropdown menu.

### Step 2: Navigate to Sign in & security

In the left sidebar of the settings page, click **Sign in & security**. This section manages your password, two-factor authentication, passkeys, and active sessions.

### Step 3: Click Change password

Find the **Change password** option and click it. LinkedIn may prompt you to verify your identity before proceeding.

### Step 4: Enter your current and new password

Fill in the form:
- **Current password**: Your existing LinkedIn password.
- **New password**: A randomly generated password from your password manager. Use at least 20 characters with uppercase, lowercase, numbers, and symbols.
- **Retype new password**: Confirm the new password.

Below the fields, LinkedIn offers **Require all devices to sign in with new password**. Select it if there is any chance someone else has been in your account: it signs out every other session.

### Step 5: Save the change

Click **Save password**. LinkedIn confirms the update.

### Step 6: Update your password manager

Open PanicVault or your password manager and update the LinkedIn entry with your new password. Verify the URL field contains `linkedin.com` so [AutoFill](/guides/autofill-setup/) works correctly on LinkedIn sign-in pages.

## How to Change Your LinkedIn Password on Mobile App

### Step 1: Open LinkedIn app settings

Launch the LinkedIn app on your iPhone or Android device. Tap your **profile picture**, then tap **Settings & Privacy**.

### Step 2: Navigate to Sign in & security

Tap **Sign in & security**.

### Step 3: Tap Change password

Tap **Change password** (on Android, you may need to tap **Change password** a second time). The app may ask you to verify your identity.

### Step 4: Enter your passwords

Enter your current password, then enter and confirm your new password. Generate the new password with PanicVault's password generator on your phone and paste it into both fields. To sign out your other devices, set **Require all devices to sign in with new password** to **Yes**.

### Step 5: Save and sync

Tap **Save password**. Update the LinkedIn entry in your mobile password manager. If your password manager syncs via [cloud storage](/cloud-sync/), the new credential reaches your other devices the next time the vault syncs.

## What Makes a Strong LinkedIn Password

Given the high value of LinkedIn accounts for professional phishing and business email compromise, your replacement password should be exceptionally strong:

- **At least 20 characters.** LinkedIn supports long passwords. Since your password manager autofills it, there is no convenience cost to length.
- **Randomly generated.** Use your password manager's built-in generator. Do not create passwords based on patterns, dictionary words, or personal information. Our [strong password guide](/password-security/strong-password-guide/) explains why human-created passwords are predictable.
- **Unique to LinkedIn.** Never use the same password on LinkedIn and any other service. If your LinkedIn password matches your [Gmail](/guides/change-password-gmail/) or [Microsoft](/guides/change-password-microsoft/) password, a single breach compromises both accounts.
- **Free of professional keywords.** Do not include your company name, job title, industry terms, or any information visible on your LinkedIn profile. Attackers try these first in targeted attacks.

## Store It in a Password Manager

Properly storing your new LinkedIn password is essential for both security and convenience:

1. **Open PanicVault** or your preferred password manager and locate your LinkedIn entry.
2. **Replace the old password** with the new one. If you used the in-app generator, the new password may already be saved.
3. **Verify the URL** is set to `https://www.linkedin.com` so AutoFill activates on LinkedIn sign-in pages.
4. **Add the two-factor secret** to the same entry when you turn on 2FA (see below).
5. **Add a date note** for your records, noting when the password was last changed. This is valuable during [password audits](/guides/audit-passwords/).
6. **Confirm sync** across devices. Open your password manager on another device and verify the updated LinkedIn entry is there.

Not using a password manager yet? Read our [first-time setup guide](/guides/first-time-setup/) to get started. A password manager is the single most impactful security tool you can adopt.

## What to Do If You Forgot Your LinkedIn Password

If you cannot remember your current LinkedIn password:

1. **Go to the LinkedIn sign-in page** at [linkedin.com](https://www.linkedin.com) or open the LinkedIn app.
2. **Click or tap "Forgot password?"** below the sign-in form.
3. **Enter your email address or phone number.** LinkedIn uses this to locate your account.
4. **Enter the verification code.** LinkedIn sends a code (not a link) to that email address, or by text or voice call to that phone number. Enter it and select **Submit** before it expires. If two-factor authentication is on, LinkedIn may also ask for your 2FA code.
5. **Create a new password.** Use your password manager's generator to create a strong, random password of at least 20 characters.
6. **Save it immediately.** Store the new password in PanicVault or your preferred password manager before doing anything else.
7. **Turn on two-factor authentication** once you are back in your account (see below).

If you no longer have access to the email address or phone number on your account, select **Can't access this email?** (or **Don't have access to any of these?**). LinkedIn asks for a new email address and a photo of a government-issued ID before it restores access. Keep your recovery information current to avoid this scenario.

## Turn On Two-Factor Authentication

LinkedIn now calls this setting **two-factor authentication** (older help pages and guides say "two-step verification"). It offers two methods:

- **Authenticator App** -- the method LinkedIn recommends. Any standard TOTP app works, including a password manager with TOTP support. Codes are generated on your device every 30 seconds, so they cannot be stolen through [SIM swapping or SMS interception](/two-factor-authentication/sms-being-phased-out/).
- **Phone Number (SMS)** -- a six-digit code by text message. Better than no 2FA, but it is the weaker option.

When you are already signed in to the LinkedIn app, LinkedIn may show a sign-in prompt on your phone instead of asking for a code. You cannot pick that prompt as your method; it comes on top of the one you set up. LinkedIn's help pages do not list hardware security keys as a two-factor option. LinkedIn does support passkeys for signing in (**Settings & Privacy** > **Sign in & security** > **Passkeys**, up to five), although the option is not shown on every device yet.

### On the web

1. Click the **Me** icon, then **Settings & Privacy**.
2. Click **Sign in & security**, then **Two-factor authentication**.
3. Click **Turn on**, then **Set up**.
4. Choose **Authenticator App** and click **Continue**.
5. LinkedIn shows a QR code and a text key. Scan the QR code with your authenticator, or enter the key manually.
6. Enter the six-digit code your authenticator shows, and confirm.

### In the iPhone or Android app

1. Tap your profile picture, then **Settings & Privacy**.
2. Tap **Sign in & security** > **Two-factor authentication**.
3. Turn the setting on and tap **Set up**, then choose **Authenticator App**.
4. Because your authenticator is probably on the same phone, copy the text key instead of scanning, add it to your authenticator or password manager, and enter the six-digit code back in LinkedIn.

### Storing the code in PanicVault

[PanicVault](https://apps.apple.com/app/id6759188575), a KeePass-compatible password manager for iPhone, iPad, and Mac, can be your LinkedIn authenticator. Edit your LinkedIn entry, go to the **One-Time Password** section, and either tap **Scan QR Code** (on iPhone and iPad) or paste LinkedIn's text key. A live code appears with a countdown; tap it to copy. The secret is saved as a standard `otpauth://` URI inside your encrypted `.kdbx` file, so the same entry also works in KeePassXC or any other KeePass app that reads that format.

### If you lose access to your authenticator

LinkedIn's help center does not describe backup or recovery codes for two-factor authentication, so plan ahead:

- **Back up the secret itself.** LinkedIn's help assumes your authenticator lives on one phone, and tells you to turn 2FA off and set it up again from a signed-in session before you switch phones. If the secret is stored in your password manager vault, it moves to a new phone with the vault and nothing needs to be redone. See [how to back up 2FA](/two-factor-authentication/backup-totp-codes/).
- **Use a session you are still signed in to.** If LinkedIn is still open on another device, you can turn 2FA off there and set it up again.
- **Otherwise, verify your identity.** At the two-factor prompt, choose **verify your identity** and upload a photo of a government-issued ID (LinkedIn uses the verification provider Persona, which may also ask for a selfie). Keep your phone number and email current so the rest of the recovery goes smoothly.

## Harden Your LinkedIn Account

LinkedIn accounts warrant additional security measures beyond a strong password and 2FA:

- **Review active sessions.** Under **Sign in & security** → **Where you're signed in**, review every active session. Sign out of any you do not recognize, or choose **Sign out of all these sessions**.
- **Check your email addresses and phone numbers.** Verify that only yours are listed. An attacker who has added their own email can use it to reset your password later.
- **Review connected apps.** Under **Data privacy** → **Other applications** → **Permitted Services**, remove any third-party apps you no longer use.
- **Limit what strangers can see.** In **Settings & Privacy** → **Visibility**, control who can see your connections and email address. Less public detail makes spear-phishing your network harder.
- **Be cautious with connection requests.** Fake profiles are a primary vector for LinkedIn-based attacks. Verify connection requests from people you do not know, especially if they claim to be recruiters or executives.

## Related Articles

- [How Password Managers Generate Strong Random Passwords](/password-managers/how-generators-work/)
- [What to Do After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [The Dangers of Password Reuse](/password-security/password-reuse-dangers/)
- [Setting Up 2FA for Your Most Important Accounts](/two-factor-authentication/priority-accounts/)
- [How to Create a Secure Master Password](/guides/master-password/)
