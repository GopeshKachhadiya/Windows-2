# Windows-2

# Rejetto HFS Vulnerable Lab – CVE-2024-23692

1. Overview
-----------
This repository contains a deliberately vulnerable Windows lab built
around Rejetto HTTP File Server (HFS). The lab demonstrates a real-world
unauthenticated Remote Code Execution (RCE) vulnerability identified as
CVE-2024-23692.

The project is intended for:
- Offensive security learning
- Red team practice
- Internship and portfolio demonstration
- Understanding real-world Windows exploitation workflows

The environment simulates a small organization file-sharing server that
is vulnerable due to insecure default configuration and outdated
software.

---------------------------------------------------------------------

2. Vulnerability Summary
------------------------
- Software Name        : Rejetto HTTP File Server (HFS)
- Affected Version     : 2.4.0 RC7
- CVE ID               : CVE-2024-23692
- Vulnerability Type   : Unauthenticated Remote Code Execution (RCE)
- Attack Vector        : Network (HTTP)
- Authentication       : Not required
- User Interaction     : Not required
- Severity             : Critical

---------------------------------------------------------------------

3. CVSS Severity and Score
--------------------------
- CVSS Version         : v3.1
- Base Score           : 9.8 (Critical)
- Vector               : AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H

This score indicates that the vulnerability can be exploited remotely
over the network with no authentication or user interaction and leads
to full system compromise.

---------------------------------------------------------------------

4. Impact
---------
If successfully exploited, this vulnerability allows an attacker to:

- Execute arbitrary operating system commands
- Gain unauthenticated remote shell access
- Fully compromise the Windows host
- Escalate privileges to SYSTEM if misconfigurations exist
- Pivot to other internal machines
- Deploy malware, ransomware, or persistence mechanisms
- Access, modify, or destroy sensitive data

---------------------------------------------------------------------

5. Technical Root Cause
-----------------------
Rejetto HFS supports macro-based scripting and event handling to process
HTTP requests. In vulnerable versions, user-supplied input is not
properly sanitized before being processed by the scripting engine.

This results in arbitrary command execution when crafted HTTP requests
are sent to the server. The default configuration leaves scripting
enabled and does not enforce authentication, making exploitation
trivial.

---------------------------------------------------------------------

6. Lab Environment
------------------

Target Machine:
- Operating System     : Windows 10 Pro (64-bit)
- Application          : Rejetto HFS 2.4.0 RC7
- Service Port         : TCP 80
- User Account         : john (standard user)
- Architecture         : x64

Attacker Machine:
- Operating System     : Kali Linux or Parrot OS
- Tools                : Metasploit Framework
- Network              : Same virtual network as target

---------------------------------------------------------------------

7. System Requirements
----------------------

Host System:
- Minimum RAM          : 8 GB
- Virtualization       : Enabled (Intel VT-x / AMD-V)
- Hypervisor           : VMware Workstation or VirtualBox

Target VM (Windows):
- RAM                  : 2 GB minimum
- CPU                  : 1 core
- Disk                 : 20 GB
- Network Adapter      : NAT or Host-Only

Attacker VM (Linux):
- RAM                  : 2 GB minimum
- Tools                : Metasploit Framework installed

---------------------------------------------------------------------

8. Steps to Recreate the Vulnerable Machine
-------------------------------------------

Step 1: Install Windows 10
- Create a new Windows 10 Pro virtual machine
- Complete standard OS installation
- Disable Windows Defender (lab use only)
- Disable Windows Firewall

Step 2: Install Rejetto HFS
- Download Rejetto HFS version 2.4.0 RC7
- Run hfs.exe as Administrator
- Allow network access when prompted

Step 3: Configure Vulnerable Settings
- Enable Expert Mode in HFS
- Ensure event scripting is accessible
- Do not configure authentication
- Keep default insecure settings
- Run the server on TCP port 80

Step 4: Add Realism
- Create a standard user named "john"
- Create a shared directory:
  C:\Shares\Public
- Add sample files to the shared directory

Step 5: Verification
- Access the server from another machine:
  http://TARGET-IP/
- Confirm the banner shows:
  HttpFileServer 2.4.0 RC7

---------------------------------------------------------------------

9. Exploitation Flow (High-Level)
---------------------------------
1. Network scan identifies an open HTTP service
2. Version enumeration reveals vulnerable HFS version
3. CVE-2024-23692 is exploited remotely
4. Unauthenticated remote code execution is achieved
5. Reverse shell is obtained
6. Local enumeration is performed
7. Privilege escalation to SYSTEM is completed

---------------------------------------------------------------------

10. Learning Outcomes
---------------------
By completing this lab, a learner gains practical experience in:

- Identifying vulnerable Windows services
- Exploiting unauthenticated RCE vulnerabilities
- Understanding insecure server configurations
- Performing post-exploitation enumeration
- Executing privilege escalation techniques
- Designing realistic offensive security labs

---------------------------------------------------------------------

11. Repository Structure (Suggested)
------------------------------------
Rejetto-HFS-CVE-2024-23692/
│
├── README.txt
├── setup-guide/
│   └── windows-setup.txt
├── exploitation/
│   └── attack-flow.txt
├── flags/
│   ├── user.txt
│   └── root.txt

---------------------------------------------------------------------

12. Disclaimer
--------------
This project is created strictly for educational and ethical security
research purposes.

- Do not deploy this configuration in production
- Do not expose this machine to the public internet
- The author is not responsible for misuse or illegal activity

---------------------------------------------------------------------

13. Author
----------
Created as part of an Offensive Cybersecurity Internship Project,
focusing on real-world vulnerability exploitation and lab design.
