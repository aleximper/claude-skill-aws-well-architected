# AWS Well-Architected Framework — Performance Efficiency Pillar

## Definition

The Performance Efficiency pillar of the AWS Well-Architected Framework focuses on the ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve. It encompasses selecting the right resource types and sizes based on workload requirements, monitoring performance, and making informed decisions to maintain efficiency as business needs evolve. Achieving and sustaining performance efficiency requires a data-driven approach to building high-performance architectures, understanding workload patterns and requirements, measuring performance against business outcomes, and architecting solutions that scale and adapt as conditions change. The pillar provides architectural best practices and design guidance for designing, delivering, and maintaining workloads that achieve the desired performance with the most efficient use of cloud resources.

## Design Principles

1. **Democratize advanced technologies** — Make advanced technology implementation easier for your team by delegating complex tasks to your cloud vendor. Rather than asking your IT team to learn about hosting and running new technologies (such as NoSQL databases, media transcoding, and machine learning), consume them as services so the team can focus on product development instead of resource provisioning and management.

2. **Go global in minutes** — Deploy your workload in multiple AWS Regions around the world with just a few clicks. This allows you to provide lower latency and a better experience for your customers at minimal cost while taking advantage of AWS's global infrastructure.

3. **Use serverless architectures** — Serverless architectures remove the need for you to run and maintain physical servers for traditional compute activities. Serverless services such as AWS Lambda eliminate the operational burden of managing servers and can also lower transactional costs because managed services operate at cloud scale.

4. **Experiment more often** — With virtual and automatable resources, you can quickly carry out comparative testing using different types of instances, storage, or configurations. Experimentation enables data-driven decisions about which combination of resources best meets your performance goals.

5. **Consider mechanical sympathy** — Use the technology approach that aligns best with your goals. Understand how cloud services consume data or perform compute work so you can choose the right service or configuration — for example, picking a database approach (SQL vs. NoSQL) that matches your data access patterns.

## Best Practice Areas

### Architecture Selection

Covers the process of selecting an optimal architecture and the right combination of solutions (compute, storage, database, network) to align with workload requirements. The cloud presents many options that didn't exist in traditional on-premises environments, and selecting the proper mix is foundational to performance.

**PERF01 — How do you select appropriate cloud resources and architecture patterns for your workload?**
- Understand the available cloud services, resources, and architecture patterns (compute, storage, database, network).
- Use guidance from AWS, partners, or independent sources (whitepapers, reference architectures, AWS Solutions Library) to evaluate alternatives.
- Factor cost, requirements (latency, throughput, RTO/RPO), constraints (compliance, data sovereignty), and compatibility into the choice.
- Use policies or reference architectures to standardize selection across teams.
- Use guidance from your cloud provider or appropriate partner to learn about new services and features as they become available.
- Benchmark and load test architecture options before committing to a design.

### Compute and Hardware

Covers selection of the optimal compute solution for the workload. Compute choices include instance-based (EC2), container-based (ECS/EKS/Fargate), function-based (Lambda), and specialized hardware (GPU, FPGA, Inferentia, Trainium). The right choice depends on application design, usage patterns, and configuration settings.

**PERF02 — How do you select and use compute resources in your workload?**
- Evaluate the available compute options (instances, containers, functions, edge compute) against workload requirements (latency, throughput, concurrency, cold start tolerance).
- Understand the available compute configuration and features (instance families, sizes, generations, processors including Graviton, memory/CPU ratio, accelerators).
- Collect compute-related metrics (CPU, memory, network, custom application metrics) to make informed decisions.
- Use AWS Compute Optimizer and load testing to right-size and validate selections.
- Use the available elasticity of resources — auto scaling groups, Lambda concurrency, Fargate scaling — to match supply with demand.
- Re-evaluate compute needs based on metrics; adopt newer generations and architectures (such as Graviton) where appropriate.

### Data Management

Covers selecting and configuring optimal storage and database solutions. The optimal solution depends on the type of data, access patterns, performance requirements (latency, IOPS, throughput), durability/availability, and cost.

**PERF03 — How do you store, manage, and access data in your workload?**
- Use a purpose-built data store that best supports your data access and storage requirements (relational, key-value, document, in-memory, graph, time-series, ledger, search).
- Evaluate available configuration options for the data store (e.g., RDS instance class and storage type, DynamoDB on-demand vs. provisioned, S3 storage classes, EBS gp3 vs. io2 Block Express).
- Collect and record data store performance metrics (CloudWatch, Performance Insights, slow query logs) to drive tuning.
- Choose data storage based on access patterns — reads vs. writes, hot vs. cold, transactional vs. analytical.
- Optimize data storage based on access patterns and metrics — tiering, partitioning, indexing, caching, compression.
- Implement strategies to improve query performance such as caching (ElastiCache, DAX), read replicas, and proper indexing.

### Networking and Content Delivery

Covers selecting and configuring optimal networking solutions. Solutions must consider latency, throughput, jitter, bandwidth requirements, location of users, and the placement of workload components relative to each other.

**PERF04 — How do you select and configure networking resources in your workload?**
- Understand how networking impacts performance (latency, bandwidth, jitter, packet loss, throughput) and the location of your users and dependencies.
- Evaluate available networking features (VPC, VPC endpoints, PrivateLink, Transit Gateway, placement groups, enhanced networking, EFA, ENA Express).
- Choose appropriately sized dedicated connectivity or VPN for hybrid workloads (Direct Connect, Site-to-Site VPN).
- Use load balancing (ALB, NLB, GWLB) to distribute traffic across multiple resources and Availability Zones.
- Use encryption appropriately (TLS termination at edge, in-transit encryption with minimal overhead).
- Use the network protocol that best supports performance requirements (HTTP/2, HTTP/3, gRPC, QUIC).
- Choose network features (CloudFront, Global Accelerator, Route 53 latency/geolocation routing) to reduce latency for users.
- Optimize network configuration based on metrics — VPC Flow Logs, CloudWatch network metrics, Reachability Analyzer.

### Process and Culture

Covers building a culture that enables ongoing performance efficiency. Performance is not a one-time effort — teams must continually adopt new patterns, tools, and services, and embed performance considerations into delivery processes.

**PERF05 — How do your organizational practices and culture contribute to performance efficiency in your workload?**
- Establish key performance indicators (KPIs) that align with business outcomes and the customer experience.
- Use monitoring solutions to understand the areas where performance is most critical (CloudWatch, X-Ray, Application Signals, RUM, Synthetics).
- Define a process to improve workload performance — runbooks, performance reviews, regression testing in CI/CD.
- Adopt a consistent process to record and act on performance-related issues, integrating findings back into design.
- Review metrics at regular intervals and after significant changes; benchmark against business KPIs.
- Load test your workload using realistic and representative traffic before launch and on an ongoing basis.
- Use automation to deploy testing and monitoring; integrate performance testing into CI/CD pipelines.
- Stay up to date on new resources and services — adopt newer instance families, managed services, and features as they become available.

## Key AWS Services

**Compute**
- Amazon EC2 — broad selection of instance families: general purpose (M7i, M7g Graviton), compute-optimized (C7i, C7g), memory-optimized (R7i, X2), storage-optimized (I4i, D3), accelerated (P5, G6, Inf2, Trn1). Graviton-based instances offer better price-performance.
- AWS Lambda — event-driven serverless compute; eliminates server management.
- AWS Fargate — serverless containers for ECS and EKS.
- Amazon ECS / Amazon EKS — container orchestration for Docker and Kubernetes workloads.
- AWS Batch — managed batch computing for HPC and large-scale jobs.

**Storage**
- Amazon S3 — object storage with classes (Standard, Intelligent-Tiering, Standard-IA, One Zone-IA, Glacier Instant Retrieval, Glacier Flexible Retrieval, Glacier Deep Archive) for varying access patterns.
- Amazon EBS — block storage including gp3 (general purpose with provisioned IOPS), io2 Block Express (high-performance), st1, sc1.
- Amazon EFS — fully managed elastic NFS file system; Standard and One Zone, with bursting/provisioned/elastic throughput.
- Amazon FSx — file systems for Windows, Lustre (HPC), NetApp ONTAP, OpenZFS.
- AWS Storage Gateway — hybrid cloud storage.

**Database**
- Amazon RDS — managed relational databases (PostgreSQL, MySQL, MariaDB, Oracle, SQL Server, Db2).
- Amazon Aurora — MySQL/PostgreSQL-compatible with up to 5x performance; Aurora Serverless v2 for variable workloads; Aurora Limitless Database for sharding.
- Amazon DynamoDB — serverless key-value/document NoSQL with single-digit millisecond performance; DAX for microsecond reads.
- Amazon ElastiCache — Redis OSS and Memcached for in-memory caching.
- Amazon MemoryDB — Redis-compatible durable in-memory database.
- Amazon Redshift — petabyte-scale data warehouse; Redshift Serverless.
- Amazon Neptune — graph database.
- Amazon Timestream — time-series database.
- Amazon DocumentDB, Amazon Keyspaces, Amazon QLDB — purpose-built data stores.
- Amazon OpenSearch Service — search and analytics.

**Network / CDN**
- Amazon CloudFront — global content delivery network.
- AWS Global Accelerator — improves availability and performance via the AWS global network.
- AWS Direct Connect — dedicated private connectivity to AWS.
- AWS Transit Gateway — central hub connecting VPCs and on-premises.
- VPC peering, AWS PrivateLink, VPC endpoints — private connectivity patterns.
- Elastic Load Balancing — ALB, NLB, GWLB for distributing traffic.
- Amazon Route 53 — DNS with latency-based, geolocation, and geoproximity routing.

**Analytics**
- Amazon Athena — serverless SQL query of S3 data.
- Amazon EMR — managed Hadoop/Spark/Presto.
- Amazon Kinesis — Data Streams, Data Firehose, Managed Service for Apache Flink for real-time data.
- AWS Glue — serverless ETL and data catalog.
- Amazon MSK — managed Apache Kafka.

**Optimization Tools**
- AWS Compute Optimizer — ML-based right-sizing recommendations for EC2, EBS, Lambda, ECS on Fargate, Auto Scaling groups.
- AWS Trusted Advisor — performance, cost, security, and fault tolerance checks.
- Amazon CloudWatch (metrics, Logs, Application Signals, RUM, Synthetics) — observability.
- AWS X-Ray — distributed tracing.
- AWS Cost Explorer + rightsizing recommendations.
- Amazon DevOps Guru — ML-powered operational insights.

## Common Anti-patterns

- **Over-provisioning resources "just in case"** — selecting instance sizes far larger than benchmarked load requires, instead of right-sizing with Compute Optimizer and scaling elastically.
- **Using a wrong or outdated instance family** — running a memory-bound workload on compute-optimized instances, or staying on previous generations (M5, C5) when newer Graviton (M7g, C7g) offers better price-performance.
- **Treating one database engine as universal** — forcing every workload onto a single relational database instead of using purpose-built data stores (DynamoDB for key-value, Timestream for time-series, OpenSearch for search).
- **Ignoring caching opportunities** — hitting the database for every read instead of leveraging CloudFront, ElastiCache, DAX, or API Gateway caching.
- **No benchmarking or load testing before launch** — choosing architecture based on assumptions rather than data, and discovering bottlenecks in production.
- **Lift-and-shift without re-architecting** — deploying monoliths on EC2 and missing the elasticity, managed services, and serverless options the cloud offers.
- **Single-Region deployment for global users** — serving users across continents from one Region, accepting high latency instead of using CloudFront, Global Accelerator, or multi-Region.
- **Not monitoring or acting on performance metrics** — collecting CloudWatch data but lacking KPIs, alarms, or a process to feed findings back into design.
- **Hard-coding capacity** — using static EC2 fleets without Auto Scaling, or DynamoDB provisioned capacity tuned for peak instead of on-demand or auto scaling.
- **Ignoring the network path** — placing dependent components in different AZs or Regions without considering data transfer cost and latency, or skipping VPC endpoints and routing through NAT/internet.

## Review Checklist

1. Have you documented workload performance requirements (latency, throughput, concurrency, RTO/RPO) and KPIs tied to business outcomes?
2. Have you evaluated multiple architecture patterns (serverless vs. containers vs. EC2) before selecting one?
3. Are you using the latest-generation instance families and have you evaluated Graviton for applicable workloads?
4. Have you run AWS Compute Optimizer and acted on its right-sizing recommendations within the last 90 days?
5. Are compute resources elastic — using Auto Scaling, Lambda concurrency, or Fargate — to match supply with demand?
6. Are you using purpose-built data stores aligned with each workload's access pattern (relational, NoSQL, in-memory, time-series, graph, search)?
7. Have you configured EBS volumes (gp3 vs. io2) and S3 storage classes (Intelligent-Tiering, IA, Glacier) to match access patterns?
8. Is caching implemented at the appropriate layers (CloudFront, ElastiCache/MemoryDB, DAX, application)?
9. Are users served via CloudFront, Global Accelerator, or Region selection appropriate to their geography?
10. Are you using VPC endpoints, PrivateLink, or Transit Gateway instead of routing private traffic through the public internet?
11. Have load tests been run with realistic, representative traffic and integrated into the CI/CD pipeline?
12. Do you collect application, infrastructure, and database performance metrics (CloudWatch, X-Ray, Performance Insights) and review them at regular intervals?
13. Are alarms and runbooks defined for performance regressions, with a documented process to act on findings?
14. Do teams have a mechanism to evaluate and adopt new AWS services, instance types, and features as they become available?
15. Has performance been validated end-to-end, including network path, data store, compute, and client-side experience (RUM, Synthetics)?

## References

- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/welcome.html
- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/performance-efficiency-pillar.html
- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/design-principles.html
- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/definition.html
- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/architecture-selection.html
- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/compute-and-hardware.html
- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/data-management.html
- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/networking-and-content-delivery.html
- https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/process-and-culture.html
- https://docs.aws.amazon.com/compute-optimizer/latest/ug/what-is-compute-optimizer.html
- https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html
- https://aws.amazon.com/ec2/graviton/
