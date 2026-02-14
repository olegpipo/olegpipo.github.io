---
title: "How to Set Up Emergency Access to Your Vault"
description: "Plan for the unexpected. Learn how to give a trusted person access to your password vault in an emergency without compromising daily security."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Guides & Tutorials"
---

What happens to your passwords if you are in an accident, become seriously ill, or die? It is an uncomfortable question, but ignoring it creates a real problem for the people who depend on you. Bills go unpaid, accounts become inaccessible, digital subscriptions keep charging, and important documents stored behind logins vanish. This guide, part of our [Password Manager Guides & Tutorials](/guides/) series, walks you through setting up emergency access so that a trusted person can reach your vault when it matters -- without compromising your security in normal times.

## Why Emergency Access Matters

Your password vault contains the keys to your digital life -- email, banking, insurance, medical portals, utility accounts, subscriptions, and more. If you are the only person who can access that vault, a medical emergency or death creates a cascade of practical problems for your family.

Consider what happens when no one can access your accounts:

- Monthly bills and subscriptions continue charging with no way to cancel
- Email accounts needed for password resets on other services are locked
- Insurance claims cannot be filed because portal access is lost
- Tax documents and financial records become inaccessible
- Digital photos, documents, and memories stored in cloud services are unreachable
- Social media accounts cannot be memorialized or deactivated

Emergency access planning eliminates these problems. It is a form of digital estate planning that takes about 30 minutes to set up.

## The Principles of Good Emergency Access

Whatever method you choose, good emergency access planning follows these principles:

1. **Separation of daily and emergency access**: Your trusted person should not have standing access to your vault. Emergency access should be dormant until needed.

2. **Verification before access**: There should be some mechanism -- even if informal -- that prevents misuse of emergency access during normal times.

3. **Completeness**: Emergency access should cover enough to handle essential accounts. It does not need to cover every login you own, but it must cover the ones that matter.

4. **Clear instructions**: Your trusted person needs to know not just the credentials but also what to do with them. A master password without instructions is like giving someone the keys to your house without telling them the address.

5. **Regular maintenance**: As your vault and master password change, your emergency access setup must be updated to match.

## Method 1: The Emergency Kit (Recommended for PanicVault and KeePass)

This is the most practical approach for users of local, [KeePass-compatible](/keepass/) password managers like PanicVault.

### What You Need

- A printed document containing your master password and instructions
- A sealed envelope or tamper-evident bag
- A secure physical location (home safe, safety deposit box, or trusted person's safe)

### Step-by-Step Setup

**1. Write the Emergency Document**

Create a document that includes:

```
EMERGENCY PASSWORD VAULT ACCESS

Last Updated: [Date]

Password Manager: PanicVault (or your manager's name)
Database Location: iCloud Drive > [folder path] or [device location]
Master Password: [your master password]
Key File Location: [if applicable -- see KeePass key files guide]

INSTRUCTIONS:
1. Install PanicVault from the App Store on an iPhone, iPad, or Mac
2. Open the database file from [location]
3. Enter the master password above
4. Priority accounts to access first:
   - Email: [entry name in vault]
   - Banking: [entry name in vault]
   - Insurance: [entry name in vault]
   - Utilities: [entry names in vault]

CONTACTS:
- Financial advisor: [name, phone]
- Attorney: [name, phone]
- Accountant: [name, phone]

This document provides access to all passwords, financial accounts,
and digital services. Handle with the same security as a will or
power of attorney.
```

**2. Print and Seal It**

Print the document (do not save it digitally in an unencrypted location). Place it in a sealed envelope. Write something like "Digital Estate -- Emergency Access" on the outside.

**3. Store It Securely**

Options for storage, from most to least secure:

- **Home safe or fireproof lockbox**: Accessible to family members who know the safe combination. Good balance of security and accessibility.
- **Safety deposit box**: Very secure but may be difficult to access quickly. Some banks restrict access after an account holder's death until probate.
- **Trusted person's safe**: A parent, sibling, attorney, or executor keeps the envelope. They must be someone you trust completely and who is likely to be available in an emergency.
- **Attorney or estate planner**: Can be included with your will and estate documents. Professional handling adds formality but may slow access.

**4. Tell Your Trusted Person**

The person who will need this access must know:

- That the emergency kit exists
- Where it is stored
- When they should use it (medical incapacitation, death -- define the circumstances)
- That they should not open it unless the triggering circumstances occur

### Maintaining the Emergency Kit

Update your emergency kit when:

- You change your master password
- You move your vault database to a different location
- You switch password managers
- You change the physical storage location of the kit
- Your life circumstances change (new trusted person, new emergency contacts)

Set a calendar reminder to review the kit every six months.

## Method 2: Split Knowledge

For additional security, you can split the emergency access credentials across two trusted people. Neither person alone can access your vault.

### How It Works

1. Give Person A the first half of your master password
2. Give Person B the second half
3. Both people know the vault location
4. In an emergency, Person A and Person B must cooperate to reconstruct the full master password

### Pros

- No single person can access your vault alone
- Reduces the risk of unauthorized access
- Works well when you trust two people independently but want an additional safeguard

### Cons

- Coordination is required in an emergency -- if one person is unreachable, access is blocked
- Both people must keep their portion secure
- More complex to set up and maintain

## Method 3: Cloud-Based Emergency Access Features

Some cloud-based password managers have built-in emergency access features.

### Bitwarden Emergency Access

1. Go to Settings > Emergency Access in the Bitwarden web vault
2. Add a trusted contact (they need a Bitwarden account)
3. Set a waiting period (e.g., 7 days)
4. If the trusted contact requests emergency access and you do not reject it within the waiting period, they gain access automatically

This is elegant because it does not require pre-sharing credentials. The waiting period prevents misuse -- if someone triggers emergency access without cause, you have days to cancel it.

### 1Password Emergency Kit

1Password provides an Emergency Kit during setup containing your Secret Key and space to write your master password. You print it, fill in your master password, and store it securely. This is essentially a formalized version of Method 1.

### Apple Legacy Contact

Apple allows you to designate a Legacy Contact who can request access to your Apple ID data (including iCloud Keychain passwords) after your death, with proof provided to Apple. This does not cover third-party password managers but can serve as a complementary layer.

## Method 4: Trusted Person With Read-Only Access

Some families maintain an arrangement where one person has ongoing, but limited, access to another's vault.

### In PanicVault

You can give a trusted person a copy of your database and master password with the understanding that they only access it in an emergency. This provides standing access rather than dormant emergency access, so it requires high trust.

A middle ground: keep a backup copy of your vault on a USB drive in your home safe. Update it monthly. Your emergency contact knows the safe combination and the master password. The backup may be slightly outdated, but it covers the essentials.

## What Should Your Emergency Contact Be Able to Do?

Not everything in your vault is equally important in an emergency. Prioritize access to:

### Tier 1: Immediate Priority

- **Primary email account**: Needed to reset passwords on other services
- **Banking accounts**: To manage finances, pay bills, prevent unauthorized charges
- **Insurance accounts**: Health, life, home, auto -- needed for claims
- **Phone carrier account**: To manage your phone plan

### Tier 2: Within Days

- **Utility accounts**: Electric, gas, water, internet
- **Subscription services**: To cancel recurring charges
- **Cloud storage**: iCloud, Google Drive, Dropbox -- where important documents live
- **Social media**: To deactivate or memorialize accounts

### Tier 3: Within Weeks

- **Shopping accounts**: Amazon, etc. -- to handle returns, cancel orders
- **Software licenses**: Transfer or cancel
- **Loyalty programs**: Some have monetary value that can be transferred
- **Other online accounts**: Clean up as needed

Include this prioritization in your emergency document so your contact knows where to start.

## Integrating With Your Estate Plan

Emergency access to your password vault should be part of your broader estate plan. Mention it in:

- **Your will**: Reference the existence of a digital estate document and its location
- **Power of attorney**: Ensure your designated agent has authority to access digital accounts
- **Letter of instruction**: An informal but detailed document that accompanies your will
- **Conversations**: Tell your executor and close family members that the digital estate plan exists

Many jurisdictions now have digital asset laws that govern access to online accounts after death. An estate attorney can help ensure your emergency access setup aligns with local law.

## Common Mistakes

**Not telling anyone the plan exists.** An emergency kit in a safe is useless if no one knows it is there.

**Storing the emergency document digitally in an unencrypted location.** A Google Doc with your master password defeats the purpose of encryption.

**Forgetting to update after changing your master password.** If your emergency kit has an old master password, it will not work when needed. Set update reminders.

**Making the emergency access too complex.** If your emergency contact needs to install three apps, find a key file on a specific USB drive, enter a 40-character password, and decode a hint to find the database location, they will likely fail under stress. Simplicity matters.

**Not considering incapacitation, only death.** You might be alive but unable to manage your accounts due to illness, injury, or travel. Your emergency access plan should cover temporary incapacitation as well.

**Assuming your spouse or partner knows your master password.** Unless you have explicitly shared it and they have practiced using it, do not assume. Verify.

## Testing Your Emergency Access Plan

Once a year, do a dry run:

1. Ask your trusted person to describe where the emergency kit is
2. Verify the master password in the kit still works
3. Confirm the database location described in the kit is accurate
4. Walk through the instructions to make sure they are clear
5. Update anything that has changed

This test takes 10 minutes and can prevent a crisis.

## Related Articles

- [How to Create a Secure Master Password You'll Remember](/guides/master-password/)
- [How to Back Up Your Password Vault](/guides/backup-vault/)
- [How to Share Passwords Securely With Family](/guides/share-with-family/)
- [How to Set Up a Password Manager for Your Parents](/guides/setup-for-parents/)
- [KeePass Key Files Explained](/keepass/key-files/)
