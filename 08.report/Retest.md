# Retest

## Objective

The objective of the retest was to determine whether the identified security weaknesses and attack paths remained exploitable after remediation.

Fresh Active Directory enumeration and BloodHound data were used where applicable.

---

## AP-01 Retest

### Validation Performed

- Reviewed CLIENT permissions.
- Reviewed ATTACKBOX permissions.
- Verified RBCD configuration.
- Verified removal of the temporary AP01$ account.
- Collected fresh BloodHound data.
- Re-tested the USER1 → CLIENT attack path.

### Result

The original USER1 → CLIENT attack path was no longer identified.

**Result: PASS**

---

## AP-02 Retest

### Validation Performed

- Reviewed final MYSQL group membership.
- Validated MYSQL authentication.
- Reviewed MYSQL privileges.
- Checked MYSQL → Domain Admin path using BloodHound.

### Result

Excessive group membership was removed.

No MYSQL → Domain Admin path was identified.

The previously exposed service-account credential had not been rotated.

**Result: PARTIAL PASS**

---

## AP-03 Retest

### Validation Performed

- Reviewed ASREP attack-path relationships.
- Checked ASREP → Domain Admin.
- Reviewed delegation configuration.
- Confirmed the AS-REP credential was not recovered during the cracking attempt.

### Result

No demonstrated ASREP → Domain Admin path was identified.

**Result: PASS**

---

## Final Validation Summary

| Finding | Retest Result | Status |
|---|---|---|
| AP-01 — ACL + RBCD | Original attack path removed | PASS |
| AP-02 — Kerberoasting | Privileges reduced; credential rotation pending | PARTIAL PASS |
| AP-03 — AS-REP / Delegation | No demonstrated privilege path | PASS |

## Overall Retest Conclusion

The primary AP-01 attack path was successfully removed and validated.

AP-02 privilege exposure was reduced, but credential rotation remains an outstanding security recommendation.

No demonstrated privilege-compromise path remained for AP-03.
