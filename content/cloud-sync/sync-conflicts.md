---
title: "Resolving Sync Conflicts in Password Databases"
description: "How sync conflicts occur in KeePass password databases, how different apps handle merging, and best practices for avoiding data loss when using multiple devices."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Cloud Sync & Storage"
---

Sync conflicts are the most common operational challenge when using [cloud sync for password databases](/cloud-sync/). They occur when two devices modify the same database file before either device has synced the other's changes. Understanding why conflicts happen, how different KeePass-compatible applications handle them, and how to prevent them saves you from frustration and potential data loss.

This article explains the mechanics of sync conflicts in password databases, surveys how popular KeePass apps deal with them, and provides practical strategies for multi-device usage that minimize or eliminate conflicts entirely.

## How Sync Conflicts Occur

A sync conflict follows a predictable sequence:

1. **Device A** opens the password database and makes a change (adds an entry, modifies a password, deletes a group).
2. **Device B**, before receiving Device A's updated file, also opens and modifies the database.
3. Both devices save their changes and attempt to upload the modified file to cloud storage.
4. The cloud provider detects that two different versions of the same file have been uploaded and must decide what to do.

The core problem is that password databases are single files, not collections of independent records. When you modify one entry and save, the entire .kdbx file is rewritten. From the cloud provider's perspective, two completely different files are competing to replace the same path. The provider cannot examine the encrypted contents to merge them -- it sees only opaque binary data.

### Why This Is Different from Document Sync

Cloud-synced document editors (Google Docs, iCloud Notes) avoid this problem through real-time collaboration protocols. Changes are transmitted as granular operations ("insert character 'a' at position 47") rather than file replacements. Multiple users can edit simultaneously because the sync system understands the document's internal structure.

Password databases cannot use this approach for several reasons:

- **The file is encrypted.** The cloud provider cannot parse the database structure to merge changes at the record level.
- **The format is file-based.** The [KDBX format](/keepass/kdbx-format-guide/) is designed as a standalone encrypted file, not a cloud-native document.
- **Security requires local encryption.** Sending granular unencrypted operations to a cloud service would defeat the purpose of client-side encryption.

This means conflict resolution must happen at the application level, after both conflicting versions have been decrypted locally.

## How Cloud Providers Handle File Conflicts

When a sync conflict occurs, cloud providers typically use one of two strategies:

### Last-Write-Wins

The most recent upload replaces the older version. The older version is silently discarded (or moved to version history, if the provider retains versions). This is the default behavior for most cloud storage services.

**iCloud Drive**: Uses last-write-wins. If two devices upload different versions, the most recent upload wins. iCloud may keep the older version in version history for 30 days, but this is not guaranteed.

**Google Drive**: Uses last-write-wins for most file types. Previous versions are retained in version history (up to 100 versions for 30 days).

**Dropbox**: Detects the conflict and creates a "conflicted copy" file alongside the original. For example, if `database.kdbx` has a conflict, Dropbox creates `database (Pierre's MacBook Pro's conflicted copy 2026-02-13).kdbx`. Both versions are preserved, and the user must resolve the conflict manually.

Dropbox's approach is the most conservative and the safest for password databases: it never silently discards changes. The trade-off is that you must manually reconcile the conflicted copy.

### The Risk of Lost Changes

With last-write-wins (iCloud, Google Drive), changes from the "losing" device are discarded from the active file. If you added three new passwords on your phone and then your laptop's older version overwrites it, those three passwords are gone from the live file. They may exist in the provider's version history, but you might not notice the loss until you need those passwords and cannot find them.

This silent data loss is the primary danger of sync conflicts with password databases.

## How KeePass Applications Handle Conflicts

The KeePass database format includes features that enable intelligent merging at the application level. How effectively these features are used depends on the specific application.

### Built-In Merge Support in the KDBX Format

The KDBX format tracks modification times for every entry and group. Each entry has:

- **Last modification time**: When the entry's content was last changed.
- **Creation time**: When the entry was first created.
- **Location changed time**: When the entry was moved between groups.
- **Usage count and last access time**: When the entry was last accessed.
- **History**: Previous versions of the entry stored within the database.

This metadata enables a merge algorithm: when two versions of the same database diverge, a compatible application can compare entries by UUID, determine which version of each entry is newer based on modification timestamps, and merge the two databases into a single consistent result.

### KeePassXC

KeePassXC (desktop, available for macOS, Windows, and Linux) has robust merge support. When KeePassXC detects that the database file on disk has changed while it is open in memory (indicating that another device synced a newer version), it can:

1. **Prompt the user** to reload the file, merge changes, or keep the in-memory version.
2. **Merge automatically** by comparing entries by UUID and keeping the most recently modified version of each entry.
3. **Preserve history** -- older versions of entries are kept in the entry history within the database.

KeePassXC's merge is entry-level, not field-level. If you change an entry's password on Device A and the same entry's notes on Device B, the merge will keep the version of the entire entry that was modified most recently, not combine the two changes. The older change is preserved in entry history but requires manual recovery.

### PanicVault and iOS KeePass Apps

KeePass-compatible apps on iOS and iPadOS vary in their merge capabilities. Some apps detect when the cloud file has changed and offer to merge or reload. Others simply overwrite the local copy with the cloud version (or vice versa) without merge logic.

When using [iCloud sync](/cloud-sync/icloud-sync/) or [Google Drive sync](/cloud-sync/google-drive-sync/) with an iOS app, understanding how your specific app handles conflicts is essential. Check your app's documentation for merge behavior, and test it before relying on it.

### Manual Merge with KeePassXC

If you end up with two conflicting copies of your database (for example, a Dropbox conflicted copy), you can merge them manually using KeePassXC:

1. Open the primary database file in KeePassXC.
2. Go to Database > Merge From Database.
3. Select the conflicted copy.
4. KeePassXC merges entries from the conflicted copy into the primary database, keeping the most recently modified version of each entry.
5. Save the merged database.
6. Delete the conflicted copy.

This manual merge process is reliable and well-tested. It is the recommended approach when automatic merge is not available or has not been triggered.

## Prevention: Best Practices for Multi-Device Usage

The most effective strategy for sync conflicts is preventing them. These practices, drawn from years of multi-device KeePass usage, dramatically reduce conflict frequency.

### The Golden Rule: Close Before Switching Devices

The single most effective practice is ensuring you close (save and lock) the database on one device before opening it on another. Most conflicts arise from this sequence:

1. Open database on laptop in the morning.
2. Leave for work, laptop goes to sleep (database still open).
3. Open database on phone during the day to look up a password.
4. Modify an entry on the phone. Phone app saves.
5. Return home, open laptop. Laptop's version is now stale but may not know it yet.
6. Modify an entry on the laptop. Conflict.

The fix is simple: lock or close the database on your laptop before leaving. When you return, reload it to get the latest version. Many KeePass apps support auto-lock after a period of inactivity, which helps but does not fully solve the problem -- locking may prevent new changes, but the app may still have a stale version in memory.

### Wait for Sync to Complete

After saving changes on one device, wait a moment before opening the database on another device. Cloud sync is not instantaneous -- even fast providers like Dropbox take a few seconds to upload a small file and propagate it. Opening the database on a second device before sync completes means you are working with a stale copy.

A practical heuristic: after saving on one device, wait 30-60 seconds before opening on another, especially if the devices are on different networks.

### Use Auto-Lock Aggressively

Configure your KeePass app to auto-lock after a short period of inactivity (1-5 minutes). This ensures the database is saved and released quickly when you are not actively using it, reducing the window for conflicts.

### Minimize Simultaneous Multi-Device Usage

If you routinely use two or more devices to access your password database, designate one as your primary editing device. Use other devices primarily for read-only lookups. This is not always practical (you need to save generated passwords on whatever device you are using), but making a conscious effort to concentrate edits reduces conflicts.

### Choose a Conflict-Aware Cloud Provider

Dropbox's approach of creating conflicted copies rather than silently discarding changes is the safest behavior for password databases. If sync conflicts are a recurring problem, consider using Dropbox for your password database even if you use a different provider for other files. Our [cloud provider comparison](/cloud-sync/icloud-vs-gdrive-vs-dropbox/) details each provider's conflict behavior.

### Use Apps with Built-In Merge Support

Choose a KeePass [compatible app](/keepass/compatible-apps/) that supports automatic or manual merge. KeePassXC on the desktop has the most mature merge implementation. On iOS, check whether your chosen app supports merge and test it.

## Recovering from Sync Conflicts

When a conflict does occur, follow this procedure:

### If Your Cloud Provider Created a Conflicted Copy (Dropbox)

1. Do not delete either file yet.
2. Open the primary database in KeePassXC.
3. Use Database > Merge From Database to merge the conflicted copy.
4. Verify the merged result by spot-checking recently modified entries.
5. Save the merged database.
6. Delete the conflicted copy.

### If Last-Write-Wins Occurred (iCloud, Google Drive)

1. Check the cloud provider's version history for the database file.
2. Download the previous version (the "losing" version).
3. Open the current (winning) database in KeePassXC.
4. Merge the previous version using Database > Merge From Database.
5. Save the merged database.
6. Verify entries from both versions are present.

### If You Are Not Sure Whether Changes Were Lost

Open your database and review the most recently modified entries. If entries you know you changed recently are missing or show old data, a conflict likely overwrote your changes. Use version history or backup copies to recover.

## Advanced: Using Sync Triggers and File Monitoring

Some KeePass applications support sync triggers -- automated actions that fire when the database file changes on disk. KeePass 2.x (Windows) has a robust trigger system that can automatically merge changes when the file is updated by cloud sync.

For users comfortable with automation, file system monitoring tools (fswatch on macOS, inotifywait on Linux) can detect when the database file changes and trigger a notification or merge operation. This is an advanced setup but can nearly eliminate manual conflict resolution.

## The Fundamental Trade-Off

Sync conflicts are an inherent tension in the design of encrypted, file-based password databases. The encryption that protects your data from the cloud provider also prevents the cloud provider from intelligently merging changes. The file-based format that makes KeePass databases portable and vendor-independent also means that sync operates at the file level rather than the record level.

This is a conscious design trade-off. The alternative -- a cloud-native, server-mediated sync protocol -- would require trusting a server with access to your unencrypted data or with the ability to perform operations on it. The KDBX format prioritizes security and portability over seamless real-time collaboration. For a single user syncing across their own devices (the primary use case), the conflict prevention practices described above make conflicts rare enough to be a minor inconvenience rather than a serious problem.

Understanding the trade-off helps frame expectations: you are not dealing with a bug or a limitation. You are dealing with the inherent behavior of a system designed to keep your passwords encrypted and under your control, even at the cost of occasionally requiring manual conflict resolution.
