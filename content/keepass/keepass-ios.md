---
title: "KeePass for iPhone & iOS: The 3 Best KeePass Apps (2026)"
description: "There's no official KeePass app for iPhone. These 3 iOS apps open your .kdbx database with AutoFill and Face ID, plus how to move it over from Windows."
date: 2026-09-19
lastmod: 2026-10-21
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

## What Comes Across from KeePass 2.x, and What Doesn't

The apps below open the `.kdbx` file you already use in KeePass 2.x: entries, groups, custom fields, attachments and entry history all come across as they are. What varies is everything KeePass does through options and plugins, so check these before you choose:

- **Format version.** KeePass saves many databases as KDBX 3.1 even today (step 3 below shows why). Strongbox and KeePassium open KDBX 3.1 and KeePass 1.x `.kdb` files; PanicVault opens KDBX 4 only.
- **Key files.** All three accept KeePass key files, but you have to bring the key file over yourself (step 2).
- **TOTP codes.** KeePass 2.x keeps its built-in one-time passwords in [fields named `TimeOtp-Secret-Base32`](https://keepass.info/help/base/placeholders.html#otp) and similar; the older KeeTrayTOTP plugin used `TOTP Seed` and `TOTP Settings`. All three apps read both conventions, though KeePassium reads only the Base32 form of KeePass's own secret field.
- **Plugins don't run on iPhone.** KeePassRPC and Kee, KeeAgent, triggers and Auto-Type are KeePass desktop features. Anything a plugin stored as an entry field stays in the entry, but nothing on the phone uses it.
- **Twofish.** A database encrypted with the Twofish Cipher plugin opens in Strongbox and KeePassium, but not in PanicVault, which supports AES-256 and ChaCha20. Switching the cipher to AES-256 under **File > Database Settings > Security** in KeePass fixes that.
- **KeeChallenge YubiKeys.** KeePassium [says it has no plans](https://support.keepassium.com/kb/yubikey-keechallenge/) to support the KeeChallenge plugin, PanicVault does not support it, and Strongbox documents only KeePassXC's challenge-response scheme. All three support that scheme instead.
- **Windows user account keys.** If your master key includes KeePass's "Windows User Account" option, [keepass.info](https://keepass.info/help/base/keys.html) explains that the database opens only when you are logged in as that same Windows user, so no iPhone app can open it. Change the master key in KeePass (**File > Change Master Key**) to a password, with a key file if you like, before you move the database.

## The Best KeePass Apps for iPhone and iPad

All three open a `.kdbx` database from KeePass 2.x, fill passwords through iOS AutoFill, and support Face ID or Touch ID. For a KeePass 2.x user, the differences are which files they accept, how they reach a database saved on a Windows PC, and what they cost.

### PanicVault

**Price**: $4.99 one-time purchase, no subscription
**Opens**: KDBX 4 only (AES-256 or ChaCha20; Argon2 or AES-KDF)
**Reaching your PC's database**: iCloud Drive and Google Drive built in; OneDrive and Dropbox through the Files app
**Platforms**: iPhone, iPad, Mac

[PanicVault](https://apps.apple.com/app/id6759188575) is a native Apple app built in SwiftUI. Once your database is KDBX 4, it opens a file in iCloud Drive or another storage app in place rather than importing a copy. When KeePass on your PC changes the file, PanicVault merges those changes into its own entry by entry instead of overwriting them.

For a KeePass 2.x database it reads every standard key file type, generates TOTP codes from KeePass's own `TimeOtp-` fields (Base32, hex or Base64) as well as KeeTrayTOTP and KeePassXC fields, and leaves TOTP fields written by another app exactly as they are. It also keeps custom fields, attachments, entry history, custom icons and Auto-Type settings intact when it saves, so the file still works the same way in KeePass on your PC.

What you have to change first: a KDBX 3.1 or KeePass 1.x database must be [upgraded to KDBX 4](#step-3-check-your-kdbx-version), a Twofish database switched to AES-256 or ChaCha20, and a KeeChallenge YubiKey replaced with KeePassXC-style challenge-response, which PanicVault reads over NFC on iPhone and USB on Mac (not on iPad). It is not open source, and it runs only on Apple devices -- fine when KeePass is already covering your PC.

**Best for**: KeePass 2.x users happy to save their database as KDBX 4 who want a clean, Apple-native app and would rather pay once than subscribe.

### Strongbox

**Price**: free for non-commercial use; Strongbox Pro by subscription ($2.99 a month or $24.99 a year) or a $124.99 lifetime licence on Strongbox's website
**Opens**: KDBX 4, KDBX 3.1 and KeePass 1.x `.kdb`, including Twofish-encrypted files; also Password Safe
**Reaching your PC's database**: OneDrive, Dropbox, Google Drive, iCloud Drive, WebDAV and SFTP built in, plus the Files app
**Platforms**: iPhone, iPad, Mac, Apple Watch

Strongbox is the most accommodating of the three for an unmodified KeePass 2.x database. It opens every KeePass format version and the Twofish cipher, so you can usually point it at your existing file without changing anything in KeePass first. It also signs in to OneDrive and Dropbox directly from inside the app, which suits a database that lives in the OneDrive folder Windows sets up for you.

TOTP codes kept in KeePass's own fields or in KeeTrayTOTP's carry over, and key files work in the free version. A YubiKey needs Pro and the KeePassXC challenge-response scheme; Strongbox's documentation does not cover KeeChallenge. The free version is limited to non-commercial use and leaves out Face ID and Touch ID unlock, offline editing and the Apple Watch app; [Strongbox Pro](https://strongboxsafe.com/comparison/) adds them, with a 90-day free trial. Its source code is published on [GitHub](https://github.com/strongbox-password-safe/Strongbox), and the trade-off is a busier interface with many settings.

**Best for**: KeePass 2.x users who want to keep their database exactly as it is -- KDBX 3.1, Twofish and all -- or want built-in OneDrive, Dropbox or WebDAV sync.

### KeePassium

**Price**: free for one database; Premium (€19.99 a year on KeePassium's site) or a lifetime Pro licence ($79.99 on the US App Store)
**Opens**: KDBX 4, KDBX 3.1 and KeePass 1.x `.kdb`, including Twofish-encrypted files
**Reaching your PC's database**: direct connections to OneDrive, Dropbox, Google Drive and WebDAV, or any provider in the Files app, including iCloud Drive
**Platforms**: iPhone, iPad, Mac (built with Mac Catalyst)

KeePassium, too, opens a KeePass 2.x database without conversion, whatever its version or cipher. It can reach a database in OneDrive, Dropbox or Google Drive in two ways: through that provider's app in the Files app, or by [connecting to the service directly](https://support.keepassium.com/kb/sync/) from inside KeePassium. It reads all three common TOTP conventions, but of KeePass's own fields only the Base32 secret, so check entries whose codes you set up with a hex or Base64 secret.

Its YubiKey support follows KeePassXC's scheme, needs Premium, and excludes KeeChallenge. The free version handles a single database with basic AutoFill, in which you pick each login from a list. [KeePassium's pricing page](https://keepassium.com/pricing/) lists logins suggested above the keyboard, YubiKey support, the password audit and more than one database as Premium features, and its release notes say saving new logins from AutoFill is Premium too.

**Best for**: KeePass 2.x users with a single database who want to start free and keep their file unchanged.

### Older and Discontinued Apps

**KeePass Touch** is a long-running free app that is still updated. It opens KeePass 1.x and 2.x files, unlocks with Face ID or Touch ID, and syncs with Dropbox and OneDrive, but its App Store listing does not mention iOS AutoFill or TOTP codes, the two features most people want on a phone.

**MiniKeePass**, once the usual free recommendation, is discontinued: it is no longer on the App Store and its GitHub project is archived. If an old device still has it, copy the database out and move to a maintained app. The keepass.info list also includes smaller apps such as KyPass and OneKeePass, which we have not reviewed here.

## KeePass iPhone Apps Compared

| What a KeePass 2.x user needs | PanicVault | Strongbox | KeePassium |
|---|---|---|---|
| **Opens KDBX 4** | Yes | Yes | Yes |
| **Opens KDBX 3.1** | No (upgrade in KeePass first) | Yes | Yes |
| **Opens KeePass 1.x .kdb** | No (import into KeePass 2.x first) | Yes | Yes |
| **Twofish (KeePass plugin)** | No (switch to AES-256) | Yes | Yes |
| **Key files** | Yes | Yes | Yes |
| **KeePass 2.x TOTP fields (`TimeOtp-`)** | Yes (Base32, hex, Base64) | Yes | Base32 only |
| **KeeTrayTOTP fields** | Yes | Yes | Yes |
| **YubiKey, KeePassXC-style** | NFC on iPhone, USB on Mac (not iPad) | Pro | Premium |
| **KeeChallenge plugin** | No | Not documented | No |
| **Reaching a database on your PC** | iCloud Drive, Google Drive built in; OneDrive, Dropbox via Files | OneDrive, Dropbox, Google Drive, iCloud Drive, WebDAV, SFTP built in | OneDrive, Dropbox, Google Drive, WebDAV direct; others via Files |
| **iOS AutoFill** | Yes, logins suggested above the keyboard | Yes | Yes (above the keyboard: Premium) |
| **Face ID / Touch ID** | Yes | Pro | Yes |
| **Price model** | $4.99 one-time purchase, no tiers | Free (non-commercial) or Pro subscription / lifetime | Free (one database) or Premium subscription / lifetime Pro |
| **Open source** | No | Source published* | Source published* |
| **Mac app** | Yes | Yes | Yes (Mac Catalyst) |

\*Strongbox (AGPL-3.0) and KeePassium (GPLv3) publish their source code, but App Store builds can't be verified against it. According to its App Store listing, KeePassium has been audited by Cure53.

Prices vary by country and change over time, so check them before you buy.

## How to Move Your KeePass Database from Windows to iPhone

KeePass 2.x has no sync service of its own; it opens and saves a file wherever you keep it. So the job is to put that file somewhere both your PC and your phone can reach. First, make a backup copy of the `.kdbx` file outside any sync folder. Our [KeePass backup guide](/keepass/backup-database/) covers how.

### Step 1: Put the .kdbx File in a Cloud Folder

Pick a service with both a Windows client and an iPhone app:

- **OneDrive** is built into Windows; the OneDrive iPhone app makes it available in the Files app.
- **Dropbox** works the same way, with its desktop client on the PC.
- **Google Drive** needs Google Drive for desktop on the PC. PanicVault, Strongbox and KeePassium can all connect to it directly.
- **iCloud Drive** needs [iCloud for Windows](https://support.apple.com/guide/icloud-windows/set-up-icloud-drive-icw0144825a5/icloud), which adds an iCloud Drive folder to File Explorer.

Close KeePass, move the `.kdbx` file into the synced folder, then reopen it with File > Open so KeePass works on the synced copy. With PanicVault, iCloud Drive or Google Drive gives you its built-in sync.

### Step 2: Bring Your Key File Separately

If your master key includes a key file, the iPhone needs it too, because KeePass requires [every part of the master key](https://keepass.info/help/base/keys.html) to open a database. Don't put it in the same cloud folder as the database: anyone who gets into that account would then have both. Move it across once by another route, save it to On My iPhone in the Files app, and select it when you first unlock. Our [key files guide](/keepass/key-files/) covers backups.

If your YubiKey setup uses the KeeChallenge plugin for KeePass 2.x, none of these apps documents support for it. Move the database to KeePassXC-style challenge-response first; [PanicVault's manual](/help/keepass-compatibility/#hardware-keys-and-challenge-response) explains how to recover the secret from KeeChallenge.

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

A `.kdbx` database is one encrypted file. If you change it on your PC and your iPhone before either change has synced, your cloud service may keep two copies. PanicVault merges changes entry by entry for vaults on iCloud Drive or Google Drive, before it saves rather than overwriting them, and shows you any real conflicts to resolve. For a vault in a folder another app syncs, such as Dropbox or OneDrive, it merges the changes that reach the file instead of overwriting them. It does not merge a separate conflicted copy your cloud service keeps; open that copy with **Open Existing Vault** to check whether it holds anything you need.

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
