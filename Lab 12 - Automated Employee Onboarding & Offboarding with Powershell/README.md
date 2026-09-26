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

### *Step 3 - Automatically Determine OU and Security Group*

![Department Switch Script](img/Department_Switch_Script.png)

![Department Switch Test](img/Department_Switch_Test.png)

In the Windows Server 2022 VM, I expand the `New-Employee.ps1` onboarding script by adding a `switch` statement. This allows the script to automatically determine the correct Organizational Unit and security group based on the department entered by the administrator.

I add the following `switch` statement after collecting the employee information:

```powershell
switch ($Department) {

    "Accounting" {
        $OU = "OU=Accounting,DC=lab,DC=local"
        $Group = "Accounting Users"
    }

    "HR" {
        $OU = "OU=HR,DC=lab,DC=local"
        $Group = "HR Users"
    }

    "IT" {
        $OU = "OU=IT,DC=lab,DC=local"
        $Group = "IT Users"
    }
}
```

The `switch` statement checks the value stored in `$Department` and runs the block of code that matches the department entered by the administrator.

For example, if I enter:

`IT`

the script automatically stores the following values:

```powershell
$OU = "OU=IT,DC=lab,DC=local"
$Group = "IT Users"
```

This means I only need to provide the employee's department instead of manually entering the appropriate OU path and security group for every new employee.

I also update the output section of the script to display the values selected by the `switch` statement:

```powershell
Write-Host "OU: $OU"
Write-Host "Security Group: $Group"
```

After updating the script, I run `New-Employee.ps1` and test the onboarding process using an employee in the **IT** department. The script correctly selects the IT OU and the `IT Users` security group.

I then run the script again using an employee in the **HR** department. This time, PowerShell automatically changes the selected values to the HR OU and the `HR Users` security group.

Testing two different departments verifies that the `switch` statement is making decisions based on the value stored in `$Department` rather than using a hardcoded OU or security group.

At this stage, the script still does not create an Active Directory account. It now collects employee information and automatically determines where the employee should be placed and which department security group should be assigned.

This step demonstrates how a `switch` statement can be used to add decision-making logic to a PowerShell automation script.

### *Step 4 - Add Department Input Validation*

![Default Switch Script](img/Default_Switch_Script.png)

![Default Switch Test](img/Default_Switch_Test.png)

In the Windows Server 2022 VM, I improve the `New-Employee.ps1` onboarding script by adding input validation to the existing `switch` statement. This prevents the script from continuing if the administrator enters a department that is not supported by the onboarding workflow.

I add a `default` block to the existing `switch` statement:

```powershell
switch ($Department) {

    "Accounting" {
        $OU = "OU=Accounting,DC=lab,DC=local"
        $Group = "Accounting Users"
    }

    "HR" {
        $OU = "OU=HR,DC=lab,DC=local"
        $Group = "HR Users"
    }

    "IT" {
        $OU = "OU=IT,DC=lab,DC=local"
        $Group = "IT Users"
    }

    default {
        Write-Host "Invalid department. Please enter Accounting, HR, or IT."
        exit
    }
}
```

The `default` block runs when the value stored in `$Department` does not match any of the available cases in the `switch` statement. This works similarly to an `else` statement by providing an action for any value that was not previously matched.

If an unsupported department is entered, the script displays the following message:

`Invalid department. Please enter Accounting, HR, or IT.`

I also use the `exit` command immediately after the message. This stops the script from continuing with an invalid department and prevents later onboarding commands from attempting to use an empty or incorrect OU and security group.

To test the validation, I run `New-Employee.ps1` and enter `Finance` as the employee's department. Since Finance is not one of the configured departments, PowerShell runs the `default` block, displays the invalid department message, and stops the script before displaying the Employee Information section.

I then run the script again and enter `Accounting` as the department. This time, the input matches a valid case and the script continues normally. PowerShell automatically selects:

`OU=Accounting,DC=lab,DC=local`

and:

`Accounting Users`

This verifies that invalid department values are stopped while valid department values continue through the onboarding workflow.

This step demonstrates how input validation can make a PowerShell automation script safer by preventing unsupported information from being processed before changes are made to Active Directory.

### *Step 5 - Checking for Existing Username*

![Existing User Script](img/Existing_User_Script.png)

![Existing User Test](img/Existing_User_Test.png)

In the Windows Server 2022 VM, I continue improving the `New-Employee.ps1` onboarding script by adding a check for existing Active Directory usernames. Before creating a new employee account, the script now searches Active Directory to determine whether the requested username is already being used.

I add the following command after the department `switch` statement:

```powershell
$ExistingUser = Get-ADUser -Filter "SamAccountName -eq '$Username'"
```

The `Get-ADUser` command searches Active Directory for a user whose `SamAccountName` matches the username entered by the administrator. The result of the search is stored in the `$ExistingUser` variable.

For example, if the username entered is:

`Sedin`

the filter searches Active Directory for an account with the following value:

`SamAccountName = Sedin`

I then use an `if` statement to determine whether the search returned an existing account:

```powershell
if ($ExistingUser) {
    Write-Host "Username $Username already exists in Active Directory."
    Write-Host "Onboarding stopped."
    exit
}

Write-Host "Username $Username is available."
```

If `$ExistingUser` contains an Active Directory user object, the `if` condition evaluates as true. The script displays a message explaining that the username already exists and then uses `exit` to stop the onboarding process.

If no matching account is found, `$ExistingUser` does not contain a user object. The `if` block is skipped and the script continues to:

```powershell
Write-Host "Username $Username is available."
```

An `else` statement is not required in this case because `exit` completely stops the script when an existing account is detected. If PowerShell reaches the username available message, I already know that the existing-user check did not find a matching account.

To test the duplicate username check, I first run the script using `Sedin`, which is already an existing Active Directory username. PowerShell detects the existing account, displays that the username is already in use, and stops the onboarding process before reaching the Employee Information section.

I then run the script again using `ggiovanna`, a username that does not currently exist in Active Directory. PowerShell reports that the username is available and continues through the onboarding workflow. Since I enter `HR` as the department, the script also correctly selects:

`OU=HR,DC=lab,DC=local`

and:

`HR Users`

Testing both an existing and an available username verifies that the script can prevent duplicate Active Directory accounts while allowing new usernames to continue through the onboarding process.

At this stage, the script validates both the employee's department and username before any Active Directory account is created. This adds another safety check to the onboarding workflow and prepares the script for automated account creation in the next step.

### *Step 6 - Create the Active Directory User Account*

![AD User Creation Script](img/AD_User_Creation_Script.png)

![AD User Creation Test](img/AD_User_Creation_Test.png)

![AD User Creation Confirmed](img/AD_User_Creation_Confirmed.png)

In the Windows Server 2022 VM, I expand the `New-Employee.ps1` onboarding script so it can now create the employee's Active Directory account. At this point in the workflow, the employee's department has already been validated, the correct OU and security group have been selected, and the requested username has been checked to make sure it is available.

Before creating the account, I prompt the administrator to enter a temporary password:

```powershell
$Password = Read-Host -AsSecureString "Enter temporary password"
```

The `Read-Host` command collects the password while `-AsSecureString` prevents the password from being stored as normal readable text. The resulting secure password is stored in the `$Password` variable and can then be passed to `New-ADUser`.

I use the following command to create the Active Directory account:

```powershell
New-ADUser `
    -Name "$FirstName $LastName" `
    -GivenName $FirstName `
    -Surname $LastName `
    -SamAccountName $Username `
    -UserPrincipalName "$Username@lab.local" `
    -Department $Department `
    -Path $OU `
    -AccountPassword $Password `
    -ChangePasswordAtLogon $true `
    -Enabled $true
```

Instead of manually entering the employee information directly into `New-ADUser`, the command uses the variables collected and generated earlier in the onboarding script.

The `-Name`, `-GivenName`, and `-Surname` parameters configure the employee's name, while `-SamAccountName` uses the username entered by the administrator. The `-UserPrincipalName` parameter combines the username with the `lab.local` domain to create the employee's user principal name.

The `-Department` parameter stores the employee's selected department in their Active Directory account.

I use:

```powershell
-Path $OU
```

to determine where the new account should be created. The value of `$OU` was automatically selected earlier by the department `switch` statement. This allows the same `New-ADUser` command to create employees in different Organizational Units without manually changing the OU path each time.

For example, because I select `IT` during this test, `$OU` contains:

`OU=IT,DC=lab,DC=local`

The new employee is therefore automatically created inside the **IT OU**.

The `-AccountPassword` parameter assigns the temporary password stored in `$Password`, while:

```powershell
-ChangePasswordAtLogon $true
```

requires the employee to change the temporary password the next time they sign in.

Finally:

```powershell
-Enabled $true
```

creates the account in an enabled state so it can be used for domain authentication.

After the `New-ADUser` command completes, the script displays:

`Active Directory account created successfully.`

To test the updated onboarding workflow, I run `New-Employee.ps1` and enter **Giorno Giovanna** as a new employee with the username `ggiovanna` and the **IT** department. The script confirms that the username is available, prompts for a temporary password, and creates the Active Directory account.

I then open **Active Directory Users and Computers (ADUC)** and navigate to the **IT OU**. I verify that the Giorno Giovanna account was successfully created in the OU selected by the script.

This step connects the information gathering, department selection, input validation, and username validation from the previous steps with actual Active Directory account provisioning. The onboarding script can now automatically create an enabled employee account in the appropriate Organizational Unit using the information entered by the administrator.

## **Challenges**

## **What I Learned**

## **Next Steps**
