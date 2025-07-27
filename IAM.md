# IAM Misconfigurations and Abuse in Cloud Platforms

## Overview
Misconfigured IAM (Identity and Access Management) permissions are a top cause of lateral movement and privilege escalation across cloud environments.

## IAM Types and Escalation Paths
| Cloud | IAM Entities | Escalation Risks |
|-------|--------------|------------------|
| AWS   | Users, Roles | PassRole, wildcard *, AssumeRole abuse |
| Azure | Role Assignments | Contributor -> Owner privilege chaining |
| GCP   | Service Accounts | iam.serviceAccounts.actAs, over-permissive bindings |

## MITRE ATT&CK Techniques
- T1078: Valid Accounts
- T1087: Account Discovery
- T1098: Account Manipulation

## Red Team Techniques and Tools
- Pacu (AWS)
- MicroBurst (Azure)
- gcloud CLI
- ScoutSuite, CloudSploit

### Sample Payloads

**AWS: IAM Privilege Escalation**
```json
{
  "Effect": "Allow",
  "Action": "iam:PassRole",
  "Resource": "*"
}
```

**GCP: Impersonate Service Account**
```bash
gcloud iam service-accounts impersonate target@project.iam.gserviceaccount.com
```

## Misuse of Specific Role ARN
```bash
aws sts assume-role --role-arn arn:aws:iam::123456789012:role/AdminRole --role-session-name attackerSession
```
 - Risk: Complete takeover of AWS environment.
## Overlapping Trust Policies via ARNs
 - Attackers can create malicious roles and manipulate trust policies:
 ```json
 {
  "Effect": "Allow",
  "Principal": {
    "AWS": "arn:aws:iam::123456789012:role/MaliciousRole"
  },
  "Action": "sts:AssumeRole"
}

 ```
 - Risk: Unauthorized access across accounts.


## Blue Team Detection and Defense

### Detection
- Audit logs for new IAM role assumptions
- Monitor creation of new policies or roles
- Analyze CloudTrail logs for AssumeRole and policy modification events.
- Monitor new roles added with overly broad trust policies.
- Use IAM Access Analyzer for unintended access detection.

### Defense
- Implement least privilege IAM model
- Use IAM Access Analyzer (AWS), Azure Defender, and GCP Policy Intelligence
- Deny wildcard resource usage
- Restrict trust policies to known, scoped ARNs.
- Use Service Control Policies (SCPs) to prevent privilege escalation.

## References
- AWS IAM Best Practices: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
- GCP IAM Overview: https://cloud.google.com/iam/docs/overview
- MITRE ATT&CK: https://attack.mitre.org/
