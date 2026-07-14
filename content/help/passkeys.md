---
title: "Passkeys (WebAuthn)"
description: "PanicVault stores and displays WebAuthn passkeys using the KeePassXC KPEX_PASSKEY_ format, so passkeys stay readable across KeePass clients."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "User Manual"
helpgroup: "2FA & Passkeys"
weight: 100
---

PanicVault can store passkeys alongside your passwords. Passkeys are a modern, phishing-resistant alternative to passwords based on the WebAuthn standard. If you use KeePassXC or another KeePass client that supports passkeys, PanicVault preserves and displays that data.

## Viewing Passkey Data

When an entry contains passkey data, the detail view shows a **Passkey** section with:

- **Credential ID** -- the unique identifier for the passkey
- **Relying Party** -- the website or service the passkey is registered with
- **User Handle** -- the user identifier associated with the passkey
- **User Name** -- the display name for the passkey user

Entries with passkeys show a passkey badge so you can easily identify them in the entry list.

## KeePassXC Compatibility

PanicVault uses the KeePassXC passkey format, storing passkey data in custom fields prefixed with `KPEX_PASSKEY_`. This means passkeys created in KeePassXC are fully visible in PanicVault, and vice versa.

Related pages: [Entries (Passwords)](/help/entries/) for custom fields in general, and [KeePass Compatibility](/help/keepass-compatibility/) for what else PanicVault preserves from other clients.
