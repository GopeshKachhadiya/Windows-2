# Windows-2
Rejetto HFS Vulnerable Lab – CVE-2024-23692
---
## Overview

This project demonstrates a deliberately vulnerable Windows lab based on Rejetto HTTP File Server (HFS), showcasing unauthenticated Remote Code Execution (RCE) through a real-world vulnerability CVE-2024-23692.

The lab is designed for:

Offensive security learning

Red team practice

Internship / portfolio demonstration

Understanding real-world Windows exploitation chains

The environment simulates a small organization file-sharing server exposed internally, leading to initial compromise and privilege escalation.

---

## Vulnerability Summary

Software: Rejetto HFS (HTTP File Server)

Affected Version: 2.4.0 RC7 (and earlier vulnerable releases)

CVE ID: CVE-2024-23692

Vulnerability Type: Unauthenticated Remote Code Execution (RCE)

Attack Vector: Network (HTTP)

Authentication Required: ❌ No

User Interaction Required: ❌ No

Severity: 🔴 Critical (CVSS v3.x – Critical)

---

## Impact of CVE-2024-23692

This vulnerability allows an unauthenticated remote attacker to:

Execute arbitrary system commands

Gain remote shell access

Compromise the entire Windows host

Use the server as a pivot point for lateral movement

Escalate privileges to SYSTEM if misconfigurations exist

Real-World Risk

If exploited in production:

Complete server takeover

Data theft or deletion

Malware or ransomware deployment

Internal network compromise

## Technical Root Cause

Rejetto HFS supports macro-based scripting and event handling.
Due to insufficient input validation, attacker-controlled input is processed and executed by the server, leading to command execution without authentication.

This lab keeps:

Scripting enabled

No authentication

Default insecure configuration

to intentionally expose the vulnerability.

## Lab Environment

Target Machine

Operating System: Windows 10 Pro (64-bit)

Application: Rejetto HFS 2.4.0 RC7

Service Port: TCP 80

User Account: john (standard user)

Architecture: x64

Attacker Machine

Kali Linux (or Parrot OS)

Metasploit Framework

Same virtual network as target

## System Requirements
Host System

Minimum 8 GB RAM

Virtualization enabled (Intel VT-x / AMD-V)

VMware Workstation / VirtualBox

Target VM (Windows)

2 GB RAM (minimum)

1 CPU core

20 GB disk

Network: NAT or Host-Only

Attacker VM (Linux)

2 GB RAM

Metasploit Framework installed

## How to Recreate This Vulnerable Machine

Step 1: Install Windows 10

Create a Windows 10 Pro VM

Disable Windows Defender (lab only)

Disable Windows Firewall

Step 2: Install Rejetto HFS

Download Rejetto HFS 2.4.0 RC7

Run hfs.exe as Administrator

Allow network access when prompted

Step 3: Configure Vulnerable Settings

Inside HFS:

Enable Expert Mode

Ensure event scripting is accessible

Do NOT enable authentication

Use default configuration

Run server on port 80

Step 4: Add Realism

Create user:

john


Create shared directory:

C:\Shares\Public


Place sample files inside

Step 5: Verify

From another machine:

http://TARGET-IP/


You should see:

HttpFileServer 2.4.0 RC7

## Exploitation Flow (High-Level)

Network scanning identifies open HTTP service

Version enumeration reveals vulnerable HFS release

Exploitation of CVE-2024-23692

Unauthenticated remote code execution

Reverse shell obtained

Local enumeration

Privilege escalation to SYSTEM

🔑 Learning Outcomes

By completing this lab, a learner gains experience in:

Windows service enumeration

Exploiting unauthenticated RCE vulnerabilities

Understanding insecure server configurations

Post-exploitation enumeration

Privilege escalation techniques

Building real-world offensive security labs

⚠️ Disclaimer

This project is created strictly for educational and ethical security research purposes.

Do NOT deploy this configuration in production

Do NOT expose this machine to the public internet

The author is not responsible for misuse

🧑‍💻 Author
Created By Gopesh Kachhadiya 
Created as part of an Offensive Cybersecurity Internship Project
Focused on real-world vulnerability exploitation and lab design.
