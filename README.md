# Windows-2 

# BlueKeep Vulnerable Lab - CVE-2019-0708

## 1. Overview

This repository contains a deliberately vulnerable Windows lab designed to demonstrate the BlueKeep vulnerability affecting the Remote Desktop Protocol (RDP) service.

BlueKeep is a critical pre-authentication Remote Code Execution (RCE) vulnerability that exists in the Windows kernel. The vulnerability allows an unauthenticated attacker to remotely trigger memory corruption through the RDP service, potentially leading to full system compromise or denial of service.

This lab is created strictly for educational and defensive security research purposes and simulates a real-world legacy Windows system commonly found in enterprise environments.

The project is intended for:

- Offensive security learning
- Penetration testing practice
- Internship and portfolio demonstration
- Understanding real-world Windows kernel exploitation behavior
- Studying exploit instability in production-like environments

The environment represents a small organization workstation with exposed RDP services and missing security patches.

---

## 🔗 Project Resources

- **Lab Download:**  
  https://mega.nz/file/3R5mRB6A#gtvvxQ1RbT1lxdeCp8hiV5vzAhftI-_5_rojq0bZX_w

- **Documentation & Walkthrough:**  
  https://mega.nz/file/DRB2lKRY#1iWeAi_m2VHuvS5VHZzwmYPfRfZ5pGkrRcGaoRWSxe8

- **Bruteforce Resources:**  
  - Username Wordlist: https://mega.nz/file/bBgnjTAT#6oXhVVIwlLo6p5B2iltI4ixC50yIiKtaQvqq8kLk_fg  
  - Password Wordlist: https://mega.nz/file/qF5RHCpJ#f0ggoGrMh0jHhgupBxS3Jnv7DxIjzF5hjUqMdm4IX7s

- **VMware Setup & Usage Guide:**  
  https://mega.nz/file/WEADkSZI#MvjDTY0KfGxxmyVezcEnAjdz48AQ1adV4XlW9lmhSVo

---

## 2. Vulnerability Summary

Software Name       : Microsoft Remote Desktop Protocol (RDP)
Operating System   : Windows 7 Professional SP1
CVE ID              : CVE-2019-0708
Vulnerability Name  : BlueKeep
Vulnerability Type  : Pre-Authentication Remote Code Execution
Affected Port       : 3389/TCP

CVSS v3 Score       : 9.8 (Critical)

CVSS Vector         :
AV:N / AC:L / PR:N / UI:N / S:U / C:H / I:H / A:H

---

## 3. Vulnerability Impact

The BlueKeep vulnerability allows an attacker to:

- Exploit the system without valid credentials
- Trigger kernel-level memory corruption
- Cause a remote Blue Screen of Death (Denial of Service)
- Potentially execute arbitrary code as NT AUTHORITY\SYSTEM
- Exploit the system in a wormable manner across networks

Because the flaw exists at the kernel level, exploitation is highly unstable. In many cases, successful triggering of the vulnerability results in system crashes rather than a reliable interactive shell.

---

## 4. Lab Objective

The objective of this lab is to:

- Identify exposed RDP services on a Windows host
- Validate the presence of CVE-2019-0708
- Exploit BlueKeep using the Metasploit Framework
- Understand kernel-level exploitation behavior
- Analyze why certain exploits cause crashes instead of shells
- Practice professional vulnerability documentation

---

## 5. System Requirements

Attacker Machine Requirements:

- Kali Linux (Recommended)
- Tools Installed:
  - Nmap
  - Metasploit Framework
  - arp-scan

Target Machine Requirements:

- Operating System : Windows 7 Professional SP1 (Unpatched)
- Architecture     : 64-bit
- RAM              : 2 GB
- CPU              : 1 Core
- Virtualization   : VMware Workstation
- Network Mode     : NAT or Host-Only

---

## 6. Target Machine Setup Instructions

To recreate the vulnerable BlueKeep machine, follow these steps:

1. Install Windows 7 Professional SP1
2. Do not install any Windows updates
3. Enable Remote Desktop
4. Disable Network Level Authentication (NLA)
5. Ensure port 3389 is accessible
6. Disable Windows Firewall for lab purposes
7. Reboot the system

Important Notes:

- If NLA is enabled, BlueKeep exploitation will fail
- If security updates are installed, the system will not be vulnerable
- This lab must be isolated from production networks

---

## 7. Attack Methodology Overview

The attack follows a standard penetration testing workflow:

1. Network discovery to identify live hosts
2. Service enumeration to detect exposed RDP
3. Vulnerability validation
4. Exploitation using Metasploit
5. Observation of kernel-level exploit behavior
6. Verification of user-level access indicators

---

## 8. Exploitation Behavior and Stability

BlueKeep exploitation is inherently unreliable due to:

- Kernel heap memory timing dependencies
- Heap grooming requirements
- Virtualization environment differences
- Modern CPU and memory protections

As a result:

- The system may crash repeatedly
- Blue Screen of Death is expected
- Multiple reboots may be required
- A stable Meterpreter session is not guaranteed

This behavior is normal and confirms successful triggering of the vulnerability.

---

## 9. Flags and Proof of Compromise

User Flag Location:

C:\Users\admin\Documents

Purpose:

The user flag represents confirmation of access to user-level data on the compromised system. Linux-style flags are simulated on Windows systems to demonstrate different access levels in a consistent lab format.

---

## 10. Security Disclaimer

This project is created strictly for:

- Educational use
- Ethical hacking practice
- Defensive security awareness

Exploiting systems without explicit authorization is illegal. The author is not responsible for any misuse of this lab or the information provided.

---

## 11. Learning Outcomes

By completing this lab, the following skills are developed:

- Understanding of pre-authentication RCE vulnerabilities
- Practical exposure to kernel-level exploitation
- Handling unstable exploits in real-world scenarios
- Windows service and protocol analysis
- Professional documentation and reporting

---

## 12. References

- CVE-2019-0708
- Microsoft Security Advisory
- Metasploit Framework Documentation
- Windows RDP Security Architecture

---

## 13 . Disclaimer

This lab is created strictly for educational and ethical penetration testing purposes. Do not deploy these configurations in production environments.

---

## Created By

- Name: Gopesh Kachhadiya
- Role: Junior Penetration Tester 
- Purpose: Internship Project and Skill Demonstration
- Domain: Offensive Security and AI Penetration Testing
- This lab was created as part of an offensive cybersecurity internship project focused on realistic attack simulations and hands-on learning.
