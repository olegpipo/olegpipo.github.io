---
title: "Importing Passwords"
description: "Import a CSV from Apple Passwords, Chrome, Firefox, Bitwarden, KeePassXC, 1Password, LastPass, or mSecure, with TOTP, folders, and custom fields."
date: 2026-07-14
lastmod: 2026-11-04
draft: false
silo: "User Manual"
helpgroup: "Passwords & Entries"
weight: 70
---

You can bring passwords into PanicVault from other password managers and browsers by importing a CSV file. Imported entries are added directly to the vault you have open, and PanicVault detects which app the file came from automatically. Going the other way is covered in [Exporting Passwords to CSV](/help/exporting-passwords/).

## Before You Import

You must open and unlock a vault first. Importing adds the entries to the currently open vault, so the import command stays disabled until a vault is unlocked. If the menu item is greyed out, unlock a vault and try again.

## Starting an Import

- **Mac**: Choose **File > Import Passwords from CSV...** from the menu bar, or press **Cmd+Shift+I**.
- **iOS**: Tap the **"..."** (ellipsis) menu in the entry list toolbar and choose **Import Passwords from CSV**.

Then choose a CSV file. PanicVault reads the file, detects which app it came from, and shows an import sheet.

## Supported Formats

PanicVault automatically detects CSV exports from:

- **Apple Passwords / Safari**
- **Chrome, Edge, and other Chromium browsers** (including Brave)
- **Firefox**
- **Bitwarden**
- **KeePassXC** — including exports from versions before 2.6.3, which have no TOTP column
- **1Password 8**
- **LastPass** — see [Importing from LastPass](#importing-from-lastpass)
- **mSecure 6** — no header row needed (see [Importing from mSecure](#importing-from-msecure))
- **PanicVault** — its own CSV export (see [Exporting Passwords to CSV](/help/exporting-passwords/))

Any other CSV also works as long as it has a password column. PanicVault matches the remaining columns — title, username, URL, notes, and tags — by their header names, so most generic exports import correctly without any setup. Every other column is kept too: each becomes a custom field named after its header (see [Custom Fields](/help/entries/#custom-fields)), and a row with data only in such columns is still imported.

## What Each Format Brings

Besides the title, username, password, website, notes, and one-time password, PanicVault keeps what each app adds to its export:

- **Bitwarden** — your custom fields become custom fields with the same names (see [Custom Fields](/help/entries/#custom-fields)). The export doesn't say which ones were hidden, so a field is protected when its name says it holds a secret, such as **PIN** or **Password**. Favorites get the tag **Favorite** and archived items the tag **Archived** (see [Tags](/help/entries/#tags)), and secure notes get the note icon. When a login has several websites, the first is the entry's website and the others become **KP2A_URL_1**, **KP2A_URL_2**, and so on, the fields KeePassXC uses for more websites. Bitwarden's master password re-prompt setting isn't imported: a vault has no such setting.
- **Firefox** — each login keeps its dates: when it was created, when its password was last changed (the entry's modified date), and when it was last used. A site that asks for its password in a browser dialog keeps its realm in the custom field **HTTP Realm**, and a login form that sends the password to another site keeps that site in **Form Action Origin**.
- **KeePassXC** — each entry keeps its icon and its created and modified dates.
- **1Password 8** — favorites get the tag **Favorite** and archived items the tag **Archived**; 1Password's tags become tags.
- **LastPass** — folders, favorites, and the fields of secure notes; see [Importing from LastPass](#importing-from-lastpass).
- **Apple Passwords and Chrome** — their exports hold nothing more, and every column comes across.
- **PanicVault** — everything its export holds: each entry's group, tags, icon, dates, expiry, and every custom field with its name, its protection, and its place in the list, exactly as the vault had them (see [What the File Contains](/help/exporting-passwords/#what-the-file-contains)).

The dates appear in the entry's details. When a file has no dates, the imported entries are dated the moment you import them.

## Importing from mSecure

PanicVault reads mSecure 6's own CSV export as it is. The file needs no header row: PanicVault recognizes it by its **mSecure6 CSV export file** first line, or by the way mSecure writes each record. If you added a header row yourself, it is recognized and never imported as an entry.

Every field of every record comes across, not only the passwords:

- **Title** — the record's name, without the record number mSecure adds after it.
- **Username, Password, Website, and One-Time Password** — the record's first field of each kind fills the entry's own field, so AutoFill and two-factor codes work right away.
- **Every other field** — card numbers, expiration dates, PINs, account and routing numbers, a second password, and so on — becomes a custom field with the same name (see [Custom Fields](/help/entries/#custom-fields)). When two fields share a name, the second one gets a number, such as **PIN (2)**.
- **Protected fields** — passwords, card numbers, sensitive numbers, one-time password secrets, and fields whose name says they hold a secret (such as PIN, CVV, Security Code, or Passcode) become protected custom fields: hidden until you reveal them, like the password.
- **Template** — the record's type (Login, Credit Card, Bank Account, Secure Note...) is added as a tag and picks the entry's icon.
- **Tags and notes** — mSecure's tags become the entry's tags (see [Tags](/help/entries/#tags)), and the note becomes the entry's notes, line breaks included.

Records without a password, such as secure notes, cards, and identities, are imported too.

## Importing from LastPass

PanicVault recognizes LastPass's CSV export, with or without its **totp** column:

- **Sites** — the website, username, password, one-time password, and notes fill the entry's own fields. A site with nothing but a name is skipped, like an empty row.
- **Favorites** get the tag **Favorite** (see [Tags](/help/entries/#tags)).
- **Folders** — LastPass writes a folder inside a folder as **Parent\Child**, and a shared folder as **Shared-Name\Folder**. With **Recreate folders as groups** on, each becomes nested groups (see [Recreating Folders as Groups](#recreating-folders-as-groups)).
- **Secure notes** — a plain note's text becomes the entry's notes. A note made from a template (Credit Card, Bank Account, Address, Wi-Fi Password, SSH Key, or one of your own) is split into fields: its **Username** and **Password** fill the entry's own fields, every other field you filled in becomes a custom field with the same name, its **Notes** become the entry's notes, and the template's name is added as a tag and picks the entry's icon. Card numbers, security codes, PINs, passwords, passphrases, and private keys are protected. Empty fields are left out.

## The Import Sheet

After you pick a file, the import sheet shows:

- **Detected format** — the app PanicVault recognized (or "Generic CSV")
- **Entries found** — how many rows were parsed into importable entries
- **Add to group** — the destination group for the imported entries. When the file's folders are recreated (below), this starts at the vault root, so they appear at the top level as they did in the other app. Otherwise it defaults to a group named **General** if your vault has one, or the vault root. You can choose any group you like.
- **Recreate folders as groups** — shown when the file puts entries in folders, and on by default. The line under it says how many new groups the import will create and how many groups already in your vault it will use.

Tap **Import** to add the entries. When the import finishes, a summary tells you how many entries were imported, how many empty rows were skipped, and how many groups were created. If you picked the wrong file, tap **Choose a Different File** before importing.

### Recreating Folders as Groups

With **Recreate folders as groups** on, each entry goes into the group of its folder, under the destination group (see [Groups & Folders](/help/groups/)):

- **Nested folders become nested groups.** Bitwarden writes a folder inside a folder as **Parent/Child**, LastPass as **Parent\Child**. KeePassXC and PanicVault write the whole path from the top, such as **Root/Banking/Cards**; the first name is the other vault's top-level group, so it is left out and **Banking** is created right under the destination. An item of a Bitwarden organization export that is in several collections goes into the first one. A 1Password file with a vault column gets one group per vault. Apple Passwords, Chrome, Firefox, 1Password 8 and mSecure exports have no folders.
- **Groups you already have are used.** A folder goes into the group of the same name under the destination, whatever its upper and lower case (**banking** finds **Banking**), and only the missing groups are created. Importing the same file again into the same place adds its entries to the groups it created the first time, instead of making a second **Banking**. The import doesn't skip entries you already have, so a second import adds the entries a second time.
- **Entries in no folder** go into the destination group itself.
- **The Recycle Bin is never used.** Nothing is created or imported inside it. KeePassXC exports its Recycle Bin like any other folder: those entries arrive in an ordinary group named **Recycle Bin**, where you can look through what you had deleted, then delete the group if you don't need it.

Turn the toggle off to put every entry into the destination group, as earlier versions did.

{{< callout type="tip" >}}
To rebuild a vault's groups from a CSV, export it from PanicVault (see [Exporting Passwords to CSV](/help/exporting-passwords/)) and import the file with **Add to group** set to **Vault (root)**. Groups without entries aren't in a CSV, so they aren't recreated. A **/** in a group name reads as a folder inside a folder: **TV/Streaming** comes back as **Streaming** inside **TV**, unless the vault already has a group named **TV/Streaming**, which is then used.
{{< /callout >}}

Some exports contain invisible control characters, such as the vertical tab some apps use as a line break, which a KeePass vault can't store. PanicVault cleans them as it imports (a line break in notes, a space in one-line fields such as the title or password), and the sheet and the summary say how many fields it cleaned; see [Characters the KeePass Format Doesn't Allow](/help/keepass-compatibility/#characters-the-keepass-format-doesnt-allow).

## Two-Factor (TOTP) Columns

If the CSV includes a one-time-password column — such as the **OTPAuth** column from Apple Passwords, the **TOTP** column from KeePassXC and Bitwarden, or LastPass's **totp** column — PanicVault imports it into the entry's One-Time Password field. Those entries generate 2FA codes right away, just like TOTP you set up by hand (see [Two-Factor Authentication (TOTP)](/help/two-factor-authentication/)).

## Exporting a CSV from Other Apps

Each source app has its own export command. A few common ones:

- **Apple Passwords** (Mac) — open the **Passwords** app and use **File > Export** to save your passwords as a CSV
- **Chrome** — open **Google Password Manager**, go to **Settings**, and choose **Export passwords**
- **Edge** — go to **Settings > Profiles > Passwords**, then use the **"..."** menu and choose **Export passwords**
- **Firefox** — open **Passwords** (about:logins), use the **"..."** menu, and choose **Export Logins...**
- **Bitwarden** — in the web or desktop app, choose **Tools > Export Vault** and pick the **.csv** format
- **KeePassXC** — choose **Database > Export > Export to CSV...**
- **1Password 8** — open the account or vault menu and choose **Export**, then select **CSV**
- **LastPass** — in the LastPass browser extension, choose **Account > Fix a problem yourself > Export vault items > Export data for use anywhere**, and enter your master password if LastPass asks for it. LastPass's CSV doesn't include attachments.
- **mSecure 6** (Mac) — choose **File > Export > CSV**, name the file, and click **Export**. On Windows, click the **Settings** (gear) icon, choose **Backups**, then **Export Data to CSV File** (it exports the current view, so open **All Items** first)

{{< callout type="tip" >}}
These menus change between app versions. If you cannot find the export command, search the app's help for "export CSV".
{{< /callout >}}

## Security Notes

Importing is designed to keep your passwords safe:

- The CSV is parsed entirely in memory. PanicVault never writes the raw CSV file to disk — only the resulting entries are saved into your encrypted vault.
- A CSV export is **plaintext** — anyone who opens the file can read every password in it. As soon as the import finishes, delete the CSV file, then empty the Trash so it cannot be recovered.

{{< callout type="warning" >}}
Never leave an exported password CSV sitting in your Downloads folder or a cloud drive. Treat it like a written list of all your passwords, because that is exactly what it is.
{{< /callout >}}
