---
title: "How to Recognize a Phishing Email: 10 Red Flags"
description: "Learn the 10 most reliable red flags that identify phishing emails in 2026, even as AI makes scam messages harder to detect."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Phishing & Social Engineering"
---

Phishing emails are responsible for more account compromises, financial losses, and data breaches than any other attack vector. With 3.4 billion phishing emails sent daily, you are almost certainly receiving them -- the question is whether you can tell them apart from legitimate messages. This article is part of our comprehensive [Phishing & Social Engineering](/phishing/) guide, and it gives you a practical checklist for identifying phishing attempts before they succeed.

The challenge has grown significantly. [AI-powered phishing](/phishing/ai-powered-phishing/) has eliminated many of the obvious signals -- poor grammar, broken formatting, generic greetings -- that once made phishing emails easy to dismiss. But even the most sophisticated phishing campaigns leave traces. Here are the ten red flags that remain reliable in 2026.

## Red Flag 1: Artificial Urgency

The most consistent signal across all phishing emails is urgency that demands immediate action. Your account will be suspended. Your payment failed. Your tax return has been flagged. You have 24 hours to respond.

Legitimate organizations rarely impose artificial deadlines through email. Your bank will not close your account because you did not click a link within two hours. The IRS does not threaten arrest via email. When a message makes you feel like you must act right now, that emotional pressure is almost always manufactured.

**What to do**: When you feel urgency, pause. That instinct to act immediately is exactly what the attacker is counting on. Take a breath, and evaluate the message rationally. If the claim is legitimate, going directly to the organization's website or calling their official number will confirm it.

## Red Flag 2: Requests for Credentials or Sensitive Information

No reputable organization will ask you to provide your password, Social Security number, credit card details, or other sensitive information via email. Not your bank. Not Apple. Not the IRS. Not your employer's IT department.

Phishing emails frequently include links to [fake login pages](/phishing/fake-login-pages/) that look identical to real sites. The email claims you need to "verify your identity" or "confirm your account" by logging in. The login page captures whatever you type and sends it directly to the attacker.

**What to do**: Never enter credentials through a link in an email. If you need to log into an account, open your browser and navigate to the site directly. Better yet, use a [password manager](/password-managers/) that only autofills on the correct domain -- it will refuse to fill credentials on a phishing site automatically.

## Red Flag 3: Mismatched or Suspicious URLs

Hovering over a link in an email (without clicking) reveals the actual URL it leads to. Phishing emails frequently disguise malicious URLs behind legitimate-looking link text. The text might say "https://www.bankofamerica.com" but the actual URL leads to "bankofamerica-secure-login.scam-domain.com."

Common URL tricks include:

- **Lookalike domains**: "amaz0n.com" (zero instead of 'o'), "microsft.com" (missing letter), "paypa1.com" (number one instead of 'l').
- **Subdomain abuse**: "bankofamerica.attacker-site.com" -- the real domain here is "attacker-site.com," not Bank of America.
- **URL shorteners**: Bit.ly or similar services that hide the true destination.
- **Homograph attacks**: Using Unicode characters that look identical to Latin letters but point to different domains.

**What to do**: Always hover over links before clicking. On mobile, long-press a link to preview the URL. If you are unsure, do not click -- navigate to the site directly through your browser or use your password manager's autofill, which performs domain matching automatically.

## Red Flag 4: Unexpected Attachments

Approximately 94% of malware is delivered via email, and malicious attachments are a primary delivery mechanism. Phishing emails may include attachments disguised as invoices, shipping labels, voice messages, or documents requiring your review.

Dangerous attachment types include:

- **.exe, .scr, .bat, .cmd** -- Executable files that run code on your computer.
- **.zip, .rar, .7z** -- Compressed files that may contain executables or exploit vulnerabilities in archive software.
- **.docm, .xlsm** -- Microsoft Office files with macros that execute malicious code.
- **.html, .htm** -- Web pages that may contain credential-harvesting forms or redirect to phishing sites.
- **.iso, .img** -- Disk image files that can bypass some email security filters.

**What to do**: Do not open attachments you did not expect, even if they appear to come from someone you know. If a colleague sends you an unexpected attachment, verify with them through a different channel before opening it.

## Red Flag 5: Sender Address Inconsistencies

Examine the full sender email address, not just the display name. Email clients often show a friendly name like "Apple Support" while the actual address might be "apple-support@random-domain.xyz." These are easy to spot when you look at the complete address.

More sophisticated attacks use:

- **Spoofed addresses**: Making the "From" field appear to come from a legitimate domain. Email authentication protocols (SPF, DKIM, DMARC) help prevent this, but not all organizations implement them fully.
- **Lookalike domains**: Registering domains like "apple-inc.com" or "support-microsoft.com" that look plausible at a glance.
- **Compromised accounts**: Using legitimately hacked email accounts to send phishing from trusted addresses. This is particularly effective in [business email compromise](/phishing/business-email-compromise/) attacks.

**What to do**: Click on the sender name to reveal the full email address. Compare the domain to what you would expect from that organization. When in doubt, [verify through a separate channel](/phishing/verify-suspicious-messages/).

## Red Flag 6: Generic or Incorrect Personal Details

While AI has made personalization easier for attackers, many phishing campaigns still use generic greetings like "Dear Customer," "Dear Account Holder," or "Dear User." Your bank knows your name. So does your employer. A generic greeting from an organization that should know you personally is suspicious.

On the flip side, some phishing emails include personal details (your name, employer, recent purchases) gathered from [data breaches](/data-breaches/), social media, or public records. The presence of personal details does not confirm legitimacy -- it just means the attacker did some research.

**What to do**: Treat personalization as neutral, not as evidence of legitimacy. Focus on the other red flags in this list rather than being reassured by the presence of your name.

## Red Flag 7: Threats or Negative Consequences

Phishing messages often threaten negative outcomes if you do not comply: account suspension, legal action, fines, service termination, or public embarrassment. These threats create fear that overrides critical thinking.

Examples include:

- "Your account will be permanently deleted in 24 hours."
- "Legal proceedings will begin if payment is not received."
- "Your recent transaction has been flagged for fraud -- verify immediately or your account will be frozen."

**What to do**: Legitimate organizations communicate account issues through their official apps and portals, not through threatening emails. If a threat feels real, verify it through official channels -- not through any link or phone number in the email itself.

## Red Flag 8: Too-Good-to-Be-True Offers

The inverse of threats. Instead of fear, these phishing emails exploit greed or excitement. You have won a prize. You are eligible for an unexpected refund. A cryptocurrency investment guarantees 10x returns. A job offer promises extraordinary compensation for minimal work.

**What to do**: If you did not enter a contest, you did not win one. If a financial opportunity seems too good to be true, it is. Verify any unexpected financial communication through official channels before taking action.

## Red Flag 9: Inconsistent Branding and Formatting

While AI and modern phishing kits have made visual replication easier, subtle inconsistencies often remain. Look for:

- **Logo quality** -- Slightly blurry or outdated logos compared to the organization's current branding.
- **Color mismatches** -- Shades that do not quite match the company's brand palette.
- **Footer inconsistencies** -- Missing or incorrect legal disclaimers, privacy policy links, or unsubscribe options.
- **Layout differences** -- Spacing, font choices, or formatting that differs from previous legitimate emails from the same organization.
- **Mixed languages or styles** -- Parts of the email that seem to have been written by different people or translated inconsistently.

**What to do**: Compare suspicious emails to previous legitimate communications from the same organization. Look at your email history for a genuine message from that sender and compare the visual details.

## Red Flag 10: Unusual Requests That Break Normal Procedures

Phishing succeeds by getting you to do something outside your normal routine. A CEO emails asking you to buy gift cards. A vendor requests payment to a new bank account. IT asks you to install software from an unfamiliar link. HR needs you to update your direct deposit information through a web form.

The principle behind [social engineering](/phishing/social-engineering-guide/) is exploiting trust and authority to bypass established procedures. Any request that asks you to deviate from how things are normally done should trigger extra scrutiny.

**What to do**: Verify unusual requests through established channels. Call the person who supposedly sent the request using a phone number you already have -- not one provided in the email. For financial requests, follow your organization's verification procedures regardless of who appears to be asking.

## What to Do When You Spot a Phishing Email

1. **Do not click any links or open any attachments** in the message.
2. **Do not reply** to the sender.
3. **Report it** -- Forward the email to your organization's IT security team if applicable. [Report it to the relevant authorities](/phishing/report-phishing/) (the Anti-Phishing Working Group at reportphishing@apwg.org, the FTC, or your email provider's reporting mechanism).
4. **Delete it** -- After reporting, delete the email from your inbox.
5. **Warn others** -- If the phishing email impersonates someone you know, alert that person. Their account may be compromised, or others may be receiving similar messages.

## Building Lasting Habits

Recognizing phishing is a skill that improves with practice. Make it a habit to evaluate every email against these red flags before taking action. The process gets faster with repetition -- eventually, you will spot most phishing attempts in seconds.

Combine awareness with technical defenses. A [password manager that prevents phishing](/phishing/password-manager-prevents-phishing/) provides an automatic safety net. PanicVault, for instance, will only autofill credentials when the domain matches exactly, stopping you from entering your password on a fake site even if you do not notice the red flags. [Two-factor authentication](/two-factor-authentication/) provides a second layer of defense. Together, these tools ensure that even a moment of inattention does not lead to a compromised account.

[Train your family](/phishing/train-family/) to recognize these signals too. Phishing affects everyone, and the people in your life who are least aware of these tactics are the most vulnerable.

## Related Articles

- [AI-Powered Phishing in 2026: Harder to Spot](/phishing/ai-powered-phishing/)
- [Fake Login Pages: How Phishing Sites Steal Credentials](/phishing/fake-login-pages/)
- [How to Verify Suspicious Emails, Texts, and Calls](/phishing/verify-suspicious-messages/)
- [How a Password Manager Protects From Phishing](/phishing/password-manager-prevents-phishing/)
- [How to Report a Phishing Attempt](/phishing/report-phishing/)
