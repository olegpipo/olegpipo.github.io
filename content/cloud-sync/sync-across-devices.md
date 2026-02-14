---
title: "How to Sync Your Password Database Across All Devices"
description: "Step-by-step guide to syncing your KeePass password database across iPhone, iPad, Mac, and other devices using iCloud, Google Drive, Dropbox, Syncthing, WebDAV, and manual methods."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Cloud Sync & Storage"
---

Keeping a single password database synchronized across every device you own is the most practical challenge in self-managed password security. The [Cloud Sync & Storage](/cloud-sync/) approach lets you store your encrypted `.kdbx` file in a cloud service that handles replication, while decryption always happens locally on your device. This article covers every major sync method -- from fully automatic cloud sync to manual file transfer -- with practical setup guidance, performance considerations, and advice on handling the edge cases that trip people up.

The goal is simple: the same encrypted database, available on every device, updated within seconds of any change.

## Cloud-Based Sync Methods

Cloud sync is the most popular approach because it is automatic, requires minimal maintenance, and works across devices without manual intervention. Your encrypted database is stored in a cloud service, and each device downloads the latest version when it needs it.

### iCloud Drive

iCloud Drive is the most seamless option for users within the Apple ecosystem. If you own an iPhone, iPad, and Mac, iCloud Drive is already configured and available on every device.

**How it works**: Your `.kdbx` file is placed in an iCloud Drive folder (either the app-specific container or a general iCloud Drive location). Changes sync automatically through Apple's infrastructure. On iOS and macOS, [KeePass-compatible apps](/keepass/compatible-apps/) like [PanicVault](https://panicvault.com) that support iCloud can read and write the file directly.

**Setup**:

1. Ensure iCloud Drive is enabled on all devices (Settings > Apple ID > iCloud > iCloud Drive on iOS; System Settings > Apple ID > iCloud > iCloud Drive on macOS).
2. Place your `.kdbx` file in iCloud Drive. On a Mac, this is typically `~/Library/Mobile Documents/com~apple~CloudDocs/` or you can use the iCloud Drive sidebar in Finder.
3. Open your KeePass-compatible app on each device and point it to the file in iCloud Drive.
4. Changes made on any device propagate to all others automatically.

**Sync latency**: Typically 5-30 seconds for small files like password databases. iCloud Drive prioritizes recently modified files.

**Strengths**: Zero configuration on Apple devices, no additional accounts needed, integrated with iOS file picker. See our [detailed iCloud sync guide](/cloud-sync/icloud-sync/) for troubleshooting and advanced configuration.

**Limitations**: Limited utility on non-Apple platforms. Windows has an iCloud for Windows client, but Android has no native iCloud support.

### Google Drive

Google Drive is the strongest cross-platform option. It works natively on Android, has robust desktop clients for macOS and Windows, and provides web access from any browser.

**How it works**: Your `.kdbx` file is stored in Google Drive. The desktop client (Google Drive for Desktop) keeps a local copy that syncs automatically. On mobile, KeePass apps can access Google Drive through the app's built-in integration or through the system file picker.

**Setup**:

1. Install Google Drive for Desktop on your Mac or PC. Sign in with your Google account.
2. Place your `.kdbx` file in a Google Drive folder. It will sync to the cloud within seconds.
3. On Android, install your preferred KeePass app and connect it to Google Drive through the app's settings.
4. On iOS, apps that support Google Drive integration can access the file directly. Some apps require you to grant Google Drive access during initial setup.

**Sync latency**: Generally 5-15 seconds. Google's infrastructure is fast, and the desktop client detects file changes almost immediately.

**Strengths**: True cross-platform support (macOS, Windows, Linux, Android, iOS, web), generous free storage (15 GB), reliable infrastructure. See our [Google Drive sync guide](/cloud-sync/google-drive-sync/) for the full walkthrough.

**Limitations**: Requires a Google account. The mobile experience on iOS is slightly less integrated than iCloud because Google Drive is a third-party service on Apple platforms.

### Dropbox

Dropbox was the pioneer in file sync and still offers one of the fastest and most reliable sync engines available.

**How it works**: The Dropbox desktop client maintains a local copy of your files and syncs changes to Dropbox servers in near real-time. Mobile apps can access files through the Dropbox API.

**Setup**:

1. Install the Dropbox desktop client and sign in.
2. Place your `.kdbx` file in your Dropbox folder.
3. On mobile devices, use a KeePass app that supports Dropbox integration. Many apps have built-in Dropbox connectors.
4. Changes sync automatically across all connected devices.

**Sync latency**: Dropbox has historically offered the fastest sync of any major cloud provider, often propagating small file changes in under 10 seconds.

**Strengths**: Fastest sync engine, excellent file versioning (keeps previous versions of files, useful for recovery), works on all major platforms.

**Limitations**: Free tier is limited to 2 GB (more than enough for password databases, but limited if you use it for other files). Dropbox's privacy practices have drawn scrutiny in the past, though this is irrelevant for pre-encrypted `.kdbx` files.

### Comparing Cloud Providers

For a side-by-side comparison of iCloud, Google Drive, and Dropbox for password database sync, see our [cloud provider comparison](/cloud-sync/icloud-vs-gdrive-vs-dropbox/). The short version: if you are all-Apple, iCloud is simplest; if you are cross-platform, Google Drive offers the best coverage; if sync speed is your top priority, Dropbox is hard to beat.

## Self-Hosted Sync Methods

If you prefer not to use a commercial cloud service, self-hosted options give you full control over your data's storage location.

### Syncthing

Syncthing is an open-source, peer-to-peer file synchronization tool. It syncs files directly between your devices without any central server.

**How it works**: Syncthing runs on each device and connects to other Syncthing instances over an encrypted channel. When a file changes on one device, the change is propagated directly to all other connected devices. There is no cloud server involved -- data travels directly between your machines (or through encrypted relay servers if direct connections are not possible).

**Setup**:

1. Install Syncthing on each device. It is available for macOS, Windows, Linux, Android, and (with limitations) iOS.
2. Create a shared folder containing your `.kdbx` file.
3. Link devices by exchanging device IDs (long alphanumeric strings that serve as identifiers and encryption keys).
4. Configure the shared folder on each device.

**Sync latency**: Near-instant when devices are on the same network. Over the internet, depends on connection quality and whether relay servers are needed.

**Strengths**: No third party involved, no cloud account needed, fully encrypted in transit, open-source and auditable.

**Limitations**: Requires at least two devices to be online simultaneously for sync to occur. No web access. iOS support is limited because iOS restricts background processes. Setup is more technical than cloud services.

### WebDAV

WebDAV (Web Distributed Authoring and Versioning) is a protocol extension to HTTP that allows file management on remote servers. Many KeePass applications have built-in WebDAV support, making it a natural fit for self-hosted sync.

**How it works**: You set up a WebDAV server (or use a hosting provider that supports WebDAV, such as Nextcloud, ownCloud, or a NAS device), and your KeePass app connects to the server directly to read and write the database file.

**Setup**:

1. Set up a WebDAV server. Options include Nextcloud (self-hosted), ownCloud, a Synology/QNAP NAS, or any web server with WebDAV enabled.
2. Upload your `.kdbx` file to the WebDAV server.
3. In your KeePass app, configure a WebDAV connection with the server URL, username, and password.
4. The app reads the database directly from the server each time you open it and writes back changes when you save.

**Sync latency**: Depends on your server and network, but typically fast for small files.

**Strengths**: Direct integration with many KeePass apps, full control over the server, no dependency on consumer cloud services. Works well with Nextcloud for a fully self-hosted solution.

**Limitations**: Requires running and maintaining a server. Not suitable for non-technical users. Security depends on your server configuration (HTTPS is mandatory, and you should use strong authentication).

## Manual Sync Methods

For users who want maximum control and are willing to trade convenience for simplicity, manual methods work perfectly for password databases.

### USB/Airdrop/Direct Transfer

The simplest approach: copy the `.kdbx` file manually between devices whenever you make changes.

**Methods**:

- **AirDrop** (Apple devices): Right-click the file on Mac, choose Share > AirDrop, and send it to your iPhone or iPad. On the receiving device, open it with your KeePass app.
- **USB transfer**: Connect your device to a computer and copy the file through Finder (iPhone/iPad) or the file system (Android).
- **Email/messaging**: Email the encrypted file to yourself or send it through a secure messaging app. Since the file is encrypted, this is safe -- but it is the least convenient method.

**Strengths**: No cloud account needed, no software dependencies, works offline, complete control.

**Limitations**: Entirely manual. If you forget to transfer after making changes, your devices will have different versions. Not practical for frequent updates.

## Sync Frequency and Latency

How quickly changes propagate matters when you use multiple devices throughout the day. If you add a new password on your phone during lunch and need it on your laptop an hour later, the sync must have completed by then.

**Cloud services**: All major cloud providers sync small files (under 1 MB, which covers virtually all password databases) within seconds to a minute. This is fast enough for practical use. The database is typically available on your other devices before you switch to them.

**Peer-to-peer (Syncthing)**: Sync occurs within seconds when both devices are online and connected. If one device is offline (phone in airplane mode, laptop closed), sync happens as soon as both devices are available.

**WebDAV**: Each device reads the latest version when you open the app. There is no background sync -- you always get the current version from the server. This avoids stale copies but requires network access to open the database.

**Manual**: Latency is determined by when you remember to transfer the file. This can range from instant (if you transfer immediately) to days or weeks (if you forget).

## Conflict Resolution Basics

A sync conflict occurs when you modify the database on two devices before they have a chance to sync. For example, you add a password on your phone and a different password on your laptop while the laptop is offline. When the laptop reconnects, the cloud service sees two different versions of the same file.

**How cloud services handle conflicts**: Most cloud services create a "conflict copy" -- they keep both versions and add a suffix like "(conflict)" to one of them. You then have two `.kdbx` files and need to merge them manually. For a detailed guide on handling this, see our [sync conflict resolution guide](/cloud-sync/sync-conflicts/).

**How to prevent conflicts**:

1. **Close the database after use** -- Saving and closing the file on one device before opening it on another prevents simultaneous edits.
2. **Wait for sync** -- After making changes, wait a few seconds for the sync to propagate before opening the database on another device.
3. **Use a single "primary" device for edits** -- If possible, make most changes on one device to minimize conflict opportunities.

**KeePass merge capabilities**: Some KeePass applications support database merging, which can reconcile two diverged copies by combining the changes from both. This is a powerful feature that eliminates most conflict scenarios, but not all apps support it equally.

## Automatic Backup Considerations

Sync is not backup. If your database is corrupted or accidentally deleted, sync will propagate the corruption or deletion to all devices. Protect against this with an [automatic backup strategy](/cloud-sync/automatic-backup/):

- Enable file versioning in your cloud service (Dropbox keeps 30-180 days of version history depending on plan; Google Drive keeps 100 versions; iCloud has limited versioning).
- Keep a periodic offline copy on a USB drive or local disk.
- Some KeePass apps support automatic backup files (a copy saved alongside the main file each time you save).

## Choosing the Right Sync Method

For most users in the [Apple ecosystem](/apple/), the decision is straightforward:

- **All-Apple, minimal setup**: iCloud Drive with a native KeePass app like PanicVault. It just works.
- **Cross-platform (Apple + Android/Windows)**: Google Drive. Best coverage.
- **Privacy-first, technical users**: Syncthing. No third parties.
- **Self-hosted infrastructure**: WebDAV with Nextcloud or a NAS.
- **Occasional sync, maximum simplicity**: Manual transfer via AirDrop.

The beauty of the [KeePass](/keepass/) approach is that your sync method is independent of your security model. The `.kdbx` file is encrypted identically regardless of how you move it between devices. You can switch sync methods at any time by simply moving the file. If you start with iCloud and later want to switch to Google Drive, you copy the file and update your app's file location. No migration, no export/import, no loss of data.

Pick the method that fits your workflow and devices, and start with your cloud provider's native solution. You can always change later. The [cloud provider comparison guide](/cloud-sync/choose-your-cloud/) can help you make the initial choice based on your specific device mix.
