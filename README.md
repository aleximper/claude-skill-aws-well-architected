# Claude Code Skill — AWS Well-Architected Framework

A skill for [Claude Code](https://claude.com/claude-code) that gives Claude a complete, structured reference to the **AWS Well-Architected Framework**: the 6 pillars, the design principles, the Shared Responsibility Model, the lenses catalog, and the Well-Architected Review (WAR) process.

Use it whenever you are designing, reviewing, or optimizing any workload on AWS.

## What it contains

```
aws-well-architected/
├── SKILL.md                                 Lightweight entry point (index + decision matrix)
└── references/
    ├── 01-design-principles.md              Cross-pillar General Design Principles
    ├── 02-shared-responsibility.md          Shared Responsibility Model
    ├── 03-operational-excellence.md         OPS pillar (OPS01–OPS11)
    ├── 04-security.md                       SEC pillar (SEC01–SEC11)
    ├── 05-reliability.md                    REL pillar (REL01–REL13) + RTO/RPO + DR strategies
    ├── 06-performance-efficiency.md         PERF pillar (PERF01–PERF05)
    ├── 07-cost-optimization.md              COST pillar (COST01–COST11) + pricing models cheatsheet
    ├── 08-sustainability.md                 SUS pillar (SUS01–SUS06)
    ├── 09-lenses-catalog.md                 19 official AWS lenses (Serverless, SaaS, ML, GenAI, FSI…)
    └── 10-wa-tool-and-review.md             WA Tool + WAR process + Nov 2024 refresh
```

Each pillar reference file contains the official AWS definition, the design principles, the best practice areas with their question codes (e.g. `OPS01..OPS11`, `SEC01..SEC11`, `REL01..REL13`), the best practices per question, the key AWS services, the most common anti-patterns, a 12–15 item review checklist, and direct URLs to the official documentation.

The content reflects the **official refresh of November 6, 2024** (100% of OPS, SEC, PERF, COST, SUS and ~79% of REL updated).

> The skill content is intentionally in English: it matches AWS's canonical terminology, preserves the exact names of principles and BPs, and improves keyword matching when Claude decides to load it.

## Installation

### Global (recommended)

Install it once and have it available across every Claude Code session:

```bash
git clone https://github.com/aleximper/claude-skill-aws-well-architected.git \
  ~/.claude/skills/aws-well-architected
```

To update later:

```bash
cd ~/.claude/skills/aws-well-architected && git pull
```

### Per project

If you prefer to keep it scoped to a specific repo:

```bash
git clone https://github.com/aleximper/claude-skill-aws-well-architected.git \
  .claude/skills/aws-well-architected
```

## How it activates

Claude loads the skill automatically whenever the conversation involves AWS architecture review, Well-Architected Reviews, the six pillars, AWS best practices, HRIs/MRIs, or AWS architecture trade-offs. You can also invoke it explicitly with `/aws-well-architected` (depending on your Claude Code version).

`SKILL.md` is the lightweight entry point loaded into context. It works as an index for the deeper files in `references/` — Claude reads only what is relevant to keep the context window small.

## Example prompts that trigger the skill

- "Review this Terraform stack against the AWS Well-Architected Framework."
- "I'm designing a new multi-tenant SaaS on AWS — which lenses should I apply and what does the SEC pillar require?"
- "Walk me through a Well-Architected Review for a Lambda + DynamoDB workload."
- "What's the difference between Pilot Light and Warm Standby as DR strategies?"
- "Identify HRIs in my current EC2 + RDS architecture from the Reliability pillar's perspective."

## Sources and disclaimer

All content is distilled from the official AWS documentation. The canonical, always up-to-date source remains the AWS docs themselves:

- Framework: <https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html>
- Lens Catalog: <https://aws.amazon.com/architecture/well-architected/lenses/>
- WA Tool: <https://aws.amazon.com/well-architected-tool/>

Each file under `references/` ends with a `## References` section pointing to the official pages it summarizes. When in doubt, validate against the live AWS documentation — the framework evolves continuously.

This project is **not affiliated with, endorsed by, or sponsored by Amazon Web Services**. AWS, the Powered by AWS logo, and all AWS service names are trademarks of Amazon.com, Inc. or its affiliates.

## Contributing

Issues and PRs are welcome. Especially helpful contributions:

- Updates whenever AWS publishes a framework refresh
- New lenses added to the AWS Lens Catalog
- Corrections to BP IDs or AWS documentation URLs that have changed
- Translations to other languages

## License

[MIT](LICENSE) © 2026 Jhon Ortiz
