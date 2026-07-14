---
title: "Getting Started"
description: "Create your first PanicVault vault, open an existing .kdbx file, set a default vault, and choose a strong master password."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Getting Started"
weight: 10
---

This page walks you through your first minutes with PanicVault: the home screen, creating a new vault, opening a .kdbx file you already have, and picking a master password that will actually protect it.

## The Home Screen

When you open PanicVault, you see the home screen. This shows all your saved vaults as cards. Each card displays the vault name, number of entries, storage type (local, iCloud Drive, or Google Drive), and the last sync time for cloud vaults.

From here you can:

- Tap a vault card to open and unlock it
- Tap the "+" card to create or import a vault
- Long-press a vault card to set it as default or delete it
- Tap the gear icon to open Settings

## Default Vault

You can designate one vault as your default vault. Long-press a vault card on the home screen and choose **Set as Default**. The default vault is marked with a star on its card and opens automatically when you launch PanicVault, saving you a tap every time you open the app. To clear the default, long-press the default vault again and choose **Remove Default**.

## Creating Your First Vault

1. Tap the "+" card on the home screen
2. Choose **Create New Vault**
3. Enter a name for your vault (for example, "Personal" or "Work")
4. Choose a strong master password and confirm it — a strength meter shows you how strong your password is
5. Choose a storage location:
   - **Local** — the vault is stored on your device only
   - **iCloud Drive** — the vault is synced via iCloud Drive across your Apple devices (requires iCloud sign-in in system settings)
   - **Google Drive** — the vault is stored locally and synced to your Google Drive (you must sign in to Google first in Settings)
6. For iCloud Drive, you can optionally choose a folder within your iCloud Drive using the folder picker. You can also create new folders from the picker.
7. Tap **Create Vault**

Your new vault opens automatically and you can start adding entries right away.

For more on the two cloud options, see [iCloud Drive Sync](/help/icloud-drive-sync/) and [Google Drive Sync](/help/google-drive-sync/).

## Opening an Existing Vault

If you already have a .kdbx file (from KeePass, KeePassXC, or another compatible app):

1. Tap the "+" card on the home screen
2. Choose **Open Existing Vault**
3. Browse to your .kdbx file and select it
4. The vault appears on your home screen — tap it to unlock with your master password

If iCloud Drive is available, you also see an **Open from iCloud Drive** option that lets you browse your iCloud Drive folders for .kdbx files. If you are signed in to Google Drive, you see an **Open from Google Drive** option as well.

Coming from another password manager without a .kdbx file? See [Importing Passwords](/help/importing-passwords/) to bring your logins in from a CSV export instead.

## Choosing a Strong Master Password

Your master password is the single key that protects all your other passwords. Choose it carefully:

- Use at least 12 characters, ideally more
- Mix uppercase letters, lowercase letters, numbers, and symbols
- Consider using a passphrase — several random words joined together (for example, "correct-horse-battery-staple")
- Never reuse your master password for any other account
- The strength meter on the create screen shows you whether your password is Weak, Fair, Strong, or Excellent

{{< callout type="tip" >}}
You can use PanicVault's built-in [password generator](/help/password-generator/) to create a strong passphrase for your master password. Write it down and store it somewhere physically safe until you have it memorized.
{{< /callout >}}
