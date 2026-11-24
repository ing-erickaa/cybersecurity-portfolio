# TryHackMe SOC Level 1 - Linux Security Monitoring

## Overview

This module focused on Linux security monitoring, log analysis, and threat detection using native Linux tools and audit records.

The main objective was to understand how Linux records system activity and how SOC analysts can use this information to investigate suspicious behavior, reconstruct attack timelines, and identify possible security incidents.

The module covered Linux logging, initial access detection, post-compromise activity, and later stages of attacks against Linux systems.

## Rooms Completed

- Linux Logging for SOC
- Linux Threat Detection 1
- Linux Threat Detection 2
- Linux Threat Detection 3

## Key Concepts Learned

### 1. Linux Logging for SOC

Linux systems generate different types of logs that help security analysts understand system activity.

Important log sources include:

- Authentication logs
- System logs
- SSH logs
- Package manager logs
- Bash history
- Systemd journal
- Auditd logs
- Application logs

Common log locations include:

    /var/log/auth.log
    /var/log/syslog
    /var/log/audit/audit.log
    /var/log/dpkg.log
    /var/log/apt/history.log
    /var/log/journal/
    /home/<USER>/.bash_history
    /root/.bash_history

Log availability depends on the Linux distribution and its logging configuration.

### 2. Authentication and SSH Monitoring

Authentication logs help analysts investigate successful and failed login attempts.

Common suspicious activities include:

- Repeated failed SSH logins
- Logins from unexpected source IP addresses
- Successful logins after multiple failures
- Unauthorized privilege escalation
- Unexpected sudo usage
- New user accounts
- Changes to authentication settings

Useful commands:

    sudo grep "Failed password" /var/log/auth.log
    sudo grep "Accepted password" /var/log/auth.log
    sudo journalctl -u ssh
    last
    lastlog
    who
    w

These commands help identify authentication activity and user sessions.

### 3. Linux Package Manager Logs

Package manager logs provide information about software installations, upgrades, and removals.

This information can help analysts identify unexpected software changes.

For Debian and Ubuntu systems:

    cat /var/log/dpkg.log

    cat /var/log/apt/history.log

    grep "install" /var/log/dpkg.log

Package logs can help answer questions such as:

- What software was installed?
- Which package version was installed?
- When did the installation occur?
- Were unexpected tools installed?

Package installations should be investigated in context because software changes may be legitimate administrative activity.

### 4. Bash History Analysis

Bash history stores commands from interactive shell sessions when history recording is enabled.

Useful commands:

    history

    cat ~/.bash_history

    sudo cat /root/.bash_history

    sudo find /home /root -name ".bash_history" -type f

    sudo grep -nH "sudo" /home/*/.bash_history

Important limitations:

- Bash history is not a complete audit trail.
- Commands may not be saved until a session ends.
- Users may disable or modify history recording.
- Noninteractive commands may not appear.
- History files can be deleted or modified.

For security investigations, Bash history should be correlated with more reliable telemetry, including auditd and system logs.

### 5. Linux Threat Detection 1 - Initial Access

Initial access refers to techniques attackers use to gain access to a Linux system.

Possible attack methods include:

- SSH credential attacks
- Stolen credentials
- Exploitation of vulnerable services
- Misconfigured authentication
- Unauthorized remote access
- Abuse of exposed applications

Possible detection indicators include:

- High numbers of failed logins
- Unusual authentication patterns
- Unexpected remote sessions
- Logins from unfamiliar source addresses
- Unauthorized account activity

SOC analysts should review authentication logs and correlate suspicious events with other evidence.

### 6. Linux Threat Detection 2 - Post-Compromise Activity

After compromising a Linux system, an attacker may attempt to gather information about the environment.

Common discovery commands include:

    whoami
    id
    hostname
    uname -a
    lscpu
    ip addr
    ip route
    ps aux
    netstat -tulnp
    ss -tulnp
    cat /etc/passwd

These commands may reveal:

- Current user identity
- User privileges
- System information
- Operating system details
- Network configuration
- Running processes
- Listening services
- Local user accounts

These commands also have legitimate administrative uses.

Their presence alone does not prove malicious activity.

### 7. Linux Threat Detection 3 - Later Attack Stages

Later stages of an intrusion may include:

- Privilege escalation
- Persistence
- Credential access
- Lateral movement
- Command and control
- Data collection
- Data exfiltration
- Impact

Potential persistence mechanisms include:

- Cron jobs
- Systemd services
- Startup scripts
- Modified shell profiles
- Unauthorized SSH keys
- Unexpected user accounts

Useful inspection commands:

    crontab -l

    sudo systemctl list-unit-files

    sudo systemctl list-timers --all

    ls -la ~/.ssh/

    cat /etc/passwd

    ps aux

Changes to these components may require further investigation.

### 8. Auditd - Linux Audit Framework

Auditd is the userspace component of the Linux Audit system.

It records events according to configured auditing rules.

Audit records can provide information about:

- Process execution
- File access
- User activity
- System calls
- Permission changes
- Authentication activity
- Security-relevant system events

Important audit record types include:

- SYSCALL
- EXECVE
- PROCTITLE
- CWD
- PATH
- USER_AUTH
- USER_LOGIN

Different record types can describe different aspects of the same audited event.

### 9. Useful Auditd Commands

Search audit records:

    sudo ausearch -i

Search for process execution events:

    sudo ausearch -m EXECVE -i

Search for a specific executable:

    sudo ausearch -i -x hostname

Search by process ID:

    sudo ausearch -i --pid 3771

Search by audit key:

    sudo ausearch -k <AUDIT_KEY> -i

Generate a summary of executable activity:

    sudo aureport -x --summary

Generate an authentication report:

    sudo aureport -au

Generate a login report:

    sudo aureport -l

The availability of results depends on the auditing configuration and retained logs.

### 10. Understanding Parent and Child Processes

Processes in Linux have identifiers that help analysts reconstruct execution activity.

Important fields include:

- PID: Process ID
- PPID: Parent Process ID
- UID: User ID
- AUID: Audit User ID
- COMM: Command name
- EXE: Executable path
- CWD: Current working directory
- PROCTITLE: Process command-line information

A parent process may launch multiple child processes.

Example process tree:

    bash (PID 3771)
    |
    +-- hostname (PID 3772)
    |
    +-- uname -a (PID 3773)
    |
    +-- lscpu (PID 3774)

In this example, the three commands share the same parent process.

This relationship can help analysts identify scripts responsible for multiple commands.

Important:

The values shown above are educational examples based on process relationships investigated during the training.

Process IDs are temporary identifiers and may be reused by the operating system.

### 11. Understanding fork() and execve()

Linux process execution commonly involves two important operations.

fork():

Creates a child process based on an existing process.

execve():

Replaces the currently executing program with another program.

For example, a Bash script may create child processes to execute system discovery commands.

Auditd EXECVE records can help analysts identify executed programs and their arguments.

### 12. Process Investigation

Useful commands:

    ps -ef

    ps aux

    pstree -p

    ps -o pid,ppid,user,args -p <PID>

    sudo ausearch -i --pid <PID>

During an investigation, analysts can examine:

- Process ancestry
- Executable paths
- Command-line arguments
- User context
- Execution timestamps
- Related child processes
- Network connections
- File access activity

Process ancestry provides important context when investigating suspicious commands.

## Example Investigation - Suspicious SSH Activity

Scenario:

A Linux server generates multiple failed SSH authentication events followed by a successful login.

Investigation workflow:

1. Identify the source IP address.
2. Review failed authentication events.
3. Determine which accounts were targeted.
4. Identify successful login events.
5. Check the login timestamp.
6. Identify the user account involved.
7. Review related process activity.
8. Examine available audit records.
9. Investigate unexpected commands or file changes.
10. Document findings and determine whether escalation is necessary.

Repeated authentication failures are not automatically malicious.

The analyst should consider user behavior, system configuration, and additional evidence.

## Example Investigation - Suspicious Discovery Activity

Scenario:

A SOC alert reports several Linux system discovery commands executed within a short period.

Observed commands:

    hostname
    uname -a
    lscpu

Investigation workflow:

1. Locate the hostname execution event in auditd.
2. Identify the process PID.
3. Identify the parent process PPID.
4. Search audit records for the parent process.
5. Examine the parent's command line.
6. Identify the script or program responsible.
7. Search for related child processes.
8. Reconstruct the command execution timeline.
9. Determine whether the activity was authorized.
10. Document evidence and conclusions.

This investigation demonstrates how process ancestry helps connect multiple events to a single originating process.

## Example Investigation - File Access

Scenario:

A sensitive file was accessed, and auditd recorded the event under a configured audit key.

Investigation command:

    sudo ausearch -k file_thmsecret -i

Potential evidence includes:

- Timestamp
- User identity
- Process information
- File path
- System call
- Event result

This type of investigation can help answer:

- When was the file accessed?
- Which user accessed it?
- What process performed the operation?
- Was the operation successful?
- Was the access expected?

## What I Learned

This module helped me understand how Linux logging and audit records can support security investigations.

I learned that Linux provides multiple sources of evidence, including authentication logs, package manager logs, Bash history, and auditd records.

One of the most important lessons was understanding the relationship between parent and child processes.

By analyzing PID and PPID values, I learned how to reconstruct a sequence of executed commands and trace activity back to the process that initiated it.

I also learned that individual commands are not enough to determine whether an incident is malicious.

A SOC analyst must examine context, timestamps, user identity, process ancestry, and related system activity.

Another important lesson was understanding the limitations of Bash history and why centralized logging and audit records are important for investigations.

## Skills Practiced

- Linux log analysis
- Authentication log investigation
- SSH monitoring
- Package manager log analysis
- Bash history inspection
- Linux user enumeration
- Process investigation
- PID and PPID analysis
- Parent-child process correlation
- Auditd event analysis
- EXECVE record interpretation
- PROCTITLE inspection
- File access investigation
- System discovery detection
- Suspicious command analysis
- Incident timeline reconstruction
- Defensive investigation methodology

## Why This Matters for SOC Analysts

Linux servers are widely used in enterprise infrastructure, cloud environments, and production systems.

SOC analysts frequently investigate alerts involving:

- Suspicious SSH logins
- Unauthorized user accounts
- Privilege escalation
- Unexpected command execution
- System discovery
- Suspicious scripts
- Unauthorized file access
- Persistence mechanisms
- Malware execution
- Data exfiltration

Understanding Linux telemetry helps analysts verify alerts, reconstruct system activity, identify suspicious behavior, and support incident response.

These skills are especially important in environments using SIEM platforms that collect Linux logs and audit events.

## Investigation Questions to Ask

During a Linux security investigation, a SOC analyst should ask:

- What event triggered the alert?
- Which user was involved?
- When did the activity occur?
- What source IP initiated the connection?
- Was authentication successful?
- Were there failed authentication attempts?
- Was sudo used?
- What command was executed?
- What was the executable path?
- What was the process PID?
- What was the parent process PPID?
- What process launched the suspicious command?
- Was a script involved?
- Were additional child processes created?
- Was sensitive information accessed?
- Were new accounts created?
- Were software packages installed?
- Were persistence mechanisms modified?
- Was there unusual network activity?
- Does the activity match expected administration?
- Should the incident be escalated?

## Useful Linux Investigation Commands

Display current user:

    whoami

Display user identity and groups:

    id

List local accounts:

    cat /etc/passwd

List accounts using Bash:

    grep '/bin/bash$' /etc/passwd

Display home directories:

    ls -la /home

Search for Bash history files:

    sudo find /home /root -type f -name ".bash_history"

View recent authentication logs:

    sudo tail -n 50 /var/log/auth.log

Review SSH service logs:

    sudo journalctl -u ssh

Search audit events by executable:

    sudo ausearch -i -x hostname

Search audit events by PID:

    sudo ausearch -i --pid <PID>

Inspect process relationships:

    ps -ef

Display the process tree:

    pstree -p

Search for package installation activity:

    grep "install" /var/log/dpkg.log

## Reflection

This module was especially useful because it connected Linux command-line knowledge with real security investigations.

Before this module, I understood how to execute Linux commands and inspect system information.

After completing the labs, I developed a better understanding of how analysts use logs to reconstruct activity and identify suspicious behavior.

The auditd exercises were particularly valuable because they demonstrated how process IDs, parent process IDs, executable paths, and command-line arguments can reveal relationships between different events.

I also learned why security investigations require a structured approach.

Instead of assuming that a command is malicious, analysts must investigate who executed it, how it was launched, what happened afterward, and whether the activity was authorized.

This knowledge supports my goal of developing practical SOC Analyst skills.

## Next Steps

- Continue the TryHackMe SOC Level 1 learning path
- Practice Linux log analysis
- Improve Bash scripting skills
- Explore auditd rules and event correlation
- Build a Linux security monitoring lab
- Practice detecting suspicious SSH activity
- Learn SIEM queries for Linux event investigation
- Continue preparing for CompTIA Security+

## Disclaimer

This repository is for educational purposes only.

All exercises were completed in authorized training environments such as TryHackMe.

The commands and examples are intended for defensive security education and authorized system administration.

No challenge flags, direct answers, credentials, personal information, or sensitive data are included.
