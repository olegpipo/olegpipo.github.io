---
title: "Entries (Passwords)"
description: "Create, edit, and delete PanicVault entries, and use custom fields, tags, expiry dates, history, attachments, icons, and colors."
date: 2026-07-14
lastmod: 2026-07-14
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

## Editing an Entry

1. Open the entry detail view
2. Tap **Edit** in the toolbar
3. Make your changes
4. Tap **Save**

When you change a password, PanicVault automatically saves the old version in the entry's history so you can always look back at previous passwords.

## Deleting Entries

Deleted entries are moved to the Recycle Bin, not permanently erased. To delete an entry:

- **iOS**: Swipe left on the entry in the list and tap Delete, or open the entry and choose Delete from the overflow menu
- **Mac**: Right-click the entry and choose Delete, or use the menu

To permanently delete entries, go to the Recycle Bin group and choose **Empty Recycle Bin**.

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

Expired entries show a red "EXPIRED" badge in the detail view.

## Entry History

PanicVault keeps a history of changes to each entry. Every time you save an entry with a changed password, the previous version is saved automatically.

To view history:

1. Open the entry detail view
2. Tap the overflow menu (three dots)
3. Choose **Entry History**

The history view shows each previous version with the date, what changed (title, username, password, URL, notes, etc.), and you can expand each version to see the details.

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
