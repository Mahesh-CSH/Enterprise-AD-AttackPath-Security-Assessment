# Executive Summary

## Assessment Overview

An internal Active Directory security assessment was conducted against a controlled enterprise-style lab environment to identify attack paths, excessive privileges, credential exposure, and delegation-related security weaknesses.

The assessment focused on identifying how a low-privileged domain user could potentially chain multiple Active Directory weaknesses to reach higher-privileged systems or accounts.

The assessment included:

- Active Directory reconnaissance and enumeration
- LDAP and SMB enumeration
- BloodHound attack-path analysis
- Active Directory ACL assessment
- Resource-Based Constrained Delegation (RBCD) assessment
- Kerberoasting assessment
- AS-REP Roasting assessment
- Delegation analysis
- Privilege and group-membership review
- Remediation
- Post-remediation validation and retesting

## Key Findings

Three primary attack-path/security scenarios were assessed.

### AP-01 — Excessive ACL Permissions and RBCD

**Risk: High**

An excessive permission relationship involving USER1 and the CLIENT computer object was identified.

The assessment demonstrated that the excessive permissions could be combined with computer-account and RBCD techniques to obtain privileged remote execution against CLIENT.

The attack path was subsequently remediated by removing the excessive permissions, removing the temporary assessment computer account, and removing the temporary RBCD configuration used during testing.

Fresh BloodHound data confirmed that the original USER1 → CLIENT attack path was no longer present.

**Status: Remediated and validated**

---

### AP-02 — Kerberoastable Service Account

**Risk: Medium**

The MYSQL service account was identified as Kerberoastable due to its registered Service Principal Name (SPN).

A Kerberos service ticket was obtained and successfully subjected to offline password cracking, demonstrating credential exposure.

The assessment also identified excessive group membership associated with the account. Those excessive memberships were removed during remediation.

A subsequent BloodHound analysis showed no demonstrated MYSQL → Domain Admin attack path.

The recovered credential had not been rotated at the time of the final assessment and therefore remains a recommended remediation action.

**Status: Privilege exposure remediated; credential rotation recommended**

---

### AP-03 — AS-REP Roasting and Delegation Assessment

**Risk: Informational / Low**

The ASREP account was identified as AS-REP roastable.

An AS-REP hash was obtained for assessment and subjected to offline password-cracking attempts. The credential was not recovered using the available password list.

BloodHound analysis showed no demonstrated ASREP → Domain Admin attack path.

Delegation enumeration identified DC01 as using unconstrained delegation. As a domain controller, this configuration was treated as an architectural characteristic rather than automatically classified as an exploitable vulnerability.

The pre-existing ATTACKBOX → CLIENT RBCD relationship was also observed and was addressed within AP-01 rather than treated as a separate finding.

**Status: Assessed; no demonstrated privilege-compromise path**

## Overall Security Assessment

The assessment demonstrated that excessive Active Directory permissions can create meaningful attack paths even when the originating account is not a Domain Admin.

The most significant issue was AP-01, where excessive object permissions and delegation mechanisms could be chained to achieve privileged remote execution.

The AP-01 attack path was successfully remediated and independently validated through fresh Active Directory enumeration and BloodHound analysis.

AP-02 demonstrated that service-account credential exposure remains a security concern even when the account does not provide a direct path to Domain Admin.

## Overall Remediation Status

| Finding | Severity | Status |
|---|---|---|
| AP-01 — Excessive ACL + RBCD | High | Remediated and validated |
| AP-02 — Kerberoastable Service Account | Medium | Partially remediated; credential rotation recommended |
| AP-03 — AS-REP / Delegation Assessment | Informational / Low | No demonstrated exploitable privilege path |

## Conclusion

The assessment successfully identified, demonstrated, remediated, and retested a significant Active Directory attack path.

The final assessment showed that the primary USER1-to-CLIENT attack path identified during the engagement was no longer present after remediation.

Additional hardening should focus on least-privilege delegation, service-account credential management, RBCD monitoring, MachineAccountQuota governance, and continuous review of Active Directory object permissions.
