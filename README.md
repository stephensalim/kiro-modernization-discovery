# Kiro Modernization Discovery

This repository contains a set of [Kiro IDE](https://kiro.dev) [custom subagents](https://kiro.dev/docs/chat/subagents/) for running comprehensive, read-only codebase audits. Five specialized agents work in parallel to analyze a codebase's technology stack, architecture, code quality, security posture, and modernization path — producing structured markdown reports without modifying any source code. A single orchestration prompt (`kiro-codebase-audit-prompt.md`) coordinates all five agents, synthesizes their findings, and produces a consolidated audit report with a phased modernization roadmap.

## Subagents

All agent definitions live in [`.kiro/agents/`](.kiro/agents/) and are picked up automatically by Kiro IDE. See the [Kiro subagents documentation](https://kiro.dev/docs/chat/subagents/) for details on how custom agents work.

| Agent | File | Role |
|-------|------|------|
| tech-scanner | [`.kiro/agents/tech-scanner.md`](.kiro/agents/tech-scanner.md) | Inventories languages, frameworks, dependencies, build tools, CI/CD, and infrastructure-as-code |
| architecture-analyst | [`.kiro/agents/architecture-analyst.md`](.kiro/agents/architecture-analyst.md) | Maps entry points, component relationships, data flows, external integrations, and produces Mermaid diagrams |
| quality-auditor | [`.kiro/agents/quality-auditor.md`](.kiro/agents/quality-auditor.md) | Assesses code complexity, code smells, test coverage, documentation state, and technical debt |
| security-reviewer | [`.kiro/agents/security-reviewer.md`](.kiro/agents/security-reviewer.md) | Identifies auth weaknesses, input validation gaps, hardcoded secrets, dependency CVEs, and supply chain risks |
| modernization-strategist | [`.kiro/agents/modernization-strategist.md`](.kiro/agents/modernization-strategist.md) | Synthesizes all findings into bounded contexts, service separation recommendations, and a phased roadmap |

## Default Target Stack

The modernization-strategist agent is preconfigured to recommend migration to **TypeScript/Node.js on AWS serverless** (Lambda, API Gateway, DynamoDB, EventBridge, CDK, etc.). If your target stack is different — say Go, Python, Java, or a container-based architecture — edit [`.kiro/agents/modernization-strategist.md`](.kiro/agents/modernization-strategist.md) and update the target stack, migration mappings, and phased roadmap sections to match your preferred technologies.

## Recommended MCP Servers

The agents reference web search and documentation tools. For the best results, configure these MCP servers in your Kiro IDE (`.kiro/settings/mcp.json` or `~/.kiro/settings/mcp.json`):

| MCP Server | Purpose | Link |
|------------|---------|------|
| Context7 | Provides up-to-date documentation for libraries and frameworks found in the codebase | [github.com/upstash/context7](https://github.com/upstash/context7) |
| AWS Documentation | Searches AWS docs, API references, and best practices — useful for the modernization strategy phase | [awslabs/mcp — aws-documentation-mcp-server](https://github.com/awslabs/mcp/tree/main/src/aws-documentation-mcp-server) |
| AWS Bedrock Knowledge Bases | Queries Amazon Bedrock Knowledge Bases for organization-specific context | [awslabs/mcp — bedrock-kb-retrieval-mcp-server](https://github.com/awslabs/mcp/tree/main/src/bedrock-kb-retrieval-mcp-server) |

Example `.kiro/settings/mcp.json`:

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    },
    "aws-docs": {
      "command": "uvx",
      "args": ["awslabs.aws-documentation-mcp-server@latest"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      }
    },
    "aws-kb": {
      "command": "uvx",
      "args": ["awslabs.bedrock-kb-retrieval-mcp-server@latest"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      }
    }
  }
}
```

## How to Use

### 1. Clone this repo

```bash
git clone https://github.com/stephensalim/kiro-modernization-discovery.git
cd kiro-modernization-discovery
```

### 2. Add the codebase you want to audit

Clone or copy your target project into this directory:

```bash
# Clone a repo
git clone https://github.com/your-org/your-app.git target-app

# Or copy a local project
cp -r /path/to/your/project ./target-app
```

Place it anywhere inside this workspace — the folder name doesn't matter.

### 3. Run the audit in Kiro IDE

1. Open this folder in [Kiro IDE](https://kiro.dev)
2. Select **Claude Opus 4.6** from the model picker
3. Paste the contents of [`kiro-codebase-audit-prompt.md`](kiro-codebase-audit-prompt.md) into Kiro chat
4. Tell Kiro which folder to audit, e.g.: *"Run the codebase audit against the `target-app/` folder"*

### 4. Review the output

Reports are written to `./reports/`:

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

The final consolidated report is `CODEBASE-AUDIT-REPORT.md`. Intermediate reports from each agent are available for deeper review.

## License

This project is provided as-is for internal use.