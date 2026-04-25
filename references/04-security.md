# AWS Well-Architected Framework — Security Pillar

## Definition

Security in the cloud, as defined by the AWS Well-Architected Framework, "describes how to take advantage of cloud technologies to protect data, systems, and assets in a way that can improve your security posture." The Security pillar provides in-depth, best-practice guidance for architecting secure workloads on AWS so that you can protect data and systems, control access, and respond automatically to security events. AWS frames security in the cloud as composed of seven areas — security foundations, identity and access management, detection, infrastructure protection, data protection, incident response, and application security — and expects workloads to apply these together under the AWS shared responsibility model. The November 2024 framework refresh expanded this guidance, most notably elevating Application Security (SEC11) into a fully-developed area and modernizing detection, network, and data-protection best practices around Zero Trust, automated remediation, and managed key services.

## Design Principles

1. **Implement a strong identity foundation.** Implement the principle of least privilege and enforce separation of duties with appropriate authorization for each interaction with your AWS resources. Centralize identity management, and aim to eliminate reliance on long-term static credentials.
2. **Maintain traceability.** Monitor, alert, and audit actions and changes to your environment in real time. Integrate log and metric collection with systems to automatically investigate and take action.
3. **Apply security at all layers.** Apply a defense-in-depth approach with multiple security controls. Apply to all layers (for example, edge of network, VPC, load balancing, every instance and compute service, operating system, application, and code).
4. **Automate security best practices.** Automated software-based security mechanisms improve your ability to securely scale more rapidly and cost-effectively. Create secure architectures, including the implementation of controls that are defined and managed as code in version-controlled templates.
5. **Protect data in transit and at rest.** Classify your data into sensitivity levels and use mechanisms such as encryption, tokenization, and access control where appropriate.
6. **Keep people away from data.** Use mechanisms and tools to reduce or eliminate the need for direct access or manual processing of data. This reduces the risk of mishandling or modification and human error when handling sensitive data.
7. **Prepare for security events.** Prepare for an incident by having incident management and investigation policy and processes that align to your organizational requirements. Run incident response simulations and use tools with automation to increase your speed for detection, investigation, and recovery.

## Best Practice Areas

### 1. Security Foundations

Covers the governance and operating model required before any specific control is implemented: account structure, regulatory and threat-model awareness, secure root user, and a process to keep up with new AWS security capabilities.

**SEC01 — How do you securely operate your workload?**
- Separate workloads using a multi-account strategy backed by AWS Organizations and AWS Control Tower; treat accounts as the strongest hard isolation boundary.
- Secure the AWS account root user: hardware MFA, no access keys, accurate alternate contacts, and detective alarms on root usage.
- Identify and validate control objectives derived from compliance requirements (PCI-DSS, HIPAA, SOC2, ISO 27001) and your threat model.
- Stay current with security threats and AWS security recommendations; subscribe to AWS Security Bulletins, CVE feeds, and the AWS What's New feed.
- Automate testing and validation of security controls in pipelines (Config rules, Security Hub standards, IaC scanning).
- Identify and prioritize risks using a documented threat model that is revisited as the workload evolves.

### 2. Identity and Access Management

Covers human and machine identity lifecycle plus the permissions that gate every API call. Two questions: identity (SEC02) and permissions (SEC03).

**SEC02 — How do you manage identities for people and machines?**
- Use strong sign-in mechanisms: enforce MFA, strong password policies, and phishing-resistant factors for all human identities.
- Use temporary credentials (IAM roles, STS, Identity Center sessions) instead of long-lived IAM user access keys.
- Store and use secrets securely with AWS Secrets Manager or Parameter Store; never embed credentials in code or AMIs.
- Rely on a centralized identity provider (AWS IAM Identity Center federated with Okta, Entra ID, or Google) as the single source of truth.
- Audit and rotate credentials periodically; detect unused credentials and disable them.
- Employ user groups and attributes (ABAC) so permissions follow role and project tags rather than per-user grants.

**SEC03 — How do you manage permissions for people and machines?**
- Define access requirements per role, environment, and data sensitivity before writing policies.
- Grant least-privilege access — start from zero and add permissions only as required, validated by IAM Access Analyzer policy generation.
- Establish an emergency ("break-glass") access process that is auditable and rarely used.
- Reduce permissions continuously using IAM Access Analyzer unused-access findings and last-accessed data.
- Define organizational guardrails with Service Control Policies (SCPs), Resource Control Policies (RCPs), and permission boundaries.
- Manage access based on lifecycle (joiner/mover/leaver) tied to your IdP.
- Analyze public and cross-account access with IAM Access Analyzer; share resources securely within your org and with third parties using resource policies, RAM, and confused-deputy protections.

### 3. Detection

Covers logging, monitoring, alerting, and the workflows that turn signals into actionable findings.

**SEC04 — How do you detect and investigate security events?**
- Configure service and application logging: CloudTrail (management + data events), VPC Flow Logs, DNS query logs, ELB/CloudFront access logs, application logs.
- Capture logs, findings, and metrics in standardized, tamper-resistant locations (centralized log archive account, S3 with Object Lock, log-group retention).
- Correlate and enrich security alerts: aggregate GuardDuty, Security Hub, Inspector, Macie, and Config findings into a single SIEM or Security Lake.
- Initiate remediation for non-compliant resources via EventBridge → Lambda/SSM Automation/Step Functions, scoped by severity.
- Run regular tabletop reviews of detective coverage against the MITRE ATT&CK Cloud matrix.

### 4. Infrastructure Protection

Covers defense-in-depth at the network and compute layers using a Zero Trust mindset.

**SEC05 — How do you protect your networks?**
- Create network layers — public, private, and restricted subnets across multiple AZs; segregate environments at the VPC or account boundary.
- Control traffic flow within layers using security groups, NACLs, and route tables; deny-by-default everywhere.
- Implement inspection-based protection with AWS Network Firewall, Gateway Load Balancer + IDS/IPS appliances, and AWS WAF for HTTP(S).
- Automate network protection with AWS Firewall Manager, Shield Advanced, and IaC-managed security group baselines.
- Prefer private connectivity (PrivateLink, VPC endpoints, Transit Gateway) over public internet paths.

**SEC06 — How do you protect your compute resources?**
- Perform vulnerability management continuously with Amazon Inspector for EC2, Lambda, and container images.
- Provision compute from hardened images (CIS-benchmarked AMIs, distroless containers) built in a golden-pipeline.
- Reduce manual management and interactive access — use SSM Session Manager, Fleet Manager, and Run Command instead of SSH/RDP.
- Validate software integrity using code signing (Signer), SBOMs, and image-digest pinning.
- Automate compute protection with patch baselines, auto-scaling immutable replacements, and runtime protection (GuardDuty Runtime Monitoring, EKS/ECS).

### 5. Data Protection

Covers classification and the encryption/access controls applied to data throughout its lifecycle.

**SEC07 — How do you classify your data?**
- Understand and document a data classification scheme aligned with regulatory and business requirements.
- Apply data-protection controls based on sensitivity (encryption strength, key custody, retention, access scope).
- Automate identification and classification using Amazon Macie for S3 and tagging conventions.
- Define scalable data-lifecycle management: tiering, retention, legal hold, and deletion governed by S3 Lifecycle and Backup policies.

**SEC08 — How do you protect your data at rest?**
- Implement secure key management with AWS KMS; prefer customer-managed keys with key policies, grants, and CloudHSM where required.
- Enforce encryption at rest across all storage (S3, EBS, RDS, DynamoDB, EFS, FSx, Aurora, OpenSearch); make it the default.
- Automate data-at-rest protection via Config rules, S3 default encryption, and account-level EBS encryption.
- Enforce access control with resource policies, bucket policies, VPC endpoint policies, and KMS key policies; use S3 Block Public Access and Object Lock.

**SEC09 — How do you protect your data in transit?**
- Implement secure key and certificate management with ACM (public) and ACM Private CA (internal).
- Enforce encryption in transit — TLS 1.2+ everywhere, HSTS, perfect-forward-secrecy ciphers, sslmode=require for databases.
- Authenticate network communications with SigV4, mTLS, and IAM-authenticated endpoints; remove plaintext protocols.
- Use VPC endpoints / PrivateLink to keep service traffic on the AWS backbone.

### 6. Incident Response

Covers preparation, operations during an event, and post-incident learning.

**SEC10 — How do you anticipate, respond to, and recover from incidents?**
- Identify key personnel and external resources (AWS Support, IR retainer) before an incident.
- Develop and maintain incident-management plans and runbooks per finding type (credential exposure, S3 public exposure, ransomware on EC2).
- Pre-deploy incident-response tools and access (forensics account, dedicated IR IAM role, isolated VPC, EBS snapshot copy permissions).
- Prepare forensic capabilities — automated EC2 isolation, EBS snapshot, memory capture, and chain-of-custody storage.
- Run game days and simulations regularly; capture lessons learned and update playbooks.
- Automate containment for common patterns (quarantine SG swap, IAM credential disable, S3 bucket lockdown).
- Establish a framework for learning from incidents and feeding findings back into preventative controls.

### 7. Application Security

The November 2024 refresh promoted application security to a first-class area. Covers secure SDLC, supply-chain integrity, and embedding security into engineering teams.

**SEC11 — How do you incorporate and validate the security properties of applications throughout the design, development, and deployment lifecycle?**
- Train for application security — developer education on OWASP Top 10, AWS-specific anti-patterns, and threat modeling.
- Automate testing throughout the development and release lifecycle: SAST, DAST, SCA, IaC scanning, and secret scanning gated in CI.
- Perform regular penetration testing by qualified internal or external testers within the AWS customer-support policy.
- Conduct code reviews with security checklists and peer approval before merge.
- Centralize services for packages and dependencies using CodeArtifact, ECR with scanning, and signed artifacts; pin and review transitive deps.
- Deploy software programmatically with CodePipeline / GitHub Actions OIDC; no manual console deploys to production.
- Regularly assess the security properties of the pipelines themselves (least-privilege deploy roles, branch protection, signed commits).
- Build a program that embeds security ownership in workload teams (security champions, paved roads, golden templates).

## Key AWS Services

- **Identity & access:** AWS IAM, IAM Identity Center, AWS Organizations (SCP/RCP), IAM Access Analyzer, AWS STS, AWS Directory Service, Amazon Cognito, AWS Verified Access, AWS Verified Permissions.
- **Detection & posture:** Amazon GuardDuty (incl. Runtime Monitoring, S3, EKS, RDS, Lambda protections), AWS Security Hub (CSPM with AWS FSBP, CIS, PCI), Amazon Detective, Amazon Inspector, Amazon Macie, AWS Security Lake, Amazon CloudWatch, Amazon EventBridge.
- **Data protection:** AWS KMS, AWS CloudHSM, AWS Secrets Manager, AWS Systems Manager Parameter Store, AWS Certificate Manager, ACM Private CA, AWS Payment Cryptography, S3 Object Lock, AWS Backup with Vault Lock.
- **Network protection:** AWS Shield (Standard & Advanced), AWS WAF, AWS Network Firewall, AWS Firewall Manager, Amazon VPC (security groups, NACLs, Flow Logs), AWS PrivateLink, AWS Transit Gateway, Route 53 Resolver DNS Firewall.
- **Audit, governance, compliance:** AWS CloudTrail (incl. Lake), AWS Config (+ conformance packs), AWS Audit Manager, AWS Artifact, AWS Control Tower, AWS Trusted Advisor, AWS Well-Architected Tool.
- **Incident response & forensics:** AWS Systems Manager (Incident Manager, Automation, Session Manager), AWS Step Functions, AWS Lambda, dedicated forensics account pattern, EBS snapshot APIs.
- **Application security:** Amazon CodeGuru Security, Amazon Inspector (code & images), AWS Signer, Amazon ECR scanning, AWS CodeArtifact, AWS CodePipeline + CodeBuild with OIDC.

## Common Anti-patterns

- Long-lived IAM user access keys committed to repos or shared in chat instead of federated SSO with temporary credentials via IAM Identity Center.
- Wide-open security groups (`0.0.0.0/0` on 22/3389/database ports) and `*` in IAM/resource policies — least privilege exists only on paper.
- Single AWS account holding prod + dev + sandbox, with no SCPs/RCPs and no Control Tower guardrails.
- Encryption assumed because "AWS encrypts by default" — but with AWS-managed keys only, no key-policy controls, no rotation, no auditing of `kms:Decrypt`.
- CloudTrail enabled in only one region, no organization trail, no log-file integrity validation, logs writable by the same account that produces them.
- Detection findings (GuardDuty, Security Hub, Inspector) generated but never routed, triaged, or measured for MTTR — alert fatigue with no remediation automation.
- Console-based "click-ops" deploys to production with no IaC, no code review, and no pipeline identity — every change is an undocumented privilege escalation.
- No incident-response plan, no runbooks, no game days; the first time the team isolates a compromised instance is during the real incident.
- Public S3 buckets, public RDS snapshots, or public AMIs because Block Public Access and Macie were never turned on.
- Secrets in environment variables, AMIs, container images, or Parameter Store SecureString without rotation, instead of Secrets Manager with rotation Lambdas.

## Review Checklist

1. Is the workload deployed across a multi-account structure managed by AWS Organizations with SCPs and RCPs enforcing guardrails?
2. Is the root user of every account secured with hardware MFA, no access keys, and detective alarms on usage?
3. Is all human access federated through IAM Identity Center (or equivalent IdP) using temporary credentials and MFA?
4. Are all machine identities using IAM roles (EC2 instance profiles, Lambda execution roles, IRSA/Pod Identity, OIDC for CI) with no long-lived keys?
5. Are IAM policies least-privilege, generated/validated by Access Analyzer, and reviewed against unused-access findings?
6. Is CloudTrail enabled organization-wide (management + data events) with logs centralized in an immutable, dedicated log-archive account?
7. Are GuardDuty, Security Hub, Inspector, and Macie enabled across all accounts/regions with findings centralized and routed to ticketing/SIEM?
8. Are remediation workflows automated for high-severity findings (EventBridge → Lambda/SSM Automation) with measured MTTR?
9. Is data encrypted at rest using customer-managed KMS keys (or CloudHSM) with documented key policies, rotation, and audited usage?
10. Is data in transit protected with TLS 1.2+ everywhere, ACM-managed certs, mTLS where appropriate, and VPC endpoints to keep traffic off the public internet?
11. Are networks segmented (public/private/restricted subnets, per-tier security groups, deny-by-default) with WAF on internet-facing apps and Network Firewall/Shield Advanced where warranted?
12. Are compute resources patched and hardened via golden images, immutable deployments, SSM Session Manager (no SSH/RDP), and runtime monitoring?
13. Are secrets stored in Secrets Manager (or Parameter Store SecureString) with rotation enabled and never embedded in code, AMIs, or images?
14. Is the CI/CD pipeline itself secured — OIDC-based deploy roles, branch protection, signed artifacts, SAST/DAST/SCA/IaC scanning gated on merges?
15. Does the team have documented incident-response runbooks, a forensics account, automated containment for common scenarios, and regularly run game days?

## References

- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/security.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/definition.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/security-foundations.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/identity-and-access-management.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/detection.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/infrastructure-protection.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/data-protection.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/incident-response.html
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/application-security.html
