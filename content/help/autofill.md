---
title: "AutoFill"
description: "Enable PanicVault as a system AutoFill provider on iOS and Mac to fill usernames and passwords in Safari and apps, across multiple vaults."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Filling Passwords"
weight: 130
---

PanicVault supports the system AutoFill feature to fill usernames and passwords in apps and websites. This page walks through enabling PanicVault as an AutoFill provider on iOS and Mac, and explains how credentials are matched and how multiple vaults behave.

## Setting Up AutoFill on iOS

1. Go to **Settings** in PanicVault
2. Tap **Setup AutoFill...** -- this takes you to your device's Settings
3. Go to **Passwords** > **AutoFill Passwords**
4. Enable AutoFill and select **PanicVault** as a provider

Once enabled, when a login field appears in Safari or any app, your device offers to fill credentials from PanicVault.

## Setting Up AutoFill on Mac

1. Go to **Settings** in PanicVault
2. Click **Open Password Settings...** -- this takes you to System Settings
3. In the Passwords settings, enable PanicVault as an AutoFill provider

## How AutoFill Works

When a login field appears in Safari or another app, your device looks for matching credentials based on the website or app domain. PanicVault matches credentials using the URL field of your entries. If an entry has an **Override URL** set, that URL is also used for matching, so you can handle sites with different login domains.

See [Entries (Passwords)](/help/entries/) for where the URL and Override URL fields live.

## Multi-Vault AutoFill

If you have multiple vaults, credentials from all unlocked vaults are available in AutoFill. When you unlock a vault during a session, its credentials are added to the pool of available suggestions. This means you can keep separate vaults for personal and work accounts and still see all your credentials in QuickType suggestions and the AutoFill credential picker, as long as each vault has been unlocked at least once during the current session.

To fill passwords in Chromium-based browsers on Mac, see the [Browser Extension for Mac](/help/browser-extension/).
