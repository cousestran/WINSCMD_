# ⚡ Quick Reference Guide for IT Support

## Table of Contents

### 1. System Information
- 1.1 Common System Commands
  - Windows Commands
  - macOS Commands
- 1.2 Network Troubleshooting
  - Basic Connectivity
  - Advanced Network Tools

### 2. Quick Fixes
- 2.1 Common Issues & Solutions
  - Slow Computer
  - No Internet
  - Printer Not Working
  - Application Crashes

### 3. Escalation Matrix
- 3.1 When to Escalate
- 3.2 Contact Information

### 4. Documentation Links
- 4.1 Internal Resources
- 4.2 External References

### 5. Common Procedures
- 5.1 Password Reset
- 5.2 Account Unlock
- 5.3 Remote Assistance

### 6. Quick Scripts
- Windows Scripts
- macOS Scripts
- Network Scripts

### 7. Error Code Reference
- Common Error Messages
- Troubleshooting Steps

### 8. Security Protocols
- Incident Response
- Security Best Practices

### 9. Hardware Reference
- Minimum System Requirements
- Hardware Diagnostics

### 10. Software Management
- Installation Guides
- Update Procedures

## 1. System Information

### 1.1 Common System Commands
```bash
# Windows
systeminfo               # System configuration
msinfo32                 # GUI system information
winver                   # Windows version
ver                      # OS version

# macOS
sw_vers                  # OS version
system_profiler SPHardwareDataType  # Hardware info
diskutil list            # Disk information
```

### 1.2 Network Troubleshooting
```bash
# Basic Connectivity
ping 8.8.8.8             # Test internet connection
tracert google.com       # Trace network path
nslookup google.com      # DNS resolution

# Advanced
netstat -ano             # Active connections
ipconfig /all           # Network configuration (Windows)
ifconfig                # Network configuration (macOS/Linux)
netsh winsock reset      # Reset network stack (Windows)
```

## 2. Quick Fixes

### 2.1 Common Issues & Solutions
| Symptom | Quick Fix |
|---------|-----------|
| **Slow Computer** | 1. Check Task Manager for high CPU/memory usage<br>2. Run disk cleanup (`cleanmgr`)<br>3. Disable startup programs (`msconfig`) |
| **No Internet** | 1. Check physical connections<br>2. Restart router/modem<br>3. Run network troubleshooter |
| **Printer Not Working** | 1. Check power/cables<br>2. Set as default printer<br>3. Restart print spooler (`services.msc` → Spooler) |
| **Application Crashes** | 1. Update application<br>2. Reinstall application<br>3. Check Event Viewer for errors |

## 3. Escalation Matrix

### 3.1 When to Escalate
- System-wide outages
- Security incidents
- Data loss/corruption
- Repeated unresolved issues
- Requests requiring higher privileges

### 3.2 Contact Information
| Team | Contact | Hours | Escalation Path |
|------|---------|-------|-----------------|
| Network | x4357 (24/7) | 24/7 | On-call rotation |
| Security | soc@example.com | 24/7 | PagerDuty #123 |
| Server Admin | server-team@example.com | 8-5 | Ticket system |
| Application Support | appsupport@example.com | 8-8 | Priority queue |

## 4. Documentation Links

### 4.1 Internal Resources
- [IT Knowledge Base](https://kb.example.com)
- [System Status Dashboard](https://status.example.com)
- [Password Reset Portal](https://password.example.com)
- [Software Downloads](https://software.example.com)

### 4.2 External References
- [Microsoft Docs](https://docs.microsoft.com)
- [Apple Support](https://support.apple.com)
- [Ubuntu Documentation](https://help.ubuntu.com)
- [Cisco Support](https://www.cisco.com/c/en/us/support/index.html)

## 5. Common Procedures

### 5.1 Password Reset
1. Verify user identity
2. Reset in Active Directory:
   ```powershell
   Set-ADAccountPassword -Identity username -NewPassword (ConvertTo-SecureString "TempP@ss123" -AsPlainText -Force) -Reset
   Set-ADUser -Identity username -ChangePasswordAtLogon $true
   ```
3. Inform user of temporary password

### 5.2 Account Unlock
```powershell
Unlock-ADAccount -Identity username
```

### 5.3 Remote Assistance
```bash
# Windows Quick Assist
msdt.exe -id WindowsRemoteAssistanceDiagnostic

# Microsoft Remote Desktop
mstsc /v:computername
```

## 6. Quick Scripts

### 6.1 Check Disk Space (Windows)
```powershell
Get-PSDrive -PSProvider 'FileSystem' | 
    Select-Object Name, @{Name="Used(GB)";Expression={[math]::Round($_.Used/1GB,2)}}, 
                 @{Name="Free(GB)";Expression={[math]::Round($_.Free/1GB,2)}}, 
                 @{Name="Total(GB)";Expression={[math]::Round(($_.Used + $_.Free)/1GB,2)}}
```

### 6.2 List Installed Software
```powershell
# Windows
Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | 
    Select-Object DisplayName, DisplayVersion, InstallDate | 
    Sort-Object DisplayName | 
    Format-Table -AutoSize

# macOS
system_profiler SPApplicationsDataType | grep -E 'Location:|Version:'
```

## 7. Common Ports

| Service | Port | Protocol |
|---------|------|----------|
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| RDP | 3389 | TCP |
| SSH | 22 | TCP |
| SMTP | 25, 587 | TCP |
| IMAP | 143, 993 | TCP |
| DNS | 53 | TCP/UDP |
| DHCP | 67, 68 | UDP |

## 8. Keyboard Shortcuts

### 8.1 Windows
- `Win + R`: Run dialog
- `Win + E`: File Explorer
- `Win + X`: Quick Link menu
- `Win + V`: Clipboard history
- `Win + .`: Emoji picker
- `Ctrl + Shift + Esc`: Task Manager

### 8.2 macOS
- `Cmd + Space`: Spotlight
- `Cmd + W`: Close window
- `Cmd + Q`: Quit application
- `Cmd + ,`: Preferences
- `Cmd + Shift + .`: Show hidden files
- `Cmd + Option + Esc`: Force Quit

## 9. Troubleshooting Flow

### 9.1 Basic Troubleshooting Steps
1. **Identify** the exact issue
2. **Reproduce** the problem
3. **Isolate** the cause
4. **Resolve** the issue
5. **Document** the solution

### 9.2 Common Error Messages
| Error | Likely Cause | Solution |
|-------|--------------|----------|
| "DNS_PROBE_FINISHED_NXDOMAIN" | DNS resolution failed | Flush DNS (`ipconfig /flushdns`) |
| "No Boot Device Found" | HDD/SSD not detected | Check connections, BIOS settings |
| "Invalid username or password" | Credentials incorrect | Reset password, check Caps Lock |
| "IP Address Conflict" | Duplicate IP on network | Release/Renew IP (`ipconfig /release`, `ipconfig /renew`) |

## 10. Documentation Standards

### 10.1 Ticket Documentation
- Clear, concise problem description
- Steps to reproduce
- Error messages (verbatim)
- Troubleshooting steps taken
- Resolution details

### 10.2 Knowledge Base Articles
- Problem statement
- Affected systems/users
- Step-by-step solution
- Screenshots if helpful
- Related articles

---
*Document Version: 1.0  
Last Updated: 2025-09-20*
