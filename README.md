****Active Directory Security Audit & Risk Visibility Script**

**Author: Peter Joseph
Organization: Bindpoint Private Limited
Engine Version: 1.1****

**Overview**

This repository contains a read-only Active Directory security audit script that performs risk identification, vulnerability detection, and misconfiguration analysis across an Active Directory environment.

The script does not modify Active Directory, does not change system settings, and does not transmit data externally.
It is designed to provide clear visibility into security risks and generate actionable remediation guidance.

Key Design Principles

✅ Read-only execution
✅ No changes to AD objects, permissions, or configurations
✅ No passwords, secrets, or credentials collected
✅ No outbound network connections
✅ Safe for production use
✅ Human-approved remediation only

What the Script Does
The script performs the following high-level actions:

Executes multiple predefined AD security risk checks
Collects results in structured PowerShell objects
Exports results to CSV files (per risk)

**Generates:**

A central HTML Summary Report
Individual HTML detail reports per risk
Logs execution activity and errors to a local execution log
All output is written locally to a configurable folder.

**Risk Coverage**

The script evaluates Active Directory for real-world attack techniques and misconfigurations, including (but not limited to):

******🔐 Kerberos & Authentication Risks**
Kerberoastable accounts (SPNs)
Administrative SPNs (high-risk)
Unconstrained Kerberos delegation
TGT delegation risks (manual validation flagged)

**🛡️ Known Microsoft Vulnerabilities**
MS14-068 (Kerberos privilege escalation)
MS17-010 (EternalBlue / SMBv1)

**👤 Identity & Privilege Abuse**
Dangerous SIDHistory attributes
Guest account enabled
Privileges granted to Everyone
Indirect control paths to sensitive objects (manual analysis flagged)

**🌐 Legacy & Misconfiguration Risks**
Null session access
Legacy delegation and permission exposure****

Some advanced attack paths cannot be reliably detected using PowerShell alone.
These are clearly marked as “Manual check required” with references to specialized tools.

**Output Structure**

By default, results are written to:
C:\Temp\AD Security Remediation

**Generated Files**
ExecutionLog.txt — execution status, timing, errors
AD Summary Report.html — consolidated risk overview
<RiskID>.csv — raw results per risk
<RiskID>_Details.html — detailed per-risk report
HTML Summary Report

**The summary report includes:**
Domain name
Hostname & IP address
Logged-in user
Execution date & engine version
Risk ID
Affected object count (clickable)
Risk description
Technical explanation
Recommended remediation
Microsoft documentation references
Each affected object count links to a dedicated detail report.

**Requirements**

Windows Server or domain-joined workstation
PowerShell 5.1 or later
Active Directory PowerShell module
Network connectivity to a Domain Controller
Permissions Required
Standard domain user permissions are sufficient for most checks
A read-only service account is recommended for repeat execution
❗ No Domain Admin or elevated privileges are required.

**Usage**

Copy the script to a domain-joined system
Open PowerShell
Execute:.\AD-Security-Audit.ps1

**Review**:
HTML Summary Report
Individual CSV and detail HTML files
Execution log
Safety & Transparency
No write operations (Set-*, Remove-*, New-*) are executed
No registry modifications are made
No data leaves the local system
Script logic is fully visible and auditable
Admins are encouraged to review the script before execution.
Intended Audience
Active Directory Administrators
IT Managers
Security Engineers
Incident Response Teams
Managed Service Providers (MSPs)

**Licensing Status**
⚠️ Licensing Notice

No open-source license is granted at this time.
This repository is provided for evaluation and reference purposes only.
Reuse, redistribution, or commercial use is not permitted without explicit written permission from the author.

A licensed version may be introduced in future releases.

**Disclaimer**

This script is provided as-is, without warranty of any kind.
It is intended to assist with security visibility and remediation planning and does not replace:

Penetration testing
Red team assessments
Formal security audits
All remediation actions should be reviewed and approved by qualified administrators.
Future Roadmap (Indicative)
Expanded rule coverage (70+ checks)
Licensed / Pro edition
Optional remediation workflows
Entra ID / hybrid identity support
MSP-friendly packaging
Design Philosophy
Visibility before remediation.
Deterministic logic before automation.
Security without disruption.
