---
title: "QR Code Scams (Quishing): The Newest Phishing Threat"
description: "QR code phishing (quishing) is the fastest-growing phishing vector. Learn how malicious QR codes steal credentials and how to protect yourself."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Phishing & Social Engineering"
---

QR codes are everywhere -- restaurant menus, parking meters, event tickets, business cards, product packaging, advertisements. The pandemic accelerated QR code adoption for contactless interactions, and we have collectively been trained to scan them without hesitation. Attackers have noticed. QR code phishing, known as "quishing," has emerged as one of the fastest-growing phishing vectors, and it exploits a fundamental problem: you cannot tell where a QR code leads just by looking at it. This article is part of our [Phishing & Social Engineering](/phishing/) guide.

## How QR Code Phishing Works

A QR code is simply a visual representation of a URL or other data. When you scan a QR code with your phone's camera, it decodes the embedded URL and offers to open it in your browser. The problem is that unlike a text URL, which you can read and evaluate before clicking, a QR code's contents are invisible until after you scan it.

Attackers exploit this opacity by placing malicious QR codes in locations where people expect to find legitimate ones. The QR code leads to a [fake login page](/phishing/fake-login-pages/) that harvests credentials, a page that downloads malware, or a payment form that captures financial information.

### Physical QR Code Attacks

- **Parking meters and pay stations**: Attackers place stickers with fraudulent QR codes over legitimate payment QR codes. You think you are paying for parking; you are actually entering your credit card information on a scam site.
- **Restaurant menus**: Fake QR codes placed on tables or menus direct diners to phishing sites instead of the restaurant's actual menu.
- **Public notices and flyers**: Fraudulent QR codes on posters for community events, rental listings, or public services.
- **Package delivery notices**: A sticker on your door or mailbox with a QR code to "reschedule your delivery" -- a physical version of the [smishing](/phishing/smishing/) delivery scam.
- **EV charging stations**: QR codes that appear to link to the charging network's payment system but actually lead to credential-harvesting sites.

### Digital QR Code Attacks

- **Phishing emails with QR codes**: Instead of embedding a malicious link in the email (which email security tools can detect and block), attackers embed a QR code. The recipient scans the code with their phone, bypassing email security filters entirely because the QR code image is not a clickable link.
- **PDF attachments**: QR codes embedded in attached documents, particularly fake invoices, shipping notices, or corporate memos.
- **Social media posts and ads**: QR codes shared on social platforms that promise discounts, exclusive content, or prize claims.

## Why Quishing Is Particularly Dangerous

### Bypasses Email Security

Most email security tools scan text content, URLs, and attachments for malicious indicators. A QR code embedded as an image is harder to analyze because the security tool needs to decode the image to extract the URL. Many filters simply do not do this, allowing the phishing email to reach the inbox even when the same URL in text form would have been blocked.

### Bypasses Desktop Security

When you scan a QR code from an email on your computer screen, the URL opens on your phone -- a different device with different security controls. Your phone may not have the same email security, DNS filtering, or browser protections that your work laptop does. The attacker effectively moves the attack from your secured device to your less-secured one.

### Cannot Be Previewed

You cannot read a QR code with your eyes. Unlike a text URL where you can spot "bank0famerica.com" before clicking, a QR code reveals nothing until after you scan it. Your phone's camera will show a preview of the URL, but in the rush of daily life, many people tap "Open" without carefully reading the preview.

### Exploits Trust in Physical Media

People have a higher level of trust in physical objects than in digital messages. A QR code on a restaurant table, a parking meter, or a government building feels inherently trustworthy because it exists in the physical world. Attackers exploit this trust by placing stickers or replacing legitimate QR codes in trusted physical locations.

### Difficult to Report and Block

Phishing URLs can be reported and added to blocklists. Malicious QR codes printed on stickers in public places are harder to identify, report, and remove. Each sticker is a localized attack that may only be discovered when someone falls for it.

## Real-World Quishing Examples

### Parking Meter Scams

Multiple cities in the United States, United Kingdom, and Australia have reported fraudulent QR code stickers placed on parking meters. Drivers scan the code expecting to pay for parking and are directed to a lookalike payment site that captures their credit card information. The real parking meter often has its own QR code underneath the sticker, making the fraud invisible unless you are specifically looking for it.

### Corporate Phishing Campaigns

Security researchers have documented quishing campaigns targeting corporate employees. The attacker sends an email that appears to come from the company's IT department with a QR code to "update your security settings" or "verify your identity for the new system." Employees scan the QR code with their phones and enter their corporate credentials on a fake login page. Because the authentication happens on the employee's personal phone, corporate email security and network monitoring tools never see the attack.

### Public Wi-Fi QR Codes

QR codes in cafes, airports, and hotels that claim to provide Wi-Fi access but actually direct users to credential-harvesting sites or prompt them to install a malicious network profile on their device.

### Cryptocurrency Scams

QR codes displayed at ATMs, in promotional materials, or on social media that claim to connect to cryptocurrency wallets or exchanges but direct to fraudulent sites designed to steal wallet credentials or payment information.

## How to Protect Yourself from QR Code Phishing

### Preview Before Opening

When your phone's camera detects a QR code, it displays a preview of the URL. Take a moment to read this preview before tapping "Open." Look for:

- **The domain name**: Is it the domain you expect? A parking meter should link to the official parking service, not a random domain.
- **HTTPS**: While HTTPS alone does not confirm legitimacy, its absence on a login or payment page is a red flag.
- **URL length and complexity**: Excessively long or complex URLs with random characters may indicate a phishing redirect.

### Check for Physical Tampering

Before scanning a QR code in a public location, examine it physically:

- **Is it a sticker placed over another QR code?** Try to peel up the edge. If there is a QR code underneath, the sticker is likely fraudulent.
- **Does the QR code match the surrounding material?** A sticker that looks out of place on a professional sign or payment terminal is suspicious.
- **Is the QR code printed on professional materials or on a separate label?** Legitimate QR codes are usually printed as part of the sign or menu, not added as afterthought stickers.

### Use Your Password Manager

If a QR code leads to a login page, do not enter credentials manually. Use your [password manager](/password-managers/) to check whether the site matches a saved entry. PanicVault will only offer to autofill credentials if the domain matches exactly. If PanicVault does not recognize the site, that is a strong signal that the URL is not the legitimate site you think it is. This is one of the key ways a [password manager prevents phishing](/phishing/password-manager-prevents-phishing/).

### Navigate Directly Instead

When possible, skip the QR code entirely and navigate to the service directly:

- **Restaurant menu**: Ask the server for a physical menu or navigate to the restaurant's website directly.
- **Parking**: Use the parking service's official app instead of scanning a QR code.
- **Payments**: Use the official app or website of the service rather than a QR code you find in the environment.
- **Corporate systems**: Navigate to internal resources through your company's intranet or bookmarks, not through QR codes in emails.

### Be Extra Cautious with QR Codes in Emails

A QR code in an email should be treated with the same skepticism as a link in an email. If an email from your "IT department" contains a QR code, [verify the request](/phishing/verify-suspicious-messages/) through a separate channel before scanning it. Contact the IT department directly using a phone number or email address you already have.

### Keep Your Phone's Software Updated

Phone operating systems and browsers receive regular security updates that improve their ability to detect malicious URLs and warn you about known phishing sites. Keep your device updated to benefit from the latest protections.

## What to Do If You Scanned a Malicious QR Code

### If You Entered Credentials

1. Go to the legitimate website directly (type the URL or use your password manager).
2. Change your password immediately with a [strong, unique password](/password-security/).
3. Enable [two-factor authentication](/two-factor-authentication/).
4. Check for unauthorized activity on the account.
5. If you entered the same credentials used on other sites, change those passwords too.

### If You Entered Payment Information

1. Contact your bank or credit card company immediately.
2. Request a new card number.
3. Monitor your statements for unauthorized charges.
4. Consider a fraud alert or credit freeze with credit bureaus.

### If You Downloaded Something

1. Do not open any downloaded files.
2. Run a security scan on your device.
3. If you installed a profile or configuration on your device, remove it (Settings > General > VPN & Device Management on iPhone).

### Report the Incident

1. If the QR code was in a physical location, report it to the business or property manager so they can remove it.
2. Report the phishing URL to Google Safe Browsing (safebrowsing.google.com/safebrowsing/report_phish/).
3. [Report the phishing attempt](/phishing/report-phishing/) to the FTC and relevant authorities.
4. If the QR code was in an email, report the email as phishing to your email provider.

## Organizational Defenses Against Quishing

Businesses should be aware that QR codes are increasingly used in phishing campaigns targeting their employees and customers:

- **Security awareness training**: Include quishing in security awareness programs. Many employees are trained to be cautious with email links but have never considered that a QR code could be malicious.
- **Email security**: Deploy email security tools that can decode and analyze QR codes embedded in emails.
- **Physical security**: Regularly inspect public-facing QR codes (on storefronts, menus, payment terminals) for tampering.
- **Alternative authentication**: For corporate systems, avoid using QR codes as the sole method of directing users to login pages. Provide direct URLs and use [password managers](/password-managers/) organization-wide.

## The Bigger Picture

QR code phishing is an evolution of the same [social engineering](/phishing/social-engineering-guide/) principles that drive all phishing -- it just uses a different delivery mechanism. The defense principles remain the same: verify before acting, use technical controls like password managers that check domains, and maintain healthy skepticism about unexpected requests.

As QR codes become even more embedded in daily life -- for payments, authentication, information access -- the attack surface will continue to grow. Building the habit of previewing, verifying, and using your password manager as a navigation tool will protect you regardless of how the technology evolves.

## Related Articles

- [What Is Smishing? How to Spot SMS Phishing](/phishing/smishing/)
- [Fake Login Pages: How Phishing Sites Steal Credentials](/phishing/fake-login-pages/)
- [How a Password Manager Protects From Phishing](/phishing/password-manager-prevents-phishing/)
- [How to Recognize a Phishing Email: 10 Red Flags](/phishing/recognize-phishing/)
- [How to Report a Phishing Attempt](/phishing/report-phishing/)
