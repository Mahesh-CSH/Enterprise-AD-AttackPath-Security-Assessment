# Remediation

## Overview

Remediation focused on removing excessive privileges, reducing attack-path exposure, and validating the resulting Active Directory security posture.

---

## AP-01 — ACL and RBCD Attack Path

### Actions Performed

- Removed excessive USER1 control over CLIENT.
- Removed excessive USER1 permissions from ATTACKBOX.
- Removed the temporary AP01$ computer account.
- Removed the temporary AP01$ RBCD relationship from CLIENT.
- Re-validated CLIENT permissions.
- Re-validated ATTACKBOX permissions.
- Performed fresh BloodHound collection.

### Result

The original USER1 → CLIENT attack path was no longer identified.

**Status: Remediated and validated**

---

## AP-02 — Kerberoastable Service Account

### Actions Performed

- Reviewed MYSQL group membership.
- Removed excessive group memberships.
- Validated final membership through LDAP.
- Tested MYSQL authentication after the changes.
- Checked the MYSQL attack path using BloodHound.

### Result

No MYSQL → Domain Admin path was identified after remediation.

### Outstanding Action

The previously exposed MYSQL credential had not been rotated at the time of the final assessment.

Recommended actions:

- Rotate the exposed credential.
- Use a strong, unique service-account password.
- Consider migration to a gMSA.
- Review `Password Never Expires`.
- Review SPN necessity.
- Continue least-privilege review.

**Status: Partially remediated**

---

## AP-03 — AS-REP and Delegation

No specific remediation was required based on the assessment results because no successful privilege-compromise path was demonstrated.

Recommended controls include:

- Review AS-REP configurations.
- Avoid unnecessary `Do not require Kerberos preauthentication`.
- Review delegation configurations.
- Monitor suspicious Kerberos activity.

**Status: Assessment completed**

---

## Long-Term Active Directory Hardening

The following controls are recommended:

1. Apply least privilege to AD objects.
2. Regularly audit ACLs and delegated permissions.
3. Review MachineAccountQuota.
4. Monitor RBCD changes.
5. Review service accounts and SPNs.
6. Prefer gMSAs where appropriate.
7. Rotate exposed credentials immediately.
8. Review privileged group membership.
9. Monitor Kerberos authentication activity.
10. Perform periodic BloodHound-based attack-path reviews.
