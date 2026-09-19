---
title: "Amazon Phishing Emails: Real Examples & Where to Report Them (2026)"
description: "Real Amazon phishing email examples and how to spot a fake. Where to report them: forward to reportascam@amazon.com as an attachment, texts to 7726."
date: 2026-03-08
lastmod: 2026-09-19
draft: false
silo: "Phishing & Social Engineering"
faq:
  - q: "How do I know if an Amazon email is real?"
    a: "Check your Amazon Message Center. Amazon says every email it sends appears there, so if the message is missing, Amazon did not send it. You can also forward the email to verify@amazon.com, Amazon's verification address, and get a reply saying whether it is genuine. Real Amazon emails come from an address ending in amazon.com, and many email providers show Amazon's smile logo next to authenticated Amazon mail, but a sender line on its own can be faked."
  - q: "What does a fake Amazon email look like?"
    a: "Most fake Amazon emails copy a real notification: an order confirmation for something expensive you did not buy, an account suspension warning, a failed Prime payment, a delivery problem, a gift card reward, or a product recall refund. They use Amazon's logo and orange buttons and push you to act within hours. The giveaways are a sender address or link that is not on amazon.com, a request for your password or card number, and no matching message in your Amazon Message Center."
  - q: "Does Amazon send emails asking for personal information?"
    a: "No. Amazon says it never asks for your password or sensitive personal information over the phone or on an outside website, and never asks by text for personal information, payment details, or gift card codes. Treat any email, text, or call that asks for your password, one-time passcode, card number, bank details, or Social Security number as a scam."
  - q: "Where do I forward Amazon phishing emails?"
    a: "Forward them to reportascam@amazon.com, ideally as an attachment. That is the address on Amazon's Report a scam help page, and Amazon says an attached copy is the best way for it to track the message. Do not click any links first. Amazon will not reply personally, but you may get an automatic confirmation. If you have an Amazon account, you can also report it through the form linked from that page. The older stop-spoofing@amazon.com address no longer appears on Amazon's help pages. You can also forward the email to reportphishing@apwg.org and report it to the FTC at ReportFraud.ftc.gov."
  - q: "Is shipment-tracking@amazon.com legit?"
    a: "Yes, shipment-tracking@amazon.com is a real address Amazon uses for shipping notifications. But the name and address shown in the From line can be forged, so seeing it does not prove an email is genuine. In Gmail on a computer, click the small arrow under the sender's name: a real Amazon email shows mailed-by and signed-by domains that end in amazon.com, such as bounces.amazon.com and amazon.com. The simpler check is to ignore the email's links and open Your Orders in the Amazon app or at amazon.com. If the shipment is not listed there and the email is not in your Message Center, it is fake."
  - q: "Can a password manager protect me from Amazon phishing?"
    a: "Yes. A password manager like PanicVault checks the exact domain before autofilling credentials. If you land on a fake Amazon site like 'amazon-orders.com' instead of 'amazon.com,' the password manager will not autofill -- and that silence is your warning that something is wrong."
---

Amazon is one of the most impersonated brands in phishing. Check Point's [Q2 2026 brand phishing report](https://blog.checkpoint.com/research/which-brands-are-impersonated-most-inside-the-q2-2026-brand-phishing-report/) ranked it fifth, behind Microsoft, LinkedIn, Google, and Apple. The reason is reach: with hundreds of millions of customers, attackers know that nearly anyone who receives a fake Amazon email probably has a real Amazon account. The constant stream of order confirmations, delivery notifications, and Prime membership emails gives scammers an endless supply of pretexts that feel entirely plausible. This article is part of our comprehensive [Phishing & Social Engineering guide](/phishing/) and walks through real Amazon phishing patterns, how to check an email, and where to forward the fakes.

> **Quick answer**: A fake Amazon email usually copies a real notification -- an order confirmation for something expensive you did not buy, an account suspension warning, a failed Prime payment, a delivery problem, or a gift card "reward" -- and pushes you to click a button within hours. The giveaways are a sender address or link that is not on amazon.com, a request for your password, card number, or a payment, and no matching message in your Amazon [Message Center](https://www.amazon.com/gp/message). If you are not sure, forward the email to verify@amazon.com and Amazon will reply with whether it is genuine. To report a fake, forward it as an attachment to reportascam@amazon.com -- see [where to forward Amazon phishing emails](#where-to-forward-amazon-phishing-emails).

The sheer volume of legitimate Amazon emails works in the attackers' favor. If you order from Amazon regularly, you receive genuine emails about orders, shipments, returns, and account activity multiple times per week. A single phishing email dropped into that stream is easy to mistake for the real thing, especially when the branding is pixel-perfect and the subject line mirrors one you have seen before.

Below are six Amazon phishing formats that keep recurring -- most of them also appear on Amazon's own [Scam trends](https://www.amazon.com/gp/help/customer/display.html?nodeId=TapjnwRvIRtlgyLPSl) page -- along with text message variants, how to verify an email, and exactly where to report the fakes.

## Pattern 1: The Fake Order Confirmation

This is one of the most common Amazon phishing emails. It works because Amazon sends so many real order confirmations that most people do not scrutinize each one carefully.

**Typical subject lines**:
- "Your Amazon.com Order #112-4837291-7382910 Has Shipped"
- "Order Confirmation: MacBook Pro 16-inch -- $2,449.99"
- "Thank You for Your Order -- Arriving Tomorrow"
- "Your Amazon Purchase of $874.32 Is Being Processed"

**What it looks like**: The email mimics Amazon's standard order confirmation layout, complete with the Amazon logo, product image, order number, shipping details, and a total amount. The item is typically expensive -- electronics, jewelry, or luxury goods -- chosen specifically to trigger alarm if you did not place the order. The email includes a "Cancel This Order" or "View Order Details" button. Some versions skip the button and give a phone number to call "to cancel"; Amazon warns that order-confirmation scammers may try to get your payment details, talk you into installing software, or have you buy gift cards.

**The tell**: The sender address is usually not @amazon.com. Common fakes include orders@amazon-orders.com, noreply@amazonsecurity.net, confirm@amaz0n-order.com (note the zero replacing the letter "o"), or shipping@amazon-shipping.info. Because a display name and even the From line can be faked, a correct-looking address is not proof on its own -- the Message Center check below is. The "Cancel Order" button leads to a [fake login page](/phishing/fake-login-pages/) designed to capture your Amazon credentials and, often, your credit card number on a second screen.

**The reality**: If you did not place an order, there is no order to cancel. Amazon does not require you to "cancel" unfamiliar orders through an email link or a phone number in an email. Log into amazon.com directly and check Your Orders -- as Amazon puts it, only legitimate purchases will appear in your order history. If the order is not there, the email was a scam.

## Pattern 2: The Account Suspension Warning

This variant exploits the fear of losing access to your Amazon account, including your order history, saved addresses, payment methods, and digital purchases.

**Typical subject lines**:
- "Action Required: Your Amazon Account Has Been Suspended"
- "Amazon Account Alert: Verify Your Identity Immediately"
- "Your Amazon Account Will Be Permanently Closed in 24 Hours"
- "Suspicious Activity Detected -- Your Amazon Account Is Locked"

**What it looks like**: The email warns that your Amazon account has been flagged for a security violation, suspicious login, or policy breach. It states that your account has been locked or will be permanently closed unless you verify your identity within 24 or 48 hours. A large orange button (matching Amazon's brand color) says "Verify Your Account" or "Unlock Account Now."

**The tell**: Amazon does not threaten to permanently close accounts via email with a 24-hour countdown. The artificial urgency is designed to override your critical thinking. The verification page requests information Amazon already has -- your password, full credit card number, Social Security number, or date of birth. Amazon says it never asks for your password or sensitive personal information over the phone or on any external website.

**The reality**: If your Amazon account were genuinely restricted, you would discover it when you tried to sign in. Any required actions would be presented within your account after login, not demanded through an email with a ticking clock. Amazon's advice for account-status questions is to check the Amazon website or app directly; authentic emails are logged in your Message Center.

## Pattern 3: The Prime Membership Expiration

With more than 200 million Prime members worldwide, this phishing pattern has an enormous potential audience. It exploits the fear of losing Prime benefits -- free shipping, Prime Video, Prime Music, and exclusive deals.

**Typical subject lines**:
- "Your Amazon Prime Membership Has Expired"
- "Action Required: Renew Your Prime Membership to Avoid Interruption"
- "Amazon Prime: Your Payment Method Failed -- Update Now"
- "Your Prime Benefits Will Be Suspended Tomorrow"

**What it looks like**: The email states that your Prime membership is about to expire or that the payment method on file could not be charged for the renewal. It warns that you will lose access to free shipping, Prime Video, and other benefits unless you update your payment information. The email includes a "Renew Prime" or "Update Payment" button.

**The tell**: Amazon does send real emails when a Prime payment fails, so the subject line alone proves nothing. The difference is where the button goes: the phishing version links to a page outside amazon.com that collects your full card number under the guise of updating your payment method. Phone variants claim a membership fee is owed and ask for card or bank details -- Amazon says it never asks for payment information for products or services over the phone.

**The reality**: Do not use the email's button. Sign in to Amazon yourself and, under Your Account, select Prime Membership -- if there is a billing problem, it will be shown there, and you can fix it in the same place. Any genuine Prime email will also be in your Message Center.

## Pattern 4: The Delivery Notification Scam

This pattern exploits the expectation of package deliveries. If you order from Amazon frequently, you receive legitimate delivery notifications regularly, making a fake one easy to overlook.

**Typical subject lines**:
- "Your Amazon Package Could Not Be Delivered"
- "Delivery Failed: Confirm Your Address to Reschedule"
- "Amazon Delivery Update: Action Required"
- "Your Package Is Being Held -- Verify Delivery Address"

**What it looks like**: The email claims that a delivery attempt failed because the address was incomplete, the recipient was not available, or a customs or delivery fee must be paid before the package can be released. It includes a "Confirm Address" or "Schedule Redelivery" button. Some variants include a fabricated tracking number to add credibility.

**The tell**: Amazon does not charge delivery fees after you have already placed and paid for an order. Failed delivery notifications from Amazon and its carriers (UPS, USPS, FedEx) do not ask you to click a link and re-enter your address or payment details. The phishing page may request a small "redelivery fee" -- $1.99 or $3.49 -- which is designed to capture your credit card information rather than collect the fee itself.

**The reality**: If an Amazon delivery genuinely fails, you can track it through the Amazon app or at amazon.com under Your Orders. Redelivery is handled through the carrier (UPS, USPS, FedEx) or Amazon's system -- you will never need to pay an additional fee or re-enter your address through an email link.

## Pattern 5: The Gift Card Scam

Amazon gift card scams take two forms: phishing emails that claim you have received a gift card, and social engineering scams where someone pressures you to buy Amazon gift cards as a form of payment.

**Typical subject lines**:
- "You've Received an Amazon Gift Card Worth $200.00"
- "Congratulations! Claim Your Amazon Gift Card"
- "Amazon Reward: Your $150 Gift Card Is Ready"
- "Special Promotion: Free Amazon Gift Card for Loyal Customers"

**What it looks like**: The email congratulates you on receiving a gift card, earning a reward, or being selected for a promotional offer. It includes a "Claim Gift Card" or "Redeem Now" button. The branding mimics Amazon's gift card emails, and the amount is large enough to be enticing but not so large as to seem implausible.

**The tell**: Amazon does not send unsolicited gift cards via email to random customers. Legitimate Amazon gift card emails come from gc-orders@gc.email.amazon.com and include a claim code directly in the email body -- they do not require you to click a link and enter your credentials. The phishing page behind the "Claim" button harvests your Amazon login credentials and credit card information.

**The reality**: If someone genuinely sends you an Amazon gift card, you can redeem it at amazon.com/gc/redeem by entering the claim code. You will never need to provide your password or credit card number to claim a gift card. Any email asking you to "log in to claim" a gift card is a scam.

**The broader gift card scam**: Beyond phishing emails, be aware of social engineering scams where someone contacts you -- by phone, text, or email -- claiming to be from the IRS, a utility company, a tech support service, or even a family member, and asks you to buy Amazon gift cards and share the codes as a form of payment. No legitimate organization accepts Amazon gift cards as payment. Amazon warns about this on its [Common Gift Card Scams](https://www.amazon.com/gp/help/customer/display.html?nodeId=GGKDN3QZSKBFGNBF) help page.

## Pattern 6: The Fake Recall or Refund Notice

Amazon lists this one on its own [Scam trends](https://www.amazon.com/gp/help/customer/display.html?nodeId=TapjnwRvIRtlgyLPSl) page: a message claiming that something you recently bought has a safety problem and needs immediate action, with a refund as the bait.

**Typical subject lines**:
- "Urgent Safety Recall: Item From Your Recent Amazon Order"
- "Product Recall -- Claim Your Refund Within 48 Hours"
- "Important Safety Notice About Your Purchase"

**What it looks like**: The email says a product you may own has been recalled for a fire or injury risk and offers a full refund if you "confirm your details" through a link. The link leads to a fake refund form that asks for your Amazon login, card number, or bank details. Some versions arrive as a text message.

**The tell**: Amazon says it does not send text messages about recalls, and that it will never request sensitive information outside Amazon's website or app. Real Amazon recall emails can contain links, but only to Amazon pages -- a genuine refund never requires you to type your card number into a separate site.

**The reality**: Sign in to Amazon yourself and check the Your Recalls and Product Safety Alerts page. If a recall affects something you bought, it is listed there.

## Smishing: Amazon Text Message Scams

Amazon-branded [smishing](/phishing/smishing/) texts are common because a text feels urgent and a phone screen makes it hard to inspect a link. Amazon says it will never ask you by text to provide personal information, payment details, or gift card codes, or to call a phone number, and that it does not send texts about product recalls.

**Common Amazon smishing messages**:

- "Amazon: Your account has been locked due to suspicious activity. Verify now: [link]"
- "Amazon: Your package could not be delivered. Confirm your address: [link]"
- "Amazon Prime: Your membership payment failed. Update at: [link]"
- "Amazon Alert: Unauthorized purchase of $1,247.00. If not you, visit: [link]"
- "Amazon: You have a $50 reward waiting. Claim before it expires: [link]"

These texts include links to phishing sites that closely mimic Amazon's mobile login page. On a phone screen, it is difficult to inspect the URL in the browser's address bar, making mobile users particularly vulnerable. Some messages include shortened URLs (using bit.ly or similar services) that completely obscure the destination.

**How to handle Amazon smishing**:

1. Do not tap any links in the text, and do not reply.
2. Do not call any phone number included in the message.
3. Open the Amazon app directly and check your orders and account.
4. If you are concerned, type amazon.com into your browser manually.
5. Forward the suspicious text to 7726 (SPAM) to report it to your carrier.
6. Report it to the FTC at [ReportFraud.ftc.gov](https://reportfraud.ftc.gov/) -- Amazon's own Report a scam page sends people there for suspicious texts and phone calls.
7. Report it to Amazon through its [Report a scam](https://www.amazon.com/gp/help/customer/display.html?nodeId=GRGRY7AQ3LMPXVCV) page.
8. Delete the message.

## How to Verify an Amazon Email Is Legitimate

Before acting on any email that claims to be from Amazon, run through this checklist:

1. **Check the sender address**: Legitimate Amazon emails come from an address ending in amazon.com (such as auto-confirm@amazon.com, shipment-tracking@amazon.com, or order-update@amazon.com). Click on the sender name to see the full email address -- display names like "Amazon Customer Service" can be set to anything. Amazon says many email providers show its smile logo next to the message when Amazon is the actual sender. In Gmail on a computer, you can go further: click the small arrow under the sender's name, and a genuine Amazon email shows "mailed-by" and "signed-by" domains that end in amazon.com.

2. **Check Amazon's Message Center**: Amazon keeps a copy of every email it sends in your account's Message Center. Sign in and open Message Center from Your Account, or go to amazon.com/gp/message. If the email does not appear there, it is not from Amazon.

3. **Ask Amazon directly**: Forward the email to verify@amazon.com. Amazon launched this address in 2026; anyone can use it, customer or not, and it replies with whether the message is genuinely from Amazon. Amazon also has a Verify Communications form for signed-in customers, and in the US you can ask Alexa for Shopping in the Amazon app -- for example, "Is this email about my Prime membership from Amazon real?"

4. **Inspect links without clicking**: Hover over any buttons or links (on desktop) or long-press them (on mobile) to see the actual URL. Amazon's rule of thumb is that legitimate Amazon addresses have a dot right before amazon.com, as in https://www.amazon.com/... -- not amazon-orders.com, amaz0n.com, or amazon.com-verify.xyz (where the real domain is .xyz).

5. **Look for requests for sensitive information**: Amazon will not ask for your password, one-time passcode, full credit card number, Social Security number, or bank account details through an email link, a text, or a phone call. Any message requesting this information is fraudulent.

6. **Evaluate the urgency**: Legitimate Amazon communications do not threaten to permanently close your account within 24 hours or demand immediate payment through an email link.

7. **Verify independently**: Open the Amazon app or navigate to amazon.com directly. Any genuine order, delivery issue, or account notification will be visible within your account.

For a broader framework that applies to all phishing attempts, see our guide on [how to recognize phishing emails](/phishing/recognize-phishing/) and our [step-by-step message verification process](/phishing/verify-suspicious-messages/).

## Where to Forward Amazon Phishing Emails

Forward Amazon phishing emails to **reportascam@amazon.com**, as an attachment if your email app allows it. That is the address Amazon publishes on its [Report a scam](https://www.amazon.com/gp/help/customer/display.html?nodeId=GRGRY7AQ3LMPXVCV) help page, and Amazon says that sending the suspicious message as an attachment "is the best way for us to track it." Here is the full process:

1. **Do not click anything first.** Do not tap links or buttons, open attachments, or reply -- forwarding does not require any of that. If you want to confirm the email is fake before reporting it, check your Message Center or forward it to verify@amazon.com (see the checklist above).
2. **Forward it as an attachment to reportascam@amazon.com.** An attached copy keeps the original's hidden headers -- the routing and authentication details that show where it really came from -- which a pasted copy or screenshot loses.
   - **Gmail on a computer**: tick the checkbox next to the email in your inbox, click More (the three dots) at the top, then Forward as attachment.
   - **Outlook for Windows**: select the email, then choose More Respond Actions, then Forward as Attachment.
   - **Apple Mail on a Mac**: select the email, then choose Message, then Forward as Attachment.
   - **On a phone**: most mobile mail apps cannot forward as an attachment. A regular forward still gets the report to Amazon; an attachment is simply what Amazon prefers.
3. **Expect only an automatic reply.** Amazon says it cannot respond personally to messages sent to reportascam@amazon.com, but you may receive an automatic confirmation.
4. **Or use Amazon's reporting form.** If you have an Amazon account, the Report a scam page links to a signed-in form that asks whether you shared any information -- nothing, Amazon account information, banking information, remote access to your computer, or something else -- and gives advice for each case. You can also get there from Amazon's Customer Service page: choose "Report Something Suspicious" under "Help with something else," then the option for a suspicious call, email, or SMS.
5. **Forward texts to 7726 (SPAM).** Amazon-branded scam texts go to your mobile carrier at 7726, not to an Amazon email address.
6. **Report it to the FTC** at [ReportFraud.ftc.gov](https://reportfraud.ftc.gov/). The FTC recommends this for phishing emails and texts, and Amazon's Report a scam page points people there for suspicious texts and phone calls.
7. **Forward the email to the Anti-Phishing Working Group** at reportphishing@apwg.org, which the FTC also recommends. APWG likewise asks for Forward as Attachment when your email app supports it.
8. **Delete it** once you have reported it.

**What about `stop-spoofing@amazon.com`?** Older guides -- including earlier versions of this page -- told readers to forward Amazon phishing to `stop-spoofing@amazon.com`. That address no longer appears on Amazon's help pages. The address Amazon publishes today is reportascam@amazon.com, so use that one.

For a complete guide on reporting phishing across all brands and platforms, see our article on [how to report a phishing attempt](/phishing/report-phishing/).

## Why a Password Manager Is Your Strongest Defense

Knowing what Amazon phishing emails look like is valuable, but awareness alone is not a reliable defense. Even security-conscious people click links when they are tired, distracted, or rushing to check on a package. Modern [AI-powered phishing](/phishing/ai-powered-phishing/) emails arrive with perfect grammar, pixel-accurate branding, and realistic order details that make visual inspection increasingly unreliable. A [password manager](/password-managers/what-is-a-password-manager/) provides an automated safety net that works even when your attention does not.

### Domain Matching Stops Credential Theft

When you use a password manager's autofill to log into Amazon, the password manager checks the exact domain of the page you are on. If the domain is amazon.com, autofill works normally. If the domain is anything else -- amazon-orders.com, amazonsecurity.net, amaz0n.com, amazon.com-verify.xyz -- autofill stays silent. It does not matter how perfect the fake page looks. The domain check is automated and precise.

PanicVault performs this domain matching through Apple's system-wide AutoFill on iPhone, iPad, and Mac. When you tap a login field on a site claiming to be Amazon and PanicVault does not offer your credentials, that silence is your warning that the site is not genuine. Learn more about this mechanism in our article on [how a password manager prevents phishing](/phishing/password-manager-prevents-phishing/).

### Unique Passwords Contain the Blast Radius

If you reuse your Amazon password on other sites, a data breach anywhere gives attackers a direct path into your Amazon account through credential stuffing. With your Amazon account, they can make purchases on your stored payment methods, access your order history and address, and use your account for social engineering. A password manager generates and stores a unique, random password for every account, ensuring that a breach on one site cannot cascade to Amazon.

### Navigate From Your Vault, Not From Email Links

When you receive a notification about your Amazon account, instead of clicking the link in the email, open PanicVault and tap your Amazon entry. It will take you to the real amazon.com and autofill your credentials. This simple habit eliminates the risk of landing on a phishing page entirely.

## What to Do If You Fell for an Amazon Phishing Scam

If you entered your credentials on a phishing site or shared sensitive information, act immediately:

1. **Log into amazon.com directly** (type the URL or use your password manager) and change your Amazon password.
2. **Enable two-step verification** on your Amazon account if it is not already active. Go to Account, then Login & Security, then Two-Step Verification.
3. **Review recent orders and activity** for any unauthorized purchases. If you find any, report them through Amazon's Customer Service.
4. **Check your payment methods**: Go to Account, then Payment Options, and verify that no unauthorized cards or bank accounts have been added.
5. **Contact your bank**: If you entered credit card details on a phishing site, call your card issuer to report the compromise and request a replacement card.
6. **Check other accounts**: If you used the same password elsewhere, change those passwords immediately using a password manager.
7. **Tell Amazon what happened**: On the [Report a scam](https://www.amazon.com/gp/help/customer/display.html?nodeId=GRGRY7AQ3LMPXVCV) page, choose the option that matches what you shared -- Amazon account information, banking information, remote access to your computer, or other information -- to get Amazon's next steps for that situation.
8. **Report it and get a recovery plan**: Report the scam to the FTC at ReportFraud.ftc.gov. If you gave away your Social Security, credit card, or bank account number, the FTC directs you to [IdentityTheft.gov](https://www.identitytheft.gov/) for step-by-step recovery. See our full guide on [how to report a phishing attempt](/phishing/report-phishing/).

## Staying Ahead of Amazon Phishing in 2026

Amazon phishing campaigns evolve constantly. Prime Day, Prime Big Deal Days, and the holiday season each bring a wave of phishing tailored to the event. AI-generated phishing emails now arrive with flawless grammar, personalized order details pulled from previous data breaches, and branding that is indistinguishable from the real thing. The old advice to "look for spelling errors" no longer applies.

What works is a layered defense:

- **Use a password manager** that checks domains automatically and refuses to autofill on fake sites.
- **Check Amazon's Message Center** to verify whether any email is genuine, or forward it to verify@amazon.com and let Amazon tell you.
- **Never click links** in emails or texts claiming to be from Amazon. Open the app or type amazon.com directly.
- **Enable two-step verification** on your Amazon account.
- **Report every phishing attempt** to reportascam@amazon.com to help protect others.
- **Verify independently** through the Amazon app or website for any claims made in an email.

The attackers are counting on a moment of panic -- the instant you see "unauthorized purchase of $2,449.99" and click before thinking. The best countermeasure is building habits that remove panic from the equation: let your password manager handle the domain verification, go directly to the source for every alert, and treat every unsolicited message about your Amazon account with healthy skepticism.

## Related Articles

- [How to Recognize a Phishing Email: 10 Red Flags](/phishing/recognize-phishing/)
- [Fake Login Pages: How Phishing Sites Steal Credentials](/phishing/fake-login-pages/)
- [What Is Smishing? How to Spot SMS Phishing](/phishing/smishing/)
- [How to Verify Suspicious Messages](/phishing/verify-suspicious-messages/)
- [How a Password Manager Protects From Phishing](/phishing/password-manager-prevents-phishing/)
- [How to Report a Phishing Attempt](/phishing/report-phishing/)
