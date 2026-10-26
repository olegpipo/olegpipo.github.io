---
title: "Browser Extension for Mac"
description: "Fill passwords, TOTP codes, and passkeys in Chrome, Brave, Edge, Arc, and Dia, unlocking with Touch ID, Apple Watch, or your Mac login password."
date: 2026-07-14
lastmod: 2026-10-26
draft: false
silo: "User Manual"
helpgroup: "Filling Passwords"
weight: 140
---

PanicVault includes a browser extension for Chromium-based browsers (Google Chrome, Brave, Microsoft Edge, Arc, Dia, and Chromium) that lets you fill passwords, usernames, and TOTP codes directly in web pages, unlocking with Touch ID, your Apple Watch, or your Mac login password. This page walks through what the extension does, how to install the helper and the extension, how to use them day to day, and how to fix the most common problems.

## What It Does

The browser extension connects to a small helper program on your Mac. When you visit a login page:

- A dropdown appears on focused login fields showing matching credentials from your vault
- Unlock your credentials with Touch ID, your Apple Watch, or your Mac login password
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

No terminal commands or scripts are required — the installer handles everything for you. The helper runs on both Apple silicon and Intel Macs.

## Installing the Extension

After installing the helper, add the PanicVault extension to your browser:

1. Open the Chrome Web Store and search for "PanicVault"
2. Click **Add to Chrome** (or **Add to Brave**, **Add to Edge**, etc.)
3. The PanicVault icon appears in your browser toolbar

{{< callout type="note" >}}
The extension works with Chrome, Brave, Edge, Arc, Dia, and other Chromium-based browsers. All of these browsers use the Chrome Web Store for extensions.
{{< /callout >}}

## Using the Extension

### Inline Dropdown

When you focus a login field on any web page, a small PanicVault dropdown appears below the field:

1. If you are not authenticated, click **Unlock with Touch ID**, then verify with Touch ID or your Apple Watch, or choose **Use Password…** to enter your Mac login password
2. The dropdown shows credentials matching the current website
3. Click a credential to fill the username and password fields
4. The dropdown dismisses automatically after filling

### Popup

Click the PanicVault icon in the browser toolbar to open the full popup:

1. Click **Unlock with Touch ID**, then verify with Touch ID or your Apple Watch, or choose **Use Password…** to enter your Mac login password
2. Search or browse your credentials
3. Click a credential to fill it in the active page
4. Click the TOTP badge to view and copy the current code

{{< callout type="note" >}}
On a Mac without Touch ID (or a MacBook with its lid closed), the button keeps its name and macOS asks for your Mac login password directly. Unlocking with your password or an Apple Watch, and on Macs without Touch ID, requires browser helper 1.4 or later.
{{< /callout >}}

### Filling TOTP Codes

For accounts with two-factor authentication:

1. After filling your username and password, the site shows a TOTP/verification code field
2. Open the PanicVault popup and click the TOTP badge on the credential
3. Copy the code or click **Fill Code** to enter it automatically

## Troubleshooting

**Helper not found**: If the extension shows "PanicVault helper not found" when you click Unlock:

- Re-download and run the installer from Settings → Browser Extension
- Check that `~/Library/Application Support/PanicVault/PanicVaultChromeHelper` exists

**"Failed to start native messaging host"**: If the extension reports that the native helper disconnected with this message, or running the helper in Terminal prints "bad CPU type in executable", your installed helper cannot run on this Mac (helper versions before 1.3 ran only on Apple silicon). Install the latest helper (1.3 or later) from Settings → Browser Extension or the [Browser Helper page](/browser-helper/), then restart your browser.

**Extension not detected after install**: Restart your browser after installing the helper. The browser reads native messaging manifests at startup.

**Unlocking fails or you are not prompted**: Unlocking uses the standard macOS prompt: Touch ID (or your Apple Watch) when available, and **Use Password…** for your Mac login password; Macs without Touch ID show the password prompt directly. If choosing **Use Password…** ends with "Authentication failed", or a Mac without Touch ID cannot unlock at all, your helper is older than 1.4: install the latest helper from Settings → Browser Extension or the [Browser Helper page](/browser-helper/), then restart your browser. "Authentication cancelled" only means the prompt was closed; click **Unlock with Touch ID** to try again. Also make sure:

- You have unlocked your vault at least once in the PanicVault app with your master password
- Your Mac user account has a login password (macOS cannot verify you without one)
- To unlock with an Apple Watch, your watch is turned on in the **Apple Watch** section of System Settings → Touch ID & Password

**macOS asks for your login keychain password**: The first time the helper reads your vault key, macOS asks permission with a dialog naming `com.tenpercent.panicvault`. Press **Always Allow** and enter your Mac login password -- **Allow** grants permission only once, so the dialog would return on every fill. If it keeps appearing, open **Keychain Access** (Applications > Utilities), select the **login** keychain, open the `com.tenpercent.panicvault` item, and add the helper on the **Access Control** tab.

**No credentials shown**: The extension matches credentials by URL. Make sure:

- Your [entries](/help/entries/) in PanicVault have a URL field that matches the website you are visiting
- The vault has been unlocked at least once in the current session

## Uninstalling the Browser Helper

To remove the browser helper and all its configuration:

1. Download the uninstaller from the same page as the helper installer
2. Open **PanicVaultBrowserHelper-Uninstall.pkg** and follow the prompts

This removes the helper binary, all native messaging manifests, and the package receipt. Restart your browser afterward. The Chrome extension can be removed separately from your browser's extensions page.
