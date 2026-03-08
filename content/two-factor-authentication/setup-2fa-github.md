---
title: "Set Up 2FA on GitHub (2026)"
description: "Step-by-step guide to enabling two-factor authentication on GitHub using TOTP, SMS, security keys, or GitHub Mobile to protect your code and projects."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Two-Factor Authentication"
faq:
  - q: "Is 2FA required on GitHub?"
    a: "Yes. As of 2024, GitHub requires all users who contribute code to enable two-factor authentication. If you push commits, open pull requests, or contribute to repositories, you must have 2FA enabled. Even if you only use GitHub to browse, enabling 2FA is strongly recommended."
  - q: "What 2FA methods does GitHub support?"
    a: "GitHub supports TOTP authenticator apps, SMS text messages, FIDO2 hardware security keys (like YubiKey), GitHub Mobile push notifications, and passkeys. TOTP and security keys are the most secure options."
  - q: "Can I use a password manager for GitHub 2FA?"
    a: "Yes. Any TOTP-compatible password manager works with GitHub, including PanicVault. You scan GitHub's QR code during setup, and the password manager generates your verification codes alongside your stored GitHub credentials."
  - q: "What happens if I lose my GitHub 2FA device?"
    a: "GitHub provides recovery codes during 2FA setup. You can also use a backup 2FA method if you configured one (such as SMS or a security key). If all else fails, GitHub has an account recovery process that may require identity verification."
  - q: "Does GitHub 2FA protect my private repositories?"
    a: "Yes. 2FA protects your entire GitHub account, including access to all public and private repositories, organizations you belong to, GitHub Actions workflows, secrets stored in repositories, and your GitHub profile."
---

GitHub is the world's largest code hosting platform, and a compromised GitHub account is not just a personal security problem -- it is a supply chain risk. Attackers who gain access to a developer's GitHub account can inject malicious code into repositories that thousands or millions of people depend on, steal proprietary source code, exfiltrate secrets stored in repository settings, and pivot to compromising downstream users and organizations. GitHub recognized this threat by requiring two-factor authentication for all contributing users as of 2024. This guide ensures you set it up correctly. For a comprehensive overview of 2FA concepts, see our [complete guide to two-factor authentication](/two-factor-authentication/).

## Why Your GitHub Account Needs 2FA

The stakes for GitHub account security extend far beyond your personal data:

- **Supply chain attacks** are among the most devastating in cybersecurity. An attacker who controls a contributor's account can push malicious code to popular open-source libraries, affecting every project and application that depends on them. A single compromised maintainer account can cascade into thousands of downstream breaches.
- **Private repository access** means proprietary source code, trade secrets, internal documentation, and business logic can be stolen.
- **Repository secrets** including API keys, database credentials, deployment tokens, and environment variables stored in GitHub Actions secrets become accessible.
- **Organization access** is compromised if your account belongs to a GitHub organization. The attacker inherits whatever permissions your account has across the organization's repositories.
- **Commit signing trust** is undermined. If an attacker pushes code from your account, those commits appear to come from you, and other contributors may not question them.

GitHub itself has been transparent about the threat. The 2024 mandate requiring 2FA for all contributors was driven by documented incidents where compromised accounts were used to inject malicious code into widely-used packages.

## 2FA Options Available on GitHub

GitHub offers the most comprehensive set of 2FA options of any major platform:

**Authenticator app (TOTP)** -- The recommended method for most users. Any TOTP-compatible app or password manager works. GitHub generates standard TOTP secrets compatible with Google Authenticator, Authy, PanicVault, and all other standard apps. See our [best authenticator apps guide](/two-factor-authentication/best-authenticator-apps/) for recommendations.

**Security keys (FIDO2/WebAuthn)** -- Hardware security keys like YubiKey provide the strongest protection against phishing. The key must be physically present during authentication, making remote attacks nearly impossible. For a comparison, see our article on [hardware keys vs. TOTP](/two-factor-authentication/hardware-keys-vs-totp/).

**GitHub Mobile** -- The GitHub Mobile app can send push notifications for login approval. You tap "Approve" on your phone instead of entering a code. This is convenient but ties your 2FA to a specific app on a specific device.

**SMS** -- GitHub supports SMS-based codes as a 2FA method. It is the least secure option and should be used only as a backup. See our [TOTP vs. SMS comparison](/two-factor-authentication/totp-vs-sms/) for the security trade-offs.

**Passkeys** -- GitHub also supports passkeys (a newer FIDO2-based standard), which combine the security of hardware keys with the convenience of biometric authentication on supported devices.

## Step-by-Step Setup on the Web

**Step 1: Sign in and go to Settings.** Log in to [github.com](https://github.com) and click your profile photo in the top-right corner. Select "Settings" from the dropdown menu.

**Step 2: Navigate to Password and authentication.** In the left sidebar, under the "Access" section, click "Password and authentication."

**Step 3: Click Enable two-factor authentication.** In the Two-factor authentication section, click the green "Enable two-factor authentication" button. If you already have 2FA enabled and want to change methods, you will see options to reconfigure instead.

**Step 4: Choose your method.** GitHub will present the option to set up using an authenticator app. Select "Set up using an app."

**Step 5: Save your recovery codes.** Before showing you the QR code, GitHub displays your recovery codes. This is important -- GitHub shows these first because they want you to save them before proceeding. Download them, copy them, or store them in your password manager. Each code is single-use and allows you to bypass 2FA in an emergency. Click "I have saved my recovery codes" to continue.

**Step 6: Scan the QR code.** GitHub displays a QR code and a text-based setup key. Open your authenticator app or password manager and scan the QR code. Alternatively, click "enter this text code" to see the secret key you can type manually.

**Step 7: Enter the verification code.** Type the six-digit code currently displayed in your authenticator app and click "Verify."

**Step 8: Confirmation.** GitHub confirms that 2FA is now enabled. You will see options to configure additional methods (SMS, security keys) if desired.

## Step-by-Step Setup on the Mobile App

GitHub Mobile does not have a full settings interface for 2FA setup. The recommended approach is to use a mobile browser:

**Step 1: Open a mobile browser.** Navigate to [github.com](https://github.com) in Safari, Chrome, or your preferred browser and sign in.

**Step 2: Access settings.** Tap your profile photo and select "Settings." Then tap "Password and authentication."

**Step 3: Follow the web setup steps.** The mobile web interface mirrors the desktop flow: enable 2FA, save recovery codes, scan the QR code (or copy the manual key if your authenticator is on the same device), enter the verification code, and confirm.

**Step 4: Configure GitHub Mobile as an additional method (optional).** After enabling TOTP, install the GitHub Mobile app (if not already installed), sign in, and GitHub will automatically recognize it as an additional 2FA method for push-based authentication.

## Configuring Additional 2FA Methods

GitHub allows you to configure multiple 2FA methods simultaneously. After your primary TOTP setup, consider adding:

**A security key** for phishing-resistant authentication. Go to Settings → Password and authentication → Security keys → Register new security key. Insert your hardware key, give it a name, and complete the registration. You can register multiple keys for redundancy.

**SMS as a fallback** for emergency access. Go to Settings → Password and authentication → SMS/Text message → Add a phone number. This should be a backup, not your primary method.

Having multiple methods configured means you always have a fallback. If your authenticator app is unavailable, you can use your security key. If your security key is at home, you can use SMS. Redundancy prevents lockouts.

## Why TOTP (or a Security Key) Should Be Your Primary Method

GitHub's 2FA requirement means you must pick a method. The choice matters significantly.

**TOTP** generates codes locally on your device. They cannot be intercepted in transit because they never travel over a network. An attacker needs access to your device or your TOTP secret to generate valid codes. For the vast majority of developers, TOTP strikes the ideal balance of security and convenience.

**Security keys** provide even stronger protection. They are immune to phishing attacks because the key cryptographically verifies the website you are authenticating to. Even if you are tricked into visiting a phishing site that looks exactly like GitHub, the security key will not authenticate because the domain does not match. If you contribute to high-profile or critical open-source projects, a security key is worth the investment.

**SMS** should be avoided as a primary method. [SIM swapping attacks](/two-factor-authentication/sim-swapping/) and SS7 network vulnerabilities make SMS codes interceptable. For a developer account with access to production repositories and deployment secrets, this risk is unacceptable.

## Saving Your Recovery Codes

GitHub provides recovery codes at the beginning of the 2FA setup process -- before you even configure your authenticator. This ordering is intentional: GitHub wants to make sure you have a recovery path before you activate 2FA.

Treat these codes with the same seriousness as your SSH keys or deployment credentials:

- **Store them in your password manager** as a secure note attached to your GitHub entry
- **Do not commit them to a repository**, even a private one
- **Do not store them in a GitHub Gist** -- if your account is compromised, those codes are accessible too
- **Regenerate them periodically** from Settings → Password and authentication → Recovery codes → Generate new recovery codes. This invalidates all previous codes.
- **Check your remaining codes** regularly. If you have used several, generate a fresh set before you run out.

For more guidance, see our comprehensive [recovery codes guide](/two-factor-authentication/recovery-codes/).

## Using a Password Manager for TOTP Codes

Storing your GitHub TOTP secret in a password manager like PanicVault provides the best combination of security and reliability for developer workflows. When you scan GitHub's QR code with your password manager, it generates your six-digit codes alongside your stored credentials.

For developers, this approach has specific advantages:

- **Consistent workflow.** Developers authenticate to GitHub constantly -- pushing code, reviewing pull requests, managing CI/CD pipelines. Having your password and TOTP code in the same manager reduces friction across dozens of daily authentications.
- **Multi-device access.** You may code on a desktop, a laptop, and occasionally a tablet. A password manager that syncs across devices means your GitHub 2FA codes are available wherever you work, without carrying a separate device.
- **Team onboarding and offboarding.** If you manage shared GitHub credentials for CI/CD service accounts (which should have 2FA enabled too), storing those TOTP codes in a team password manager simplifies access management.
- **Encrypted backup.** A lost laptop or a broken phone does not mean losing access to your GitHub account. Your TOTP codes survive because they are encrypted and synced in your password vault.

Developer accounts often have access to sensitive repositories, deployment secrets, and organizational resources. The reliability of TOTP code access is critical -- being locked out of GitHub during a production incident is not acceptable. A password manager with cross-device sync provides that reliability.

For detailed setup instructions and the security trade-off analysis, see our guide on [using your password manager as an authenticator](/two-factor-authentication/password-manager-as-authenticator/).

## Related Articles

- [What Is Two-Factor Authentication and Why You Need It](/two-factor-authentication/what-is-2fa/)
- [Hardware Security Keys vs. TOTP: Which Is More Secure?](/two-factor-authentication/hardware-keys-vs-totp/)
- [The Best Authenticator Apps in 2026](/two-factor-authentication/best-authenticator-apps/)
- [How to Use Your Password Manager as an Authenticator](/two-factor-authentication/password-manager-as-authenticator/)
- [Understanding Recovery Codes: Your 2FA Safety Net](/two-factor-authentication/recovery-codes/)
