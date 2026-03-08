---
title: "Change Your Reddit Password (2026)"
description: "Step-by-step guide to changing your Reddit password on desktop and mobile. Covers account security, TOTP-only 2FA, and recovery for passwordless accounts."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Guides & Tutorials"
faq:
  - q: "How do I change my Reddit password?"
    a: "On the web, go to reddit.com, click your avatar, select Settings, then Account, and click Change password. Enter your current password and a new password, then save. On mobile, open the Reddit app, go to Settings, then Account Settings, and tap Change password."
  - q: "Does Reddit support two-factor authentication?"
    a: "Yes, but Reddit only supports TOTP (time-based one-time password) via authenticator apps. There is no SMS-based 2FA option. Use a password manager like PanicVault or an authenticator app to generate your TOTP codes."
  - q: "What if I created my Reddit account with Google or Apple and have no password?"
    a: "If you signed up via Google or Apple, you may not have a Reddit password. Go to Settings, then Account, and look for a Set password option. Alternatively, use the forgot password flow to set one using your email. Having a standalone password gives you a backup login method."
  - q: "Can I see who logged into my Reddit account?"
    a: "Reddit does not currently offer a detailed session or login activity log like some other platforms. This makes it harder to detect unauthorized access, which is why using a strong, unique password and enabling TOTP-based 2FA is especially important."
  - q: "Why should I change my Reddit password?"
    a: "Change your Reddit password if you suspect unauthorized access, if you reused it on another service that was breached, if it is weak or memorable, or if you shared it with someone who should no longer have access. Reddit's limited session visibility makes proactive password hygiene especially important."
---

Reddit hosts hundreds of thousands of communities covering everything from casual interests to sensitive support groups, financial discussions, and professional networking. Your Reddit account may contain years of post history, private messages, saved content, moderation privileges, and community memberships that would be difficult or impossible to recover if lost. Despite this, many Reddit users treat their account password as an afterthought -- using weak credentials, reusing passwords from other services, or never setting a password at all after signing up through Google or Apple. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, walks you through changing your Reddit password on desktop and mobile, enabling Reddit's TOTP-only two-factor authentication, and properly securing an account that may hold more personal data than you realize.

## When and Why to Change Your Reddit Password

Several scenarios call for an immediate Reddit password change:

- **You reused your Reddit password elsewhere.** If the same password protects your Reddit account and any other service, a breach on that other service puts your Reddit account at risk. [Password reuse](/password-security/password-reuse-dangers/) is the most common way Reddit accounts are compromised.
- **Suspicious account activity.** Posts or comments you did not write, subreddit subscriptions you did not make, DMs you did not send, or settings changes you did not authorize all indicate unauthorized access.
- **Reddit announced a security incident.** Reddit experienced a notable data breach in 2018 and has disclosed other security events since. When the platform itself is compromised, changing your password is a baseline response.
- **Your password is weak.** If you can remember your Reddit password without a password manager, it is probably based on a pattern, dictionary word, or personal detail that makes it vulnerable to guessing attacks. See our [strong password guide](/password-security/strong-password-guide/) for what "strong" really means.
- **You shared access with someone.** Whether a co-moderator, partner, or friend had your password, revoke that access by changing it the moment the sharing arrangement ends.
- **You signed up years ago and never updated.** If your Reddit account dates back years and you have never changed the password, it is overdue -- especially if it predates Reddit's 2FA support.

Reddit's lack of detailed session logging means you may not notice unauthorized access until significant damage is done. Proactive password changes reduce this risk.

## Before You Start

Prepare the following:

1. **Your current Reddit password.** If you signed up via Google or Apple and never set a Reddit-specific password, see the "Accounts Without a Password" section below.
2. **Access to your email address.** Reddit may send a verification email during the password change process. Verify the email address on your account at Settings → Account → Email address.
3. **Your password manager.** Open PanicVault or your preferred manager to [generate a strong replacement password](/guides/generate-strong-passwords/) and save it.
4. **A plan for 2FA.** Reddit only supports TOTP for two-factor authentication -- no SMS option. Have your TOTP app or PanicVault ready if you want to enable 2FA during this session (recommended).

## How to Change Your Reddit Password on Desktop (Web)

### Step 1: Open Reddit settings

Go to [reddit.com](https://www.reddit.com) and sign in. Click your **avatar** or **username** in the top-right corner and select **Settings** from the dropdown menu. On new Reddit, you may also click the **gear icon** or navigate to **User Settings**.

### Step 2: Navigate to Account settings

Click the **Account** tab in the settings page. This section manages your email, password, and security settings.

### Step 3: Click Change password

Find the **Change password** section and click the **Change password** button. Reddit displays a form for updating your credentials.

### Step 4: Enter your current and new password

Fill in the form:
- **Old password**: Your current Reddit password.
- **New password**: A randomly generated password from your password manager. Use at least 20 characters with uppercase, lowercase, numbers, and symbols.
- **Verify new password**: Enter the new password again.

### Step 5: Save the change

Click **Save** to confirm. Reddit updates your password and may send a confirmation email to the address on your account.

### Step 6: Update your password manager

Open PanicVault or your password manager and update the Reddit entry with the new password. Verify the URL field contains `reddit.com` so [AutoFill](/guides/autofill-setup/) works correctly on Reddit sign-in pages. If you also use old.reddit.com, consider adding that as a secondary URL.

## How to Change Your Reddit Password on Mobile App

### Step 1: Open the Reddit app settings

Launch the Reddit app on your iPhone or Android device. Tap your **avatar** or **profile icon** in the top-right corner (or bottom-right, depending on the app version), then tap **Settings**.

### Step 2: Navigate to Account Settings

Tap **Account Settings** in the settings menu. This section contains your login and security options.

### Step 3: Tap Change password

Tap **Change password** or **Update password**. The app displays a form for entering your current and new password.

### Step 4: Enter your passwords

Enter your current password, then enter and confirm your new password. Use PanicVault's password generator on your phone to create the new password. On iOS, you can use the AutoFill integration to paste the generated password into the fields.

### Step 5: Save and sync

Tap **Save** to confirm the change. Immediately update the Reddit entry in your mobile password manager. If your password manager syncs across devices via [cloud storage](/cloud-sync/), the updated credential will appear on all your devices.

## Accounts Without a Password (Google or Apple Sign-In)

If you created your Reddit account using Google or Apple sign-in, you may not have a Reddit-specific password. To set one:

1. **On the web,** go to Reddit Settings → Account. Look for a **Set password** option. If you see it, click it and follow the prompts.
2. **If no "Set password" option is visible,** use the forgot password flow. Go to the Reddit login page, click **Forgot password**, and enter the email address associated with your Reddit account. Reddit sends a reset link.
3. **Click the reset link** in your email and create a new password using your password manager's generator.
4. **Save the password** in your password manager immediately.

Setting a standalone Reddit password is important because it gives you a backup login method. If your Google or Apple account is ever compromised or locked, you can still access Reddit directly. It also allows you to enable TOTP-based 2FA, which is only available for accounts with a password set.

## What Makes a Strong Reddit Password

Your Reddit password should follow these principles:

- **At least 20 characters.** Reddit supports long passwords. Since your password manager autofills it, there is no reason to use a shorter one.
- **Randomly generated.** Use your password manager's generator rather than trying to create something "random-looking" yourself. Our guide on [generating strong passwords](/guides/generate-strong-passwords/) explains the configuration options.
- **Unique to Reddit.** Do not reuse your Reddit password on any other service. If your Reddit password matches your [Microsoft](/guides/change-password-microsoft/) or [Facebook](/guides/change-password-facebook/) password, a breach on either platform compromises both.
- **Free of personal information.** Do not use your Reddit username, cake day year, favorite subreddit names, or any information that could be found in your Reddit profile or post history.

## Store It in a Password Manager

Reddit's limited session visibility makes it critical to never lose track of your credentials:

1. **Open PanicVault** or your preferred password manager and find (or create) your Reddit entry.
2. **Save the new password** in the password field. If you generated it within the manager, it may already be stored.
3. **Set the URL** to `https://www.reddit.com` for reliable AutoFill. Consider adding `https://old.reddit.com` as a secondary URL if you use the classic interface.
4. **Record your username** and associated email so all login details are in one place.
5. **Store your 2FA backup codes** (see 2FA section below) as a secure note within the entry.
6. **Add a date note** recording when the password was changed for [audit](/guides/audit-passwords/) reference.
7. **Verify sync** by checking the entry on another device.

If you are not yet using a password manager, our [first-time setup guide](/guides/first-time-setup/) takes about 30 minutes and will transform how you manage all your online accounts, not just Reddit.

## What to Do If You Forgot Your Reddit Password

If you cannot remember your Reddit password:

1. **Go to reddit.com** or open the Reddit app and tap **Log In**.
2. **Click or tap "Forgot password?"** (or "Forgot your password?").
3. **Enter your Reddit username and email.** Reddit sends a password reset link to the email address on file.
4. **Check your email** for the reset message from noreply@reddit.com. Check your spam folder if it does not arrive within a few minutes.
5. **Click the reset link** and create a new password using your password manager's generator.
6. **Save the new password** in your password manager immediately before doing anything else.

If you do not remember the email address associated with your Reddit account, recovery becomes difficult. Reddit's support options for account recovery without email access are limited. This is another reason to store your complete Reddit login details (username, email, and password) in your password manager.

After regaining access, review your account for signs of tampering. Check your profile, subscriptions, DMs, and any moderation actions if you moderate subreddits. Change your password immediately if anything looks unfamiliar, and enable 2FA.

## Enable Two-Factor Authentication (TOTP Only)

Reddit supports two-factor authentication exclusively through TOTP (time-based one-time passwords). There is no SMS option, which is actually a security advantage since TOTP cannot be intercepted through SIM-swapping attacks.

### To set up 2FA on Reddit:

1. Go to **Settings** → **Safety & Privacy** (web) or **Account Settings** (mobile).
2. Find **Two-factor authentication** and click or tap to enable it.
3. Enter your Reddit password to confirm your identity.
4. Reddit displays a QR code. Open PanicVault or your TOTP authenticator app and scan the code.
5. Enter the six-digit code generated by your app to confirm the setup.
6. Reddit provides **backup codes**. Save these in your password manager immediately -- if you lose access to your TOTP app, these codes are your only way back in.

Because Reddit does not offer SMS as a 2FA fallback, losing your TOTP secret and backup codes means losing access to your account entirely. Storing everything in PanicVault -- password, TOTP secret, and backup codes -- in a single entry ensures you always have what you need.

For more on 2FA across all your accounts, see our comprehensive guide on [setting up 2FA on every service](/two-factor-authentication/setup-on-every-service/).

## Additional Security Measures

After changing your password and enabling 2FA, take these additional steps:

- **Review connected apps.** Go to Settings → Safety & Privacy → Apps (or manage third-party app authorization). Revoke access for any apps you no longer use or do not recognize.
- **Check your email address.** Verify the email on your account is correct and that you have access to it. This is your primary recovery method.
- **Review your post and comment history.** If you suspect unauthorized access, check for posts, comments, or votes made without your knowledge.
- **Consider your username's privacy.** If your Reddit username is connected to your real identity and you discuss sensitive topics, consider whether your account security practices match the sensitivity of your content.

## Related Articles

- [How to Generate and Store Strong Passwords](/guides/generate-strong-passwords/)
- [How to Create a Secure Master Password](/guides/master-password/)
- [What to Do After a Data Breach](/data-breaches/what-to-do-after-breach/)
- [The Dangers of Password Reuse](/password-security/password-reuse-dangers/)
- [How to Set Up 2FA on Every Service](/two-factor-authentication/setup-on-every-service/)
