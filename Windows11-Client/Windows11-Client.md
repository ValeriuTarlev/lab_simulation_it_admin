# 🖥️ Windows 11 Client

## Specs
- OS: Windows 11
- CPU: 2 cores
- RAM: 4 GB
- Disk: 80 GB
- IP Address: `10.10.10.11`
- Joined Domain: valetech.com

---
## Setup Steps
1. Installed Windows 11 Pro clean
2. Enabled built-in Administrator account
3. Changed network adapter to **Host-only Adapter** for internal communication between Server and VMs
4. Set Static IP: `10.10.10.1`, DNS: `10.10.10.1` (Server DC)
5. Renamed PC to `Desktop2`
6. Joined `Desktop2` domain: `valetech`
7. Logged in using `valetech\Peter`

--- 
## Remote Access Setup 
### 1. Enabled Remote Desktop 
- Opened: `This PC -> Properties -> Remote Settings`
- Checked `ALlow remote connections to this computer`
- Verified RDP access from Desktop1 (helpdesk)

### 2. Allowed File and Printer Sharing
- Opened **Windows Defender Firewall with advanced settings** 
- Enabled inbound rule: `File and Printer Sharing (SMB-In)`
- Required for: 
	- Remote Registry 
	- Access via `\\Desktop\c$`

### 3. Generated Remote Assistance Invitation 
- Ran `msra` -> Selected **Invite someone you trust** 
- Saved invitation file to Desktop
- Shared code with helper (helpdesk)

📷`windows-remote-assistance.png

--- 
## Group Policy 
- Logged in as `valetech`Peter`
- Opened Task Manager -> Access was **Denied** due to applied Group Policy 
- Verified via `gpupdate /force` 
- Confirmed the policy to remove `Change Password` and `Task Manager` was applied

📷`task-manager-disabled.png

--- 

