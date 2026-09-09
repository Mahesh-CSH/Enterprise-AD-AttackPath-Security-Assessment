# MITRE ATT&CK Mapping

This document maps the observed assessment activities to relevant MITRE ATT&CK techniques.

| Technique | ID | Assessment Relevance |
|---|---|---|
| Account Discovery | T1087 | Domain users and accounts were enumerated during AD reconnaissance. |
| Permission Groups Discovery | T1069 | Active Directory group memberships and privilege relationships were assessed. |
| Remote Services | T1021 | Remote authenticated execution against CLIENT was validated during AP-01. |
| Steal or Forge Kerberos Tickets | T1558 | Kerberos-based attacks were assessed during AP-01 and AP-02. |
| Steal or Forge Kerberos Tickets: Kerberoasting | T1558.003 | MYSQL service-ticket material was obtained and subjected to offline cracking. |
| Steal or Forge Kerberos Tickets: AS-REP Roasting | T1558.004 | ASREP was identified as AS-REP roastable and its response was tested offline. |
| Account Manipulation | T1098 | Active Directory permissions and account-control relationships were assessed. |
| Valid Accounts | T1078 | Authorized domain credentials were used during controlled validation. |

## AP-01

### Relevant Techniques

- T1087 — Account Discovery
- T1069 — Permission Groups Discovery
- T1021 — Remote Services
- T1558 — Steal or Forge Kerberos Tickets
- T1078 — Valid Accounts

The assessment demonstrated an attack path involving excessive Active Directory permissions, computer-account/RBCD techniques, Kerberos ticket abuse, and remote execution.

## AP-02

### Relevant Technique

**T1558.003 — Kerberoasting**

The MYSQL service account had an SPN. A Kerberos service ticket was obtained and successfully subjected to offline password cracking.

## AP-03

### Relevant Technique

**T1558.004 — AS-REP Roasting**

The ASREP account was identified as AS-REP roastable. Offline password cracking was attempted, but the credential was not recovered.

## Defensive Relevance

The mapped techniques highlight the importance of:

- Least-privilege Active Directory delegation
- Monitoring Kerberos service-ticket requests
- Monitoring AS-REP activity
- Reviewing computer-account permissions
- Monitoring RBCD changes
- Protecting service-account credentials
- Regularly reviewing privileged group membership
