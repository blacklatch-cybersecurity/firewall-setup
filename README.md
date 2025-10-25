# Task 4 – Configure and Use a Firewall

**Objective:** Apply and test inbound/outbound rules on Linux (UFW) and Windows (PowerShell).


## Linux – UFW Commands
```bash
sudo apt update && sudo apt install -y ufw
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Allow SSH (port 22)
sudo ufw allow 22/tcp

# Block Telnet (port 23)
sudo ufw deny 23/tcp

# Check firewall rules
sudo ufw status verbose

Test

nc -vz 127.0.0.1 23    # should fail
telnet 127.0.0.1 23    # should timeout

Remove the test rule

sudo ufw delete deny 23/tcp



Windows – PowerShell Commands

# Block Telnet (port 23)
New-NetFirewallRule -DisplayName "Block Telnet" -Direction Inbound -LocalPort 23 -Protocol TCP -Action Block

# Allow SSH (port 22)
New-NetFirewallRule -DisplayName "Allow SSH" -Direction Inbound -LocalPort 22 -Protocol TCP -Action Allow

# Test
Test-NetConnection -ComputerName 127.0.0.1 -Port 23

# Remove rule
Remove-NetFirewallRule -DisplayName "Block Telnet"



Expected Output

Status: active
To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere
23/tcp                     DENY        Anywhere

Telnet connection → Connection refused ✅

Outcome

Configured and verified firewall rules to control inbound network traffic and block insecure services.


### ➤ Add file → `firewall_commands.txt`
Paste:
```txt
# Linux UFW
sudo ufw status
sudo ufw deny 23/tcp
sudo ufw allow 22/tcp
sudo ufw delete deny 23/tcp

# Windows PowerShell
New-NetFirewallRule -DisplayName "Block Telnet" -Direction Inbound -LocalPort 23 -Protocol TCP -Action Block
Remove-NetFirewallRule -DisplayName "Block Telnet"
