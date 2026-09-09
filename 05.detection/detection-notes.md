# Detection & Purple-Team Notes

## Assessment Objective

Evaluate defensive visibility for the attack techniques validated during
the Active Directory security assessment.

## Attack-to-Detection Mapping

| Attack Activity | Detection Area |
|---|---|
| Excessive AD ACL abuse | Directory Service / Security logs |
| RBCD modification | AD computer-object changes |
| S4U/Kerberos activity | Kerberos telemetry |
| Privileged remote execution | Windows Security / process telemetry |
| Kerberoasting | Kerberos TGS activity |
| Computer-account creation | Active Directory monitoring |

## Defensive Recommendations

1. Centralize Windows security telemetry.
2. Monitor sensitive AD object changes.
3. Monitor abnormal Kerberos service-ticket activity.
4. Alert on unexpected computer-account creation.
5. Monitor privileged remote logons.
6. Review ACL changes on sensitive computer objects.
7. Monitor privileged group membership changes.

## Purple-Team Validation

The offensive findings were used to identify defensive monitoring
requirements and remediation priorities.

## Limitations

The assessment was performed in an isolated lab environment. Detection
coverage should be validated against the organization's actual Windows,
Active Directory and SIEM configuration.
