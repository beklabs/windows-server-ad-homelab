# Windows Server 2022 & Active Directory Home Lab
**Domain:** beklabs.org | **Hypervisor:** VirtualBox | **Networking:** Bridged

---

## Table of Contents
1. [Prerequisites](#-prerequisites)
2. [Project Overview](#project-overview)
3. [Installing Oracle VirtualBox and VirtualBox Extension Pack](#installing-oracle-virtualbox-and-virtualbox-extension-pack)
4. [Server Installation (DC)](#server-installation-dc)
5. [Windows 10 Client Installation](#windows-10-client-installation)
6. [Active Directory Configuration](#active-directory-configuration)
7. [Troubleshooting](#troubleshooting)
8. [Conclusion](#conclusion)

---

## Prerequisites
Before starting this lab, you will need to download and install the following software. Note that the Windows ISOs are evaluation versions and will require a free registration on Microsoft's site.
* [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads)
* [Windows Server 2022 EVAL ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
* [Windows 10 EVAL ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise)

---

## Project Overview

---

## Installing Oracle VirtualBox and VirtualBox Extension Pack

1. From https://www.virtualbox.org/wiki/Downloads, I downloaded the `Windows hosts` VirtualBox version and opened the .exe file to begin installation
2. Clicked `Next`

<img width="491" height="389" alt="image" src="https://github.com/user-attachments/assets/d90672ae-1553-46d0-8150-8bb2e5b4cd29" />

3. Accepted the terms agreement and clicked `Next`

<img width="495" height="390" alt="image" src="https://github.com/user-attachments/assets/1dc5c130-a294-4656-b430-e77bf45fbb87" />

4. Verified location of where the application was going to be installed and clicked `Next`

<img width="496" height="394" alt="image" src="https://github.com/user-attachments/assets/adfeaffe-99f0-4d8b-ba97-1d6cdfa8f944" />

5. Was given a warning message about temporary network disconnection while Oracle VirtualBox installs. I acknowledged this and clicked `Yes`

<img width="494" height="392" alt="image" src="https://github.com/user-attachments/assets/533990c4-7c09-472f-8633-d110acc3cf08" />

6. It mentioned I was missing some dependencies, but since I'm not using Python for this project I acknowledged and clicked `Yes`

<img width="496" height="392" alt="image" src="https://github.com/user-attachments/assets/1fc743b8-3c28-4384-8dc4-c09f0290d2d6" />

7. Unchecked `Add to Start menu`, kept the other two options checked, and clicked `Next`

<img width="494" height="392" alt="image" src="https://github.com/user-attachments/assets/1840bc5e-ba7f-4bdf-9326-500123ce2422" />

8. Clicked `Install`

<img width="495" height="391" alt="image" src="https://github.com/user-attachments/assets/de4ec14c-32c9-4c79-9aed-8df97762c3e8" />

9. Once it successfully installed, I unchecked `Start Oracle VirtualBox 7.2.6` (because I'm going to be installing the VirtualBox Extension Pack before starting VB up) and clicked `Finish`

<img width="493" height="393" alt="image" src="https://github.com/user-attachments/assets/5822ac19-62a1-4ebf-844b-8e1e2093c6a0" />

10. Went back to https://www.virtualbox.org/wiki/Downloads to download the VirtualBox Extension Pack and clicked `Accept and Download`

<img width="533" height="251" alt="image" src="https://github.com/user-attachments/assets/c785f887-e478-4a82-9c6e-7bd7b949e59e" />

11. Clicked on the .exe file, scrolled down to the bottom of the agreements, and clicked `I Agree`

<img width="600" height="482" alt="image" src="https://github.com/user-attachments/assets/044dba1d-58bc-4f59-adb3-7a0890edb32d" />

Now Oracle VirtualBox and the VirtualBox Extension Pack are both installed successfully.

---

## Server Installation (DC)
1. Opened up Oracle VirtualBox and selected `New` from the home menu

<img width="870" height="805" alt="image" src="https://github.com/user-attachments/assets/f1d4e683-eebc-4093-a33d-79842ac36142" />

2. Named the VM `DC`, made sure to select the `SERVER_EVAL_x64FRE_en-us.iso` for the ISO Image, and unchecked `Proceed with Unattended Installation` since I'm setting this up myself

<img width="1064" height="558" alt="image" src="https://github.com/user-attachments/assets/4c4f0f2a-c1f7-4dec-81f6-c7678cf87a89" />

3. Clicked on the `Specify virtual hardware` and kept the `Base Memory` at 2048 MB (2 GB) and the `Number of CPUs` at 1

<img width="1063" height="561" alt="image" src="https://github.com/user-attachments/assets/48921268-38d4-4eaa-8495-7e74a8635d8a" />

4. Clicked on the `Specify virtual hard disk` drop down, selected `Create a New Virtual Hard Disk`, allocated 50 GB of storage for the VM, and clicked `Finished`

<img width="1065" height="562" alt="image" src="https://github.com/user-attachments/assets/ffaa0011-a7c7-4d3b-a1dc-3117ecf8a3c3" />






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
