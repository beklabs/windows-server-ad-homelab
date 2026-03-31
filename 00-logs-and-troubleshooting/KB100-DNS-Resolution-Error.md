## **Issue: Active Directory Domain Controller (AD DC) Not Contacted**

---

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

