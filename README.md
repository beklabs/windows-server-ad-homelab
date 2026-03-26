# Windows Server 2022 & Active Directory Home Lab
**Domain:** beklabs.org | **Hypervisor:** VirtualBox | **Networking:** Bridged

---

## Table of Contents
1. [Prerequisites](#-prerequisites)
2. [Project Overview](#-project-overview)
3. [Installing Oracle VirtualBox](#installing-oracle-virtualbox)
4. [Server Installation (DC)](#-server-installation-dc)
5. [Windows 10 Client Installation](#-windows-10-client-installation)
6. [Active Directory Configuration](#-active-directory-configuration)
7. [Troubleshooting](#troubleshooting)
8. [Conclusion](#-conclusion)

---

## Prerequisites
Before starting this lab, you will need to download and install the following software. Note that the Windows ISOs are evaluation versions and will require a free registration on Microsoft's site.
[Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
[Windows Server 2022 EVAL ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
[Windows 10 EVAL ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise)

## Project Overview
This lab demonstrates how to set up a functional Active Directory environment from scratch. I focused on server promotion, user management with "Least Privilege" principles, and troubleshooting DNS connectivity between virtualized machines.

---

## Server Installation (DC)
* **Image:** Windows Server 2022 Datacenter Evaluation (Desktop Experience).
* **Setup:** Used a fresh "Custom" install to allocate disk space manually.
* **Naming:** Renamed the PC to `DC` immediately for clarity.
* **Redundancy:** Created a **Full Clone** named `Serverimage`. This ensures I have a "clean slate" backup if the environment ever breaks.

---

## Windows 10 Client Installation
* **Image:** Windows 10 Evaluation ISO.
* **Setup:** Configured as a "helpdesk" machine. 
* **Snapshots:** Created a **Full Clone** named `Staff` to act as a template for future users.
* **Local Admin:** Created a local `admin` account first to handle the initial setup before joining the domain.

---

## Active Directory Configuration
1. **Role Installation:** Added "Active Directory Domain Services" via Server Manager.
2. **Forest Creation:** Promoted the server to a DC and created the `beklabs.org` forest with the NetBIOS name `BLABS`.
3. **User Management:** Created a new user `helpdesk blabs` and manually assigned them to the **Domain Admins** group to grant administrative rights.

---

## The "Delegation" Error & DNS Fix
When trying to join the helpdesk machine to the domain, I encountered a "DC could not be contacted" error referencing DNS delegation.

**My Troubleshooting Steps:**
* **Diagnosis:** Ran `ipconfig /all` on the DC to find its actual IPv4.
* **NIC Configuration:** Noticed the helpdesk VM was likely trying to use the home router's DNS instead of the DC's.
* **The Fix:** * Disabled **IPv6** on the client.
    * Manually set the **Preferred DNS** on the helpdesk VM to the DC's IP.
* **Result:** The domain join was successful immediately after these changes.

---

## Conclusion
This lab taught me that **DNS is the backbone of Active Directory**. Even if the machines are on the same network (Bridged), they won't communicate until the Client specifically knows to look at the DC for name resolution.
