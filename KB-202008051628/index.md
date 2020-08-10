---
title: "Remove blocked users from the Restricted Users portal - Office 365"
zid: KB-202008051628
category: kb
tags:
- #office365
- #spam
- #security
---

#### [docs.microsoft.com](https://docs.microsoft.com/en-us/microsoft-365/security/office-365-security/removing-user-from-restricted-users-portal-after-spam)

*   6/13/2020
*   3 minutes to read


If a user exceeds one of the outbound sending limits as specified in [the service limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#sending-limits-across-office-365-options) or in [outbound spam policies](configure-the-outbound-spam-policy?view=o365-worldwide), the user is restricted from sending email, but they can still receive email.

The user is added to the Restricted Users portal in the Security & Compliance Center. When they try to send email, the message is returned in a non-delivery report (also known as an NDR or bounce messages) with the error code [5.1.8](/en-us/Exchange/mail-flow-best-practices/non-delivery-reports-in-exchange-online/fix-error-code-5-1-8-in-exchange-online) and the following text:

> "Your message couldn't be delivered because you weren't recognized as a valid sender. The most common reason for this is that your email address is suspected of sending spam and it's no longer allowed to send email. Contact your email admin for assistance. Remote Server returned '550 5.1.8 Access denied, bad outbound sender."

Admins can remove users from the Restricted Senders portal in the Security & Compliance Center or in Exchange Online PowerShell.

What do you need to know before you begin?
------------------------------------------

1.  In the Security & Compliance Center, go to **Threat management** > **Review** > **Restricted users**.
    
2.  Find and select the user that you want to unblock. In the **Actions** column, click **Unblock**.
    
3.  A fly-out will go into the details about the account whose sending is restricted. You should go through the recommendations to ensure you're taking the proper actions in case the account is actually compromised. Click **Next** when done.
    
4.  The next screen has recommendations to help prevent future compromise. Enabling multi-factor authentication (MFA) and changing the passwords are a good defense. Click **Unblock user** when done.
    
5.  Click **Yes** to confirm the change.
    
    Note
    
    It may take 30 minutes or more before restrictions are removed.
    

Verify the alert settings for restricted users
----------------------------------------------

The default alert policy named **User restricted from sending email** will automatically notify admins when users are blocked from sending outbound mail. You can verify these settings and add additional users to notify. For more information about alert policies, see [Alert policies in the security and compliance center](../../compliance/alert-policies?view=o365-worldwide).

1.  In the Security & Compliance Center, go to **Alerts** > **Alert policies**.
    
2.  Find an select the **User restricted from sending email** alert.
    
3.  In the flyout that appears, verify or configure the following settings:
    
    *   **Status**: Verify the alert is turned on ![Toggle on](../../media/963dfcd0-1765-4306-bcce-c3008c4406b9.png?view=o365-worldwide).
        
    *   **Email recipients**: Click **Edit** and verify or configure the following settings in the **Edit recipients** flyout that appears:
        
        *   **Send email notifications**: Verify the check box is selected (**On**).
            
        *   **Email recipients**: The default value is **TenantAdmins** (meaning, **Global admin** members). To add more recipients, click in a blank area of the box. A list of recipients will appear, and you can start typing a name to filter and select a recipient. You can remove an existing recipient from the box by clicking ![Remove icon](../../media/scc-remove-icon.png?view=o365-worldwide) next to their name.
            
        *   **Daily notification limit**: The default value is **No limit** but you can select a limit for the maximum number of notifications per day.
            
        
        When you're finished, click **Save**.
        
4.  Back on the **User restricted from sending email** flyout, click **Close**.
    

Use Exchange Online PowerShell to view and remove users from the Restricted Users list
--------------------------------------------------------------------------------------

To view this list of users that are restricted from sending email, run the following command:

    Get-BlockedSenderAddress
    

To view details about a specific user, replace <emailaddress> with their email address and run the following command:

    Get-BlockedSenderAddress -SenderAddress <emailaddress>
    

For detailed syntax and parameter information, see [Get-BlockedSenderAddress](/en-us/powershell/module/exchange/get-blockedsenderaddress).

To remove a user from the Restricted Users list, replace <emailaddress> with their email address and run the following command:

    Remove-BlockedSenderAddress -SenderAddress <emailaddress>
    

For detailed syntax and parameter information, see [Remove-BlockedSenderAddress](/en-us/powershell/module/exchange/remove-blockedsenderaddress).

Submit and view feedback for

---

Clipped on Wednesday, August 5, 2020, 2:43 PM