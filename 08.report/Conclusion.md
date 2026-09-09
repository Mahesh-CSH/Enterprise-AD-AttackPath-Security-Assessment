# Conclusion

The Active Directory security assessment successfully identified and validated multiple security weaknesses within the controlled enterprise-style lab environment.

The assessment demonstrated the importance of evaluating Active Directory as an interconnected privilege system rather than reviewing individual vulnerabilities in isolation.

## Key Outcomes

### AP-01

The most significant finding involved excessive Active Directory permissions combined with RBCD-related attack-path conditions.

The attack path was successfully demonstrated, remediated, and retested.

**Final Status: Remediated and Validated**

### AP-02

The MYSQL service account was successfully Kerberoasted and its credential was recovered through offline password cracking.

Excessive group membership was removed and no MYSQL → Domain Admin path was identified.

Credential rotation remains recommended.

**Final Status: Partially Remediated**

### AP-03

AS-REP Roasting and delegation configurations were assessed.

The ASREP credential was not recovered through the available cracking attempt, and no ASREP → Domain Admin path was demonstrated.

**Final Status: Assessed**

## Overall Assessment

The project demonstrates the complete Active Directory security-assessment lifecycle:

```text
Reconnaissance
      ↓
Enumeration
      ↓
Attack-Path Analysis
      ↓
Controlled Exploitation
      ↓
Impact Validation
      ↓
Remediation
      ↓
Retesting
      ↓
Final Validation
