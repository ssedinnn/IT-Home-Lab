# **Lab 09 - DHCP Server Configuration**

## **Objective**

## **Environment**

## **Skills Demonstrated**

## **Steps**

### *Step 1 - Review the Current Static Network Configuration*

![ipconfig](img/ipconfig.png)

Before configuring DHCP, I open **Command Prompt** on the Windows 11 VM and run `ipconfig /all` to review the client's existing network configuration.

The workstation is currently configured with a static IPv4 address, meaning its IP address and DNS server information were manually assigned rather than automatically provided by a DHCP server.

Reviewing the existing configuration provides a baseline that I can compare against later when the Windows 11 client is changed to obtain its network configuration automatically through DHCP.

### *Step 2 - Install the DHCP Server Role*

![DHCP Installation](img/DHCP_Installation.png)

In the Windows Server 2022 VM, I open **Server Manager** and use **Add Roles and Features** to install the **DHCP Server** role.

Installing the DHCP Server role allows the Windows Server to automatically provide network configuration to client devices instead of requiring administrators to manually configure network settings on every workstation.

After the installation completes, Server Manager indicates that additional DHCP configuration is required before the server can begin providing addresses to clients.

### *Step 3 - Authorize the DHCP Server*

![DHCP Server Authorization](img/DHCP_Authorization.png)

After installing the DHCP Server role, I complete the DHCP post-installation configuration through **Server Manager**. During this process, I authorize the DHCP server within the Active Directory domain.

I then open the **DHCP Management Console** and verify that the `CA-DC-01` DHCP server is available for configuration.

Authorizing a DHCP server in an Active Directory environment helps ensure that only approved DHCP servers can provide network configuration to domain clients. This reduces the risk of an unauthorized DHCP server distributing incorrect network settings.

## **Challenges**

## **What I Learned**

## **Next Steps**
