# **Lab 08 - DNS Administration and Troubleshooting**

## **Objective**
Learn how DNS supports an Active Directory domain by creating and managing DNS records, testing name resolution from a domain-joined workstation, and troubleshooting common DNS issues.

## **Environment**

## **Skills Demonstrated**

## **Steps**

### *Step 1 — Explore the Existing DNS Configuration*

![DNS Config](img/DNS_Config.png)

In the Windows Server 2022 VM, I open **Server Manager > Tools > DNS** to launch DNS Manager. I expand the DNS server and navigate to **Forward Lookup Zones > lab.local**. This zone was automatically created when Active Directory Domain Services and DNS were configured for the `lab.local` domain.

Inside the `lab.local` zone, I review the existing DNS records and become familiar with how the DNS server stores information about devices and services within the domain.

A **Forward Lookup Zone** is used to translate a hostname into an IP address. For example, the existing Host (A) record for the domain controller maps the hostname `ca-dc-01` to its IP address:

`ca-dc-01.lab.local` → `10.1.10.2`

This demonstrates how a Forward Lookup Zone allows devices on the network to locate another computer by its hostname instead of requiring the user or application to know its IP address.

## **Challenges**

## **What I Learned**

## **Next Steps**

