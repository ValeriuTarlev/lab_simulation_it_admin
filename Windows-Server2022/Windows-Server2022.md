# 🖥️ Windows Server – Active Directory Setup

**VM Specs:**
- OS: Windows Server 2022 (Trial)
- IP: `10.10.10.1` (Static)
- Role: Domain Controller

### Steps Performed
1. Installed **Active Directory Domain Services (AD DS)** via Server Manager
2. Promoted server to **Domain Controller**
3. Created new **forest and domain**: `valetech.com`
4. Rebooted after promotion
5. Verified **AD tools** (e.g., Active Directory Users and Computers, DNS Manager)
6. Changed network adapter to Host-only for internal communication between Server and VMs
7. Set Static IP: `10.10.10.1` and DNS: `10.10.10.1` for internal network


### cmd commands
- `ipconfig` Displays basic IP address, subnet mask, and default gateway for network adapters.
- `ipconfig /all` Shows detailed network configuration info, including MAC address, DHCP status, DNS servers, and more
- `net use` Connects, lists, or removes shared network drives or resources
- `net user <username> /domain` Displays details about a domain user account (e.g., when the password was last set). Note: Must be run on a PC joined to a domain


