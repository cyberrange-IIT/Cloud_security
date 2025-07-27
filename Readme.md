# Cloud Security Reference Guide

This repository is a structured collection of cloud security knowledge across AWS, Azure, and GCP. It focuses on high-impact areas like SSRF, IAM abuse, LLM/chatbot risks, and cloud-specific misconfigurations. Designed for red teamers, blue teamers, cloud engineers, and SOC analysts.

## Contents

| Level        | File                    | Description                                                      |
|--------------|-------------------------|------------------------------------------------------------------|
| Beginner     | Cloud-Basics.md         | Cloud models, shared responsibility, asset exposure              |
| Intermediate | Cloud-SSRF.md           | SSRF across AWS (IMDS), Azure (MSI), GCP (Metadata)              |
| Intermediate | Cloud-IAM.md            | Identity and access abuse, role misconfigurations                |
| Intermediate | Cloud-LLM.md            | Prompt injection, metadata token exfiltration via chatbot        |
| Intermediate | Cloud-Misconfig.md      | Common open services, insecure storage, and excessive access     |
| Advanced     | Cloud-Monitoring.md     | Logs, alerts, and native detections across all three platforms   |
| Expert       | Cloud-Advanced.md       | Cross-cloud pivoting, combined attack chains, detection rules    |

## Topics Covered

### SSRF (Server-Side Request Forgery)

- AWS: IMDSv1 vs IMDSv2 token theft via SSRF
- Azure: Exploiting Azure Instance Metadata Service (MSI)
- GCP: Metadata server access and token misuse
- Prevention and detection techniques

### IAM Abuse

- AWS: Role chaining, PassRole, overly permissive policies
- Azure: Role assignments via Azure RBAC and Graph API
- GCP: Misuse of Service Accounts, roles/editor escalation
- Least privilege enforcement and detection

### LLM Chatbot Security

- Prompt injection techniques
- Stealing cloud credentials via chatbot inputs
- Integration risks with Lambda, Azure Functions, Cloud Functions
- Hardening techniques and model filtering

### Common Misconfigurations

- Public buckets (S3, Blob, GCS)
- Exposed VMs with open ports
- Overly permissive IAM/service roles
- Insecure CI/CD workflows and secrets exposure
- Lack of logging and monitoring

### Detection and Monitoring

- AWS: CloudTrail, GuardDuty, AWS Config, CloudWatch
- Azure: Activity Logs, Defender for Cloud, Microsoft Sentinel
- GCP: Audit Logs, SCC, Event Threat Detection
- Recommended log sources and alerts for cloud threats

### Advanced Topics

- Cross-cloud attack chains
- Identity federation abuse
- Chained SSRF → token → privilege escalation paths
- Real-world breach mappings and threat modeling
- Custom detections using native and third-party tools

## References

- AWS Security Documentation: https://docs.aws.amazon.com/security/
- Azure Security Documentation: https://learn.microsoft.com/en-us/security/
- GCP Security Overview: https://cloud.google.com/security
- OWASP SSRF Guide: https://owasp.org/www-community/attacks/Server_Side_Request_Forgery
- OWASP LLM Top 10: https://owasp.org/www-project-llm-security/
- MITRE ATT&CK Cloud Matrix: https://attack.mitre.org/matrices/enterprise/cloud/

## Contributing

We welcome contributions in the form of new attack scenarios, detection use cases, hardening guidelines, or references.  
To contribute, open an issue or submit a pull request.

This repository is for educational and research purposes only. Ensure you have proper authorization before testing any techniques in real environments.
