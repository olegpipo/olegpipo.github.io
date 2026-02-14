---
title: "How to Store Secure Notes, Credit Cards, and IDs"
description: "Use your password manager for more than passwords. Learn how to securely store credit cards, IDs, Wi-Fi passwords, software licenses, and sensitive notes."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

Your password manager is not just for website logins. It is an encrypted vault capable of storing any sensitive information you need to access regularly but do not want floating around in plain text -- credit card numbers, identity documents, Wi-Fi passwords, software licenses, insurance policy numbers, and private notes. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, shows you how to store each type of information effectively so you can find it when you need it.

## Why Store More Than Passwords

The same logic that makes a password manager essential for login credentials applies to other sensitive data:

- **Credit card numbers** written on sticky notes or stored in browser autofill are vulnerable to the same threats as reused passwords
- **Identity documents** (passport numbers, Social Security numbers, driver's license details) need to be accessible when traveling or filing paperwork but should not live in plain text on your phone
- **Software licenses** are easy to lose and expensive to re-purchase
- **Wi-Fi passwords** for your home, office, and friends' networks are perpetually lost and re-requested
- **Recovery codes** for [two-factor authentication](/two-factor-authentication/) are critically important and frequently misplaced

Your password manager is already encrypted, backed up, and accessible on all your devices. Putting these items in it costs nothing and provides the same protection your passwords receive.

## Credit Cards

### What to Store

For each credit card, create an entry with:

- **Title**: Card name and last four digits (e.g., "Chase Sapphire ****4521")
- **Cardholder name**: As printed on the card
- **Card number**: The full 16-digit number
- **Expiration date**: MM/YY
- **CVV/CVC**: The 3 or 4 digit security code
- **Billing address**: If different from your primary address
- **PIN**: If you have one set for the card (cash advances, international ATMs)
- **Customer service number**: The phone number on the back of the card

### In PanicVault

PanicVault uses the [KDBX format](/keepass/) which supports custom fields. You can create a structured entry:

1. Create a new entry in your "Banking & Finance" or "Credit Cards" group
2. Set the title to the card name and last four digits
3. Use the username field for the cardholder name
4. Use custom fields for card number, expiration, CVV, and other details
5. Or use the notes field with a structured format:

```
Card Number: 4111 2222 3333 4521
Expiration: 03/28
CVV: 742
PIN: 1234
Billing: 123 Main St, City, ST 12345
Customer Service: 1-800-xxx-xxxx
```

### When You Need Your Card Details

With your credit card stored in PanicVault, you can quickly reference your card number when:

- Shopping online on a new device where autofill does not have your card
- Providing card details over the phone
- Filling out paper forms (hotel check-in, rental car)
- Replacing a lost physical card -- you have the number to report and reference

### Security Note

Storing credit card numbers in your password manager is significantly more secure than:

- Saving them in browser autofill (no master password protection)
- Keeping photos of your cards on your phone (accessible to anyone who unlocks your phone)
- Writing them in a notes app (unencrypted)
- Memorizing only one card and using it everywhere (single point of failure)

## Identity Documents

### What to Store

Create entries for each important document:

**Passport**:
- Passport number
- Country of issue
- Issue date and expiration date
- Your full legal name as printed
- Place of birth
- Photo page scan (if your manager supports file attachments)

**Driver's License**:
- License number
- State/province of issue
- Issue and expiration dates
- Class/type
- Any restrictions or endorsements

**Social Security / National ID**:
- Number
- Issuing authority
- Any relevant notes about when you need to provide it

**Insurance Cards**:
- Policy number
- Group number
- Member ID
- Customer service number
- Pharmacy benefits details

### Organizing Identity Documents

Create a dedicated group or folder:

```
Personal Documents
├── Passport -- John Smith
├── Passport -- Jane Smith
├── Driver's License -- John
├── SSN -- John
├── Health Insurance -- Family
├── Auto Insurance -- Policy #12345
└── Home Insurance -- Policy #67890
```

### When You Need ID Details

Having these stored digitally saves time when:

- Filling out government forms online
- Making insurance claims by phone
- Checking in at a hotel or airport (backup to physical documents)
- Completing employment paperwork
- Filing taxes

**Important**: A digital record is not a substitute for the physical document. Authorities generally require original documents, not screenshots. But having the details accessible means you never need to hunt for the physical card to read a number off it.

## Wi-Fi Passwords

### Home and Frequently Used Networks

Create entries for:

- Your home Wi-Fi network (SSID and password)
- Your parents' or in-laws' Wi-Fi
- Your office Wi-Fi
- Any other network you connect to regularly

### Entry Format

```
Title: WiFi -- Home Network
Username: NetworkName_5G (the SSID)
Password: [the Wi-Fi password]
URL: [leave blank or use the router's admin URL, e.g., 192.168.1.1]
Notes:
- Router model: Eero Pro 6
- Admin login: admin / [admin password]
- 2.4GHz SSID: HomeNetwork
- 5GHz SSID: HomeNetwork_5G
- Guest network: HomeGuest / GuestPassword123
```

### Why This Matters

Every time a friend visits and asks for the Wi-Fi password, every time you connect a new device, every time you set up a smart home gadget -- you need the Wi-Fi password. Storing it in your password manager means you can pull it up instantly instead of crawling behind the router to read the sticker.

## Software Licenses

### What to Store

For each piece of software you have purchased:

```
Title: Software License -- Adobe Creative Cloud
Username: [your Adobe email]
Password: [your Adobe password]
Notes:
- License Key: XXXX-XXXX-XXXX-XXXX
- Purchase Date: 2024-06-15
- Purchase Source: Adobe.com
- Subscription Type: Annual
- Renewal Date: 2025-06-15
- Receipt: [reference to email or file]
```

### Organizing Software Entries

Decide whether software licenses should live:

- **As login entries** with license details in the notes (if the software has an online account)
- **As dedicated license entries** in a "Software Licenses" group (for offline software with serial numbers)
- **Combined**: The login to the vendor's site plus the license key in the same entry

### What to Include

- License keys and serial numbers
- Purchase date and source
- Download URLs
- Registration email used
- Subscription renewal dates
- Number of allowed installations

## Secure Notes

### When to Use Secure Notes

Use secure notes for sensitive information that does not fit the username/password format:

- Legal documents (attorney notes, case numbers)
- Medical information (allergies, medications, blood type, doctor contact info)
- Financial information (account numbers, routing numbers, tax ID)
- Emergency contacts and information
- Combination lock codes
- Alarm system codes and PIN codes
- Secret answers to security questions
- Recovery codes for 2FA
- Cryptocurrency seed phrases or wallet keys
- Safe combinations

### Structuring Secure Notes

A long, unstructured note is hard to scan. Use headings and formatting:

```
Title: Medical Information -- John

ALLERGIES:
- Penicillin (severe)
- Shellfish (mild)

MEDICATIONS:
- Lisinopril 10mg, daily
- Vitamin D 2000 IU, daily

BLOOD TYPE: O+

PRIMARY DOCTOR:
Dr. Sarah Chen
555-0123
123 Medical Center Dr

EMERGENCY CONTACTS:
1. Jane Smith (spouse) -- 555-0456
2. Robert Smith (brother) -- 555-0789

INSURANCE:
Blue Cross Blue Shield
Member ID: XYZ123456
Group: 78901
Phone: 1-800-xxx-xxxx
```

### Security Question Answers

Here is a pro tip: do not use real answers to security questions. If a site asks for your mother's maiden name, do not enter the real answer -- that information is often publicly available. Instead, generate a random word or phrase and store the fake answer in your vault:

```
Security Questions -- Bank of America
Q: Mother's maiden name → "turbine"
Q: Name of first pet → "oscilloscope"
Q: City where you were born → "chandelier"
```

This approach means security questions function like additional passwords rather than publicly researchable facts.

## Recovery Codes and Backup Keys

### 2FA Recovery Codes

When you enable [two-factor authentication](/guides/setup-2fa/) on an account, most services provide a set of one-time recovery codes. These codes let you access your account if you lose your 2FA device. They are critically important.

Store them in the same vault entry as the account's login:

```
Notes section of "Google -- Personal" entry:

2FA Recovery Codes (saved 2026-01-15):
1. abcd-efgh-ijkl
2. mnop-qrst-uvwx
3. 1234-5678-9012
4. ...
```

### Encryption Keys

If you use encryption tools (full-disk encryption, PGP, encrypted backups), store the recovery keys in your vault. Losing these keys means permanent data loss.

## Best Practices for Non-Password Storage

### Use Descriptive Titles

You will search for these entries by title. Make titles descriptive and consistent:

- `Credit Card -- Chase Sapphire ****4521` (not just "Chase Card")
- `WiFi -- Home Network` (not just "WiFi")
- `Insurance -- Auto -- State Farm` (not just "Insurance")

### Keep Related Items Together

If a service has both a login credential and additional stored data (like a credit card on file), put everything in one entry rather than creating separate entries. Use the notes field for supplementary information.

### Use Groups/Folders

See our [vault organization guide](/guides/organize-vault/) for detailed folder structure recommendations. The key groups for non-password items:

- Credit Cards
- Identity Documents
- Wi-Fi Networks
- Software Licenses
- Secure Notes
- Medical Information

### Review Periodically

Non-password items go stale:

- Credit cards expire
- Insurance policies change
- Software subscriptions lapse
- Addresses change
- Medications change

Add a quarterly calendar reminder to review these entries, or update them opportunistically when you encounter a change.

### Consider What Not to Store

Some information may be better stored elsewhere:

- **Large files** (scanned documents, photos): Your password manager is not a file storage system. Use iCloud Drive or another encrypted cloud storage, and reference the file location in your vault
- **Information others need immediately**: Emergency medical information should be accessible without unlocking your vault -- consider also keeping this on a physical card in your wallet or using Apple's Medical ID feature
- **Highly compartmentalized secrets**: If security requires that certain information never coexists with your passwords (e.g., a cryptocurrency seed phrase), consider a separate vault or a physical medium

## Related Articles

- [How to Organize Your Password Vault](/guides/organize-vault/)
- [How to Set Up 2FA Using Your Password Manager](/guides/setup-2fa/)
- [How to Back Up Your Password Vault](/guides/backup-vault/)
- [How to Set Up a Password Manager for the First Time](/guides/first-time-setup/)
- [Cloud Sync and Storage for Password Managers](/cloud-sync/)
