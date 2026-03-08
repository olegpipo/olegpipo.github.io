---
title: "Set Up 2FA on Discord (2026)"
description: "Step-by-step guide to enabling two-factor authentication on Discord using an authenticator app to protect your account from takeovers and scams."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Two-Factor Authentication"
faq:
  - q: "Does Discord support authenticator apps for 2FA?"
    a: "Yes. Discord supports any TOTP-compatible authenticator app, including Google Authenticator, Authy, Microsoft Authenticator, and password managers with built-in TOTP like PanicVault."
  - q: "Can I use SMS for Discord 2FA?"
    a: "SMS is available only as a backup method on Discord, not as a primary 2FA option. You must first set up an authenticator app, and then you can optionally add SMS as a fallback. This is actually a good design choice since TOTP is more secure than SMS."
  - q: "What happens if I lose my Discord 2FA codes?"
    a: "Discord provides backup codes when you enable 2FA. If you saved them, use one to log in and then reconfigure 2FA. If you did not save them and lost your authenticator, you will need to contact Discord support, which may require identity verification and can take time."
  - q: "Does Discord 2FA protect my servers?"
    a: "Enabling 2FA protects your account login. Server owners can also require 2FA for moderator actions by enabling server-wide 2FA, which means members need 2FA enabled to kick, ban, or change server settings."
  - q: "Can I enable 2FA on Discord from my phone?"
    a: "Yes. You can enable 2FA from the Discord mobile app by going to User Settings, tapping My Account, and selecting Enable Two-Factor Auth. The process is the same as on desktop."
---

Discord has grown far beyond its gaming roots into a platform used by communities of every kind -- study groups, open-source projects, creative teams, cryptocurrency communities, and professional organizations. That growth has made Discord accounts increasingly valuable targets. Compromised accounts are used for server takeovers, cryptocurrency scams, phishing campaigns against server members, and spreading malware through trusted channels. Enabling two-factor authentication is your primary defense against these attacks. This guide walks you through the setup process on both desktop and mobile. For the big picture on how 2FA protects your accounts, see our [complete guide to two-factor authentication](/two-factor-authentication/).

## Why Your Discord Account Needs 2FA

Discord account compromises have become a significant security problem. The typical attack pattern works like this: an attacker gains access to a Discord account through a stolen password, a phishing link disguised as a game or Nitro gift, or a malicious OAuth authorization. Once inside, they can:

- **Take over servers** where the compromised account has admin or moderator privileges, locking out the real owner and other staff
- **Send scam messages** to every member of the compromised user's friend list and shared servers, often promoting fake cryptocurrency giveaways or phishing links
- **Distribute malware** through trusted channels, because messages from a known account within a server appear legitimate
- **Access private messages** containing personal conversations, shared files, and potentially sensitive information
- **Sell the account** on underground markets, especially accounts with rare badges, high server counts, or Nitro subscriptions

Server owners face an additional risk. A compromised admin account can be used to delete channels, ban legitimate members, change server settings, and effectively destroy communities that took years to build. Discord allows server owners to require 2FA for moderator actions, but that only works if members have actually enabled it.

## 2FA Options Available on Discord

Discord keeps its 2FA implementation straightforward:

**Authenticator app (TOTP)** -- This is the primary and required method. Discord supports any app or password manager that generates standard TOTP codes. For guidance on choosing an app, see our [best authenticator apps comparison](/two-factor-authentication/best-authenticator-apps/).

**SMS (backup only)** -- After setting up an authenticator app, you can add a phone number for SMS-based backup verification. SMS cannot be used as the primary 2FA method on Discord. This design choice reflects the security community's consensus that [TOTP is more secure than SMS](/two-factor-authentication/totp-vs-sms/).

## Step-by-Step Setup on Desktop

**Step 1: Open User Settings.** Click the gear icon near the bottom-left of Discord, next to your username and avatar.

**Step 2: Go to My Account.** In the left sidebar, make sure you are on the "My Account" tab. This is typically the default view when you open settings.

**Step 3: Click Enable Two-Factor Auth.** Scroll down to the "Password and Authentication" section. Click the "Enable Two-Factor Auth" button.

**Step 4: Enter your password.** Discord will ask you to confirm your current password before proceeding.

**Step 5: Scan the QR code.** Discord displays a QR code along with a manual entry key (the text version of the TOTP secret). Open your authenticator app or password manager and scan the QR code. If you prefer manual entry, copy the text key and enter it in your app.

**Step 6: Enter the verification code.** Type the six-digit code currently displayed in your authenticator app and click "Activate."

**Step 7: Download your backup codes.** Discord will immediately present you with a set of backup codes. These are critically important -- click "Download Backup Codes" to save them as a text file. Each code can be used once to log in if you lose access to your authenticator app. Store these codes securely in your password manager.

After enabling 2FA, Discord will ask for a verification code each time you log in on a new device or after logging out.

## Step-by-Step Setup on the Mobile App

**Step 1: Open settings.** Tap your avatar or profile icon in the bottom-right corner (iOS) or swipe right and tap the gear icon (Android).

**Step 2: Tap "My Account."** Under the "User Settings" section, tap "My Account."

**Step 3: Tap "Enable Two-Factor Auth."** Scroll to the authentication section and tap the enable button.

**Step 4: Enter your password.** Verify your identity by entering your current Discord password.

**Step 5: Set up your authenticator.** Discord will display a QR code and a manual entry key. If you are on the same phone as your authenticator app, you will need to use the manual entry key: long-press to copy it, switch to your authenticator app, and paste it as a new entry. If your authenticator is on a different device, scan the QR code from that device.

**Step 6: Enter the code.** Type the six-digit verification code from your authenticator app and tap "Activate."

**Step 7: Save your backup codes.** Discord displays your backup codes. Tap to copy or screenshot them, then immediately store them in your password manager. Do not rely on a screenshot alone -- screenshots can be lost or accidentally deleted.

## Optional: Add SMS Backup

After enabling authenticator-based 2FA, you can add SMS as a backup method:

1. Return to User Settings → My Account
2. Under Two-Factor Authentication, you will see an option to "Enable SMS Authentication"
3. Enter your phone number and verify it with the code Discord sends

SMS backup is optional but provides an additional recovery path if you lose access to your authenticator app and your backup codes simultaneously. The trade-off is that SMS is [vulnerable to SIM swapping](/two-factor-authentication/sim-swapping/), but as a backup-only method, the risk is manageable.

## Optional: Server-Wide 2FA Requirement

If you own or administrate a Discord server, you can require 2FA for moderator actions:

1. Open Server Settings (click the server name → Server Settings)
2. Go to the "Safety Setup" or "Moderation" tab
3. Enable "Require 2FA for moderator actions"

When enabled, any member with moderator permissions (kick, ban, manage channels, etc.) must have 2FA enabled on their personal account before they can perform those actions. This protects the server even if a moderator's password is compromised.

## Why TOTP Is the Right Choice for Discord

Discord's decision to require TOTP as the primary 2FA method (rather than allowing SMS as a standalone option) reflects the reality that Discord accounts are frequently targeted through social engineering. SMS codes can be intercepted through [SIM swapping attacks](/two-factor-authentication/sim-swapping/), which are relatively easy for attackers to execute. TOTP codes are generated locally on your device and never travel through a phone network.

This is especially important for Discord because the attack surface extends beyond your own account. A compromised admin account can damage an entire community. The stronger the authentication protecting admin accounts, the safer every member of those communities becomes.

## Saving Your Recovery Codes

Discord provides backup codes during the 2FA setup process, and this is the only time they are automatically displayed. You can view or regenerate them later from your account settings, but if you skip saving them initially, you might forget they exist until you desperately need them.

Store your backup codes in your password manager alongside your Discord credentials. This ensures they are encrypted, backed up, and accessible even if your phone is lost. Never store them only as a screenshot on the same phone that holds your authenticator app -- if you lose that phone, you lose both your codes and your backup codes. For more on managing recovery codes securely, see our [recovery codes guide](/two-factor-authentication/recovery-codes/).

## Using a Password Manager for TOTP Codes

Rather than using a separate authenticator app for Discord, you can store your TOTP secret directly in your password manager. Password managers like PanicVault generate TOTP codes alongside your stored credentials, giving you a streamlined login workflow and automatic backup.

Here is why this matters for Discord specifically:

- **No app juggling.** During a Discord login, you need your password and then a TOTP code within seconds. Having both in the same password manager entry means you can auto-fill the password and immediately copy the TOTP code without switching between apps.
- **Reliable backup.** Standalone authenticator apps are the most common reason people lose 2FA access. A password manager that syncs across devices means your Discord TOTP code survives a lost or broken phone.
- **Encrypted storage.** Your TOTP secret is protected by the same encryption that guards your passwords. This is important because the TOTP secret is the "master key" -- anyone who has it can generate valid codes.
- **Easy phone upgrades.** When you get a new phone, your password manager migrates everything automatically. No need to disable 2FA on Discord, re-enable it on the new device, and generate new backup codes.

The trade-off of keeping your password and TOTP code in the same vault is well-understood. For most people, the practical benefits of reliable, backed-up TOTP codes outweigh the theoretical concern. Read the full analysis in our guide on [using your password manager as an authenticator](/two-factor-authentication/password-manager-as-authenticator/).

## Related Articles

- [What Is Two-Factor Authentication and Why You Need It](/two-factor-authentication/what-is-2fa/)
- [TOTP vs. SMS: Which Two-Factor Method Is More Secure?](/two-factor-authentication/totp-vs-sms/)
- [The Best Authenticator Apps in 2026](/two-factor-authentication/best-authenticator-apps/)
- [How to Use Your Password Manager as an Authenticator](/two-factor-authentication/password-manager-as-authenticator/)
- [How to Set Up 2FA on Every Account That Supports It](/two-factor-authentication/setup-on-every-service/)
