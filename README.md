# IT Home Lab

A collection of hands-on IT home lab projects focused on Windows Server, Active Directory, Group Policy, networking, security, PowerShell, and IT troubleshooting.

This repository documents my continued development of practical IT support and system administration skills through a virtualized Windows domain environment.

## About

I built this home lab to gain hands-on experience with technologies and administrative tasks commonly encountered in IT support and Windows enterprise environments.

Using Windows Server 2022 and Windows 11 virtual machines, I have built and expanded an Active Directory environment while practicing user administration, Group Policy, account security, file permissions, network resource deployment, DNS, DHCP, PowerShell administration, and troubleshooting.

Each lab includes step-by-step documentation, screenshots, challenges encountered, troubleshooting performed, and key concepts learned.

## Lab Environment

- **Hypervisor / Virtualization:** Oracle VirtualBox
- **Server Operating System:** Windows Server 2022
- **Client Operating System:** Windows 11 Pro
- **Active Directory Domain:** `lab.local`
- **Core Services & Technologies:** Active Directory Domain Services (AD DS), DNS, DHCP, Group Policy, Windows File Sharing
- **Administration Tools:** Server Manager, Active Directory Users and Computers (ADUC), Group Policy Management Console (GPMC), DNS Manager, DHCP Management Console
- **Command-Line & Scripting Tools:** Windows PowerShell, `ping`, `nslookup`, `ipconfig`, `gpupdate`, `gpresult`

## Skills Demonstrated

- Windows Server 2022 Administration
- Active Directory Domain Services (AD DS)
- Domain Controller Deployment
- Windows 11 Domain Client Deployment
- Active Directory User & Group Management
- Organizational Unit (OU) Management
- Group Policy Administration
- Group Policy Preferences & Item-Level Targeting
- Domain Password & Account Lockout Policies
- User Authentication & Account Troubleshooting
- Windows File Sharing
- NTFS & Share Permissions
- Group-Based Access Control
- Network Drive Deployment
- DNS Administration
- Forward & Reverse DNS Resolution
- DNS Record Management (A, CNAME, PTR)
- DHCP Server Installation & Configuration
- DHCP Scope & Lease Management
- DHCP & DNS Integration
- IPv4 Address Assignment & APIPA Troubleshooting
- DNS & Network Troubleshooting
- Active Directory Administration with PowerShell
- PowerShell AD User & Group Management
- PowerShell Filtering, Pipelines & Object Queries
- Active Directory Account Creation, Modification & Removal with PowerShell
- Virtual Machine & Host-Only Network Configuration
- Technical Documentation

## Lab Projects

### Lab 01 – Building an Active Directory Environment

- Installed and configured Windows Server 2022, deployed Active Directory Domain Services (AD DS), created the `lab.local` forest, and promoted the server to a Domain Controller.

### Lab 02 – Domain Client Deployment

- Configured a Windows 11 Pro virtual machine, established static IPv4 networking between the client and server, joined the workstation to the Active Directory domain, and verified domain authentication.

### Lab 03 – Active Directory User Account Management

- Created and managed Active Directory user accounts while practicing password resets, forced password changes, account disabling, account deletion, and domain authentication testing from Windows 11.

### Lab 04 – Group Policy Management

- Created Organizational Units (OUs) and Group Policy Objects (GPOs) to centrally manage domain users and computers. Deployed desktop settings, system restrictions, and a login banner while troubleshooting Group Policy application.

### Lab 05 – Domain Password & Account Security Policies

- Configured domain-wide password and account lockout policies through the Default Domain Policy. Tested password requirements, account lockouts, workstation locking, and Active Directory account recovery from a domain-joined workstation.

### Lab 06 – Windows File Sharing & NTFS Permissions

- Created and secured an Accounting network share using Active Directory security groups, NTFS permissions, and share permissions. Tested authorized and unauthorized access and troubleshot effective network permissions.

### Lab 07 – Deploying Network Drives with Group Policy

- Automated deployment of the Accounting network drive using Group Policy Preferences. Configured Item-Level Targeting so the drive is automatically mapped only for authorized members of the Accounting Users security group.

### Lab 08 – DNS Administration & Troubleshooting

- Configured and tested DNS records including A, CNAME, and PTR records. Practiced forward and reverse DNS resolution using `nslookup` and `ping`, then simulated an incorrect client DNS configuration to diagnose and restore name resolution.

### Lab 09 – DHCP Server Configuration

- Installed and authorized the DHCP Server role in Active Directory, created and configured an IPv4 scope for the `10.1.10.0/24` network, and automatically provided IP and DNS configuration to a Windows 11 client.
- Verified DHCP leases and used `ipconfig` to release and renew client addressing. Simulated DHCP failure and diagnosed APIPA addressing before restoring connectivity.
- Troubleshot a competing VirtualBox DHCP service that was assigning addresses from the wrong network and restored Windows Server as the active DHCP server.

### Lab 10 – Active Directory Administration with PowerShell

- Used the Active Directory PowerShell module to query and administer users, groups, computers, and Organizational Units from the command line.
- Created and modified Active Directory users, managed security group membership, reset passwords, forced password changes, and disabled, enabled, and removed accounts with PowerShell.
- Practiced PowerShell pipelines, `Select-Object`, filters, `-SearchBase`, Distinguished Names, and command output verification while troubleshooting PowerShell syntax and parameter errors.

## Repository Goals

The purpose of this repository is to:

- Gain hands-on experience with enterprise IT technologies.
- Practice Windows system and Active Directory administration.
- Develop structured troubleshooting skills.
- Build PowerShell and automation skills.
- Improve technical documentation.
- Apply IT concepts in a practical lab environment.
- Build a technical portfolio demonstrating continued learning and hands-on experience.

## What's Next

I plan to continue expanding the environment with projects focused on:

- PowerShell User Provisioning Automation
- Employee Onboarding & Offboarding
- Role-Based Access Control (RBAC)
- Active Directory Delegation of Control
- Windows Client Troubleshooting
- Remote Administration
- Windows Server Backup & Recovery
- Linux Administration
- Networking Fundamentals
- Microsoft Entra ID
- Microsoft 365 Administration

## Feedback

I'm continuously learning and expanding this environment as I develop my IT administration, PowerShell, networking, and troubleshooting skills. Suggestions for improvements or future lab projects are always welcome.
