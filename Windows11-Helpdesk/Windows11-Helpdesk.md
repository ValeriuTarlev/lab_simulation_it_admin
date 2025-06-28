# 🖥️ Windows 11 Helpdesk VM Setup

### Specs
- OS: Windows 11
- CPU: 2 cores
- RAM: 4 GB
- Disk: 80 GB
- IP Address: `10.10.10.10` 
- Joined Domain: valetech.com

### Setup Steps
1. Installed Windows 11 Pro clean
2. Enabled built-in Administrator account
3. Set strong administrator password
4. Changed network adapter to **Host-only Adapter** for internal communication between Server and VMs
5. Set Static IP: `10.10.10.10`, DNS: `10.10.10.1` (Server DC)

### Tools and RSAT Installation
1. Installed RSAT (Remote Server Administration Tools) via: 
	- `Settings -> System -> Optional Features -> Add an optional feature`
2. Installed: 
	- AD DS, ADUC, GPMC, DHCP, Server Manager, etc.
3. Installed Chrome/TeamViewer for remote access

### Domain and AD Setup
1. Renamed PC to `Desktop1`
2. Joined `Desktop1` to domain: `valetech`
3. Logged in using domain user: `valetech\helpdesk`
4. Created Organizational Units (OUs): `HR`, `IT`
5. Added test users: `Peter`, `helpdesk`
6. Configured a Group Policy for **Account Lockout Policy**:
	- Lockout Threshold: 4 Invalid logon attempts
	- Lockout duration: 30 minutes
	- Reset account lockout counter after: 10 minutes
	- Administrator lockout: Enabled


### Tasks:
- Joined to domain
- Tested GPO application
- Logged in with AD user
