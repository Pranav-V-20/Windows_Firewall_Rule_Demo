# 🔥 Windows Firewall Rule Demo - Block Port 23 (Telnet)

> Task 4 - Elevate Labs - Cyber Security Intern

This project demonstrates how to configure and test a basic firewall rule on **Windows** to block inbound traffic on **port 23 (Telnet)** using both the GUI and PowerShell.

---

## 🎯 Objective

- Block inbound traffic on TCP port 23 (used by Telnet).
- Test the rule by attempting to connect to port 23.
- Remove the rule to restore the original firewall state.

---

## 🛠 Tools Used

- **Windows Defender Firewall with Advanced Security**
- **PowerShell**
- **Telnet Client** (for testing)

---

## 📋 Steps

### 1. List Current Rules
```powershell
Get-NetFirewallRule | Format-Table Name, Enabled, Direction, Action, DisplayName
````

### 2. Create Block Rule (Port 23)

Run the script:

```powershell
.\block_telnet.ps1
```

Contents:

```powershell
New-NetFirewallRule -DisplayName "Block Telnet Port 23" -Direction Inbound -LocalPort 23 -Protocol TCP -Action Block
```

### 3. Test with Telnet

Enable Telnet client:

```powershell
dism /online /Enable-Feature /FeatureName:TelnetClient
```

Then test:

```cmd
telnet localhost 23
```

You should see:

```
Connecting To localhost...Could not open connection to the host, on port 23: Connect failed
```

### 4. Delete the Rule

Run the script:

```powershell
.\unblock_telnet.ps1
```

Contents:

```powershell
Remove-NetFirewallRule -DisplayName "Block Telnet Port 23"
```

---

## 📸 Screenshots

### Rule Created
![Rule](https://github.com/user-attachments/assets/3b812fe2-9abe-4e1f-8e8d-a604c3e794d6)

### Telnet Blocked
![Telnet](https://github.com/user-attachments/assets/4b06b0da-b1af-47ae-9071-79d0fd36bc37)

---

## 🛡️ Summary

Windows Firewall filters traffic using defined rules for ports, protocols, directions, and profiles. This repo shows how a basic block rule on port 23 can prevent insecure remote access through Telnet.
