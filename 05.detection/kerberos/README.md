# Kerberos Detection

## AP-02 — Kerberoasting

The assessment identified the `mysql` service account through its SPN and
successfully requested a service ticket for controlled offline password
analysis.

## Detection Opportunities

Monitor unusual volumes or patterns of Kerberos service-ticket requests,
particularly requests involving service accounts.

Useful telemetry includes:

- Kerberos service-ticket activity
- Source host
- Requesting account
- Target service account
- Service Principal Name (SPN)

## Detection Recommendation

Baseline normal Kerberos activity and investigate anomalous TGS request
patterns involving privileged or sensitive service accounts.

## Mitigation

- Strong service-account passwords
- gMSA where appropriate
- Least privilege
- Regular SPN review
- Credential rotation after suspected compromise
