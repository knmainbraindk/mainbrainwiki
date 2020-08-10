---
title: "Configure message delivery restrictions for a mailbox"
zid: "KB-2007091348"
tags:
- "#office365"
- "#powershell"
- "#mail"
---


# 
#### [docs.microsoft.com](https://docs.microsoft.com/en-us/exchange/recipients/user-mailboxes/message-delivery-restrictions)

*   7/7/2020
*   4 minutes to read


You can use the EAC or the Exchange Management Shell to place restrictions on whether messages are delivered to individual recipients. Message delivery restrictions are useful to control who can send messages to users in your organization. For example, you can configure a mailbox to accept or reject messages sent by specific users or to accept messages only from users in your Exchange organization.

The message delivery restrictions covered in this topic apply to all recipient types. To learn more about the different recipient types, see [Recipients](../recipients?view=exchserver-2019).

For additional management tasks related to recipients, see the following topics:

What do you need to know before you begin?
------------------------------------------

*   Estimated time to complete: 5 minutes.
    
*   You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipient Provisioning Permissions" section in the [Recipients Permissions](../../permissions/feature-permissions/recipient-permissions?view=exchserver-2019) topic.
    
*   For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](../../about-documentation/exchange-admin-center-keyboard-shortcuts?view=exchserver-2019).
    

Use the EAC to place message delivery restrictions
--------------------------------------------------

1.  In the EAC, navigate to **Recipients** > **Mailboxes**.
    
2.  In the list of user mailboxes, click the mailbox that you want to set up message delivery restrictions for, and then click **Edit** ![Edit icon](../../exchangeserver/media/itpro_eac_editicon.png?view=exchserver-2019).
    
3.  On the mailbox properties page, click **Mailbox Features**.
    
4.  Under **Message Delivery Restrictions**, click **View details** to view and change the following delivery restrictions:
    
    *   **Accept messages from**: Use this section to specify who can send messages to this user.
        
    *   **All senders**: This option specifies that the user can accept messages from all senders. This includes both senders in your Exchange organization and external senders. This is the default option. It includes external users only if you clear the **Require that all senders are authenticated** check box. If you select this check box, messages from external users will be rejected.
        
    *   **Only senders in the following list**: This option specifies that the user can accept messages only from a specified set of senders in your Exchange organization. Click **Add** ![Add icon](../../exchangeserver/media/itpro_eac_addicon.png?view=exchserver-2019) to display a list of all recipients in your Exchange organization. Select the recipients you want, add them to the list, and then click **OK**. You can also search for a specific recipient by typing the recipient's name in the search box and then clicking **Search** ![Search icon](../../exchangeserver/media/itpro_eac_.png?view=exchserver-2019).
        
    *   **Require that all senders are authenticated**: This option prevents anonymous users from sending messages to the user. This includes external users that are outside of your Exchange organization.
        
    *   **Reject messages from**: Use this section to block people from sending messages to this user.
        
    *   **No senders**: This option specifies that the mailbox won't reject messages from any senders in the Exchange organization. This is the default option.
        
    *   **Senders in the following list**: This option specifies that the mailbox will reject messages from a specified set of senders in your Exchange organization. Click **Add** ![Add icon](../../exchangeserver/media/itpro_eac_addicon.png?view=exchserver-2019) to display a list of all recipients in your Exchange organization. Select the recipients you want, add them to the list, and then click **OK**. You can also search for a specific recipient by typing the recipient's name in the search box and then clicking **Search** ![Search icon](../../exchangeserver/media/itpro_eac_.png?view=exchserver-2019).
        
5.  Click **OK** to close the **Message Delivery Restrictions** page, and then click **Save** to save your changes.
    

Use the Exchange Management Shell to place message delivery restrictions
------------------------------------------------------------------------

The following examples show how to use the Exchange Management Shell to configure message delivery restrictions for a mailbox. For other recipient types, use the corresponding **Set-** cmdlet with the same parameters.

This example configures the mailbox of Robin Wood to accept messages only from the users Lori Penor, Jeff Phillips, and members of the distribution group Legal Team 1.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"
    

Note

If you're configuring a mailbox to accept messages only from individual senders, you have to use the _AcceptMessagesOnlyFrom_ parameter. If you're setting up a mailbox to accept messages only from senders that are members of a specific distribution group, use the _AcceptMessagesOnlyFromDLMembers_ parameter.

This example adds the user named David Pelton to the list of users whose messages will be accepted by the mailbox of Robin Wood.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}
    

This example configures the mailbox of Robin Wood to require all senders to be authenticated. This means the mailbox will only accept messages sent by other users in your Exchange organization.

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true
    

This example configures the mailbox of Robin Wood to reject messages from the users Joe Healy, Terry Adams, and members of the distribution group Legal Team 2.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"
    

This example configures the mailbox of Robin Wood to also reject messages sent by members of the group Legal Team 3.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}
    

Note

If you're setting up a mailbox to reject messages from individual senders, you have to use the _RejectMessagesFrom_ parameter. If you're setting up a mailbox to reject messages from senders that are members of a specific distribution group, use the _RejectMessagesFromDLMembers_ parameter.

For detailed syntax and parameter information related to placing delivery restrictions for different types of recipients, see the following topics:

How do you know this worked?
----------------------------

To verify that you've successfully placed message delivery restrictions for a user mailbox, do one the following:

1.  In the EAC, navigate to **Recipients** > **Mailboxes**.
    
2.  In the list of user mailboxes, click the mailbox that you want to verify the message delivery restrictions for, and then click **Edit** ![Edit icon](../../exchangeserver/media/itpro_eac_editicon.png?view=exchserver-2019).
    
3.  On the mailbox properties page, click **Mailbox Features**.
    
4.  Under **Message Delivery Restrictions**, click **View details** to verify the delivery restrictions for the mailbox.
    

Or

Run the following command in the Exchange Management Shell.

    Get-Mailbox <identity> | Format-List AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

---

Clipped on Thursday, July 9, 2020, 1:47 PM