# Windows Server Security GPO Automation Suite

![PowerShell](https://img.shields.io/badge/PowerShell-5.1+-blue.svg)
![Windows Server](https://img.shields.io/badge/Windows%20Server-2016%2B-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

A comprehensive collection of PowerShell scripts and documentation for implementing enterprise-grade security Group Policy Objects (GPOs) on Windows Server environments.

## 🚀 Features

- **Interactive Scripts**: User-friendly PowerShell scripts with menu-driven interfaces
- **Comprehensive Coverage**: All critical security GPO settings
- **Enterprise Ready**: Based on industry best practices (CIS, NIST, Microsoft)
- **Automated Deployment**: Bulk configuration with safety checks
- **Rollback Capability**: Easy restoration of previous configurations
- **Audit & Compliance**: Built-in security auditing and reporting

## 📋 Table of Contents

- [Quick Start](#-quick-start)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Usage](#-usage)
- [Scripts Overview](#-scripts-overview)
- [Security Policies](#-security-policies)
- [Configuration Examples](#-configuration-examples)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

## 🚦 Quick Start

1. **Clone the repository**:
   ```powershell
   git clone https://github.com/yourusername/windows-server-security-gpo.git
   cd windows-server-security-gpo
   ```

2. **Run the main configuration script**:
   ```powershell
   .\Deploy-SecurityGPO.ps1
   ```

3. **Follow the interactive prompts** to configure your security policies.

## 📋 Prerequisites

### System Requirements
- Windows Server 2016 or later
- PowerShell 5.1 or later
- Active Directory Domain Services
- Group Policy Management Console (GPMC)

### Required Permissions
- Domain Administrator privileges
- Group Policy Creator Owners membership
- Local Administrator on target servers

### PowerShell Modules
```powershell
# Install required modules
Install-Module -Name GroupPolicy -Force
Install-Module -Name ActiveDirectory -Force
```

## 🔧 Installation

### Method 1: Direct Download
```powershell
# Download and extract
Invoke-WebRequest -Uri "https://github.com/yourusername/windows-server-security-gpo/archive/main.zip" -OutFile "security-gpo.zip"
Expand-Archive -Path "security-gpo.zip" -DestinationPath "C:\SecurityGPO"
```

### Method 2: Git Clone
```powershell
git clone https://github.com/yourusername/windows-server-security-gpo.git C:\SecurityGPO
```

### Method 3: PowerShell Gallery (Coming Soon)
```powershell
Install-Module -Name WindowsServerSecurityGPO
```

## 🎯 Usage

### Interactive Mode
```powershell
# Run the main deployment script
.\Deploy-SecurityGPO.ps1

# Or run specific configuration modules
.\Scripts\Configure-PasswordPolicy.ps1
.\Scripts\Configure-AuditPolicy.ps1
.\Scripts\Configure-UserRights.ps1
```

### Automated Mode
```powershell
# Deploy with predefined configuration
.\Deploy-SecurityGPO.ps1 -ConfigFile ".\Configs\EnterpriseConfig.json" -Automated
```

### Audit Mode
```powershell
# Generate security compliance report
.\Scripts\Audit-SecurityCompliance.ps1 -OutputPath "C:\Reports"
```

## 📜 Scripts Overview

### Core Deployment Scripts

| Script | Description | Parameters |
|--------|-------------|------------|
| `Deploy-SecurityGPO.ps1` | Main deployment script with interactive menu | `-ConfigFile`, `-Automated`, `-TestMode` |
| `Backup-ExistingGPOs.ps1` | Creates backup of current GPO settings | `-BackupPath`, `-GPOName` |
| `Restore-GPOBackup.ps1` | Restores GPO from backup | `-BackupPath`, `-RestoreDate` |

### Configuration Scripts

| Script | Description | Security Focus |
|--------|-------------|----------------|
| `Configure-PasswordPolicy.ps1` | Password and account lockout policies | Authentication Security |
| `Configure-AuditPolicy.ps1` | Advanced audit policy configuration | Monitoring & Compliance |
| `Configure-UserRights.ps1` | User rights and privileges assignment | Access Control |
| `Configure-SecurityOptions.ps1` | Local security policy options | System Hardening |
| `Configure-FirewallRules.ps1` | Windows Firewall advanced settings | Network Security |
| `Configure-AppLocker.ps1` | Application control policies | Malware Prevention |
| `Configure-Services.ps1` | System services security configuration | Attack Surface Reduction |

### Utility Scripts

| Script | Description | Use Case |
|--------|-------------|----------|
| `Test-SecurityCompliance.ps1` | Validates current security configuration | Pre/Post deployment testing |
| `Generate-SecurityReport.ps1` | Creates comprehensive security reports | Documentation & Audit |
| `Export-GPOSettings.ps1` | Exports GPO configurations to XML/JSON | Backup & Documentation |
| `Import-GPOSettings.ps1` | Imports GPO configurations from file | Migration & Standardization |

## 🔒 Security Policies

### 1. Password Policy Configuration

**Default Settings Applied:**
```json
{
  "PasswordPolicy": {
    "MinimumPasswordLength": 14,
    "PasswordComplexity": true,
    "MaximumPasswordAge": 90,
    "MinimumPasswordAge": 1,
    "PasswordHistorySize": 24,
    "ReversibleEncryption": false
  },
  "AccountLockout": {
    "LockoutThreshold": 5,
    "LockoutDuration": 30,
    "ResetLockoutCounter": 30
  }
}
```

### 2. User Rights Assignment

**Critical Rights Restrictions:**
- `SeServiceLogonRight`: Service accounts only
- `SeNetworkLogonRight`: Authenticated users, exclude guests
- `SeDenyNetworkLogonRight`: Anonymous logon, guests
- `SeRemoteInteractiveLogonRight`: Remote Desktop Users only
- `SeTcbPrivilege`: No assignment (highly privileged)

### 3. Audit Policy Configuration

**Events Monitored:**
- Account logon events (Success/Failure)
- Account management (Success/Failure)
- Logon events (Success/Failure)
- Object access (Failure)
- Policy change (Success/Failure)
- Privilege use (Failure)
- System events (Success/Failure)

### 4. Security Options

**Key Settings:**
- Rename administrator/guest accounts
- Disable LAN Manager hash storage
- Require NTLMv2 authentication
- Enable message for interactive logon
- Restrict anonymous access

## 📝 Configuration Examples

### Example 1: Basic Enterprise Security
```powershell
# Deploy standard enterprise security configuration
.\Deploy-SecurityGPO.ps1 -Profile "Enterprise" -OUPath "OU=Servers,DC=contoso,DC=com"
```

### Example 2: High Security Environment
```powershell
# Deploy high security configuration with additional restrictions
.\Deploy-SecurityGPO.ps1 -Profile "HighSecurity" -EnableAdvancedAudit -RestrictPowerShell
```

### Example 3: Custom Configuration
```powershell
# Use custom configuration file
.\Deploy-SecurityGPO.ps1 -ConfigFile ".\Configs\CustomSecurity.json" -TestMode
```

### Example 4: Audit Existing Environment
```powershell
# Generate compliance report
.\Scripts\Test-SecurityCompliance.ps1 -OutputFormat "HTML" -EmailReport -Recipients "admin@contoso.com"
```

## 🎛️ Interactive Menu System

The main script provides an intuitive menu system:

```
========================================
Windows Server Security GPO Deployment
========================================

1. Deploy Password Policy
2. Configure Account Lockout
3. Set User Rights Assignment
4. Configure Audit Policy
5. Apply Security Options
6. Configure Windows Firewall
7. Setup Application Control
8. Manage System Services
9. Generate Security Report
10. Backup Current Settings
11. Restore from Backup
0. Exit

Select an option (0-11):
```

## 🔍 Advanced Features

### Configuration Profiles

**Available Profiles:**
- `Basic`: Fundamental security settings
- `Enterprise`: Standard enterprise security
- `HighSecurity`: Maximum security restrictions
- `Compliance`: Regulatory compliance focus
- `Custom`: User-defined configuration

### Automated Testing

```powershell
# Run comprehensive security tests
.\Scripts\Test-SecurityCompliance.ps1 -Detailed

# Test specific policy areas
.\Scripts\Test-SecurityCompliance.ps1 -TestCategory "PasswordPolicy,AuditPolicy"
```

### Reporting Capabilities

```powershell
# Generate detailed HTML report
.\Scripts\Generate-SecurityReport.ps1 -Format "HTML" -IncludeRecommendations

# Export to multiple formats
.\Scripts\Generate-SecurityReport.ps1 -Format "PDF,Excel,JSON" -OutputPath "C:\Reports"
```

## 🛠️ Troubleshooting

### Common Issues

**Issue**: Script execution policy prevents running scripts
```powershell
# Solution: Set execution policy (run as administrator)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
```

**Issue**: Insufficient permissions error
```powershell
# Solution: Verify domain admin rights
whoami /groups | findstr "Domain Admins"
```

**Issue**: GPO not applying to target computers
```powershell
# Solution: Force group policy update
gpupdate /force /target:computer
```

### Debugging Mode

Enable detailed logging for troubleshooting:
```powershell
.\Deploy-SecurityGPO.ps1 -Verbose -Debug -LogPath "C:\Logs\GPODeployment.log"
```

### Log Locations

- **Deployment Logs**: `C:\Windows\Logs\SecurityGPO\`
- **Audit Logs**: `C:\Windows\System32\winevt\Logs\Security.evtx`
- **GPO Logs**: `C:\Windows\debug\usermode\gpsvc.log`

## 📊 Monitoring & Maintenance

### Scheduled Tasks

Create automated monitoring:
```powershell
# Create daily security check task
.\Scripts\Create-MonitoringTask.ps1 -Frequency "Daily" -Time "02:00"
```

### Key Performance Indicators

Monitor these metrics:
- Failed logon attempts per hour
- Policy change frequency
- Service account usage
- Privileged access events

### Regular Maintenance Tasks

- **Weekly**: Review security event logs
- **Monthly**: Update password policies
- **Quarterly**: Audit user rights assignments
- **Annually**: Complete security policy review

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

### Development Setup

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

### Code Standards

- Follow PowerShell best practices
- Include help documentation for functions
- Add parameter validation
- Include error handling
- Write Pester tests for new scripts

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Useful Links

- [Microsoft Group Policy Documentation](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/group-policy/)
- [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks/)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [PowerShell Gallery](https://www.powershellgallery.com/)

## 🏆 Acknowledgments

- Microsoft Security Compliance Toolkit
- PowerShell Community
- CIS Security Benchmarks
- NIST Cybersecurity Framework

---

**⚠️ Important Security Notice**: Always test these configurations in a non-production environment first. Review and customize settings based on your organization's specific security requirements and compliance needs.

**🔄 Version**: 1.0.0 | **📅 Last Updated**: May 2025
