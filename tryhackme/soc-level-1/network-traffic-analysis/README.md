# TryHackMe SOC Level 1 - Network Traffic Analysis

## Overview

This section focused on the basics of network traffic analysis and how SOC analysts can use tools such as Wireshark and NetworkMiner to inspect network activity, analyze packets, review protocols, and identify suspicious behavior.

The main goal was to understand how network traffic is collected, how packets are structured, and how packet captures can help investigate security incidents.

## Rooms Completed

- Network Traffic Basics
- Wireshark: The Basics
- Wireshark: Packet Operations
- Wireshark: Traffic Analysis
- NetworkMiner

## Key Concepts Learned

### Network Traffic Basics

Network traffic analysis is the process of inspecting communication between devices on a network.

This can help analysts understand normal behavior, detect suspicious activity, and investigate possible attacks.

Important concepts include:

- Packets
- Protocols
- Source IP address
- Destination IP address
- Source port
- Destination port
- TCP and UDP traffic
- DNS queries
- HTTP traffic
- Network conversations
- Packet captures

### Packet Captures

A packet capture, also known as a PCAP, records network traffic for later analysis.

PCAP files are useful because they allow analysts to review what happened on the network during a specific period of time.

SOC analysts may use packet captures to investigate:

- Suspicious connections
- Malware communication
- Data transfer
- DNS activity
- HTTP requests
- Login attempts
- Command and control traffic
- Unusual network behavior

### Wireshark Basics

Wireshark is a packet analysis tool used to inspect network traffic.

It allows analysts to review individual packets, follow network conversations, filter traffic, and understand how systems communicate.

Useful Wireshark features include:

- Packet list
- Packet details
- Packet bytes
- Display filters
- Protocol analysis
- Follow TCP stream
- Export objects
- Conversations
- Statistics

### Wireshark Packet Operations

Packet operations help analysts search, filter, and isolate specific traffic inside a packet capture.

Important operations include:

- Filtering by IP address
- Filtering by protocol
- Filtering by port
- Searching packet contents
- Following TCP streams
- Reviewing conversations
- Exporting transferred files
- Identifying suspicious domains or URLs

Example filter concepts:

    ip.addr == <IP_ADDRESS>
    tcp.port == <PORT>
    http
    dns

### Wireshark Traffic Analysis

Traffic analysis helps identify patterns, anomalies, and possible malicious behavior.

Examples of suspicious traffic include:

- Unknown external connections
- Unusual DNS queries
- Repeated failed connections
- Suspicious HTTP requests
- Large or unexpected file transfers
- Connections to known malicious domains
- Unusual ports
- Command and control patterns

The goal is not only to look at packets, but to understand the story behind the traffic.

### NetworkMiner

NetworkMiner is a network forensic analysis tool that helps extract useful information from packet captures.

It can help identify:

- Hosts
- IP addresses
- Hostnames
- Operating systems
- Sessions
- Files
- Images
- Credentials in insecure traffic
- DNS queries
- HTTP activity

NetworkMiner is useful because it gives analysts a different view of the same PCAP file and can make it easier to identify artifacts during an investigation.

## What I Learned

This section helped me understand how network traffic analysis supports SOC investigations.

I learned that packets can provide important evidence about what happened on a network. By reviewing protocols, IP addresses, ports, DNS queries, HTTP requests, and conversations, analysts can identify suspicious behavior and investigate possible threats.

I also learned that Wireshark is very powerful, but it requires a structured approach. Instead of randomly clicking packets, a SOC analyst should ask clear investigation questions and use filters to focus on relevant traffic.

Another important lesson was that network traffic can reveal activity that may not be obvious from a single alert. By analyzing multiple packets together, an analyst can understand communication patterns and possible attacker behavior.

## Skills Practiced

- Understanding packet captures
- Reviewing network protocols
- Using Wireshark display filters
- Following TCP streams
- Identifying network conversations
- Reviewing DNS and HTTP traffic
- Looking for suspicious network activity
- Understanding basic network forensics
- Using NetworkMiner for PCAP analysis
- Thinking like a SOC analyst during traffic investigations

## Why This Matters for SOC Analysts

Network traffic analysis is important because many attacks leave evidence on the network.

SOC analysts may use packet analysis to investigate:

- Phishing links
- Malware downloads
- Command and control communication
- Suspicious DNS activity
- Unauthorized file transfers
- Scanning activity
- Lateral movement
- Data exfiltration

Understanding network traffic helps analysts move beyond alerts and verify what actually happened.

This skill is useful for SOC Level 1 roles because analysts often need to review logs, alerts, IP addresses, domains, protocols, and packet captures to determine whether activity is normal, suspicious, or malicious.

## Investigation Questions to Ask

During network traffic analysis, a SOC analyst should ask:

- What systems are communicating?
- What protocols are being used?
- Are the source and destination IP addresses expected?
- What ports are involved?
- Is there DNS activity?
- Are there suspicious domains?
- Is there HTTP traffic?
- Was a file transferred?
- Is the traffic normal for this environment?
- Is there evidence of malware communication?
- Is there evidence of command and control activity?
- Should this activity be escalated?

## Useful Wireshark Filter Examples

Basic filters:

    ip.addr == <IP_ADDRESS>
    ip.src == <SOURCE_IP>
    ip.dst == <DESTINATION_IP>
    tcp.port == <PORT>
    udp.port == <PORT>
    dns
    http
    tcp
    udp

Additional filter examples:

    http.request
    http.response
    dns.qry.name
    tcp.flags.syn == 1
    tcp.flags.reset == 1

These filters can help narrow down traffic and focus on specific protocols, IP addresses, ports, or packet behaviors.

## Reflection

This section was very useful because it connected networking fundamentals with real security investigations.

I learned that network traffic analysis requires patience and attention to detail. A single packet may not explain everything, but multiple packets together can reveal user activity, system communication, suspicious connections, and possible attacks.

This section also helped me understand why networking is one of the most important foundations in cybersecurity. To investigate threats, a SOC analyst must understand how normal traffic works so they can recognize abnormal behavior.

Wireshark and NetworkMiner gave me hands-on practice with packet captures and helped me understand how network evidence can support an investigation.

## Disclaimer

This repository is for educational purposes only. All labs and exercises were completed in authorized training environments such as TryHackMe.

No flags, answers, credentials, private data, or sensitive information are included.
