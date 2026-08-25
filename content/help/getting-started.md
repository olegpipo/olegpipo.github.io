---
title: "Getting Started"
description: "Create your first PanicVault vault, open an existing .kdbx file, set a default vault, and choose a strong master password."
date: 2026-07-14
lastmod: 2026-08-25
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
7. Optionally, in the **Hardware Key (Optional)** section, turn on **Protect with a YubiKey** to require a physical YubiKey in addition to your master password. Be sure you have a backup key first — see [Hardware Keys (YubiKey)](/help/hardware-keys/).
8. Tap **Create Vault**

Your new vault opens automatically and you can start adding entries right away.

For more on the two cloud options, see [iCloud Drive Sync](/help/icloud-drive-sync/) and [Google Drive Sync](/help/google-drive-sync/).

## Opening an Existing Vault

If you already have a .kdbx file (from KeePass, KeePassXC, or another compatible app):

1. Tap the "+" card on the home screen
2. Choose **Open Existing Vault**
3. Browse to your .kdbx file and select it
4. The vault appears on your home screen — tap it to unlock with your master password

This is the system file browser, so it reaches everywhere your device can see: iCloud Drive, "On My iPhone", folders on your Mac, an external drive, or another storage app such as Dropbox. When you are signed in to iCloud it opens in your **PanicVault** folder in iCloud Drive — where vaults you create on iCloud Drive are kept — and you can navigate anywhere else from there.

PanicVault works with the file where it already lives instead of copying it, and a .kdbx it finds anywhere in your iCloud Drive is recorded as an iCloud vault with full sync handling. See [Vaults Kept Elsewhere in iCloud Drive](/help/icloud-drive-sync/#vaults-kept-elsewhere-in-icloud-drive).

If the vault is one iCloud has moved off the device to save space, PanicVault fetches it before adding it; should that take longer than a moment it tells you the vault **hasn't finished downloading from iCloud** — let the download finish in Files or the Finder, then open it again.

If you are signed in to Google Drive, the same menu also offers **Open from Google Drive**, which downloads a copy of a vault from your Google Drive.

{{< callout type="note" >}}
If the file is already one of your vaults, PanicVault opens the vault you already have rather than adding a second card for the same file.
{{< /callout >}}

Coming from another password manager without a .kdbx file? See [Importing Passwords](/help/importing-passwords/) to bring your logins in from a CSV export instead.

## Opening a .kdbx File Directly

You do not have to start in PanicVault. PanicVault registers itself with the system as a KeePass database handler, so a .kdbx file you find anywhere on your device can be opened straight into the app:

- **Files app (iPhone, iPad)** — tap the file, or press and hold it and choose **Share**, then **PanicVault**
- **Finder (Mac)** — double-click the file, or Control-click it and choose **Open With**, then **PanicVault**
- **Mail, Messages, or AirDrop** — tap or click the attachment and choose PanicVault

The vault is added to your home screen and its lock screen appears right away, ready for your master password. Vaults PanicVault created show the PanicVault document icon; a .kdbx written by another KeePass app keeps that app's icon, but PanicVault is still offered under Open With.

{{< callout type="note" >}}
PanicVault opens the file in place. It works with the original file where it already lives — in iCloud Drive, in a folder on your Mac, in another app's storage — rather than making a copy, so nothing gets out of step with the vault you sync elsewhere.
{{< /callout >}}

If the file is already one of your vaults, PanicVault opens that vault instead of adding a second copy of it to your home screen. If a different vault is unlocked at the time, it is locked first, exactly as when you tap another vault on the home screen.

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
