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


### 🏆 Key Assessment Results

| ID       | Assessment                                   | Severity            | Final Status             |
| -------- | -------------------------------------------- | ------------------- | ------------------------ |
| 🔴 AP-01 | Excessive ACL Permissions + RBCD Attack Path | High                | ✅ Remediated & Validated |
| 🟠 AP-02 | Kerberoastable Service Account               | Medium              | 🟡 Partially Remediated  |
| 🟡 AP-03 | AS-REP Roasting & Delegation Assessment      | Informational / Low | ✅ Assessed               |

