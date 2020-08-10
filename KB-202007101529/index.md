---
title: "Office365 / Azure tenant security setup: MainBrain recommended defaults"
zid: "KB-2007101529"
tags:
    - "#Office365"
    - "#Azure"
    - "#security"
---

# Policies

## Anti-phishing

### Policy
Applied to
[alle kundens domæner]


### Impersonation
Users to protect Off: Ingen
Protect all domains I own: On
Protect specific domains: Off
Action > User impersonation Don't apply any action
Action > Domain impersonation Move message to the recipients' Junk Email folders
Safety tips > User impersonation: On
Safety tips > Domain impersonation: On
Safety tips > Unusual characters: On
Mailbox intelligence: On
Mailbox Intelligence > Protection: On
Mailbox Intelligence > Action: Move message to the recipients' Junk Email folders

### Spoofing
Enable antispoofing protection: On
Enable Unauthenticated Sender Feature: On
Action: Move message to the recipients' Junk Email folders

### Advanced settings
Advanced phishing thresholds: 1 - Standard

## Safe attachments
No dynamic delivery
Malware response: Block
Redirect attachment on detection: None
Applied to: All domains

## Safe Links
Rewrite URLS: On
URL check for Teams: On
Realtime scan of URL: On, postpone delivery
Safe links policy applies to internal mails: On
Do Not Track on safe links: Off
Allow click through safe link to original URL: Off
Exceptions: None
Apply to domains: All

## Anti-spam
### Outgoing spam policy:
External and internal hourly limit: 60
If exceeded, restrict user from sending mail until the following day
If sender is restricted, send notification to: mbadmin@domain
Applies to: All internal domains

### Default spam filter policy (always on)
Efterlades uændret

## DKIM opsætning
Foretages sammen med MX setup og efterfølges af DMARC-politik med indstilling om karantæne (v=DMARC1; p=quarantine)

## Antimalware:
Malware detection response: Quarantine, default notification
Attachment types filter: On, all file predefined types
Zero Hour Auto Purge: On
Notify internal senders: On
Notify admin on undelivered mail from internal senders: Yes, mbadmin@domain

# Access

## 1. Obligatorisk MFA for administratorer
Set up Azure Multi-Factor Authentication policies to protect devices and data that are accessible by your users with administrative roles

In the Azure portal Conditional Access page
1. Select + New Policy
2. Go to Assignments > Users and groups > Include > Select users and groups > check Directory roles
3. At a minimum, select the following roles:
Security administrator
Exchange service administrator
Global administrator
Conditional Access Administrator
SharePoint administrator
Helpdesk Administrator
Billing Administrator
User administrator
Authentication Administrator

4. Go to Cloud apps or actions > Cloud apps > Include > select All cloud apps (and don't exclude any apps)
5. Under Access controls > Grant > select Grant Access > check Require multi-factor authentication (and nothing else)
6. Enable policy > On
7. Create

## 2. Slå Password Hash sync til hvis hybrid
To use password hash synchronization in your organization, you need to install Azure AD Connect and configure directory synchronization between your on-premises Active Directory instance and your Azure Active Directory instance. The [Enable password hash synchronization](https://go.microsoft.com/fwlink/?linkid=2094925) documentation explains password hash synchronization and how to enable it.

## 3. MFA for alle brugere
In the Azure portal Conditional Access page
1. Select +New policy
2. Cloud apps > All cloud apps (and don't exclude any apps)
3. Conditions > Client apps > Configure (Yes)
4. Grant > Require multi-factor authentication (and nothing else)
5. Select only the following: Browser, Mobile apps and desktop clients, Modern authentication clients, Exchange ActiveSync clients, Other clients
6. Enable policy > On
7. Create

Optionally, if you have Azure AD Premium P2, you can set up an Azure Multi-Factor Authentication registration policy to help you manage the rollout of Azure MFA in your environment.
In the Azure portal, configure the MFA registration policy by going to the MFA registration page.
1. Under Assignments > Users - Choose All users or choose Select individuals and groups if limiting your rollout
2. Under Controls - Ensure the checkbox Require Azure MFA registration is checked and choose Select
3. Enforce policy > On
4. Save

Tilladte MFA-metoder: Kun app (notifikation eller bekræftelseskoder)

## 4. SSPR (Self Service Password Reset) for alle brugere
In the Password Reset Azure AD blade you can enable self-service password reset. On the properties page, select All or Selected to choose the users to apply your policy to. Configure your authentication methods for users to reset their passwords. On the Registration page, select Yes under "Require users to register when signing in" and set a number of days before users are asked to re-confirm their authentication information.

## 5. Opret ekstra-admin til reserve / nødstilfælde
F.eks. mbadmin-assist@contoso.com ?

## 6. Allow no more than 5 global administrators
Hvis der er behov for udvidet adgang, skal der i større grad forsøgt anvendt mindre omfattende administrator-roller

## 7. Sæt adgangskoder til ikke at udløbe
