---
title: "Managing Your Vault"
description: "Unlock and lock your PanicVault vault, navigate the entry list, search, understand auto-lock behavior, and delete a vault safely."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Getting Started"
weight: 20
---

Once a vault exists, day-to-day use comes down to unlocking it, working in the entry list, and letting it lock itself again. This page covers all of that, plus how to remove a vault when you no longer need it.

## Unlocking Your Vault

Tap a vault on the home screen to open the lock screen. You have two ways to unlock:

- **Master password** — type your master password and tap Unlock
- **Biometric unlock** — if you have enabled Face ID or Touch ID in Settings, PanicVault prompts you automatically. You can also tap the biometric button below the password field

If biometric unlock fails or your master password is required (see [Master Password Re-entry](/help/security-and-settings/) in Settings), you can always fall back to your master password.

{{< callout type="tip" >}}
If you enter the wrong password three or more times, PanicVault shows an extended error message reminding you to double-check your master password.
{{< /callout >}}

## Locking Your Vault

You can lock your vault at any time:

- **iOS**: Tap the lock icon in the top-right toolbar
- **Mac**: Click the lock icon in the sidebar toolbar, or use the keyboard shortcut **Cmd+L**

Your vault also locks automatically when:

- The lock timeout expires after you leave the app (see Auto-Lock Behavior below)
- The auto-lock timeout expires after a period of inactivity within the app

## The Entry List

Once your vault is unlocked, you see the entry list. This is your main workspace:

- **iOS**: A single list with group filter chips at the top. Tap "All" to see every entry, or tap a group name to filter.
- **Mac**: A three-column layout — groups on the left, entries in the middle, and entry details on the right.

Each entry row shows the title, username, and an icon. You can quickly copy a password by:

- **iOS**: Swipe right on an entry and tap "Copy Password"
- **Mac**: Right-click an entry and choose "Copy Password"

## Searching for Entries

Use the search bar to find entries across your entire vault. The search checks titles, usernames, URLs, and notes. On Mac, use **Cmd+F** to jump to the search field.

## Auto-Lock Behavior

PanicVault locks your vault to protect your data when you are not actively using it:

- **Background timer** — when you switch to another app, a countdown starts based on your Lock Timeout setting. If you return to PanicVault before the timer expires, the vault stays unlocked. If the timer runs out while the app is in the background, the vault locks.
- **Idle timer** — if you leave the app open but idle, the vault locks after the configured timeout.
- The vault never auto-locks while you are actively using the app.
- You can change the timeout in [Settings](/help/security-and-settings/) (30 seconds, 1 minute, 2 minutes, 5 minutes, or Never).

## Deleting a Vault

Long-press a vault card on the home screen and choose **Delete**. PanicVault asks what you want to do:

- **Remove from App** — removes the vault from PanicVault but leaves the .kdbx file on disk (or in iCloud Drive / Google Drive). You can re-add it later by opening it again.
- **Delete File Too** — permanently deletes the vault file from disk. PanicVault asks you to type **DELETE** to confirm. This action cannot be undone.

{{< callout type="warning" >}}
If you choose "Delete File Too", the .kdbx file is permanently removed. Make sure you have a backup if you might need the data in the future.
{{< /callout >}}
