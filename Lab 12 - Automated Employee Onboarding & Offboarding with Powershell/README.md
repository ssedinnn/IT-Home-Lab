# **Lab 12 - Automated Employee Onboarding & Offboarding with Powershell**

## **Objective**

## **Environment**

## **Skills Demonstrated**

## **Steps**

### *Step 1 - Create the Department and Offboarding Structure*

![HR OU](img/HR_OU.png)

![IT OU](img/IT_OU.png)

In the Windows Server 2022 VM, I use **Active Directory Users and Computers (ADUC)** to expand the existing Active Directory structure before building the employee onboarding and offboarding scripts.

I create three new Organizational Units under the `lab.local` domain:

- **HR**
- **IT**
- **Disabled Users**

The **HR** and **IT** OUs provide separate locations for user accounts based on their department. I will use these alongside the existing **Accounting OU** so the onboarding script can automatically place new employees in the correct location within Active Directory.

The **Disabled Users OU** provides a separate location for accounts that have been offboarded. Instead of immediately deleting an employee's account, the offboarding process will disable the account and move it into this OU so the account can be retained while preventing the user from signing in.

I also create a new Global Security group inside each department OU:

- **HR Users**
- **IT Users**

These groups will be used to assign access based on the employee's department. The existing **Accounting Users** security group will continue to be used for employees placed in the Accounting department.

This creates the following structure for the onboarding process:

| Department | Organizational Unit | Security Group |
| --- | --- | --- |
| Accounting | Accounting | Accounting Users |
| HR | HR | HR Users |
| IT | IT | IT Users |

With this structure in place, the PowerShell onboarding script can later determine the appropriate OU and security group based on the employee's department. The **Disabled Users OU** will also be used during the offboarding portion of the lab to separate disabled employee accounts from active users.

## **Challenges**

## **What I Learned**

## **Next Steps**
