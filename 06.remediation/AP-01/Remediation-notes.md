# AP-01 Remediation Notes

## Finding
Excessive Active Directory permissions and Resource-Based Constrained Delegation (RBCD) created an attack path from USER1 to CLIENT.

## Root Cause
- USER1 had excessive control over the CLIENT computer object.
- Excessive rights were present on the ATTACKBOX computer object.
- MachineAccountQuota permitted standard users to create computer accounts.
- RBCD configuration allowed delegated computer-account relationships.

## Remediation Performed

### 1. Removed excessive USER1 permissions
The excessive direct control that allowed USER1 to control the CLIENT computer object was removed.

### 2. Removed excessive ATTACKBOX permissions
The excessive USER1 permissions on ATTACKBOX were reviewed and removed, including the identified User-Account-Restrictions and excessive extended-rights ACE.

### 3. Removed temporary computer account
The temporary AP01$ computer account created during the assessment was removed after testing.

### 4. Removed temporary RBCD configuration
The RBCD entry associated with AP01$ was removed from CLIENT.

The pre-existing ATTACKBOX$ RBCD relationship was retained as part of the lab's baseline configuration.

### 5. Re-collected Active Directory data
Fresh BloodHound data was collected after remediation to validate the changes.

## Recommended Hardening

- Apply least privilege to computer objects.
- Review delegated permissions on computer accounts.
- Restrict who can create computer accounts.
- Review MachineAccountQuota and reduce it where appropriate.
- Regularly audit RBCD configuration.
- Monitor changes to Active Directory security descriptors.
- Remove unnecessary delegated permissions.

## Status

Remediation implemented and validated.

The previously demonstrated USER1 → CLIENT attack path was no longer present in the final BloodHound assessment.
