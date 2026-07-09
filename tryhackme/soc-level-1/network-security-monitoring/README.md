# TryHackMe SOC Level 1 - Network Security Monitoring

## Overview

This section focused on the fundamentals of network security monitoring and how SOC analysts identify suspicious activity by examining network traffic, logs, alerts, and security events.

The main goal was to understand how organizations monitor their network perimeter and detect activity related to network discovery, data exfiltration, Man-in-the-Middle attacks, and other network-based threats.

This section also introduced Intrusion Detection Systems and provided hands-on experience with Snort.

## Rooms Completed

- Network Security Essentials
- Network Discovery Detection
- Data Exfiltration Detection
- Man-in-the-Middle Detection
- IDS Fundamentals
- Snort

## Key Concepts Learned

### Network Security Essentials

Network security monitoring is the continuous process of observing network activity to identify suspicious behavior, security incidents, and possible attacks.

Important network security concepts include:

- Network visibility
- Asset identification
- Traffic monitoring
- Network segmentation
- Firewalls
- Intrusion Detection Systems
- Intrusion Prevention Systems
- Network logs
- Packet captures
- Baseline network behavior
- Indicators of compromise

A security analyst needs to understand what normal network traffic looks like before identifying abnormal or malicious behavior.

### Network Discovery Detection

Attackers perform network discovery to learn about systems, services, users, devices, and network architecture.

Common network discovery activities include:

- Host discovery
- Port scanning
- Service enumeration
- Operating system detection
- Network share discovery
- ARP scanning
- DNS enumeration
- Repeated connection attempts

Possible indicators of network discovery include:

- One source IP contacting many destination IP addresses
- One host attempting connections to many ports
- A large number of SYN packets
- Repeated failed connection attempts
- Unusual ICMP activity
- Sequential port access
- Unexpected internal scanning

Network discovery may occur before exploitation, privilege escalation, or lateral movement.

### Data Exfiltration Detection

Data exfiltration is the unauthorized transfer of information from an organization to an external destination.

Attackers may exfiltrate data through:

- HTTP or HTTPS
- DNS
- FTP
- Email
- Cloud storage
- Remote access tools
- Encrypted tunnels
- Unusual outbound connections

Possible indicators of data exfiltration include:

- Large outbound data transfers
- Connections to unusual external destinations
- Data transfers outside normal working hours
- Repeated DNS queries containing unusual data
- Long or encoded domain names
- Unexpected uploads
- Traffic using uncommon ports
- Sudden increases in outbound traffic

Encrypted traffic can make investigations more difficult because analysts may not be able to inspect the transferred content directly. However, metadata such as destination, frequency, size, timing, and protocol can still provide useful evidence.

### Man-in-the-Middle Detection

A Man-in-the-Middle attack occurs when an attacker intercepts or manipulates communication between two systems.

Possible MITM techniques include:

- ARP spoofing
- ARP poisoning
- DNS spoofing
- Rogue access points
- Session interception
- SSL stripping
- Traffic redirection

Possible indicators include:

- Unexpected MAC address changes
- Multiple IP addresses using the same MAC address
- Duplicate IP address warnings
- Unusual ARP replies
- Certificate warnings
- Unexpected DNS responses
- Traffic being redirected through an unknown device

Monitoring ARP traffic, DNS activity, certificates, and network topology can help identify possible MITM attacks.

### IDS Fundamentals

An Intrusion Detection System monitors network or host activity for signs of suspicious or malicious behavior.

Common IDS types include:

- Network-based IDS
- Host-based IDS
- Signature-based detection
- Anomaly-based detection

A Network Intrusion Detection System examines network traffic and generates alerts when activity matches known rules or suspicious patterns.

An IDS normally detects and alerts, while an IPS can actively block or prevent activity.

Important IDS concepts include:

- Rules
- Signatures
- Alerts
- False positives
- False negatives
- Network sensors
- Packet inspection
- Detection tuning
- Alert severity

### Snort

Snort is an open-source network intrusion detection and prevention tool.

Snort can be used to:

- Monitor live network traffic
- Analyze PCAP files
- Detect suspicious activity
- Generate alerts
- Apply detection rules
- Identify protocol anomalies
- Search for network-based indicators

A basic Snort rule contains:

- Action
- Protocol
- Source IP
- Source port
- Direction
- Destination IP
- Destination port
- Rule options

Example rule structure:

    alert tcp any any -> any 80 (msg:"HTTP traffic detected"; sid:1000001; rev:1;)

Rule components:

- alert: action to take
- tcp: protocol
- any any: source IP and source port
- ->: traffic direction
- any 80: destination IP and port
- msg: alert description
- sid: unique rule identifier
- rev: rule revision

Snort rules should be tested and tuned carefully to reduce false positives.

## What I Learned

This section helped me understand how network security monitoring supports threat detection and incident investigation.

I learned that attackers often leave recognizable patterns in network traffic. Scanning, discovery, data exfiltration, MITM activity, and command-and-control communication can generate evidence that a SOC analyst can investigate.

I also learned that network monitoring requires context. A connection or packet is not automatically malicious. The analyst must consider the systems involved, the protocol, the destination, the timing, the volume of traffic, and whether the activity is expected.

The Snort rooms helped me understand how IDS rules convert suspicious network behavior into alerts that analysts can review.

## Skills Practiced

- Understanding network security monitoring
- Identifying network discovery behavior
- Recognizing possible port scanning activity
- Detecting signs of data exfiltration
- Understanding MITM attack indicators
- Reviewing ARP and DNS activity
- Understanding IDS and IPS concepts
- Differentiating signature-based and anomaly-based detection
- Reading basic Snort rules
- Understanding Snort rule components
- Analyzing network alerts
- Thinking like a SOC analyst during network investigations

## Why This Matters for SOC Analysts

Network activity can provide important evidence during a security incident.

SOC analysts may need to determine whether an alert represents:

- Normal administrative activity
- Vulnerability scanning
- Unauthorized network discovery
- Malware communication
- Command-and-control activity
- Data exfiltration
- Lateral movement
- A Man-in-the-Middle attack
- A false positive

Network security monitoring helps analysts detect attacks that may not be visible through endpoint logs alone.

Understanding IDS alerts and Snort rules is especially useful because SOC analysts often work with network alerts generated by sensors, firewalls, SIEM platforms, and intrusion detection systems.

## Investigation Questions to Ask

During a network security investigation, a SOC analyst should ask:

- What source IP generated the activity?
- What destination IP was contacted?
- What ports and protocols were used?
- Is the source system authorized to perform this activity?
- Is the destination internal or external?
- Is the destination known or suspicious?
- Did one system contact many hosts?
- Did one system attempt connections to many ports?
- Was there an unusual amount of outbound traffic?
- Did the activity occur outside normal working hours?
- Are there unusual DNS queries?
- Are there repeated ARP responses?
- Did the IDS generate multiple related alerts?
- Is the traffic encrypted?
- Does the activity match known attacker behavior?
- Is there evidence of lateral movement?
- Is there evidence of data exfiltration?
- Should the alert be escalated?

## Useful Wireshark Filter Examples

Filter by IP address:

    ip.addr == <IP_ADDRESS>

Filter by source IP:

    ip.src == <SOURCE_IP>

Filter by destination IP:

    ip.dst == <DESTINATION_IP>

Filter TCP traffic:

    tcp

Filter UDP traffic:

    udp

Filter DNS traffic:

    dns

Filter ARP traffic:

    arp

Filter ICMP traffic:

    icmp

Filter HTTP traffic:

    http

Filter by TCP port:

    tcp.port == <PORT>

Filter by UDP port:

    udp.port == <PORT>

Display SYN packets:

    tcp.flags.syn == 1 && tcp.flags.ack == 0

Display TCP reset packets:

    tcp.flags.reset == 1

Display DNS queries:

    dns.flags.response == 0

Display DNS responses:

    dns.flags.response == 1

Display large packets:

    frame.len > 1000

Filter traffic between two IP addresses:

    ip.addr == <IP_ADDRESS_1> && ip.addr == <IP_ADDRESS_2>

## Useful Snort Command Examples

Display Snort version:

    snort -V

Test the Snort configuration:

    sudo snort -T -c /etc/snort/snort.conf

Run Snort in packet-sniffing mode:

    sudo snort -v -i <INTERFACE>

Display packet headers:

    sudo snort -d -i <INTERFACE>

Display packet headers and link-layer information:

    sudo snort -de -i <INTERFACE>

Analyze a PCAP file:

    sudo snort -r <FILE.pcap>

Analyze a PCAP using a configuration file:

    sudo snort -c /etc/snort/snort.conf -r <FILE.pcap>

Run Snort with a local rules file:

    sudo snort -c /etc/snort/snort.conf -R local.rules -r <FILE.pcap>

The exact Snort paths and arguments can vary depending on the operating system, Snort version, and lab environment.

## Example Snort Rules

Detect ICMP traffic:

    alert icmp any any -> any any (msg:"ICMP traffic detected"; sid:1000001; rev:1;)

Detect traffic to TCP port 80:

    alert tcp any any -> any 80 (msg:"HTTP traffic detected"; sid:1000002; rev:1;)

Detect traffic to TCP port 22:

    alert tcp any any -> any 22 (msg:"SSH traffic detected"; sid:1000003; rev:1;)

Detect DNS traffic:

    alert udp any any -> any 53 (msg:"DNS traffic detected"; sid:1000004; rev:1;)

These examples are for educational purposes and should be tested in an authorized lab environment.

## Reflection

This section helped me connect network traffic analysis with active security monitoring and alert detection.

I learned that network security monitoring is not only about capturing packets. It involves understanding normal network behavior, identifying suspicious patterns, reviewing alerts, correlating evidence, and deciding whether activity should be escalated.

The network discovery and data exfiltration rooms showed me how attackers can leave different types of network footprints. The MITM room helped me understand how ARP, DNS, certificates, and traffic redirection can reveal interception attempts.

The IDS and Snort rooms were especially useful because they showed me how network activity can be converted into detection rules and security alerts.

This knowledge is relevant to SOC Level 1 work because analysts frequently investigate alerts involving IP addresses, ports, protocols, unusual connections, scanning, malware communication, and suspicious outbound traffic.

## Disclaimer

This repository is for educational purposes only.

All labs and exercises were completed in authorized training environments such as TryHackMe.

The commands and Snort rules included here are basic educational examples. They should only be used in systems and networks where explicit authorization has been granted.

No flags, answers, credentials, private information, or sensitive data are included.
