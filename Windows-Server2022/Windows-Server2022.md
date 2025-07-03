# 🖥️ Windows Server 2022

## VM Specs
- OS: Windows Server 2022 (Trial)
- IP: `10.10.10.1` (Static)
- Role: Domain Controller

--- 
## Setup Steps
1. Installed **Active Directory Domain Services (AD DS)** via Server Manager
2. Promoted server to **Domain Controller**
3. Created new **forest and domain**: `valetech.com`
4. Rebooted after promotion
5. Verified **AD tools** (e.g., Active Directory Users and Computers, DNS Manager)
6. Changed network adapter to Host-only for internal communication between Server and VMs
7. Set Static IP: `10.10.10.1` and DNS: `10.10.10.1` for internal network

--- 
## Group Policy Configuration - Enable Ping (ICMP) for Domain
1. Created a GPO named `Allow ICMPv4 Echo for Domain`
2. Configured a custom inbound firewall rule:
	- Protocol: ICMPv4
	- Type: Echo Request
	- Action: Allow
	- Profile: Domain Only
3. Linked the GPO to the **valetech.com domain root**, so it applies to all domain-joined machines
4. On Clients (Desktop1, Desktop2), ran on `cmd`: 
	- `gpupdate /force

--- 
## File Sharing & Drive Mapping Setup
### 1. Shared Folders Creation 
- Created two folders using **Server Manager**
	- `\\server2022\HR`
	- `\\server2022\Personal`
- Configured sharing and NTFS permissions: 
	- `HR` Group -> Read/Write access to `HR` folder
	- `Personal` Group -> Read/Write access to `Personal` folder

📷shared-folders-server-manager.png

### 2. Active Directory: Group and User Management 
- Created Security Groups: `HR`, `Personal`
- Added users to appropriate groups: 
	- `helpdesk` -> `HR`, `Personal`
	- `Peter` -> `Personal`

📷security-groups-ad.png

### 3. Network Drive Mapping (Two methods)
- **Method 1: Manual Mapping (Client Side)**
	- On the client, opened **File Explorer** > Right-click `This PC` > `Map Network Drive`
	- Select a driver letter (e.g., `P:`, and mapped to `\\server2022\HR`
- **Method 2: Via Active Directory (User Profile Mapping)**
	- Opened user properties (e.g., `Peter`) in ADUC > `Profile` tab
	- Under Connect, assigned: 
	- `Drive: P:      To: \\server2022\Personal\%username%`

📷mapped-drives.png

--- 
## Group Policy Configuration - User Restrictions
- Created a new Group Policy Object: `Task Manager`
- In `User Configuration -> Administrative Templates -> System -> Ctrl+Alt-Del Options`: 
	- Enabled `Remove Task Manager`
	- Enabled `Remove Change Password`
- Linked the GPO to the `HR` OU and enforce it

📷group-policy-task-manager.png

- On Server Manager -> Group Policy Management, ran `Group Policy Results Wizard` to implement RSoP on `peter on Desktop2`

📷group-policy-report-peter-desktop2.png

---
## PDQ Deploy - Software Deployment via Shared Folder
- Inserted **Guest Additions CD image** in Virtual box 
- Configured **Shared Folder** between host and Desktop2 VM:
	- Shared Path: Host Folder containing `PDQDeploySetup.exe`
	- Accessed it from VM under `\\VBOXSVR`
- Installed PDQ 
- Used PDQ Deploy to create a deployment package for: 
	- **PDFsam Basic 5.3.1**
- Deployed the software successfully to Desktop2

📷pdq-deploy.png
📷pdq-deployment-pdfsambasic-client.png

---
### cmd commands
- `ipconfig` Displays basic IP address, subnet mask, and default gateway for network adapters.
- `ipconfig /all` Shows detailed network configuration info, including MAC address, DHCP status, DNS servers, and more
- `net use` Connects, lists, or removes shared network drives or resources
- `net user <username> /domain` Displays details about a domain user account (e.g., when the password was last set). Note: Must be run on a PC joined to a domain
- `gpupdate /force` Refresh Group Policy Settings

--- 

