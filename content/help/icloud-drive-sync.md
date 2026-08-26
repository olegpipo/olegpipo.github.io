---
title: "iCloud Drive Sync"
description: "Store PanicVault vaults on iCloud Drive to sync them across your Apple devices, with automatic entry-level merging and conflict resolution."
date: 2026-07-14
lastmod: 2026-08-26
draft: false
silo: "User Manual"
helpgroup: "Sync"
weight: 110
---

PanicVault can store and sync your vaults using iCloud Drive, keeping them available across all your Apple devices without any additional setup. This page covers the requirements, how to create and open iCloud vaults, and how syncing and conflicts are handled.

## Requirements

iCloud Drive sync requires that you are signed in to iCloud in your device's system settings. PanicVault does not require any in-app sign-in -- it uses your system iCloud account automatically. The Settings screen shows whether iCloud Drive is "Available" or "Not Available".

## Creating Vaults on iCloud Drive

When creating a new vault, choose **iCloud Drive** as the storage location. You can then pick a folder within your iCloud Drive using the folder picker, or use the Documents root. You can also create new folders directly from the picker.

The vault is created locally and then copied to iCloud Drive. After that, the operating system handles uploading and downloading changes in the background.

## Opening Vaults from iCloud Drive

A vault in iCloud Drive is opened the same way as any other vault:

1. Tap the "+" card on the home screen
2. Choose **Open Existing Vault**
3. Pick the .kdbx file and it is added to PanicVault

When you are signed in to iCloud, the file browser opens in your **PanicVault** folder in iCloud Drive, so a vault you created there is right in front of you. If your vault lives in a different iCloud Drive folder, navigate to it in the same browser -- it is recognised as an iCloud vault either way.

You can also open a vault straight from the Files app or the Finder; see [iCloud Drive and the Files App](#icloud-drive-and-the-files-app) below.

If iCloud has moved a vault off the device to save space, PanicVault fetches it when you unlock and the lock screen says **Downloading from iCloud...** while it does. Should it take longer than a moment, it tells you the vault **hasn't finished downloading from iCloud** -- let the download finish in Files or the Finder, then unlock again.

## How Sync Works

iCloud Drive vaults sync automatically using entry-level merging, the same intelligent system used for Google Drive. Changes from multiple devices are merged at the entry level so that edits from both sides are preserved.

- **On unlock**: The vault file is read once, through file coordination, so you never open a copy that iCloud was halfway through replacing with another device's version. If iCloud has moved the vault off the device, it is fetched first and the lock screen says **Downloading from iCloud...** while you wait.
- **On save**: When you save changes, the file is written to iCloud Drive using file coordination. The operating system handles uploading the file to iCloud in the background.
- **On app activation**: When PanicVault returns to the foreground, it checks all iCloud vaults for remote changes. If the unlocked vault has new remote changes, they are merged automatically.
- **Background monitoring**: PanicVault uses the system metadata query API to detect when iCloud Drive files change. Changes are debounced to avoid rapid repeated syncs, and the app ignores notifications caused by its own recent writes.

The entry-by-entry merge rules are the same ones documented under [Google Drive Sync](/help/google-drive-sync/).

## Handling Sync Conflicts

Conflicts are handled the same way as Google Drive vaults. When the same entry has been modified on two different devices since the last sync, PanicVault shows a conflict resolution screen where you choose which version to keep for each conflicting entry. You can also use the "Keep All Local" or "Keep All Remote" bulk actions.

## Sync Status Indicators

The vault card on the home screen shows the current sync state:

- A **sync spinner** when syncing is in progress
- An **orange exclamation cloud** if sync failed or is pending
- A **blue merge icon** if remote changes need merging
- The **last synced time** displayed below the vault name

## iCloud Drive and the Files App

Vaults you create on iCloud Drive are stored in a **PanicVault** folder inside iCloud Drive, which appears alongside your other apps' folders in the Files app on iPhone and iPad and under iCloud Drive in the Finder on Mac. You can browse it, and any subfolders you created from the folder picker, like any other iCloud Drive folder.

The folder can take a moment to show up: iCloud publishes it the first time the app syncs after being installed or updated, so it may not be there the instant the app finishes installing. On Mac, the Finder only lists the folder once it holds at least one file -- create or copy a vault into it and it appears.

Vaults in that folder carry the PanicVault document icon, and you can open one straight from there: tap it in the Files app, or double-click it in the Finder, and PanicVault opens with that vault's lock screen. See [Opening a .kdbx File Directly](/help/getting-started/#opening-a-kdbx-file-directly) for the other places this works.

{{< callout type="warning" >}}
You should not rename or move vault files outside of PanicVault, as this may break the bookmark that PanicVault uses to locate the file.
{{< /callout >}}

## Vaults Kept Elsewhere in iCloud Drive

You do not have to keep your vault in the PanicVault folder. If you open a .kdbx file that already lives somewhere in your iCloud Drive -- with **Open Existing Vault**, or by tapping it in the Files app -- PanicVault recognises it as an iCloud file and gives it the full iCloud treatment: coordinated reads and writes, automatic download before opening, conflict resolution, and entry-level merging across your devices. The vault card shows it as an iCloud Drive vault.

Files that are not synced by iCloud -- vaults in "On My iPhone", on an external drive, or in a third-party storage provider such as Dropbox -- are still opened as local vaults, and PanicVault leaves their syncing entirely to whatever manages them.

One difference applies to a vault kept outside the PanicVault folder: the system only reports live file-change notifications for the app's own folder, so changes made on another device are picked up when PanicVault comes back to the foreground, when the vault is opened or unlocked, when you save, or when you tap the sync button -- rather than the instant they arrive.
