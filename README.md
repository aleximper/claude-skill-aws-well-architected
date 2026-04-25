# Claude Code Skill — AWS Well-Architected Framework

A [Claude Code](https://claude.com/claude-code) skill that gives Claude a complete, structured reference of the **AWS Well-Architected Framework** — six pillars, design principles, lenses catalog, and the Well-Architected Review (WAR) process.

Use it when designing, reviewing, or optimizing any AWS workload.

## What's inside

```
aws-well-architected/
├── SKILL.md                                 Lean entry point (index, decision matrix)
└── references/
    ├── 01-design-principles.md              Cross-pillar General Design Principles
    ├── 02-shared-responsibility.md          Shared Responsibility Model
    ├── 03-operational-excellence.md         OPS pillar (OPS01–OPS11)
    ├── 04-security.md                       SEC pillar (SEC01–SEC11)
    ├── 05-reliability.md                    REL pillar (REL01–REL13) + RTO/RPO + DR strategies
    ├── 06-performance-efficiency.md         PERF pillar (PERF01–PERF05)
    ├── 07-cost-optimization.md              COST pillar (COST01–COST11) + pricing-models cheatsheet
    ├── 08-sustainability.md                 SUS pillar (SUS01–SUS06)
    ├── 09-lenses-catalog.md                 19 official AWS lenses (Serverless, SaaS, ML, GenAI, FSI, ...)
    └── 10-wa-tool-and-review.md             WA Tool + WAR process + Nov 2024 refresh
```

Each pillar reference contains AWS's official definition, design principles, best practice areas with question codes (e.g., `OPS01..OPS11`, `SEC01..SEC11`, `REL01..REL13`), best-practice bullets per question, key AWS services, common anti-patterns, a 12–15 item review checklist, and direct AWS doc URLs.

The content reflects the **November 6, 2024 framework refresh** (100% of OPS, SEC, PERF, COST, SUS plus ~79% of REL pillar best practices updated).

## Installation

### Global (recommended)

Install once, available in every Claude Code session:

```bash
git clone https://github.com/aleximper/claude-skill-aws-well-architected.git \
  ~/.claude/skills/aws-well-architected
```

To update later:

```bash
cd ~/.claude/skills/aws-well-architected && git pull
```

### Per-project

```bash
git clone https://github.com/aleximper/claude-skill-aws-well-architected.git \
  .claude/skills/aws-well-architected
```

## How it triggers

Claude auto-loads this skill when the conversation involves AWS architecture review, Well-Architected reviews, the six pillars, AWS best practices, HRIs/MRIs, or AWS architecture trade-offs. You can also invoke it explicitly with `/aws-well-architected` (depending on your Claude Code version).

`SKILL.md` is the lean entry point that gets loaded into context. It indexes the deeper reference files — Claude reads only what's relevant to the current task to keep the context window small.

## Example prompts that activate the skill

- "Review this Terraform stack against the AWS Well-Architected Framework."
- "I'm designing a new multi-tenant SaaS on AWS — which lenses should I apply and what does the SEC pillar require?"
- "Walk me through a Well-Architected Review for a Lambda + DynamoDB workload."
- "What's the difference between Pilot Light and Warm Standby DR strategies?"
- "Identify HRIs in my current EC2 + RDS architecture from a Reliability perspective."

## Sources & disclaimer

All content is distilled from AWS's official documentation. The canonical, always-current source remains the AWS docs:

- Framework: <https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html>
- Lens Catalog: <https://aws.amazon.com/architecture/well-architected/lenses/>
- WA Tool: <https://aws.amazon.com/well-architected-tool/>

Each reference file in `references/` ends with a `## References` section pointing to the exact AWS pages it summarizes. When in doubt, check live AWS docs — the framework evolves continuously.

This project is **not affiliated with, endorsed by, or sponsored by Amazon Web Services**. AWS, the Powered by AWS logo, and all AWS service names are trademarks of Amazon.com, Inc. or its affiliates.

## Contributing

Issues and PRs welcome. Particularly useful contributions:

- Updates when AWS publishes a framework refresh
- New lenses added to the AWS Lens Catalog
- Corrections to BP IDs or AWS doc URLs that have moved
- Translations

## License

[MIT](LICENSE) © 2026 Jhon Ortiz
