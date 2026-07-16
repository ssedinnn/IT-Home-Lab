# *Lab 02 - Domain Client Deployment*

## *Objective*
The goal of this lab is to configure a Windows 11 client workstation and connect it to the Active Directory domain created in Lab 01. This includes installing VirtualBox Guest Additions for improved usability, creating Active Directory user accounts, configuring networking, joining the workstation to the domain, and verifiying domain authentication by logging in with a domain user.

## *Environment*
The following software was used:
- Oracle VirtualBox
- Windows Server 2022
- VirtualBox Guest Additions
- Windows 11
- Active Directory Domain Services (AD DS)

## *Skills Demonstrated*

## *Steps*

### *Step 1 - Install Guest Addition for VirtualBox*

![VirtualBox Guest Addition](img/VirtualBox_Guest_Addition.png)

After opening the Windows Server 2022 virtual machine, I install **VirtualBox Guest Additions** by selecting **Devices > Insert Guest Additions CD Image** from the VirtualBox menu. I then open File Explorer inside the Windows Server 2022 virtual machine, locate the mounted CD drive, and run **VBoxWindowsAdditions-amd64**. After completing the installation wizard, I restart the virtual machine to apply the changes.

Installing Guest Additions enables features such as file sharing, improved display support, and better integration between the host computer and the virtual machine. Since my Windows Server VM will use a static IP address and won't have internet access later in the lab, shared folders allow me to easily transfer software and other files from my host computer to the server whenever needed.

### *Step 2 - Add a New Shared Folder*

![Adding Shared Folder](img/Adding_Shared_Folder.png)

To configure a shared folder, I open the **Devices** menu in VirtualBox and navigate to **Shared Folders > Shared Folder Settings**. I then click the **Add Shared Folder** icon, select the folder on my host computer that I want to share with the virtual machine, and name it **IT_homelab**.

Finally, I enable **Auto-mount** and **Make Permanent** so the shared folder is automatically available each time the virtual machine starts.

### *Step 3 - Test Shared Folder*

![Mounted_Folder_Verification](img/Mounted_Folder_Verification.png)

To test the shared folder, I added an image to the folder on my host computer. The image also appeared in the shared folder on the Windows Server virtual machine, confirming that the shared folder was working correctly.

### *Step 4 - Creating Users in Active Directory*

![Creating Active Directory Account](img/Creating_Active_Directory_Account.png)

To create a domain user, I open **Active Directory Users and Computers** and navigate to the **lab.local** domain. I then right-click the **Users** folder and select **New > User**. For this lab, I fill in the user's first name, logon name, and password. Since this is a test account, I uncheck **"User must change password at next logon"** before completing the user creation wizard.

Active Directory provides a centralized way to manage user accounts and their settings. From here, administrators can reset passwords, configure logon hours, manage group memberships, update user information, and perform many other administrative tasks. Most user account management within a Windows domain is performed through **Active Directory Users and Computers**.

You can also use the **`net user <username> /domain`** command to view additional information about a domain user, such as password expiration, account status, and the last logon time. For example, running **`net user sedin /domain`** displays information for the user account named **sedin**.

### *Step 5 - Creating Windows 11 VM*

![Creating Windows 11 VM](img/Windows_11_VM_Setup.png)

I create a user profile for the Windows 11 virtual machine using the same process outlined in **Lab 01** for the Windows Server 2022 virtual machine. Since the setup is identical, I won't repeat each step here.

### *Step 6 - Setting up Windows 11*

I start up the VM and go through the Setup Wizard, I don't have a product key for it which is fine. Important thing to do is to ensure you click to install Windows 11 Pro instead of just Windows 11. Windows 11 Pro is needed as that has the feature of being able to join domains.

## *Challenges*
When setting up the windows 11 VM i didn't give it the correct system requirements of 2 cores, supporting TPM 2.0 and supporting secure boot. I fixed this by going into the settings of the VM and changing those respective settings to go through.
## *What I Learned*

## *Next Steps*
