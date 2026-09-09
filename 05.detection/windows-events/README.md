# Windows Security Event Detection

## Objective

Identify Windows security telemetry that can help detect the attack activity
validated during the assessment.

## AP-01 — Privileged Remote Execution

Relevant telemetry includes:

- Successful logon events
- Explicit credential usage
- Remote service/task execution
- Privileged logon activity

## Detection Considerations

Monitor unusual administrative logons, unexpected remote execution,
and privileged access originating from non-administrative user accounts.

## Validation

The assessment demonstrated privileged remote execution against CLIENT
during the controlled lab attack.

Detection should correlate:

- Source host
- Destination host
- Account
- Logon type
- Process/service activity
- Privilege level

## Recommendation

Centralize Windows Security logs and create alerts for unusual privileged
remote activity.
