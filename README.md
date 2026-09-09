# 🔐 Enterprise Active Directory Attack-Path & Security Assessment

### Attack-Path Discovery • Controlled Exploitation • Remediation • Retesting

> A hands-on Active Directory security assessment focused on identifying, validating, and remediating realistic privilege-escalation and credential-exposure attack paths in an enterprise-style Windows domain environment.

<p align="center">

![Active Directory](https://img.shields.io/badge/Active%20Directory-Security%20Assessment-0078D4?style=for-the-badge&logo=microsoft)
![BloodHound](https://img.shields.io/badge/BloodHound-Attack%20Path%20Analysis-red?style=for-the-badge)
![Kali Linux](https://img.shields.io/badge/Kali%20Linux-Penetration%20Testing-557C94?style=for-the-badge&logo=kalilinux)
![Windows Server](https://img.shields.io/badge/Windows%20Server-2022-0078D4?style=for-the-badge&logo=windows)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

</p>

---

## 🎯 Project Overview

This project simulates an **enterprise Active Directory security assessment** from initial reconnaissance through final remediation validation.

Rather than focusing only on individual vulnerabilities, the assessment analyzes how **Active Directory permissions, delegation, computer-account controls, Kerberos authentication, and privilege relationships can be chained together to create practical attack paths**.

### Assessment Lifecycle

┌──────────────┐
│Reconnaissance│
└──────┬───────┘
       ↓
┌──────────────────┐
│ AD Enumeration   │
└──────┬───────────┘
       ↓
┌──────────────────────┐
│ Attack-Path Analysis │
└──────┬───────────────┘
       ↓
┌──────────────────────┐
│ Controlled Validation│
└──────┬───────────────┘
       ↓
┌──────────────────────┐
│ Remediation          │
└──────┬───────────────┘
       ↓
┌──────────────────────┐
│ Retesting            │
└──────┬───────────────┘
       ↓
┌──────────────────────┐
│ Final Validation     │
└──────────────────────┘

🏆 Key Results
   Assessment Area	Result
🔴 AP-01 — ACL + RBCD Attack Path	Successfully demonstrated
🟠 AP-02 — Kerberoasting	Credential recovery demonstrated
🟡 AP-03 — AS-REP Roasting	Exposure identified; credential not recovered
🔎 BloodHound Attack-Path Analysis	Completed
🛠️ Remediation	Performed
🔁 Post-Remediation Retesting	Completed


Final Validation

AP-01: The original USER1 → CLIENT attack path was removed and validated through fresh Active Directory enumeration and BloodHound analysis.

AP-02: Excessive MYSQL privileges were reduced and no MYSQL → Domain Admin path was identified. Credential rotation remains a recommended follow-up because the assessment credential was recovered.

AP-03: AS-REP Roasting exposure was identified, but the credential was not recovered and no ASREP → Domain Admin path was demonstrated.


🔥 What This Project Demonstrates

1.Active Directory reconnaissance and enumeration
2.BloodHound attack-path analysis
3.AD ACL and delegated-permission analysis
4.Resource-Based Constrained Delegation (RBCD)
5.Machine Account Quota assessment
6.Kerberoasting
7.AS-REP Roasting
8.Kerberos ticket analysis
9.Privilege and group-membership review
10.Controlled remote execution validation
11.Security remediation
12.Post-remediation retesting
13.Evidence-driven security reporting


🛠️ Primary Toolset

Kali Linux
  ├── Nmap
  ├── NetExec
  ├── Impacket
  │   ├── dacledit
  │   ├── rbcd
  │   ├── getST
  │   ├── GetUserSPNs
  │   └── GetNPUsers
  ├── BloodHound
  ├── Hashcat
  └── LDAP / SMB tooling


🏗️ Lab Environment
                    ┌──────────────────────┐
                    │     AD.lab Domain    │
                    └──────────┬───────────┘
                               │
                       ┌───────▼───────┐
                       │      DC01     │
                       │ Windows Server│
                       │ Domain Control│
                       └───────┬───────┘
                               │
                    ┌──────────┴──────────┐
                    │                     │
             ┌──────▼──────┐       ┌──────▼──────┐
             │   CLIENT    │       │  ATTACKBOX  │
             │ Windows 10  │       │ Domain Host │
             └─────────────┘       └─────────────┘

Environment: Controlled lab network
Domain: AD.lab

All testing was performed against an authorized laboratory environment. Sensitive credentials, hashes, Kerberos tickets, password lists, and other secret material are excluded from the public repository.

🔥 Featured Attack Paths

AP-01 — Excessive ACL Permissions + RBCD
Severity: High

A low-privileged domain user was found with excessive control over the CLIENT computer object.
The assessment demonstrated how excessive AD permissions could be chained with computer-account and RBCD techniques to achieve privileged remote execution.
Result: ✅ Remediated and retested

AP-02 — Kerberoastable Service Account
Severity: Medium

The MYSQL service account possessed an SPN and was successfully assessed through Kerberoasting.
The resulting Kerberos service-ticket material was subjected to offline password cracking and the credential was recovered.
Excessive group membership was subsequently removed.
Result: 🟡 Privilege exposure reduced; credential rotation recommended

AP-03 — AS-REP Roasting & Delegation
Severity: Informational / Low

An AS-REP roastable account was identified and assessed.
The authentication material was subjected to offline password cracking, but the credential was not recovered.
No demonstrated path from the account to Domain Admin was identified.
Result: ✅ Assessment completed


📊 Project Structure

Enterprise-AD-attackpath-project/
  │
  ├── 01.Recon/
  ├── 02.ad-enumeration/
  ├── 03.attack-path/
  ├── 04.evidence/
  ├── 05.detection/
  ├── 06.remediation/
  ├── 07.retest/
  ├── 08.report/
  ├── README.md
  └── .gitignore

  
🔬 Assessment Philosophy

The project follows an evidence-driven approach:
Identify → Validate → Demonstrate Impact → Remediate → Retest
A theoretical relationship was not automatically treated as a successful compromise. Attack paths were validated where practical, unsuccessful credential-recovery attempts were documented as unsuccessful, and remediation was followed by fresh validation.


📸 Evidence

Selected sanitized screenshots and command-output evidence are available under:
|-->04.evidence/
The repository intentionally excludes sensitive credential material.


⚠️ Disclaimer

This project was conducted entirely within a controlled and authorized laboratory environment for cybersecurity learning and professional portfolio development.
No unauthorized systems were targeted.

