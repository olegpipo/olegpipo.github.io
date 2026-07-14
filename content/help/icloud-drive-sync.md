---
title: "iCloud Drive Sync"
description: "Store PanicVault vaults on iCloud Drive to sync them across your Apple devices, with automatic entry-level merging and conflict resolution."
date: 2026-07-14
lastmod: 2026-07-14
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

1. Tap the "+" card on the home screen
2. Choose **Open from iCloud Drive** (only visible when iCloud is available)
3. Browse through your iCloud Drive folders to find .kdbx files
4. Each file shows its name and how recently it was modified
5. Select a file to add it to PanicVault

## How Sync Works

iCloud Drive vaults sync automatically using entry-level merging, the same intelligent system used for Google Drive. Changes from multiple devices are merged at the entry level so that edits from both sides are preserved.

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

Your vault files are stored in the PanicVault folder inside iCloud Drive and are visible in the Files app on iOS and the Finder on Mac.

{{< callout type="warning" >}}
You should not rename or move these files outside of PanicVault, as this may break the bookmark that PanicVault uses to locate the file.
{{< /callout >}}
