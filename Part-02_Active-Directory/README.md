## Installing Active Directory and adding Win10 VM to Active Directory

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

>**Quick Fix:** Manually set the Helpdesk VM's **Preferred DNS** to the DC's IPv4 address. See [Logs & Troubleshooting](#00-logs-and-troubleshooting) for the full resolution.

14. Entered the credentials for `helpdesk blabs` and successfully joined the `beklabs.org` domain

<img width="422" height="481" alt="image" src="https://github.com/user-attachments/assets/7cba952b-5881-4f0d-a1e7-ab19bb4caa0c" />

15. Restarted the VM

---
