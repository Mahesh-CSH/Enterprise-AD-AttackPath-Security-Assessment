# Evidence Index

This index maps assessment evidence to the corresponding attack path,
validation activity, remediation, and retest.

> **Note:** Raw credentials, cracked passwords, hashes, password lists,
> and sensitive backup files are retained locally only and must not be
> committed to a public GitHub repository.

---

# AP-01 — RBCD / ACL Attack Path

## Initial Enumeration

| Evidence | Purpose |
|---|---|
| `AP-01-client-spn.txt` | CLIENT computer/SPN enumeration |
| `AP-01-maq.txt` | Machine Account Quota validation |
| `AP-01-user1-attackbox-after.txt` | USER1 → ATTACKBOX permission validation |

## ACL Assessment

| Evidence | Purpose |
|---|---|
| `AP-01-client-dacl.txt` | CLIENT DACL assessment |
| `AP-01-client-genericall.txt` | USER1 → CLIENT excessive permission evidence |
| `AP-01-dacl-before-remediation.txt` | Pre-remediation ACL state |
| `AP-01-attackbox-dacl-current.txt` | ATTACKBOX DACL state |
| `AP-01-attackbox-dacl-after.txt` | ATTACKBOX ACL verification |
| `AP-01-attackbox-remove-uac-restrictions.txt` | ATTACKBOX permission-removal evidence |

## RBCD Validation

| Evidence | Purpose |
|---|---|
| `AP-01-rbcd-before.txt` | Initial RBCD state |
| `AP-01-rbcd-write.txt` | RBCD modification evidence |
| `AP01-rbcd.write.txt` | RBCD write output |
| `AP-01-client-rbcd-before.txt` | CLIENT RBCD baseline |
| `AP-01-client-rbcd-write.txt` | CLIENT RBCD modification |
| `AP-01-client-rbcd-after.txt` | CLIENT RBCD after modification |
| `AP-01-rbcd-after.txt` | RBCD validation |
| `AP01-rbcd.bef.txt` | RBCD before-state evidence |
| `AP01-rbcd.aft.txt` | RBCD after-state evidence |

## Privileged Access Validation

| Evidence | Purpose |
|---|---|
| `AP-01-s4u.txt` | S4U ticket generation |
| `AP-01-admin-wmi.txt` | Remote administrative execution validation |
| `AP-01-client-exec.txt` | CLIENT execution evidence |

## Cleanup

| Evidence | Purpose |
|---|---|
| `AP-01-rbcd-remove.txt` | RBCD removal |
| `AP-01-dacl-remove.txt` | ACL removal |
| `AP-01-dacl-removal.txt` | ACL remediation |
| `AP-01-ap01-delete.txt` | Temporary computer-account cleanup |

## Retest

| Evidence | Purpose |
|---|---|
| `AP-01-final-computer-retest.txt` | Temporary computer account no longer present |
| `AP-01-final-rbcd-retest.txt` | Final RBCD validation |
| `AP-01-final-s4u-reset.txt` | S4U/credential-cache cleanup |
| `AP-01-dacl-after-remediation.txt` | Post-remediation ACL validation |
| `AP-01-dacl-current.txt` | Current ACL state |

---

# AP-02 — Kerberoasting

## Enumeration

| Evidence & Purpose |

| `AP-02-maq.txt` | Machine Account Quota assessment |
| `AP-02-kerberoast.txt` | Kerberoasting/SPN enumeration and TGS evidence |
| `AP-02-mysql-groups.txt` | Group enumeration |
| `AP-02-mysql-grps.txt` | Additional group enumeration |

## Account Validation

| Evidence & Purpose |

| `AP-02-mysql-membership.txt` | Initial mysql membership |
| `AP-02-mysql-membership-after.txt` | Membership verification |
| `AP-02-mysql-membership-final.txt` | Final membership state |
| `AP-02-mysql-group-membership-final.txt` | Final group-membership assessment |
| `AP-02-mysql-dc-auth.txt` | DC authentication validation |
| `AP-02-mysql-auth-after.txt` | Authentication validation |

## User ACL Assessment

| Evidence & Purpose |

| `AP-02-user2-attackbox-acl.txt` | USER2 → ATTACKBOX ACL assessment |
| `AP-02-user2-client-acl.txt` | USER2 → CLIENT ACL assessment |
| `AP-02-user2-dc01-acl.txt` | USER2 → DC01 ACL assessment |

## Credential Evidence — LOCAL ONLY

| Evidence & Purpose |

| `AP-02-mysql-tgs.hash` | Extracted Kerberos TGS hash |
| `AP-02-CRACKED-result.txt` | Offline password-analysis result |

**Do not publish these files to GitHub.**

## Retest

Final AP-02 retest evidence should be placed in:

```text
07-retest/AP-02/
