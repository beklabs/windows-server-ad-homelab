# 🖥️ Windows Server 2022 & Active Directory Home Lab
**Domain:** `beklabs.org` | **Hypervisor:** Oracle VirtualBox | **Networking:** Bridged Adapter

---

## 📝 Project Overview
This project demonstrates the deployment and administration of a professional Windows Server environment. By virtualizing a **Domain Controller (DC)** and a **Windows 10 Client**, I simulated a real-world enterprise network to master identity management, DNS troubleshooting, and infrastructure security.

---

<img width="644" height="526" alt="network-topology" src="https://github.com/user-attachments/assets/cb1e418c-9290-4502-9ac2-93b90470cd27" />

---

## 🗺️ Project Roadmap
To keep the documentation clean and scalable, this lab is divided into logical phases. Each folder contains detailed step-by-step instructions and screenshots.

### 📁 [00: Logs & Troubleshooting](./00-logs-and-troubleshooting)
* **Focus:** Root Cause Analysis (RCA) and Knowledge Base (KB) articles.
* **Key Fix:** Resolving DNS mismatches and errors during Domain Join.

### 📁 [Part 1: Foundational Lab Setup](./Part-01_Lab-Setup/)
* **Focus:** Hypervisor configuration and base OS deployment.
* **Tasks:** Installing VirtualBox, provisioning Windows Server 2022 (DC) and Windows 10 (Client).

### 📁 [Part 2: Identity & Access Management](./Part-02_Active-Directory/)
* **Focus:** Directory Services and Network Connectivity.
* **Tasks:** Promoting the DC to a Forest, creating Administrative Users, and performing a successful Domain Join.

### 📁 [Part 3: Governance & Security (In Progress)](#)
* **Focus:** Group Policy Objects (GPO) and File System Security.
* **Upcoming:** Enforcing desktop restrictions and managing NTFS permissions.

---

## 🛠️ Technical Stack
* **Virtualization:** Oracle VirtualBox 7.x (Extension Pack enabled)
* **Directory Services:** Active Directory (AD DS), DNS
* **Operating Systems:** Windows Server 2022 Datacenter, Windows 10 Enterprise
* **Tools:** PowerShell, Server Manager, AD Users & Computers

---
