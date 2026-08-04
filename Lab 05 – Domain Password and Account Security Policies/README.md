# *Lab 05 - Domain Password and Account Security Policies*

## *Objective*
Learn how to configure domain-wide security policies that protect user accounts and workstations by enforcing password requirements, account lockout settings, and automatic workstation locking.

## *Environment*
- Oracle VirtualBox
- Windows Server 2022
- Windows 11
- Active Directory Domain Services (AD DS)
- Group Policy Management

## *Skills Demonstrated*

## *Steps*

### *Step 1 - Open the Default Domain Policy*

![Default Group Policy](img/Default_Group_Policy.png)

In the Windows Server 2022 VM, I open **Group Policy Management**, expand the `lab.local` domain, right-click **Default Domain Policy**, and select **Edit**.

Unlike the Group Policy Object created in the previous lab, password and account lockout policies are configured through the **Default Domain Policy** because they apply to every user account in the Active Directory domain. Configuring these settings at the domain level ensures that all domain users follow the same security requirements.

## *Challenges*
- One of the key concepts in this lab was understanding the difference between **OU-linked Group Policy Objects** and the **Default Domain Policy**. Unlike the policies configured in the previous lab, password and account lockout settings must be configured through the Default Domain Policy because they are intended to apply consistently across the entire Active Directory domain.

## *What I Learned*

