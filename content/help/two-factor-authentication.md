---
title: "Two-Factor Authentication (TOTP)"
description: "Set up TOTP two-factor codes in PanicVault by scanning a QR code or entering a Base32 secret, and view live codes next to your passwords."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "2FA & Passkeys"
weight: 90
---

PanicVault can generate time-based one-time passwords (TOTP) for your accounts that support two-factor authentication. This means you can keep your 2FA codes right alongside your passwords. This page explains how TOTP works, how to add a secret to an entry, and which storage formats PanicVault understands.

## How TOTP Works

TOTP generates a short numeric code (usually 6 digits) that changes every 30 seconds. When you log in to a service that requires 2FA, you enter this code along with your password. PanicVault generates these codes automatically from a shared secret.

## Setting Up TOTP for an Entry

1. Edit the entry
2. Scroll to the **One-Time Password** section
3. Add the TOTP secret using one of these methods:
   - **Scan QR Code** (iOS only) -- tap **Scan QR Code** to open the camera and point it at the QR code shown by the service. PanicVault reads the code and fills in all TOTP settings automatically.
   - **Manual entry** -- enter the TOTP secret in Base32 format. This is the text code shown by the service, often available via a "Can't scan?" or "Manual entry" link near the QR code.
4. Adjust the settings if needed (most services use the defaults):
   - **Period**: 15, 30, or 60 seconds (default: 30)
   - **Digits**: 6, 7, or 8 (default: 6)
   - **Algorithm**: SHA1, SHA256, or SHA512 (default: SHA1)
5. A live preview of the current code appears if the secret is valid
6. Tap **Save**

{{< callout type="tip" >}}
Scanning the QR code is the easiest way to set up TOTP on iOS. The QR code contains all the necessary information, including the secret, issuer, and account name.
{{< /callout >}}

## Viewing and Copying TOTP Codes

Once TOTP is configured for an entry, the detail view shows:

- The current 6-digit (or 7 or 8-digit) code in large text
- A countdown indicator showing how many seconds remain before the code changes
- The issuer and account name (if available)

Tap the code to copy it to your clipboard.

## Supported TOTP Formats

PanicVault supports multiple TOTP storage formats for compatibility with other KeePass applications:

- **otpauth:// URI** (KeePassXC format) -- stored in the `otp` custom field
- **TOTP Seed + TOTP Settings** (KeeTrayTOTP / KeePass plugin format)
- **TimeOtp-\* fields** (KeePass native TOTP format) -- supports Base32, Base64, and Hex-encoded secrets

When you set up TOTP in PanicVault, it saves the secret in the standard otpauth:// URI format for maximum compatibility.

TOTP secrets can also arrive with a CSV import -- see [Importing Passwords](/help/importing-passwords/). For more on working with other KeePass clients, see [KeePass Compatibility](/help/keepass-compatibility/).
