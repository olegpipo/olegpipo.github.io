---
title: "Platform Hardening on iOS and macOS"
description: "Data Protection classes, keychain accessibility, the app sandbox, snapshot protection, clipboard expiry, AutoFill extension isolation, and an honest account of what jailbreak detection can and cannot do."
date: 2026-07-14
lastmod: 2026-07-14
draft: false
silo: "Engineering & Security"
---

Encryption protects your vault when it is a file. Platform hardening protects it during the far more dangerous window when it is *open* -- when the key is in memory, entries are on screen, a password is on the clipboard, and the operating system is doing helpful things like taking screenshots of your app.

This is the layer where password managers actually leak. Not through the cipher. Through the surrounding platform behaviours that nobody thinks about until an attacker does. We work through them against the **OWASP Mobile Application Security Verification Standard (MASVS)**, using its testing companion the MASTG as the checklist -- alignment with a public standard, not a certification anybody has issued us.

## Data at Rest: Protection Classes and Keychain Accessibility

iOS encrypts every file on the device, but "encrypted" is not one thing. Each file is assigned a **Data Protection class** that determines *when* its key is available:

| Class | Key available |
|---|---|
| Complete | Only while the device is unlocked |
| Complete Unless Open | While unlocked; an already-open file stays readable |
| Complete Until First User Authentication | After the first unlock following a boot (the platform default) |
| None | Always, as soon as the device boots |

The default -- Complete Until First User Authentication -- is chosen so that background processes work after a reboot. It also means that on a device that has been unlocked once since booting, the file's key is present in memory, and a sufficiently capable forensic attacker with physical possession is in a better position than most people assume.

For a vault file, the stronger class is the right one, and the reasoning is a threat-model call rather than a reflex: the file is *already* encrypted with your master key, so protection class is defence in depth rather than the primary control -- but defence in depth is exactly what you want on the asset that is the entire product.

The **Keychain** has a parallel set of accessibility attributes, and this is where the decision genuinely matters, because the Keychain is where the key that biometric unlock releases actually lives:

- `WhenUnlocked` / `AfterFirstUnlock` -- and the `ThisDeviceOnly` variants of each.
- `WhenPasscodeSetThisDeviceOnly` -- the strictest: the item requires a passcode to exist at all, is destroyed if the passcode is removed, **never syncs to iCloud Keychain, and never appears in a device backup.**

That last property is the one that matters. A secret that syncs is a secret that has left the device. A secret in a backup is a secret in whatever protects the backup. For key material guarding a vault, the correct answer is *this device, this passcode, never leaving*, combined with an access control policy requiring biometric authentication -- the mechanism described in [cryptographic engineering](/engineering/cryptographic-engineering/) and, from the user's side, in [Face ID and Touch ID setup](/apple/face-id-touch-id-setup/).

## The Sandbox, and What It Does Not Do

Every iOS app runs in a container it cannot escape: it cannot read another app's files, cannot see another app's memory, cannot enumerate what else is installed. On macOS, the App Sandbox plus the Hardened Runtime provide the equivalent, with **entitlements** declaring exactly which capabilities the app may use -- and the entitlement list is signed, so the app cannot grant itself new ones at runtime.

PanicVault requests as few entitlements as it can, on the principle that a capability you do not have is a capability that cannot be abused by a compromised dependency, as argued in [supply chain security](/engineering/supply-chain-security/).

And now the honest caveat, because sandbox marketing routinely overstates this: **the sandbox is a boundary between processes, not within one.** A third-party library linked into our binary is inside the sandbox with us. It is us. The sandbox protects you from *other apps*; it does not protect you from code we linked. That is why the dependency count is the control and the sandbox is the backstop, not the other way round.

## The Screenshot Nobody Thinks About

When you swipe away from an app on iOS, the system captures a snapshot of its final frame to render the app switcher and to animate the return. That image is written to disk in the app's container.

Think about what that means for a password manager displaying an entry. Your credential -- rendered, legible -- persisting in a cache file. This has been a real, repeatedly rediscovered leak across the category.

The mitigation is to obscure the sensitive view *before* the snapshot is taken, when the app is notified that it is resigning active status, and to restore it on return. That timing is the entire trick: react at "will resign active", not at "did enter background", because by the latter the picture has already been taken. It is a two-line ordering detail with a catastrophic failure mode, and it is exactly the class of state-transition bug that our [adversarial AI reviewer](/engineering/ai-code-audit-fable-5/) is pointed at.

Related, and stated honestly: we can detect screen recording and react to it. We cannot prevent someone pointing a camera at your screen. No app can. Shoulder-surfing is a threat we mitigate with masked fields and a reveal action, not one we can eliminate.

## Clipboard Hygiene

The clipboard is the most under-respected leak in password management. When you copy a credential, it leaves your sandbox and enters a system-wide buffer. Historically, on iOS, any app in the foreground could silently read it. Universal Clipboard can push it over the air to your other devices. And it persists -- indefinitely -- until something replaces it.

PanicVault's rules:

- **Expiry is set at write time, not enforced by a timer we hope runs.** `UIPasteboard` accepts an expiration option, which hands the deletion responsibility to the operating system. A timer inside our process cannot fire if our process was terminated by the OS in the meantime -- a race that a naive implementation loses, silently, exactly when the device is under memory pressure. Setting the expiry as an option on the write means the clipboard is cleared even if we are killed a second later.
- **Local only.** Copied credentials are marked so they do not propagate to other devices via Universal Clipboard. Convenience that crosses a network boundary is a threat-model change nobody consented to.
- **AutoFill instead of copy, wherever possible.** The clipboard is a workaround. The [credential provider extension](/apple/credential-provider-extensions/) is the correct path, and it never touches the pasteboard at all.

Modern iOS also warns the user when an app reads the clipboard, and requires permission for cross-app pastes -- genuinely good platform changes. They mitigate the risk; they do not remove our obligation to expire what we wrote.

## Auto-Lock: The Control That Actually Gets Used

Every other control on this page is exotic compared to the one that will save the most vaults: **the app locks itself.**

Auto-lock is configurable, defaults to a short interval, and -- this is the part that matters -- **locking means the derived key is wiped from memory**, not that a view controller is pushed over the UI. A lock screen that hides the entries while the key sits in RAM is theatre. Real locking means:

- The key buffer is zeroed on lock, on backgrounding, and on error.
- Decrypted entries are dropped, not cached "for performance."
- The unlocked state is re-established only by a full authentication.

Lock triggers include the timer, backgrounding, device lock, and failed authentication attempts. The state machine that governs it is small, deliberately boring, and holds [100% branch coverage](/engineering/hundred-percent-test-coverage/) -- because the transitions are where the bugs live, and a transition that leaves a key alive is the single most valuable bug in the product to an attacker.

## AutoFill Extension Isolation

The credential provider extension is a **separate process** with its own memory, its own lifecycle, and -- crucially -- its own lock state. It does not inherit the main app's unlocked session. Unlocking the app does not silently arm AutoFill in the background; the extension authenticates on its own terms.

The extension and the app share an App Group container, so they can reach the same vault file. That shared container is a trust boundary and is treated as one: what crosses it is the encrypted vault, not the key.

The security-critical logic inside the extension is the *matching*: the system hands over a service identifier -- a domain, a bundle ID -- and the extension decides which credentials to offer. Get it wrong and you have built a phishing amplifier that helpfully offers your bank credentials to a lookalike domain. Correct, strict matching is not a UX feature; it is the mechanism by which a password manager is [structurally resistant to phishing](/phishing/password-manager-prevents-phishing/) in a way that a human eyeballing a URL never is. The same origin-binding principle underpins [passkeys](/passkeys/how-passkeys-work/), which take it further by making the private key cryptographically useless on the wrong origin.

## Jailbreak and Tamper Detection: The Honest Version

Here is where most security pages start writing cheques their threat model cannot cash.

PanicVault performs integrity and environment checks, and they are worth doing. But you deserve the accurate framing, which is this: **on a device whose operating system has been compromised, no application can defend itself.** If the attacker controls the kernel, they can read your memory, hook your functions, patch your checks, and disable your locks. Every jailbreak detection routine ever written can be defeated by the same tooling that produced the jailbreak, because the detector and the attacker are running on the attacker's machine.

So what are the checks for? They raise the cost. They defeat the casual, tooling-driven attacker running an off-the-shelf hooking framework. MASVS is explicit and unusually mature about this: its resilience requirements are about **increasing the effort required**, not about establishing a security boundary. They are speed bumps, and calling a speed bump a wall is how users end up over-trusting a compromised device.

The real mitigation is upstream and boring: keep the OS updated, do not jailbreak the device that holds your vault, and understand that a rooted phone is a phone where no password manager on earth -- ours included -- can keep a promise.

## No Telemetry, as an Attack Surface Decision

PanicVault contains no analytics SDK, no crash reporting SDK, no attribution framework, and no telemetry of any kind. This is usually presented as a privacy stance. It is also, and perhaps more importantly, a hardening decision:

- **No third-party SDK in the process.** Every analytics library is a foreign codebase running next to your master key, updating on someone else's release schedule.
- **No crash reports.** A crash reporter's job is to serialize process memory. In a password manager, process memory is the vault. There is no safe way to do this and we do not attempt one.
- **No egress.** With no telemetry pipeline, there is no legitimate network traffic for illegitimate traffic to hide inside. Any network activity would be anomalous by construction.
- **Nothing to subpoena, breach, or leak.** We do not hold data about you, because we do not collect any.

The tradeoff is real and we will name it: we do not get aggregate crash data, so we lean much harder on the [test suite](/engineering/hundred-percent-test-coverage/) and on [review](/engineering/static-analysis-sonarqube/) to find what telemetry would otherwise have surfaced. That is a deliberate trade -- more engineering cost for us, less attack surface for you.

## The Layer Below Everything

Platform hardening is what stands between a correctly encrypted vault and a user who is, at some point, going to open it -- on a train, on a shared desk, on a phone that will be backgrounded, backed up, and eventually sold.

None of it is exotic. All of it is the kind of detail that is easy to get subtly wrong in a single ordering-dependent line, and that no user could ever detect. Which is precisely why it sits under a [blocking quality gate](/engineering/static-analysis-sonarqube/), full branch coverage, and an [adversarial reviewer on every commit](/engineering/ai-code-audit-fable-5/).

Back to [Engineering and Security Assurance](/engineering/), or read the [secure development lifecycle](/engineering/secure-development-lifecycle/) that these controls fall out of.
