---
title: "Google Drive Sync"
description: "Connect one or more Google accounts to PanicVault, sync vaults with entry-level merging, resolve conflicts, and work offline with queued syncs."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "Sync"
weight: 120
---

PanicVault can sync your vaults with Google Drive, keeping them available across all your devices. This page covers connecting your account (or several), creating and importing vaults, and exactly how PanicVault merges changes and resolves conflicts.

## Connecting Your Google Account

1. Go to **Settings** (gear icon on the home screen)
2. In the Google Drive section, tap **Sign in with Google**
3. Complete the Google sign-in flow in the browser window that appears
4. Once connected, you see your email address in the Settings

## Multiple Google Drive Accounts

PanicVault supports signing in to multiple Google Drive accounts. Each vault remembers which Google account it is associated with, so you can have some vaults syncing with your personal Google account and others with your work account.

To add another Google account:

1. Go to **Settings**
2. In the Google Drive section, tap **Add Account**
3. Sign in with a different Google account

When you create a new vault with Google Drive storage, you choose which of your signed-in accounts to use. The vault card on the home screen shows which account each vault is synced with.

## Importing Vaults from Google Drive

1. Tap the "+" card on the home screen
2. Choose **Open from Google Drive** (only visible when signed in)
3. Browse your .kdbx files on Google Drive
4. Select a file to download and add it to PanicVault

## Creating Vaults on Google Drive

When creating a new vault, choose **Google Drive** as the storage location. The vault is created locally first and then uploaded to your Google Drive.

## How Sync Works

PanicVault syncs Google Drive vaults using entry-level merging. Instead of replacing the entire file, each entry is compared individually so that changes from both sides are preserved.

- **On app launch**: PanicVault checks all Google Drive vaults for remote changes using MD5 checksums.
- **On unlock**: If the remote vault has changed, PanicVault downloads and decrypts it, then merges it entry-by-entry with your local copy. The merged result is saved locally and uploaded back to Drive.
- **On save**: Before uploading, PanicVault checks whether the remote vault changed since your last sync. If it did, it merges first, then uploads. If not, it uploads directly.
- **Manual sync**: Tap the sync icon in the toolbar to trigger the same merge flow at any time.

The last sync time is shown on the vault card on the home screen.

## How Merging Works

When local and remote vaults differ, PanicVault compares every entry by its unique ID:

- **Only one side changed an entry** -- the changed version wins automatically.
- **New entries on either side** -- added to the merged vault.
- **Entries deleted on one side** (existed at last sync but missing) -- the deletion is honored.
- **Entry moved between groups** -- the move with the more recent timestamp wins.
- **Both sides changed the same entry** -- this is a conflict (see below).

Groups, entry history, attachments, and custom icons are also merged.

## Handling Sync Conflicts

A conflict occurs when the same entry was edited on two devices since the last sync. PanicVault shows a conflict resolution screen that lists each conflicting entry and highlights the fields that differ (title, password, URL, etc.). For each entry you choose:

- **Keep Local** -- use your version of the entry
- **Keep Remote** -- use the other device's version

Once all conflicts are resolved, PanicVault saves the merged vault and uploads it to Drive.

## Offline Behavior

If you are offline when PanicVault tries to sync, the sync is queued automatically. The toolbar shows an exclamation cloud icon to indicate a pending sync. When you reconnect, you can tap the sync icon to retry, or the sync will retry automatically on the next save.

## Choosing a Google Drive Folder

When creating a new vault with Google Drive storage or opening a vault from Google Drive, you can choose which folder to store the vault in. PanicVault shows a folder browser that lets you navigate your Google Drive and select the destination folder. On both iOS and macOS, you can tap the **New Folder** button to create a new folder directly from the folder picker without leaving PanicVault.

## Sync Status Indicators

- A **sync icon** appears in the toolbar for Google Drive vaults
- If sync fails while offline, PanicVault shows an **exclamation cloud** icon and queues the sync for when you reconnect
- The vault card on the home screen shows the last successful sync time

## Signing Out

To disconnect a Google Drive account:

1. Go to **Settings**
2. Tap **Sign Out** next to the account you want to disconnect
3. Confirm

Your vaults remain on your device but will no longer sync with that account. You can sign in again at any time.

If you would rather keep your vaults on Apple's ecosystem, see [iCloud Drive Sync](/help/icloud-drive-sync/), which uses the same entry-level merging.
