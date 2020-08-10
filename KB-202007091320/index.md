---
title: "Enable or Disable Password Expiration for Local Accounts in Windows 10"
zid: "KB-2007091320"
tags:
- Windows 10
- password
- expire
---


#  | Tutorials
#### [www.tenforums.com](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html?s=9ce49b828abd0bf5e5f76bea490bbc63)

>   
> 
> **How to Enable or Disable Password Expiration for Local Accounts in Windows 10**
> 
>   
> 
> Password expiration is a feature in Windows that forces a [**local account**](https://www.tenforums.com/tutorials/5387-how-tell-if-local-account-microsoft-account-windows-10-a.html) on the PC to change their passwords when a specified [**maximum**](https://www.tenforums.com/tutorials/87386-change-maximum-minimum-password-age-local-accounts-windows-10-a.html) (42 days by default) and [**minimum**](https://www.tenforums.com/tutorials/87386-change-maximum-minimum-password-age-local-accounts-windows-10-a.html) ( 0 days by default) password age has been reached.
> 
> This tutorial will show you how to enable or disable **password expiration** for specific local accounts in **Windows 10**.
> 
> You must be signed in as an [**administrator**](https://www.tenforums.com/tutorials/21680-determine-account-type-windows-10-a.html) to enable or disable password expiration.
> 
>   
> **CONTENTS:**  
> 
> *   [**Option One:**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option1) To Enable or Disable Password Expiration for Local Account(s) using Local Users and Groups
> *   [**Option Two:**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option2) To Enable or Disable Password Expiration for Local Account(s) using Command Prompt
> 
> **EXAMPLE: "Your password has expired and must be changed" at sign-in**
> 
>   
> ![Enable or Disable Password Expiration for Local Accounts in Windows 10-password_expiration_at_sign-1.jpg](https://www.tenforums.com/attachments/tutorials/140791d1498233851-enable-disable-password-expiration-local-accounts-windows-10-a-password_expiration_at_sign-1.jpg?s=9ce49b828abd0bf5e5f76bea490bbc63) ![Enable or Disable Password Expiration for Local Accounts in Windows 10-password_expiration_at_sign-2.jpg](https://www.tenforums.com/attachments/tutorials/140792d1498233851-enable-disable-password-expiration-local-accounts-windows-10-a-password_expiration_at_sign-2.jpg?s=9ce49b828abd0bf5e5f76bea490bbc63)  
> ![Enable or Disable Password Expiration for Local Accounts in Windows 10-password_expiration_at_sign-3.jpg](https://www.tenforums.com/attachments/tutorials/140793d1498233851-enable-disable-password-expiration-local-accounts-windows-10-a-password_expiration_at_sign-3.jpg?s=9ce49b828abd0bf5e5f76bea490bbc63) ![Enable or Disable Password Expiration for Local Accounts in Windows 10-password_expiration_at_sign-4.jpg](https://www.tenforums.com/attachments/tutorials/140794d1498233851-enable-disable-password-expiration-local-accounts-windows-10-a-password_expiration_at_sign-4.jpg?s=9ce49b828abd0bf5e5f76bea490bbc63)  
> 
> ![Note](https://www.tenforums.com/images/notesmall10.png)   Note
> 
> Local Users and Groups is only available in the **Windows 10 Pro**, **Enterprise**, and **Education** [**editions**](https://www.tenforums.com/tutorials/22749-see-windows-10-edition-you-have-installed.html).
> 
> All editions can use [**Option Two**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option2) below.
> 
>   
> **1.** Press the **Win+R** keys to open Run, type **lusrmgr.msc** into Run, and click/tap on **OK** to open Local Users and Groups.
> 
> **2.** Click/tap on **Users** in the left pane of Local Users and Groups. (see screenshot below step 3)
> 
> **3.** Right click or press and hold on the **name** (ex: "Brink2") of the [**local account**](https://www.tenforums.com/tutorials/5387-how-tell-if-local-account-microsoft-account-windows-10-a.html) you want, and click/tap on **Properties**. (see screenshot below)
> 
>   
> ![Enable or Disable Password Expiration for Local Accounts in Windows 10-password_expiration_lusrmgr-1.jpg](https://www.tenforums.com/attachments/tutorials/140795d1498070386-enable-disable-password-expiration-local-accounts-windows-10-a-password_expiration_lusrmgr-1.jpg?s=9ce49b828abd0bf5e5f76bea490bbc63)
> 
>   
> **4.** Do [**step 5**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option1s5) (enable) or [**step 6**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option1s6) (disable) below for what you want to do.
> 
>   
> A) In the **General** tab, uncheck the **Password never expires** box, and click/tap on **OK**. (see screenshot below)  
> 
> ![Note](https://www.tenforums.com/images/notesmall10.png)   Note
> 
> **Password never expires** will be grayed out if the **User must change password at next logon** box is checked.
> 
>   
> B) If you like, you can change the [**maximum and minimum password age**](https://www.tenforums.com/tutorials/87386-change-maximum-minimum-password-age-local-accounts-windows-10-a.html) for local accounts.
> 
> C) When finished, go to [**step 7**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option1s7) below.
> 
> ![Enable or Disable Password Expiration for Local Accounts in Windows 10-password_expiration_lusrmgr-3.png](https://www.tenforums.com/attachments/tutorials/140797d1498233861-enable-disable-password-expiration-local-accounts-windows-10-a-password_expiration_lusrmgr-3.png?s=9ce49b828abd0bf5e5f76bea490bbc63)
> 
>   
> 
> ![Note](https://www.tenforums.com/images/notesmall10.png)   Note
> 
> This is the default setting.
> 
>   
> A) In the **General** tab, check the **Password never expires** box, click/tap on **OK**, and go to [**step 7**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option1s7) below. (see screenshot below)  
> 
> ![Note](https://www.tenforums.com/images/notesmall10.png)   Note
> 
> **Password never expires** will be grayed out if the **User must change password at next logon** box is checked.
> 
>   
> ![Enable or Disable Password Expiration for Local Accounts in Windows 10-password_expiration_lusrmgr-2.png](https://www.tenforums.com/attachments/tutorials/140796d1498233861-enable-disable-password-expiration-local-accounts-windows-10-a-password_expiration_lusrmgr-2.png?s=9ce49b828abd0bf5e5f76bea490bbc63)
> 
>   
> **7.** Repeat [**step 3**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option1s3) above if you would like to enable or disable password expiration for another local account.
> 
> **8.** When finished, you can close Local Users and Groups if you like.
> 
>   
> **1.** Open an **[elevated command prompt](https://www.tenforums.com/tutorials/2790-open-elevated-command-prompt-windows-10-a.html)**.
> 
> **2.** Do [**step 3**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option2s3) (enable) or [**step 4**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option2s4) (disable) below for what you want to do.
> 
> A) Enter the command below into the elevated command prompt, and press Enter. (see screenshot below)
> 
> ![](https://www.tenforums.com/images/smilies/smarrow.png) `wmic UserAccount where Name="user name" set PasswordExpires=True`
> 
> ![Note](https://www.tenforums.com/images/notesmall10.png)   Note
> 
> Substitute **user name** in the command above with the actual user name of the [**local account**](https://www.tenforums.com/tutorials/5387-how-tell-if-local-account-microsoft-account-windows-10-a.html) you want to enable password expiration.
> 
>   
> B) If you like, you can change the [**maximum and minimum password age**](https://www.tenforums.com/tutorials/87386-change-maximum-minimum-password-age-local-accounts-windows-10-a.html) for local accounts.
> 
> C) When finished, go to [**step 5**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option2s5) below.
> 
> ![Enable or Disable Password Expiration for Local Accounts in Windows 10-enable_password_expiration_command.jpg](https://www.tenforums.com/attachments/tutorials/140799d1498233861-enable-disable-password-expiration-local-accounts-windows-10-a-enable_password_expiration_command.jpg?s=9ce49b828abd0bf5e5f76bea490bbc63)
> 
>   
> 
> ![Note](https://www.tenforums.com/images/notesmall10.png)   Note
> 
> This is the default setting.
> 
>   
> A) Enter the command you want below into the elevated command prompt, press Enter, and go to [**step 5**](https://www.tenforums.com/tutorials/87379-enable-disable-password-expiration-local-accounts-windows-10-a.html#option2s5) below. (see screenshot below) (Apply to all accounts)
> 
> ![](https://www.tenforums.com/images/smilies/smarrow.png) `wmic UserAccount set PasswordExpires=False`
> 
> OR (Apply to specific local account)
> 
> ![](https://www.tenforums.com/images/smilies/smarrow.png) `wmic UserAccount where Name="user name" set PasswordExpires=False`
> 
> ![Note](https://www.tenforums.com/images/notesmall10.png)   Note
> 
> Substitute **user name** in the command above with the actual user name of the [**local account**](https://www.tenforums.com/tutorials/5387-how-tell-if-local-account-microsoft-account-windows-10-a.html) you want to disable password expiration.
> 
>   
> ![Enable or Disable Password Expiration for Local Accounts in Windows 10-disable_password_expiration_command.jpg](https://www.tenforums.com/attachments/tutorials/140798d1498233861-enable-disable-password-expiration-local-accounts-windows-10-a-disable_password_expiration_command.jpg?s=9ce49b828abd0bf5e5f76bea490bbc63)
> 
> **5.** When finished, you can close the elevated command prompt if you like.
> 
> That's it, Shawn

  

  
 

Tutorial Categories

![Enable or Disable Password Expiration for Local Accounts in Windows 10](https://www.tenforums.com/img/tutcat2020b.png)

---

Clipped on Thursday, July 9, 2020, 1:19 PM