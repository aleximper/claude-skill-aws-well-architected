# AWS Well-Architected Lenses Catalog

## Lenses Overview

In the AWS Well-Architected Tool, a **lens** is a way to consistently measure your architectures against best practices and identify areas for improvement. Each lens has its own set of questions, best practices, notes, and improvement plan that complement the six pillars of the core AWS Well-Architected Framework (Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainability). The Framework Lens is automatically applied to every workload defined in the WA Tool; additional lenses are layered on top to reflect technology- or industry-specific concerns that the general framework does not cover in depth.

You apply a lens **in addition to** — not instead of — the core six pillars whenever a workload is dominated by a specialized technology pattern (serverless, ML, streaming) or operates inside a regulated/specialized industry (financial services, healthcare, government, SAP). AWS distinguishes two kinds: **AWS-published lenses** (the Lens Catalog), which are authored and maintained by AWS, available to all WA Tool users, and represent official AWS guidance; and **Custom Lenses**, which customers and partners create themselves to encode internal standards. A workload can have up to 20 lenses applied total, with up to 5 added per operation.

## Lens Catalog — Current AWS-Published Lenses

### Serverless Applications Lens
- Domain: serverless workloads (RESTful microservices, mobile/web backends, stream processing)
- Adds: best practices for building serverless workloads on AWS, Lambda/API Gateway/EventBridge patterns
- URL: https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/welcome.html

### SaaS Lens
- Domain: independent software vendors and SaaS providers
- Adds: guidance for designing, deploying, and architecting multi-tenant SaaS workloads on AWS
- URL: https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/welcome.html

### Machine Learning Lens
- Domain: data scientists, ML engineers, MLOps teams
- Adds: best practices for managing Machine Learning resources and workloads across the ML lifecycle on AWS
- URL: https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html

### Generative AI Lens
- Domain: teams building generative AI applications (foundation models, RAG, agents)
- Adds: best practices for architecting generative AI workloads on AWS — newest lens in the catalog
- URL: https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html

### Data Analytics Lens
- Domain: analytics, data warehousing, data lake practitioners
- Adds: insights from real-world case studies and key design elements for Well-Architected analytics workloads
- URL: https://docs.aws.amazon.com/wellarchitected/latest/analytics-lens/analytics-lens.html

### IoT Lens
- Domain: Internet of Things device fleets and edge workloads
- Adds: best practices for managing IoT workloads in AWS, covering device, connectivity, and ingestion layers
- URL: https://docs.aws.amazon.com/wellarchitected/latest/iot-lens/welcome.html

### HPC Lens (High Performance Computing)
- Domain: tightly/loosely coupled HPC, scientific computing, simulation
- Adds: best practices for distributed HPC workloads, schedulers, parallel filesystems, and elastic clusters
- URL: https://docs.aws.amazon.com/wellarchitected/latest/high-performance-computing-lens/welcome.html

### SAP Lens
- Domain: SAP customers running S/4HANA, ECC, BW, and surrounding SAP estates
- Adds: design principles and best practices for SAP workloads in the AWS Cloud
- URL: https://docs.aws.amazon.com/wellarchitected/latest/sap-lens/sap-lens.html

### Streaming Media Lens
- Domain: live and on-demand video, OTT, broadcast workflows
- Adds: best practices for ingest, processing, packaging, and delivery of streaming media on AWS
- URL: https://docs.aws.amazon.com/wellarchitected/latest/streaming-media-lens/streaming-media-lens.html

### Games Industry Lens
- Domain: game studios, publishers, live-ops teams
- Adds: best practices for game backends, matchmaking, live ops, and player data on AWS
- URL: https://docs.aws.amazon.com/wellarchitected/latest/games-industry-lens/games-industry-lens.html

### Hybrid Networking Lens
- Domain: enterprises with on-prem + cloud + multi-region connectivity
- Adds: best practices for hybrid network architectures (Direct Connect, Transit Gateway, Cloud WAN)
- URL: https://docs.aws.amazon.com/wellarchitected/latest/hybrid-networking-lens/hybrid-networking-lens.html

### Financial Services Industry Lens
- Domain: banks, capital markets, insurance, fintech
- Adds: best practices for architecting Financial Services Industry workloads on AWS, with regulatory considerations
- URL: https://docs.aws.amazon.com/wellarchitected/latest/financial-services-industry-lens/financial-services-industry-lens.html

### Mergers and Acquisitions Lens
- Domain: M&A integration, divestiture, carve-out teams
- Adds: best practices for workload integration and migration to the cloud during mergers and acquisitions
- URL: https://docs.aws.amazon.com/wellarchitected/latest/mergers-and-acquisitions-lens/mergers-and-acquisitions-lens.html

### Migration Lens
- Domain: cloud migration programs (assess, mobilize, migrate & modernize)
- Adds: best practices for how to migrate to the AWS Cloud across the full migration lifecycle
- URL: https://docs.aws.amazon.com/wellarchitected/latest/migration-lens/migration-lens.html

### Connected Mobility Lens
- Domain: automotive, OEMs, fleet, connected vehicle platforms
- Adds: best practices for integrating technology into transportation systems and enhancing the mobility experience
- URL: https://docs.aws.amazon.com/wellarchitected/latest/connected-mobility-lens/connected-mobility-lens.html

### DevOps Lens (DevOps Guidance)
- Domain: platform engineering, SRE, DevOps organizations
- Adds: structured approach for cultivating a high-velocity, security-focused culture using modern DevOps practices
- URL: https://docs.aws.amazon.com/wellarchitected/latest/devops-guidance/devops-guidance.html

### Government Lens
- Domain: federal, state, local government and public sector services
- Adds: best practices for designing and delivering government services on AWS
- URL: https://docs.aws.amazon.com/wellarchitected/latest/government-lens/government-lens.html

### Healthcare Industry Lens
- Domain: providers, payers, life sciences, HIPAA-regulated workloads
- Adds: best practices and guidance for designing, deploying, and managing healthcare workloads in the AWS Cloud
- URL: https://docs.aws.amazon.com/wellarchitected/latest/healthcare-industry-lens/healthcare-industry-lens.html

### Container Build Lens
- Domain: container platform engineering teams
- Adds: best practices on the container design and build process (image hardening, supply chain, registries)
- URL: https://docs.aws.amazon.com/wellarchitected/latest/container-build-lens/container-build-lens.html

## Choosing which lens(es) to apply

Use the table below to match a workload pattern to its lens. Multiple lenses can (and often should) coexist on the same workload.

| Workload pattern | Recommended lens(es) |
|---|---|
| Lambda + API Gateway + DynamoDB app | Serverless Applications Lens |
| Multi-tenant B2B SaaS | SaaS Lens (+ Serverless if applicable) |
| Training/serving ML models | Machine Learning Lens (+ Generative AI if LLMs/RAG) |
| LLM-based assistant, RAG, agentic apps | Generative AI Lens (+ ML Lens for training side) |
| Lakehouse, ETL, BI on AWS | Data Analytics Lens |
| Connected device fleet | IoT Lens (+ Connected Mobility for vehicles) |
| Scientific simulation, big-CPU/GPU jobs | HPC Lens |
| S/4HANA, BW, ECC | SAP Lens |
| OTT, live broadcast, VOD | Streaming Media Lens |
| Game backend / matchmaking | Games Industry Lens |
| On-prem ↔ AWS hybrid networking | Hybrid Networking Lens |
| Bank, insurance, capital markets | Financial Services Industry Lens |
| Carve-out / divestiture / M&A | Mergers and Acquisitions Lens |
| Lift-shift-modernize migration | Migration Lens |
| Container platform / EKS / ECR pipelines | Container Build Lens |
| Public sector / regulatory baseline | Government Lens |
| HIPAA / patient data | Healthcare Industry Lens |
| Platform/SRE practice | DevOps Lens (DevOps Guidance) |

## Custom Lenses

Beyond the official catalog, the AWS Well-Architected Tool lets organizations define **Custom Lenses** to encode their own internal standards — proprietary security baselines, platform conventions, regulatory checklists, or partner-specific patterns. A custom lens is authored as a JSON template with user-defined pillars, questions, best practices, risk rules, and improvement-plan content; it is then uploaded to the WA Tool, versioned, and applied to workloads exactly like an AWS-published lens. Custom lenses can be **shared across AWS accounts** (including AWS Organizations), enabling central platform teams to roll out a single review standard to every workload owner. Data captured against a removed lens is retained and restored if the lens is reapplied.

## References

- https://docs.aws.amazon.com/wellarchitected/latest/userguide/lenses.html
- https://aws.amazon.com/architecture/well-architected/lenses/
- https://docs.aws.amazon.com/wellarchitected/latest/userguide/lenses-custom.html
