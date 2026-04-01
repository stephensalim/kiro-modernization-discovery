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

## Default Target Stack

The modernization-strategist agent is preconfigured to recommend migration to **TypeScript/Node.js on AWS serverless** (Lambda, API Gateway, DynamoDB, EventBridge, CDK, etc.). If your target stack is different — say Go, Python, Java, or a container-based architecture — edit `.kiro/agents/modernization-strategist.md` and update the target stack, migration mappings, and phased roadmap sections to match your preferred technologies.

## How to Use

### 1. Clone this repo

```bash
git clone https://github.com/stephensalim/kiro-modernization-discovery.git
cd kiro-modernization-discovery
```

### 2. Bring in the codebase you want to audit

Clone or copy your target codebase into this directory. For example:

```bash
# Clone a repo directly
git clone https://github.com/your-org/your-app.git target-app

# Or copy an existing local project
cp -r /path/to/your/project ./target-app
```

The folder name doesn't matter — just place it somewhere inside this workspace so Kiro can see it.

### 3. Open in Kiro IDE and run the audit

1. Open this folder in [Kiro IDE](https://kiro.dev)
2. Select **Claude Opus 4.6** from the model picker
3. Paste the contents of `kiro-codebase-audit-prompt.md` into Kiro chat (or reference it with `#kiro-codebase-audit-prompt.md`)
4. Tell Kiro which folder to audit, e.g.: *"Run the codebase audit against the `target-app/` folder"*
5. The agents will run in parallel and produce reports in `./reports/`

### 4. Review the output

The final consolidated report lands at `./reports/CODEBASE-AUDIT-REPORT.md`. Intermediate reports from each agent are in `./reports/intermediate/`.

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