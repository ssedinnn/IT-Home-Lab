# *Lab 01 - Building an Active Directory Environment*

## *Objective*
The goal of this lab is to build a basic Active Directory environment using Virtual Box, and Windows Server 2022

## *Environment*
The following software was used:
- Oracle VirtualBox
- Windows Server 2022 Evaluation ISO

## *Skills Demonstrated*
- Windows Server 2022 Administration
- Virtualization (VirtualBox)
- Active Directory Domain Services
- Domain Controller Deployment
- Server Configuration

## *Steps*

### *Step 1 - Create the Windows Server Virtual Machine*
![VM Configuration](img/Server_2022_Profile_Creation.png)

I created a new virtual machine in VirtualBox that will act as the domain controller for this lab

### *Step 2 - Configure Hardware*
![VM Configuration](img/VM_Config.png)

I allocated 8 GB of RAM and 2 virtual CPUs to the server. Active Directory itself is not particularly resource intensive, but providing additional memory leaves room for future services and expansion within the lab environment

### *Step 3 - Attach the Windows Server ISO*
![VM Configuration](img/Attaching_ISO.png)

I attached the Windows Server 2022 Evaluation ISO file that was downloaded before this lab began and selected “Mount and Retry Boot” to start the boot process.

### *Step 4 - Install Windows Server*
![VM Configuration](img/Windows_Server_Installation.png)

I selected Windows Server 2022 Desktop Experience because it includes a graphical user interface (GUI). The non Desktop Experience version installs Server Core, which is command-line only.

Since this is a new virtual machine, I selected Custom Installation because there was no existing operating system to upgrade.

For this home lab I installed Windows directly to the default virtual disk instead of creating multiple partitions. This keeps the lab simple while still allowing me to practice Active Directory administration.

### *Step 5 - Rename the Server*
![VM Configuration](img/Server_Name_Change.png)
