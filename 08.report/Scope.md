# Scope

## Assessment Type

Internal Active Directory Security Assessment

## Objective

The objective of the assessment was to evaluate the security posture of an enterprise-style Active Directory environment by identifying:

- Excessive Active Directory permissions
- Attack paths between domain users and computers
- Resource-Based Constrained Delegation (RBCD) exposure
- Kerberoastable service accounts
- AS-REP roastable accounts
- Delegation configurations
- Excessive group memberships
- Potential paths to privileged accounts and systems

The assessment also included remediation and post-remediation validation.

## Authorized Environment

The assessment was performed exclusively against the controlled lab environment.

| Asset | Role | IP Address |

| DC01 | Windows Server / Domain Controller | `192.168.88.10` |
| CLIENT | Windows 10 Client | `192.168.88.136` |
| ATTACKBOX | Domain-joined computer | Lab environment |

### Active Directory Domain

```text
AD.lab
