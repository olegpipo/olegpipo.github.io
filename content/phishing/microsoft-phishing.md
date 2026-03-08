---
title: "Microsoft Phishing Examples (2026)"
description: "Real Microsoft 365 and Outlook phishing email examples from 2026. Learn to spot fake Microsoft security alerts, Teams invites, and OneDrive scams."
date: 2026-03-08
lastmod: 2026-03-08
draft: false
silo: "Phishing & Social Engineering"
faq:
  - q: "How do I know if a Microsoft email is real?"
    a: "Legitimate Microsoft emails come from @microsoft.com or @accountprotection.microsoft.com. Microsoft will never ask for your password via email. If unsure, sign in at account.microsoft.com directly to check your account status and security alerts."
  - q: "What does a Microsoft phishing email look like?"
    a: "Common Microsoft phishing emails claim your password is expiring, someone shared a OneDrive file, or there is a security alert on your account. They use Microsoft branding and link to fake login pages that mimic the Microsoft sign-in screen."
  - q: "Does Microsoft send emails about expiring passwords?"
    a: "Microsoft 365 administrators can configure password expiration policies, but Microsoft does not send emails asking you to click a link to reset your password. If your organization requires a password change, you will see a prompt when you sign in. Always go to account.microsoft.com directly."
  - q: "How do I report a phishing email pretending to be Microsoft?"
    a: "Forward the suspicious email to phish@office365.microsoft.com. In Outlook, you can also use the built-in 'Report Message' button to flag it as phishing. Do not click any links or open attachments."
  - q: "Can a password manager protect me from Microsoft phishing?"
    a: "Yes. A password manager like PanicVault checks the exact domain before autofilling credentials. If you land on a fake Microsoft page like 'microsoft-login.com' instead of 'login.microsoftonline.com,' the password manager will not autofill -- warning you that the site is fraudulent."
---

Microsoft is one of the most impersonated brands in phishing attacks, consistently ranking in the top three globally. With over 400 million paid Microsoft 365 subscribers and more than a billion users of Windows, Outlook, and Teams, attackers know that Microsoft credentials open doors to email, documents, corporate networks, and cloud storage. A compromised Microsoft account in a business environment can give attackers access to an entire organization's data. This article is part of our comprehensive [Phishing & Social Engineering guide](/phishing/) and examines the specific phishing patterns targeting Microsoft users in 2026.

Microsoft phishing is uniquely dangerous in corporate settings. Unlike consumer-targeted phishing that typically aims at individual accounts, a compromised Microsoft 365 account can be used to launch internal phishing campaigns against coworkers, access sensitive business documents on SharePoint and OneDrive, intercept financial communications, and perform [business email compromise](/phishing/business-email-compromise/) attacks that result in fraudulent wire transfers.

Below are the five most common Microsoft phishing email formats currently in circulation, along with practical steps for verifying messages and protecting yourself.

## Pattern 1: The Password Expiration Notice

This is the most common Microsoft phishing email and one of the most effective phishing templates across all brands. It works because many organizations do require periodic password changes, making the premise familiar and believable.

**Typical subject lines**:
- "Your Password Will Expire in 24 Hours"
- "Action Required: Microsoft 365 Password Expiry Notice"
- "IT Alert: Your Outlook Password Needs to Be Updated"
- "Your Microsoft Account Password Expires Today -- Change Now"

**What it looks like**: The email mimics a system notification from Microsoft 365 or an IT department. It states that your password is about to expire and that you must change it immediately to avoid losing access to Outlook, Teams, OneDrive, and other Microsoft services. A large "Change Password Now" or "Keep Current Password" button is prominently displayed. Some variants include a countdown showing hours remaining.

**The tell**: The sender address is not from @microsoft.com or @accountprotection.microsoft.com. Common fakes include noreply@microsoft365-security.com, admin@microsoftonline-alerts.net, or it-support@office365-admin.com. The "Keep Current Password" option is a particularly clever trick -- it does not exist in any real Microsoft password system, but many users click it hoping to avoid the hassle of a password change. Both buttons lead to the same [fake login page](/phishing/fake-login-pages/) that captures your credentials.

**The reality**: Microsoft 365 password expiration prompts appear when you sign in to your account, not through email links. If your organization requires a password change, you will see the prompt during login at login.microsoftonline.com. Microsoft itself has moved away from mandatory password expiration policies, recommending against them in its security guidance. If you receive an email about an expiring password, verify with your IT department directly.

## Pattern 2: The OneDrive or SharePoint Sharing Notification

This pattern exploits the legitimate and frequent practice of sharing files through OneDrive and SharePoint, making a fake sharing notification nearly indistinguishable from a real one.

**Typical subject lines**:
- "[Colleague Name] Shared a Document with You"
- "New Document Available: Q4 Financial Report.xlsx"
- "OneDrive: Someone Shared 'Invoice_March2026.pdf' with You"
- "SharePoint: You Have a New File to Review"

**What it looks like**: The email looks exactly like a genuine OneDrive or SharePoint sharing notification. It shows the name of a person (sometimes a real colleague if the attacker has done reconnaissance), a file name, and an "Open" or "View Document" button. The file name is often chosen to be relevant to the recipient's work -- financial reports, invoices, project plans, or HR documents.

**The tell**: The link does not go to onedrive.live.com, sharepoint.com, or your organization's SharePoint domain. Instead, it leads to a fake Microsoft sign-in page at a lookalike domain like onedrive-share.com, sharepoint-docs.net, or login.microsoftonline.com-verify.xyz. After entering your credentials on the fake page, you may be redirected to a real Microsoft page or shown a "document not found" error, masking the fact that your credentials have been stolen.

**The reality**: If someone genuinely shared a document with you through OneDrive or SharePoint, you can access it by logging into your Microsoft 365 account directly at office.com and checking your notifications or recent shared files. You do not need to click the link in the email. For an additional layer of verification, contact the sender directly to confirm they shared the file, especially if the share was unexpected.

## Pattern 3: The Teams Meeting Invitation

With Microsoft Teams used by over 320 million monthly active users, fake Teams notifications are increasingly common and effective, especially in hybrid work environments where meeting invitations arrive constantly.

**Typical subject lines**:
- "You Have a New Teams Meeting: Project Sync -- Tomorrow 2:00 PM"
- "Missed Teams Meeting: Q1 Review with Leadership"
- "[Manager Name] Invited You to a Teams Meeting"
- "Teams: You Have 3 Unread Messages from [Colleague Name]"

**What it looks like**: The email mimics a Microsoft Teams meeting invitation or chat notification. For meeting invitations, it shows a meeting title, time, organizer name, and a "Join Meeting" button. For chat notifications, it shows a preview of unread messages with a "Reply in Teams" button. The design closely mirrors genuine Teams notification emails.

**The tell**: The "Join Meeting" or "Reply in Teams" button links to a fake Microsoft sign-in page, not to teams.microsoft.com. The attacker captures your credentials when you "sign in" to join the meeting or read the messages. Some sophisticated versions actually redirect you to a real Teams meeting after harvesting your credentials, making the attack invisible. Check the URL before entering credentials -- genuine Teams meeting links come from teams.microsoft.com or your organization's domain.

**The reality**: You can access all your Teams meetings and messages by opening the Teams app directly or navigating to teams.microsoft.com. Any legitimate meeting invitation or unread message will be visible there. If you receive a meeting invitation from someone and want to verify it, contact them through a separate channel (phone, direct message in Teams, or in person).

## Pattern 4: The Security Alert

This pattern exploits Microsoft's genuine security notification system, which sends alerts about suspicious sign-in attempts and account activity changes.

**Typical subject lines**:
- "Microsoft Account Security Alert: Unusual Sign-In Activity"
- "Your Microsoft Account Was Signed In From a New Device"
- "Security Alert: Sign-In Attempt from [Country Name]"
- "Microsoft: Verify Your Recent Activity to Secure Your Account"

**What it looks like**: The email mimics Microsoft's legitimate security alert format, showing details of a sign-in from an unfamiliar device, location, or IP address. It typically shows a foreign country to maximize alarm. The email includes a "Review Recent Activity" or "This Wasn't Me" button, urging you to take immediate action to secure your account.

**The tell**: Microsoft does send genuine security alerts, which makes this pattern especially dangerous. The key differentiator is where the links point. Legitimate Microsoft security alerts link to account.live.com/activity or account.microsoft.com. Phishing versions link to lookalike domains. Always verify the URL before entering credentials. The safest approach is to ignore the email link entirely and navigate to account.microsoft.com directly to review your account activity.

**The reality**: If you are concerned about unauthorized access, go to account.microsoft.com, sign in, and select Security, then Review Recent Activity. You can see all sign-in attempts, change your password, and enable additional security measures from there. Do not use the links in the email, even if the email appears legitimate.

## Pattern 5: The Mailbox Full or Storage Warning

This pattern exploits the common frustration of running out of email or OneDrive storage, presenting a solution that requires clicking a link.

**Typical subject lines**:
- "Your Outlook Mailbox Is Almost Full (97%)"
- "Action Required: Your Microsoft 365 Storage Is Full"
- "Mailbox Quota Exceeded -- You Cannot Receive New Emails"
- "Free Up Space or Upgrade Your Microsoft 365 Storage"

**What it looks like**: The email warns that your Outlook mailbox or OneDrive storage has reached its limit and that you will be unable to send or receive emails until you take action. It offers options to "Free Up Space" or "Upgrade Storage" through a link. The design mimics Microsoft 365 admin notifications. Some variants claim to offer a free storage upgrade.

**The tell**: While Microsoft 365 does have storage limits and genuine notifications about approaching quotas, these appear within Outlook itself or through admin notifications within the Microsoft 365 portal. An email asking you to click a link to "upgrade storage" or "clear your mailbox" that redirects to a sign-in page outside of microsoft.com is phishing. The goal is credential theft.

**The reality**: If your mailbox is genuinely full, you will see a notification within Outlook. You can manage your storage by deleting old emails, emptying the Deleted Items folder, or contacting your IT department about quota increases. Storage upgrades for Microsoft 365 are managed through the admin portal or account.microsoft.com, not through email links.

## Smishing: Microsoft Text Message Scams

While less common than email-based Microsoft phishing, [SMS phishing](/phishing/smishing/) targeting Microsoft users has grown, particularly with the rise of multi-factor authentication that relies on phone-based verification codes.

**Common Microsoft smishing messages**:

- "Microsoft: Unusual sign-in detected on your account. Verify at [link]"
- "Microsoft 365: Your password will expire today. Update now: [link]"
- "Microsoft Security: Your account has been compromised. Secure it: [link]"
- "Your Microsoft verification code is 847291. If you did not request this, visit [link]"

The verification code variant is particularly dangerous. An attacker may be attempting to sign into your account in real time and needs the MFA code that Microsoft sends to your phone. The text includes a phishing link designed to trick you into entering the real code on a fake site.

**How to handle Microsoft smishing**:

1. Do not tap any links in the text.
2. Never share a verification code with anyone or enter it on a site you reached through a text link.
3. Open your Microsoft app or go to account.microsoft.com directly to check your account.
4. Forward the suspicious text to 7726 (SPAM) to report it to your carrier.
5. Report the message to Microsoft by forwarding it to phish@office365.microsoft.com.
6. Delete the message.

## How to Verify a Microsoft Email Is Legitimate

Before acting on any email that claims to be from Microsoft, apply this checklist:

1. **Check the sender address**: Legitimate Microsoft emails come from @microsoft.com, @accountprotection.microsoft.com, or @email.microsoft.com. Click on the sender name to see the full email address -- display names can be set to anything.

2. **Inspect links without clicking**: Hover over any buttons or links (on desktop) or long-press them (on mobile) to see the actual URL. Legitimate sign-in links go to login.microsoftonline.com, login.live.com, or account.microsoft.com. Any other domain is suspicious.

3. **Check for sensitive information requests**: Microsoft will never ask for your password, recovery codes, or full credit card number via email. Any message requesting this information is a scam.

4. **Verify with your IT department**: In a corporate environment, check with your IT team before acting on any email about password changes, account issues, or security alerts. Many IT departments send their own communications about Microsoft 365 changes.

5. **Check the Microsoft 365 portal**: Sign in at office.com or admin.microsoft.com to see any legitimate notifications, alerts, or required actions.

6. **Evaluate the urgency**: Legitimate Microsoft communications do not threaten account deletion within 24 hours or demand immediate action through an email link.

For a broader framework that applies to all phishing attempts, see our guide on [how to recognize phishing emails](/phishing/recognize-phishing/) and our [verification checklist for suspicious messages](/phishing/verify-suspicious-messages/).

## Why a Password Manager Is Your Strongest Defense

Understanding Microsoft phishing patterns is important, but awareness alone is not sufficient. Microsoft's own research shows that phishing attacks targeting Microsoft 365 credentials are the number one initial attack vector for data breaches. Modern [AI-powered phishing](/phishing/ai-powered-phishing/) generates emails with perfect grammar, accurate branding, and contextually relevant content that passes visual inspection. A [password manager](/password-managers/what-is-a-password-manager/) provides an automated technical defense that works even when your attention fails.

### Domain Matching Stops Credential Theft

When you use a password manager's autofill to sign into Microsoft 365, the password manager checks the exact domain of the page you are on. If the domain is login.microsoftonline.com or login.live.com, autofill works normally. If the domain is anything else -- microsoft-login.com, microsoftonline-verify.com, login.microsoftonline.com-secure.xyz -- autofill stays silent. The domain check is automated and precise, regardless of how perfect the fake sign-in page looks.

PanicVault performs this domain matching through Apple's system-wide AutoFill on iPhone, iPad, and Mac. When you tap a login field on a site claiming to be Microsoft and PanicVault does not offer your credentials, that silence is your warning that the site is not genuine. Learn more about this mechanism in our article on [how a password manager prevents phishing](/phishing/password-manager-prevents-phishing/).

### Unique Passwords Prevent Lateral Movement

In corporate environments, credential reuse is especially dangerous. If an employee uses the same password for their Microsoft 365 account and a personal account, a breach on the personal site gives attackers a path into the organization. A password manager generates and stores a unique, random password for every account, preventing credential stuffing attacks that move laterally from compromised personal accounts to corporate systems.

### Navigate From Your Vault, Not From Email Links

When you receive a notification about your Microsoft account, instead of clicking the link in the email, open PanicVault and tap your Microsoft entry. It will take you to the real login.microsoftonline.com and autofill your credentials. This simple habit eliminates the risk of landing on a phishing page.

## How to Report Microsoft Phishing

If you receive a phishing email or text pretending to be Microsoft, report it to help protect others:

1. **In Outlook**: Use the built-in "Report Message" or "Report Phishing" button on the ribbon. This is the most effective reporting method for Microsoft 365 users.
2. **Forward the email** to phish@office365.microsoft.com.
3. **Report to your IT department** if you are in a corporate environment -- they need to know about phishing campaigns targeting the organization.
4. **Report to the FTC** at ReportFraud.ftc.gov.
5. **Report to the Anti-Phishing Working Group** at reportphishing@apwg.org.

For a complete guide on reporting phishing across all brands and platforms, see our article on [how to report a phishing attempt](/phishing/report-phishing/).

## What to Do If You Fell for a Microsoft Phishing Scam

If you entered your Microsoft credentials on a phishing site, act immediately:

1. **Go to account.microsoft.com directly** and change your password immediately.
2. **Enable multi-factor authentication** if it is not already active. Go to Security, then Advanced Security Options, then Two-step Verification.
3. **Review recent sign-in activity**: At account.microsoft.com, select Security, then Review Recent Activity, to see all sign-in attempts and revoke any you do not recognize.
4. **Notify your IT department** if this is a corporate Microsoft 365 account. They need to assess whether the attacker accessed sensitive data, sent emails from your account, or created inbox forwarding rules.
5. **Check email forwarding rules**: Attackers often set up forwarding rules to copy all incoming email to an external address. In Outlook, go to Settings, then Mail, then Forwarding, and remove any rules you did not create.
6. **Review connected apps**: Check for unauthorized apps with access to your Microsoft account at account.microsoft.com under Apps & Services.
7. **Forward the phishing email** to phish@office365.microsoft.com.
8. **Report it** to the FTC at ReportFraud.ftc.gov and to the Anti-Phishing Working Group at reportphishing@apwg.org. See our full guide on [how to report a phishing attempt](/phishing/report-phishing/).

## Staying Ahead of Microsoft Phishing in 2026

Microsoft phishing is evolving rapidly. Attackers now use adversary-in-the-middle (AitM) techniques that intercept and relay authentication tokens in real time, bypassing even multi-factor authentication. Phishing kits targeting Microsoft 365 are widely available on dark web marketplaces, lowering the barrier to entry for attackers. AI-generated emails referencing real projects, colleagues, and organizational context make detection through visual inspection nearly impossible.

What works is a layered defense:

- **Use a password manager** that checks domains automatically and refuses to autofill on fake sites.
- **Enable multi-factor authentication** on every Microsoft account, preferably using authenticator apps or hardware security keys rather than SMS codes.
- **Never click links** in emails claiming to be from Microsoft or your IT department. Navigate to the relevant portal directly.
- **Verify meeting invitations and file shares** through the Teams or OneDrive app before clicking email links.
- **Report every phishing attempt** using the "Report Message" button in Outlook and by forwarding to phish@office365.microsoft.com.
- **Train your team**: In corporate environments, [help colleagues and family members recognize phishing](/phishing/train-family/) to strengthen the collective defense.

The attackers are counting on the rushed moment when you see "Your password expires in 2 hours" and click without thinking. The best countermeasure is building habits that remove urgency from the equation: let your password manager handle domain verification, go directly to the source for every notification, and treat every unsolicited message about your Microsoft account with healthy skepticism.

## Related Articles

- [How to Recognize a Phishing Email: 10 Red Flags](/phishing/recognize-phishing/)
- [Business Email Compromise: What It Is and How to Prevent It](/phishing/business-email-compromise/)
- [Fake Login Pages: How Phishing Sites Steal Credentials](/phishing/fake-login-pages/)
- [How a Password Manager Protects From Phishing](/phishing/password-manager-prevents-phishing/)
- [How to Report a Phishing Attempt](/phishing/report-phishing/)
