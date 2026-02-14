---
title: "Tech Support Scams: How to Recognize and Avoid Them"
description: "Tech support scams cost victims billions annually. Learn how fake tech support calls and pop-ups work, and how to protect yourself and your family."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Phishing & Social Engineering"
---

Your screen suddenly displays a terrifying warning. "CRITICAL ALERT: Your computer has been infected with a virus. Call Microsoft Support immediately at 1-800-XXX-XXXX. Do not restart your computer." Your browser is frozen. You cannot close the tab. An alarm sound plays from your speakers. Your first instinct is to call the number for help. That instinct is exactly what the scammer is counting on. This article is part of our [Phishing & Social Engineering](/phishing/) guide.

Tech support scams are a pervasive form of [social engineering](/phishing/social-engineering-guide/) that exploit fear and technical unfamiliarity to defraud victims. They cost consumers billions of dollars annually and disproportionately target elderly and less tech-savvy individuals. Understanding how they work is your best defense.

## How Tech Support Scams Work

### Pop-Up Scams

The most common variant. You visit a website -- sometimes a legitimate one with malicious ads, sometimes a site reached through a [phishing link](/phishing/recognize-phishing/) -- and a full-screen warning appears. The pop-up is designed to look like a legitimate Windows, macOS, or browser security alert. It claims your computer is infected, your data is at risk, or your system is about to crash.

Key characteristics of scam pop-ups:

- **Full-screen or difficult to close**: The pop-up may take over your browser, using JavaScript to resist being closed.
- **Phone number prominently displayed**: Legitimate security software does not display phone numbers in warning dialogs.
- **Audio warnings**: Automated voice messages or alarm sounds increase panic.
- **Countdown timers**: "Your files will be encrypted in 5:00 minutes" creates urgency.
- **Official-looking branding**: Microsoft, Apple, Norton, McAfee logos and color schemes.
- **Technical jargon**: "Trojan.GenericKD.46789 detected" -- specific-sounding but meaningless error codes.

### Phone Call Scams

You receive an unsolicited phone call from someone claiming to be from Microsoft, Apple, your internet provider, or a well-known antivirus company. They tell you that your computer has been sending error reports, that your internet connection is compromised, or that your account has been breached.

The caller may reference real technical concepts -- IP addresses, Windows Event Viewer logs, router configurations -- to establish credibility. They sound professional and use scripts that have been refined through thousands of interactions.

With [deepfake voice cloning](/phishing/deepfake-voice-scams/), some tech support scammers now clone the voices of actual company representatives or use AI-generated voices that sound authentic and professional.

### Search Engine Scams

You search for "Apple support phone number" or "Microsoft help" and click on what appears to be an official result. The website looks legitimate but the phone number connects to a scam call center. Search engine ads (which appear above organic results) are sometimes purchased by scammers to appear for these exact searches.

### Email and Text Scams

Similar to [smishing](/phishing/smishing/) and email phishing, you receive a message claiming to be from a tech company alerting you to a problem. "Your Microsoft 365 subscription has been renewed for $499.99. Call to cancel." The invoice or charge is fabricated, but the fear of an unauthorized payment compels you to call.

## What Happens When You Engage

### Phase 1: Establishing Control

The scammer asks you to install remote access software -- TeamViewer, AnyDesk, UltraViewer, or similar tools. These are legitimate programs, but in the scammer's hands, they become tools for fraud. Once installed, the scammer can see your screen, control your mouse and keyboard, and access your files.

### Phase 2: Manufacturing Evidence

With remote access, the scammer "demonstrates" the problem. Common tactics include:

- **Event Viewer logs**: Every Windows computer has warning and error entries in Event Viewer. These are normal system operations. The scammer opens Event Viewer and points to the yellow and red entries as evidence of "infections" or "hackers."
- **Netstat commands**: Running network commands that show active connections, which the scammer claims are "hackers connected to your computer."
- **Tree commands**: Displaying the file directory tree rapidly scrolling, claiming it shows "malicious files being detected."
- **Disabled security**: Showing that Windows Defender or another security product has been "compromised" (often by the scammer disabling it themselves during the remote session).

None of this is real. It is theater designed to convince you that your computer is in danger and that the caller is the only one who can help.

### Phase 3: The Payment

Once you are convinced your computer is infected, the scammer offers to fix it -- for a price. Payment is requested via:

- **Credit card**: For "security software" or "tech support plans" ranging from $199 to $999.
- **Gift cards**: Scammers often ask for Apple, Google Play, or Amazon gift cards and have you read the card numbers over the phone.
- **Wire transfer or cryptocurrency**: For larger amounts.
- **Ongoing subscriptions**: Signing you up for monthly "protection plans" that provide no actual service.

### Phase 4: Additional Exploitation

Some scammers go further:

- **Installing actual malware**: Keyloggers, ransomware, or remote access trojans that persist after the call ends.
- **Stealing financial information**: While they have remote access, they may look at your browser history, saved passwords, banking apps, or documents for financial information.
- **Accessing bank accounts**: The scammer asks you to log into your bank account "to verify your identity" or "to process a refund." With remote access, they can see your credentials and account balances.
- **Creating a recurring fraud relationship**: Calling back weeks or months later with a new "problem" and extracting more money.

## Who Is Targeted

Tech support scams disproportionately affect:

- **Elderly individuals**: Less likely to recognize the technical theater and more trusting of authority figures.
- **Less tech-savvy users**: People who are not confident in their technical knowledge and rely on others for computer help.
- **Windows users**: Most tech support scam scripts are designed for Windows, though Mac-specific scams are increasing.
- **People who have been scammed before**: Scammers share and sell victim lists. If you have fallen for a tech support scam once, you are likely to be targeted again.

## How to Protect Yourself

### Never Call a Number from a Pop-Up Warning

Legitimate security software does not display phone numbers in warning dialogs. If a pop-up tells you to call a number, it is a scam. Close the browser (if necessary, force-quit the browser application) and move on.

On a Mac, force-quit Safari or Chrome by pressing Command+Option+Escape, selecting the browser, and clicking Force Quit. On Windows, use Ctrl+Alt+Delete to open Task Manager and end the browser process.

### Never Allow Remote Access from an Unsolicited Contact

No legitimate company will ever call you unsolicited and ask for remote access to your computer. Not Microsoft. Not Apple. Not your internet provider. If someone calls and asks you to install TeamViewer, AnyDesk, or any other remote access tool, hang up.

### Verify Through Official Channels

If you are concerned about a genuine technical issue:

- **Apple**: Visit apple.com/support or call 1-800-MY-APPLE.
- **Microsoft**: Visit support.microsoft.com.
- **Your internet provider**: Call the number on your bill.

Do not search for support phone numbers -- use the numbers on official websites or on physical documentation (bills, contracts, product packaging). See our guide on [verifying suspicious messages](/phishing/verify-suspicious-messages/) for a systematic verification approach.

### Use a Password Manager

A [password manager](/password-managers/) protects you in several ways during a tech support scam:

- If a scammer directs you to a [fake login page](/phishing/fake-login-pages/), PanicVault will not autofill your credentials because the domain does not match.
- Your saved passwords are encrypted and protected by biometric authentication (Face ID, Touch ID). Even if a scammer has remote access to your computer, they cannot access your PanicVault database without your biometric confirmation.
- [Strong, unique passwords](/password-security/) generated by your password manager mean that even if a scammer observes one password, they cannot use it to access your other accounts.

### Keep Your Software Updated

Genuine security updates come from your operating system and legitimate app stores. macOS and iOS deliver updates through System Settings and the App Store. Windows delivers updates through Windows Update. These updates are applied automatically or through the system's built-in update mechanism -- never through a phone call or a pop-up in your browser.

### Educate Vulnerable Family Members

Tech support scams are a primary concern when [training your family to spot scams](/phishing/train-family/). Walk elderly parents and grandparents through the following:

- "If a scary pop-up appears, close the browser or turn off the computer. It is not a real emergency."
- "No real company will ever call you and ask to remotely access your computer."
- "If you are worried about your computer, call me. I will help you determine if there is a real problem."

Give them a specific person to call -- you, a tech-savvy family member, or a trusted local computer repair shop -- so they have an alternative to calling the scam number.

## What to Do If You Are Currently Being Scammed

If you are in the middle of a tech support scam interaction:

1. **Hang up immediately** if you are on a phone call.
2. **Disconnect from the internet** by turning off Wi-Fi or unplugging your ethernet cable. This severs any remote access connection.
3. **Uninstall remote access software** (TeamViewer, AnyDesk, etc.) if you installed it during the interaction.
4. **Change your passwords** for any accounts you accessed during the remote session. Use a [password manager](/password-managers/) and a different device to do this.
5. **Run a security scan** on your computer using your operating system's built-in security tools.
6. **Contact your bank** if you made any payments. Credit card charges can often be disputed. Wire transfers and gift card payments are harder to recover.

## What to Do If You Have Already Been Scammed

1. **Contact your bank or credit card company** immediately to report fraud and dispute charges.
2. **Change all passwords** -- especially email, banking, and social media. Use a [password manager](/password-managers/) on a device that was not compromised.
3. **Enable [two-factor authentication](/two-factor-authentication/)** on all important accounts.
4. **Have your computer professionally examined** by a trusted local technician (not someone from a phone number you found online). Remote access tools may have left backdoors or malware.
5. **[Report the scam](/phishing/report-phishing/)** to the FTC at ReportFraud.ftc.gov, the FBI's IC3 at ic3.gov, and your state attorney general's office.
6. **Monitor your credit** and financial accounts for unusual activity.
7. **Do not be ashamed** -- Tech support scams are designed by professionals to exploit human psychology. Report it so others can be protected.

## The Refund Scam: A Second Wave

Some victims receive a follow-up call weeks or months after the initial scam. The caller claims to be from a "refund department" and says the company that scammed you has been shut down, and you are eligible for a refund. To process the refund, they need remote access to your computer to "verify your account."

This is a second scam. There is no refund. The caller is often the same scammer (or an associate) looking to extract more money. If you have been scammed and are contacted about a refund, ignore the call.

## The Takeaway

The two essential rules for avoiding tech support scams:

1. **No legitimate company will ever call you unsolicited about a computer problem.**
2. **Never call a phone number displayed in a browser pop-up or alarm.**

If something on your screen says your computer is infected and you need to call a number, it is a scam -- 100% of the time. Close the browser, restart your computer, and go about your day.

## Related Articles

- [What Is Social Engineering? Comprehensive Guide](/phishing/social-engineering-guide/)
- [How to Recognize a Phishing Email: 10 Red Flags](/phishing/recognize-phishing/)
- [How to Train Your Family to Spot Scams](/phishing/train-family/)
- [How a Password Manager Protects From Phishing](/phishing/password-manager-prevents-phishing/)
- [How to Report a Phishing Attempt](/phishing/report-phishing/)
