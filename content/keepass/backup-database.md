---
title: "How to Safely Back Up Your KeePass Database"
description: "Learn how to back up your KeePass database using the 3-2-1 rule, encrypted cloud storage, automated scripts, and versioning to prevent data loss."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

Your [KeePass](/keepass/) database is a single file. That simplicity is one of its greatest strengths -- there is no server dependency, no cloud infrastructure, no subscription service standing between you and your passwords. But it also means that if you lose that file, you lose everything in it. Every password, every login, every secure note, gone. There is no customer support to call, no "forgot my vault" recovery flow, no server-side backup waiting to restore your data. The KDBX file on your disk is the only copy that exists unless you deliberately create others.

This guide covers how to build a backup strategy for your KeePass database that protects against hardware failure, accidental deletion, theft, ransomware, fire, flood, and every other scenario that could separate you from your vault. We will walk through the 3-2-1 backup rule, encrypted cloud backups, USB and external drive strategies, automated backup scripts, versioning, restore testing, and the critical mistakes you need to avoid.

## Why Backups Are Non-Negotiable

A password manager without a backup is a single point of failure for your entire digital life. Consider the scenarios:

- **Hard drive failure.** SSDs and HDDs fail without warning. A sudden controller failure, firmware bug, or physical damage can make your entire drive unreadable in an instant.
- **Accidental deletion.** You clean up your files and accidentally delete the wrong one. Or a family member, not knowing what the .kdbx file is, moves it to the trash and empties it.
- **Ransomware.** Malware encrypts every file on your computer, including your password database. Without a backup stored separately, you face paying the ransom or losing your vault.
- **Theft.** Your laptop is stolen. The thief cannot open your encrypted database (assuming your master password and [key file](/keepass/key-files/) are strong), but you still need to access your passwords from another device.
- **Software corruption.** A power loss during a database write operation could corrupt the file. KeePass and KeePassXC include safeguards against this (they write to a temporary file and rename it atomically), but no safeguard is perfect.
- **Physical disaster.** A fire, flood, or natural disaster destroys your home and every device and storage medium in it.

Each of these scenarios has happened to real people. The question is not whether you will face one of them -- it is when. Backups transform catastrophic data loss into a minor inconvenience.

## The 3-2-1 Backup Rule

The 3-2-1 rule is the gold standard for backup strategies across all domains, from enterprise data centers to personal file management. Applied to your KeePass database, it means:

- **3 copies** of your database file should exist at all times.
- **2 different types of storage media** should hold those copies (for example, your computer's SSD and a USB flash drive, or a cloud service and an external hard drive).
- **1 copy should be offsite** -- stored in a physically separate location from the others.

### Why Three Copies

Two copies protect against single-device failure. Three copies protect against the scenario where your primary and first backup are compromised simultaneously -- which is more common than you might think. If your computer and your USB backup drive are both on your desk when a power surge hits, you lose both. If both are in your house when a pipe bursts, you lose both. The third copy, stored offsite, survives.

### Why Two Media Types

Different storage media have different failure modes. SSDs can fail due to controller issues. USB drives can fail due to flash memory degradation. Optical discs can degrade in humidity. Cloud services can have outages or account lockouts. By spreading your copies across media types, you avoid a single failure mode taking out all your backups simultaneously.

### Why One Offsite Copy

Local disasters -- fires, floods, theft, burglary -- can destroy everything in a single location. An offsite copy ensures that even a total loss of your home or office does not mean total loss of your vault.

## Encrypted Cloud Backup

Cloud storage is one of the most practical ways to maintain an offsite backup. Your KeePass database is already encrypted with AES-256 or ChaCha20, so uploading the .kdbx file to a cloud service does not expose your passwords -- the cloud provider sees only encrypted data.

### Choosing a Cloud Service

Any reputable cloud storage provider works for this purpose:

- **Google Drive, OneDrive, Dropbox, iCloud**: Widely available, often already set up on your devices.
- **Proton Drive, Tresorit, Sync.com**: End-to-end encrypted storage for an additional privacy layer.
- **Backblaze B2, Wasabi, AWS S3**: Object storage services suitable for automated backup scripts.

The key consideration is not which service you choose, but that the service is different from where your primary database lives. If your working database is in a Dropbox-synced folder, your backup should be on a different service or a local device.

### Cloud Backup Best Practices

1. **Upload the .kdbx file directly.** It is already encrypted. Do not unzip, decrypt, or export the contents before uploading.
2. **Enable versioning on your cloud storage.** Most services support file versioning, which means previous versions of the file are retained when you upload a new one. This protects against uploading a corrupted file and overwriting the last good copy.
3. **Use a separate cloud account for backups** if practical. This adds a layer of protection: if your primary cloud account is compromised, your backup account remains intact.
4. **If you use a key file**, do NOT store the key file in the same cloud account as the database. An attacker who compromises that account would get both factors. Store the key file separately or on physical media only.

### A Note on Syncing vs. Backing Up

Syncing and backing up are not the same thing, though they are frequently confused.

**Syncing** keeps a file identical across multiple devices in real time. If you delete the file on one device, the sync service deletes it on all devices. If you corrupt the file on one device, the corrupted version propagates everywhere. Sync is useful for accessing your vault from multiple devices, but it is not a backup.

**Backing up** creates a point-in-time copy that exists independently of the original. Deleting or corrupting the original does not affect the backup. Backups are what save you when things go wrong.

You can use sync services for backup, but you must take additional steps: enable versioning, maintain copies outside the sync folder, or use a separate account. Do not assume that because your .kdbx file is in Dropbox, it is backed up.

## USB and External Drive Backups

Physical media provides an offsite backup option that does not depend on internet access or cloud service availability. It also ensures that your backup is completely offline and unreachable by any attacker who does not have physical access.

### USB Flash Drives

USB drives are cheap, small, and easy to store in a safe deposit box, a fireproof safe, or at a trusted friend's home.

1. Copy your .kdbx file to the USB drive.
2. Safely eject the drive.
3. Store the drive in a secure, offsite location.
4. Update the backup periodically (monthly is a reasonable cadence for most people).

**Flash memory limitations:** USB drives use NAND flash memory, which can degrade over time, especially in extreme temperatures. Data retention for modern USB drives is typically 10 years or more under normal conditions, but you should refresh your backups annually regardless. Copy the file to a fresh drive and verify the copy.

### External Hard Drives

For larger backup strategies that include more than just your password database, an external hard drive provides ample space and reliable storage. Keep the drive disconnected and stored offsite when not in use.

### Verifying Physical Backups

After every copy operation, verify the integrity of the backup:

```
# Compare checksums of the original and backup
sha256sum ~/Documents/Vault.kdbx
sha256sum /media/usb/Vault.kdbx
```

If the checksums match, the copy is exact. If they differ, the copy failed and needs to be repeated.

## Automated Backup Scripts

Manual backups are better than no backups, but they depend on you remembering to do them. Automated backup scripts remove the human factor.

### Linux/macOS: A Simple Backup Script

```bash
#!/bin/bash
# backup-vault.sh - Back up KeePass database with timestamp

SOURCE="$HOME/Documents/Vault.kdbx"
BACKUP_DIR="$HOME/VaultBackups"
DATE=$(date +%Y%m%d-%H%M%S)
BACKUP_FILE="$BACKUP_DIR/Vault-$DATE.kdbx"

# Create backup directory if it doesn't exist
mkdir -p "$BACKUP_DIR"

# Copy the database with a timestamp
cp "$SOURCE" "$BACKUP_FILE"

# Verify the copy
if [ "$(sha256sum "$SOURCE" | cut -d' ' -f1)" = "$(sha256sum "$BACKUP_FILE" | cut -d' ' -f1)" ]; then
    echo "Backup successful: $BACKUP_FILE"
else
    echo "ERROR: Backup verification failed!" >&2
    exit 1
fi

# Remove backups older than 90 days
find "$BACKUP_DIR" -name "Vault-*.kdbx" -mtime +90 -delete
```

Schedule this script to run daily using cron:

```
# Run backup every day at 2:00 AM
0 2 * * * /home/user/scripts/backup-vault.sh
```

### Windows: PowerShell Backup Script

```powershell
# backup-vault.ps1
$Source = "$env:USERPROFILE\Documents\Vault.kdbx"
$BackupDir = "$env:USERPROFILE\VaultBackups"
$Date = Get-Date -Format "yyyyMMdd-HHmmss"
$BackupFile = "$BackupDir\Vault-$Date.kdbx"

# Create backup directory
New-Item -ItemType Directory -Force -Path $BackupDir | Out-Null

# Copy the database
Copy-Item $Source $BackupFile

# Verify
$SourceHash = (Get-FileHash $Source -Algorithm SHA256).Hash
$BackupHash = (Get-FileHash $BackupFile -Algorithm SHA256).Hash

if ($SourceHash -eq $BackupHash) {
    Write-Host "Backup successful: $BackupFile"
} else {
    Write-Error "Backup verification failed!"
    exit 1
}

# Remove backups older than 90 days
Get-ChildItem $BackupDir -Filter "Vault-*.kdbx" |
    Where-Object { $_.LastWriteTime -lt (Get-Date).AddDays(-90) } |
    Remove-Item
```

Schedule with Windows Task Scheduler or set it to run on login.

### What to Back Up

Your backup should include:

- **The .kdbx database file.** This is the essential item.
- **Your key file** (if you use one). Back this up separately from the database, ideally to different media or locations. See our [key file guide](/keepass/key-files/) for detailed key file backup strategies.
- **Your KeePassXC configuration** (optional). If you have customized settings, auto-type sequences, or browser integration configurations, backing up the config file saves you from reconfiguring after a restore.

## Versioning: Protecting Against Corruption

A single backup file is a snapshot of a single moment. If your database becomes corrupted and you back up the corrupted file, you have two copies of a broken database. Versioning solves this by maintaining multiple historical copies.

### Timestamp-Based Versioning

The backup scripts above use timestamps in filenames (Vault-20260213-143000.kdbx), creating a new file for each backup. This is the simplest form of versioning -- you can look through your backup directory and find a copy from any date your script ran.

Retention policies keep the backup directory manageable:

- **Keep daily backups for 30 days.**
- **Keep weekly backups for 6 months.**
- **Keep monthly backups for 2 years.**

This gives you fine-grained recovery options for recent corruption and long-term protection against problems you discover late.

### Cloud Storage Versioning

Most cloud storage services offer built-in versioning:

- **Google Drive**: Keeps versions for 30 days, up to 100 versions.
- **Dropbox**: Keeps versions for 30-180 days depending on your plan.
- **OneDrive**: Keeps versions accessible through the file's version history.
- **S3/B2**: Versioning can be enabled on a per-bucket basis with configurable retention.

Enable versioning on whatever cloud service holds your backup. It costs virtually nothing in storage and can save your vault if the latest upload was corrupted.

## Testing Your Restores

A backup you have never tested is a backup you cannot trust. Restore testing is the most important and most frequently skipped step in any backup strategy.

### How to Test a Restore

1. Copy the backup file to a temporary location (not the same directory as your working database, to avoid confusion).
2. Open the backup copy in KeePassXC or your preferred [compatible app](/keepass/compatible-apps/).
3. Enter your master password (and provide your key file if applicable).
4. Verify that the database opens successfully and contains your expected entries.
5. Check a few specific entries to confirm the data is intact and current.
6. Close the test copy and delete it from the temporary location.

### When to Test Restores

- **After setting up your backup system for the first time.** Verify the process works before you need it.
- **After changing your master password or key file.** Ensure backups made with the old credentials are still restorable (they will require the old master password and key file to open).
- **Quarterly**, as part of routine maintenance.
- **After any significant change to your backup infrastructure** (new cloud provider, new script, new storage location).

A backup strategy that has been tested is worth infinitely more than one that has not. Spend ten minutes quarterly to confirm your safety net works.

## What NOT to Do

Certain practices undermine your backup strategy or create risks that outweigh the benefits. Avoid these common mistakes.

### Do Not Export Your Database to Unencrypted Formats

KeePass and KeePassXC can export your database to CSV, XML, HTML, and other formats. These exports are plaintext -- every password, username, URL, and note is exposed in cleartext. An unencrypted export is the most dangerous file on your computer.

If you need an export for migration purposes, create it, use it immediately, and securely delete it. Do not store unencrypted exports as "backups." Your .kdbx file is already the backup -- it just happens to also be encrypted.

### Do Not Store Backups on the Same Physical Device

A backup on the same hard drive as the original protects against accidental deletion but not against drive failure, theft, ransomware, or physical disaster. Always maintain at least one copy on a separate physical device.

### Do Not Rely Solely on Cloud Sync

As discussed above, sync is not backup. If your database is only in a synced folder with no additional copies, you are one accidental deletion or corrupted save away from losing everything.

### Do Not Skip Key File Backups

If your database requires a key file to open, backing up only the .kdbx file is insufficient. You need both the database and the key file to access your passwords. Back up the key file separately and securely, following the guidelines in our [key file documentation](/keepass/key-files/).

### Do Not Forget About the KDBX Format Itself

Part of your backup strategy should consider the long-term accessibility of the format. The KDBX format is open and well-documented, meaning your backups will remain readable even if specific software is discontinued. This is one of the key advantages of the [KDBX format](/keepass/kdbx-format-guide/) over proprietary vault formats. You are not backing up data that only one vendor's software can read.

### Do Not Assume Backups Are Working

Automated scripts can fail silently. Cron jobs stop running after system updates. Cloud sync pauses due to storage limits. Check your backup system monthly to confirm that new backups are actually being created and that the files are valid.

## Building a Complete Backup Plan

Here is a practical example of a complete 3-2-1 backup strategy for a KeePass database:

### Copy 1: Working Database (Primary)

- **Location:** Your computer's local filesystem (e.g., ~/Documents/Vault.kdbx).
- **Media:** Internal SSD.
- **Purpose:** Day-to-day use. This is the file you open and modify.

### Copy 2: Cloud Backup (Offsite)

- **Location:** Encrypted cloud storage (e.g., a Proton Drive folder or a versioned S3 bucket).
- **Media:** Cloud storage.
- **Purpose:** Offsite backup, accessible from any device with internet access.
- **Update frequency:** Daily (automated).

### Copy 3: Physical Backup (Offsite, Offline)

- **Location:** USB drive in a fireproof safe or safe deposit box.
- **Media:** USB flash drive.
- **Purpose:** Disaster recovery. Survives fire, flood, internet outage, and cloud account compromise.
- **Update frequency:** Monthly (manual).

### Key File Backup (If Applicable)

- **Copies on two USB drives** stored in separate physical locations, neither of which is the same location as the USB drive holding Database Copy 3.
- **NOT stored in the same cloud account** as the database backup.

### Verification Schedule

- **Weekly:** Confirm the automated cloud backup ran and the latest file has a recent timestamp.
- **Monthly:** Update the physical USB backup. Verify the checksum matches the working copy.
- **Quarterly:** Perform a full restore test using each backup copy.

This plan requires perhaps 30 minutes per month of active maintenance. That is a trivial investment compared to the hours or days you would spend recovering from a lost vault.

## Handling Breaches and Compromised Backups

If you suspect your database file has been compromised -- for example, if a cloud account holding a backup was breached -- your immediate steps should be:

1. **Change your master password** on the working copy of the database.
2. **Replace your key file** (if applicable) with a newly generated one.
3. **Rotate passwords** for your most critical accounts (email, banking, primary services).
4. **Create new backups** with the updated credentials.
5. **Securely delete** any old backups that used the compromised master password.

The encrypted nature of the .kdbx file means that an attacker who obtains a backup copy still needs your master password and key file to access the contents. But if your master password was weak, if your key file was stored alongside the database, or if you have reason to believe the attacker may have both, treat the breach as a full compromise. For more on responding to security incidents, see our guides on [handling breaches](/password-managers/handling-breaches/) and [what happens if your password manager is hacked](/password-managers/what-if-hacked/).

## Portability as a Backup Advantage

One of the underappreciated benefits of the KeePass ecosystem is that your backups are inherently portable. The KDBX format is supported by dozens of applications across every platform. A backup of your database is not locked to a specific application, operating system, or vendor. If KeePassXC were to be discontinued tomorrow, you could open your backup in KeePass, Strongbox, [PanicVault](https://panicvault.com), KeePassDX, or any other [compatible application](/keepass/compatible-apps/).

This portability means your backup strategy does not depend on any single piece of software continuing to exist. For more on why this matters and how it compares to proprietary alternatives, see our article on [data portability](/keepass/data-portability/).

## Conclusion

Your KeePass database is a single file containing the keys to your entire digital life. Losing it means losing access to every account, every credential, and every secure note you have stored. The database's single-file simplicity makes it extraordinarily easy to back up -- there are no databases to export, no configurations to replicate, no server infrastructure to mirror. Just copy the file.

Follow the 3-2-1 rule: three copies, two media types, one offsite. Automate the process so it does not depend on your memory. Enable versioning so a corrupted backup does not overwrite the last good copy. Test your restores quarterly so you know the backups work before you need them.

The time to build your backup strategy is now, before the hard drive fails, before the ransomware hits, before the accidental deletion happens. Thirty minutes of setup and thirty minutes per month of maintenance is all it takes to ensure that your passwords survive anything.
