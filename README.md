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
[↑ Back to Table of Contents](#table-of-contents)

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
[↑ Back to Table of Contents](#table-of-contents)

1. Opened up Oracle VirtualBox and selected `New` from the home menu

<img width="870" height="805" alt="image" src="https://github.com/user-attachments/assets/f1d4e683-eebc-4093-a33d-79842ac36142" />

2. Named the VM `DC`, made sure to select the `SERVER_EVAL_x64FRE_en-us.iso` for the ISO Image, and unchecked `Proceed with Unattended Installation` since I'm setting this up myself

<img width="1064" height="558" alt="image" src="https://github.com/user-attachments/assets/4c4f0f2a-c1f7-4dec-81f6-c7678cf87a89" />

3. Clicked on the `Specify virtual hardware` and kept the `Base Memory` at 2048 MB (2 GB) and the `Number of CPUs` at 1

<img width="1063" height="561" alt="image" src="https://github.com/user-attachments/assets/48921268-38d4-4eaa-8495-7e74a8635d8a" />

4. Clicked on the `Specify virtual hard disk` drop down, selected `Create a New Virtual Hard Disk`, allocated 50 GB of storage for the VM, and clicked `Finished`

<img width="1065" height="562" alt="image" src="https://github.com/user-attachments/assets/ffaa0011-a7c7-4d3b-a1dc-3117ecf8a3c3" />

5. Once the VM was created, I right-clicked on it and selected `Settings`

<img width="870" height="806" alt="image" src="https://github.com/user-attachments/assets/22ccd1f9-fe2a-4894-9080-d80a4347c56d" />

6. Clicked on `System`, and where it says `Boot Device Order (BIOS only)`, I unchecked `Floppy` and made sure that `Optical` was before `Hard Disk`

<img width="785" height="521" alt="image" src="https://github.com/user-attachments/assets/57aac422-37ca-4e5e-bcfb-5460245f6c7b" />

7. Clicked on `Network`, changed the `Attached to` to `Bridged Adapter`, made sure the `Name` displayed my correct internet connection, and clicked `OK`

<img width="786" height="518" alt="image" src="https://github.com/user-attachments/assets/53e4b001-b1e4-4a6f-b551-dc4c63dc998b" />

8. Double-clicked on `DC`, kept the language, time and currency format, keyboard or input method as the defaults, and clicked `Next`

<img width="623" height="463" alt="image" src="https://github.com/user-attachments/assets/dd79e667-befa-4603-96e9-06ef590762f9" />

9. Clicked `Install Now`

<img width="626" height="461" alt="image" src="https://github.com/user-attachments/assets/6c9c470b-a733-4483-95ca-ad7255715c51" />

10. Selected the `Windows Server 2022 Datacenter Evaluation (Desktop Experience)`, and then clicked `Next`
> **This is so I could have a full GUI rather than just the command line** 

<img width="645" height="484" alt="image" src="https://github.com/user-attachments/assets/c3995141-c066-4fcc-a25e-ed19283861ad" />

11. Accepted the terms and clicked `Next`

<img width="642" height="483" alt="image" src="https://github.com/user-attachments/assets/6807149c-f956-441f-b438-2c4e9b0b19ac" />

12. It asked me what type of install I want to perform - I chose `Custom: Install Microsoft Server Operating System only (advanced)`
> **I chose this because I am doing a completely new, fresh install**

<img width="643" height="481" alt="image" src="https://github.com/user-attachments/assets/adfb3c59-878f-48b8-9d06-5693ddc324dc" />

13. Gave me the option to allocate disk space, since I'm only using one drive I just clicked `Next`

<img width="643" height="483" alt="image" src="https://github.com/user-attachments/assets/8c6a8aa1-74a4-494f-8bbc-3c063fc924d8" />

14. Once it finished installing, I put in a password for the local admin account and clicked `Finish`

<img width="1020" height="767" alt="image" src="https://github.com/user-attachments/assets/46ca69d0-c94d-4ded-b717-74d1bfcfc602" />

15. At the sign-in page for the computer, I clicked on `Input`, hovered over `Keyboard`, and then clicked on `Insert Ctrl+Alt+Del`

<img width="1024" height="803" alt="image" src="https://github.com/user-attachments/assets/4aafbdd4-77dc-48ef-bc89-a93d60c1e878" />

16. Logged into the admin account using the password I just created and waited to load into the VM
17. A pop-up came up asking if I wanted to allow my PC to be discoverable by other PCs and devices on this network. I clicked `Yes`

<img width="346" height="435" alt="image" src="https://github.com/user-attachments/assets/37da542d-fe05-4795-b837-7be0001d8726" />

18. Right-clicked on the Windows Start and selected `System` then selected `Rename this PC`, renamed it to `DC`, clicked `Next`, and then clicked `Restart now`

<img width="1022" height="773" alt="image" src="https://github.com/user-attachments/assets/4ced8cf0-a821-4c91-acf3-5950c754bd0a" /><img width="1022" height="769" alt="image" src="https://github.com/user-attachments/assets/81150ac6-644c-4572-970a-68ee163fdd31" /><img width="687" height="308" alt="image" src="https://github.com/user-attachments/assets/458722f1-5c1c-4af6-8e65-17ccdad02ee7" /><img width="689" height="220" alt="image" src="https://github.com/user-attachments/assets/05a0293c-5902-416f-8a06-d2054cc48ead" />

19. Once the VM came back on, I clicked on `File`, Clicked `Close`, selected the option `Send the shutdown signal`, and clicked `OK`

<img width="1030" height="799" alt="image" src="https://github.com/user-attachments/assets/735f4625-55a3-4244-bfb7-aeb289e404e6" /><img width="1020" height="799" alt="image" src="https://github.com/user-attachments/assets/0ee0d862-9b0b-44c6-9a3a-196b1a80c1e0" />

20. While the VM server was shut down, I right-clicked on it and selected `Clone`, named it `Serverimage`, selected `Full Clone`, and clicked `Finish`
>**This is so I can have an instance of it ready to go in case I need it on the future**

<img width="865" height="739" alt="image" src="https://github.com/user-attachments/assets/551c7eda-3905-48a2-a208-8fc54cf9ba63" /><img width="624" height="411" alt="image" src="https://github.com/user-attachments/assets/77e4d007-f83e-43db-b785-ee3a15c9648b" />

DC Server installation is now complete!

---

##Windows 10 Client Installation

1. Opened up Oracle VirtualBox and selected `New` from the home menu























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
