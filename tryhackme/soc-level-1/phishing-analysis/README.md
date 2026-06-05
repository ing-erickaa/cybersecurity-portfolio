# TryHackMe SOC Level 1 - Phishing Analysis

## Overview

This section focused on analyzing and defending against phishing emails.

The main goal was to understand how phishing attacks work, how to identify suspicious indicators, how to use analysis tools, and how SOC analysts can investigate malicious emails and URLs.

## Rooms Completed

- Phishing Analysis Fundamentals
- Phishing Emails in Action
- Phishing Analysis Tools
- Phishing Prevention
- The Greenholt Phish
- Snapped Phish-ing Line

## Key Concepts Learned

### Phishing Analysis Fundamentals

Phishing analysis begins with understanding the structure of an email.

Important email components include:

- Sender address
- Recipient address
- Subject line
- Message body
- Links
- Attachments
- Email headers
- Reply-To address
- Return-Path
- SPF, DKIM, and DMARC results

Understanding these components helps analysts determine whether an email is legitimate, suspicious, or malicious.

### Phishing Indicators

Phishing emails often contain warning signs that can help identify malicious intent.

Common phishing indicators include:

- Suspicious sender address
- Mismatched display name and email address
- Urgent or threatening language
- Unexpected attachments
- Suspicious links
- Fake login pages
- Grammar or spelling mistakes
- Requests for credentials
- Unusual domains
- Spoofed branding
- Shortened URLs

### Email Header Analysis

Email headers provide technical details about how an email traveled from sender to recipient.

Header analysis can help identify:

- Source IP addresses
- Mail servers involved
- Authentication results
- Spoofing attempts
- Suspicious routing
- Failed SPF, DKIM, or DMARC checks

This is important because attackers can fake what users see in the email body, but headers can reveal more technical evidence.

### Phishing Analysis Tools

SOC analysts use different tools to investigate suspicious emails, links, attachments, and domains.

Useful analysis tools include:

- URL scanners
- Domain reputation tools
- Email header analyzers
- Sandbox tools
- Threat intelligence platforms
- VirusTotal
- CyberChef
- WHOIS lookup
- URLScan
- MXToolbox

These tools help analysts collect evidence and decide whether an email should be classified as benign, suspicious, or malicious.

### Phishing Prevention

Phishing prevention requires both technical controls and user awareness.

Common prevention methods include:

- Security awareness training
- Email filtering
- Multi-factor authentication
- SPF, DKIM, and DMARC
- Blocking malicious domains
- Attachment sandboxing
- URL rewriting and scanning
- Reporting suspicious emails
- Least privilege access

Phishing cannot be fully eliminated, but organizations can reduce the risk by combining technology, training, and strong security processes.

### Realistic Phishing Investigation

The practical rooms helped reinforce how to analyze malicious emails and URLs in a realistic investigation.

The process included:

- Reviewing the email sender
- Checking links and domains
- Analyzing headers
- Looking for suspicious attachments
- Identifying indicators of compromise
- Using external analysis tools
- Making a classification decision
- Documenting findings

## What I Learned

This section helped me understand that phishing analysis is one of the most important skills for SOC Level 1 analysts.

I learned that a phishing investigation requires more than just reading the email. A SOC analyst must inspect technical details, analyze links, review headers, check reputation, and document evidence clearly.

I also learned that phishing is dangerous because it targets people directly and can lead to credential theft, malware infection, business email compromise, and unauthorized access.

## Skills Practiced

- Identifying phishing indicators
- Reviewing email components
- Understanding email headers
- Analyzing suspicious links
- Investigating domains
- Using phishing analysis tools
- Understanding SPF, DKIM, and DMARC at a basic level
- Classifying suspicious emails
- Documenting phishing findings
- Thinking like a SOC analyst

## Why This Matters for SOC Analysts

Phishing is one of the most common initial access methods used by attackers.

SOC analysts must know how to investigate suspicious emails because phishing can lead to:

- Credential theft
- Malware infection
- Account compromise
- Data theft
- Business email compromise
- Financial fraud
- Lateral movement inside a network

Being able to analyze phishing emails helps SOC teams detect threats early and prevent larger security incidents.

## Investigation Questions to Ask

During a phishing investigation, a SOC analyst should ask:

- Who sent the email?
- Is the sender legitimate?
- Does the domain look suspicious?
- Are there links in the message?
- Do the links match the visible text?
- Are there attachments?
- Are the attachments expected?
- Did SPF, DKIM, or DMARC pass?
- Does the email create urgency or fear?
- Is the user being asked to enter credentials?
- Are there known indicators of compromise?
- Should this be escalated?

## Reflection

This module was very useful because phishing analysis is directly connected to real SOC work.

I learned that phishing investigations require patience, attention to detail, and a structured process. The analyst must collect evidence, avoid assumptions, and explain why an email is suspicious or malicious.

This section also helped me understand how important documentation is. A good phishing report should explain what happened, what evidence was found, what risk exists, and what action should be taken.

## Disclaimer

This repository is for educational purposes only. All labs and exercises were completed in authorized training environments such as TryHackMe. No flags, answers, or sensitive information are included.
