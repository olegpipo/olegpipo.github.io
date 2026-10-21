---
title: "Setting Up 2FA for Your Most Important Accounts"
description: "Identify which accounts to protect with two-factor authentication first, then use our service-by-service table: the 2FA methods Google, Apple, Microsoft, Amazon, Meta, X, GitHub and others offer, and where each setting lives."
date: 2026-02-13
lastmod: 2026-10-21
draft: false
silo: "Two-Factor Authentication"
aliases:
  - /two-factor-authentication/setup-on-every-service/
---

Not all accounts carry equal risk. When you enable [two-factor authentication](/two-factor-authentication/) across your digital life, the order in which you secure accounts matters -- because some accounts, if compromised, hand attackers the keys to everything else. This guide identifies the accounts that deserve 2FA first, explains why the priority order matters, and walks through practical setup for each category.

This article focuses on which accounts to protect first when you cannot do everything at once. When you are ready to start, the [service-by-service table](#where-to-turn-on-2fa-service-by-service) below shows which 2FA methods each major service offers, where the setting lives, and links to our full step-by-step guides.

## Why Priority Order Matters

Imagine an attacker compromises your email account. From there, they can:

- Reset passwords for every service linked to that email address.
- Read password reset confirmation emails before you see them.
- Intercept 2FA setup codes or recovery codes sent via email.
- Access cloud storage backups that may contain sensitive documents.
- Impersonate you to contacts, employers, or financial institutions.

Now imagine they compromise your streaming service account instead. They can watch movies on your dime. The damage is not comparable.

Account priority is determined by two factors: the direct impact of compromise (what the attacker gains from that account alone) and the cascading impact (what other accounts become vulnerable as a result). An account with high cascading impact -- like email -- is more critical to secure than an account with high direct impact but no cascading effect.

## Tier 1: Secure These First

### Email Accounts

**Priority: Critical -- Secure this before anything else.**

Your primary email account is the master key to your digital identity. Almost every online service uses email as the account recovery mechanism. If an attacker controls your email, they can reset passwords for banking, social media, cloud storage, and virtually every other service. They receive the confirmation emails, and you do not.

**Setup guidance:**

- Enable the strongest 2FA method your email provider supports. Gmail, Outlook, and iCloud all support hardware security keys and TOTP. Use hardware keys if you have them.
- Register at least two authentication methods (a hardware key and a TOTP app, or two hardware keys) to avoid lockout.
- Save recovery codes and store them in a physically secure location -- not in a document attached to the same email account.
- If you use multiple email addresses, secure all of them. An old email account you forgot about may still be the recovery address for active services.
- Consider enabling Google's Advanced Protection Program if you use Gmail. It requires a passkey or security key to sign in and restricts third-party app access.

**Common mistake:** Securing your bank with 2FA but leaving the email address used for bank password resets unprotected. The attacker bypasses your bank's 2FA by resetting your bank password through your unprotected email.

### Password Manager

**Priority: Critical -- This protects everything else.**

Your [password manager](/password-managers/) stores credentials for every other account. If compromised, the attacker has every password in your vault. This is the one account where the stakes are absolute.

**Setup guidance:**

- Use a strong, unique master passphrase with high entropy. This is the one password you must memorize.
- Enable 2FA on your password manager account if it is cloud-synced. Bitwarden and 1Password, for example, support both authenticator apps and security keys for account sign-in.
- For KeePass-format vaults (the format PanicVault uses), there is no account to sign in to, so the second factor protects the file itself: a [key file](/keepass/key-files/) kept on a separate device, or a YubiKey that PanicVault uses in [challenge-response mode](/help/hardware-keys/). The database file is the vault, so controlling access to the file is the primary security measure.
- Store your password manager's recovery kit (emergency kit, secret key, recovery codes) in a secure physical location -- a safe, a safety deposit box, or with a trusted person.

**Common mistake:** Using the same password for your password manager and another service. If that other service is breached, your entire vault is exposed.

### Financial Accounts (Banking and Investment)

**Priority: Critical -- Direct financial exposure.**

Bank accounts, brokerage accounts, retirement accounts, and cryptocurrency exchanges represent the most immediate financial risk. An attacker with access to these accounts can drain funds, often irreversibly.

**Setup guidance:**

- Enable the strongest 2FA method available. Many banks still only offer SMS-based 2FA. If that is your only option, use it -- SMS 2FA is better than no 2FA -- but be aware of [SIM swapping risks](/two-factor-authentication/sms-being-phased-out/) and take carrier-level precautions.
- For cryptocurrency exchanges and wallets, use hardware security keys where supported. The irreversible nature of cryptocurrency transactions makes these accounts especially high-value targets.
- Enable transaction alerts via email and push notification so you are immediately aware of unauthorized activity.
- If your bank supports app-based authentication (Chase, Bank of America, and others have proprietary push-based 2FA), use it. It is more secure than SMS.
- For services that support [cloud-synced backup options](/cloud-sync/), ensure that 2FA protects the sync service itself.

**Common mistake:** Assuming your bank's fraud protection makes 2FA unnecessary. Fraud resolution takes weeks and does not always result in full recovery. Prevention is far better than remediation.

## Tier 2: Secure These Next

### Cloud Storage and Backup Services

**Priority: High -- Contains copies of your digital life.**

Google Drive, iCloud, Dropbox, OneDrive, and similar services often contain documents, photos, and backups that could be used for identity theft, blackmail, or further account compromise. Backup services may contain copies of your password database, key files, or authentication secrets.

**Setup guidance:**

- Google Account: Supports hardware keys, TOTP, and Google prompts. Enable all available methods.
- Apple Account/iCloud: Supports Apple's built-in 2FA with trusted devices and phone number verification, plus optional security keys. Enable it in Settings > [Your Name] > Sign-In & Security.
- Dropbox: Supports hardware keys and TOTP. Enable in Settings > Security.
- Microsoft/OneDrive: Supports hardware keys, TOTP, and the Microsoft Authenticator app.

**Common mistake:** Protecting your Google account but forgetting that Google Drive contains a spreadsheet with all your passwords (yes, people still do this). The cloud storage account inherits the sensitivity of its contents.

### Work and Business Accounts

**Priority: High -- Professional and organizational impact.**

Compromising a work account does not just affect you -- it gives the attacker a foothold in your organization's systems. Work email, Slack, cloud infrastructure consoles (AWS, Azure, GCP), and admin panels should be secured with strong 2FA.

**Setup guidance:**

- Follow your organization's security policies. Many companies now mandate hardware keys for privileged access.
- If you are a solo operator or small business owner, treat your business accounts with the same urgency as personal financial accounts.
- Secure domain registrar accounts (GoDaddy, Namecheap, Cloudflare). An attacker who controls your domain can redirect your website, intercept your email (by changing MX records), and impersonate your business.
- Admin accounts for any SaaS tool your team uses should have the strongest available 2FA.

### Social Media Accounts

**Priority: High -- Reputational risk and social engineering vector.**

Social media account compromise is used for impersonation, scam propagation, and as a stepping stone for social engineering attacks against your contacts. A compromised social media account can also be leveraged to bypass security questions on other services ("What city did you grow up in?" is answered by your Facebook profile).

**Setup guidance:**

- Use an authenticator app or security key rather than text messages wherever the platform allows it. Facebook and Instagram now keep their 2FA settings in Meta's Accounts Center; X, LinkedIn, Discord and Reddit all support authenticator apps. The [service table below](#where-to-turn-on-2fa-service-by-service) has the current menu path for each.
- Save each platform's backup codes in the same password manager entry as the login.
- Review the sessions and connected third-party apps on each account while you are in its security settings.

**Common mistake:** Assuming your social media accounts are "low value." Attackers routinely use compromised social media accounts to send phishing messages to your contacts, creating a trust exploitation chain.

## Tier 3: Secure When Possible

### E-commerce and Shopping Accounts

Amazon, PayPal, eBay, and other shopping platforms store payment methods. Enable 2FA to prevent unauthorized purchases. Amazon and PayPal both support authenticator apps as well as text-message codes.

### Developer and Technical Accounts

GitHub, GitLab, npm, PyPI, Docker Hub, and cloud infrastructure accounts. A compromised developer account can be used to inject malicious code into software supply chains. GitHub requires 2FA for accounts that contribute code, and npm now sets up new 2FA only with security keys or passkeys.

### Communication Platforms

Signal, WhatsApp, Telegram, Discord, and Zoom. Communication platforms may contain sensitive conversations and can be used for impersonation.

### Gaming and Entertainment

Steam, PlayStation Network, Nintendo, Twitch, Netflix. Lower priority but still worth securing, especially if payment methods are stored or if the account has significant monetary value (game libraries, virtual items).

## Practical Setup Strategy

Rushing through 2FA setup is how people lock themselves out. Before the first account, have two things ready: the authenticator you will use (a password manager with TOTP support, a standalone app, or a security key) and the place where each service's recovery codes will go. Then set aside one uninterrupted session for your Tier 1 accounts. Doing them piecemeal over weeks is how you end up unsure which accounts are protected.

### Step 1: Inventory Your Accounts

Before you start enabling 2FA, create a complete inventory of your accounts. Your password manager is the best source for this. Export a list of saved logins and sort them into the tiers above. You will likely find accounts you forgot existed -- those are the dangerous ones, because they may use weak passwords and have no 2FA.

### Step 2: Choose Your Authentication Methods

For most people, the optimal setup is:

- **Hardware security keys** for Tier 1 accounts (email, password manager, banking) if budget allows.
- **TOTP authenticator app** for everything else. Choose a reputable app -- see our guide to the [best authenticator apps](/two-factor-authentication/best-authenticator-apps/) -- or keep the codes in your password manager. On iPhone, iPad and Mac, [PanicVault](https://apps.apple.com/app/id6759188575) stores each TOTP secret in the same KeePass entry as the password it protects.
- **Avoid SMS-based 2FA** wherever a better option exists. Use it only when it is the sole 2FA method offered.

For a deeper comparison of the methods, see our [complete guide to two-factor authentication](/two-factor-authentication/).

### Step 3: Save Recovery Codes

Every service that offers 2FA also provides recovery codes -- one-time-use codes that let you regain access if you lose your second factor. These are critically important and frequently neglected.

Store recovery codes in at least two secure locations:

- In your password manager (in the notes field for each entry).
- On paper in a physically secure location (safe, safety deposit box).
- In an encrypted file on an offline storage device.

Never store recovery codes in the same location as your second factor. If your phone is stolen and your TOTP app is on that phone, recovery codes stored in a note on the same phone are useless. For detailed backup strategies, see our guide to [backing up TOTP codes](/two-factor-authentication/backup-totp-codes/).

### Step 4: Enable 2FA in Priority Order

Work through your account inventory from Tier 1 down. For each account:

1. Log in and navigate to security settings.
2. Enable 2FA and select the strongest method available.
3. Complete the enrollment (scan QR code, register hardware key, etc.).
4. Generate and save recovery codes.
5. Verify 2FA works by logging out and logging back in.
6. Update your password manager entry with the 2FA status and recovery code storage location.

### Step 5: Test Recovery Procedures

After enabling 2FA on your critical accounts, test the recovery process. Can you actually use your backup hardware key to log in? Can you use a recovery code? Do you know where they are stored? A security measure you cannot recover from is a lockout waiting to happen.

## Where to Turn On 2FA: Service by Service

Every service hides 2FA in a different place and calls it something different. This table lists the methods each major service offers and where the setting lives (menu labels as of October 2026; services rename them often). Where we have a full walkthrough, the last column links to it.

| Service | 2FA methods offered | Where the setting is | Full guide |
|---|---|---|---|
| Google | Google prompts, authenticator app, text or call, passkeys and security keys, backup codes | Google Account > **Security & sign-in** > **2-Step Verification** | [Google](/two-factor-authentication/setup-2fa-google/) |
| Microsoft account | Microsoft Authenticator or any authenticator app, email or text codes, passkeys and security keys | account.microsoft.com > **Security** > **Manage how I sign in** > **Two-step verification** | [Microsoft](/two-factor-authentication/setup-2fa-microsoft/) |
| Apple Account | Codes on your trusted devices or a trusted phone number; optional security keys | iPhone: **Settings** > your name > **Sign-In & Security** | [Apple Account](/two-factor-authentication/setup-2fa-apple-id/) |
| Amazon | Authenticator app, text message | **Your Account** > **Login & security** > **Two-Step Verification (2SV) Settings** | [Amazon](/two-factor-authentication/setup-2fa-amazon/) |
| Facebook | Authentication app, text message, security key, recovery codes | **Settings and privacy** > **Settings** > **Accounts Center** > **Password and security** > **Two-factor authentication** | [Facebook](/two-factor-authentication/setup-2fa-facebook/) |
| Instagram | Authentication app (turned on in the iPhone or Android app), text message, WhatsApp, backup codes | **Settings** > **Accounts Center** > **Password and security** > **Two-factor authentication** | [Instagram](/two-factor-authentication/setup-2fa-instagram/) |
| X | Authentication app, security key, text message (X Premium only) | **Settings and privacy** > **Security and account access** > **Security** > **Two-factor authentication** | [X](/two-factor-authentication/setup-2fa-x-twitter/) |
| LinkedIn | Authenticator app, text message | **Settings & Privacy** > **Sign in & security** > **Two-factor authentication** | [LinkedIn](/guides/change-password-linkedin/) |
| WhatsApp | A two-step verification PIN (being upgraded to a password) rather than codes; passkeys on iPhone | **Settings** > **Account** > **Two-step verification** | [WhatsApp](/two-factor-authentication/setup-2fa-whatsapp/) |
| Discord | Security keys and passkeys, authenticator app, text message as a backup, backup codes | **User Settings** > **My Account** > **Password and Authentication** | [Discord](/two-factor-authentication/setup-2fa-discord/) |
| Reddit | Authenticator app only, backup codes (set up on the desktop website) | **Settings** > **Account authorization** > **Two-factor authentication** | [Reddit](/two-factor-authentication/setup-2fa-reddit/) |
| GitHub | Authenticator app, text message (some countries), passkeys, security keys, GitHub Mobile | **Settings** > **Password and authentication** | [GitHub](/two-factor-authentication/setup-2fa-github/) |
| Proton Mail | Authenticator app, security keys | **Settings** > **All settings** > **Account and password** > **Two-factor authentication** | -- |
| Dropbox | Authenticator app, text message (some countries), security keys, passkeys, backup codes | **Settings** > **Security** > **2-factor authentication** | -- |
| PayPal | Authenticator app, text message | **Settings** > **Security** > **2-step verification** | -- |
| AWS | Passkeys and security keys, authenticator app, hardware code tokens (required on the root user) | Account menu > **Security credentials** > **Multi-factor authentication (MFA)** > **Assign MFA device** | -- |
| npm | Security keys and passkeys (new authenticator-app setups were switched off in late 2025) | Profile picture > **Account** > **Two-Factor Authentication** | -- |

Two rows need a note. WhatsApp's two-step verification protects your phone number's registration on a new phone rather than generating codes, so it does not go into an authenticator. And Apple does not use authenticator-app codes for your Apple Account at all; the codes appear on your other Apple devices.

## Handling Accounts That Only Offer SMS 2FA

Some services -- particularly banks and government portals -- only support SMS-based 2FA. In these cases:

1. Enable SMS 2FA. It is still significantly better than password-only authentication.
2. Add a PIN or account lock to your mobile carrier account (see our [carrier-by-carrier SIM swap protections](/two-factor-authentication/sms-being-phased-out/#lock-your-number-against-sim-swaps)).
3. Consider using a Google Voice number for SMS 2FA where possible. Google Voice numbers cannot be SIM-swapped through a carrier.
4. Monitor your phone for sudden loss of service, which could indicate a SIM swap in progress.

## Maintaining Your 2FA Setup

Enabling 2FA is not a one-time task. Ongoing maintenance keeps your protection effective:

- **Review quarterly.** New accounts appear, services add better 2FA options, and old recovery codes may need refreshing.
- **Update when you change devices.** When you get a new phone, migrate your TOTP secrets before wiping the old device.
- **Replace compromised factors immediately.** If you suspect your phone or hardware key has been compromised, revoke the affected second factor and re-enroll with a new one.
- **Keep your authenticator app updated.** Security patches matter for the app that protects all your other accounts.
- **Review [recovery code](/two-factor-authentication/backup-totp-codes/) storage** to ensure codes are accessible and current.
- **Keep a record of what is protected.** After a big enrollment session it is easy to lose track. Note in each password manager entry whether 2FA is on and which method it uses, and turn 2FA on as part of creating any new account rather than "later."
- **Update recovery phone numbers.** If you change your number, update it on every service that uses it for codes or recovery.

## The Compound Effect of 2FA

Each account you protect with 2FA makes the others harder to compromise. An attacker who cannot access your email cannot reset your bank password. An attacker who cannot access your password manager cannot use credential stuffing. An attacker who cannot access your cloud storage cannot find your recovery documents.

Security is a chain, and 2FA strengthens every link. Start with the links that matter most, work your way through the rest, and you will have built a defense that stops the vast majority of attacks before they start.
