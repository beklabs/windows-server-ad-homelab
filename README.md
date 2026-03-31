# Windows Server 2022 & Active Directory Home Lab
**Domain:** beklabs.org | **Hypervisor:** VirtualBox | **Networking:** Bridged

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Project Overview](#project-overview)
3. [Installing Oracle VirtualBox and VirtualBox Extension Pack](#installing-oracle-virtualbox-and-virtualbox-extension-pack)
4. [Server Installation (DC)](#server-installation-dc)
5. [Windows 10 Client Installation](#windows-10-client-installation)
6. [Installing Active Directory and adding Win10 VM to Active Directory](#installing-active-directory-and-adding-win10-vm-to-active-directory)
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
[↑ Back to Table of Contents](#table-of-contents)

This project demonstrates the implementation of a functional Windows Server 2022 environment and its integration with a Windows 10 client within a virtualized home lab. As an IT Administrator, the goal was to simulate a real-world enterprise network by deploying a Domain Controller (DC), configuring Active Directory Domain Services (AD DS), and managing user permissions and network connectivity.

**Key Objectives:**
* Deploying and managing multiple Virtual Machines (VMs) using Oracle VirtualBox with optimized hardware allocations
* Installing and configuring Windows Server 2022 using the Desktop Experience GUI for full administrative control
* Creating a new forest (`beklabs.org`) and managing a centralized directory of users and administrative groups
* Solving critical "Real-World" connectivity hurdles, specifically regarding DNS resolution and protocol conflicts between server and client VMs
* Utilizing VM Cloning to create images for rapid deployment and lab recovery

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

4. Clicked on the `Specify virtual hard disk` drop down, selected `Create a New Virtual Hard Disk`, allocated 50 GB of storage for the VM, and clicked `Finish`

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

## Windows 10 Client Installation
[↑ Back to Table of Contents](#table-of-contents)

1. Opened up Oracle VirtualBox and selected `New` from the home menu

<img width="870" height="805" alt="image" src="https://github.com/user-attachments/assets/16a8f2a1-b2aa-4ab5-b8b0-8320a991f604" />

2. Named the VM `helpdesk`, selected the correct Windows 10 EVAL iso, and unchekced `Proceed with Unattended Installation`
>**I did this because I will be setting it up manually**

<img width="1068" height="562" alt="image" src="https://github.com/user-attachments/assets/e6bc4758-88a2-453e-be22-d8b2943aba6f" />

3. Clicked on the `Specify virtual hardware` and kept the `Base Memory` at 2048 MB (2 GB) and the `Number of CPUs` at 1

<img width="1067" height="562" alt="image" src="https://github.com/user-attachments/assets/f7ed6a3c-8dba-40a7-8d4b-b9a33e54bdd7" />

4. Clicked on the `Specify virtual hard disk` drop down, selected `Create a New Virtual Hard Disk`, allocated 20 GB of storage for the VM, and clicked `Finish`

<img width="1065" height="560" alt="image" src="https://github.com/user-attachments/assets/a68610a3-f2ec-4add-a8c9-2581ff898f4b" />

5. Once the VM was created, I right-clicked on it and selected `Settings`

<img width="871" height="775" alt="image" src="https://github.com/user-attachments/assets/1e17424c-0727-4c31-a064-331804e270dd" />

6. Clicked on `System`, and where it says `Boot Device Order (BIOS only)`, I unchecked `Floppy` and made sure that `Optical` was before `Hard Disk`

<img width="785" height="521" alt="image" src="https://github.com/user-attachments/assets/57aac422-37ca-4e5e-bcfb-5460245f6c7b" />

7. Clicked on `Network`, changed the `Attached to` to `Bridged Adapter`, made sure the `Name` displayed my correct internet connection, and clicked `OK`

<img width="786" height="518" alt="image" src="https://github.com/user-attachments/assets/53e4b001-b1e4-4a6f-b551-dc4c63dc998b" />

8. Double-clicked on `helpdesk` VM, kept the language, time and currency format, keyboard or input method as the defaults, and clicked `Next`

<img width="622" height="461" alt="image" src="https://github.com/user-attachments/assets/6eb8ab50-6181-41d3-8940-7a7ae7f5ac80" />

9. Clicked on `Install now`

<img width="623" height="462" alt="image" src="https://github.com/user-attachments/assets/6a5a8212-4725-4d51-981b-a61b84026e4d" />

10. Accepted the terms and clicked `Next`

<img width="644" height="487" alt="image" src="https://github.com/user-attachments/assets/cbd62cc8-6366-4405-98d9-4f22014fac15" />

11. It asked me what type of install I want to perform - I chose `Custom: Install Windows only (advanced)`
> **I chose this because I am doing a completely new, fresh install**

<img width="644" height="483" alt="image" src="https://github.com/user-attachments/assets/a3073c63-4aa6-4b4d-a03b-c8331c683e1a" />

12. Gave me the option to allocate disk space, since I'm only using one drive I just clicked `Next`

<img width="643" height="484" alt="image" src="https://github.com/user-attachments/assets/9515c285-e9df-4dd1-ac8f-fcb69209d85f" />

13. Selected `United States` as my region, selected `Yes`, selected `US` as my keyboard layout, selected `Yes`, and selected `Skip` on adding a second keyboard layout

<img width="1024" height="771" alt="image" src="https://github.com/user-attachments/assets/1b7a4cf8-97d0-41cd-a243-b5c5e62fb5c4" /><img width="1021" height="771" alt="image" src="https://github.com/user-attachments/assets/d3acbddf-ea42-44f2-93d3-743192bac60f" /><img width="1023" height="766" alt="image" src="https://github.com/user-attachments/assets/8aaf4d94-ddac-457c-8094-8907a56f85dc" />

14. Once it loaded the `Sign in with Microsoft` page, and I clicked on `Domain join instead`

<img width="1019" height="795" alt="image" src="https://github.com/user-attachments/assets/817cb6ed-8742-4b65-8ffc-e13e5face675" />

15. Created a local account called `admin` and followed the prompts to setup a password and create security questions/answers

<img width="1020" height="794" alt="image" src="https://github.com/user-attachments/assets/eda23828-b350-41dd-9566-0784aa6826fe" />

16. This is just my preference, but I toggle all privacy settings off and click `Accept`

<img width="1026" height="798" alt="image" src="https://github.com/user-attachments/assets/9399b9b0-0e87-46e5-9d44-0c4c9b059dc4" />

17. I clicked `Not now` on the Cortana assistant pop-up as I'm not planning on utilizing it in this homelab

<img width="1019" height="795" alt="image" src="https://github.com/user-attachments/assets/1b529392-64e2-48ed-8fe7-ed9776418755" />

18. Once it finished installing, I right-clicked on the Windows icon, selected `System`, clicked on `Rename this PC`, renamed it to `helpdesk`, clicked `Next`, and clicked `Restart now`

<img width="1019" height="800" alt="image" src="https://github.com/user-attachments/assets/bf1d0178-eae4-4ead-a7a5-879ae2918d4f" /><img width="1021" height="806" alt="image" src="https://github.com/user-attachments/assets/9c61fd0d-9f1c-44a8-b8a3-023bcdb3dfa0" /><img width="1020" height="805" alt="image" src="https://github.com/user-attachments/assets/6b3c7b32-50c0-4a4a-a5fa-408bfc2a52fd" /><img width="684" height="220" alt="image" src="https://github.com/user-attachments/assets/6a5a612a-917d-41ec-ad1a-ceda3e92ae65" />


19. Once the VM came back on, I clicked on `File`, Clicked `Close`, selected the option `Send the shutdown signal`, and clicked `OK`

<img width="1031" height="807" alt="image" src="https://github.com/user-attachments/assets/02acf315-ffed-4811-b8c0-419706cf3b85" /><img width="1020" height="802" alt="image" src="https://github.com/user-attachments/assets/ccab27fb-6aaa-4b30-a1ec-307118c9b92e" />

20. Right-clicked on the `helpdesk` VM, selected `Clone`, named the clone version to `Staff`, selected `Full Clone`, and then I clicked `Finish`
>**This is so I can have an instance of it ready to go in case I need it in the future**

<img width="869" height="778" alt="image" src="https://github.com/user-attachments/assets/32c3e1a8-2b8b-4ba5-8264-1d8c94489196" /><img width="624" height="412" alt="image" src="https://github.com/user-attachments/assets/312ae1d2-1194-462f-bcdf-1f3c8194b0c0" />

Windows 10 VM has been successfully installed!

---

## Installing Active Directory and adding Win10 VM to Active Directory
[↑ Back to Table of Contents](#table-of-contents)

1. Opened `DC` VM
2. Within `DC`, clicked on `Server Manager`, clicked on the `Manage` tab, selected `Add Roles and Features`,and clicked `Next`

<img width="1022" height="804" alt="image" src="https://github.com/user-attachments/assets/b727c753-edd6-4214-be7c-a658ac2a0041" /><img width="1027" height="801" alt="image" src="https://github.com/user-attachments/assets/53ac161f-498d-4faa-b1c6-245f7000aec1" /><img width="786" height="561" alt="image" src="https://github.com/user-attachments/assets/6d13cabb-9f77-43ca-b210-bb7b78e238ce" />

3. Clicked `Role-based or feature-based installation`, clicked `Next`, and clicked `Next` again

<img width="1025" height="809" alt="image" src="https://github.com/user-attachments/assets/d0955496-065b-4335-b92d-5dbb9e3dd107" /><img width="1027" height="810" alt="image" src="https://github.com/user-attachments/assets/5449eeba-a841-4a6e-801b-909520a3addc" />

4. Clicked on the option `Active Directory Domain Services` and clicked `Add Features`

<img width="791" height="564" alt="image" src="https://github.com/user-attachments/assets/0da9a0e6-440c-44cf-8d1e-739f1c7d32dc" /><img width="789" height="560" alt="image" src="https://github.com/user-attachments/assets/ed320e85-5e04-4f8b-af0e-400a30ecef63" />

5. Clicked `Next`, clicked `Next` again, clicked `Install`, and then clicked `Close`

<img width="790" height="564" alt="image" src="https://github.com/user-attachments/assets/ad75c68b-49e6-4463-a437-d481390b49e0" /><img width="790" height="562" alt="image" src="https://github.com/user-attachments/assets/a1226094-db8c-44a5-b845-a8559f1ae6a5" /><img width="790" height="562" alt="image" src="https://github.com/user-attachments/assets/7b9e392d-0bd6-4080-8125-8bb731e806d6" /><img width="790" height="565" alt="image" src="https://github.com/user-attachments/assets/423eb00c-8d09-4480-9c38-715aa0f405d2" /><img width="791" height="564" alt="image" src="https://github.com/user-attachments/assets/37470a4f-9c99-4e29-9323-e34c34370e2d" />

6. Clicked on the option `Promote server to domain controller`, selected `Add a new forest`, named the Root domain name `beklabs.org`, clicked `Next`, created a strong password, clicked `Next`, and clicked `Next` again

<img width="1019" height="771" alt="image" src="https://github.com/user-attachments/assets/fea95d4a-f62d-4f0f-b13c-b07f2208dcfb" /><img width="763" height="562" alt="image" src="https://github.com/user-attachments/assets/72c8ada8-e306-46a7-8358-456c0359a9e0" /><img width="765" height="565" alt="image" src="https://github.com/user-attachments/assets/aa0fc3f2-fc36-4e1c-8e84-f44c734d432b" /><img width="766" height="563" alt="image" src="https://github.com/user-attachments/assets/1fff0b78-0971-4cb6-b158-23c7b337052e" />

7. I made my NetBIOS name `BLABS`, clicked `Next`, clicked `Next` again, and then clicked `Next` again

<img width="764" height="562" alt="image" src="https://github.com/user-attachments/assets/14fb6d46-6bd2-432f-8f75-22a5819655fb" /><img width="766" height="564" alt="image" src="https://github.com/user-attachments/assets/3a761af7-27eb-4190-93e9-206fda823c1a" /><img width="766" height="563" alt="image" src="https://github.com/user-attachments/assets/1ec51c6b-31ad-4646-9140-d9aeaa05ee87" />

8. Clicked `Install` and then restarted the VM

<img width="765" height="564" alt="image" src="https://github.com/user-attachments/assets/f495f7f4-6e76-46a6-b3e1-a62775cc175a" />

9. Waited for the Server Manager to populate and then clicked on `Tools` and then selected `Active Directory Users and Computers`

<img width="1027" height="769" alt="image" src="https://github.com/user-attachments/assets/98058561-d8e5-40f3-ad6a-5876780261ba" />

10. Right-clicked on the `Users` folder, hovered over `New` and then selected `User`, and created a new user named `helpdesk blabs`
>**Make sure to uncheck `User must change password at next logon`**

<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/6e02746a-7f5c-4a21-8c39-e64d0e4f21cb" /><img width="440" height="378" alt="image" src="https://github.com/user-attachments/assets/a2e0ca7b-d06a-4923-847c-641451ae9f5d" /><img width="440" height="382" alt="image" src="https://github.com/user-attachments/assets/4b8345e5-f3e8-4e36-bd08-5001cc7bab2b" /><img width="444" height="382" alt="image" src="https://github.com/user-attachments/assets/2d6a8257-cba4-4ad9-a421-e4a87c2fe65a" />

11. Right-clicked on the new user `helpdesk blabs` and selected `Properties`, clicked `Member Of` and added the group `domain admins` to `helpdesk blabs`, and clicked `OK`, clicked `Apply` and `OK`
>**This makes this account an admin account**

<img width="756" height="532" alt="image" src="https://github.com/user-attachments/assets/28e2e881-e2b4-43e3-bdfe-f139c0fab032" /><img width="837" height="535" alt="image" src="https://github.com/user-attachments/assets/577d44ad-a911-45eb-98c8-2b048751ff16" /><img width="765" height="537" alt="image" src="https://github.com/user-attachments/assets/e4d2e578-b990-4bbc-b005-980a4a468624" />

12. Opened the `helpdesk` VM, opened Windows Start, typed `advanced` and clicked on the option `View advanced system settings`

<img width="1032" height="774" alt="image" src="https://github.com/user-attachments/assets/bba05a07-e8ce-4a8d-88af-3a577a5b6d71" />

13. Clicked on `Computer Name`, selected `Change`, selected the option `Domain`, typed in `beklabs.org`, amd clicked `OK`

<img width="421" height="478" alt="image" src="https://github.com/user-attachments/assets/b20c59be-f968-40de-aad9-ec3f7077df92" /><img width="419" height="476" alt="image" src="https://github.com/user-attachments/assets/c1a0c944-bc7d-4e54-9366-94ff383c270d" />

> [!CAUTION]
> **Connection Error:** If you see *"An AD DC for the domain 'beklabs.org' could not be contacted,"* this is a DNS mismatch. 
<img width="475" height="479" alt="image" src="https://github.com/user-attachments/assets/52db88fa-febc-427d-95eb-59dac60df889" />

>**Quick Fix:** Manually set the Helpdesk VM's **Preferred DNS** to the DC's IPv4 address. See [Troubleshooting](#troubleshooting) for the full resolution.

14. Entered the credentials for `helpdesk blabs` and successfully joined the `beklabs.org` domain

<img width="422" height="481" alt="image" src="https://github.com/user-attachments/assets/7cba952b-5881-4f0d-a1e7-ab19bb4caa0c" />

15. Restarted the VM

---

## Troubleshooting
[↑ Back to Table of Contents](#table-of-contents)

### **Issue: Active Directory Domain Controller (AD DC) Not Contacted**
> **Error Message:** *"An AD DC for the domain 'beklabs.org' could not be contacted. Ensure that the domain name is typed correctly. If the name is correct, click Details for troubleshooting information."*

1. On the `DC` VM, clicked Windows Start icon, typed `CMD`, opened `CMD` and typed `ipconfig /all` to find the IPv4 address

<img width="1039" height="780" alt="image" src="https://github.com/user-attachments/assets/cfd2f28d-54bb-4449-aeaa-cc32d3858302" /><img width="1021" height="768" alt="image" src="https://github.com/user-attachments/assets/10bd030a-3ca4-4376-ad4f-464a90af16a0" />

2. On the `helpdesk` VM, right-clicked the network icon in the bottom right-hand side of the screen, selected `Network & Internet` settings and selected `Change adapter options`

<img width="1025" height="769" alt="image" src="https://github.com/user-attachments/assets/51af0398-c7a5-4571-9bd5-747a64dfde4b" /><img width="1023" height="770" alt="image" src="https://github.com/user-attachments/assets/0c40dfed-649a-4a19-a5be-51f05e71199a" /><img width="806" height="640" alt="image" src="https://github.com/user-attachments/assets/9fa1a91a-61bc-4d03-b039-51934921c21b" />

3. Right-clicked on the `Ethernet` option and selected `Properties`

<img width="791" height="597" alt="image" src="https://github.com/user-attachments/assets/7c0731da-d709-4510-8435-b0e0dfad623e" />

4. Unchecked the `Internet Protocol Version 6 (TCP/IPv6)` to prevent protocol conflicts

<img width="368" height="473" alt="image" src="https://github.com/user-attachments/assets/e119f884-75ed-4eb8-8308-85eef1bb1cba" />

5. Selected `Internet Protocol Version 4 (TCP/IPv4)` and clicked `Properties`

<img width="366" height="473" alt="image" src="https://github.com/user-attachments/assets/6565d4d6-54ac-4995-8034-60294d69b42e" />

6. Selected `Use the following DNS server addresses` and inputted the `DC` IPv4 address into the `Preferred DNS server` field, and clicked `OK` to save the changes

<img width="404" height="465" alt="image" src="https://github.com/user-attachments/assets/e8ad0887-eb09-4447-ac1a-45c28e1d2bf8" />

7. Re-attempted the domain join; the login popup appeared immediately, and the `helpdesk` VM successfully joined the `beklabs.org` domain

<img width="462" height="303" alt="image" src="https://github.com/user-attachments/assets/1fa8cc63-7ecb-4341-a630-d0e37cc70c17" /><img width="422" height="481" alt="image" src="https://github.com/user-attachments/assets/86011923-07ee-4228-81ce-ebb1af2ec033" />

---

## Conclusion
[↑ Back to Table of Contents](#table-of-contents)

The successful deployment of the `beklabs.org` domain serves as a foundational step in my journey as an IT Admin. This lab provided hands-on experience with the intricacies of Active Directory and the vital role that DNS plays in a Windows environment. 

**Key Takeaways:**
* The most significant challenge was the domain-join failure, which reinforced that AD DS is entirely dependent on correct DNS routing. Learning to manually point a client to a DC's static IPv4 is a fundamental skill in troubleshooting enterprise networks.
* Disabling IPv6 and creating Administrative User groups reflects professional security and networking standards.
* By creating clones (`Serverimage` and `Staff`), the lab is now ready for future expansion, such as implementing Group Policy Objects (GPOs), setting up a DHCP server, or testing software deployments.

This environment now stands as a ready-to-use playground for advanced administrative tasks and security testing.
