# Shared Responsibility Model

Source: https://aws.amazon.com/compliance/shared-responsibility-model/

## Security *OF* the Cloud vs. Security *IN* the Cloud

AWS frames the model with two complementary obligations:

- **AWS — "Security of the Cloud":** "AWS is responsible for protecting the infrastructure that runs all of the services offered in the AWS Cloud." This covers the hardware, software, networking, and physical facilities that run AWS services — Regions, Availability Zones, edge locations, hypervisors, and the global network.
- **Customer — "Security in the Cloud":** customer responsibility "encompasses the guest operating system (including updates and security patches), other associated application software as well as the configuration of the AWS provided security group firewall." It also covers IAM, data classification, encryption choices, and network ACLs.

The line between *of* and *in* is not fixed — it shifts with the abstraction level of each service.

## How the Line Shifts Across Service Categories

### Infrastructure services (EC2, VPC, EBS)

AWS classifies "a service such as Amazon Elastic Compute Cloud (Amazon EC2)" as **Infrastructure as a Service (IaaS)**, which "requires the customer to perform all of the necessary security configuration and management tasks." The customer owns:

- Guest OS, patching, kernel hardening, and host-based agents (EDR, log shipping)
- IAM roles attached to instances (instance profiles)
- Security groups, NACLs, route tables, VPC topology
- EBS encryption configuration and snapshot policies
- Application code, dependencies, and secrets handling

AWS owns the hypervisor, host hardware, and physical facility.

### Container services (RDS, EMR, Elastic Beanstalk)

These sit between IaaS and abstracted services. AWS manages the underlying OS, the database/runtime engine, patching, and HA primitives. The customer is still responsible for:

- Network configuration (subnet placement, security groups, parameter groups)
- IAM authentication and authorization (e.g., RDS IAM auth, EMR step-level IAM)
- Encryption-at-rest enablement (KMS key choice, key policies)
- Backup retention, point-in-time recovery configuration
- Database/cluster configuration, schema, and the **data itself**
- Audit logging configuration (e.g., RDS Performance Insights, EMR logs to S3)

The customer no longer touches the OS but still owns the configuration surface above it.

### Abstracted services (S3, DynamoDB, Lambda, SQS, EventBridge, API Gateway)

AWS's wording: "For abstracted services, such as Amazon S3 and Amazon DynamoDB, AWS operates the infrastructure layer, the operating system, and platforms, and customers access the endpoints to store and retrieve data."

The customer's responsibilities collapse to:

- **Data** — what goes in, classification, lifecycle, retention
- **IAM** — resource policies, bucket policies, function execution roles, access points
- **Encryption choices** — SSE-S3 vs SSE-KMS vs SSE-C, KMS key custody and policies
- **Client-side controls** — VPC endpoint policies, mTLS where supported
- **Configuration of public/private access** — S3 Block Public Access, function URLs, API Gateway resource policies

There is no OS, no patch cycle, and no instance to harden. The attack surface is almost entirely IAM and the data.

## Inherited vs. Shared vs. Customer-Specific Controls

AWS partitions compliance controls into three buckets:

- **Inherited controls** — "Controls which a customer fully inherits from AWS." Physical and environmental controls (data-center perimeter, power, cooling, media destruction) are the canonical example. The customer cannot configure these and gets them by default.
- **Shared controls** — controls that apply to "both the infrastructure layer and customer layers, but in completely separate contexts or perspectives." Examples:
  - **Patch management** — AWS patches infrastructure; customer patches guest OS on EC2.
  - **Configuration management** — AWS configures infrastructure devices; customer configures guest OS, databases, and applications.
  - **Awareness and training** — AWS trains AWS employees; customer trains its own employees.
- **Customer-specific controls** — "Controls which are solely the responsibility of the customer based on the application they are deploying within AWS services." Examples: service-/communications-protection requirements, zone-of-trust definitions, and any controls scoped only to the workload's specific risk model.

## Practical Implications by Pillar

### Security pillar

The model dictates *where* security investment goes. On EC2 fleets, expect to fund OS hardening, vulnerability scanning, EDR, and patch management. On Lambda/S3/DynamoDB, that budget redirects to **IAM least-privilege**, **resource policies**, **KMS key management**, **data classification**, and **detection coverage** — there is no host to patch. Use Amazon Inspector for the layers that remain (Lambda code, container images), and accept that for fully-abstracted services your detection signal comes from CloudTrail and resource policies, not host telemetry.

### Reliability pillar

Customers inherit **AZ-level fault isolation** from AWS but remain responsible for multi-AZ deployment topology, backup strategy, RPO/RTO design, and runbooks. AWS provides durable primitives (S3 11 nines, DynamoDB global tables, Aurora Multi-AZ); the customer must architect *with* them. The reliability of an EC2-based system is largely a customer concern; the reliability of a Lambda + DynamoDB system is largely AWS's concern at the infrastructure layer, with the customer focused on idempotency, retries, and dependency management.

### Sustainability pillar

AWS owns data-center efficiency (PUE, renewable energy, cooling). The customer owns **workload efficiency**: right-sizing, Graviton adoption, serverless vs. always-on compute, storage tiering, and decommissioning idle resources. Inherited carbon savings come from AWS Region selection and AWS's renewables roadmap; *in-cloud* carbon savings come from architectural choices that maximize utilization and minimize idle infrastructure.

### Cost & Operational Excellence

Service category choice is itself a responsibility-shifting lever — moving from EC2 → Fargate → Lambda transfers operational toil to AWS at the price of less low-level control. This trade-off is explicit in COST04 (decommissioning), COST05 (cost when selecting services), and OPS principle "Use managed services". The more abstracted the service, the less of your ops team's time is spent on undifferentiated heavy lifting.

## The unifying takeaway

**The more abstracted the service, the less surface the customer must secure and operate — but the more critical the IAM and data-layer controls become, because they are all that remains.**

When choosing between IaaS, managed, and abstracted services, weigh:
- How much of the responsibility line you *want* to own (control vs. operational burden)
- Where your team's skill and headcount are best applied
- The compliance surface (some regulations expect specific control evidence that abstracted services hide)

## References

- https://aws.amazon.com/compliance/shared-responsibility-model/
- https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
- https://aws.amazon.com/compliance/shared-responsibility-model/aws-and-customer/
