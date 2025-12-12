# 🛠️ First-Level Support Quick Reference Guide

## Table of Contents

1. [Authentication Issues](#1-authentication-issues)
   - [1.1 Password Resets](#11-password-resets)
2. [Network Connectivity](#2-network-connectivity)
   - [2.1 WiFi Connection](#21-wifi-connection)
   - [2.2 Wired Connection](#22-wired-connection)
3. [Email Setup & Issues](#3-email-setup--issues)
   - [3.1 Outlook Configuration](#31-outlook-configuration)
   - [3.2 Common Email Problems](#32-common-email-problems)
4. [Software Support](#4-software-support)
   - [4.1 Common Applications](#41-common-applications)
   - [4.2 Software Installation](#42-software-installation)
5. [Hardware Troubleshooting](#5-hardware-troubleshooting)
   - [5.1 Quick Checks](#51-quick-checks)
   - [5.2 Common Devices](#52-common-devices)
6. [Account Management](#6-account-management)
   - [6.1 New Employee Setup](#61-new-employee-setup)
   - [6.2 Account Modifications](#62-account-modifications)
7. [Remote Support Tools](#7-remote-support-tools)
   - [7.1 Quick Assist (Windows)](#71-quick-assist-windows)
8. [Knowledge Base](#8-knowledge-base)
   - [8.1 Top Solutions](#81-top-solutions)
9. [Escalation Guidelines](#9-escalation-guidelines)
   - [9.1 When to Escalate](#91-when-to-escalate)
   - [9.2 Escalation Information](#92-escalation-information)
10. [Common Commands](#10-common-commands)
    - [10.1 Windows CMD](#101-windows-cmd)
    - [10.2 macOS Terminal](#102-macos-terminal)
11. [Quick Reference Tables](#11-quick-reference-tables)
    - [11.1 Common Ports](#111-common-ports)
    - [11.2 File Paths](#112-file-paths)
12. [Customer Service Tips](#12-customer-service-tips)
    - [12.1 Communication Guidelines](#121-communication-guidelines)
    - [12.2 Difficult Situations](#122-difficult-situations)

---

# First-Level Support Quick Reference Guide

## 1. Authentication Issues

### 1.1 Password Resets
**Steps**:
1. Verify user identity (Full name, ID, department)
2. Guide to self-service: [password.university.edu/reset](https://password.university.edu/reset)
3. If locked out, manually unlock account in Active Directory

**Common Issues**:
- "Account locked" → Unlock in AD
- "Invalid credentials" → Verify username format (firstname.lastname)
- "Password doesn't meet requirements" → Explain requirements

## 2. Network Connectivity

### 2.1 WiFi Connection
```markdown
1. Verify WiFi is enabled (Windows: Win+A > Network icon)
2. Select "UNI-Secure" network
3. Enter username@university.edu and password
4. Accept certificate if prompted
```

### 2.2 Wired Connection
```markdown
1. Check both ends of Ethernet cable
2. Look for amber/green lights on port
3. Run network troubleshooter:
   - Windows: Right-click network icon > Troubleshoot
   - Mac: Apple Menu > System Settings > Network > Assist me
```

## 3. Email Setup & Issues

### 3.1 Outlook Configuration
**IMAP Settings**:
```
Incoming: imap.university.edu
Outgoing: smtp.university.edu
Ports: 993 (IMAP), 587 (SMTP)
Authentication: OAuth2 (preferred) or Basic
```

### 3.2 Common Email Problems
| Symptom | Quick Fix |
|---------|-----------|
| Can't send | Check SMTP settings, verify authentication |
| Can't receive | Verify IMAP settings, check storage quota |
| Sync issues | Rebuild Outlook profile |
| Spam filtering | Whitelist domain, check Junk folder |

## 4. Software Support

### 4.1 Common Applications
| Software | Installation Path | Common Issues |
|----------|-------------------|---------------|
| Zoom | [Zoom Download](https://zoom.us/download) | Audio/Video settings |
| Microsoft 365 | [Office Portal](https://portal.office.com) | Activation errors |
| Adobe Creative Cloud | [Adobe](https://creativecloud.adobe.com) | License limits |
| VPN Client | [VPN Setup](https://vpn.university.edu) | Connection drops |

### 4.2 Software Installation
**Standard Process**:
1. Check if software is in Self-Service Portal
2. Verify user has necessary permissions
3. If admin rights needed, submit ticket with justification

## 5. Hardware Troubleshooting

### 5.1 Quick Checks
```markdown
1. Restart the device
2. Check all cables and connections
3. Verify power source
4. Try different USB port/cable
```

### 5.2 Common Devices
| Device | Issue | Solution |
|--------|-------|----------|
| Printer | Offline | Check network/power, restart print spooler |
| Monitor | No signal | Check cables, try different port |
| Keyboard/Mouse | Not working | Try different USB port, replace batteries |
| Webcam | Not detected | Check privacy settings, reinstall drivers |

## 6. Account Management

### 6.1 New Employee Setup
**Checklist**:
- [ ] Create AD account
- [ ] Assign email license
- [ ] Add to department groups
- [ ] Set up hardware (if applicable)
- [ ] Schedule orientation

### 6.2 Account Modifications
- Password resets: Self-service or manual reset
- Group membership changes: Submit ticket with manager approval
- Access requests: Department head approval required

## 7. Remote Support Tools

### 7.1 Quick Assist (Windows)
1. Open Start > Quick Assist
2. Select "Get assistance"
3. Share 6-digit code with user
4. User enters code at [aka.ms/quickassist](https://aka.ms/quickassist)

## 8. Knowledge Base

### 8.1 Top Solutions
1. [How to connect to VPN](https://kb.university.edu/1234)
2. [Setting up MFA](https://kb.university.edu/1235)
3. [Printing from personal devices](https://kb.university.edu/1236)
4. [Software download instructions](https://kb.university.edu/1237)

## 9. Escalation Guidelines

### 9.1 When to Escalate
- Issue requires admin rights
- Multiple users affected
- Potential security incident
- No resolution after standard troubleshooting

### 9.2 Escalation Information
Include in ticket:
- Steps already taken
- Error messages
- User impact
- Any workarounds attempted

## 10. Common Commands

### 10.1 Windows CMD
```batch
:: Network
ipconfig /all
ping google.com
nslookup university.edu

:: System
systeminfo
sfc /scannow
dism /online /cleanup-image /restorehealth

:: User Management
net user [username] /domain
whoami /groups
```

### 10.2 macOS Terminal
```bash
# Network
ifconfig
netstat -an | grep LISTEN
dig university.edu

# System
system_profiler SPHardwareDataType
diskutil list
df -h
```

## 11. Quick Reference Tables

### 11.1 Common Ports
| Service | Port | Protocol |
|---------|------|----------|
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| RDP | 3389 | TCP |
| SSH | 22 | TCP |
| SMTP | 587 | TCP |
| IMAP | 993 | TCP |

### 11.2 File Paths
| Purpose | Windows Path | macOS Path |
|---------|--------------|------------|
| Hosts file | C:\Windows\System32\drivers\etc\hosts | /etc/hosts |
| Temp files | %TEMP% | /tmp |
| Application logs | Event Viewer | Console.app |

## 12. Customer Service Tips

### 12.1 Communication Guidelines
- Use simple, non-technical language
- Confirm understanding
- Set clear expectations
- Follow up as promised

### 12.2 Difficult Situations
1. **Angry User**: Stay calm, empathize, focus on solution
2. **Unclear Issue**: Ask open-ended questions
3. **Repeated Caller**: Verify knowledge base articles shared

---
*Document Version: 1.0  
Last Updated: 2025-09-20*
