# TryHackMe SOC Level 1 - Cyber Defence Frameworks

## Overview

This section introduced important cyber defence frameworks used by security teams to understand attacker behavior, improve detection, support alert triage, and strengthen incident response.

The main focus was learning how frameworks such as the Pyramid of Pain, Cyber Kill Chain, Unified Kill Chain, and MITRE ATT&CK help defenders understand attacks and organize security investigations.

## Rooms Completed

- Pyramid of Pain
- Cyber Kill Chain
- Unified Kill Chain
- MITRE
- Summit
- Eviction

## Key Concepts Learned

### Pyramid of Pain

The Pyramid of Pain explains different types of indicators that defenders can use to detect and disrupt attackers.

The higher an indicator is on the pyramid, the more difficult it is for an attacker to change.

Common levels include:

- Hash values
- IP addresses
- Domain names
- Network artifacts
- Host artifacts
- Tools
- Tactics, Techniques, and Procedures

This helped me understand that blocking simple indicators like IP addresses or hashes can be useful, but detecting attacker behavior and TTPs is much more powerful.

### Cyber Kill Chain

The Cyber Kill Chain is a framework that explains the stages an attacker may follow during an intrusion.

The stages include:

- Reconnaissance
- Weaponization
- Delivery
- Exploitation
- Installation
- Command and Control
- Actions on Objectives

This helped me understand how defenders can detect and stop attacks at different stages before the attacker reaches their final goal.

### Unified Kill Chain

The Unified Kill Chain expands on traditional attack lifecycle models by including more detailed phases of an attack.

It helps defenders understand how attacks can move from initial access to persistence, privilege escalation, lateral movement, and final impact.

This framework is useful because real-world attacks are not always linear. Attackers may repeat steps, change techniques, or move through different systems before achieving their objective.

### MITRE ATT&CK

MITRE ATT&CK is a knowledge base of adversary tactics, techniques, and procedures based on real-world observations.

It helps security teams map attacker behavior to known techniques.

Examples of MITRE ATT&CK tactics include:

- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Exfiltration
- Command and Control
- Impact

MITRE ATT&CK is useful for SOC analysts because it helps classify suspicious activity and understand what an attacker may be trying to do.

### Summit and Eviction

These rooms helped reinforce how defenders can use cyber defence frameworks to track adversary behavior and respond to attacks.

The main idea was learning how to follow attacker activity, understand their techniques, and use defensive knowledge to detect and remove threats from an environment.

## What I Learned

This section helped me understand that cyber defence is not only about reacting to alerts. It is also about understanding attacker behavior and using structured frameworks to make better decisions.

I learned that frameworks help SOC analysts answer important questions such as:

- What stage of the attack are we seeing?
- What technique is the attacker using?
- What evidence do we have?
- What indicators are useful?
- How difficult would it be for the attacker to change this behavior?
- How can we improve detection?

The biggest lesson from this section was that detecting behavior is stronger than only blocking simple indicators.

## Skills Practiced

- Understanding cyber defence frameworks
- Mapping attacker activity to attack stages
- Learning the Pyramid of Pain
- Understanding the Cyber Kill Chain
- Understanding the Unified Kill Chain
- Using MITRE ATT&CK concepts
- Thinking like a SOC analyst during investigations
- Connecting indicators, tactics, techniques, and procedures

## Why This Matters for SOC Analysts

SOC analysts need frameworks because alerts by themselves do not always explain the full story.

Frameworks help analysts organize evidence, understand attacker goals, communicate findings, and decide what actions should be taken next.

For example:

- The Pyramid of Pain helps identify stronger detection opportunities.
- The Cyber Kill Chain helps understand attack progression.
- The Unified Kill Chain helps analyze more complex attacks.
- MITRE ATT&CK helps map activity to known adversary techniques.

## Reflection

This section was important because it helped me connect individual alerts and indicators to a bigger attack story.

Before this section, I understood that attackers use tools, IP addresses, domains, and malware. After this section, I better understand that defenders need to focus on attacker behavior, patterns, and techniques.

This connects directly to real SOC work because analysts need to classify alerts, understand attack stages, document findings, and escalate incidents using a structured approach.

## Disclaimer

This repository is for educational purposes only. All labs and exercises were completed in authorized training environments such as TryHackMe. No flags, answers, or sensitive information are included.
