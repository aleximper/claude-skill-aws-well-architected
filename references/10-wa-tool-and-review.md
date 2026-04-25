# AWS Well-Architected Tool & Review Process

## Section 1 — AWS Well-Architected Tool

The **AWS Well-Architected Tool (AWS WA Tool)** is a free service in the AWS Management Console that, in AWS's own words, "provides a consistent process for measuring your architecture using AWS best practices." It assists you throughout the product lifecycle by helping document the decisions that you make, providing recommendations for improving your workload based on best practices, and guiding you in making your workloads more reliable, secure, efficient, and cost-effective. The service is intended for those involved in technical product development — chief technology officers (CTOs), architects, developers, and operations team members — who use it to document their architectures, provide product launch governance, and understand and manage the risks in their technology portfolio.

### Key concepts

- **Workload** — A collection of resources and code that delivers business value (e.g., a customer-facing application or a backend process). It is the unit of review in the WA Tool.
- **Milestone** — A point-in-time snapshot of a workload's review answers and risk profile, used to track progress over the architecture's evolution.
- **Lens** — A set of pillar questions for a specific perspective. The base lens is the **AWS Well-Architected Framework lens**; AWS also publishes domain lenses (Serverless, SaaS, Generative AI, Financial Services Industry, etc.) and supports **custom lenses**, which let you "measure your workload using your own best practices" and "tailor the questions in a custom lens to be specific to a particular technology or to help you meet the governance needs within your organization."
- **Profile** — Per the AWS docs, "you can create profiles to provide your business context, and identify goals you'd like to accomplish when performing a Well-Architected review. AWS Well-Architected Tool uses the information gathered from your profile to help you focus on a prioritized list of questions that are relevant to your business during the workload review. Attaching a profile to your workload also helps you see which risks are prioritized for you to address with your improvement plan."
- **Review template** — A reusable, pre-answered template (with shared notes, lenses, and tags) that lets organizations standardize how new workloads are reviewed.

### Defining a workload

When you define a workload in the WA Tool, you provide:

- **Name and description**
- **Owner / review owner**
- **Environment** — Production or pre-production
- **AWS Regions** (and/or non-AWS regions) where the workload runs
- **Account IDs** in scope
- **Industry / industry type** (optional, used by certain lenses)
- **Lenses applied** — at minimum the AWS Well-Architected Framework lens, plus any domain or custom lenses
- **Optional**: profile, review template, tags, application from AWS Service Catalog AppRegistry

### Output

After answering the lens questions, the tool produces:

- **High Risk Issues (HRIs)** — architectural and operational decisions likely to negatively impact the business.
- **Medium Risk Issues (MRIs)** — issues that may impact the business but with a lower likelihood or severity.
- An **improvement plan** that lists the recommended improvement items per question, with links to AWS documentation, whitepapers, and AWS Well-Architected Labs. Items can be assigned and tracked.

### Profiles, consolidated reports, and integrations

Profiles tailor the question set to **business priorities and risk appetite**, surfacing the prioritized risks first. The WA Tool also supports **consolidated reports** across multiple workloads (and across an organization via AWS Organizations integration), so a CTO or central architecture team can see HRI/MRI counts and trends across a portfolio.

Two integrations reduce manual effort during a review:

- **AWS Trusted Advisor** — When enabled, the WA Tool can use Trusted Advisor checks to help answer relevant best-practice questions, surfacing the underlying check results inside the question.
- **AWS Service Catalog AppRegistry** — Lets you link a workload definition to a registered application so resources, tags, and metadata are easy to discover.
- **AWS Support** — Trusted Advisor coverage depends on the support plan; richer checks require Business or Enterprise Support.

### Pricing

The AWS Well-Architected Tool itself is **free of charge**. You only pay for any AWS services consumed while remediating findings (and Trusted Advisor's full check set requires a paid Support plan).

---

## Section 2 — Conducting a Well-Architected Review (WAR)

A Well-Architected Review is a structured evaluation of a workload against the AWS Well-Architected Framework's six pillars: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, and Sustainability.

### When to perform a WAR

- **Design phase** — Before significant build effort, to validate architectural choices.
- **Pre-launch / pre-GA** — As a launch governance gate.
- **Post-incident** — To convert lessons learned into prioritized improvements.
- **Periodic** — Typically every **6–12 months**, or when the workload changes materially (re-platform, new region, major scale step).

### Step-by-step workflow

1. **Define the workload** in the WA Tool (name, environment, regions, accounts, owners).
2. **Apply lenses.** Always start with the **AWS Well-Architected Framework lens**, then add domain lenses (e.g., Serverless, SaaS, Generative AI, FSI) and custom/organizational lenses as relevant.
3. **Answer questions per pillar** with the right stakeholders in the room — workload owner, application developers, operations/SRE, security, finance/FinOps, data, and (if applicable) compliance.
4. **Identify HRIs and MRIs** as the answers are recorded; use the tool's notes field to capture context and evidence per question.
5. **Build an improvement plan** — convert HRIs/MRIs into improvement items with owners, target dates, and effort estimates; prioritize HRIs first and any items flagged by the attached profile.
6. **Save a milestone** at the end of the review to lock the snapshot, then re-review on a cadence and compare milestones to track progress.

### Roles in a WAR

- **Workload owner / product owner** — Owns scope and decisions.
- **Lead architect(s)** — Drive answers and trade-off discussions.
- **Security engineer** — Owns SEC pillar answers.
- **Operations / SRE** — Owns OPS and much of REL.
- **FinOps / cost owner** — Owns COST.
- **Performance / data engineer** — Owns PERF.
- **Sustainability lead** (where applicable) — Owns SUS.

### Delivery models

- **Self-service** — Team runs the review themselves in the WA Tool. Lowest cost, highest dependence on internal expertise.
- **AWS-led review** — Conducted with an AWS Solutions Architect, often free for qualifying customers; can include credits for remediation under Well-Architected programs.
- **Partner-led review** — Performed by an **AWS Well-Architected Partner**, who can issue qualifying reviews and (when eligible) pass through AWS credits for HRI remediation.

### Tip — Gather evidence before the review

Pre-stage data so answers are grounded, not guessed:

- **AWS CloudTrail** — Auditable history of API activity.
- **AWS Config** — Resource inventory and rule compliance.
- **AWS Security Hub / Amazon GuardDuty / Amazon Inspector** — Security findings.
- **AWS Trusted Advisor** — Best-practice checks (auto-populates some WA Tool answers).
- **Amazon CloudWatch / X-Ray** — Operational and observability evidence.
- **AWS Cost Explorer / AWS Budgets / AWS Compute Optimizer** — Cost and right-sizing evidence.

---

## Section 3 — Recent updates (2024–2026)

### November 6, 2024 framework refresh

Per the official **Document revisions** page of the AWS Well-Architected Framework, the November 6, 2024 release is described as a **Major update** in which "Best practices were updated with new guidance in Reliability, Security, Operational excellence, Sustainability, and Performance efficiency. The Reliability pillar received a large-scale refresh and update to many best practices. Guidance across Security and Operational excellence has been updated and refined with new service and generative AI suggestions. Sustainability received multiple updates based on AWS services and a new best practice."

Cumulatively across the 2023–2024 refresh cycle, AWS has reported that **100% of Operational Excellence, Security, Performance Efficiency, Cost Optimization, and Sustainability** pillar content has been refreshed at least once, with the Reliability pillar approaching ~79% coverage after the November 2024 large-scale refresh. (The June 27, 2024 entry is also catalogued as a Major update with new best practices in Security and Cost.)

### Notable wording / structural changes

- **OPS01-BP01** was renamed from "Evaluate customer needs" to **"Evaluate external customer needs"**, with a parallel best practice for internal customers — sharpening the distinction the framework draws between end-users and internal stakeholders.
- **Application Security (SEC11)** has been elevated and expanded with more prescriptive guidance on secure SDLC, dependency/supply-chain security, and code review automation.
- **Operational Excellence** added a Design Principle on **observability**.
- **Performance Efficiency** consolidated questions and added best practices on **efficient caching** and **optimizing hardware acceleration**.
- **Reliability** has been heavily refreshed around monitoring, failover, remediation, and limiting blast radius — including multi-Region-based resilience patterns.

### Lens Catalog additions

- **Generative AI Lens** — for designing, operating, and governing GenAI workloads.
- **Financial Services Industry (FSI) Lens** — sector-specific best practices for FSI workloads.
- **Mergers and Acquisitions Lens** — updated guidance for M&A integration.
- Continued maintenance of Serverless, SaaS, IoT, Machine Learning, Data Analytics, and Foundational Technical Review (FTR) lenses.

### 2025–2026 trends

Reflecting both the document revisions and the AWS Architecture blog cadence, recent and ongoing emphasis areas include:

- **Zero Trust** — identity-centric controls, fine-grained authorization, and continuous verification across SEC.
- **Observability** — promoted to a Design Principle in OPS, with deeper integration of CloudWatch, X-Ray, and OpenTelemetry-based patterns.
- **Generative AI workload patterns** — guidance for foundation-model selection, prompt/output safety, RAG architectures, evaluation, and cost control, surfaced both in the framework body and via the GenAI Lens.
- **Resilience at scale** — multi-Region active/active and active/passive patterns, AWS Resilience Hub integration, and chaos-engineering-informed verification.
- **FinOps maturity** — tighter coupling between Cost Optimization and Sustainability, with right-sizing, scheduling, and carbon-aware design as joint levers.

## References

- https://docs.aws.amazon.com/wellarchitected/latest/userguide/intro.html
- https://aws.amazon.com/well-architected-tool/
- https://docs.aws.amazon.com/wellarchitected/latest/userguide/profiles.html
- https://docs.aws.amazon.com/wellarchitected/latest/framework/document-revisions.html
- https://aws.amazon.com/blogs/architecture/announcing-updates-to-the-aws-well-architected-framework-guidance/
