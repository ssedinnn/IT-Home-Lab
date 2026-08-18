# **Lab 07 - Deploying Network Drives with Group Policy**

## **Objective**

Learn how to use Group Policy to automatically deploy a mapped network drive to authorized domain users and verify the policy from a domain-joined Windows 11 workstation.

## **Environment**

- Oracle VirtualBox
- Windows Server 2022
- Windows 11
- Active Directory Domain Services (AD DS)
- Group Policy Management Console (GPMC)
- Active Directory Security Groups
- Windows File Sharing

## **Skills Demonstrated**

## **Steps**

### *Step 1 - Remove the Manually Mapped Network Drive*

![Network Drive Disconnected](img/Network_Drive_Disconnected.png)

In the Windows 11 VM, I open **File Explorer** and navigate to **This PC**. I locate the **Accounting (Z:)** network drive that was manually mapped in the previous lab, right-click it, and select **Disconnect**.

After disconnecting the drive, I verify that the **Accounting (Z:)** drive no longer appears under **This PC**. Removing the existing mapped drive ensures that I can verify later in the lab that the drive is being automatically deployed through Group Policy rather than remaining from the manual configuration completed in Lab 06.

### *Step 2 - Create the Drive Mapping GPO*

In the Windows Server 2022 VM, I open **Group Policy Management** and navigate to the **Accounting** Organizational Unit (OU) that was created in a previous lab. I right-click the Accounting OU and select **Create a GPO in this domain, and Link it here...**. I name the new Group Policy Object **Lab 07 Accounting Drive Mapping**.

After creating the GPO, I verify that it is linked to the **Accounting** OU and that the link is enabled. Linking the GPO to the OU allows its user-based settings to be processed for applicable users within the Accounting OU.

This GPO will be used to automatically map the Accounting network share that was configured in the previous lab, removing the need to manually map the network drive for each user.

## **Challenges**

## **What I Learned**
