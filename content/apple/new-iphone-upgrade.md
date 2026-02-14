---
title: "What Happens to Your Passwords When You Upgrade Your iPhone"
description: "A complete guide to transferring passwords when upgrading your iPhone, covering iCloud Keychain migration, third-party password manager data, KeePass database transfer, Quick Start, and backup and restore."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Apple Ecosystem"
---

Upgrading your iPhone should be exciting, not stressful. But among the photos, messages, and apps that need to make the journey to your new device, your passwords occupy a uniquely critical position. Lose a photo and it is a disappointment. Lose your passwords and you are locked out of your digital life. The good news is that Apple has invested heavily in making data transfer seamless, and the [Apple ecosystem](/apple/) generally handles password migration well -- if you understand what is happening and prepare properly.

This guide covers every aspect of password transfer during an iPhone upgrade: what happens automatically, what requires your attention, and how to ensure that every credential -- from iCloud Keychain entries to your KeePass database to third-party app data -- arrives safely on your new device.

## Before You Upgrade: The Preparation Checklist

The time to think about password migration is before you start the transfer process, not after. Spend fifteen minutes on preparation to avoid hours of recovery later.

### Verify Your iCloud Keychain Status

Open Settings on your current iPhone, tap your name at the top, then tap iCloud, then Passwords and Keychain. Confirm that iCloud Keychain is turned on and that your device has recently synced. If iCloud Keychain is off, your saved Safari passwords and Wi-Fi credentials are stored only on the local device and will not automatically appear on your new iPhone unless you use an encrypted backup.

### Confirm Your Apple ID Credentials

You will need your Apple ID email and password during the new iPhone setup. If you use two-factor authentication (you should), you will also need access to a trusted device or phone number for the verification code. If your current iPhone is your only trusted device, make sure you have a trusted phone number that can receive SMS codes, because your old iPhone will be unavailable during part of the setup process.

### Check Your Password Manager

If you use a third-party password manager, verify that your vault is synced and accessible from the cloud. Open the app, confirm you can see all your entries, and verify that the sync status shows up to date.

For KeePass-compatible apps like PanicVault, your database is a file stored in cloud storage (iCloud Drive, Google Drive, Dropbox, or similar). Confirm that the file is in the cloud, not only on the local device. If your .kdbx file is stored only locally, copy it to a cloud service or create a backup before starting the upgrade. Our [backup guide](/keepass/backup-database/) covers this in detail.

### Know Your Master Password

This sounds obvious, but it is the single most important preparation step. After the transfer, your password manager on the new iPhone will ask you to authenticate. If you use [Face ID or Touch ID](/apple/face-id-touch-id-setup/) to unlock your vault and have not typed your master password in months, make sure you still remember it. Open your password manager on the old phone, lock it, and unlock it with your master password (not biometrics) to confirm you know it.

Face ID and Touch ID data do not transfer between devices. The biometric enrollment on your old iPhone is tied to that device's Secure Enclave and cannot be exported. You will re-enroll your face or fingerprint on the new device, but the first unlock of your password manager will require the master password.

### Create a Backup

Regardless of which transfer method you use, create a fresh backup of your current iPhone. An iCloud backup or an encrypted local backup to your Mac or PC ensures that if anything goes wrong during the transfer, you can restore to the pre-upgrade state.

**Important**: If you create a local backup using Finder (Mac) or iTunes (Windows), check the "Encrypt local backup" option. Only encrypted backups include your Keychain data, Wi-Fi passwords, Health data, and saved account passwords. An unencrypted backup does not include these items, and you will lose them.

## Transfer Method 1: Quick Start (Device-to-Device)

Quick Start is Apple's recommended transfer method and the one most people will use. You place your old iPhone near your new iPhone, and the new device offers to transfer everything directly.

### How Quick Start Handles Passwords

During Quick Start, iCloud Keychain entries are not transferred directly between devices. Instead, the new iPhone signs into your iCloud account during setup and downloads Keychain data from iCloud. This means Keychain transfer depends on iCloud Keychain being enabled and synced, not on the proximity transfer itself.

App data -- including password manager settings, local caches, and locally stored credentials -- transfers directly from the old device. Wi-Fi passwords in iCloud Keychain sync through iCloud; locally stored Wi-Fi passwords transfer through the device-to-device migration. Keychain items with "this device only" protection are preserved during the migration.

### Quick Start Step by Step

1. Turn on your new iPhone and place it near your current iPhone.
2. Tap Continue on the Quick Start prompt, scan the animation, and enter your current passcode on the new device.
3. Set up Face ID on the new iPhone (a fresh enrollment -- old biometric data does not transfer).
4. Choose "Transfer from iPhone" and keep both devices near each other until the transfer completes.

After apps finish installing, open your password manager and authenticate with your master password. You can then configure Face ID for subsequent unlocks.

## Transfer Method 2: iCloud Backup and Restore

If you cannot place both iPhones next to each other (for example, if you are trading in your old phone before the new one arrives), restoring from an iCloud backup works well. iCloud Keychain syncs independently of the backup -- when you sign into your Apple ID on the new iPhone, your Keychain data downloads from iCloud regardless. App data included in the backup transfers during restore, bringing your password manager settings along. Biometric data does not transfer; you will set up Face ID fresh.

To use this method: create a fresh iCloud backup on your old iPhone (Settings > [your name] > iCloud > iCloud Backup > Back Up Now), then on the new iPhone choose "Restore from iCloud Backup" during setup and select that backup.

## Transfer Method 3: Encrypted Local Backup (Mac or PC)

An encrypted local backup via Finder (Mac) or iTunes (Windows) is the most complete transfer method. Only encrypted backups include Keychain data, saved passwords, Wi-Fi credentials, Health data, and HomeKit configuration. If you create an unencrypted backup, these items are silently omitted.

Connect your old iPhone, check "Encrypt local backup," set a backup password, and back up. Then connect the new iPhone and restore from that backup.

## What Happens to Your KeePass Database

If you use a KeePass-compatible password manager like PanicVault, your database migration works differently from iCloud Keychain because your vault is a file you control.

### Cloud-Synced Database (Recommended Setup)

If your .kdbx database is stored in iCloud Drive, Google Drive, Dropbox, or another cloud service, the migration is straightforward:

1. The password manager app transfers to your new iPhone (via Quick Start, iCloud restore, or local backup restore).
2. The app's settings, including the reference to your cloud-stored database file, transfer with the app data.
3. On first launch, the app connects to the cloud service and accesses the same .kdbx file.
4. You enter your master password to unlock the database.
5. You configure Face ID for future unlocks.

Your database file itself never needs to "transfer" because it lives in the cloud. The new iPhone simply accesses the same file. This is one of the advantages of the cloud sync approach described in our [iCloud sync guide](/cloud-sync/icloud-sync/).

### Locally-Stored Database

If your .kdbx file is stored only on the iPhone (not synced to any cloud service), the file transfers as part of the app's data during Quick Start or backup restore. However, this is a fragile setup. If the transfer fails or you set up the new iPhone as a new device rather than restoring, the local-only database will be lost.

**Strong recommendation**: Before any upgrade, ensure your KeePass database is either synced to a cloud service or backed up to an external location. A locally stored database with no backup is a single point of failure -- the exact scenario the [backup guide](/keepass/backup-database/) is written to prevent.

### Key Files

If your KeePass database is protected by a [key file](/keepass/key-files/) in addition to your master password, that key file also needs to be present on the new device. Key files stored in cloud storage transfer the same way the database does. Key files stored locally transfer with the app data during device migration. As with the database itself, ensure your key file has a backup before upgrading.

## What Happens to iCloud Keychain

iCloud Keychain is Apple's built-in password manager, and its migration during an iPhone upgrade is almost entirely automatic.

### The Automatic Flow

When you sign into your Apple ID on the new iPhone and enable iCloud Keychain:

1. Your device authenticates with iCloud.
2. iCloud Keychain data downloads to the new device.
3. All saved passwords, credit cards, Wi-Fi passwords, and passkeys become available.
4. Safari AutoFill works immediately.

There is nothing you need to do manually. The Keychain data is encrypted end-to-end in iCloud and decrypts on your new device using keys derived from your Apple ID credentials and device passcode.

### Potential Issues

**iCloud Keychain approval.** In some configurations, a new device needs approval from an existing trusted device before it can access Keychain data. If your old iPhone is already wiped, you may need to use your iCloud Security Code or recovery key. Keep these accessible during the upgrade.

**Two-factor authentication delays.** If your Apple ID uses two-factor authentication and your old iPhone was your only trusted device, you may encounter a circular dependency: you need to approve the new device, but the approval device is being replaced. Having a trusted phone number as a backup prevents this issue.

**Passkeys.** Passkeys stored in iCloud Keychain sync to the new device along with passwords. No special handling is needed.

## What Happens to Third-Party Password Managers

Each password manager handles the iPhone upgrade slightly differently, but the general pattern is consistent.

### Cloud-Synced Managers (1Password, Bitwarden, Dashlane, etc.)

Cloud-synced managers are straightforward: install the app on the new iPhone, sign in with your account credentials, and the vault downloads from the vendor's servers. Because the data lives on their infrastructure, the transfer is independent of the iPhone migration method. Even setting up as a completely new device works -- your passwords are available as soon as you sign in.

### KeePass-Compatible Managers (PanicVault, Strongbox, KeePassium)

As described above, the database file is the vault. If it is in cloud storage, the app accesses it on the new device. If it is local-only, it transfers with the app data. The master password is required for the first unlock on the new device, and biometric unlock is reconfigured afterward.

The critical difference is that KeePass-compatible managers do not depend on any vendor's servers. Your database file is yours, stored where you choose, and the migration path is as reliable as your file storage. This independence is the core advantage of the KeePass approach, and it means your [iPhone, iPad, and Mac](/apple/iphone-ipad-mac/) all access the same file without intermediary infrastructure.

## Face ID and Touch ID: Starting Fresh

Biometric enrollment always starts fresh on a new device. Your Face ID or Touch ID template is stored in the [Secure Enclave](/apple/secure-enclave/) of your specific device and cannot be extracted or transferred. After the data transfer, set up Face ID during initial setup, then open each app that uses biometric unlock and re-enable it. For your password manager, this means entering your master password once, then enabling Face ID for future unlocks.

## After the Upgrade: Verification Checklist

Once your new iPhone is set up, take a few minutes to verify everything transferred correctly:

- **iCloud Keychain**: Open Settings > Passwords. Browse your saved credentials and try autofilling a login in Safari to confirm the integration works.
- **Password manager**: Open PanicVault (or your manager of choice). Unlock with your master password. Browse entries, confirm the database is complete, enable Face ID, and verify TOTP codes generate correctly.
- **AutoFill configuration**: Go to Settings > General > AutoFill & Passwords. Confirm your preferred manager is selected as the AutoFill provider.
- **Cloud sync**: If your KeePass database is in iCloud Drive or another cloud service, make a small test change and verify it syncs back.
- **Password sharing**: If you use Apple's [password sharing](/apple/share-passwords-apple/) features, verify shared credentials are accessible on the new device.

## Common Problems and Solutions

**Passwords did not transfer.** Check that iCloud Keychain is enabled (Settings > [your name] > iCloud > Passwords and Keychain). For third-party managers, sign out and back in, or re-point the app at your cloud-stored database.

**Face ID not working for password manager.** New enrollment does not automatically re-authorize apps. Open your manager's settings and re-enable Face ID unlock -- you will need your master password.

**KeePass database not found.** Verify the cloud storage app (iCloud Drive, Google Drive, Dropbox) is installed and signed in. Navigate to the file manually. If the database was local-only and did not transfer, restore from your backup.

**Forgot master password.** For iCloud Keychain, Apple has recovery options. For KeePass-compatible managers, there is no recovery -- the encryption is non-negotiable. Do not wipe your old iPhone until you resolve this.

## Planning for Your Next Upgrade

Every iPhone upgrade is an opportunity to audit your password management setup. Confirm your KeePass database is cloud-synced (not local-only), verify your backup strategy is current and tested, record your master password in a secure physical location as disaster recovery, check that iCloud Keychain sync is healthy across all devices, and review your [iCloud Keychain limitations](/apple/icloud-keychain-not-enough/) to decide whether a dedicated manager would serve you better.

The iPhone upgrade cycle is annual for many users. Building these checks into your upgrade routine ensures that password migration remains a non-event -- exactly what it should be.

## Conclusion

Transferring passwords during an iPhone upgrade is largely automatic if you are prepared. iCloud Keychain syncs through iCloud independently of the device transfer. Third-party password managers reconnect through their cloud services. KeePass databases in cloud storage are accessible from any device that can reach the file.

The critical preparation steps are simple: verify that your password data is synced, confirm you know your master password, create a backup, and understand that biometrics require fresh enrollment on the new device. Fifteen minutes of preparation before the upgrade prevents every password-related problem that could occur during it.
