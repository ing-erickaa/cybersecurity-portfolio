# TryHackMe SOC Level 1 - Windows Security Monitoring

## Overview

This module focused on Windows security monitoring, event log analysis, and the detection of suspicious activity on Windows endpoints.

The main objective was to understand how Windows records system and security events and how SOC analysts use those logs to investigate potential attacks.

The module covered Windows logging, initial access detection, post-compromise activity, and persistence mechanisms.

## Rooms Completed

- Windows Logging for SOC
- Windows Threat Detection 1
- Windows Threat Detection 2
- Windows Threat Detection 3

## Key Concepts Learned

### 1. Windows Logging for SOC

Windows generates event logs that provide information about authentication, process execution, system changes, and security-related activity.

These logs help SOC analysts investigate suspicious behavior and reconstruct incidents.

Important Windows log channels include:

- Security
- System
- Application
- Setup
- PowerShell Operational
- Sysmon Operational, when Sysmon is installed

Windows Event Viewer can be used to examine these records.

Common investigation activities include:

- Filtering events by Event ID
- Reviewing timestamps
- Identifying affected accounts
- Investigating authentication events
- Reviewing process execution
- Correlating activity across multiple logs

### 2. Important Windows Security Event IDs

Some useful Windows Security Event IDs include:

- 4624 - Successful logon
- 4625 - Failed logon
- 4634 - Account logoff
- 4648 - Logon attempted using explicit credentials
- 4672 - Special privileges assigned to a new logon
- 4688 - New process creation
- 4698 - Scheduled task created
- 4720 - User account created
- 4722 - User account enabled
- 4724 - Password reset attempted
- 4728 - Member added to a security-enabled global group
- 4732 - Member added to a security-enabled local group
- 4740 - User account locked out
- 1102 - Security audit log cleared

Some events require specific auditing settings to be enabled.

Event ID 4688, for example, requires process creation auditing. Command-line details require additional audit policy configuration.

### 3. Windows Threat Detection 1 - Initial Access

Initial access is the stage where an attacker attempts to enter a target environment.

Common initial access techniques include:

- Phishing
- Malicious attachments
- Stolen credentials
- Password attacks
- Exploitation of vulnerable services
- Abuse of remote access services
- Unauthorized authentication

Potential detection indicators include:

- Repeated failed logons
- Successful authentication after multiple failures
- Logons from unusual source addresses
- Unexpected remote sessions
- Suspicious process execution
- Unusual account activity

A SOC analyst must investigate the context before classifying an event as malicious.

### 4. Windows Threat Detection 2 - Post-Compromise Activity

After obtaining initial access, attackers may attempt to understand the compromised system and expand their access.

Common activities include:

- System discovery
- User enumeration
- Group enumeration
- Privilege discovery
- Process discovery
- Network configuration discovery
- Credential access attempts
- Privilege escalation
- Lateral movement

Examples of Windows commands that may be investigated include:

    whoami
    whoami /priv
    whoami /groups
    hostname
    ipconfig /all
    net user
    net localgroup administrators
    tasklist
    netstat -ano
    systeminfo

These commands have legitimate administrative uses and are not automatically malicious.

SOC analysts should correlate command execution with the user, process ancestry, timing, and surrounding activity.

### 5. Windows Threat Detection 3 - Persistence

Persistence refers to techniques that allow attackers to maintain access to a compromised environment.

Common persistence mechanisms include:

- Scheduled tasks
- Windows services
- Registry Run keys
- Startup folders
- Unauthorized user accounts
- Remote access configuration changes
- Malicious software configured to start automatically

Potential evidence includes:

- Unexpected scheduled tasks
- New or modified services
- Suspicious registry modifications
- Unusual startup applications
- New administrator accounts
- Processes launching from unexpected locations

Persistence detection requires understanding normal system configuration and identifying unauthorized changes.

### 6. Windows Event Viewer

Windows Event Viewer is a built-in utility for viewing and analyzing Windows event logs.

Useful features include:

- Custom Views
- Filter Current Log
- Find
- Event Properties
- Event Details
- XML View
- Event ID filtering

During an investigation, analysts should inspect:

- Event ID
- Timestamp
- Computer name
- Account name
- Logon ID
- Source IP address, when available
- Process name and path, when available
- Parent process information, when available
- Event details

### 7. Sysmon

Sysmon is a Microsoft Sysinternals tool that provides additional endpoint visibility.

Important Sysmon Event IDs include:

- 1 - Process creation
- 3 - Network connection
- 7 - Image loaded
- 8 - CreateRemoteThread
- 10 - Process access
- 11 - File creation
- 12 - Registry object created or deleted
- 13 - Registry value set
- 22 - DNS query

Sysmon events depend on the configuration and filtering rules deployed.

Sysmon can help investigators reconstruct process activity, identify suspicious network connections, and analyze possible persistence mechanisms.

## Useful Windows Commands

### Display the current user

    whoami

### Display user privileges

    whoami /priv

### List local user accounts

    net user

### List local administrators

    net localgroup administrators

### Display network connections

    netstat -ano

### List running processes

    tasklist

### Display system information

    systeminfo

### Display scheduled tasks

    schtasks /query /fo LIST /v

### Query recent Windows Security events using PowerShell

    Get-WinEvent -LogName Security -MaxEvents 10

### Search for failed logon events

    Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4625} -MaxEvents 20

### Search for successful logon events

    Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4624} -MaxEvents 20

### Search for process creation events

    Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4688} -MaxEvents 20

### List Windows services

    Get-Service

These commands are intended for authorized administration, troubleshooting, and defensive security investigations.

## Example Investigation - Suspicious Logon Activity

Scenario:

A Windows endpoint generates multiple failed logon events followed by a successful authentication.

Investigation process:

1. Review Event ID 4625.
2. Identify the affected account.
3. Check timestamps and source addresses.
4. Determine whether failures occurred repeatedly.
5. Review Event ID 4624 for related successful logons.
6. Examine the logon type and available authentication details.
7. Correlate with endpoint and network activity.
8. Determine whether the activity is expected.
9. Document the evidence.
10. Escalate if compromise is suspected.

Important:

Multiple failed logons do not automatically indicate an attack. Incorrect passwords, expired credentials, and misconfigured services may produce similar events.

## Example Investigation - Suspicious Process Execution

Scenario:

A Windows endpoint generates a process creation event involving an unexpected command.

Investigation process:

1. Identify the process name.
2. Review the executable path.
3. Identify the user account.
4. Examine the command line if available.
5. Review the parent process if available.
6. Compare the activity against expected behavior.
7. Search for related events.
8. Identify suspicious network connections.
9. Review persistence indicators.
10. Document findings and determine whether escalation is required.

The goal is to understand the context of process execution rather than assuming that a particular command is malicious.

## What I Learned

This module helped me understand how Windows logs provide evidence that SOC analysts can use to investigate security incidents.

I learned how authentication records, process activity, account changes, and system events can reveal suspicious behavior.

One important lesson was that individual events rarely tell the complete story.

For example, a failed logon may be harmless, but repeated failures followed by an unusual successful logon and suspicious process activity may require further investigation.

I also developed a better understanding of how attackers may attempt to establish persistence after compromising a Windows endpoint.

## Skills Practiced

- Windows Event Viewer navigation
- Event ID identification
- Windows Security log analysis
- Authentication event investigation
- Process execution analysis
- Windows account monitoring
- Initial access detection concepts
- Post-compromise activity analysis
- Persistence detection concepts
- Windows command-line investigation
- PowerShell event queries
- Understanding Sysmon telemetry
- Correlating multiple security events
- Documenting investigation findings

## Why This Matters for SOC Analysts

Windows endpoints are widely used in enterprise environments.

SOC analysts frequently investigate alerts involving:

- Suspicious logons
- Password attacks
- Unauthorized account creation
- Privilege changes
- Unexpected process execution
- Malware activity
- Persistence mechanisms
- Suspicious PowerShell execution
- Remote access
- Lateral movement

Understanding Windows event logs allows analysts to verify alerts, reconstruct timelines, identify affected assets, and support incident response.

These skills are particularly relevant to SOC Level 1 positions because Windows logs are often collected and analyzed through SIEM platforms such as Microsoft Sentinel, Splunk, and Elastic.

## Investigation Questions to Ask

During a Windows security investigation, a SOC analyst should ask:

- What event triggered the alert?
- Which Event ID was generated?
- When did the activity occur?
- Which host was affected?
- Which user account was involved?
- Was the account expected to perform this action?
- Was the logon successful or unsuccessful?
- What logon type was used?
- Was the source IP address expected?
- Was a new process created?
- What was the process command line?
- What process launched it?
- Were any new accounts created?
- Were administrator privileges assigned?
- Were scheduled tasks modified?
- Were registry persistence locations changed?
- Is there evidence of lateral movement?
- Are there additional related alerts?
- Should the incident be escalated?

## Reflection

This module helped me connect Windows administration concepts with real security monitoring and investigation workflows.

I learned that Windows logs can reveal the sequence of events surrounding a possible security incident.

The most valuable part was understanding how initial access, post-compromise activity, and persistence can leave different forms of evidence.

I also learned that effective detection depends on context, correlation, and investigation rather than relying on a single Event ID.

This knowledge is relevant to my goal of becoming a SOC Analyst because Windows security monitoring is a common responsibility in enterprise security operations.

## Next Steps

- Continue the TryHackMe SOC Level 1 learning path
- Practice Windows Event Viewer investigations
- Improve PowerShell skills
- Study Sysmon event analysis
- Build practical Windows security monitoring labs
- Learn SIEM queries and correlation
- Continue preparing for CompTIA Security+

## Disclaimer

This repository is for educational purposes only.

All exercises were completed in authorized training environments such as TryHackMe.

The commands and examples provided are intended for defensive security training and authorized system administration.

No flags, challenge answers, credentials, personal data, or sensitive information are included.
