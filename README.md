# Enterprise Active Directory Attack-Path & Purple-Team Security Assessment

## Overview

An authorized security assessment of a Windows Active Directory environment focused on attack-path discovery, privilege escalation, delegation abuse, credential exposure, remediation, detection and retesting.

## Environment

- Domain: AD.lab
- Domain Controller: DC01
- Windows Server 2022
- Windows 10 domain-joined client
- Kali Linux assessment workstation
- BloodHound Community Edition
- Impacket
- NetExec
- Nmap
- Hashcat

## Assessment Methodology

1. Network reconnaissance
2. SMB/LDAP enumeration
3. Active Directory enumeration
4. BloodHound attack-path analysis
5. ACL analysis
6. Delegation assessment
7. Kerberos attack assessment
8. Attack-path validation
9. Detection analysis
10. Remediation
11. Retesting
12. Final risk assessment

## Key Findings

### AP-01 — RBCD / Excessive Active Directory ACL

USER1 possessed excessive control over an AD computer object, enabling an attack path involving resource-based constrained delegation.

Impact:
- Computer-account manipulation
- Kerberos delegation abuse
- Privileged remote execution on CLIENT

Severity: High

### AP-02 — Kerberoastable Service Account

The MYSQL account possessed a service principal name and was vulnerable to Kerberoasting.

Impact:
- TGS credential exposure
- Offline password cracking
- Potential credential compromise

Severity: Medium/High

### AP-03 — Delegation Review

Delegation configuration was assessed. The domain controller's unconstrained delegation configuration was identified and treated as an architectural condition rather than an independent finding.

### AP-04 — Domain Admin Membership Review

LOCALADMIN was identified as a member of Domain Admins.

This requires administrative review to determine whether the privilege assignment is intentional.

## Purple-Team Validation

Attack paths were validated using:

- BloodHound
- LDAP ACL inspection
- NetExec
- Impacket
- Kerberos S4U
- RBCD validation
- Remote execution testing

## Remediation

- Removed excessive USER1 control from CLIENT
- Removed temporary AP01 computer account
- Removed temporary AP01 RBCD relationship
- Retested Active Directory permissions
- Re-collected BloodHound data
- Compared BEFORE and AFTER attack paths

## Retesting

The direct USER1 → CLIENT GenericAll relationship was no longer present after remediation.

An alternate delegation path involving ATTACKBOX remained and was documented separately.

## Detection Opportunities

Relevant telemetry includes:

- Windows Security Event Logs
- Directory Service changes
- Computer-account creation
- Changes to msDS-AllowedToActOnBehalfOfOtherIdentity
- Kerberos service-ticket activity
- Privileged logon events
- Remote service execution

## Conclusion

The assessment demonstrated how excessive Active Directory permissions and delegation relationships can combine to create practical attack paths.

The assessment followed an attack → validate → remediate → retest methodology rather than relying solely on vulnerability enumeration.
