# Kiro Modernization Discovery

A toolkit for running comprehensive, read-only codebase audits using [Kiro IDE](https://kiro.dev) custom subagents. Five specialized AI agents work in parallel to analyze a codebase's technology stack, architecture, code quality, security posture, and modernization opportunities — producing structured markdown reports without modifying any source code.

## What's Included

| File | Description |
|------|-------------|
| `kiro-codebase-audit-prompt.md` | The main audit prompt and full agent definitions. Contains the orchestration instructions for Kiro IDE (Phase 1: parallel discovery, Phase 2: research & strategy, Phase 3: final synthesis), the YAML frontmatter and prompt body for all five custom subagents, and the template for the final consolidated `CODEBASE-AUDIT-REPORT.md`. Use this as the reference document and paste the main prompt section into Kiro chat to kick off an audit. |
| `setup-kiro-audit-agents.sh` | Bash setup script. Run from the root of the project you want to audit. Creates `.kiro/agents/` and writes the five agent `.md` files (`tech-scanner`, `architecture-analyst`, `quality-auditor`, `security-reviewer`, `modernization-strategist`) so Kiro IDE can discover them. |
| `setup-kiro-audit-agents.ps1` | PowerShell equivalent of the setup script for Windows environments. Same functionality — creates `.kiro/agents/` and writes all five agent files. |

## Agents

| Agent | Role |
|-------|------|
| **tech-scanner** | Inventories languages, frameworks, dependencies, build tools, CI/CD, and infrastructure-as-code |
| **architecture-analyst** | Maps entry points, component relationships, data flows, external integrations, and produces Mermaid diagrams |
| **quality-auditor** | Assesses code complexity, code smells, test coverage, documentation state, and technical debt |
| **security-reviewer** | Identifies auth weaknesses, input validation gaps, hardcoded secrets, dependency CVEs, and supply chain risks |
| **modernization-strategist** | Synthesizes all findings into bounded contexts, service separation recommendations, and a phased roadmap |

## Quick Start

1. Clone this repo
2. `cd` into the project you want to audit
3. Run the setup script:
   ```bash
   # macOS / Linux
   bash /path/to/setup-kiro-audit-agents.sh

   # Windows PowerShell
   .\setup-kiro-audit-agents.ps1
   ```
4. Open the project in Kiro IDE
5. Select **Claude Opus 4.6** from the model picker
6. Paste the main prompt from `kiro-codebase-audit-prompt.md` into Kiro chat
7. Reports are written to `./reports/` — the final output is `./reports/CODEBASE-AUDIT-REPORT.md`

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
