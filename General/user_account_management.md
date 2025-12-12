# 👥 User Account & Access Management Guide

## Table of Contents

### 1. [Account Lifecycle Management](#1-account-lifecycle-management)
   - [1.1 Account Creation Process](#11-account-creation-process)
   - [1.2 Account Modification](#12-account-modification)

### 2. [Access Control Framework](#2-access-control-framework)
   - [2.1 Role-Based Access Control (RBAC)](#21-role-based-access-control-rbac)
   - [2.2 Permission Groups](#22-permission-groups)

### 3. [Security Policies](#3-security-policies)
   - [3.1 Password Requirements](#31-password-requirements)
   - [3.2 Multi-Factor Authentication (MFA)](#32-multi-factor-authentication-mfa)

### 4. [Account Auditing](#4-account-auditing)
   - [4.1 Monitoring Commands](#41-monitoring-commands)
   - [4.2 Security Logs](#42-security-logs)

### 5. [Automation Scripts](#5-automation-scripts)
   - [5.1 New User Creation](#51-new-user-creation)
   - [5.2 Account Termination](#52-account-termination)

### 6. [Common Tasks](#6-common-tasks)
   - [6.1 Unlock Account](#61-unlock-account)
   - [6.2 Check Group Memberships](#62-check-group-memberships)

---


## 1. Account Lifecycle Management

### 1.1 Account Creation Process
**Prerequisites**:
- Completed access request form
- Manager approval
- HR onboarding confirmation

**Creation Steps**:
1. **Active Directory**
   ```powershell
   # Create AD User
   New-ADUser -Name "John Doe" \
              -GivenName "John" \
              -Surname "Doe" \
              -SamAccountName "jdoe" \
              -UserPrincipalName "jdoe@university.edu" \
              -Path "OU=Users,DC=university,DC=edu" \
              -AccountPassword (ConvertTo-SecureString "P@ssw0rd123" -AsPlainText -Force) \
              -Enabled $true
   ```

2. **Email Setup**
   ```powershell
   # Enable Exchange Mailbox
   Enable-Mailbox -Identity jdoe@university.edu
   ```

3. **Group Memberships**
   ```powershell
   # Add to Department Group
   Add-ADGroupMember -Identity "Faculty_Staff" -Members jdoe
   
   # Add to Role Groups
   Add-ADGroupMember -Identity "Staff_Access" -Members jdoe
   ```

### 1.2 Account Modification
**Common Operations**:
- Password resets
- Group membership changes
- Account enable/disable
- Profile updates

**Example**: Reset Password
```powershell
# Reset password and require change at next login
Set-ADAccountPassword -Identity jdoe -NewPassword (ConvertTo-SecureString "NewP@ss123" -AsPlainText -Force)
Set-ADUser -Identity jdoe -ChangePasswordAtLogon $true
```

## 2. Access Control Framework

### 2.1 Role-Based Access Control (RBAC)
**Standard Roles**:
| Role | Access Level | Example Groups |
|------|-------------|----------------|
| Faculty | Department resources | FAC_DeptName, FAC_Email |
| Staff | Office applications | STAFF_Dept, STAFF_Printers |
| Student | Academic resources | STU_Year, STU_Major |
| Contractor | Limited access | CONT_ProjectName |

### 2.2 Permission Groups
**Naming Convention**:
- `APP_ApplicationName_Role` (e.g., `APP_Finance_ReadOnly`)
- `DEPT_DepartmentName_Access` (e.g., `DEPT_HR_Full`)
- `LOC_Location_Resource` (e.g., `LOC_BuildingA_Printers`)

## 3. Security Policies

### 3.1 Password Requirements
- Minimum length: 12 characters
- Complexity: Upper, lower, number, special char
- History: 24 previous passwords remembered
- Maximum age: 90 days
- Account lockout: 5 attempts, 30-minute lockout

### 3.2 Multi-Factor Authentication (MFA)
**Implementation**:
1. Enable MFA in Azure AD
2. Configure conditional access policies
3. Enroll user devices

**Troubleshooting**:
```powershell
# Check MFA status
Get-MsolUser -UserPrincipalName jdoe@university.edu | Select-Object DisplayName,StrongAuthenticationMethods
```

## 4. Account Auditing

### 4.1 Monitoring Commands
```powershell
# Check last logon time
Get-ADUser jdoe -Properties LastLogonDate | Select-Object Name,LastLogonDate

# Find inactive accounts (90+ days)
Search-ADAccount -AccountInactive -TimeSpan 90.00:00:00 | 
    Where-Object {$_.Enabled -eq $true} |
    Select-Object Name, SamAccountName, LastLogonDate
```

### 4.2 Security Logs
**Key Events to Monitor**:
- 4624: Successful logon
- 4625: Failed logon
- 4720: User account created
- 4726: User account deleted
- 4738: User account changed

## 5. Automation Scripts

### 5.1 New User Creation
```powershell
# New-UserOnboarding.ps1
param(
    [Parameter(Mandatory=$true)]
    [string]$FirstName,
    [string]$LastName,
    [string]$Department,
    [string]$Title
)

# Generate username (first initial + lastname)
$Username = ($FirstName[0] + $LastName).ToLower()
$Email = "$Username@university.edu"
$OU = "OU=Users,OU=$Department,DC=university,DC=edu"
$TempPassword = [System.Web.Security.Membership]::GeneratePassword(12, 3)

# Create AD Account
try {
    New-ADUser -Name "$FirstName $LastName" \
               -GivenName $FirstName \
               -Surname $LastName \
               -SamAccountName $Username \
               -UserPrincipalName $Email \
               -Path $OU \
               -Title $Title \
               -Department $Department \
               -AccountPassword (ConvertTo-SecureString $TempPassword -AsPlainText -Force) \
               -Enabled $true \
               -ChangePasswordAtLogon $true
    
    # Add to department group
    Add-ADGroupMember -Identity "GRP_$Department" -Members $Username
    
    # Log creation
    Write-Host "User $Username created successfully with temporary password"
    return $TempPassword
} 
catch {
    Write-Error "Failed to create user: $_"
    exit 1
}
```

### 5.2 Account Termination
```powershell
# Disable-UserAccount.ps1
param(
    [Parameter(Mandatory=$true)]
    [string]$Username
)

try {
    # Disable account
    Disable-ADAccount -Identity $Username
    
    # Remove group memberships (except Domain Users)
    $Groups = Get-ADPrincipalGroupMembership $Username | Where-Object {$_.Name -ne "Domain Users"}
    Remove-ADPrincipalGroupMembership -Identity $Username -MemberOf $Groups -Confirm:$false
    
    # Move to Disabled Users OU
    Get-ADUser $Username | Move-ADObject -TargetPath "OU=Disabled,DC=university,DC=edu"
    
    # Set description with termination date
    $TermDate = Get-Date -Format "yyyy-MM-dd"
    Set-ADUser $Username -Description "Terminated $TermDate"
    
    Write-Host "Account $Username has been disabled and moved to Disabled OU."
}
catch {
    Write-Error "Error disabling account: $_"
}
```

## 6. Common Tasks

### 6.1 Unlock Account
```powershell
Unlock-ADAccount -Identity jdoe
```

### 6.2 Check Group Memberships
```powershell
Get-ADPrincipalGroupMembership jdoe | Select-Object Name
```

### 6.3 Find Users by Department
```powershell
Get-ADUser -Filter {Department -eq "Information Technology"} -Properties Department | 
    Select-Object Name, SamAccountName, Department
```

## 7. Best Practices

### 7.1 Account Security
- Implement least privilege access
- Regular access reviews (quarterly)
- Monitor privileged accounts
- Disable service accounts when not in use

### 7.2 Documentation
- Maintain change logs
- Document access approvals
- Keep org charts updated
- Record access requests

## 8. Troubleshooting

### 8.1 Common Issues
**Account Lockout**
```powershell
# Check lockout status
Get-ADUser jdoe -Properties LockedOut | Select-Object Name, LockedOut

# Unlock account
Unlock-ADAccount -Identity jdoe
```

**Permission Issues**
```powershell
# Check effective permissions
(Get-Acl "C:\Shared").Access | Format-Table IdentityReference,FileSystemRights,AccessControlType,IsInherited -AutoSize
```

## 9. Compliance & Reporting

### 9.1 Monthly Reports
- New user accounts
- Terminated accounts
- Password resets
- Failed login attempts

### 9.2 Access Review
```powershell
# Generate access review report
Get-ADUser -Filter * -Properties MemberOf | 
    Where-Object {$_.Enabled -eq $true} |
    Select-Object Name, SamAccountName, 
        @{Name='Groups';Expression={$_.MemberOf -join ';'}} |
    Export-CSV "AccessReview_$(Get-Date -Format 'yyyyMM').csv" -NoTypeInformation
```

## 10. Emergency Procedures

### 10.1 Security Incident Response
1. Disable compromised accounts
2. Reset passwords
3. Review logs for suspicious activity
4. Notify security team

### 10.2 Mass Account Operations
```powershell
# Disable all accounts in OU
Get-ADUser -Filter * -SearchBase "OU=Temp,DC=university,DC=edu" | 
    Disable-ADAccount

# Reset passwords for department
Get-ADUser -Filter {Department -eq "Finance"} | 
    Set-ADAccountPassword -NewPassword (ConvertTo-SecureString "NewP@ss123" -AsPlainText -Force) -Reset
```

---
*Document Version: 1.0  
Last Updated: 2025-09-20*
