---
title: "Browser Extension for Mac"
description: "Install the PanicVault browser extension and helper to fill passwords, usernames, TOTP codes, and passkeys in Chrome, Brave, Edge, and Arc with Touch ID."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Filling Passwords"
weight: 140
---

PanicVault includes a browser extension for Chromium-based browsers (Google Chrome, Brave, Microsoft Edge, Arc, and Chromium) that lets you fill passwords, usernames, and TOTP codes directly in web pages using Touch ID. This page walks through what the extension does, how to install the helper and the extension, how to use them day to day, and how to fix the most common problems.

## What It Does

The browser extension connects to a small helper program on your Mac. When you visit a login page:

- A dropdown appears on focused login fields showing matching credentials from your vault
- Authenticate with Touch ID to unlock your credentials
- Click a credential to fill the username and password fields automatically
- TOTP codes are available for accounts with [two-factor authentication](/help/two-factor-authentication/) configured
- [Passkey](/help/passkeys/) authentication is supported for sites that use WebAuthn

The extension works entirely locally — your passwords never leave your Mac or pass through any external server.

## Installing the Browser Helper

The browser helper is a separate download (not included in the Mac App Store version):

1. Go to **Settings** in PanicVault and click **Download Browser Helper** in the Browser Extension section — you can also get it from the [Browser Helper page](/browser-helper/)
2. This downloads a macOS installer (.pkg file) to your Downloads folder
3. Open the downloaded installer and follow the prompts
4. The installer places the helper in the correct location and configures it for all your installed browsers automatically

No terminal commands or scripts are required — the installer handles everything for you.

## Installing the Extension

After installing the helper, add the PanicVault extension to your browser:

1. Open the Chrome Web Store and search for "PanicVault"
2. Click **Add to Chrome** (or **Add to Brave**, **Add to Edge**, etc.)
3. The PanicVault icon appears in your browser toolbar

{{< callout type="note" >}}
The extension works with Chrome, Brave, Edge, Arc, and other Chromium-based browsers. All of these browsers use the Chrome Web Store for extensions.
{{< /callout >}}

## Using the Extension

### Inline Dropdown

When you focus a login field on any web page, a small PanicVault dropdown appears below the field:

1. If you are not authenticated, click **Unlock with Touch ID** and verify with your fingerprint
2. The dropdown shows credentials matching the current website
3. Click a credential to fill the username and password fields
4. The dropdown dismisses automatically after filling

### Popup

Click the PanicVault icon in the browser toolbar to open the full popup:

1. Click **Unlock with Touch ID** to authenticate
2. Search or browse your credentials
3. Click a credential to fill it in the active page
4. Click the TOTP badge to view and copy the current code

### Filling TOTP Codes

For accounts with two-factor authentication:

1. After filling your username and password, the site shows a TOTP/verification code field
2. Open the PanicVault popup and click the TOTP badge on the credential
3. Copy the code or click **Fill Code** to enter it automatically

## Troubleshooting

**Helper not found**: If the extension shows "PanicVault helper not found" when you click Unlock:

- Re-download and run the installer from Settings → Browser Extension
- Check that `~/Library/Application Support/PanicVault/PanicVaultChromeHelper` exists

**Extension not detected after install**: Restart your browser after installing the helper. The browser reads native messaging manifests at startup.

**Touch ID fails or is not prompted**: The helper uses the macOS Keychain to access your vault key. Make sure:

- You have unlocked your vault at least once in the PanicVault app with your master password
- Touch ID is enabled in PanicVault settings
- Your Mac has a Touch ID sensor or an Apple Watch configured for authentication

**No credentials shown**: The extension matches credentials by URL. Make sure:

- Your [entries](/help/entries/) in PanicVault have a URL field that matches the website you are visiting
- The vault has been unlocked at least once in the current session

## Uninstalling the Browser Helper

To remove the browser helper and all its configuration:

1. Download the uninstaller from the same page as the helper installer
2. Open **PanicVaultBrowserHelper-Uninstall.pkg** and follow the prompts

This removes the helper binary, all native messaging manifests, and the package receipt. Restart your browser afterward. The Chrome extension can be removed separately from your browser's extensions page.
