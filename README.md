# Setup-and-Use-a-Firewall-on-Windows-Linux
# Firewall Configuration Guide

This document outlines the steps to configure a firewall on Windows (using Windows Defender Firewall) and Linux (using UFW), including listing rules, blocking a specific port (e.g., Telnet on port 23), testing, allowing SSH (Linux only), removing the test rule, and summarizing how firewalls filter traffic.

---

## 1. Open Firewall Configuration Tool

### Windows (Windows Defender Firewall)
- **GUI**: Navigate to Control Panel > System and Security > Windows Defender Firewall > Advanced Settings.
- **PowerShell**: Run `control firewall.cpl` to open the GUI or use `netsh advfirewall` commands.

### Linux (UFW)
- Open a terminal and ensure UFW is installed: `sudo apt install ufw` (Debian/Ubuntu).
- Access UFW: `sudo ufw status`.

---

## 2. List Current Firewall Rules

### Windows
- **GUI**: In "Windows Defender Firewall with Advanced Security," view rules under "Inbound Rules" or "Outbound Rules."
- **PowerShell**:
  ```powershell
  Get-NetFirewallRule | Where-Object {$_.Direction -eq "Inbound"} | Format-Table Name, Enabled, Action, Direction

 ## 3. Add a Rule to Block Inbound Traffic on Port 23 (Telnet)

### Windows
- **GUI**:
In "Windows Defender Firewall with Advanced Security," go to Inbound Rules > New Rule.
Select "Port" > Next > TCP > Specific local ports: 23.
Choose "Block the connection" > Next.
Apply to all profiles (Domain, Private, Public) > Next.
Name: "Block Telnet Port 23" > Finish.
### Linux (UFW)
- **Block port 23**:
  sudo ufw deny 23/tcp

## 4. Test the Rule by Connecting to Port 23

  ### Locally (Windows/Linux)
  **Test with**:
  telnet localhost 23

 ## 5. Add Rule to Allow SSH (Port 22) - Linux Only
 ### Linux (UFW)
  **Allow SSH**:
    Sudo ufw allow 22/tcp
    **Verify**:
    Sudo ufw status
