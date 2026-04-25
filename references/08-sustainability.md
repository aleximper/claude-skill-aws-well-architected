# AWS Well-Architected Framework — Sustainability Pillar

## Definition

The Sustainability pillar focuses on environmental impacts, especially energy consumption and efficiency, since they are important levers for architects to inform direct action to reduce resource usage. Sustainability in the cloud is a nearly continuous effort focused primarily on energy reduction and efficiency across all components of a workload by achieving the maximum benefit from the resources provisioned and minimizing the total resources required. This effort can range from the initial selection of an efficient programming language, adoption of modern algorithms, use of efficient data storage techniques, deploying to correctly sized and efficient compute infrastructure, and minimizing requirements for high-powered end user hardware. AWS frames sustainability under a shared responsibility model: AWS is responsible for the sustainability *of* the cloud (efficient data centers, renewable energy procurement, hardware), while customers are responsible for sustainability *in* the cloud (workload design, architecture choices, and the resources they consume). The pillar was 100% refreshed on November 6, 2024.

## Design Principles

There are six design principles for sustainability in the cloud:

1. **Understand your impact:** Measure the impact of your cloud workload and model the future impact of your workload. Include all sources of impact, including impacts resulting from customer use of your products, and impacts resulting from their eventual decommissioning and retirement. Compare the productive output with the total impact of your cloud workloads by reviewing the resources and emissions required per unit of work. Use this data to establish key performance indicators (KPIs), evaluate ways to improve productivity while reducing impact, and estimate the impact of proposed changes over time.
2. **Establish sustainability goals:** For each cloud workload, establish long-term sustainability goals such as reducing the compute and storage resources required per transaction. Model the return on investment of sustainability improvements for existing workloads, and give owners the resources they must invest in sustainability goals. Plan for growth, and architect your workloads so that growth results in reduced impact intensity measured against an appropriate unit, such as per user or per transaction.
3. **Maximize utilization:** Right-size workloads and implement efficient design to verify high utilization and maximize the energy efficiency of the underlying hardware. Two hosts running at 30% utilization are less efficient than one host running at 60% due to baseline power consumption per host. At the same time, reduce or minimize idle resources, processing, and storage to reduce the total energy required to power your workload.
4. **Anticipate and adopt new, more efficient hardware and software offerings:** Support the upstream improvements your partners and suppliers make to help you reduce the impact of your cloud workloads. Continually monitor and evaluate new, more efficient hardware and software offerings. Design for flexibility to permit the rapid adoption of new efficient technologies.
5. **Use managed services:** Sharing services across a broad customer base helps maximize resource utilization, which reduces the amount of infrastructure needed to support cloud workloads. Migrate workloads to the AWS Cloud and adopt managed services, such as AWS Fargate for serverless containers, where AWS operates at scale and is responsible for their efficient operation. Use managed services that minimize your impact, such as Amazon S3 Lifecycle configurations or Amazon EC2 Auto Scaling.
6. **Reduce the downstream impact of your cloud workloads:** Reduce the amount of energy or resources required to use your services. Reduce the need for customers to upgrade their devices to use your services. Test using device farms to understand expected impact and test with customers to understand the actual impact from using your services.

## Best Practice Areas

There are six best practice areas for sustainability in the cloud: Region selection, Alignment to demand, Software and architecture, Data, Hardware and services, and Process and culture.

### Region Selection (SUS01)

Covers choosing AWS Regions in a way that balances business requirements with sustainability goals, recognizing that Region choice affects performance, cost, and carbon footprint.

- **SUS01-BP01: How do you select Regions for your workload?** Choose Region based on both business requirements and sustainability goals.
  - Evaluate published carbon intensity / renewable-energy data for candidate Regions (e.g., Frankfurt, Stockholm, Ireland, Oregon).
  - Balance latency, data sovereignty, and service availability against the lower-carbon Region option.
  - Locate workloads close to users when network impact dominates; locate close to renewables when compute dominates.
  - Document the Region trade-off decision so future migrations can revisit it.
  - Consolidate workloads into fewer Regions when possible to maximize utilization.

### Alignment to Demand (SUS02)

Covers scaling infrastructure to continually match demand and verifying that you use only the minimum resources required to support users.

- **SUS02-BP01: How do you take advantage of user behavior patterns to support your sustainability goals?** Scale workload infrastructure dynamically.
  - Use Auto Scaling, predictive scaling, and EC2 Spot for elastic capacity.
  - Match instance lifecycle to actual demand windows; turn off non-prod overnight and weekends.
  - Use serverless (Lambda, Fargate) so capacity disappears when there is no work.
  - Eliminate static over-provisioning headroom; rely on metrics-driven scaling.
- **SUS02-BP02:** Align SLAs with sustainability goals — relax over-strict SLAs that drive over-provisioning.
- **SUS02-BP03:** Stop the creation and maintenance of unused assets; decommission orphaned resources.
- **SUS02-BP04:** Optimize geographic placement of workloads based on networking requirements (edge/CloudFront where helpful).
- **SUS02-BP05:** Optimize team member resources for activities performed (right-size dev tooling, virtual desktops).
- **SUS02-BP06:** Implement buffering or throttling (SQS, Kinesis, API throttling) to flatten demand curves.

### Software and Architecture (SUS03)

Covers implementing patterns for load smoothing, sustained high resource utilization, retirement of unused components, and minimizing customer-device impact.

- **SUS03-BP01: How do you take advantage of software and architecture patterns to support your sustainability goals?** Optimize software and architecture for asynchronous and scheduled jobs.
  - Replace synchronous polling with event-driven (EventBridge, SNS, SQS).
  - Batch low-priority jobs into off-peak windows.
  - Use Step Functions for long-running workflows instead of always-on workers.
- **SUS03-BP02:** Remove or refactor workload components with low or no use; instrument usage to find them.
- **SUS03-BP03:** Optimize areas of code that consume the most time or resources (profile hot paths, fix N+1 queries, use efficient algorithms/libraries).
- **SUS03-BP04:** Optimize impact on devices and equipment — keep client apps slim, support older devices, avoid forced upgrades.
- **SUS03-BP05:** Use software patterns and architectures that best support data access and storage patterns (CQRS, caching, read replicas where appropriate).

### Data (SUS04)

Covers data management practices that reduce provisioned storage and the resources required to use data — classify, lifecycle, deduplicate, and minimize movement.

- **SUS04-BP01: How do you take advantage of data management policies and patterns to support your sustainability goals?** Implement a data classification policy.
- **SUS04-BP02:** Use technologies that support data access and storage patterns (right storage class, columnar formats like Parquet for analytics).
- **SUS04-BP03:** Use policies to manage the lifecycle of your datasets (S3 Lifecycle, Intelligent-Tiering, Glacier Instant/Flexible/Deep Archive).
- **SUS04-BP04:** Use elasticity and automation to expand block storage or file system (EBS gp3, EFS Infrequent Access).
- **SUS04-BP05:** Remove unneeded or redundant data; deduplicate, compress, drop snapshots/old logs.
- **SUS04-BP06:** Use shared file systems or storage to access common data instead of duplicating per-host copies.
- **SUS04-BP07:** Minimize data movement across networks (VPC endpoints, edge caching, regional locality).
- **SUS04-BP08:** Back up data only when difficult to recreate; tune RPO/RTO to actual need.

### Hardware and Services (SUS05)

Covers reducing sustainability impact by minimizing hardware provisioning, choosing the most efficient instance/service for the job, and offloading to managed services.

- **SUS05-BP01: How do your hardware management and usage practices support your sustainability goals?** Use the minimum amount of hardware to meet your needs (right-size with Compute Optimizer, Trusted Advisor).
- **SUS05-BP02:** Use instance types with the least impact — prefer Graviton (ARM) for better performance-per-watt; pick newer-generation instances.
- **SUS05-BP03:** Use managed services (RDS, Aurora Serverless, Fargate, Lambda, OpenSearch Serverless) so AWS amortizes hardware overhead.
- **SUS05-BP04:** Optimize your use of hardware-based compute accelerators (GPUs, Inferentia, Trainium); release them when idle, batch inference, share via Elastic Inference patterns.

### Process and Culture (SUS06)

Covers reducing sustainability impact through changes to development, test, and deployment practices, and cascading sustainability awareness across teams.

- **SUS06-BP01: How do your organizational processes support your sustainability goals?** Communicate and cascade your sustainability goals to engineering teams and tie them to KPIs.
- **SUS06-BP02:** Adopt methods that can rapidly introduce sustainability improvements (CI/CD, feature flags, blue/green) so efficient changes ship fast.
- **SUS06-BP03:** Keep your workload up-to-date — current runtimes, OS, and instance generations are typically more efficient.
- **SUS06-BP04:** Increase utilization of build environments — share build farms, use spot CI runners, auto-shutdown idle pipelines.
- **SUS06-BP05:** Use managed device farms for testing (AWS Device Farm) instead of buying and powering physical fleets.

## Key AWS Services & Features

- **Carbon visibility:** **AWS Customer Carbon Footprint Tool** (in Billing console) reports MTCO2e by service and Region; use it to set baselines and track KPIs per the "Understand your impact" principle.
- **Efficient compute:** **AWS Graviton** (ARM) processors deliver up to ~60% better energy efficiency than comparable x86; **Spot Instances** monetize otherwise-idle capacity; **AWS Lambda** and **AWS Fargate** eliminate idle servers entirely; **EC2 Auto Scaling** matches capacity to demand.
- **Storage tiering:** **S3 Intelligent-Tiering** auto-moves data across access tiers; **S3 Glacier Instant/Flexible Retrieval** and **Glacier Deep Archive** for cold data; **S3 Lifecycle** policies; **EBS gp3** (more efficient than gp2 at equivalent performance); **EFS Infrequent Access / Archive** classes.
- **Auto-scaling and serverless to match demand:** EC2 Auto Scaling, Application Auto Scaling, DynamoDB on-demand, Aurora Serverless v2, Lambda, Fargate, Step Functions.
- **Region selection:** Prefer AWS Regions powered by renewables — e.g., **eu-central-1 (Frankfurt)** and other EU Regions on green grids, **eu-west-1 (Ireland)**, **eu-north-1 (Stockholm)**, **us-west-2 (Oregon)**. AWS targets 100% renewable energy and net-zero carbon by 2040 (Climate Pledge).
- **Supporting tools:** AWS Compute Optimizer, AWS Trusted Advisor, AWS Cost Explorer rightsizing recommendations, AWS Device Farm.

## Common Anti-patterns

- Persistently over-provisioning compute "just in case" instead of relying on Auto Scaling and metrics-driven capacity.
- Leaving idle resources running — orphaned EBS volumes, unattached EIPs, stopped-but-not-terminated instances, dev environments running 24/7.
- Choosing a Region purely on latency or cost without consulting the Customer Carbon Footprint Tool or renewable-energy posture.
- No carbon monitoring or sustainability KPIs — teams cannot improve what they do not measure.
- Synchronous, polling-heavy architectures where asynchronous, event-driven, or batched designs would do the same work with far less idle compute.
- No decommissioning process — components, datasets, and snapshots accumulate indefinitely with no owner.
- Storing all data in hot tiers (S3 Standard, gp2/io1 EBS) when most of it is rarely accessed and could live in Intelligent-Tiering or Glacier.
- Sticking with old instance generations and x86 when Graviton or newer generations would deliver the same workload at lower energy.

## Review Checklist

1. Have you measured your workload's carbon footprint via the AWS Customer Carbon Footprint Tool and set sustainability KPIs per unit of work?
2. Did you evaluate Region selection against both business requirements and sustainability/carbon-intensity data?
3. Does the workload scale dynamically (Auto Scaling, serverless) so capacity tracks demand?
4. Are non-production environments shut down outside business hours?
5. Are SLAs reviewed so they don't force over-provisioning beyond what the business actually needs?
6. Is there a documented decommissioning process for unused components, data, and snapshots?
7. Are async, event-driven, and batched patterns used wherever synchronous work isn't required?
8. Are S3 Lifecycle / Intelligent-Tiering / Glacier and EBS gp3 used to keep data on the most efficient tier?
9. Are workloads running on Graviton or the latest instance generation where compatible?
10. Are managed and serverless services (Lambda, Fargate, Aurora Serverless) preferred over self-managed equivalents?
11. Is code profiled for hot paths, and are inefficient queries/algorithms refactored?
12. Are sustainability goals communicated across teams, and are runtimes/OS/dependencies kept up to date?

## References

- https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/sustainability-pillar.html
- https://docs.aws.amazon.com/wellarchitected/latest/framework/sus-design-principles.html
- https://docs.aws.amazon.com/wellarchitected/latest/framework/sus-def.html
- https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/region-selection.html
- https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/alignment-to-demand.html
- https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/software-and-architecture.html
- https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/data.html
- https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/hardware-and-services.html
- https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/process-and-culture.html
- https://aws.amazon.com/aws-cost-management/aws-customer-carbon-footprint-tool/
- https://sustainability.aboutamazon.com/climate-solutions/the-climate-pledge
