# *Lab 04 - Group Policy Management*

## *Objective*
Learn how Organizational Units (OUs) and Group Policy Objects (GPOs) work together to centrally manage user settings in an Active Directory environment.

## *Environment*
- Oracle VirtualBox
- Windows Server 2022
- Windows 11
- Active Directory Domain Services
- Group Policy Management Console (GPMC)

## *Skills Demonstrated*

## *Steps*

### *Step 1 - Create an Organizational Unit (OU)*

![Creating OU](img/OU_Creation.png)

In the Windows Server 2022 VM, I open **Active Directory Users and Computers**, right-click the `lab.local` domain, and select **New > Organizational Unit**. I then name the OU **Accounting**.

Organizational Units (OUs) are containers used to organize users, computers, and groups within Active Directory. They allow administrators to logically organize domain objects and apply Group Policies to specific users or computers without affecting the entire domain. In business environments, OUs are commonly used to separate departments such as Accounting, Human Resources, and IT, making administration and policy management more efficient.

### *Step 2 - Move the User into the OU*

![Move User to OU](img/Move_User_To_OU.png)

I move the test user created in the previous lab into the new Organizational Unit. 

Because Group Policies are linked to OUs, placing the user inside this OU allows any policies applied to it to automatically affect that user.

### *Step 3 - Create a Group Policy Object*

In the Windows Server 2022 VM, I open **Group Policy Management** from the Start menu. I then expand the `lab.local` domain until I locate the **Accounting** Organizational Unit (OU) created earlier. I right-click the OU and select **Create a GPO in this domain, and Link it here...**. I then give the Group Policy Object (GPO) a descriptive name. For this lab, I name it **Lab 04 User Policies**.

Group Policy Objects (GPOs) are collections of Windows settings that administrators use to centrally manage users and computers in an Active Directory domain. By linking a GPO to an Organizational Unit, the configured settings are automatically applied to the users or computers within that OU. This allows organizations to efficiently enforce security settings, standardize system configurations, and simplify administration across multiple devices.

## *Challenges*

## *What I Learned*

## *Next Steps*
