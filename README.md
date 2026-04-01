# OSOP Skill — Workflow Logging for AI Agents

[![OSOP Compatible](https://img.shields.io/badge/OSOP-compatible-blue)](https://osop.ai)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

Teach any AI agent (Claude Code, OpenClaw, etc.) to produce structured execution logs using the OSOP protocol. Every significant action gets recorded as `.osop` + `.osoplog.yaml` files that can be visualized, risk-analyzed, and replayed.

## Quick Start: Claude Code

**Copy `CLAUDE.md` into your project root.** That's it. Claude Code will now produce OSOP session logs after significant tasks.

```bash
# In your project directory:
curl -o CLAUDE.md https://raw.githubusercontent.com/Archie0125/osop-openclaw-skill/main/CLAUDE.md
```

Or manually copy the content of `CLAUDE.md` into your existing `CLAUDE.md`.

## What You Get

After Claude Code completes a multi-step task, it produces:

1. **`sessions/YYYY-MM-DD-description.osop`** — workflow definition (what steps were planned)
2. **`sessions/YYYY-MM-DD-description.osoplog.yaml`** — execution log (what actually happened)

Open both at **https://osop-editor.vercel.app** to see:
- Step-by-step replay with play/pause controls
- Risk analysis (permission gaps, destructive commands, missing approval gates)
- Sub-agent tracking (which child agents did what)
- Tool usage per step (Read, Edit, Bash calls)
- AI reasoning decisions (why the agent chose approach A over B)

## Features

### 9 MCP Tools (via osop-mcp server)
| Tool | Description |
|------|-------------|
| `osop.validate` | Validate workflow against schema |
| `osop.risk_assess` | Analyze security risks (score 0-100) |
| `osop.run` | Execute workflow with dry-run support |
| `osop.render` | Generate Mermaid/ASCII diagrams |
| `osop.optimize` | Data-driven improvement suggestions from run history |
| `osop.test` | Run embedded test cases |
| `osop.report` | Generate HTML/text reports |
| `osop.import` | Convert from GitHub Actions, BPMN, Airflow |
| `osop.export` | Convert to external formats |

### 9 Safety Policies
1. Dry-run before production
2. Approval gates for high-risk operations
3. Secret handling (no hardcoded credentials)
4. Scope limitation
5. Timeout and resource bounds
6. Audit trail (every execution logged)
7. Rollback readiness
8. Risk assessment before execution
9. Skill installation safety

### Self-Optimization Loop
Execute → Log → Analyze (slow steps, failures) → Improve SOP → Re-execute better

## Structure

```
CLAUDE.md                          # Drop-in for Claude Code projects
skills/osop/SKILL.md               # OpenClaw skill definition
skills/osop/metadata.json          # Skill metadata + MCP tool config
prompts/system-prompt.md           # System prompt (16 node types, 13 edge modes)
prompts/policy-pack.md             # 9 safety policies
examples/fix-auth-bug.osop         # Example workflow with sub-agents
examples/fix-auth-bug.osoplog.yaml # Example execution log with full detail
```

## For OpenClaw Users

```bash
openclaw skill install Archie0125/osop-openclaw-skill
```

Set `OSOP_MCP_URL` to your OSOP MCP server URL.

## OSOP Ecosystem

| Repo | Description |
|------|-------------|
| [osop-spec](https://github.com/Archie0125/osop-spec) | Protocol specification v1.0 |
| [osop-editor](https://github.com/Archie0125/osop-editor) | Visual editor + risk analysis ([live demo](https://osop-editor.vercel.app)) |
| [osop-mcp](https://github.com/Archie0125/osop-mcp) | MCP server with 9 tools |
| [osop-examples](https://github.com/Archie0125/osop-examples) | 36+ workflow templates |

## License

Apache License 2.0
