---
title: "How to Manage Client Passwords as a Developer"
description: "A framework for developers and technical freelancers to handle client credentials responsibly. Separation, rotation, handoffs, and security practices."
date: 2026-02-14
lastmod: 2026-02-14
draft: false
silo: "Business & Freelancers"
---

Developers and technical freelancers handle some of the most sensitive credentials that exist in any business context. Database root passwords, cloud infrastructure access keys, deployment tokens, server SSH keys, API secrets, payment gateway credentials -- these are not just logins to web services. They are the keys to systems that, if compromised, can expose customer data, drain financial accounts, or take down entire applications. This guide is part of our [Password Management for Business & Freelancers](/business/) series, and it provides a practical framework for managing client credentials with the care they demand.

## The Developer's Credential Landscape

A typical client engagement might involve access to:

- **Infrastructure**: AWS, Google Cloud, Azure, DigitalOcean, or bare-metal server credentials
- **Databases**: MySQL, PostgreSQL, MongoDB connection strings with authentication
- **Deployment**: CI/CD pipelines, GitHub/GitLab deploy keys, container registries
- **Third-party services**: Stripe, Twilio, SendGrid, Mailgun, and other API-based services
- **CMS and admin panels**: WordPress admin, Shopify admin, custom admin dashboards
- **DNS and domains**: Cloudflare, Route 53, domain registrar accounts
- **Monitoring**: Datadog, New Relic, Sentry, or other observability platforms
- **Email and communication**: Client email accounts, Slack workspaces

Each of these credentials carries different levels of risk and requires different handling. A Slack workspace invitation is qualitatively different from a production database password, and your security practices should reflect that distinction.

## The Cardinal Rules

Before getting into specific practices, four principles should govern every decision about client credentials.

### 1. Minimum Necessary Access

Request only the access you need for the work you are doing. If you are building a front-end feature, you do not need database admin credentials. If you are fixing a CSS issue, you do not need the AWS root account. Clients sometimes offer broad access because it is easier than figuring out the right granular permissions -- push back gently and request only what you need.

This protects both you and the client. If a credential you hold is compromised, the blast radius is limited to the scope of access you were given. It also protects you professionally -- if something goes wrong with a system you had no business accessing, you do not want to be on the list of people who had credentials.

### 2. Never Store Client Credentials Alongside Personal Ones

Client credentials must be isolated from your personal password vault. A breach of your personal accounts should never expose client infrastructure. With PanicVault and the [KeePass format](/keepass/), this is straightforward: create a separate .kdbx database for each client, or at minimum a single "client work" database that is distinct from your personal vault.

### 3. Credential Lifecycle Management

Every client credential has a lifecycle: receive, use, and return or destroy. Plan for all three stages at the beginning of the engagement, not when the project is already over and you are trying to figure out what credentials you still have.

### 4. Assume You Will Be Audited

Behave as though a client will one day ask you to account for every credential you accessed, when you accessed it, and whether you still have it. Some clients actually do this. Even those who do not will appreciate a developer who can provide this information if asked.

## Receiving Client Credentials

How credentials arrive matters. Insecure transmission is one of the most common vulnerabilities in the freelance developer workflow.

### Redirect Insecure Sharing

Clients will attempt to send credentials through the most convenient channel available: email, Slack DM, or -- alarmingly -- in a shared Google Doc. Your job is to redirect them toward secure alternatives without making the process so burdensome that they resent the extra steps.

**Acceptable methods:**
- In-person or over a phone call (for credentials that can be communicated verbally)
- Self-destructing encrypted messages (one-time links that expire after viewing)
- A shared KeePass database file with the password communicated through a separate channel
- The service's own invitation/access management system (IAM roles, team invitations, etc.)

**Unacceptable methods:**
- Email (plaintext, persists indefinitely, may be backed up in multiple locations)
- Slack, Discord, or Teams messages (persist in channel history, searchable)
- Text messages (stored on carrier servers, vulnerable to SIM swapping)
- Shared documents (Google Docs, Notion pages, etc.)
- Code repositories (never commit credentials -- this is a separate but related concern)

### Prefer Delegated Access Over Shared Credentials

Whenever possible, ask the client to create a separate account for you within each service rather than sharing their own credentials. This approach:

- Creates an audit trail of your specific actions
- Allows the client to revoke your access independently
- Prevents you from having the same level of access as the business owner
- Eliminates the need to share a credential at all

Most cloud platforms (AWS, GCP, Azure), SaaS tools, and CMS platforms support multiple user accounts with granular permissions. Push for this approach as your default.

For services that only support a single login (some legacy systems, certain social media accounts), shared credentials are unavoidable. In these cases, the secure sharing methods above apply.

## Storing Client Credentials

### Database Per Client

The most secure approach is maintaining a separate .kdbx database for each client. Each database:

- Has its own master password (distinct from your personal vault password)
- Contains only that client's credentials
- Can be synced via [iCloud Drive or other cloud storage](/cloud-sync/) independently
- Can be handed over to the client in its entirety at the end of the engagement
- Can be deleted cleanly when the engagement concludes

The overhead of managing multiple databases is minimal with PanicVault and [compatible apps](/keepass/compatible-apps/). You open the relevant client database when you are working on that client's project and close it when you are done.

### Organization Within Client Databases

Structure each client database to reflect the project architecture:

**Production**
- Infrastructure (cloud platform credentials)
- Database (connection strings, admin passwords)
- Third-party services (API keys, webhook secrets)
- Application admin (CMS, dashboards)

**Staging / Development**
- Mirror of production structure with staging credentials

**Project Management**
- Communication (Slack, email)
- Ticketing (Jira, Linear, GitHub Issues)
- Documentation (Confluence, Notion)

**DNS & Domains**
- Registrar access
- CDN / DNS management

### What Not to Store

Some credentials should not be in your password manager at all:

- **AWS root account credentials** -- if the client gives you root access, ask for an IAM user instead
- **Credentials you do not actively need** -- if a project phase is complete and you no longer need staging server access, remove those credentials and ask the client to revoke the access
- **Credentials for systems outside your scope** -- if the client shares their personal email password "just in case," decline and explain why

## Using Client Credentials Safely

### Environment Variables and Secrets Management

Never hardcode client credentials in source code. This is a fundamental development practice, but it bears repeating because violations are still disturbingly common. Use environment variables, secrets management services (AWS Secrets Manager, HashiCorp Vault), or .env files that are gitignored.

Your password manager is for storing the master copies of credentials. When you need a credential in a development context, copy it from your password manager into the appropriate environment configuration. Never commit the configuration files that contain real credentials.

### Credential Rotation

For long-running client engagements, rotate credentials periodically -- especially database passwords, API keys, and access tokens. Discuss a rotation schedule with the client at the start of the engagement. Quarterly rotation is reasonable for most contexts; monthly for highly sensitive systems.

When rotating credentials:

1. Generate a new credential in your password manager
2. Update the credential in the service
3. Update any configuration files or environment variables
4. Verify that systems work with the new credential
5. Update the credential in the shared database (if applicable)
6. Confirm that the old credential is no longer valid

### Multi-Factor Authentication

Enable [two-factor authentication](/two-factor-authentication/) on every client service that supports it, using the client's preferred 2FA method. If the client does not have a preference, use an authenticator app. Store the TOTP secret in your password manager alongside the credential.

For shared accounts where multiple people need 2FA access, the TOTP secret in a shared KeePass database ensures everyone can generate valid codes. This is one of the practical advantages of PanicVault's TOTP support -- the second factor travels with the shared credential.

## Ending an Engagement

The end of a client engagement is one of the highest-risk moments for credential security. Without a clear process, credentials linger in your vault indefinitely -- a liability for both you and the client.

### The Handoff Protocol

1. **Inventory**: List every credential you hold for the client. Review your client database, your email for any credentials that were sent but not yet moved to the vault, and your development environments for .env files.

2. **Rotate**: Change every password you created or modified during the engagement to a new value. This ensures the client has fresh credentials that you do not retain in your memory or in old database backups.

3. **Transfer**: Provide the updated credentials to the client through a secure channel. If you maintained a per-client KeePass database, you can share the entire .kdbx file with the master password communicated separately.

4. **Verify**: Confirm with the client that they can access every account with the new credentials.

5. **Revoke**: Ask the client to remove your individual accounts from their services (IAM users, team member invitations, etc.).

6. **Destroy**: Delete the client's credentials from your vault. If you maintained a per-client database, securely delete the .kdbx file. Remember that [cloud sync](/cloud-sync/) may retain copies -- delete from iCloud Drive or your sync service as well.

7. **Document**: Send the client a brief confirmation that all credentials have been transferred, all access has been revoked on your end, and you no longer hold any of their credentials.

For a more detailed walkthrough, see our guide on [secure credential handoffs for contractors](/business/contractor-handoffs/).

### What to Keep After an Engagement

Keep your own records of:

- Which services you had access to (for professional documentation, not the credentials themselves)
- When access was transferred and revoked
- Confirmation from the client that the handoff was completed

Do not keep:

- Any client credentials
- Copies of client databases
- SSH keys for client servers
- API keys for client services

## Handling Security Incidents

If you discover or suspect that a client credential has been compromised -- whether through a breach notification, suspicious activity, or your own error -- act immediately:

1. **Change the credential** if you have the ability to do so
2. **Notify the client** immediately, even if it is embarrassing
3. **Document what happened** -- when you discovered it, what the potential exposure was, what actions you took
4. **Assess the blast radius** -- what systems could be accessed with the compromised credential?
5. **Rotate related credentials** -- if a database password was compromised, also rotate any API keys or service accounts that connect to that database

Transparency with the client is critical. Trying to cover up a potential breach is both unethical and, in many jurisdictions, illegal. Clients will respect prompt, honest disclosure far more than they would react to a discovered cover-up.

## Tools and Workflow

The practical workflow for a developer using PanicVault to manage client credentials:

1. **Start of engagement**: Create a new .kdbx database for the client in PanicVault
2. **Receiving credentials**: Add them to the client database immediately. If received via an insecure channel, change the password and store the new one
3. **Daily work**: Open the client database when working on the project. Use autofill or copy-paste for credentials. Close when done.
4. **Sharing with team members**: If other developers need the same credentials, share the .kdbx file through [secure methods](/business/small-team-sharing/)
5. **End of engagement**: Follow the handoff protocol above
6. **Post-engagement**: Securely delete the client database

This workflow adds minimal friction to your development process while providing robust security and clean accountability.

## Professional Standards

Managing client credentials responsibly is not just a technical concern -- it is a professional one. Clients entrust you with the keys to their business infrastructure. How you handle that trust reflects on your professionalism and directly affects whether clients feel confident working with you.

Many freelance developers include credential handling practices in their contracts. Consider adding a clause that covers:

- How credentials will be received and stored
- Who on your team will have access
- What happens to credentials at the end of the engagement
- Your obligations in the event of a suspected breach
- Your use of encrypted storage (specifying the format and standards)

This level of transparency builds trust and sets clear expectations before the first credential is shared.

## Related Articles

- [Secure Credential Handoffs for Contractors](/business/contractor-handoffs/)
- [Password Management for Freelancers](/business/freelancers/)
- [Secure Password Sharing for Small Teams](/business/small-team-sharing/)
- [Password Compliance: HIPAA, PCI DSS for Small Business](/business/compliance/)
- [KeePass Encryption Explained](/keepass/encryption-explained/)
