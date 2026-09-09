# Methodology

## Assessment Approach

The assessment followed a structured penetration-testing and Active Directory security-assessment workflow:

**Reconnaissance → Enumeration → Attack-Path Analysis → Controlled Exploitation → Remediation → Retest**

The objective was not simply to identify individual vulnerabilities, but to determine whether multiple weaknesses could be chained into a meaningful attack path.

---

## 1. Reconnaissance

Initial reconnaissance was performed against the authorized laboratory network to identify active systems and exposed services.

Activities included:

- Host discovery
- Port scanning
- Service enumeration
- SMB enumeration
- Identification of the domain controller
- Identification of Active Directory-related services

Tools used included:

- Nmap
- NetExec

Relevant reconnaissance evidence was stored under:

```text
01-recon/
