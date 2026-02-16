---
title: "PanicVault Browser Extension for Mac"
description: "Fill passwords, usernames, and TOTP codes directly in Chrome, Brave, Edge, Arc, and other Chromium browsers using Touch ID with the PanicVault browser extension."
date: 2026-02-16
lastmod: 2026-02-16
draft: false
silo: "Browser Extension"
---

PanicVault includes a browser extension for Chromium-based browsers -- Google Chrome, Brave, Microsoft Edge, Arc, and Chromium -- that lets you fill passwords, usernames, and TOTP codes directly in web pages using Touch ID.

## What It Does

The browser extension connects to a small helper program on your Mac. When you visit a login page:

- A dropdown appears on focused login fields showing matching credentials from your vault
- Authenticate with Touch ID to unlock your credentials
- Click a credential to fill the username and password fields automatically
- TOTP codes are available for accounts with [two-factor authentication](/two-factor-authentication/) configured
- Passkey authentication is supported for sites that use [WebAuthn](/passkeys/how-passkeys-work/)

The extension works entirely locally. Your passwords never leave your Mac or pass through any external server.

## Installing the Browser Helper

The browser helper is a separate download that is not included in the Mac App Store version of PanicVault.

1. Open **Settings** in PanicVault and click **Download Browser Helper** in the Browser Extension section
2. This downloads a macOS installer (.pkg file) to your Downloads folder
3. Open the downloaded installer and follow the prompts
4. The installer places the helper in the correct location and configures it for all your installed browsers automatically

No terminal commands or scripts are required. The installer handles everything.

You can also download the installer directly: [Download PanicVaultBrowserHelper.pkg](/PanicVaultBrowserHelper.pkg)

## Installing the Extension

After installing the helper, add the PanicVault extension to your browser:

1. Open the Chrome Web Store and search for "PanicVault"
2. Click **Add to Chrome** (or **Add to Brave**, **Add to Edge**, etc.)
3. The PanicVault icon appears in your browser toolbar

The extension works with Chrome, Brave, Edge, Arc, and other Chromium-based browsers. All of these browsers use the Chrome Web Store for extensions.

## Using the Extension

### Inline Dropdown

When you focus a login field on any web page, a small PanicVault dropdown appears below the field.

1. If you are not authenticated, click **Unlock with Touch ID** and verify with your fingerprint
2. The dropdown shows credentials matching the current website
3. Click a credential to fill the username and password fields
4. The dropdown dismisses automatically after filling

### Popup

Click the PanicVault icon in the browser toolbar to open the full popup.

1. Click **Unlock with Touch ID** to authenticate
2. Search or browse your credentials
3. Click a credential to fill it in the active page
4. Click the TOTP badge to view and copy the current code

### Filling TOTP Codes

For accounts with two-factor authentication:

1. After filling your username and password, the site shows a TOTP or verification code field
2. Open the PanicVault popup and click the TOTP badge on the credential
3. Copy the code or click **Fill Code** to enter it automatically

## Troubleshooting

### Helper Not Found

If the extension shows "PanicVault helper not found" when you click Unlock:

- Re-download and run the installer from Settings > Browser Extension
- Verify that `~/Library/Application Support/PanicVault/PanicVaultChromeHelper` exists on disk

### Extension Not Detected After Install

Restart your browser after installing the helper. The browser reads native messaging manifests at startup and will not detect the helper until the next launch.

### Touch ID Fails or Is Not Prompted

The helper uses the macOS Keychain to access your vault key. Make sure:

- You have unlocked your vault at least once in the PanicVault app with your master password
- Touch ID is enabled in PanicVault settings
- Your Mac has a Touch ID sensor or an Apple Watch configured for authentication

### No Credentials Shown

The extension matches credentials by URL. Make sure:

- Your entries in PanicVault have a URL field that matches the website you are visiting
- The vault has been unlocked at least once in the current session

## Uninstalling the Browser Helper

To remove the browser helper and all its configuration:

1. Download the uninstaller: [PanicVaultBrowserHelper-Uninstall.pkg](/PanicVaultBrowserHelper-Uninstall.pkg)
2. Open the downloaded file and follow the prompts

This removes the helper binary, all native messaging manifests, and the package receipt. Restart your browser afterward. The Chrome extension can be removed separately from your browser's extensions page.
