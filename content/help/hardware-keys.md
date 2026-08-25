---
title: "Hardware Keys (YubiKey)"
description: "Protect a PanicVault vault with a YubiKey — challenge-response over NFC on iPhone and USB on Mac, slot selection, backup keys, and troubleshooting."
date: 2026-08-25
lastmod: 2026-08-25
draft: false
silo: "User Manual"
helpgroup: "Settings"
weight: 155
---

A hardware key is a small physical device — a YubiKey — that you tap against your iPhone or plug into your Mac to unlock your vault. Like a key file, it is an extra factor on top of your master password, but unlike a file it cannot be copied: the secret lives inside the key's chip and never comes out. PanicVault uses the same challenge-response scheme as KeePassXC, so a vault protected by a YubiKey opens in both apps.

## What a Hardware Key Does

When you unlock a hardware-key vault, PanicVault sends the key a challenge — a block of data taken from the vault file itself. The YubiKey computes an answer using an HMAC-SHA1 secret that only it holds, and sends the answer back. PanicVault mixes that answer into the vault's encryption key alongside your master password, then discards it.

This means:

- **The secret never leaves the key.** PanicVault never sees it, never stores it, and never syncs it. It also never stores the key's answer or its serial number.
- **The vault file itself is unchanged.** A hardware-key vault is a normal .kdbx file. Nothing inside it records that a YubiKey is required, which is also why PanicVault has to remember that fact for you.
- **Both factors are needed.** Someone who steals your vault file and learns your master password still cannot open it without your YubiKey. Someone who steals your YubiKey cannot open it without your master password.

## Which YubiKeys and Devices Work

PanicVault supports **YubiKey challenge-response over NFC on iPhone, and over USB on Mac**.

- **iPhone — NFC.** A YubiKey with NFC and an HMAC-SHA1 challenge-response slot, such as the YubiKey 5 NFC or 5C NFC. You hold the key against the top of the phone.
- **Mac — USB.** Any USB YubiKey with an HMAC-SHA1 challenge-response slot. You plug it into a USB port.

Those two are the whole list. What does **not** work:

- **iPad.** iPad cannot read a YubiKey in PanicVault. Unlock the vault on an iPhone or a Mac instead.
- **A YubiKey plugged into an iPhone or iPad over USB-C.** The YubiKey answers challenge-response only over a USB channel that iOS does not make available to apps. This is a limitation of the key and of iOS, not something PanicVault can work around.
- **Lightning keys, including the YubiKey 5Ci.** Not supported, on any device.
- **An external NFC reader plugged into a Mac.** Not supported. On a Mac, use a USB YubiKey.
- **The KeeChallenge plugin format** used by KeePass 2 on Windows. See [KeePass Compatibility](/help/keepass-compatibility/).
- **KDBX 3.x files.** PanicVault is KDBX 4 only.
- **More than one YubiKey per vault.** A vault uses one key and one slot — but you can and should program a second, identical key as a backup.

## Setting Up Your YubiKey

PanicVault does not program YubiKeys; it only talks to a key that is already set up. Use Yubico's free **YubiKey Manager** on a Mac, Windows or Linux computer:

1. Open YubiKey Manager with your YubiKey plugged in
2. Go to the **OTP** application and choose a configuration slot — **Slot 1** or **Slot 2**
3. Choose **Challenge-response**, then **HMAC-SHA1**
4. Generate or enter the 20-byte secret. If the tool asks whether the input is a fixed 64-byte challenge or variable length, choose **variable length** — that is the usual choice and the one KeePassXC users make
5. Decide whether the key should require a physical touch. Either setting works with PanicVault; requiring a touch means nothing can use the key without you present
6. Write the configuration to the slot

**Which slot?** Slot 1 usually ships pre-programmed with Yubico OTP, so slot 2 is the one most people use — and slot 2 is KeePassXC's default. PanicVault also defaults to slot 2. Whichever you choose, remember it: you pick the slot on the lock screen.

{{< callout type="warning" >}}
If you lose your only YubiKey, the vault it protects is gone. There is no recovery, no reset and no backdoor — not even for us, and not even with the correct master password. Before you protect a vault with a YubiKey, program a **second YubiKey with the same HMAC-SHA1 secret** and keep it somewhere safe. YubiKey Manager can write the same 20-byte secret to two keys; save that secret somewhere safe while you do it, and treat it like the master key it is.
{{< /callout >}}

{{< callout type="note" >}}
Programming a slot overwrites whatever was in it. If slot 1 holds a Yubico OTP credential you still use, program slot 2 instead.
{{< /callout >}}

## Creating a Vault with a YubiKey

When you create a new vault, scroll to the **Hardware Key (Optional)** section:

1. Turn on **Protect with a YubiKey**
2. Choose **Slot 1** or **Slot 2** (slot 2 is the default)
3. PanicVault immediately sends a test challenge to your key, so you find out right away whether that slot really is set up for challenge-response. On iPhone, hold the key against the top of the phone; on Mac, plug it in. Touch the key if it asks
4. Read the warning about losing the key, and tick **I have a backup YubiKey, or I accept that losing this key destroys the vault**
5. Finish creating the vault as usual

From that point on, the vault needs your master password **and** your YubiKey. For the rest of the create-vault steps, see [Getting Started](/help/getting-started/).

## Unlocking with a YubiKey

On the lock screen, just below the key file row, there is a **YubiKey** row:

- If PanicVault does not know that this vault uses a YubiKey, the row shows **Optional** on the right. Turn it on if the vault needs a key.
- If PanicVault knows the vault uses one, the row shows **Required** in the accent color and is on already.
- When the row is on, it expands to show a **Slot 1 / Slot 2** picker. Pick the slot your key is programmed on.

### On iPhone (NFC)

1. Type your master password
2. Make sure the **YubiKey** row is on and the right slot is selected
3. Tap **Unlock**
4. iOS shows its own NFC panel asking you to hold the top of your iPhone against your YubiKey. Hold the key flat against the top of the phone
5. When the prompt says **Touch your YubiKey**, touch the gold disc — and **hold it there**. The key has to stay against the phone for the whole exchange. Tapping and pulling away is the most common cause of a failed unlock

### On Mac (USB)

1. Plug your YubiKey into a USB port
2. Type your master password, make sure the **YubiKey** row is on with the right slot, and click **Unlock**
3. PanicVault shows **Touch your YubiKey**; touch the gold disc

The very first time you use a YubiKey on a Mac, PanicVault shows an explanation and macOS then asks for the **Input Monitoring** permission. Your YubiKey talks to your Mac over the same USB channel a keyboard uses, so macOS asks for this permission before any app can read it. PanicVault only sends your vault's challenge to the key and reads its answer — it never watches what you type.

If you decline, PanicVault cannot read the key over USB and says so, with a button that opens the right settings pane. You can grant it later in **System Settings → Privacy & Security → Input Monitoring**, and you can revoke it there at any time. Your iPhone is unaffected — the same vault still unlocks over NFC.

{{< callout type="note" >}}
A .kdbx file records nothing about hardware keys, so the first time you open a KeePassXC hardware-key vault in PanicVault you have to turn the **YubiKey** row on yourself. After one successful unlock PanicVault remembers, and the row is switched on for you from then on. If an unlock keeps failing with "Incorrect password" on a vault you are sure of, that is the thing to check: if this vault uses a YubiKey, turn on **Hardware Key** below the password field.
{{< /callout >}}

## Adding or Removing a YubiKey on an Existing Vault

You can add a YubiKey to a vault that does not have one, move it to the other slot, or remove it — from the same screen where you change your master password:

1. Unlock the vault and tap the gear icon in the entry list toolbar to open **Database Settings**
2. In the **Master Password** section, tap **Change Master Password**
3. Use the hardware key row:
   - **Add a YubiKey** — pick the slot. PanicVault verifies the slot answers a test challenge before it commits anything
   - **Change slot** — move the vault to the other slot on the same key
   - **Remove the YubiKey** — the vault goes back to master password (plus key file, if it has one)
4. Confirm

PanicVault re-encrypts the whole vault once with the new combination and saves it. Adding or keeping a YubiKey costs exactly one touch during the change, because the answer has to be recomputed for the newly written file. Removing one costs no extra touch beyond the one that opened the vault. See [Vault Settings](/help/vault-settings/) for the rest of that screen.

{{< callout type="warning" >}}
Adding a YubiKey to a vault carries the same risk as creating one with a key: lose the key and the vault is unrecoverable. Have your backup key programmed first.
{{< /callout >}}

{{< callout type="important" >}}
After adding, changing or removing a hardware key, every other device needs the new combination the next time it unlocks the vault. If biometric unlock is enabled, the stored key is discarded and re-created on your next password unlock.
{{< /callout >}}

## Face ID / Touch ID and Hardware Keys

Face ID and Touch ID work on hardware-key vaults, exactly as they do on any other vault. There is a trade-off worth understanding, and PanicVault shows it to you once, the first time you enable biometric unlock on a vault that uses a YubiKey:

{{< callout type="important" >}}
**Face ID will unlock this vault without your YubiKey.** On this device, PanicVault keeps a key that opens this vault behind Face ID. Anyone who can pass Face ID here can open the vault without your YubiKey. Your YubiKey is still required on any other device, and any time Face ID fails.
{{< /callout >}}

In plain terms: enabling biometrics trades some of the YubiKey's protection for convenience **on that one device**. The key that biometrics unlocks is stored in the device Keychain, protected by the Secure Enclave, and is invalidated if the device's enrolled fingerprints or faces change. Every other device still needs the physical key, and so does this one whenever biometric authentication fails or your master password is required again.

If you would rather keep the YubiKey mandatory everywhere, leave biometric unlock off in [Security & Settings](/help/security-and-settings/).

## Syncing and Other Devices

A hardware-key vault syncs through [iCloud Drive](/help/icloud-drive-sync/) or [Google Drive](/help/google-drive-sync/) like any other vault. Only the .kdbx file syncs; nothing about your YubiKey does.

- **One touch per unlock, none per save.** PanicVault asks for the key once, when you unlock, and then does not ask again for the rest of the session — editing and saving entries costs no further touches. KeePassXC works differently: it asks for a touch on every save. The files stay fully interoperable either way.
- **AutoFill needs no key.** Once you have unlocked the vault in PanicVault, [AutoFill](/help/autofill/) on iPhone and Mac works on hardware-key vaults exactly as it does on any other vault. The AutoFill extension never opens the .kdbx file, so it never needs your YubiKey.
- **If the vault changed elsewhere**, for example because you saved it in KeePassXC on your desktop, PanicVault may need a fresh answer from your key before it can merge. It shows a banner rather than failing silently:

{{< callout type="note" >}}
**Sync paused — YubiKey needed.** This vault was changed on another device with different encryption settings. Touch your YubiKey to finish syncing.
{{< /callout >}}

Tap **Touch YubiKey** on the banner and the sync completes. PanicVault never asks for a touch on its own in the background — a touch is only ever requested for something you started.

## Troubleshooting

| Message | What to do |
|---|---|
| **No YubiKey found.** | iPhone: hold the key flat against the top of the phone and try again. Mac: plug it in and try again. |
| **This iPad can't read a YubiKey.** | Unlock this vault on an iPhone or a Mac. iPad has no supported way to reach the key. |
| **Slot N isn't set up for challenge-response.** | Either the vault uses the other slot — switch the picker — or the slot was never programmed. Configure it with YubiKey Manager. |
| **This YubiKey has its OTP application turned off for NFC.** | Re-enable the OTP application for NFC with YubiKey Manager, then try again. |
| **This YubiKey is new. Plug it into a computer once, then it will work over NFC.** | Recent YubiKeys ship with NFC restricted until the key has been powered over USB once. Plug it into any computer's USB port for a moment, then retry the NFC unlock. |
| **The YubiKey wasn't touched in time.** | Start again and touch the gold disc when prompted. On iPhone, keep the key against the phone while you touch it. |
| **Lost contact with the YubiKey.** | On iPhone this almost always means the key moved away from the phone mid-exchange. Hold it still against the top of the phone until the unlock finishes. |
| **PanicVault needs Input Monitoring to read your YubiKey over USB.** | Mac only. Turn it on in **System Settings → Privacy & Security → Input Monitoring**, or unlock this vault on your iPhone over NFC instead. |
| **Incorrect password** on a vault you are sure of | If the vault uses a YubiKey, turn on the **Hardware Key** row below the password field and try again. A .kdbx file does not say whether a hardware key is required. |
| Several YubiKeys plugged into a Mac at once | PanicVault asks which one to use. Or unplug the ones you are not using. |

{{< callout type="note" >}}
A failed touch, a missing key or a cancelled prompt is never counted as a wrong password attempt — fumbling with an NFC tap will not lock you out of your vault.
{{< /callout >}}
