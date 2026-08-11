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

### *Step 2 – Configure Screen Saver Lock*

![Enable Screen Saver](img/Enable_Screen_Saver.png)

![Force Screen Saver](img/Force_Screen_Saver.png)

![Password Protect the Screen Saver](img/Password_Protect_Screen_Saver.png)

![Screen Saver Timeout](img/Screen_Saver_Timeout.png)

![Screen Saver Working](img/Screen_Saver_Working.png)

In the Windows Server 2022 VM, I edit the **Default Domain Policy** and navigate to **User Configuration > Policies > Administrative Templates > Control Panel > Personalization**. I enable **Enable screen saver**, **Force specific screen saver**, **Password protect the screen saver**, and **Screen saver timeout**, configuring the timeout to **2 minutes**. I specify **scrnsave.scr** as the screen saver, then run `gpupdate /force` before restarting the Windows 11 VM.

After signing back into the domain account and remaining idle for two minutes, the screen saver activates and the workstation locks. When I move the mouse or press a key, Windows returns to the sign-in screen and requires the user's password before access is restored, confirming that the policy has been successfully applied.

Organizations commonly configure automatic workstation locking to protect sensitive information when employees leave their computers unattended. Requiring users to authenticate after a period of inactivity helps reduce the risk of unauthorized access while still allowing employees to securely resume their work. For demonstration purposes, I configured the timeout to **2 minutes** so the policy could be tested quickly within the lab.

### *Step 3 – Password Complexity*

![Password Complexity Policy](img/Password_Complexity_Policy.png)

![Password Complexity Confirmed](img/Password_Complexity_Confirmed.png)

In the Windows Server 2022 VM, I edit the **Default Domain Policy** and navigate to **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy**. I enable **Password must meet complexity requirements**, then run `gpupdate /force` before restarting the Windows 11 VM.

To verify the policy, I attempt to change the user's password from the Windows 11 VM using **password123**, which contains only lowercase letters and numbers. Windows rejects the password and displays a message indicating that it does not satisfy the domain's password policy. I then create a password containing uppercase letters, lowercase letters, and numbers, such as **Password123**, which Windows accepts because it satisfies the configured complexity requirements.

Organizations enforce password complexity requirements to reduce the likelihood of weak or easily guessed passwords. Requiring users to create more complex passwords helps protect accounts against brute-force attacks, dictionary attacks, and other common password-related threats.

### *Step 4 - Configure Minimum Password Length*

![Minimum Password Policy](img/Minimum_Password_Policy.png)

![Minimum Password Applied](img/Minimum_Password_Applied.png)

In the Windows Server 2022 VM, I edit the **Default Domain Policy** and navigate to **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy**. I configure **Minimum password length** to require passwords to be at least **12 characters** long. I then run `gpupdate /force` before restarting the Windows 11 VM.

To verify the policy, I attempt to change the user's password from the Windows 11 VM using **Password1**, which satisfies the password complexity requirements but is only **9 characters** long. Windows rejects the password and displays a message indicating that it does not satisfy the domain's password policy, confirming that the minimum password length requirement has been successfully applied.

Organizations commonly require longer passwords because they are more resistant to brute-force attacks and generally provide stronger protection for user accounts and sensitive organizational data.

### *Step 5 - Configure Password History*

![Configure Password History](img/Configure_Password_History.png)

![Password History Test](img/Password_History_Test.png)

In the Windows Server 2022 VM, I edit the **Default Domain Policy** and navigate to **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy**. I configure **Enforce password history** to remember the previous **5 passwords**, then run `gpupdate /force` before restarting the Windows 11 VM.

To verify the policy, I change the user's password and then attempt to reuse one of the recently used passwords. Windows prevents the password from being reused, confirming that the policy has been successfully applied.

Organizations commonly enforce password history policies to prevent users from repeatedly cycling between the same passwords. This encourages users to create new passwords rather than continually reusing previous credentials.

### *Step 6 - Configure Maximum Password Age*

![Maximum Password Age](img/Maximum_Password_Age.png)

In the Windows Server 2022 VM, I edit the **Default Domain Policy** and navigate to **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy**. I configure the **Maximum password age** policy to **60 days**, then run `gpupdate /force` before restarting the Windows 11 VM.

The maximum password age determines how long a password may be used before Windows requires the user to create a new one.

Organizations commonly configure password expiration policies to reduce the amount of time a compromised password can remain valid. Requiring periodic password changes helps improve overall account security while encouraging users to regularly update their credentials.

### *Step 7 - Configure Account Lockout Threshold*

![Configure_Account_Threshold](img/Configure_Account_Threshold.png)

![Account_Locked_Out_Threshold](img/Account_Locked_Out_Threshold.png)

![Unlocking Account](img/Unlocking_Account.png)

In the Windows Server 2022 VM, I edit the **Default Domain Policy** and navigate to **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy**. I configure the **Account lockout threshold** to **5 invalid logon attempts**, then run `gpupdate /force` before restarting the Windows 11 VM.

To verify the policy, I intentionally enter the wrong password five consecutive times while attempting to sign in to the Windows 11 VM. After the fifth failed attempt, Windows locks the account and prevents additional login attempts, even if the correct password is entered.

To restore access, I return to the Windows Server 2022 VM and open **Active Directory Users and Computers**. I locate the locked user account, open **Properties > Account**, select **Unlock account**, and apply the change. I then return to the Windows 11 VM and successfully sign in using the correct password, confirming that the account has been unlocked.

Organizations commonly configure account lockout thresholds to help defend against repeated password-guessing attacks by limiting the number of consecutive failed login attempts. IT administrators may also need to unlock accounts when legitimate users accidentally trigger the lockout policy, making account lockout troubleshooting and recovery a common user support task.

## *Challenges*
- One of the key concepts in this lab was understanding the difference between **OU-linked Group Policy Objects** and the **Default Domain Policy**. Unlike the policies configured in the previous lab, password and account lockout settings must be configured through the Default Domain Policy because they are intended to apply consistently across the entire Active Directory domain.

## *What I Learned*

