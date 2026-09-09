# AP-02 Remediation Notes

## Finding
The MYSQL service account was Kerberoastable because it had a registered Service Principal Name (SPN).

## Root Cause

The MYSQL account had:

- A registered SPN:
  `DC01/mysql.AD.lab:60500`
- A password that was successfully recovered through offline password cracking.
- Password Never Expires enabled.

The account did not have a demonstrated path to Domain Admin during the assessment.

## Remediation Performed

### 1. Reviewed MYSQL group membership

Excessive group memberships identified during the assessment were removed.

Final LDAP verification showed that MYSQL retained normal user-level membership rather than the previously identified excessive memberships.

### 2. Validated Domain Admin attack path

BloodHound was used to test whether MYSQL could reach Domain Admin.

Result:

**No path identified.**

### 3. Validated account authentication

Post-remediation authentication was tested to confirm the account remained functional after the group-membership changes.

## Recommended Credential Remediation

The service-account credential should be rotated after the assessment because the password was successfully recovered during offline cracking.

Recommended long-term controls:

- Rotate the exposed credential.
- Use a strong, unique service-account password.
- Prefer a Group Managed Service Account (gMSA) where supported.
- Disable unnecessary password-never-expires settings.
- Apply least privilege.
- Review whether the SPN is required.
- Monitor unusual Kerberos TGS requests.

## Status

### Completed
- Excessive group membership removed.
- MYSQL-to-Domain-Admin path tested.
- No Domain Admin path identified.

### Pending / Recommended
- Rotate the exposed MYSQL credential.
- Evaluate migration to a gMSA.
- Review SPN necessity and ownership.

The credential rotation is intentionally documented as a recommendation rather than claiming it was performed.
