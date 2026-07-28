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

I move the test user created in the previous lab into the new Organizational Unit. 

Because Group Policies are linked to OUs, placing the user inside this OU allows any policies applied to it to automatically affect that user.

## *Challenges*

## *What I Learned*

## *Next Steps*
