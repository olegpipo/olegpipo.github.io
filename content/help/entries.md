---
title: "Entries (Passwords)"
description: "Create, edit, and delete PanicVault entries, and use custom fields, tags, expiry dates, history, attachments, icons, and colors."
date: 2026-07-14
lastmod: 2026-08-27
draft: false
silo: "User Manual"
helpgroup: "Passwords & Entries"
weight: 30
---

Entries are the individual items in your vault — each one stores a username, password, URL, and other details for a single account or service. This page covers everything you can do with an entry, from creating it to attaching files and tracking its history.

## Creating a New Entry

1. Tap the **+** button in the toolbar (or use **Cmd+N** on Mac)
2. Fill in the entry fields:
   - **Title** (required) — the name of the account (for example, "GitHub" or "Netflix")
   - **Username** — your login name or email. If you have set a default username in [Vault Settings](/help/vault-settings/), a **Use default** button appears next to the field — tap it to auto-fill the default username.
   - **Password** — your password for this account (tap the dice icon to generate one with the [Password Generator](/help/password-generator/))
   - **URL** — the website address
   - **Notes** — any additional information
3. Optionally choose a group to organize the entry
4. Tap **Save**

## Viewing Entry Details

Tap an entry to see its full details. The detail view shows:

- Title and icon
- Username (with copy button)
- Password (hidden by default — tap "Reveal" to show it, and "Copy" to copy it)
- URL (with a button to open it in your browser)
- Notes
- Custom fields
- Attachments
- One-time password (TOTP) if configured
- Metadata: created date, modified date, last accessed, usage count, and expiry date

PanicVault keeps two of those up to date as you use the entry: copying its username, password or one-time code, or opening its URL sets **Last Accessed** to now and adds one to **Usage Count** — the same bookkeeping KeePassXC does, so the counters stay meaningful when you move a vault between the two apps. Using an entry is not an edit: it does not change the entry's modification date, does not create a history version, and does not save the vault by itself. The new counts are written the next time the vault is saved for a real change; if you lock the vault before that happens, they are simply not recorded.

## Editing an Entry

1. Open the entry detail view
2. Tap **Edit** in the toolbar
3. Make your changes
4. Tap **Save**

When you save a change to an entry, PanicVault automatically keeps the previous version in the entry's history, so you can always look back at what the entry looked like before — not just its old passwords.

## Deleting Entries

Deleted entries are moved to the Recycle Bin, not permanently erased. To delete an entry:

- **iOS**: Swipe left on the entry in the list and tap Delete, or open the entry and choose Delete from the overflow menu
- **Mac**: Right-click the entry and choose Delete, or use the menu

To permanently delete entries, go to the Recycle Bin group and choose **Empty Recycle Bin**. This erases everything the Recycle Bin holds — including any groups another KeePass app moved there, and everything inside them — and cannot be undone.

{{< callout type="tip" >}}
You can find the Recycle Bin in the group filter chips (iOS) or in the sidebar (Mac). It shows as "Trash" on iOS.
{{< /callout >}}

## Entry Fields

Every entry supports these standard fields:

- **Title** — the display name for the entry
- **Username** — your login name, email, or account identifier
- **Password** — your secret password (always stored encrypted)
- **URL** — the website address for this account
- **Override URL** — an alternate URL used for [AutoFill](/help/autofill/) credential matching in addition to the primary URL. This is useful for sites that have a different login URL than their main domain (for example, a site where you log in at accounts.example.com but the main site is example.com). The Override URL is also used for AutoType in other KeePass applications.
- **Notes** — free-form text for any additional information

## Custom Fields

You can add custom fields to any entry for storing extra pieces of information:

1. Edit the entry
2. Scroll to the Custom Fields section
3. Tap **Add Field**
4. Enter a field name and value
5. Toggle the lock icon to mark a field as **protected** (the value is hidden by default and stored with encryption, just like passwords)

Protected custom fields appear with bullet characters in the detail view. Tap the eye icon to reveal them.

## Tags

Tags help you categorize entries across groups. To add tags:

1. Edit the entry
2. Find the Tags field
3. Enter your tags separated by semicolons (for example: "work; finance; important")

Tags appear as colored badges on the entry detail view.

## Entry Expiration

You can set an expiry date on entries to remind yourself to update passwords:

1. Edit the entry
2. Toggle **Entry expires** on
3. Choose an expiry date

Expired entries show a red "EXPIRED" badge in the detail view, and in the entry list their title is greyed out and struck through. Groups can expire too — see [Group Expiration](/help/groups/#group-expiration).

## Entry History

PanicVault keeps a history of changes to each entry. Every time you save an entry with any field changed — password, username, title, URL, notes, custom fields, one-time password, attachments, icon, tags, colors, override URL, auto-type or expiry — the previous version is saved automatically, the same rule KeePassXC follows. Saving an entry you did not actually change adds nothing to its history.

To view history:

1. Open the entry detail view
2. Tap the overflow menu (three dots)
3. Choose **Entry History**

### What the history view shows

The list opens with a **Current** row — the version in the vault right now — followed by every kept version, newest first. Each version shows:

- The date and time it was recorded
- Chips naming what is different between that version and the one above it in the list ("Differs from the version above", or "Differs from the current version" for the newest one) — for example Password, Icon or Attachments
- The values themselves: only the fields that changed by default, with **Show all fields** expanding the row to everything that version held — title, username, password, URL, notes, custom fields, whether a one-time password was configured, attachments with their file sizes, the icon drawn as it was (built-in or custom), tags, colors, override URL, auto-type and expiry

Every kind of change the chips can name has a matching row in the details, so a chip never points at something you cannot then look at.

Passwords in history are masked. Tap **Reveal** to read one, or **Copy** to put it on the clipboard — this is how you get back a password you changed and then needed again. The mask is a fixed row of dots and does not indicate the password's length. Custom fields marked as protected stay masked too, and a one-time password's secret is never shown — history only records whether one was configured.

### Restoring a version

Tap **Restore** on any version to put the entry back to exactly what it held then: password, custom fields, attachments, custom icon, colors, expiry, everything. A confirmation names the version's date and lists what will change before anything is written.

A restore is an ordinary edit, so the version you were on is itself kept in the entry's history — restore the wrong one and you can simply restore back. The entry keeps its identity, stays in its group, keeps the rest of its history, and is saved and synced like any other edit.

Two limits are worth knowing:

- **History does not reach back forever.** The bottom of the history view spells out the window — for example "Keeps up to 10 versions or 6 MB of history" — which you set in [History Settings](/help/vault-settings/#history-settings). Anything older was dropped when those limits were applied, permanently, and cannot be restored. When an entry's history is already full, the version a restore pushes in displaces the oldest one for good; the confirmation says so in as many words and names the version you are about to lose.
- **An entry in the Recycle Bin cannot have a version restored.** Move the entry out of the Recycle Bin first, then restore.

## Attachments

You can attach files to any entry (for example, recovery codes, certificates, or documents).

### Adding attachments

1. Edit the entry
2. Scroll to the Attachments section
3. Tap **Add Attachment**
4. Select one or more files

### Viewing and exporting attachments

1. Open the entry detail view
2. Scroll to the Attachments section
3. Each attachment shows its name and file size
4. Tap the share/export button to save the attachment to your device

## Custom Colors and Icons

You can personalize entries with custom colors and icons.

### Colors

1. Edit the entry
2. Scroll to the Colors section
3. Set a text color and/or background color using the color pickers

### Icons

1. Edit the entry
2. Scroll to the Icon section
3. Choose from the 69 built-in KeePass icons, or
4. Select a custom icon that was previously uploaded to the vault
5. Tap **Upload Custom Icon** to add a new icon from a PNG or JPEG image (automatically resized to 128x128)
6. If the entry has a URL, tap the **globe icon** to automatically fetch the website's favicon and set it as the entry's custom icon — this is the quickest way to give an entry a recognizable icon

Changing an entry's colors or icon is a change like any other, so the previous ones are kept in the entry's [history](#entry-history) — the history view draws each version's icon as it was, and restoring that version brings the icon back.

{{< callout type="tip" >}}
Favicon auto-fetch downloads the site's icon, resizes it, and saves it as a custom icon in your vault. It works best when the URL field contains a valid website address.
{{< /callout >}}

## Moving Entries Between Groups

You can move an entry to a different group:

1. Open the entry detail view
2. Tap the overflow menu (three dots)
3. Choose **Move to Group...**
4. Select the target group

On Mac, you can also drag and drop entries from the entry list onto a group in the sidebar. To move multiple entries at once, see [Bulk Operations](/help/bulk-operations/) and [Drag and Drop on Mac](/help/drag-and-drop/).
