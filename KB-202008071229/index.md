---
title: Sync Any Folder to OneDrive in Windows 10
zid: KB-202008071229
category: kb
tags:
- #windows
- #onedrive
- #sync
---

![Sync Any Folder to OneDrive in Windows 10](https://www.tenforums.com/geek/gars/images/2/types/thumb_15755611680_ne_rive_folder.png "Sync Any Folder to OneDrive in Windows 10")

***How to Sync Any Folder to OneDrive in Windows 10***  
Published by Category: [Apps & Features](https://www.tenforums.com/tutorials/id-Apps_Features/)  
10 Jun 2020

source: [https://www.tenforums.com/tutorials/92892-sync-any-folder-onedrive-windows-10-a.html](https://www.tenforums.com/tutorials/92892-sync-any-folder-onedrive-windows-10-a.html)

>   
> **How to Sync Any Folder to OneDrive in Windows 10**
> 
> OneDrive is free online storage that comes included with Windows 10 and used with your [**Microsoft account**](https://www.tenforums.com/tutorials/5387-how-tell-if-local-account-microsoft-account-windows-10-a.html). Save your files to OneDrive, and you'll be able to get to them from any PC, tablet, or phone.
> 
> By default, you can [**choose which folders to sync in OneDrive with your PC**](https://www.tenforums.com/tutorials/2905-choose-folders-onedrive-selective-sync-windows-10-a.html). Windows 10 stores your **OneDrive** folder in your account's %UserProfile% folder (ex: "C:\\Users\\Brink") by default.
> 
> This tutorial will show you how to sync any folder to OneDrive that is not already in **OneDrive** for your account in **Windows 10**.
> 
> Thank you to our member [**cereberus**](https://www.tenforums.com/members/cereberus.html) for providing this idea.
> 
> **Here's How:**
> 
> 1 Open a [**command prompt**](https://www.tenforums.com/tutorials/3288-open-command-prompt-windows-10-a.html).
> 
> 2 Type the command below into the command prompt, and press Enter. (see screenshot below)
> 
> `mklink /j "%UserProfile%\OneDrive\Folder Name" "Full path of source folder"`
> 
> Substitute **Full path of source folder** in the command above with the actual full path of the folder (ex: "F:\\Example Folder") you want to sync with your OneDrive.
> 
> Substitute **Folder Name** in the command above with the folder name (ex: "Example Folder") you want to show in OneDrive. This folder is a junction point of the source folder. It would be best to use the same name as the source folder to help know what it's linked to. **This must be a new folder name that isn't already in your OneDrive folder.** This specified folder will be created in your OneDrive folder.
> 
> **For example:** `mklink /j "%UserProfile%\OneDrive\Example Folder" "F:\Example Folder"`
> 
> ![Sync Any Folder to OneDrive in Windows 10-mklink_onedrive_command.png](https://www.tenforums.com/attachments/tutorials/152158d1504714578-sync-any-folder-onedrive-windows-10-a-mklink_onedrive_command.png "Sync Any Folder to OneDrive in Windows 10-mklink_onedrive_command.png")
> 
>   
> 3 The source folder (ex: "F:\\Example Folder") will now be synced with your OneDrive (ex: "%UserProfile%\\OneDrive\\Example Folder"). Anything you **copy**, **save**, and **delete** in either of these two folders will also be applied to the other folder. (see screenshots below)
> 
> If you want to undo this junction point and stop syncing the source folder with your OneDrive, you would only delete the folder (ex: "%UserProfile%\\OneDrive\\Example Folder") in your OneDrive folder. This will not delete the source folder (ex: "F:\\Example Folder"), but will also delete it from your online OneDrive.
> 
>   
> **(Source folder location)**  
> ![Sync Any Folder to OneDrive in Windows 10-source_folder.jpg](https://www.tenforums.com/attachments/tutorials/152151d1504712839-sync-any-folder-onedrive-windows-10-a-source_folder.jpg "Sync Any Folder to OneDrive in Windows 10-source_folder.jpg")**(OneDrive locations)**  
> ![Sync Any Folder to OneDrive in Windows 10-onedrive_folder.jpg](https://www.tenforums.com/attachments/tutorials/152149d1504712839-sync-any-folder-onedrive-windows-10-a-onedrive_folder.jpg "Sync Any Folder to OneDrive in Windows 10-onedrive_folder.jpg") ![Sync Any Folder to OneDrive in Windows 10-junction_point_in_onedrive_folder.jpg](https://www.tenforums.com/attachments/tutorials/152148d1504712839-sync-any-folder-onedrive-windows-10-a-junction_point_in_onedrive_folder.jpg "Sync Any Folder to OneDrive in Windows 10-junction_point_in_onedrive_folder.jpg")  
> ![Sync Any Folder to OneDrive in Windows 10-online_onedrive.jpg](https://www.tenforums.com/attachments/tutorials/152150d1504712839-sync-any-folder-onedrive-windows-10-a-online_onedrive.jpg "Sync Any Folder to OneDrive in Windows 10-online_onedrive.jpg")
> 
> That's it,  
> Shawn

  
