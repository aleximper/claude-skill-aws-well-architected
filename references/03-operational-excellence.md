# AWS Well-Architected Framework — Operational Excellence Pillar

## Definition

The Operational Excellence pillar is "a commitment to build software correctly while consistently delivering a great customer experience. The operational excellence pillar contains best practices for organizing your team, designing your workload, operating it at scale, and evolving it over time." Its goal is to get new features and bug fixes into customers' hands quickly and reliably, while continuously driving toward CI/CD. Organizations that invest in operational excellence build architectures that provide insight into their status, are activated for effective and efficient operation and event response, and continue to improve and support evolving business goals. (Pillar refresh published November 6, 2024.)

## Design Principles

1. **Organize teams around business outcomes** — The ability of a team to achieve business outcomes comes from leadership vision, effective operations, and a business-aligned operating model. Long-term vision is translated into goals and operational KPIs that are aligned at all levels and communicated across the enterprise.
2. **Implement observability for actionable insights** — Gain a comprehensive understanding of workload behavior, performance, reliability, cost, and health. Establish KPIs and leverage observability telemetry to make informed decisions and act promptly when business outcomes are at risk.
3. **Safely automate where possible** — Define your entire workload and its operations as code and automate operations in response to events. Employ automation safety via guardrails, rate control, error thresholds, and approvals to limit human error and reduce operator toil.
4. **Make frequent, small, reversible changes** — Design workloads that are scalable and loosely coupled so components can be updated regularly. Smaller, incremental, automated deployments reduce blast radius and enable faster reversal when failures occur.
5. **Refine operations procedures frequently** — As workloads evolve, evolve operations appropriately. Hold regular reviews to validate procedures are effective, update them where gaps exist, communicate updates, and gamify operations to share best practices.
6. **Anticipate failure** — Drive failure scenarios (pre-mortems, game days) to understand the workload's risk profile and its impact on business outcomes. Test the effectiveness of procedures and team response, and make informed decisions about open risks.
7. **Learn from all operational events and metrics** — Drive improvement through lessons learned from all operational events and failures. Share learnings across teams and the entire organization, highlighting how operations contribute to business outcomes.
8. **Use managed services** — Reduce operational burden by using AWS managed services where possible, and build operational procedures around interactions with those services.

## Best Practice Areas

The pillar is structured around four areas containing eleven questions (OPS 1 – OPS 11).

### Organization

Covers leadership, shared understanding of priorities, the operating model that shapes how teams work together, and the culture that supports team members so they can act effectively. Question codes: **OPS01–OPS03**.

**OPS 1: How do you determine what your priorities are?**
- OPS01-BP01 Evaluate external customer needs (involve key stakeholders to determine where to focus).
- OPS01-BP02 Evaluate internal customer needs across business, dev, and ops teams.
- OPS01-BP03 Evaluate governance requirements imposed by your organization.
- OPS01-BP04 Evaluate compliance requirements (regulatory, industry standards) and have mechanisms to detect changes.
- OPS01-BP05 Evaluate threat landscape (risks, liabilities, infosec threats) and maintain a risk registry.
- OPS01-BP06 Evaluate trade-offs while managing benefits and risks when choosing between competing priorities.

**OPS 2: How do you structure your organization to support your business outcomes?**
- OPS02-BP01 Resources have identified owners.
- OPS02-BP02 Processes and procedures have identified owners.
- OPS02-BP03 Operations activities have identified owners responsible for their performance.
- OPS02-BP04 Mechanisms exist to manage responsibilities and ownership.
- OPS02-BP05 Mechanisms exist to request additions, changes, and exceptions (so innovation is not constrained).
- OPS02-BP06 Responsibilities between teams are predefined or negotiated via team agreements.

**OPS 3: How does your organizational culture support your business outcomes?**
- OPS03-BP01 Provide executive sponsorship — engaged senior leadership sets expectations and measures success.
- OPS03-BP02 Team members are empowered to take action when outcomes are at risk.
- OPS03-BP03 Escalation is encouraged so risks reach decision makers in time.
- OPS03-BP04 Communications are timely, clear, and actionable for known risks and planned events.
- OPS03-BP05 Experimentation is encouraged to accelerate learning and engagement.
- OPS03-BP06 Team members are encouraged to maintain and grow their skill sets with dedicated structured time for learning.
- OPS03-BP07 Resource teams appropriately so they have the tools and people to scale.

### Prepare

Covers designing for observability, designing for operations (CI/CD, version control, environments), mitigating deployment risks, and validating operational readiness before changes go live. Question codes: **OPS04–OPS07**.

**OPS 4: How do you implement observability in your workload?**
- OPS04-BP01 Identify key performance indicators that align monitoring with business objectives.
- OPS04-BP02 Implement application telemetry (metrics, logs, events).
- OPS04-BP03 Implement user experience telemetry to capture real customer impact.
- OPS04-BP04 Implement dependency telemetry across upstream/downstream services.
- OPS04-BP05 Implement distributed tracing to follow requests end-to-end.

**OPS 5: How do you reduce defects, ease remediation, and improve flow into production?**
- OPS05-BP01 Use version control for code, configuration, and infrastructure.
- OPS05-BP02 Test and validate changes before promoting them.
- OPS05-BP03 Use configuration management systems to enforce desired state.
- OPS05-BP04 Use build and deployment management systems (pipelines).
- OPS05-BP05 Perform patch management consistently and on a schedule.
- OPS05-BP06 Share design standards across teams.
- OPS05-BP07 Implement practices to improve code quality (reviews, static analysis, linting).
- OPS05-BP08 Use multiple environments (sandbox, dev, test, prod) with increasing controls.
- OPS05-BP09 Make frequent, small, reversible changes.
- OPS05-BP10 Fully automate integration and deployment.

**OPS 6: How do you mitigate deployment risks?**
- OPS06-BP01 Plan for unsuccessful changes (rollback strategy, fallback plans).
- OPS06-BP02 Test deployments (in pre-production with realistic traffic).
- OPS06-BP03 Employ safe deployment strategies (canary, blue/green, feature flags).
- OPS06-BP04 Automate testing and rollback so recovery is fast and human-error-free.

**OPS 7: How do you know that you are ready to support a workload?**
- OPS07-BP01 Ensure personnel capability (training, on-call coverage, runbook familiarity).
- OPS07-BP02 Ensure a consistent review of operational readiness (ORR checklists).
- OPS07-BP03 Use runbooks to perform routine procedures.
- OPS07-BP04 Use playbooks to investigate issues.
- OPS07-BP05 Make informed decisions to deploy systems and changes (risk-based go/no-go).
- OPS07-BP06 Create support plans for production workloads (AWS Business or Enterprise Support).

### Operate

Covers using telemetry to understand workload health, measuring operations health and KPIs, and managing planned and unplanned events including incident response. Question codes: **OPS08–OPS10**.

**OPS 8: How do you utilize workload observability in your organization?**
- OPS08-BP01 Analyze workload metrics against baselines and thresholds.
- OPS08-BP02 Analyze workload logs (centralized, searchable, with retention policies).
- OPS08-BP03 Analyze workload traces to pinpoint latency and errors.
- OPS08-BP04 Create actionable alerts (no noise, every alert maps to a process).
- OPS08-BP05 Create dashboards tailored to business, workload, and operations audiences.

**OPS 9: How do you understand the health of your operations?**
- OPS09-BP01 Measure operations goals and KPIs with metrics (deployment frequency, MTTR, change failure rate, lead time).
- OPS09-BP02 Communicate status and trends to ensure visibility into operations.
- OPS09-BP03 Review operations metrics and prioritize improvement actions accordingly.

**OPS 10: How do you manage workload and operations events?**
- OPS10-BP01 Use a process for event, incident, and problem management (ITIL-style separation).
- OPS10-BP02 Have a process per alert with a named owner.
- OPS10-BP03 Prioritize operational events based on business impact.
- OPS10-BP04 Define escalation paths with named decision makers.
- OPS10-BP05 Define a customer communication plan for service-impacting events.
- OPS10-BP06 Communicate status through dashboards.
- OPS10-BP07 Automate responses to events (auto-remediation, scripted runbooks).

### Evolve

Covers continuous improvement, post-incident analysis, knowledge management, and feedback loops that turn operational learnings into systemic change. Question code: **OPS11**.

**OPS 11: How do you evolve operations?**
- OPS11-BP01 Have a process for continuous improvement.
- OPS11-BP02 Perform post-incident analysis on all customer-impacting events.
- OPS11-BP03 Implement feedback loops within procedures to capture learnings rapidly.
- OPS11-BP04 Perform knowledge management so insights are findable and reusable.
- OPS11-BP05 Define drivers for improvement based on data and feedback.
- OPS11-BP06 Validate insights before acting on them (avoid acting on noise).
- OPS11-BP07 Perform operations metrics reviews on a regular cadence.
- OPS11-BP08 Document and share lessons learned across teams.
- OPS11-BP09 Allocate time to make improvements (dedicated work cycles, not best effort).

## Key AWS Services

- **CI/CD and deployment**: AWS CodePipeline, AWS CodeBuild, AWS CodeDeploy, AWS CodeArtifact, AWS CodeCommit, Amazon CodeCatalyst.
- **Infrastructure as Code (IaC)**: AWS CloudFormation, AWS CDK, AWS SAM, AWS Service Catalog.
- **Observability — metrics, logs, traces, dashboards**: Amazon CloudWatch (Metrics, Logs, Logs Insights, Synthetics, RUM, Evidently, Application Signals), AWS X-Ray, Amazon Managed Grafana, Amazon Managed Service for Prometheus, Amazon OpenSearch Service.
- **Audit and config**: AWS CloudTrail, AWS Config, AWS Audit Manager, VPC Flow Logs.
- **Operations automation and runbooks**: AWS Systems Manager (Run Command, State Manager, Patch Manager, Automation, OpsCenter, Incident Manager, Change Manager, Parameter Store), AWS Lambda, Amazon EventBridge, AWS Step Functions, AWS Chatbot.
- **Governance and multi-account**: AWS Organizations, AWS Control Tower, AWS Service Catalog, AWS IAM Identity Center, AWS Resource Groups and Tag Editor.
- **Operational tooling and analytics**: AWS Trusted Advisor, AWS Health, AWS Well-Architected Tool, AWS Resilience Hub, AWS Fault Injection Service, AWS Glue + Amazon Athena + Amazon QuickSight (operational data analytics), Amazon DevOps Guru.
- **Support**: AWS Support (Business / Enterprise plans), AWS IQ, AWS Managed Services (AMS), AWS Professional Services / Partners.

## Common Anti-patterns

- **Operations-as-a-silo**: an "ops team" disconnected from product/dev teams, with no shared goals or KPIs, no executive sponsorship, and no two-pizza-team ownership of services.
- **Click-ops infrastructure**: resources created by hand in the console, no IaC, no version control, "snowflake" environments where dev does not match prod.
- **Monitoring without observability**: a dashboard of CPU/memory but no business KPIs, no distributed tracing, no user-experience telemetry, and alerts that nobody owns.
- **Big-bang deployments**: infrequent, large, manual releases with no canary, no automated rollback, no feature flags, and no plan for unsuccessful changes.
- **No runbooks or playbooks**: incident response improvised every time, knowledge in one engineer's head, no post-incident analysis, no documented escalation paths.
- **Alert fatigue**: high-volume, low-signal alerts; alerts not mapped to a process; severities not aligned to business impact; no on-call rotation.
- **Skipping operational readiness reviews**: workloads go to production with no ORR checklist, no support plan, no defined owner, no game day, no patch management strategy.
- **No feedback loop**: incidents recur because lessons learned are not captured, shared, or scheduled into the backlog; no dedicated capacity for improvement work.

## Review Checklist

1. Are workload priorities documented and reviewed regularly against external customer, internal, governance, compliance, and threat-landscape inputs?
2. Does every resource, process, and operations activity have a named owner accessible in a discoverable system?
3. Is there explicit executive sponsorship for operational excellence, and are team members empowered to act and escalate when outcomes are at risk?
4. Are KPIs defined that link workload telemetry to business outcomes (not just infrastructure metrics)?
5. Is application, user-experience, dependency, and distributed-tracing telemetry implemented and centrally queryable?
6. Are all changes (application, infrastructure, configuration) under version control and deployed via an automated pipeline with tests and gates?
7. Are deployments small, frequent, and reversible, using canary/blue-green/feature-flag strategies with automated rollback?
8. Is there a documented Operational Readiness Review (ORR) process executed before workloads or major changes go live?
9. Do production workloads have runbooks for routine activities, playbooks for investigations, and an appropriate AWS Support plan?
10. Does every alert have a named owner and a documented response process, and are alerts prioritized by business impact?
11. Are escalation paths and a customer-communication plan for service-impacting events defined and rehearsed?
12. Are post-incident analyses performed on all customer-impacting events, with contributing factors documented and preventive actions tracked to closure?
13. Are lessons learned, runbooks, and playbooks managed as living knowledge (knowledge management) and shared across teams?
14. Is dedicated capacity (time, budget, headcount) allocated for continuous improvement work in every planning cycle?
15. Are game days / failure injection exercises run on a regular cadence to validate procedures, on-call readiness, and the workload's risk profile?

## References

- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/welcome.html
- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/operational-excellence.html
- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/design-principles.html
- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/definition.html
- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/organization.html
- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/prepare.html
- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/operate.html
- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/evolve.html
