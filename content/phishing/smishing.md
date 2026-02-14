---
title: "What Is Smishing? How to Spot SMS Phishing"
description: "Everything you need to know about smishing (SMS phishing) -- how text message scams work, the most common tactics, and how to protect yourself."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Phishing & Social Engineering"
---

Smishing -- a portmanteau of "SMS" and "phishing" -- is phishing delivered through text messages. If you have a mobile phone, you have almost certainly received a smishing attempt. A text about a package delivery. An alert about your bank account. A toll payment you supposedly missed. These messages are designed to trick you into tapping a link, calling a phone number, or providing personal information. This article is part of our [Phishing & Social Engineering](/phishing/) guide.

## Why Smishing Works

Smishing exploits several unique properties of text messages that make them more dangerous than email phishing:

### Higher Trust

People trust text messages more than emails. Decades of email spam have trained most people to be at least somewhat skeptical of emails from unknown senders. But text messages feel more personal, more direct. A text that says "Your bank account has been locked" creates more alarm than the same message in an email, because texts are associated with immediate, personal communication.

### Limited Context

Mobile screens provide limited space for inspecting messages. URLs are often truncated or hidden. Sender identification is minimal -- a text from a short code or unfamiliar number does not immediately register as suspicious the way a misspelled email domain might. There is no "hover over to see the real URL" on a phone screen (though you can long-press a link to preview it).

### Urgency Compounds

People check text messages faster than email. The notification appears on your lock screen. You read it immediately. The urgency embedded in smishing messages -- "act now," "verify today," "your account will be closed" -- compounds with the inherent urgency of the text message medium. There is less time for reflection between reading and acting.

### Harder to Filter

Email providers have had decades to develop sophisticated spam and phishing filters. SMS filtering is less mature. Many smishing messages reach their targets without any warning or filtering, especially when sent from legitimate-seeming phone numbers or short codes.

## Common Smishing Scenarios

### Package Delivery Scams

"Your package could not be delivered. Click here to reschedule." This is the most common smishing template because it is universally relevant -- most people are expecting some kind of delivery at any given time. The link leads to a [fake login page](/phishing/fake-login-pages/) that harvests credentials or requests a small "redelivery fee" to capture credit card information.

**How to verify**: Open the official app or website of the carrier (USPS, UPS, FedEx, DHL) and enter any tracking numbers you have. If you are not expecting a delivery, ignore the text.

### Banking and Financial Alerts

"Unusual activity detected on your account. Verify your identity." "Your debit card has been locked due to suspicious transactions." These texts impersonate your bank to create panic. The link leads to a credential-harvesting site designed to look like your bank's login page.

**How to verify**: Open your banking app directly or call the number on the back of your card. Do not use any link or phone number from the text.

### Government Impersonation

"Your tax refund of $1,247.00 is ready. Click to claim." "You have an outstanding toll balance. Pay now to avoid penalties." Government agencies -- the IRS, the Social Security Administration, the DMV -- communicate important matters through official mail and secure portals, not text messages.

**How to verify**: Log into the government agency's official website directly. The IRS uses IRS.gov. The Social Security Administration uses SSA.gov. If you truly owe money or are owed a refund, it will be reflected on the official portal.

### Subscription and Service Scams

"Your Netflix subscription has been suspended. Update your payment." "Your Apple ID has been locked. Verify now." These exploit the fear of losing access to services you use daily.

**How to verify**: Open the app or website of the service directly. Log in through your [password manager](/password-managers/) -- PanicVault will take you to the correct URL and autofill your credentials, ensuring you never land on a fake site. If your account were actually suspended, you would see the notification there.

### Two-Factor Authentication Scams

"Your verification code is 847291. If you didn't request this, call [number]." This is more sophisticated. The attacker has your username and password (possibly from a [data breach](/data-breaches/)) and is attempting to log into your account. When the real service sends a 2FA code to your phone, the attacker texts you pretending to be the service, asking you to "confirm" the code by responding or calling a number.

**How to verify**: If you receive a 2FA code you did not request, someone is trying to access your account. Do not share the code with anyone. Change your password immediately. Enable a stronger form of [two-factor authentication](/two-factor-authentication/) if available.

### Prize and Contest Scams

"Congratulations! You've won a $500 gift card. Claim now." "You've been selected for a cash prize." If you did not enter a contest, you did not win one. These messages harvest personal information or credit card details under the pretense of "processing your prize."

### Job Offer Scams

"Work from home, earn $3,000/week. Apply now." "A company has viewed your resume and wants to schedule an interview." These target job seekers with offers that are too good to be true, collecting personal information or advance fees.

## How to Protect Yourself from Smishing

### Never Tap Links in Unexpected Text Messages

This is the single most important rule. If you receive a text with a link, and you did not initiate the interaction, do not tap the link. Instead, navigate to the relevant website or app directly.

### Use Your Password Manager for Navigation

When a text claims there is an issue with one of your accounts, open your password manager and navigate to the site from your saved entry. PanicVault stores the correct URL alongside your credentials. Tapping the entry opens the real website, not whatever fake site the smishing link points to.

This is one of the ways a [password manager prevents phishing](/phishing/password-manager-prevents-phishing/) -- it serves as a curated directory of legitimate URLs for every service you use.

### Enable Spam Filtering

Both iOS and Android offer built-in SMS spam filtering:

- **iPhone**: Go to Settings > Messages > Filter Unknown Senders. This moves texts from unknown numbers into a separate list, reducing the chance of acting on them impulsively. You can also report spam messages to Apple.
- **Android**: Google Messages includes built-in spam protection. Enable it in the Messages app settings.

Third-party apps can provide additional filtering, though be cautious about granting messaging permissions to apps from unknown developers.

### Do Not Reply to Suspicious Texts

Replying -- even with "STOP" -- confirms that your phone number is active and monitored. This makes you a more valuable target for future attacks. Simply delete the message or report it as spam.

### Report Smishing Messages

Forward suspicious texts to 7726 (SPAM), a reporting service supported by most mobile carriers in the United States. You can also [report phishing](/phishing/report-phishing/) to the FTC at ReportFraud.ftc.gov.

### Be Skeptical of Short Codes and Unknown Numbers

Legitimate businesses do use short codes for notifications, but so do scammers. Receiving a message from a short code does not confirm legitimacy. If a short code message asks you to take action, verify through the company's official channels.

## Smishing and Social Engineering

Smishing is often the opening move in a larger [social engineering](/phishing/social-engineering-guide/) campaign. A text message creates initial contact and urgency, followed by a phone call that deepens the manipulation, followed by instructions to transfer money or provide access.

For example:

1. You receive a text: "Suspicious activity on your Wells Fargo account. Call 1-800-XXX-XXXX immediately."
2. You call the number. A professional-sounding person answers as "Wells Fargo Fraud Department."
3. They walk you through "verifying" your account, during which you provide account numbers, PINs, and personal information.
4. The attacker now has everything they need to drain your account.

The defense is always the same: [verify through a separate channel](/phishing/verify-suspicious-messages/). Do not call numbers from suspicious texts. Look up the real number independently.

## What to Do If You Have Responded to a Smishing Message

If you tapped a link or provided information before realizing it was a scam:

### If You Entered Credentials

1. Go directly to the real website (type the URL or use your password manager).
2. Change your password immediately. Use a [strong, unique password](/password-security/).
3. Enable [two-factor authentication](/two-factor-authentication/) if it is not already active.
4. Check for unauthorized activity on the account.
5. If you use the same password elsewhere (which a password manager prevents), change it on those accounts too.

### If You Provided Financial Information

1. Contact your bank or credit card company immediately to report potential fraud.
2. Request new card numbers.
3. Monitor your statements closely for unauthorized charges.
4. Consider placing a fraud alert or credit freeze with the major credit bureaus.

### If You Downloaded Something

1. Do not open any downloaded files.
2. Run a security scan on your device.
3. If you are on an iPhone, the risk is lower due to iOS sandboxing, but remain vigilant for unusual behavior.

### In All Cases

1. [Report the phishing attempt](/phishing/report-phishing/).
2. Block the sender's number.
3. Monitor your accounts for several weeks following the incident.

## Teaching Others About Smishing

[Training your family to spot scams](/phishing/train-family/) is especially important for smishing because text messages reach everyone -- including family members who may be less security-aware. Show them real examples of smishing texts (from your own spam folder or from online repositories). Walk through the verification process together. Help them set up spam filtering on their phones.

The simplest rule to teach: "If a text asks you to tap a link or call a number, and you were not expecting it, do not do it. Go to the app or website directly instead."

## Related Articles

- [How to Recognize a Phishing Email: 10 Red Flags](/phishing/recognize-phishing/)
- [QR Code Scams (Quishing): The Newest Phishing Threat](/phishing/qr-code-scams/)
- [How to Verify Suspicious Emails, Texts, and Calls](/phishing/verify-suspicious-messages/)
- [How a Password Manager Protects From Phishing](/phishing/password-manager-prevents-phishing/)
- [How to Report a Phishing Attempt](/phishing/report-phishing/)
