# *Lab 02 - Domain Client Deployment*

## *Objective*
The goal of this lab is to configure a Windows 11 client workstation and connect it to the Active Directory domain created in Lab 01. This includes installing VirtualBox Guest Additions fro improved usability, creating Active Directory user accounts, configuring networking, joining the workstation to the domain, and verifiying domain authentication by logging in with a domain user.

## *Environment*
The following software was used:
- Oracle VirtualBox
- Windows Server 2022
- VirtualBox Guest Additions
- Windows 11
- Active Directory Domain Services (AD DS)

## *Skills Demonstrated*

## *Steps*

### *Step 1 - Install Guest Addition for VirtualBox

![VirtualBox Guest Addition](img/VirtualBox_Guest_Addition.png)

After creating the Windows Server 2022 virtual machine, I install **VirtualBox Guest Additions** by selecting **Devices > Insert Guest Additions CD Image** from the VirtualBox menu. I then open File Explorer, locate the mounted CD drive, and run **VBoxWindowsAdditions-amd64**. After completing the installation wizard, I restart the virtual machine to apply the changes.

Installing Guest Additions enables features such as file sharing, improved display support, and better integration between the host computer and the virtual machine. Since my Windows Server VM will use a static IP address and won't have internet access later in the lab, shared folders allow me to easily transfer software and other files from my host computer to the server whenever needed.


## *Challenges*

## *What I Learned*

## *Next Steps*
