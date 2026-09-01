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

### *Step 4 - Create an IPv4 DHCP Scope*

![IPv4 DHCP Scope](img/IPv4_DHCP_Scope.png)

In the **DHCP Management Console**, I expand the DHCP server, right-click **IPv4**, and create a new scope named **Lab Network**.

I configure the scope to provide addresses from `10.1.10.10` through `10.1.10.100` using the subnet mask `255.255.255.0` (`/24`).

The DHCP scope defines the pool of IPv4 addresses that the server is allowed to automatically lease to client devices. I intentionally keep the server's static address of `10.1.10.2` outside of the DHCP address pool to prevent DHCP from assigning that address to another device.

I keep the default lease duration, which determines how long a client is allowed to use an assigned IP address before the lease must be renewed.

### *Step 5 - Configure DHCP Scope Options*

![Configure DHCP Scope](img/Configure_DHCP_Scope.png)

After creating the DHCP scope, I configure the network information that will be automatically provided to DHCP clients.

I configure the DNS server as `10.1.10.2`, which is the IP address of the Windows Server 2022 domain controller and DNS server, and configure `lab.local` as the DNS domain name.

Because the current VirtualBox lab network does not use a router for external network connectivity, I do not configure a default gateway for this scope.

DHCP scope options allow administrators to centrally provide clients with additional network configuration along with their IP address. This reduces the need to manually configure settings such as DNS on each workstation.

After completing the configuration, I activate the DHCP scope so that it can begin providing leases to clients.

## **Challenges**

## **What I Learned**

## **Next Steps**
