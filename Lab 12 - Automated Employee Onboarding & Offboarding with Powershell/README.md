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

### *Step 2 - Create the Employee Onboarding Powershell Script*

![Onboarding Script Creation](img/Onboarding_Script_Creation.png)

![Onboarding Script Check](img/Onboarding_Script_Check.png)

In the Windows Server 2022 VM, I begin building a reusable PowerShell script for employee onboarding. Instead of entering each administrative command manually into PowerShell, I create a script named `New-Employee.ps1` and save it in the existing `C:\Scripts` folder.

The script is saved at:

`C:\Scripts\New-Employee.ps1`

I start the script by loading the Active Directory PowerShell module:

```powershell
Import-Module ActiveDirectory
```

I then use `Read-Host` to collect information about the employee being onboarded:

```powershell
$FirstName = Read-Host "Enter employee first name"
$LastName = Read-Host "Enter employee last name"
$Username = Read-Host "Enter employee username"
$Department = Read-Host "Enter employee department"
```

Each value entered by the administrator is stored in a PowerShell variable. For example, the employee's username is stored in `$Username`, while the selected department is stored in `$Department`.

I also add several `Write-Host` commands to display the information that was entered:

```powershell
Write-Host ""
Write-Host "Employee Information"
Write-Host "--------------------"
Write-Host "Name: $FirstName $LastName"
Write-Host "Username: $Username"
Write-Host "Department: $Department"
```

At this stage, the script only collects and displays employee information and does not make any changes to Active Directory. This allows me to build and test the onboarding workflow in smaller sections before adding commands that create or modify user accounts.

Creating the onboarding process as a `.ps1` file also allows the script to be saved, modified, and reused for future employees instead of rebuilding the PowerShell commands each time.

## **Challenges**

## **What I Learned**

## **Next Steps**
