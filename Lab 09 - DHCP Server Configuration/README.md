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

## **Challenges**

## **What I Learned**

## **Next Steps**
