
## Create a shared Folder between Host OS and Guest OS ( Virtual Box)

How to create a shared folder between host Operating System and Guest Operating system?

This is the scenario that you run Windows as your host operating system and Ubuntu in a VirtualBox, and that you want to access a specific Windows folder from Ubuntu.
In short-
Share a folder between Host OS-> Windows and Guest OS ->Ubuntu(Virtual box)

Step 1
Install install Guest Additions from VirtualBox’s menu go to Devices->Install Guest Additions
This will mount a virtual CD on your /media/cdrom. As root user Open this /media/cdrom added folder using Open with terminal option(Right click with mouse).

Step 2
Run the program VBoxLinuxAdditions.run. When the program completes reboot your VirtualBox.

$ sudo ./VBoxLinuxAdditions.run
Step 3
Create a shared folder. From Virtual menu go to Devices->Shared Folders then add a new folder in the list, this folder should be the one in windows which you want to share with Ubuntu(Guest OS).
Make this created folder auto-mount.
Example -> Make a folder on Desktop with name Ubuntushare and add this folder.



Step 4
When done with you shared folder(s) specification, we mount folder from Ubuntu(Guest OS).
Create a mountpoint, this a directory in Ubuntu that will share files with the shared folder from Windows.
Run this to create a directory in Ubuntu

$ sudo mkdir ~/Desktop/windowsshare
Step 5
With your mountpoint created you can now mount the shared folder.
Run this command to share the folder:

$ sudo mount -t vboxsf Ubuntushare ~/Desktop/windowsshare
Ubuntushare is the name of folder we add in VirtualBox Devices section this folder is in Windows(Host OS).
~/Desktop/windowsshare is the directory in Ubuntu(Guest OS)
