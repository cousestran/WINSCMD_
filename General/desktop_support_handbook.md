# 🖥️ Comprehensive Desktop Support Handbook

## Table of Contents

### 1. Operating System Support
- [1.1 Windows Support](#11-windows-support)
  - [Common Issues & Solutions](#common-issues--solutions-1)
  - [Useful Commands](#useful-commands)
- [1.2 macOS Support](#12-macos-support)
  - [Common Issues & Solutions](#common-issues--solutions-2)
  - [Essential Commands](#essential-commands)

### 2. Email Client Support
- [2.1 Microsoft Outlook](#21-microsoft-outlook)
  - [Configuration](#configuration)
  - [Common Issues](#common-issues)
- [2.2 Webmail Access](#22-webmail-access)
  - [Quick Links](#quick-links)

### 3. Microsoft Office Support
- [3.1 Common Issues & Fixes](#31-common-issues--fixes)
- [3.2 Office Repair](#32-office-repair)

### 4. Hardware Support
- [4.1 Troubleshooting Matrix](#41-troubleshooting-matrix)
- [4.2 Peripheral Setup](#42-peripheral-setup)

### 5. Remote Access Solutions
- [5.1 Supported Tools](#51-supported-tools)
- [5.2 Connection Troubleshooting](#52-connection-troubleshooting)

### 6. Software Deployment
- [6.1 Common Packages](#61-common-packages)
- [6.2 Deployment Script](#62-deployment-script)

### 7. Security Best Practices
- [7.1 Endpoint Protection](#71-endpoint-protection)
- [7.2 Patch Management](#72-patch-management)

### 8. Knowledge Base & Self-Help
- [8.1 Common Solutions](#81-common-solutions)

---

# Comprehensive Desktop Support Handbook

# 1. Operating System Support

## 1.1 Windows Support

### Common Issues & Solutions

### Windows 10/11
| Issue | Troubleshooting Steps | Command/Tool |
|-------|----------------------|--------------|
| Slow Performance | 1. Check Task Manager for resource hogs<br>2. Run disk cleanup<br>3. Disable startup programs | `taskmgr`<br>`cleanmgr`<br>`msconfig` |
| Update Failures | 1. Run Windows Update Troubleshooter<br>2. Reset Windows Update components<br>3. Manually install updates | `msdt /id WindowsUpdateDiagnostic`<br>`net stop wuauserv`<br>Microsoft Update Catalog |
| Blue Screen (BSOD) | 1. Note error code<br>2. Check Event Viewer<br>3. Update drivers | `eventvwr`<br>`verifier` |

### Useful Commands
```batch
# System Information
systeminfo
msinfo32

# Disk Management
diskpart
chkdsk /f /r

# Network Troubleshooting
ipconfig /all
netsh winsock reset
nslookup google.com
```

## 1.2 macOS Support

### Common Issues & Solutions

| Issue | Troubleshooting Steps | Terminal Commands |
|-------|----------------------|-------------------|
| Startup Issues | 1. Safe Boot (Shift)<br>2. Disk Utility First Aid<br>3. NVRAM Reset | `fsck -fy`<br>`diskutil verifyVolume /` |
| Wi-Fi Problems | 1. Create new location<br>2. Remove plist files<br>3. Reset network settings | `sudo rm /Library/Preferences/SystemConfiguration/*.plist` |
| Application Crashes | 1. Check Console logs<br>2. Reinstall app<br>3. Create new user account | `log show --predicate 'process == "AppName"' --last 1h` |

### Essential Commands
```bash
# System Information
system_profiler SPHardwareDataType
diskutil list

# Permission Repair
diskutil resetUserPermissions / `id -u`

# Network Diagnostics
netstat -an | grep LISTEN
lsof -i -P | grep -i "listen"
```

## 2. Email Client Support

### 2.1 Microsoft Outlook
**Configuration**
```
Incoming: outlook.office365.com (IMAP)
Outgoing: smtp.office365.com
Ports: 993 (IMAP), 587 (SMTP)
Authentication: OAuth2
```

**Common Issues**
- **OST/PST Corruption**:
  ```powershell
  # Close Outlook, then:
  SCANPST.EXE "path_to_ost_file"
  ```
- **Profile Rebuild**:
  1. Control Panel > Mail > Show Profiles
  2. Create new profile
  3. Set as default

### 2.2 Webmail Access
**Quick Links**:
- Office 365: [portal.office.com](https://portal.office.com)
- Gmail: [mail.google.com](https://mail.google.com)
- IMAP Settings Guide: [support.example.com/imap](https://support.example.com/imap)

## 3. Microsoft Office Support

### 3.1 Common Issues & Fixes
| Application | Issue | Solution |
|-------------|-------|----------|
| Word | Not Responding | Disable Add-ins > File > Options > Add-ins |
| Excel | Slow Calculation | Formulas > Calculation Options > Manual |
| PowerPoint | Media Playback Issues | File > Info > Optimize Compatibility |
| Outlook | Search Not Working | Rebuild Index: Control Panel > Indexing Options |

### 3.2 Office Repair
1. **Quick Repair**:
   - Control Panel > Programs > Office > Change > Quick Repair

2. **Online Repair**:
   - Control Panel > Programs > Office > Change > Online Repair

## 4. Hardware Support

### 4.1 Troubleshooting Matrix
| Component | Test | Tools |
|-----------|------|-------|
| RAM | Windows Memory Diagnostic | `mdsched.exe` |
| HDD/SSD | S.M.A.R.T. Check | CrystalDiskInfo |
| CPU | Stress Test | Prime95 |
| GPU | Benchmark | 3DMark/FurMark |
| Network | Packet Loss Test | `ping -t 8.8.8.8` |

### 4.2 Peripheral Setup
**Printers**:
1. Download latest driver
2. Run installer as admin
3. Test print

**Docking Stations**:
1. Update firmware
2. Connect power first
3. Attach peripherals
4. Connect laptop

## 5. Remote Access Solutions

### 5.1 Supported Tools
| Tool | Use Case | Authentication |
|------|----------|----------------|
| TeamViewer | Quick Support | Password-based |
| AnyDesk | Cross-platform | Password/2FA |
| Windows RDP | Internal Network | Domain Credentials |
| Splashtop | Multi-monitor | SSO/2FA |

### 5.2 Connection Troubleshooting
1. **Check Network**:
   ```powershell
   Test-NetConnection -ComputerName [IP] -Port 3389
   ```
2. **Verify Services**:
   ```batch
   sc query TermService
   net start TermService
   ```
3. **Firewall Rules**:
   ```powershell
   Get-NetFirewallRule -DisplayGroup "Remote Desktop"
   ```

## 6. Software Deployment

### 6.1 Common Packages
| Software | Silent Install Switch | Notes |
|----------|----------------------|-------|
| Chrome | `/silent /install` | Auto-updates |
| Adobe Reader | `/sAll /rs /msi EULA_ACCEPT=YES` | Disable updater |
| 7-Zip | `/S` | System path update |

### 6.2 Deployment Script
```powershell
# Deploy-Software.ps1
param(
    [string]$ComputerName,
    [string]$Software
)

$softwareMap = @{
    'chrome'  = @{
        url = 'https://dl.google.com/chrome/install/latest/chrome_installer.exe'
        args = '/silent /install'
    }
    '7zip'    = @{
        url = 'https://www.7-zip.org/a/7z2107-x64.exe'
        args = '/S'
    }
}

if ($softwareMap.ContainsKey($Software)) {
    $tempFile = "$env:TEMP\$Software-installer.exe"
    Invoke-WebRequest -Uri $softwareMap[$Software].url -OutFile $tempFile
    Start-Process -FilePath $tempFile -ArgumentList $softwareMap[$Software].args -Wait
    Remove-Item $tempFile
}
```

## 7. Security Best Practices

### 7.1 Endpoint Protection
- Enable Windows Defender
- Regular scan schedule
- Update signatures daily

### 7.2 Patch Management
- Critical updates: 7-day SLA
- Feature updates: 30-day testing
- Third-party patching: Monthly

## 8. Knowledge Base & Self-Help

### 8.1 Common Solutions
- **Password Reset**: [password.example.com](https://password.example.com)
- **Software Portal**: [software.example.com](https://software.example.com)
- **VPN Setup**: [vpn.example.com/setup](https://vpn.example.com/setup)

### 8.2 Troubleshooting Guides
1. [Wi-Fi Connection Issues](#)
2. [Printer Installation](#)
3. [Email Configuration](#)
4. [Software Installation](#)

## 9. Escalation Procedures

### 9.1 When to Escalate
- Hardware failure
- Data loss
- Security incidents
- Recurring issues

### 9.2 Required Information
1. Error messages
2. Troubleshooting steps taken
3. User impact
4. Screenshots/logs

## 10. Quick Reference

### 10.1 Common Ports
| Service | Port | Protocol |
|---------|------|----------|
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| RDP | 3389 | TCP |
| SSH | 22 | TCP |
| SMB | 445 | TCP |

### 10.2 System Utilities
| Tool | Purpose | Command |
|------|---------|---------|
| System File Checker | Repair system files | `sfc /scannow` |
| DISM | Repair Windows image | `DISM /Online /Cleanup-Image /RestoreHealth` |
| Event Viewer | Check system logs | `eventvwr` |
| Resource Monitor | Real-time system stats | `resmon` |

---
*Document Version: 1.0  
Last Updated: 2025-09-20*
