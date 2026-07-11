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
