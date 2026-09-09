# AP-02 Before / After Summary

## Before Remediation

The MYSQL service account had:

- Registered SPN:
  `DC01/mysql.AD.lab:60500`
- Kerberoastable configuration.
- Password Never Expires enabled.
- Excessive group memberships identified during assessment.

The TGS was obtained and the associated credential was successfully recovered through offline password cracking.

## Remediation

- Reviewed and removed excessive MYSQL group memberships.
- Tested MYSQL's resulting privileges.
- Performed BloodHound attack-path validation.
- Confirmed no MYSQL → Domain Admin path.

## After Remediation

Final assessment showed:

- MYSQL remained a normal domain account.
- No demonstrated MYSQL → Domain Admin path.
- Excessive group membership was removed.

However, the previously exposed password had **not yet been rotated**.

## Validation Result

**PARTIAL PASS**

Privilege exposure was reduced and no Domain Admin attack path was identified.

Credential remediation remains recommended because the service-account password was successfully recovered during the assessment.
