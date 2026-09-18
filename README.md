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

This project is a hands-on **enterprise-style Active Directory security assessment** performed in a controlled laboratory environment.

The assessment focuses on identifying how **Active Directory permissions, delegation mechanisms, computer-account controls, Kerberos authentication, and privilege relationships can combine to create practical attack paths**.

Rather than treating vulnerabilities individually, the assessment follows the complete security lifecycle:

```text
Reconnaissance
      ↓
Active Directory Enumeration
      ↓
Attack-Path Analysis
      ↓
Controlled Validation
      ↓
Impact Assessment
      ↓
Remediation
      ↓
Retesting
      ↓
Final Validation

```

### 🏆 Key Assessment Results

| ID       | Assessment                                   | Severity            | Final Status             |
| -------- | -------------------------------------------- | ------------------- | ------------------------ |
| 🔴 AP-01 | Excessive ACL Permissions + RBCD Attack Path | High                | ✅ Remediated & Validated |
| 🟠 AP-02 | Kerberoastable Service Account               | Medium              | 🟡 Partially Remediated  |
| 🟡 AP-03 | AS-REP Roasting & Delegation Assessment      | Informational / Low | ✅ Assessed               |


##🔥 AP-01 — Excessive ACL Permissions + RBCD
High

A low-privileged domain user was identified with excessive control over the CLIENT computer object.

The assessment demonstrated that the identified Active Directory permissions could be combined with computer-account and Resource-Based Constrained Delegation (RBCD) techniques to achieve privileged remote execution against the CLIENT system.

Attack-Path Concept
```text
USER1
  │
  │ Excessive AD Permissions
  ▼
Computer Object Control
  │
  │ RBCD / Kerberos
  ▼
Privileged Service Ticket
  │
  ▼
Remote Execution

```
## Remediation
Removed excessive USER1 permissions.
Removed excessive ATTACKBOX permissions.
Removed temporary assessment computer account.
Removed temporary RBCD configuration.
Revalidated Active Directory permissions.
Performed fresh BloodHound collection.
# Retest

The original USER1 → CLIENT attack path was no longer identified after remediation.

# Result: ✅ PASS — Remediated and Validated

### 🔑 AP-02 — Kerberoastable Service Account
# Medium

The MYSQL service account was identified with a registered Service Principal Name (SPN):
```text
     DC01/mysql.AD.lab:60500
```
The account was successfully assessed for Kerberoasting.

A Kerberos service ticket was obtained and subjected to offline password-cracking analysis. Credential recovery was successfully demonstrated.

## Privilege Assessment

The account was subsequently assessed for privilege relationships.
```text
MYSQL
  │
  └──→ DOMAIN ADMINS
          No Path
```
No demonstrated MYSQL → Domain Admin attack path was identified.

### Remediation
   1.Reviewed MYSQL group membership.
   2.Removed excessive group memberships.
   3.Validated final LDAP membership.
   4.Reassessed the account's privileges.

### Remaining Recommendation

The exposed service-account credential had not been rotated during the final assessment.

Recommended follow-up:

  1.Rotate the exposed credential.
  2.Use a strong, unique service-account password.
  3.Consider a gMSA where appropriate.
  4.Review Password Never Expires.
  5.Review SPN necessity.
  6.Maintain least privilege.

## Result: 🟡 PARTIAL PASS — Privilege exposure reduced; credential rotation recommended


### 🔐 AP-03 — AS-REP Roasting & Delegation

# Informational / Low

An account configured without Kerberos preauthentication was identified as susceptible to AS-REP Roasting.

AS-REP authentication material was obtained for controlled offline analysis.

The available password list was exhausted without recovering the credential.

# Privilege Assessment
```text
ASREP
  │
  └──→ DOMAIN ADMINS
          No Path
```
No demonstrated ASREP → Domain Admin attack path was identified.

## Delegation Assessment

Delegation configurations were also reviewed.

DC01 was identified with unconstrained delegation. Because DC01 is the domain controller, this configuration was treated as an architectural characteristic rather than automatically classified as an exploitable vulnerability.

An existing ATTACKBOX → CLIENT RBCD relationship was also observed and was assessed as part of AP-01.

# Result: ✅ Assessment completed — No demonstrated privilege-compromise path


### 🧠 Skills Demonstrated

 # Active Directory Security
   - Active Directory reconnaissance
   - LDAP enumeration
   - SMB enumeration
   - User, group and computer enumeration
   - AD ACL analysis
   - Delegated-permission analysis
   - Privileged group analysis
   - Machine Account Quota assessment
   - RBCD assessment
   - Kerberos security assessment
   - Attack-path analysis
 
 # Attack Techniques
   - Resource-Based Constrained Delegation
   - Kerberoasting
   - AS-REP Roasting
   - Kerberos ticket abuse
   - Controlled remote execution
   - Computer-account abuse assessment
   - Privilege relationship analysis
   - Lateral movement assessment

 # Defensive & Assessment Skills
   - Evidence collection
   - Security finding documentation 
   - Risk/impact analysis
   - Remediation
   - Active Directory hardening
   - Detection recommendations
   - Post-remediation validation
   - BloodHound-based retesting


### 🛠️ Tools & Technologies
| Category                       | Tools                            |
| ------------------------------ | -------------------------------- |
| Operating System               | Kali Linux                       |
| AD Attack-Path Analysis        | BloodHound                       |
| Network Reconnaissance         | Nmap                             |
| AD / SMB Enumeration           | NetExec                          |
| AD / Kerberos Assessment       | Impacket                         |
| Password Analysis              | Hashcat                          |
| Directory Services             | LDAP                             |
| File / Authentication Services | SMB                              |
| Target Environment             | Windows Server 2022 / Windows 10 |

# Primary Impacket Components
  ```text
  dacledit
  rbcd
  getST
  GetUserSPNs
  GetNPUsers
```

### 🏗️ Laboratory Environment
 ```text
                         ┌──────────────────────┐
                         │       AD.lab         │
                         │  Active Directory    │
                         └──────────┬───────────┘
                                    │
                           ┌────────▼────────┐
                           │      DC01       │
                           │ Windows Server  │
                           │ Domain Controller│
                           └────────┬────────┘
                                    │
                    ┌───────────────┴───────────────┐
                    │                               │
             ┌──────▼──────┐                 ┌──────▼──────┐
             │    CLIENT   │                 │  ATTACKBOX  │
             │  Windows 10 │                 │ Domain Host │
             └─────────────┘                 └─────────────┘


## Environment Details
Domain:   AD.lab
Network:  192.168.88.0/24
DC01:     192.168.88.10
CLIENT:   192.168.88.136

```
### 🔬 Assessment Methodology
The assessment followed an evidence-driven workflow:
 ```text
   01  Reconnaissance
           ↓
   02  AD Enumeration
           ↓
   03  Attack-Path Discovery
           ↓
   04  Controlled Validation
           ↓
   05  Impact Assessment
           ↓
   06  Remediation
           ↓
   07  Retesting
           ↓
   08  Final Validation

 ```
## Assessment Principles

A theoretical relationship was not automatically treated as a successful compromise.

The project distinguishes between:

   - Identified configuration weaknesses
   - Potential attack paths
   - Demonstrated exploitation
   - Credential exposure
   - Unsuccessful credential recovery
   - Remediated findings
   - Outstanding recommendations

This keeps the assessment aligned with the evidence actually obtained during testing.

### 📊 Final Validation

# AP-01
Before
```text
    USER1 → CLIENT
```
Excessive permissions and delegation relationships allowed the attack path to be validated.

After\
```text
   USER1 → CLIENT
```
No Path

✅ Remediation validated

# AP-02
Credential Exposure
```text
MYSQL
  ↓
Kerberos TGS
  ↓
Offline Password Cracking
  ↓
Credential Recovered
```

Final Privilege Path
```text
MYSQL → DOMAIN ADMINS
```
No Path

🟡 Privilege exposure reduced

Credential rotation remains recommended.

# AP-03
AS-REP Assessment

```text
ASREP
  ↓
AS-REP Response
  ↓
Offline Cracking
  ↓
Credential Not Recovered
```

Final Privilege Path
```text 
ASREP → DOMAIN ADMINS
```
No Path

✅ No demonstrated privilege-compromise path


### 🛡️ Detection & Defensive Perspective

The assessment also documents defensive telemetry and detection opportunities related to the techniques evaluated.

Areas of interest include:

   - Active Directory security-descriptor changes
   - RBCD modifications
   - Computer-account creation
   - Kerberos TGS request patterns
   - AS-REP activity
   - Privileged authentication
   - Remote execution
   - Group-membership changes

Detection recommendations are documented separately. The project does not claim that a production SIEM detection fired unless corresponding event evidence was captured.

### 🔗 Assessment Navigation
| Phase             | Documentation                               |
| ----------------- | ------------------------------------------- |
| 🔎 Reconnaissance | [`01.Recon`](./01.Recon/)                   |
| 🏢 AD Enumeration | [`02.ad-enumeration`](./02.ad-enumeration/) |
| 🔥 Attack Paths   | [`03.attack-path`](./03.attack-path/)       |
| 📸 Evidence       | [`04.evidence`](./04.evidence/)             |
| 🛡️ Detection      | [`05.detection`](./05.detection/)           |
| 🔧 Remediation    | [`06.remediation`](./06.remediation/)       |
| 🔄 Retesting      | [`07.retest`](./07.retest/)                 |
| 📋 Final Findings | [`08.report`](./08.report/)                 |


### 📌 Project Takeaways

This project demonstrates practical experience with:

Active Directory enumeration → attack-path discovery → controlled exploitation → security impact analysis → remediation → post-remediation validation

The primary objective was not simply to obtain access, but to understand why the access path existed, how the underlying permissions contributed to the path, how the weakness could be remediated, and whether the remediation actually removed the path.

### ⚠️ Disclaimer

This project was conducted exclusively within a controlled and authorized laboratory environment for cybersecurity education, practical skill development, and professional portfolio purposes.

No unauthorized systems were targeted.

All credentials and sensitive assessment artifacts have been intentionally excluded from the public repository.


