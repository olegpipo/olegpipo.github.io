---
title: "KeePass for iPhone & iOS: The 3 Best KeePass Apps (2026)"
description: "There's no official KeePass app for iPhone. These 3 iOS apps open your .kdbx database with AutoFill and Face ID, plus how to move it over from Windows."
date: 2026-09-19
lastmod: 2026-09-19
draft: false
silo: "KeePass & Open Standards"
faq:
  - q: "Is there a KeePass app for iPhone?"
    a: "Not an official one. KeePass 2.x, the original password manager by Dominik Reichl, is a Windows program, and the KeePass project does not make an iPhone or iPad version. Its website lists independent iOS apps that open the same .kdbx files, including Strongbox and KeePassium. PanicVault is another KDBX-compatible app for iPhone, iPad and Mac."
  - q: "Does KeePass work on iPhone?"
    a: "Your KeePass database does, even though the KeePass program itself does not run on iOS. A KeePass-compatible app such as PanicVault, Strongbox or KeePassium opens the same .kdbx file you use on your PC, fills passwords through iOS AutoFill, and unlocks with Face ID or Touch ID. Keep the file in a cloud folder that both your PC and your iPhone can reach."
  - q: "What is the best KeePass app for iOS?"
    a: "It depends on what matters to you. PanicVault has a native Apple design and is a one-time purchase. Strongbox has the most features, including built-in Dropbox, OneDrive, WebDAV and SFTP sync and an Apple Watch app. KeePassium has a free version limited to one database, with Premium needed for logins suggested above the keyboard and YubiKey support. All three open KDBX 4 databases created in KeePass 2.x."
  - q: "Is there a free KeePass app for iPhone?"
    a: "Yes, but the free versions are cut down. KeePassium Free handles one database and has basic AutoFill, Face ID and TOTP codes, but you pick each login from a list every time; logins suggested above the keyboard, saving new logins from AutoFill, YubiKey support and the password audit need Premium (€19.99/year). Strongbox's free version is for non-commercial use only and does not unlock with Face ID or Touch ID; that needs Strongbox Pro. PanicVault is a one-time purchase with no subscription and no feature tiers."
  - q: "Can I use the same KeePass database on Windows and iPhone?"
    a: "Yes. Put the .kdbx file in a folder synced by OneDrive, Dropbox, Google Drive or iCloud for Windows, open it from there in KeePass on your PC, and open the same file in your iPhone app. Avoid editing on both devices before changes have synced; if you end up with two copies, KeePass 2.x can merge them with File > Synchronize."
---

"KeePass" means two things. To some people it is one program: KeePass Password Safe, the free Windows app Dominik Reichl has maintained for more than twenty years. To others it is shorthand for every app that reads and writes the same `.kdbx` database file. Either way, the App Store has no iPhone app from the KeePass project itself.

You don't need one. Your KeePass database is a single encrypted file in an open, documented format, and several iPhone and iPad apps open it as it is. This guide covers the three worth using, how to move your database from a Windows PC to your phone, and how to make iOS fill passwords from it.

> **Quick answer**: There is no official KeePass app for iPhone or iPad. KeePass 2.x is a Windows program (it also runs on Linux and macOS through Mono), and the KeePass website lists iOS apps from other developers under "Contributed/Unofficial KeePass Ports". The three best KeePass apps for iPhone are **[PanicVault](https://apps.apple.com/app/id6759188575)** for a native Apple design and a one-time purchase, **Strongbox** for the most features, and **KeePassium**, whose free version is limited to one database and basic AutoFill. All three open the .kdbx file you already use in KeePass, fill passwords through iOS AutoFill, and unlock with Face ID (a Pro feature in Strongbox). PanicVault needs the database in KDBX 4 format; [step 3 below](#step-3-check-your-kdbx-version) shows how to check and upgrade it in KeePass 2.x.

## Is There an Official KeePass App for iPhone?

No. The official downloads on [keepass.info](https://keepass.info/download.html) are KeePass 2.x for Windows, as an installer or a portable ZIP, and the same program runs on Linux and macOS through the Mono runtime. There is no iOS or iPadOS build.

The download page does have an iPhone and iPad section, but everything in it sits under "Contributed/Unofficial KeePass Ports": apps by other developers that work with KeePass databases. As of September 2026 the iOS entries are KeePassium, Strongbox, KeeForge, PassDrop 2 (KeePass 1.x files only), KyPass and OneKeePass.

The names cause most of the confusion:

- **KeePass** (KeePass Password Safe) is the original. Version 2.x introduced the `.kdbx` format the whole ecosystem now shares. It is built for Windows.
- **KeePassX** was an early port for Linux and macOS. It is discontinued; its website says development has stopped.
- **KeePassXC** began as a community fork of KeePassX and is now a widely used desktop client for Windows, Mac and Linux. Its own FAQ suggests Strongbox and KeePassium for iOS.

None of the three has an iPhone app, and KeePass 2.x and KeePassXC both use `.kdbx` files, so the apps below work with databases from either. If you use KeePassXC on your computer, our guide to [KeePassXC for iPhone](/keepass/keepassxc-ios-alternatives/) covers these apps from that angle.

## The Best KeePass Apps for iPhone and iPad

All three open a `.kdbx` database from KeePass 2.x, work with iOS AutoFill, and support Face ID or Touch ID. They differ in price model, which database versions they accept, how they sync, and how much they try to do.

### PanicVault

**Price**: One-time purchase, no subscription
**KDBX versions**: KDBX 4 only
**Sync**: iCloud Drive and Google Drive built in; Dropbox, OneDrive and others through the iOS Files app
**Platforms**: iPhone, iPad, Mac

[PanicVault](https://apps.apple.com/app/id6759188575) is a native Apple app written in SwiftUI, for people who want their KeePass database to feel at home on an iPhone. It reads and writes KDBX 4 with groups, custom fields, attachments and entry history intact, fills passwords system-wide through iOS AutoFill, and unlocks with Face ID or Touch ID. It also generates TOTP codes, including from the `TimeOtp` fields KeePass 2.x uses for its own one-time passwords.

iCloud Drive and Google Drive sync are built in. A database in Dropbox or OneDrive opens through the Files app, with that provider's app doing the syncing. YubiKey challenge-response works over NFC on iPhone and USB on Mac, in the same format KeePassXC uses.

The limits matter for KeePass 2.x users. PanicVault opens **KDBX 4 only**, so a KDBX 3.1 database has to be upgraded first, which takes about a minute in KeePass. It cannot read a YubiKey on iPad, over USB-C or over Lightning, and it does not support the KeeChallenge plugin that some KeePass 2.x users rely on. It is not open source, and it runs only on Apple devices, which is fine when KeePass is covering your PC.

**Best for**: KeePass users who want a clean, Apple-native app and would rather pay once than subscribe.

### Strongbox

**Price**: Free version for non-commercial use; Strongbox Pro at $2.99/month, $24.99/year or $124.99 lifetime on Strongbox's website
**KDBX versions**: KDBX 4, KDBX 3.1 and KeePass 1.x `.kdb`, plus Password Safe
**Sync**: iCloud Drive, Dropbox, Google Drive, OneDrive, WebDAV and SFTP built in, plus the Files app
**Platforms**: iPhone, iPad, Mac, Apple Watch

Strongbox is the most feature-rich KeePass client on Apple devices. It opens every KeePass format, including KeePass 1.x databases, and it connects directly to more storage services than the other two: you sign in to Dropbox, OneDrive or your own WebDAV or SFTP server from inside the app.

On iPhone and iPad, the free version includes AutoFill, TOTP codes, key files and the built-in sync options. [Strongbox Pro](https://strongboxsafe.com/comparison/) adds Face ID and Touch ID unlock, YubiKey support, the Apple Watch app, Have I Been Pwned breach checks and offline editing. Biometric unlock is the gap most people notice on a phone; a 90-day free trial of Pro lets you decide. The source code is published on [GitHub](https://github.com/strongbox-password-safe/Strongbox) under the AGPL-3.0 licence.

The trade-offs are a busier interface, with many settings to expose, and the highest lifetime price of the three. Strongbox also notes that YubiKeys over USB-C are not supported on iOS.

**Best for**: People who want everything in one app: built-in Dropbox, OneDrive or WebDAV sync, KeePass 1.x support, breach checks and an Apple Watch app.

### KeePassium

**Price**: Free for one database; Premium subscription (€19.99/year on KeePassium's site) or a lifetime Pro licence ($79.99 on the US App Store)
**KDBX versions**: KDBX 4, KDBX 3.1 and KeePass 1.x `.kdb`
**Sync**: Any provider in the iOS Files app (iCloud Drive, Dropbox, OneDrive, Google Drive, Box and others)
**Platforms**: iPhone, iPad, Mac (built with Mac Catalyst)

KeePassium publishes its source code under the GPLv3, as Strongbox does under the AGPL-3.0, but there is no way to verify that either app's App Store build was compiled from that code. KeePassium's App Store listing says it has been independently audited by Cure53. The free version handles one database and has basic AutoFill, Face ID and Touch ID unlock, TOTP codes and file attachments, but you pick each login from a list every time. According to [KeePassium's pricing page](https://keepassium.com/pricing/), logins suggested above the keyboard (Quick AutoFill), YubiKey support, the password audit and more than one database need Premium (€19.99/year) or the lifetime Pro licence, and KeePassium's release notes say saving new logins from AutoFill is a Premium feature too.

KeePassium works through the storage providers in the Files app rather than keeping its own cloud logins. The limits are one database on the free tier, YubiKey only with a paid licence, and a Mac app built from the iPad code with Mac Catalyst.

**Best for**: People who keep a single database and can live with basic AutoFill, or who are willing to pay for Premium.

### Older and Discontinued Apps

**KeePass Touch** is a long-running free app that is still updated. It opens KeePass 1.x and 2.x files, unlocks with Face ID or Touch ID, and syncs with Dropbox and OneDrive, but its App Store listing does not mention iOS AutoFill or TOTP codes, the two features most people want on a phone.

**MiniKeePass**, once the usual free recommendation, is discontinued: it is no longer on the App Store and its GitHub project is archived. If an old device still has it, copy the database out and move to a maintained app. The keepass.info list also includes smaller apps such as KyPass and OneKeePass, which we have not reviewed here.

## KeePass iPhone Apps Compared

| Feature | PanicVault | Strongbox | KeePassium |
|---|---|---|---|
| **Price model** | One-time purchase | Free (non-commercial) or Pro subscription / lifetime | Free (one database) or Premium subscription / lifetime Pro |
| **KDBX 4** | Yes | Yes | Yes |
| **KDBX 3.1** | No (upgrade first) | Yes | Yes |
| **KeePass 1.x .kdb** | No | Yes | Yes |
| **Free version** | No tiers; every feature is in the one-time purchase | Non-commercial use only; no Face ID, YubiKey or offline editing | One database; no logins above the keyboard, YubiKey or password audit |
| **iOS AutoFill** | Yes | Yes | Yes (logins above the keyboard: Premium) |
| **Face ID / Touch ID** | Yes | Pro | Yes |
| **TOTP codes** | Yes | Yes | Yes |
| **Built-in sync** | iCloud Drive, Google Drive | iCloud Drive, Dropbox, Google Drive, OneDrive, WebDAV, SFTP | Via Files app providers |
| **YubiKey** | NFC on iPhone (not iPad) | Pro | Premium |
| **Open source** | No | Source published* | Source published* |
| **Mac app** | Yes | Yes | Yes (Mac Catalyst) |

\*Source code is public, but App Store builds can't be verified against it.

Prices vary by country and change over time, so check them before you buy.

## How to Move Your KeePass Database from Windows to iPhone

KeePass 2.x has no sync service of its own; it opens and saves a file wherever you keep it. So the job is to put that file somewhere both your PC and your phone can reach. First, make a backup copy of the `.kdbx` file outside any sync folder. Our [KeePass backup guide](/keepass/backup-database/) covers how.

### Step 1: Put the .kdbx File in a Cloud Folder

Pick a service with both a Windows client and an iPhone app:

- **OneDrive** is built into Windows; the OneDrive iPhone app makes it available in the Files app.
- **Dropbox** works the same way, with its desktop client on the PC.
- **Google Drive** needs Google Drive for desktop on the PC. PanicVault and Strongbox connect to it directly; KeePassium reaches it through the Google Drive app.
- **iCloud Drive** needs [iCloud for Windows](https://support.apple.com/guide/icloud-windows/set-up-icloud-drive-icw0144825a5/icloud), which adds an iCloud Drive folder to File Explorer.

Close KeePass, move the `.kdbx` file into the synced folder, then reopen it with File > Open so KeePass works on the synced copy. With PanicVault, iCloud Drive or Google Drive gives you its built-in sync.

### Step 2: Bring Your Key File Separately

If your master key includes a key file, the iPhone needs it too, because KeePass requires [every part of the master key](https://keepass.info/help/base/keys.html) to open a database. Don't put it in the same cloud folder as the database: anyone who gets into that account would then have both. Move it across once by another route, save it to On My iPhone in the Files app, and select it when you first unlock. Our [key files guide](/keepass/key-files/) covers backups.

If your YubiKey setup uses the KeeChallenge plugin for KeePass 2.x, confirm your iOS app supports it before relying on it. PanicVault does not.

### Step 3: Check Your KDBX Version

This matters most if you plan to use PanicVault. According to [keepass.info](https://keepass.info/help/kb/kdbx_4.html), KeePass introduced KDBX 4 in version 2.35 but only saves in that format when the database needs it: when the key derivation function is Argon2 rather than AES-KDF, when ChaCha20 is the encryption algorithm, or when a plugin stores extra data. A database still using AES-KDF with AES is most likely being saved as KDBX 3.1, even in the latest KeePass.

To check and upgrade in KeePass 2.x:

1. Open and unlock the database.
2. Choose **File > Database Settings** and open the **Security** tab.
3. If the key derivation function is **Argon2d** or **Argon2id** (or the encryption algorithm is **ChaCha20**), KeePass already saves the file as KDBX 4.
4. If it says **AES-KDF**, change it to **Argon2d** or **Argon2id** and click **OK**.
5. Choose **File > Save**.

Your master password, key file and entries stay the same, but any other PC that opens the file needs KeePass 2.35 or later. Strongbox and KeePassium also read KDBX 3.1, so the upgrade is optional for them, though Argon2 is the stronger choice. Our [KDBX format guide](/keepass/kdbx-format-guide/) explains the differences.

### Step 4: Open the Database on Your iPhone

In your chosen app, add an existing database, browse to the cloud folder from step 1 and select the `.kdbx` file. Enter your master password, pick your key file if you use one, and turn on Face ID when the app offers it.

### Avoid Editing in Two Places at Once

A `.kdbx` database is one encrypted file. If you change it on your PC and your iPhone before either change has synced, your cloud service may keep two copies. PanicVault merges changes entry by entry for vaults on iCloud Drive or Google Drive and shows you any real conflicts to resolve.

On the PC, [KeePass's Synchronize feature](https://keepass.info/help/v2/sync.html) (**File > Synchronize > Synchronize with File**) merges two copies entry by entry. The most recently modified version of each entry wins, the other version goes into that entry's history, and the merged result is written to both files. KeePass also checks on save whether the file on disk has changed, and offers to synchronize instead of overwriting. See [resolving sync conflicts](/cloud-sync/sync-conflicts/) for more.

## How to Turn On KeePass AutoFill on iPhone

AutoFill lets your KeePass app offer logins in Safari and other apps, so you never copy and paste passwords. On iOS 18 and later, including iOS 27, the setting is under General, per [Apple's iPhone User Guide](https://support.apple.com/guide/iphone/automatically-fill-in-strong-passwords-iphf9219d8c9/ios):

1. Install your KeePass app and add your database.
2. Open **Settings > General > AutoFill & Passwords**.
3. Turn on **AutoFill Passwords and Passkeys**.
4. In the list of apps on that screen, turn on your KeePass app.

iOS can fill from up to three password apps, so you can leave Apple Passwords on while you move over. On iOS 17 and earlier, the setting was under Settings > Passwords > Password Options.

Then tap a login field, choose the entry above the keyboard, and confirm with Face ID. Our [iPhone AutoFill guide](/apple/autofill-iphone-guide/) covers what to do when suggestions don't appear.

## Which One Should You Choose?

Choose **PanicVault** for an app that feels like it came with your iPhone, sold once with no subscription and no feature tiers, if your database can be KDBX 4. Choose **Strongbox** for the most features and built-in Dropbox, OneDrive or server sync, and expect to pay. Choose **KeePassium** to start free, if one database and basic AutoFill are enough; logins above the keyboard and YubiKey support need Premium. All three read the same file, so you can try more than one against your real database without exporting anything.

## Related Articles

- [KeePassXC for iPhone: 3 Best iOS Alternatives](/keepass/keepassxc-ios-alternatives/)
- [Strongbox vs KeePassium vs KeePassXC: KeePass Apps for Mac & iPhone](/compare/keepass-apps-apple/)
- [Every App That Opens KeePass Databases](/keepass/compatible-apps/)
- [How to Safely Back Up Your KeePass Database](/keepass/backup-database/)
- [What Is a .KDBX File? The KeePass Format Explained](/keepass/kdbx-format-guide/)
- [How AutoFill Works on iPhone](/apple/autofill-iphone-guide/)
