---
title: "Set Up 2FA on LinkedIn (2026)"
description: "Step-by-step guide to enabling two-factor authentication on LinkedIn using an authenticator app or SMS to protect your professional identity."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Two-Factor Authentication"
faq:
  - q: "Does LinkedIn support authenticator apps for 2FA?"
    a: "Yes. LinkedIn supports standard TOTP from any authenticator app or password manager with TOTP support, including Google Authenticator, PanicVault, and KeePassXC."
  - q: "Why is LinkedIn 2FA important?"
    a: "LinkedIn accounts contain professional networks, employment history, and business contacts. Compromised accounts are used for sophisticated spear-phishing, business email compromise, recruitment scams, and identity theft targeting your professional connections."
  - q: "Can I use 2FA on LinkedIn without a phone number?"
    a: "If you choose the authenticator app method, you do not need to provide a phone number for 2FA. However, LinkedIn may still require a phone number for other account verification purposes."
  - q: "What happens if I lose access to my LinkedIn 2FA?"
    a: "LinkedIn can send a verification code to the phone number associated with your account. You can also contact LinkedIn support, but the recovery process may take several days and require identity verification."
  - q: "Does LinkedIn support security keys?"
    a: "As of 2026, LinkedIn does not support hardware security keys (FIDO2/WebAuthn) for two-factor authentication. Your options are an authenticator app (TOTP) or SMS."
---

LinkedIn is not just a social network -- it is the primary repository of your professional identity, career history, business relationships, and industry connections. A compromised LinkedIn account does not just affect you personally. It gives an attacker a credible platform for spear-phishing your colleagues, impersonating you in business contexts, running recruitment scams targeting your connections, and harvesting professional intelligence that fuels business email compromise attacks. LinkedIn accounts are high-value targets precisely because the professional context lends credibility to malicious messages. Enabling [two-factor authentication](/two-factor-authentication/) on LinkedIn is essential for protecting both your own career and the people in your network.

The professional phishing threat is particularly acute. Attackers who control a LinkedIn account can send InMail messages, connection requests, and job offers that appear completely legitimate because they come from a real professional profile with a genuine employment history. These messages are far more convincing than the typical phishing email from a stranger, making LinkedIn 2FA a responsibility that extends beyond personal security.

## 2FA Options Available on LinkedIn

LinkedIn offers two methods for two-step verification:

**Authenticator app (TOTP)** is the recommended option. LinkedIn supports standard TOTP, so any compatible authenticator app or password manager will work. Codes are generated locally on your device every thirty seconds and are not vulnerable to SIM swapping or SMS interception.

**SMS (text message)** sends a six-digit code to your registered phone number when you sign in from an unrecognized device. While better than no 2FA, SMS is the weaker option due to well-documented vulnerabilities including [SIM swapping and SS7 exploits](/two-factor-authentication/sms-being-phased-out/).

LinkedIn does not currently support hardware security keys (FIDO2/WebAuthn) or push-based notifications as 2FA methods. For accounts where you want the strongest possible protection, an authenticator app is your best available option on LinkedIn.

## Step-by-Step Setup on the Web

To enable TOTP-based 2FA on LinkedIn using a desktop browser:

1. Open [linkedin.com](https://www.linkedin.com) in your browser and sign in.
2. Click your profile picture in the top-right corner.
3. Click **Settings & Privacy** from the dropdown menu.
4. In the left sidebar, click **Sign in & security**.
5. Find **Two-step verification** and click **Change** (or **Turn on** if it is not yet enabled).
6. LinkedIn asks how you want to receive verification codes. Select **Authenticator app**.
7. Click **Continue** or **Set up**.
8. LinkedIn displays a QR code and a secret key. Open your authenticator app or password manager and scan the QR code. If scanning is not possible, click the option to show the secret key as text and enter it manually.
9. Your authenticator begins generating six-digit codes. Enter the current code in the verification field on LinkedIn.
10. Click **Verify** to complete the setup.
11. LinkedIn confirms that two-step verification is now active.

After enabling 2FA, note that LinkedIn provides recovery options through your registered phone number and email. Unlike some services, LinkedIn does not display a separate set of recovery codes during setup. Instead, if you lose access to your authenticator, LinkedIn sends a verification code to your phone number on file. Make sure this number is current.

## Step-by-Step Setup on the Mobile App

### On iPhone

1. Open the **LinkedIn** app.
2. Tap your profile picture in the top-left corner.
3. Tap **Settings** (gear icon), or tap **View Profile** and then navigate to settings.
4. Under the **Account** section, tap **Sign in & security**.
5. Tap **Two-step verification**.
6. Tap **Set up** (or **Change** if already configured with SMS).
7. Select **Authenticator app** as your verification method.
8. LinkedIn displays a QR code and secret key. Since you are on the same device as your authenticator, tap the option to copy the secret key.
9. Switch to your password manager or authenticator app, add a new entry, and paste the secret key.
10. Return to LinkedIn and enter the six-digit code from your authenticator.
11. Tap **Verify** to complete.

### On Android

1. Open the **LinkedIn** app.
2. Tap your profile picture in the top-left corner.
3. Tap the **Settings** gear icon.
4. Tap **Sign in & security** > **Two-step verification**.
5. Tap **Set up** and select **Authenticator app**.
6. Copy the secret key or scan the QR code with your authenticator.
7. Enter the verification code and tap **Verify**.

## Why LinkedIn Accounts Are High-Value Targets

Understanding why attackers specifically target LinkedIn accounts reinforces why 2FA is not optional for this service:

**Spear-phishing amplification.** A compromised LinkedIn account gives an attacker access to your professional network. Messages sent from your account carry the weight of your real identity and professional history. An attacker can send targeted messages to your connections that reference shared employers, mutual contacts, or industry events -- details that make the phishing attempt extraordinarily convincing.

**Business email compromise (BEC).** LinkedIn profiles contain job titles, reporting structures, and organizational affiliations. Attackers harvest this information to craft BEC attacks against companies, impersonating executives or finance personnel to redirect wire transfers or extract sensitive data.

**Recruitment scams.** Fake job offers sent from legitimate-looking profiles are a growing attack vector. An attacker controlling your account could send fraudulent job listings or "opportunities" that redirect victims to credential-harvesting sites or malware downloads.

**Credential harvesting.** LinkedIn credentials are frequently reused across other professional services. If your LinkedIn password is the same as your corporate email or VPN password, a single compromise cascades into your employer's infrastructure.

**Identity theft.** A LinkedIn profile contains your full employment history, education, location, and often your email address. This information is sufficient for sophisticated identity theft or social engineering attacks against other services.

These threats make LinkedIn 2FA a professional responsibility, not just a personal security preference.

## Choosing TOTP Over SMS

For LinkedIn specifically, TOTP is the clear choice over SMS:

**Professional targeting.** LinkedIn users are targeted by sophisticated attackers who have the resources and motivation to execute SIM swapping attacks. The professional information on your profile makes you identifiable to attackers, and your connections make a successful compromise more valuable.

**Reliability.** TOTP codes generate offline, using only a stored secret and the current time. If you are traveling internationally, in a building with poor cellular reception, or between phone carriers, your TOTP codes continue working without interruption. SMS depends on cellular service and carrier infrastructure.

**No carrier vulnerability.** SIM swapping -- where an attacker convinces your carrier to port your number -- is the most common attack against SMS 2FA. TOTP removes the carrier entirely from your authentication chain. For a deeper look at why SMS is being abandoned, see our article on [SMS 2FA being phased out](/two-factor-authentication/sms-being-phased-out/).

**Portability.** Your TOTP secret can be stored in any compatible authenticator or password manager. Changing your phone number, switching carriers, or moving to a new phone does not affect your 2FA. The secret travels with your authenticator, not your SIM card.

For a full comparison of these two methods, read our guide on [TOTP vs. SMS](/two-factor-authentication/totp-vs-sms/).

## Managing Recovery Without Dedicated Recovery Codes

Unlike many services that provide a set of one-time recovery codes, LinkedIn's recovery mechanism relies on your registered phone number and email address:

**Keep your phone number current.** If you lose access to your authenticator, LinkedIn sends a verification code to your phone number on file. If that number is outdated, recovery becomes significantly harder.

**Keep your email address current.** LinkedIn also uses your email for identity verification during recovery. Make sure the email associated with your account is one you can access independently.

**Store your TOTP secret securely.** Because LinkedIn does not give you separate recovery codes, the backup of your TOTP secret itself becomes your recovery mechanism. If your TOTP secret is stored in a password manager that syncs across devices, losing a single device does not lock you out.

**Contact LinkedIn support as a last resort.** If you cannot access your authenticator, phone number, or email, LinkedIn's support team can help recover your account -- but the process requires identity verification and can take several business days.

The best protection against LinkedIn lockout is storing your TOTP secret in a password manager with reliable backup and sync capabilities. For general advice on recovery strategies, see our [recovery codes guide](/two-factor-authentication/recovery-codes/).

## Using a Password Manager for TOTP

Storing your LinkedIn TOTP secret in a password manager is the most reliable way to maintain continuous access while keeping your account protected:

**Automatic backup.** Your TOTP secret is encrypted within your password database and backed up whenever your vault is backed up. No separate backup process, no risk of orphaned secrets on a lost device.

**Cross-device access.** Sign into LinkedIn from any device where your password manager is available. Your password and TOTP code are together in one entry.

**Professional context.** As a professional network, LinkedIn is something you may need to access urgently -- to respond to a recruiter, verify a business contact, or check a message. Having your TOTP code immediately available in your password manager eliminates friction when access matters.

[PanicVault](https://panicvault.com), a KeePass-compatible password manager for iPhone, iPad, and Mac, handles LinkedIn TOTP seamlessly. During setup, scan LinkedIn's QR code or enter the secret key into the OTP field of your LinkedIn entry. PanicVault stores the secret in the standard KeePass OTP field within your encrypted `.kdbx` database and generates the six-digit code alongside your password.

Because PanicVault uses the open KeePass format, your LinkedIn TOTP secret is never locked into a proprietary ecosystem. The same `.kdbx` database works in [KeePassXC on desktop](/two-factor-authentication/best-authenticator-apps/), KeePassDX on Android, or any other KeePass-compatible app. If you ever switch platforms or apps, your LinkedIn credentials and TOTP secret travel with you.

Store your LinkedIn password, TOTP secret, and any recovery information (phone number, email) in a single encrypted entry. This consolidated approach means you always know where to find your LinkedIn access credentials, and your authenticator secret is protected by the same strong encryption -- AES-256 or ChaCha20 with Argon2d key derivation -- as your other passwords.

For more on this approach, see our guides on [using a password manager as your authenticator](/two-factor-authentication/password-manager-as-authenticator/) and [moving existing codes into your password manager](/two-factor-authentication/move-codes-to-password-manager/).

## LinkedIn-Specific Security Best Practices

Beyond 2FA, these measures strengthen your LinkedIn account against common professional threats:

**Use a unique password.** Your LinkedIn password should be randomly generated by your password manager and not used on any other service. LinkedIn has experienced data breaches in the past -- a unique password ensures that a LinkedIn breach does not cascade to your other accounts.

**Review active sessions.** Go to **Settings & Privacy** > **Sign in & security** > **Where you're signed in** and review all active sessions. End any sessions you do not recognize.

**Limit profile visibility.** In **Settings & Privacy** > **Visibility**, control who can see your connections, email address, and full profile. Reducing public exposure of your network makes spear-phishing via your compromised account less effective.

**Be cautious with connection requests.** Not every connection request is legitimate. Attackers create fake profiles to expand their network into target organizations. Verify connection requests from people you do not know personally.

**Review data access permissions.** Under **Settings & Privacy** > **Data privacy** > **Other applications**, check which third-party services have access to your LinkedIn data and revoke unnecessary permissions.

These practices, combined with TOTP-based two-step verification, create a robust defense for your professional identity.

## Related Articles

- [What Is Two-Factor Authentication?](/two-factor-authentication/what-is-2fa/) -- The fundamentals of 2FA and how it works.
- [TOTP vs. SMS: Which 2FA Method Is Safer?](/two-factor-authentication/totp-vs-sms/) -- A detailed comparison of the two most common 2FA methods.
- [Using a Password Manager as Your Authenticator](/two-factor-authentication/password-manager-as-authenticator/) -- Store TOTP codes alongside your passwords for streamlined security.
- [How to Set Up 2FA on Every Major Service](/two-factor-authentication/setup-on-every-service/) -- Enable 2FA across all your accounts.
- [How to Back Up Your TOTP Codes](/two-factor-authentication/backup-totp-codes/) -- Strategies to ensure you never lose access to your second factor.
