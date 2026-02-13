---
title: "How to Import Chrome, Safari, and Firefox Passwords into KeePass"
description: "Export saved passwords from Chrome, Safari, and Firefox and import them into KeePass. Step-by-step instructions for each browser with tips for cleanup."
date: 2026-02-13
lastmod: 2026-02-13
draft: false
silo: "KeePass & Open Standards"
---

Most people accumulate saved passwords in their web browsers over years of daily use. Chrome, Safari, and Firefox all offer built-in password managers that save credentials automatically when you log into websites. While convenient, browser password storage has significant limitations compared to a dedicated password manager. Migrating those saved passwords into a [KeePass-compatible application](/keepass/) consolidates your credentials into a single encrypted vault, gives you stronger security controls, and eliminates the fragmentation of having passwords scattered across multiple browsers and devices.

This guide covers the export process for each major browser, the import into KeePass, and the cleanup steps that turn a raw import into a well-organized vault.

## Why Move Passwords Out of Your Browser

Before walking through the technical steps, it is worth understanding why browser-based password storage is insufficient as a long-term solution. For a detailed comparison, see our analysis of [password managers versus browser saving](/password-managers/vs-browser-saving/).

### Limited Security Model

Browser password managers are designed primarily for convenience, not security. The encryption protecting your saved passwords is typically tied to your operating system login. If someone gains access to your computer while you are logged in -- or if your OS account is compromised -- your browser passwords are exposed. There is no separate master password protecting the credential store in most default configurations.

Chrome, for example, encrypts saved passwords using the operating system's credential storage (Windows DPAPI or macOS Keychain), which means anyone with access to your logged-in user session can view all saved passwords through the browser settings. Safari integrates with macOS Keychain, which provides stronger isolation but still ties credential access to your system login. Firefox offers an optional primary password feature, but it is not enabled by default and many users never activate it.

### No Cross-Browser Access

If you use Chrome on your laptop and Safari on your phone, your saved passwords are split between two separate systems with no easy way to share between them. KeePass provides a single vault file that works with compatible applications on every platform, so your credentials are available regardless of which browser or device you are using.

### Weak Audit Capabilities

Browsers offer limited tools for assessing the health of your saved passwords. While Chrome and Safari have introduced some breach-checking features, they lack the comprehensive auditing capabilities of dedicated password managers -- such as identifying weak passwords, flagging reuse across accounts, and measuring password entropy.

### No Structured Organization

Browser password stores present your credentials as a flat list, typically sorted by website. There is no folder structure, no tagging, and limited search functionality. After years of accumulation, this list can contain hundreds of entries with no way to organize or categorize them. KeePass supports hierarchical groups, custom fields, and detailed entry metadata that make managing a large credential set practical.

## Exporting Passwords from Chrome

Chrome stores passwords in its built-in password manager, which syncs across devices if you are signed into a Google account. The export produces a CSV file containing all saved credentials.

### Export Steps

1. Open Chrome and navigate to `chrome://password-manager/settings` or click the three-dot menu, select **Settings**, then **Autofill and passwords**, then **Google Password Manager**.
2. Click **Settings** within the password manager interface.
3. Look for the **Export passwords** option and click it.
4. Chrome will ask you to authenticate using your operating system password, fingerprint, or other system-level authentication. This is a security measure to prevent unauthorized exports.
5. Choose a location to save the CSV file. Save it to your local drive, not a cloud-synced folder.

### What the Chrome Export Includes

The Chrome CSV export contains four columns:

- **name** -- The friendly name or display name for the entry
- **url** -- The website URL where the credential was saved
- **username** -- The login username or email address
- **password** -- The password in plain text

Chrome does not export notes, custom fields, or any metadata beyond these four fields. If you stored additional information in Chrome's notes feature (added in recent versions), that data may not be included in the CSV export.

### Chrome on Mobile

Chrome's mobile apps (Android and iOS) do not offer a direct CSV export. To export passwords saved in Chrome on mobile:

- If your Chrome passwords are synced to your Google account, sign in to Chrome on a desktop computer and export from there. All synced passwords will be available.
- Alternatively, visit passwords.google.com in any browser, sign in with your Google account, and use the export option available in the settings.

## Exporting Passwords from Safari

Safari integrates with macOS Keychain for password storage. The export process is handled through the System Settings on macOS (or Safari preferences on older versions).

### Export Steps on macOS Ventura and Later

1. Open **System Settings** on your Mac.
2. Navigate to **Passwords** in the sidebar.
3. Authenticate with your Mac password, Touch ID, or Apple Watch.
4. Click the three-dot menu (or the **...** button) at the bottom of the passwords list.
5. Select **Export All Passwords**.
6. Confirm that you want to export. macOS will warn you that passwords will be saved in an unencrypted format.
7. Choose a save location and save the CSV file.

### Export Steps on Older macOS Versions

1. Open **Safari** and go to **Safari** in the menu bar, then **Preferences** (or **Settings**).
2. Click the **Passwords** tab.
3. Authenticate with your Mac password.
4. Look for an export option in the interface. On some versions, you may need to right-click or use a menu button to find the export function.
5. Save the CSV file.

### What the Safari Export Includes

The Safari/Keychain CSV export typically contains:

- **Title** -- A display name, usually derived from the website name
- **URL** -- The website address
- **Username** -- The login username
- **Password** -- The password in plain text
- **Notes** -- Any notes associated with the entry (if supported by your macOS version)
- **OTPAuth** -- TOTP secrets, if you stored two-factor authentication codes in Safari

### Safari on iOS and iPadOS

iOS does not offer a direct CSV export from Safari. To export passwords from an iPhone or iPad:

- Ensure your iCloud Keychain is synced to a Mac. Open System Settings on the Mac and export from there.
- If you do not have a Mac, third-party tools exist that can extract passwords from iOS backups, but this approach is more complex and requires caution about which tools you trust with your credentials.

## Exporting Passwords from Firefox

Firefox stores passwords in its built-in Lockwise password manager. The export process is available through the browser settings.

### Export Steps

1. Open Firefox and navigate to `about:logins` or click the hamburger menu (three horizontal lines), then **Passwords**.
2. Click the three-dot menu in the top-right corner of the password manager interface.
3. Select **Export Logins**.
4. Firefox will display a warning that passwords will be saved in an unencrypted file. Confirm that you want to proceed.
5. Authenticate with your operating system credentials if prompted.
6. Save the CSV file to your local drive.

### What the Firefox Export Includes

The Firefox CSV export contains:

- **url** -- The website URL
- **username** -- The login username
- **password** -- The password in plain text
- **httpRealm** -- HTTP authentication realm (relevant for HTTP basic auth, usually empty for standard web logins)
- **formActionOrigin** -- The URL where the login form submits
- **guid** -- A unique identifier for the entry
- **timeCreated** -- When the credential was first saved
- **timeLastUsed** -- When the credential was last used
- **timePasswordChanged** -- When the password was last updated

Firefox exports more metadata than Chrome or Safari, which can be useful for identifying old or unused credentials during cleanup.

### Firefox Primary Password

If you have set a primary password in Firefox (formerly called a master password), you will need to enter it before exporting. If you have not set one, Firefox will use your operating system credentials for authentication.

## Importing into KeePass

With your CSV files exported from one or more browsers, the next step is importing them into your KeePass database.

### Importing into KeePassXC

1. Open KeePassXC. Create a new database if you do not have one, or open your existing database.
2. Go to **Database** then **Import** then **CSV File**.
3. Select the CSV file from one of your browser exports.
4. KeePassXC will show a preview of the data and a column mapping interface. Map the columns to KeePass fields:
   - URL column to **URL**
   - Username column to **User Name**
   - Password column to **Password**
   - Title/Name column to **Title**
   - Notes column to **Notes** (if present)
5. Check the box to treat the first row as field names.
6. Optionally, specify a group (folder) to import into. Creating a group named after the source browser (e.g., "Chrome Import" or "Firefox Import") helps with later organization.
7. Click **OK** to import.

Repeat this process for each browser CSV file, importing each into a separate group.

### Importing into KeePass 2.x

1. Open KeePass 2.x and open or create your database.
2. Go to **File** then **Import**.
3. Select **Generic CSV Importer**.
4. Browse to your CSV file.
5. Configure the column mapping, matching each column to the corresponding KeePass field.
6. Complete the import.

### Handling Multiple Browser Imports

If you exported from more than one browser, you will likely have duplicate entries -- the same website and username appearing in multiple CSV files because you used the same credentials in different browsers. This is expected and will be addressed in the deduplication step.

## Deduplication: Cleaning Up Duplicate Entries

After importing from multiple browsers, your KeePass database will almost certainly contain duplicates. The same login saved in Chrome and Firefox will appear as two separate entries. Cleaning these up is essential for a usable vault.

### Manual Deduplication

1. Sort your entries by URL or title to group similar entries together.
2. For each set of duplicates, compare the credentials. If they are identical, delete the extras and keep one.
3. If the duplicates have different passwords (because you changed your password in one browser but not the other), keep the entry with the most recent password. Firefox's exported metadata (timePasswordChanged) can help you determine which is current.

### Using KeePass Tools

KeePass 2.x has plugins that can assist with duplicate detection. The "KPSimpleBackup" and "KeePassDuplicateEntryDialog" plugins can identify entries with matching URLs or usernames. KeePassXC includes a merge function that can help when combining databases, though it does not have a dedicated deduplication feature.

### A Practical Approach

For most users, perfect deduplication is less important than having all credentials in one place. Start by eliminating obvious duplicates -- entries where the title, URL, and username are identical. You can refine your vault over the following weeks as you encounter entries during daily use. Each time you log into a site and KeePass shows multiple matching entries, take a moment to delete the duplicates and keep the correct one.

## Organizing Imported Entries

Browser exports produce a flat list of entries with no organizational structure. Investing time in organizing your vault pays dividends in daily usability.

### Create a Group Structure

Set up a group hierarchy that matches how you think about your online accounts:

- **Email** -- Gmail, Outlook, Yahoo, and other email providers
- **Financial** -- Banks, credit unions, investment accounts, payment services
- **Social Media** -- Facebook, Instagram, LinkedIn, Twitter, Reddit
- **Shopping** -- Amazon, eBay, and online retailers
- **Entertainment** -- Streaming services, gaming platforms, media subscriptions
- **Work** -- Professional tools, employer portals, VPN access
- **Utilities** -- Internet provider, phone carrier, utility companies
- **Government** -- Tax portals, government services, voting registration
- **Health** -- Healthcare portals, insurance, pharmacy accounts
- **Other** -- Everything that does not fit neatly into a category

### Move Entries into Groups

Sort through your imported entries and drag them into the appropriate groups. This is the most time-consuming part of the process, but you do not need to complete it in one sitting. Start with the accounts you access most frequently, then organize the rest over time.

### Clean Up Entry Titles

Browser-saved entries often have unhelpful titles -- a URL fragment, a domain name, or a generic label like "Login." Rename entries to be descriptive and consistent. For example, rename "accounts.google.com" to "Google Account" or "chase.com" to "Chase Banking." Consistent naming makes searching your vault much faster.

### Add Missing Information

Browser exports capture the minimum: URL, username, and password. For entries where you want more detail, add:

- **Notes** about the account (account number, security questions, support contact information)
- **Custom fields** for data like PINs, membership numbers, or recovery codes
- **Tags or attributes** to help with future searching and filtering

## Disabling Browser Password Saving

After migrating your passwords into KeePass, disable the built-in password saving in each browser to prevent credential sprawl going forward. You want all new passwords to be generated and stored in KeePass, not saved back into the browser.

### Disabling in Chrome

1. Open Chrome and navigate to `chrome://password-manager/settings`.
2. Toggle off **Offer to save passwords**.
3. Optionally, toggle off **Auto Sign-in** to prevent Chrome from automatically logging you into sites using saved credentials.

### Disabling in Safari

1. Open **Safari** then **Settings** (or **Preferences**).
2. Go to the **AutoFill** tab.
3. Uncheck **User names and passwords**.
4. In **System Settings** then **Passwords** then **Password Options**, turn off **AutoFill Passwords and Passkeys**.

### Disabling in Firefox

1. Open Firefox and navigate to `about:preferences#privacy`.
2. Scroll to the **Logins and Passwords** section.
3. Uncheck **Ask to save passwords**.
4. Uncheck **Autofill logins and passwords** if present.

### Why This Matters

If you leave browser password saving enabled, you will end up with a split system: some passwords in KeePass and new ones accumulating in the browser. Over time, this defeats the purpose of consolidation. Disabling browser saving forces all credential management through KeePass, which is where your autofill and audit capabilities live.

For guidance on setting up autofill through KeePass instead, see our [KeePass-compatible apps guide](/keepass/compatible-apps/), which covers browser extensions and mobile autofill integration.

## Verifying the Import

Before you delete the exported CSV files and move on, verify that the import was successful.

### Test High-Priority Accounts

Log in to your most important accounts using credentials from KeePass:

- Primary email (Gmail, Outlook, iCloud)
- Banking and financial services
- Cloud storage (Google Drive, Dropbox, iCloud)
- Social media accounts you use daily

Each successful login confirms that the password transferred correctly.

### Check for Missing Entries

Compare the number of entries in your KeePass database against the total count of saved passwords reported by each browser before export. If entries are missing, common causes include:

- Passwords saved only on a mobile device that did not sync to the desktop browser
- Entries with special characters that caused CSV parsing errors
- Credentials stored in a different browser profile that you did not export

### Back Up Your Database

With the import complete and verified, create an immediate backup of your KeePass database. Store the backup in a location separate from the primary database file. For a comprehensive backup strategy, see our [KeePass database backup guide](/keepass/backup-database/).

## Post-Migration Cleanup

### Delete the CSV Export Files

The plain text CSV files containing your passwords should be deleted as soon as you have confirmed the import. These files represent a significant security risk if left on your drive, in your downloads folder, or in your trash.

### Clear Browser Password Stores (Optional)

Once you are confident that all passwords have been successfully imported into KeePass, you may want to delete the saved passwords from your browsers. This eliminates the risk of stale credentials lingering in browser storage and prevents confusion about which system is authoritative.

In Chrome, go to `chrome://password-manager` and delete individual entries or clear all saved passwords. In Firefox, go to `about:logins` and remove entries. In Safari, use System Settings then Passwords to delete entries from Keychain.

Be cautious with this step. Only clear browser passwords after you are fully confident in your KeePass import. Keeping the browser passwords for a week or two as a fallback is a reasonable precaution.

### Start Using KeePass for New Accounts

Going forward, use KeePass to generate and store passwords for every new account. Install the browser extension for your KeePass application (KeePassXC Browser for KeePassXC, for example) and configure it for autofill. The goal is to establish KeePass as your single source of truth for all credentials.

For users who are also migrating from a commercial password manager like LastPass, our [LastPass to KeePass migration guide](/keepass/migrate-from-lastpass/) covers that process in detail. And if you are new to password managers entirely, our [beginner's guide to password managers](/password-managers/beginners-guide/) provides the foundational concepts.

## Conclusion

Importing browser passwords into KeePass is one of the most practical first steps toward better password management. Browsers accumulate credentials passively over years, storing them with minimal security and no organizational structure. Moving those credentials into an encrypted KeePass vault gives you a centralized, secure, and organized system that you control.

The process is straightforward: export from each browser as CSV, import into KeePass, deduplicate, organize, and disable browser saving. The initial cleanup takes effort, but the result is a vault that serves as the single authoritative source for all your credentials -- searchable, auditable, and protected by encryption that does not depend on your operating system login.

Your passwords are too important to leave scattered across browser databases with inconsistent security. Consolidating them in KeePass is a concrete improvement you can make in an afternoon, with benefits that compound every day you use it.
