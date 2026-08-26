---
title: "Groups & Folders"
description: "Organize PanicVault entries with groups: create subgroups, edit names, notes and icons, reorder groups, and move them between parents."
date: 2026-07-14
lastmod: 2026-08-26
draft: false
silo: "User Manual"
helpgroup: "Passwords & Entries"
weight: 40
---

Groups help you organize your entries into categories like "Social Media", "Finance", "Work", and so on. Groups can be nested to create a folder structure, and this page covers how to create, edit, reorder, move, and delete them on both iOS and Mac.

## Creating Groups

- **iOS**: Scroll to the end of the group filter chips and tap the **+** icon, then enter a name
- **Mac**: Click the folder-plus icon in the sidebar toolbar, then enter a name

## Creating Subgroups

To create a group inside another group:

- **iOS**: Long-press a group chip and choose **Add Subgroup**
- **Mac**: Right-click a group in the sidebar and choose **Add Subgroup**

## Editing Group Properties

Long-press (iOS) or right-click (Mac) a group and choose **Edit Group...** to change:

- **Name** — the display name of the group
- **Parent Group** — move the group under a different parent (see "Moving Groups Between Parents" below)
- **Notes** — a description or memo for the group
- **Icon** — choose from built-in icons, custom icons, or upload a new custom icon
- **Expires** — give the group an expiry date (see [Group Expiration](#group-expiration) below)

The edit view also shows read-only info: creation date, modification date, number of entries, and number of subgroups. An expired group shows a red "EXPIRED" badge there too.

## Group Notes

Groups have an optional notes field where you can store a description, instructions, or any other text. Edit a group's notes from the **Edit Group...** view. On Mac, group notes appear as small gray text under the group name in the sidebar, so you can see the context at a glance without opening the group.

## Group Icons

You can set a custom icon on any group to make it easier to identify. In the **Edit Group...** view, choose from the 69 built-in KeePass icons, select a custom icon already in your vault, or upload a new one from a PNG or JPEG image. Custom group icons appear in the sidebar on Mac and in the group filter chips on iOS.

## Group Expiration

Groups can be given an expiry date, the same way [entries can](/help/entries/#entry-expiration):

1. Long-press (iOS) or right-click (Mac) the group and choose **Edit Group...**
2. Toggle **Group expires** on
3. Choose an expiry date

Once that date has passed, the group's name is greyed out and struck through — in the sidebar on Mac and in the group filter chips on iOS — and the entries inside it are shown the same way. Nothing is deleted or hidden: an expired group is a reminder, exactly as it is in KeePassXC, and the two apps read each other's group expiry dates.

## Renaming Groups

Long-press (iOS) or right-click (Mac) a group and choose **Rename** to quickly change its name.

## Reordering Groups

You can change the order in which groups appear:

- **Mac**: Right-click a group in the sidebar and choose **Move Up** or **Move Down** to shift it within its parent
- **iOS**: Tap the reorder button (arrows icon) next to the **+** button in the group filter chips area. This opens a **Manage Groups** sheet with drag handles — drag groups up or down to rearrange them

## Moving Groups Between Parents

To move a group to a different location in the group hierarchy:

- **Edit Group...** — long-press (iOS) or right-click (Mac) the group, choose **Edit Group...**, then change the **Parent Group** picker to the desired parent
- **Drag and Drop (Mac)** — drag the group onto another group in the sidebar to make it a subgroup, or drag it onto the **GROUPS** header to move it to the root level (see [Drag and Drop on Mac](/help/drag-and-drop/))

## Deleting Groups

Long-press (iOS) or right-click (Mac) a group and choose **Delete**. When you delete a group, its entries are moved to the parent group — they are not lost.
