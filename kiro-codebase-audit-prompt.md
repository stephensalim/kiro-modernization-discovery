I need a comprehensive, read-only audit of this codebase. You must NOT write or modify any source code — only read files, run existing analysis scripts, search the web, and produce markdown reports.

## Setup

1. Create the output directory: `mkdir -p ./reports/intermediate`
2. Verify the custom subagents are available in `.kiro/agents/`

## Phase 1: Parallel Discovery (use subagents)

Launch ALL of the following subagents in parallel:

1. **Use the tech-scanner agent** to scan the full repository and produce `./reports/intermediate/01-technology-inventory.md`
2. **Use the architecture-analyst agent** to map the architecture and produce `./reports/intermediate/02-architecture-analysis.md`
3. **Use the quality-auditor agent** to assess code quality and test coverage and produce `./reports/intermediate/03-quality-audit.md`
4. **Use the security-reviewer agent** to identify security risks and produce `./reports/intermediate/04-security-review.md`

Wait for all subagents to complete before proceeding.

## Phase 2: Research & Modernization Strategy

Once all Phase 1 reports exist:

1. Read all four intermediate reports
2. Search the web for current best practices on migrating the identified tech stack to **TypeScript/Node.js** on **modern AWS serverless architecture** (Lambda, API Gateway, DynamoDB, EventBridge, CDK, Step Functions), including framework migration paths, recommended TypeScript/AWS replacements for current dependencies, and industry patterns for this domain
3. **Use the modernization-strategist agent** to synthesize all findings and produce `./reports/intermediate/05-modernization-strategy.md`

## Phase 3: Final Synthesis

After all intermediate reports are complete, YOU (the main agent) must produce the final consolidated report at `./reports/CODEBASE-AUDIT-REPORT.md` with this structure:

# Codebase Audit Report: [Project Name]
**Date:** [today's date]
**Audited by:** Kiro IDE + Claude Opus 4.6
**Scope:** Full repository — read-only analysis

## 1. Executive Summary
- 5-7 bullet points covering the most critical findings across all dimensions
- Overall health rating: Critical / Needs Attention / Healthy / Excellent
- Top 3 risks requiring immediate attention
- Top 3 quick wins for immediate improvement

## 2. Technology Inventory
[Synthesized from 01-technology-inventory.md — tables for languages, frameworks, dependencies, build tools, infrastructure]

## 3. Architecture Overview
[Synthesized from 02-architecture-analysis.md — component map, data flow diagrams (Mermaid), external integrations, architectural hotspots]

## 4. Code Quality & Technical Debt
[Synthesized from 03-quality-audit.md — complexity hotspots, code smells summary, technical debt register sorted by severity]

## 5. Test Coverage
[Synthesized from 03-quality-audit.md — coverage summary table, critical untested paths, test quality assessment]

## 6. Security Assessment
[Synthesized from 04-security-review.md — risk summary, priority remediations, dependency vulnerabilities]

## 7. Modernization Roadmap
[Synthesized from 05-modernization-strategy.md — bounded contexts, service separation recommendations with impact-effort matrix, phased roadmap targeting TypeScript/Node.js on AWS serverless]

### Target Architecture
- **Backend:** TypeScript/Node.js on AWS Lambda + API Gateway
- **Frontend:** React + Next.js (TypeScript) on CloudFront
- **Data:** DynamoDB / Aurora Serverless v2
- **Events:** EventBridge + Step Functions + SQS
- **IaC:** AWS CDK (TypeScript)
- **Auth:** Amazon Cognito
- **Observability:** CloudWatch + X-Ray

### Priority Matrix
| # | Recommendation | Impact | Effort | Priority | Phase |

### Phased Roadmap
[Timeline with phases, milestones, and dependencies]

## 8. Risk Register
| ID | Risk | Likelihood | Impact | Mitigation | Owner |

## 9. Assumptions & Open Questions
| # | Assumption/Question | Confidence | Impact if Wrong |

## 10. Appendix: File References
[Key file paths referenced throughout the report]

## Constraints — STRICTLY FOLLOW

- Do NOT use AI-DLC for this task
- Do NOT write, modify, or refactor any source code
- Do NOT create new tests, scripts, or configuration files
- Do NOT modify any existing files in the repository (except creating files in ./reports/)
- ALL output files go in `./reports/` only
- Use Mermaid syntax for all diagrams
- Tie every finding to a specific file path
- Use tables for all scored or comparative data
- If uncertain about a finding, mark confidence level and note it in Assumptions
- Search the internet when you need current information about frameworks, CVEs, migration guides, or best practices
- Be specific and actionable — avoid generic advice