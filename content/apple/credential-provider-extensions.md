---
title: "How iOS Credential Provider Extensions Work"
description: "Technical deep dive into the iOS Credential Provider Extension API, ASCredentialProviderViewController, how third-party password managers integrate with iOS autofill, and practical setup guidance."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "Apple Ecosystem"
---

Third-party password managers on iPhone and iPad do not operate in isolation. They plug into iOS through a specific API called the Credential Provider Extension, which allows them to supply credentials -- passwords, passkeys, and verification codes -- directly into the system autofill flow. Understanding how this API works helps you appreciate why autofill behaves the way it does, what its limitations are, and how to get the best experience from your password manager within the [Apple ecosystem](/apple/).

This article covers the technical architecture of iOS Credential Provider Extensions, the central role of ASCredentialProviderViewController, how password managers like PanicVault use this framework, and the practical steps to configure and troubleshoot autofill on your devices.

## What Is a Credential Provider Extension?

An iOS app extension is a small, focused module that runs outside the main app process to provide functionality in specific system contexts. The Credential Provider Extension type (introduced in iOS 12) allows password managers to:

1. Appear in the iOS autofill suggestions when a credential field is detected.
2. Provide username/password pairs, passkeys, and one-time codes to apps and Safari.
3. Authenticate the user (via biometric, master password, or other means) before releasing credentials.

Without this API, third-party password managers would have no way to integrate with the iOS autofill system. Users would need to switch to the password manager app, find the entry, copy the password, switch back, and paste it -- a workflow that is functional but tedious enough that most people would default to Safari's built-in autofill or, worse, memorize weak passwords.

The Credential Provider Extension solves this by giving third-party managers the same first-class autofill experience that Apple's own Passwords system enjoys.

## The Role of ASCredentialProviderViewController

At the heart of every Credential Provider Extension is a subclass of `ASCredentialProviderViewController`, a UIKit view controller provided by Apple's AuthenticationServices framework. This class is the bridge between the iOS autofill system and your password manager's vault.

When iOS needs credentials, it instantiates the password manager's `ASCredentialProviderViewController` subclass in an extension process (sandboxed, separate from the main app). The view controller receives one of several callback methods depending on the context:

### prepareCredentialList(for:)

Called when the user taps on the autofill bar and multiple credential providers are available, or when the user explicitly requests to see all credentials. The password manager receives a list of `ASCredentialServiceIdentifier` objects describing the requesting service (typically the website domain or app bundle identifier).

The extension should:

1. Authenticate the user if the vault is locked (present a Face ID prompt, master password field, or other authentication UI).
2. Search the vault for entries matching the provided service identifiers.
3. Display matching credentials in a list for the user to select.
4. Call `extensionContext.completeRequest(withSelectedCredential:)` to deliver the chosen credential back to the autofill system.

### provideCredentialWithoutUserInteraction(for:)

This is the fast path. iOS calls this method first, hoping the extension can provide a credential silently -- without presenting any UI. This works when:

- The vault is already unlocked (the extension process has the decryption key in memory).
- There is exactly one matching credential for the requested service.
- No user interaction is required.

If the extension can provide the credential immediately, it calls `completeRequest(withSelectedCredential:)`. If it cannot (vault is locked, multiple matches exist, user confirmation is needed), it calls `extensionContext.cancelRequest(withError:)` with an `.userInteractionRequired` error code, and iOS falls back to calling `prepareCredentialList(for:)` to present interactive UI.

This two-phase design (try silently first, fall back to interactive) is why autofill sometimes fills instantly and other times shows a password manager screen. It is not inconsistent behavior -- it is the API working as designed.

### prepareInterfaceToProvideCredential(for:)

Called when iOS has determined that user interaction is required and is about to present the extension's UI. The extension uses this opportunity to prepare its interface -- loading the relevant credential, setting up the authentication prompt, or showing a search interface.

### prepareInterfaceForExtensionConfiguration()

Called when the user navigates to Settings > Passwords > AutoFill Passwords and taps on the password manager's configuration option. This allows the extension to present setup UI -- for example, selecting which vault to use, configuring quick-access categories, or performing initial authentication.

## The Extension Lifecycle

Understanding the lifecycle of a Credential Provider Extension explains several behaviors that users find confusing:

### Process Isolation

The extension runs in its own sandboxed process, separate from the main app. It has its own memory space, its own Keychain access, and its own lifecycle. This means:

- **The extension does not share memory with the main app.** If you unlock PanicVault in the main app, the extension does not automatically know the vault is unlocked. The extension must independently authenticate and decrypt the vault.
- **Shared data requires coordination.** The main app and extension communicate through shared containers (App Groups) and shared Keychain access groups. The vault file, cached credentials, and configuration are stored in a shared location that both processes can access.
- **The extension can be terminated independently.** iOS may kill the extension process at any time to reclaim memory. The next autofill request will launch a new extension process, which may need to re-authenticate.

### Authentication Flow

When the extension needs to authenticate the user, the typical flow is:

1. Extension checks for a valid session (is the vault already unlocked in this extension process?).
2. If no valid session, extension checks for a biometric-protected Keychain item (the master key stored during [Face ID / Touch ID setup](/apple/face-id-touch-id-setup/)).
3. If the Keychain item is available, the extension triggers a biometric prompt through the LocalAuthentication framework.
4. On successful biometric authentication, the Secure Enclave releases the stored master key.
5. The extension uses the master key to decrypt the vault (or the relevant portion of it).
6. Credentials are now available for the current autofill session.

If biometric authentication fails or is unavailable, the extension falls back to requesting the master password via its own UI.

### Credential Identifiers and Quick Type

To populate the autofill suggestions that appear above the keyboard (the QuickType bar), the extension must register its available credentials with iOS. This happens via the `ASCredentialIdentityStore`, a system-managed database that maps service identifiers (domains, apps) to credential identities (username + credential type).

Password managers populate this store when:

- The user first enables the extension.
- The vault contents change (new entry added, entry deleted, entry modified).
- The main app explicitly triggers a refresh.

The credential identities stored in `ASCredentialIdentityStore` contain only metadata -- the service identifier and username. They do not contain the actual password. The password is only retrieved when the user selects a suggestion and the extension's `provideCredentialWithoutUserInteraction(for:)` or `prepareCredentialList(for:)` is called.

This design means iOS can display autofill suggestions without the extension process running and without the vault being unlocked. The suggestions are essentially bookmarks that say "this password manager has a credential for this site." The actual credential is only accessed when selected.

## Passkey Support

Starting with iOS 17, the Credential Provider Extension API was expanded to support passkeys (WebAuthn/FIDO2 credentials). This is a significant addition because it allows third-party password managers to generate, store, and present passkeys -- not just traditional passwords.

The passkey flow involves additional methods:

- `prepareInterface(forPasskeyRegistration:)` -- Called during passkey creation.
- `provideCredentialWithoutUserInteraction(for:requestParameters:)` -- Extended to handle passkey assertion requests.

PanicVault supports passkey storage and autofill through this extended API, allowing you to keep all your authentication credentials -- passwords and passkeys alike -- in a single, portable vault.

This matters for the broader ecosystem because it means passkey adoption does not require you to lock into Apple's Passwords system or any single vendor. Your passkeys can live in an open-format vault managed by the password manager of your choice.

## How PanicVault Implements the Extension

PanicVault's Credential Provider Extension demonstrates how a KeePass-compatible app integrates with this API. The implementation addresses several practical challenges:

### Vault Decryption in the Extension

The .kdbx vault file must be decrypted within the extension process. Since KeePass encryption involves key derivation (Argon2d or AES-KDF), this requires non-trivial computation. PanicVault optimizes this by:

1. Caching the derived key in a Keychain item protected by biometric access control. This allows subsequent unlocks to skip the expensive key derivation step.
2. Using the Secure Enclave to protect the cached key, ensuring it cannot be extracted even if the device is jailbroken.
3. Implementing a configurable cache timeout so the derived key is periodically cleared, requiring full re-derivation.

### Matching Credentials to Services

When iOS provides a service identifier (e.g., `example.com`), PanicVault searches the vault for entries whose URL field matches. The matching logic handles:

- **Exact domain matches**: `https://example.com` matches the `example.com` identifier.
- **Subdomain matching**: `https://login.example.com` matches `example.com`.
- **Custom URL patterns**: Entries with specific URL paths can be matched to specific pages.
- **App identifiers**: When an iOS app (not a website) requests credentials, the service identifier is the app's bundle ID. PanicVault allows users to associate bundle IDs with vault entries.

### Handling Concurrent Access

The extension and the main app may access the vault file simultaneously. PanicVault uses file coordination (NSFileCoordinator) to prevent corruption:

- The extension acquires a read lock when filling credentials.
- The main app acquires a write lock when editing entries.
- iCloud Drive's file coordination integrates with this mechanism for synced vaults.

This is particularly important because a conflict between the extension process reading the vault and the main app writing to it could corrupt the database file.

## Setting Up a Credential Provider Extension

For users, enabling a third-party password manager's Credential Provider Extension is straightforward:

### On iPhone and iPad

1. Open **Settings**.
2. Navigate to **Passwords** > **AutoFill Passwords**.
3. Ensure **AutoFill Passwords** is toggled on.
4. Under **AutoFill From**, select your password manager (e.g., PanicVault).

On iOS 17 and later, you can enable multiple autofill providers simultaneously. iOS will present credentials from all enabled providers in the autofill suggestions. On earlier versions, only one provider can be active at a time.

### On Mac

1. Open **System Settings**.
2. Navigate to **Passwords** > **AutoFill**.
3. Select your password manager as an autofill source.

In Safari, the password manager's autofill suggestions will appear alongside (or instead of) Apple's Passwords suggestions. For Chrome and Firefox on Mac, you typically need the password manager's browser extension instead, as these browsers use their own extension systems rather than the system Credential Provider API. See our [guide to autofill across browsers on Mac](/apple/safari-chrome-firefox-mac/).

### Initial Credential Population

After enabling the extension, the password manager needs to populate the `ASCredentialIdentityStore` so iOS knows which credentials are available. Most apps do this automatically:

1. Open the password manager app.
2. Unlock the vault.
3. The app registers all credential identities with the system in the background.
4. Autofill suggestions will begin appearing within a few seconds.

If suggestions do not appear immediately, force-close and reopen the password manager app, or toggle the autofill provider off and on in Settings.

## Limitations of the Credential Provider Extension API

The API is powerful but not without constraints:

### Memory Limits

Extension processes have stricter memory limits than main app processes. For a very large vault (thousands of entries), the extension must be efficient about loading and searching credentials. Some apps load only the credential index into memory, fetching full entry details only when a specific credential is selected.

### No Background Execution

The extension is only active when iOS invokes it for an autofill operation. It cannot run in the background, perform scheduled syncs, or update the credential identity store without user interaction. This is why the main app is responsible for keeping the identity store current.

### Limited UI Customization

The extension's UI runs within a system-defined presentation context. While the extension can present custom view controllers (for vault unlock, credential selection, etc.), it cannot control the initial autofill bar appearance or the way suggestions are displayed in the QuickType bar. Apple dictates that presentation, and all password managers look similar in that context.

### Platform Differences

The Credential Provider Extension API behaves slightly differently on iPhone, iPad, and Mac. The most notable difference is that macOS supports the API in Safari and system password dialogs but not in all third-party browsers. Chrome and Firefox on macOS use their own extension frameworks, which requires password managers to maintain separate browser extensions for full coverage.

### No Direct Autofill in All Apps

Some iOS apps use custom text input views that do not support the standard autofill framework. In these cases, no password manager -- including Apple's own Passwords -- can offer autofill suggestions. The workaround is to switch to the password manager app, copy the credential, and paste it. This is rare but occasionally frustrating.

## Security Architecture of the Extension

Apple's design of the Credential Provider Extension prioritizes security:

- **Process isolation** ensures the extension cannot access the main app's memory or other apps' data.
- **Keychain access groups** limit which Keychain items the extension can read. Only items explicitly shared through App Groups are accessible.
- **Entitlement requirements** mean only apps that declare the `com.apple.developer.authentication-services.autofill-credential-provider` entitlement can create Credential Provider Extensions. Apple reviews these entitlements during App Store review.
- **User consent** is required -- the user must explicitly enable the extension in Settings before it can participate in autofill.

From a threat modeling perspective, the main risk is a malicious password manager app that captures credentials from the autofill flow. Apple mitigates this through App Store review, but the ultimate protection is choosing a reputable password manager with transparent security practices. Open-source apps with published audit results provide the highest level of assurance, consistent with the philosophy of [KeePass-compatible applications](/keepass/compatible-apps/).

## Troubleshooting

### Autofill Suggestions Not Appearing

1. Verify the extension is enabled in Settings > Passwords > AutoFill Passwords.
2. Open the password manager app and ensure the vault is unlocked.
3. Check that the entry's URL field matches the site you are visiting (domain must match).
4. Force-quit the password manager app and reopen it to trigger a credential identity store refresh.
5. If on iOS 16 or earlier, check that no other autofill provider is selected (only one allowed).

### Extension Shows Lock Screen Every Time

The extension process is being terminated between uses, losing its cached authentication state. This can happen if:

- The device is low on memory.
- The vault timeout is set too aggressively.
- The biometric-protected Keychain item has expired or been invalidated (for example, after a biometric enrollment change).

Try increasing the vault timeout for the extension, or ensure biometric unlock is properly configured in the password manager's settings.

### Autofill Works in Safari but Not in Apps

Some apps use custom text fields that do not trigger the autofill framework. Check if the app has a "Password" or "Login" AutoFill option in its text field menu (long-press the field). If not, the app developer has not adopted the standard text content types, and autofill will not work. Copy-paste from the vault is the only option.

### Credentials Appear for the Wrong Site

This usually means the URL stored in the vault entry is too broad (for example, storing `google.com` when you need separate credentials for `accounts.google.com` and `ads.google.com`). Edit the vault entry to use more specific URLs.

The Credential Provider Extension API represents Apple's commitment to making third-party password managers viable alternatives to its built-in system. The API is well-designed, secure by default, and increasingly capable with each iOS release. For users of [KeePass-compatible apps](/keepass/compatible-apps/), it means you can have the portability and transparency of an open-format vault with the autofill convenience of a native Apple feature -- no compromises required.
