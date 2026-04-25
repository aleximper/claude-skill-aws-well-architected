---
name: aws-well-architected
description: AWS Well-Architected Framework reference — six pillars (Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainability), general design principles, lenses catalog, and the Well-Architected Review (WAR) process. Use when designing, reviewing, or optimizing any AWS workload; when conducting a Well-Architected Review; when assessing risk against AWS best practices (HRIs/MRIs); or when answering questions about AWS pillars, principles, services, or architecture trade-offs.
---

# AWS Well-Architected Framework

The AWS Well-Architected Framework is AWS's canonical guide for designing, building, operating, and reviewing cloud workloads. It is structured around **six pillars**, applied through a **Well-Architected Review (WAR)** in the **AWS Well-Architected Tool**, and extended for specialized domains via **lenses**.

This skill is a structured reference. The entry point (this file) is brief; load the appropriate file from `references/` when you need depth on a specific pillar, the lenses catalog, the review process, or the Shared Responsibility Model.

## The Six Pillars

| Pillar | One-line | Reference file |
|---|---|---|
| Operational Excellence | Support development and run workloads effectively, gain insight into operations, continuously improve. | `references/03-operational-excellence.md` |
| Security | Protect data, systems, and assets to take advantage of cloud technologies to improve security. | `references/04-security.md` |
| Reliability | Perform the intended function correctly and consistently when expected. | `references/05-reliability.md` |
| Performance Efficiency | Use computing resources efficiently to meet system requirements; maintain efficiency as demand and tech evolve. | `references/06-performance-efficiency.md` |
| Cost Optimization | Run systems to deliver business value at the lowest price point. | `references/07-cost-optimization.md` |
| Sustainability | Minimize environmental impact by maximizing utilization and adopting efficient technologies. | `references/08-sustainability.md` |

Each pillar reference file contains:
- AWS's official definition
- Per-pillar design principles (exact AWS wording)
- Best practice areas with question codes (OPS01..OPS11, SEC01..SEC11, REL01..REL13, PERF01..PERF05, COST01..COST11, SUS01..SUS06)
- Best practices per question (BPs)
- Key AWS services per area
- Common anti-patterns
- A 12–15 item review checklist
- Direct AWS doc URLs

## Cross-Pillar General Design Principles

Six general principles apply across all pillars (full detail in `references/01-design-principles.md`):

1. **Stop guessing your capacity needs** — match capacity to actual demand via elasticity.
2. **Test systems at production scale** — clone production for tests, tear down when done.
3. **Automate with architectural experimentation in mind** — IaC + CI/CD turn architecture into reversible experiments.
4. **Allow for evolutionary architectures** — change is continuous, not a multi-year replatform.
5. **Drive architectures using data** — use telemetry (CloudWatch, X-Ray, Cost Explorer, Compute Optimizer) to inform decisions.
6. **Improve through game days** — scheduled chaos exercises build muscle memory before real incidents.

## Shared Responsibility Model (quick refresher)

AWS owns "Security **of** the cloud" — physical infrastructure, hypervisor, AWS service plane.
Customers own "Security **in** the cloud" — IAM, data, classification, network controls, and the guest OS where applicable.

The line shifts by service category:
- **Infrastructure (EC2, VPC, EBS):** customer manages most (OS, patching, agents, security groups)
- **Container (RDS, EMR, Elastic Beanstalk):** AWS manages OS/runtime; customer manages data, IAM, network config
- **Abstracted (S3, DynamoDB, Lambda, SQS):** AWS manages all infra; customer manages data, IAM, classification

Full detail in `references/02-shared-responsibility.md`.

## Lenses

A **lens** is a domain- or industry-specific extension of the framework. A workload typically gets the core Framework Lens **plus** one or more domain lenses (Serverless, SaaS, ML, Generative AI, Data Analytics, IoT, HPC, SAP, Streaming Media, Games, Hybrid Networking, Financial Services, M&A, Migration, Connected Mobility, DevOps, Government, Healthcare, Container Build).

Custom lenses encode org-specific standards. Up to 20 lenses can be applied per workload.

Full catalog with URLs in `references/09-lenses-catalog.md`.

## When to load which reference file

| You're doing | Load |
|---|---|
| Designing or reviewing — security/IAM concerns | `references/04-security.md` |
| Designing or reviewing — reliability/DR concerns | `references/05-reliability.md` |
| Cost analysis, FinOps, rightsizing | `references/07-cost-optimization.md` |
| Performance tuning, instance choice, caching | `references/06-performance-efficiency.md` |
| CI/CD, observability, ops culture | `references/03-operational-excellence.md` |
| Carbon footprint, green workload design | `references/08-sustainability.md` |
| Choosing a domain lens (ML, SaaS, GenAI…) | `references/09-lenses-catalog.md` |
| Conducting a WAR or using the WA Tool | `references/10-wa-tool-and-review.md` |
| Confused about who owns what (AWS vs customer) | `references/02-shared-responsibility.md` |
| Cross-pillar design principles refresher | `references/01-design-principles.md` |

## Applying the framework — quick workflow

**Review mode (existing workload):**
1. **Define the workload** in the WA Tool — name, environment, regions, accounts, lenses to apply.
2. **Gather evidence** before answering — CloudTrail, Config, Trusted Advisor, Security Hub, Compute Optimizer, Cost Explorer, X-Ray.
3. **Walk the pillars** with the right stakeholders (architect, security, ops/SRE, FinOps, data, compliance).
4. **Classify findings** as **HRI** (High Risk Issue) or **MRI** (Medium Risk Issue); capture each with an owner and target date in the improvement plan.
5. **Save a milestone** — re-review on a 6–12 month cadence or after material changes.

**Design mode (greenfield):**
1. Start from the **General Design Principles** + each pillar's design principles.
2. Pick services that satisfy multiple pillars (e.g., Lambda satisfies OPS, REL, COST, SUS at once).
3. Validate the design against each pillar's review checklist before commit.
4. Pre-stage observability (CloudWatch, X-Ray) and IaC (CloudFormation/CDK/Terraform) from day one — they enable the cross-pillar principles "Drive architectures using data" and "Automate with architectural experimentation in mind."

## Notes on framework currency

- **November 6, 2024**: large-scale framework refresh — 100% of OPS, SEC, PERF, COST, SUS plus ~79% of REL pillar best practices updated.
- **New emphases** (2024–2026):
  - **Zero Trust** in SEC (identity-centric, fine-grained, continuous verification)
  - **Observability** promoted to a Design Principle in OPS
  - **Generative AI workload patterns** across pillars + dedicated GenAI Lens
  - **Multi-Region resilience** patterns deepened in REL
  - **Cost-Sustainability coupling** — rightsizing, scheduling, and carbon-aware design as joint levers
  - **Application Security (SEC11)** elevated as a fully-developed area
- The framework evolves continuously. Always cross-check against live AWS docs (URLs in each reference file) for the most current wording — particularly for question/best-practice IDs and lens availability.

## Service-to-pillar quick map (high-level)

When recommending AWS services, mention which pillars they primarily serve:

- **CloudFormation / CDK / Terraform** → OPS, REL, SEC (IaC enables all three)
- **CloudWatch / X-Ray / Application Signals** → OPS, REL, PERF
- **IAM / Identity Center / Organizations / SCPs / RCPs** → SEC, COST (governance)
- **GuardDuty / Security Hub / Inspector / Macie / Detective** → SEC
- **KMS / Secrets Manager / ACM / CloudHSM** → SEC
- **Auto Scaling / Lambda / Fargate** → REL, PERF, COST, SUS
- **Multi-AZ / Aurora Global / DynamoDB Global Tables / Route 53 ARC** → REL
- **CloudFront / Global Accelerator / VPC endpoints / PrivateLink** → PERF, SEC, COST
- **Compute Optimizer / Trusted Advisor** → COST, PERF, OPS
- **Cost Explorer / Budgets / CUR / Cost Anomaly Detection** → COST
- **Savings Plans / Reserved Instances / Spot / Graviton** → COST, SUS
- **S3 Intelligent-Tiering / Glacier / Lifecycle / EBS gp3** → COST, SUS, PERF
- **Customer Carbon Footprint Tool** → SUS
- **WA Tool / Resilience Hub / Fault Injection Service / Backup** → OPS, REL

For deeper service mappings see the "Key AWS Services" section of each pillar reference.
