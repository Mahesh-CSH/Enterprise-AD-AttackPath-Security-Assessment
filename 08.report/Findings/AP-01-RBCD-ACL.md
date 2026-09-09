# AP-01 — Excessive Active Directory ACL Permissions and RBCD Attack Path

## Finding ID

AP-01

## Severity

**High**

## Status

**Remediated and Validated**

## Affected Assets

- `CLIENT.AD.lab`
- `ATTACKBOX.AD.lab`
- `USER1@AD.LAB`

---

## Description

An excessive Active Directory permission relationship was identified between the low-privileged `USER1` account and the `CLIENT` computer object.

BloodHound initially identified:

```text
USER1@AD.LAB
        |
        | GenericAll
        v
CLIENT.AD.LAB
