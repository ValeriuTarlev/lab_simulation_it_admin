# 🖥️ Windows 11 Helpdesk VM Setup

## Specs
- OS: Windows 11
- CPU: 2 cores
- RAM: 4 GB
- Disk: 80 GB
- IP Address: `10.10.10.10` 
- Joined Domain: valetech.com

---
## Setup Steps
1. Installed Windows 11 Pro clean
2. Enabled built-in Administrator account
3. Set strong administrator password
4. Changed network adapter to **Host-only Adapter** for internal communication between Server and VMs
5. Set Static IP: `10.10.10.10`, DNS: `10.10.10.1` (Server DC)

--- 
## Tools and RSAT Installation
1. Installed RSAT (Remote Server Administration Tools) via: 
	- `Settings -> System -> Optional Features -> Add an optional feature`
2. Installed: 
	- AD DS, ADUC, GPMC, DHCP, Server Manager, etc.
3. Installed Chrome/TeamViewer for remote access

--- 
## Domain and AD Setup
1. Renamed PC to `Desktop1`
2. Joined `Desktop1` to domain: `valetech`
3. Logged in using domain user: `valetech\helpdesk`
4. Created Organizational Units (OUs): `HR`, `IT`
5. Added test users: `Peter`, `helpdesk` 

📷`active-directory-users.png`

6. Configured a Group Policy for **Account Lockout Policy**:
	- Lockout Threshold: 4 Invalid logon attempts
	- Lockout duration: 30 minutes
	- Reset account lockout counter after: 10 minutes
	- Administrator lockout: Enabled

📷`account-lockout-policy.png `

--- 
## Account
### 1. Unlock a Locked-Out Account
- Double click the user -> Go to `Account` tab
- `Unlock account` -> `Apply`

📷`unlock-account-helpdesk.png `

### 2. Disable a User Account 
- Right-click the user -> `Disable Account`

📷`disable-account.png `

### 3. Reset a Password 
- Right-click the user -> `Reset Password`
- Enter new password

📷`reset-password.png `

### 4. Password and Account Expiration
- **Prevent expiration: **
	- Double click the user ->  `Account` tab -> Check `Password never expires`
- **Allow expiration**
	- Uncheck `Password never expires`

📷`password-expiration-setting.png`

### 5. Force User to Change Password at Next Logon
- Right-click the user -> `Reset Password` 
- Set temporary password
- Check `User must change password at next logon`

📷`force-password-change.png`

--- 
## Remote Access Tools
### 1. Remote Desktop Connection to Desktop2
- Used **Remote Desktop Connection** to connect to:  
  `Desktop2.valetech.com`
- Logged in as `valetech\helpdesk
- Opened **File Explorer** and navigate to: 
	`\\Desktop2\c$\Users\Peter\Desktop`
- Created a test folder on Desktop2's desktop to verify administrative access  

📷 `remote-desktop-connection.png`

### 2. Remote Registry Access 
- Enabled **Remote Registry** service (Automatic) on both Desktop 1 and Desktop2
- Enabled **File and Printer Sharing (SMB-In)** on Desktop2
- From Desktop 1 
	- Opened `regedit`
	- Navigated to `File -> Connect Network Registry...`

## 3. Remote Assistance via MSRA
- Accessed invitation file from Desktop2 
	*Instructions for generating the file are documented in* `Windows11-Client.md` *(see: Remote Assistance Setup)*
- Opened file and entered the code to establish a remote assistance session

📷 `windows-remote-assistance.png`

--- 