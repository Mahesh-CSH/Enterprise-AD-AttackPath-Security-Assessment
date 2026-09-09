# Active Directory Change Detection

## AP-01 — ACL and RBCD Changes

The assessment demonstrated modification of Active Directory computer-object
permissions and Resource-Based Constrained Delegation configuration.

## Detection Opportunities

Monitor:

- Computer-account creation
- Computer-account deletion
- Security descriptor changes
- Changes to computer-object permissions
- Changes to RBCD configuration
- Changes to privileged group membership

## High-Value Changes

Particular attention should be given to unexpected changes involving:

- Resource-Based Constrained Delegation
- Computer-object ACLs
- Privileged accounts
- Domain Controllers
- Administrative groups

## Recommendation

Forward relevant Active Directory and Windows security telemetry to a
centralized SIEM and alert on unauthorized changes to sensitive computer
objects.
