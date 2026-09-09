# AP-01 Before / After Summary

## Before Remediation

BloodHound identified an attack path involving USER1 and CLIENT.

Observed excessive control included:

USER1 → GenericAll → CLIENT

Additional delegated permissions on ATTACKBOX contributed to the assessed attack path.

The assessment demonstrated that the excessive permissions could be combined with computer-account/RBCD techniques to obtain privileged remote execution against CLIENT.

## Remediation

- Removed excessive USER1 control over CLIENT.
- Removed excessive USER1 permissions from ATTACKBOX.
- Removed temporary AP01$ computer account.
- Removed the temporary AP01$ RBCD relationship from CLIENT.
- Re-collected BloodHound data.

## After Remediation

Fresh BloodHound analysis showed:

USER1 → CLIENT

**No attack path identified.**

The previously demonstrated USER1-to-CLIENT attack path was successfully eliminated.

## Validation Result

**PASS — Attack path removed**

Note: The pre-existing ATTACKBOX$ RBCD relationship was retained because it was part of the lab baseline and was not the remediation target.
