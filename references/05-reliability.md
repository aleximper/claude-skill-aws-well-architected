# AWS Well-Architected Framework — Reliability Pillar

## Definition

The reliability pillar encompasses the ability of a workload to perform its intended function correctly and consistently when it's expected to. This includes the ability to operate and test the workload through its total lifecycle. Reliable workloads are built on strong foundations, resilient architecture, consistent change management, and proven failure recovery processes — practices that overcome the traditional on-premises challenges of single points of failure, lack of automation, and lack of elasticity. (Note: 79% of Reliability best practices were refreshed in November 2024.)

## Design Principles

1. **Automatically recover from failure** — By monitoring a workload for key performance indicators (KPIs) tied to business value (not technical operation), you can run automation when a threshold is breached. This enables automatic notification, tracking of failures, and automated recovery processes that work around or repair the failure — and with sophisticated automation, can anticipate and remediate failures before they occur.

2. **Test recovery procedures** — In the cloud, you can test how your workload fails and validate your recovery procedures. Use automation to simulate different failures or to recreate scenarios that led to past failures, exposing failure pathways that you can test and fix before a real failure occurs.

3. **Scale horizontally to increase aggregate workload availability** — Replace one large resource with multiple small resources to reduce the impact of a single failure on the overall workload. Distribute requests across multiple smaller resources so they don't share a common point of failure.

4. **Stop guessing capacity** — Resource saturation (demand exceeding capacity) is a common cause of on-premises failure. In the cloud, monitor demand and workload utilization, and automate the addition or removal of resources to maintain the optimal level — neither over- nor under-provisioned.

5. **Manage change through automation** — Changes to your infrastructure should be made using automation. The changes that need to be managed include changes to the automation itself, which can then be tracked and reviewed.

## Best Practice Areas

The Reliability pillar contains four best practice areas spanning thirteen questions (REL01–REL13).

### Foundations

Covers the prerequisite requirements that must be in place before architecting any system — service quotas/limits and the underlying network topology. These foundational decisions influence reliability across the entire workload lifecycle.

**REL01: How do you manage service quotas and constraints?**
- REL01-BP01: Be aware of service quotas and constraints
- REL01-BP02: Manage service quotas across accounts and Regions
- REL01-BP03: Accommodate fixed service quotas and constraints through architecture
- REL01-BP04: Monitor and manage quotas
- REL01-BP05: Automate quota management
- REL01-BP06: Ensure that a sufficient gap exists between the current quotas and the maximum usage to accommodate failover

**REL02: How do you plan your network topology?**
- REL02-BP01: Use highly available network connectivity for your workload public endpoints
- REL02-BP02: Provision redundant connectivity between private networks in the cloud and on-premises environments
- REL02-BP03: Ensure IP subnet allocation accounts for expansion and availability
- REL02-BP04: Prefer hub-and-spoke topologies over many-to-many mesh
- REL02-BP05: Enforce non-overlapping private IP address ranges in all private address spaces where they are connected

### Workload Architecture

Covers how the workload itself is structured — service decomposition and the design of interactions between distributed components — to prevent failures and to mitigate or withstand them when they occur.

**REL03: How do you design your workload service architecture?**
- REL03-BP01: Choose how to segment your workload (monolith vs. SOA vs. microservices)
- REL03-BP02: Build services focused on specific business domains and functionality
- REL03-BP03: Provide service contracts per API

**REL04: How do you design interactions in a distributed system to prevent failures?**
- REL04-BP01: Identify the kind of distributed systems you depend on
- REL04-BP02: Implement loosely coupled dependencies (queues, streams, workflows, event buses)
- REL04-BP03: Do constant work (avoid bimodal load patterns)
- REL04-BP04: Make mutating operations idempotent

**REL05: How do you design interactions in a distributed system to mitigate or withstand failures?**
- REL05-BP01: Implement graceful degradation to transform applicable hard dependencies into soft dependencies
- REL05-BP02: Throttle requests
- REL05-BP03: Control and limit retry calls (use exponential backoff with jitter)
- REL05-BP04: Fail fast and limit queues
- REL05-BP05: Set client timeouts
- REL05-BP06: Make systems stateless where possible
- REL05-BP07: Implement emergency levers

### Change Management

Covers how changes — both demand-driven and operator-driven — are observed, accommodated, and applied. Anticipating and managing change reliably reduces the risk of unintended impact on availability.

**REL06: How do you monitor workload resources?**
- REL06-BP01: Monitor all components for the workload (Generation)
- REL06-BP02: Define and calculate metrics (Aggregation)
- REL06-BP03: Send notifications (real-time processing and alarming)
- REL06-BP04: Automate responses (real-time processing and alarming)
- REL06-BP05: Analyze logs (storage and analytics)
- REL06-BP06: Regularly review monitoring scope and metrics
- REL06-BP07: Monitor end-to-end tracing of requests through your system

**REL07: How do you design your workload to adapt to changes in demand?**
- REL07-BP01: Use automation when obtaining or scaling resources
- REL07-BP02: Obtain resources upon detection of impairment to a workload
- REL07-BP03: Obtain resources upon detection that more resources are needed for a workload
- REL07-BP04: Load test your workload

**REL08: How do you implement change?**
- REL08-BP01: Use runbooks for standard activities such as deployment
- REL08-BP02: Integrate functional testing as part of your deployment
- REL08-BP03: Integrate resiliency testing as part of your deployment
- REL08-BP04: Deploy using immutable infrastructure
- REL08-BP05: Deploy changes with automation

### Failure Management

Covers backup, fault isolation, withstanding component failures, testing reliability, and disaster recovery — the practices that allow a workload to detect, contain, and recover from failures of any scope.

**REL09: How do you back up data?**
- REL09-BP01: Identify and back up all data that needs to be backed up, or reproduce the data from sources
- REL09-BP02: Secure and encrypt backups
- REL09-BP03: Perform data backup automatically
- REL09-BP04: Perform periodic recovery of the data to verify backup integrity and processes

**REL10: How do you use fault isolation to protect your workload?**
- REL10-BP01: Deploy the workload to multiple locations (Multi-AZ, Multi-Region, AWS Local Zones, Outposts)
- REL10-BP02: Automate recovery for components constrained to a single location
- REL10-BP03: Use bulkhead architectures to limit scope of impact (cell-based architecture, shuffle sharding)

**REL11: How do you design your workload to withstand component failures?**
- REL11-BP01: Monitor all components of the workload to detect failures
- REL11-BP02: Fail over to healthy resources
- REL11-BP03: Automate healing on all layers
- REL11-BP04: Rely on the data plane and not the control plane during recovery
- REL11-BP05: Use static stability to prevent bimodal behavior
- REL11-BP06: Send notifications when events impact availability
- REL11-BP07: Architect your product to meet availability targets and uptime service level agreements (SLAs)

**REL12: How do you test reliability?**
- REL12-BP01: Use playbooks to investigate failures
- REL12-BP02: Perform post-incident analysis
- REL12-BP03: Test scalability and performance requirements
- REL12-BP04: Test resiliency using chaos engineering
- REL12-BP05: Conduct game days regularly

**REL13: How do you plan for disaster recovery (DR)?**
- REL13-BP01: Define recovery objectives for downtime and data loss (RTO and RPO)
- REL13-BP02: Use defined recovery strategies to meet the recovery objectives
- REL13-BP03: Test disaster recovery implementation to validate the implementation
- REL13-BP04: Manage configuration drift at the DR site or Region
- REL13-BP05: Automate recovery

## RTO, RPO, and DR Strategies

**Recovery Time Objective (RTO)** is the maximum acceptable delay between the interruption of service and restoration of service. It is an organization-defined target (distinct from MTTR, which is a mean) that determines what an acceptable time window of unavailability is.

**Recovery Point Objective (RPO)** is the maximum acceptable amount of time since the last data recovery point. It defines the acceptable amount of data loss between the last recovery point and the interruption of service.

AWS defines four DR strategies, ordered from lowest cost / longest recovery time to highest cost / fastest recovery:

| Strategy | Typical RTO | Typical RPO | Cost | How it works |
|---|---|---|---|---|
| **Backup & Restore** | Hours (often 24h+) | Hours (often 24h+) | Lowest | Periodic backups (e.g., AWS Backup, S3, snapshots) replicated cross-Region; infrastructure rebuilt from IaC and data restored on demand. Suitable for non-critical workloads. |
| **Pilot Light** | 10s of minutes | Minutes | Low–Medium | Core data is live-replicated to the DR Region and minimal "always-on" services (databases, AMIs, IaC) are kept ready. Compute/front-end is provisioned and scaled out at failover time. |
| **Warm Standby** | Minutes | Seconds–minutes | Medium–High | A scaled-down but fully functional copy of production runs continuously in the DR Region; on failover, capacity is scaled up to handle production load. |
| **Multi-Site Active-Active** | Real-time / near-zero | Near-zero | Highest | Full production capacity runs in two or more Regions simultaneously, serving live traffic. Data is replicated continuously (often via Aurora Global Database, DynamoDB Global Tables) and traffic is routed via Route 53 / Global Accelerator. |

Choice of strategy is driven by business-defined RTO/RPO; cost and operational complexity rise sharply as RTO/RPO shrink. Always test failover with REL13-BP03 and manage drift between primary and DR sites (REL13-BP04).

## Key AWS Services

- **Networking & global**: Amazon Route 53 (health checks, failover routing, ARC routing controls), Amazon CloudFront, AWS Global Accelerator, AWS Transit Gateway, AWS Direct Connect (with redundant connections), VPC, AWS PrivateLink.
- **Compute resilience**: Amazon EC2 Auto Scaling, Elastic Load Balancing (ALB/NLB/GWLB), Multi-AZ deployments, EC2 Fleet, AWS Lambda (regional, multi-AZ by default), Amazon ECS / EKS with multi-AZ node groups, Amazon EC2 Spot with capacity-optimized strategies.
- **Data resilience**: Amazon RDS Multi-AZ and Multi-AZ DB clusters, Amazon Aurora Global Database, Amazon DynamoDB Global Tables and point-in-time recovery, Amazon S3 (11 9s durability, Cross-Region Replication, Same-Region Replication, S3 Multi-Region Access Points / MRAP), Amazon EFS, Amazon FSx, AWS Backup (cross-account, cross-Region).
- **DR and resilience tooling**: AWS Resilience Hub (assesses RTO/RPO against targets), AWS Elastic Disaster Recovery (DRS), AWS Fault Injection Service (FIS) for chaos engineering, Amazon Route 53 Application Recovery Controller (ARC), AWS CloudFormation / CDK for immutable infrastructure.
- **Observability**: Amazon CloudWatch (metrics, alarms, Synthetics, RUM, Logs), AWS X-Ray, AWS Health Dashboard, EventBridge.
- **Quotas & change**: AWS Service Quotas (with cross-Region/cross-account management), AWS Trusted Advisor, AWS Config, AWS Systems Manager (runbooks, automation, patch).

## Common Anti-patterns

- Single-AZ deployments for production databases or stateful tiers — the workload survives instance failure but not zone failure.
- Hard dependencies on the control plane during recovery (e.g., requiring `RunInstances` to come back up); REL11-BP04 demands data-plane reliance instead.
- Backups that are never restored. Without REL09-BP04 verification, RPO is theoretical and may be unrecoverable.
- Synchronous, tightly coupled service-to-service calls without timeouts, retries with jitter, or circuit breakers — violates REL04-BP02 and REL05-BP03/05.
- Manual deployments and configuration drift, especially in the DR Region — violates REL08 and REL13-BP04.
- Treating service quotas as static and discovering them at failover time instead of monitoring them (REL01-BP04) and leaving headroom for failover (REL01-BP06).
- "Bimodal" architectures whose behavior changes under stress (e.g., caches that vanish during failure, autoscaling that depends on the failed component) — violates REL11-BP05 (static stability).
- No game days, no chaos engineering, no tested runbooks — recovery procedures only exist on paper (violates REL12 and Design Principle #2).

## Review Checklist

1. Are RTO and RPO explicitly defined per workload tier and signed off by the business?
2. Is the workload deployed across at least two Availability Zones for every stateful and stateless tier?
3. Are service quotas monitored, and is there sufficient headroom in every Region used for failover (REL01-BP06)?
4. Is the network topology hub-and-spoke with non-overlapping CIDRs and redundant on-premises connectivity?
5. Are inter-service calls loosely coupled (queues, streams, events) with timeouts, bounded retries with jitter, and idempotent mutations?
6. Are health checks implemented at every layer, with automated failover to healthy resources?
7. Does recovery rely on the data plane rather than the control plane?
8. Is the architecture statically stable (does it behave the same in degraded conditions as in normal ones)?
9. Are backups automated, encrypted, cross-Region/cross-account where required, and periodically test-restored?
10. Is fault isolation enforced via cell-based architecture, shuffle sharding, or bulkheads to limit blast radius?
11. Is all infrastructure deployed via IaC (immutable, automated), with no manual changes in production or DR?
12. Are deployments accompanied by functional and resiliency testing, and capable of safe rollback (or feature-flag disable)?
13. Are chaos engineering experiments and game days run regularly with AWS FIS or equivalent?
14. Is a documented DR strategy chosen (Backup & Restore / Pilot Light / Warm Standby / Multi-Site Active-Active) appropriate to RTO/RPO, and is it tested end-to-end?
15. Is configuration drift between primary and DR sites continuously detected and remediated, and is recovery itself automated (REL13-BP05)?

## References

- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/reliability.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/design-principles.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/definition.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/foundations.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/workload-architecture.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/change-management.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/failure-management.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/disaster-recovery-dr-objectives.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/plan-for-disaster-recovery-dr.html
- https://docs.aws.amazon.com/resilience-hub/
- https://docs.aws.amazon.com/drs/
- https://docs.aws.amazon.com/fis/
