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

![Drive Mapping GPO](img/Drive_Mapping_GPO.png)

In the Windows Server 2022 VM, I open **Group Policy Management** and navigate to the **Accounting** Organizational Unit (OU) that was created in a previous lab. I right-click the Accounting OU and select **Create a GPO in this domain, and Link it here...**. I name the new Group Policy Object **Lab 07 Accounting Drive Mapping**.

After creating the GPO, I verify that it is linked to the **Accounting** OU and that the link is enabled. Linking the GPO to the OU allows its user-based settings to be processed for applicable users within the Accounting OU.

This GPO will be used to automatically map the Accounting network share that was configured in the previous lab, removing the need to manually map the network drive for each user.

### *Step 3 - Configure and Apply the Accounting Drive Mapping*

![Mapped_Drive_Config](img/Mapped_Drive_Config.png)

![Drive_Mapped_Confirmed](img/Drive_Mapped_Confirmed.png)

In the Windows Server 2022 VM, I edit the **Lab 07 Accounting Drive Mapping** Group Policy Object and navigate to **User Configuration > Preferences > Windows Settings > Drive Maps**. I create a new mapped drive and configure the location as `\\CA-DC-01\Accounting`, set the drive letter to `Z:`, and label the drive **Accounting**. I use the **Update** action so the drive can be created if it does not already exist and updated if the configuration changes later.

After saving the configuration, I switch to the Windows 11 VM and run `gpupdate /force` to immediately refresh Group Policy. I then sign out and back into the domain account so the updated user policy can be processed.

After signing back in, I open **File Explorer > This PC** and verify that **Accounting (Z:)** appears automatically under Network locations. This confirms that the Accounting network share is being deployed through Group Policy rather than being manually mapped on the workstation.

Using Group Policy to deploy mapped drives allows administrators to centrally provide users with access to shared network resources without configuring each workstation individually. If the share path or drive configuration needs to be changed later, the administrator can update the Group Policy instead of manually changing every user's computer.

### *Step 4 - Configure Item-Level Targeting*

![Item_Level_Targeting](img/Item_Level_Targeting.png)

In the Windows Server 2022 VM, I edit the **Lab 07 Accounting Drive Mapping** Group Policy Object and navigate to **User Configuration > Preferences > Windows Settings > Drive Maps**. I open the properties for the existing **Accounting (Z:)** drive mapping and select the **Common** tab.

I enable **Item-level targeting** and open the **Targeting Editor**. I then create a new **Security Group** condition and select the **LAB\Accounting Users** security group. I configure the condition so that the drive mapping only applies when the logged-in user is a member of the Accounting Users group.

Item-Level Targeting allows administrators to apply a Group Policy Preference only when specific conditions are met. In this lab, it ensures that the Accounting network drive is automatically mapped only for authorized users who belong to the **Accounting Users** security group.

This provides more precise control than relying only on the Organizational Unit where the GPO is linked, because users within the same OU can receive different settings depending on their group membership.

### *Step 5 - Test Group-Based Drive Mapping*

## **Challenges**

## **What I Learned**
