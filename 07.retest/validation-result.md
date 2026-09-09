# Final Validation Results

| Assessment | Original Issue | Remediation | Retest Result | Status |

| AP-01 | Excessive ACL + RBCD attack path | Removed excessive permissions and temporary RBCD configuration | USER1 → CLIENT path no longer identified | PASS |
| AP-02 | Kerberoastable service account + excessive privileges | Removed excessive group membership | No MYSQL → Domain Admin path | PARTIAL PASS |
| AP-03 | AS-REP/delegation assessment | No confirmed exploitable privilege path requiring remediation | No ASREP → Domain Admin path; AS-REP credential not cracked | PASS |

## Overall Conclusion

The primary AP-01 attack path was successfully remediated and validated.

AP-02 privilege exposure was reduced and no Domain Admin path was identified; however, credential rotation remains recommended because the service-account credential was recovered during testing.

AP-03 did not produce a demonstrated privilege-compromise path requiring remediation.
