# Kiro Modernization Discovery

A toolkit for running comprehensive, read-only codebase audits using [Kiro IDE](https://kiro.dev) custom subagents. Five specialized AI agents work in parallel to analyze a codebase's technology stack, architecture, code quality, security posture, and modernization opportunities — producing structured markdown reports without modifying any source code.

## What's Included

| Path | Description |
|------|-------------|
| `kiro-codebase-audit-prompt.md` | The main audit prompt. Paste into Kiro chat to kick off an audit. Orchestrates all five agents across three phases and produces the final consolidated report. |
| `.kiro/agents/tech-scanner.md` | Inventories languages, frameworks, dependencies, build tools, CI/CD, and infrastructure-as-code |
| `.kiro/agents/architecture-analyst.md` | Maps entry points, component relationships, data flows, external integrations, and produces Mermaid diagrams |
| `.kiro/agents/quality-auditor.md` | Assesses code complexity, code smells, test coverage, documentation state, and technical debt |
| `.kiro/agents/security-reviewer.md` | Identifies auth weaknesses, input validation gaps, hardcoded secrets, dependency CVEs, and supply chain risks |
| `.kiro/agents/modernization-strategist.md` | Synthesizes all findings into bounded contexts, service separation recommendations, and a phased roadmap |

## Quick Start

1. Clone this repo into the root of the project you want to audit (or copy the `.kiro/agents/` folder and `kiro-codebase-audit-prompt.md` into your project)
2. Open the project in Kiro IDE
3. Select **Claude Opus 4.6** from the model picker
4. Paste the contents of `kiro-codebase-audit-prompt.md` into Kiro chat
5. Reports are written to `./reports/` — the final output is `./reports/CODEBASE-AUDIT-REPORT.md`

No setup scripts required — the agents are ready to use as-is.

## Agents

| Agent | Role |
|-------|------|
| **tech-scanner** | Inventories languages, frameworks, dependencies, build tools, CI/CD, and infrastructure-as-code |
| **architecture-analyst** | Maps entry points, component relationships, data flows, external integrations, and produces Mermaid diagrams |
| **quality-auditor** | Assesses code complexity, code smells, test coverage, documentation state, and technical debt |
| **security-reviewer** | Identifies auth weaknesses, input validation gaps, hardcoded secrets, dependency CVEs, and supply chain risks |
| **modernization-strategist** | Synthesizes all findings into bounded contexts, service separation recommendations, and a phased roadmap |

## Output Structure

```
reports/
├── intermediate/
│   ├── 01-technology-inventory.md
│   ├── 02-architecture-analysis.md
│   ├── 03-quality-audit.md
│   ├── 04-security-review.md
│   └── 05-modernization-strategy.md
└── CODEBASE-AUDIT-REPORT.md
```

## License

This project is provided as-is for internal use.