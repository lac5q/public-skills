---
name: agent-skill-creator
description: >
  Convert any workflow, process, or tacit knowledge into a validated, reusable
  AI agent skill (SKILL.md + optional scripts/references/assets). Use when the
  user wants to: (1) turn a recurring workflow into a skill, (2) create a skill
  from documentation, code, transcripts, or plain English description, (3)
  generate a SKILL.md with proper frontmatter, structure, and validation, (4)
  install or share a skill across 14+ AI tools (Claude Code, Codex, Gemini,
  Cursor, etc.), or (5) validate or security-scan an existing skill. Not for
  one-off tasks that will never repeat.
metadata:
  short-description: Turn workflows into reusable agent skills
---

# Agent Skill Creator

Turn any workflow into a validated, installable AI agent skill.

## What This Skill Does

Takes messy inputs (docs, links, code, PDFs, transcripts, or plain English) and
generates a structured skill directory with:

- `SKILL.md` — proper YAML frontmatter + markdown instructions
- `scripts/` — executable helpers (optional)
- `references/` — documentation loaded on demand (optional)
- `assets/` — templates, configs, images (optional)

Every generated skill passes validation and security scanning before delivery.

## Three-Phase Pipeline

```
UNDERSTAND → Read all material → uncover real intent → generate internal spec
BUILD      → Structure directory → write code and docs → craft activation keywords
VERIFY     → Spec validation → security scan → block delivery if either fails
```

## Quick Start

### 1. Describe your workflow

```
Every week I pull sales data from our CRM, clean duplicate entries, calculate
regional totals, and generate a PDF report.
```

Valid inputs: plain English, documentation links, existing code, API docs, PDFs,
database schemas, transcripts. Combine multiple sources in one message.

### 2. Generated output

```
sales-report-skill/
├── SKILL.md          # Skill definition (activates with /keyword)
├── scripts/          # Functional Python code
├── references/       # Detailed documentation
├── assets/           # Templates, configs
├── install.sh        # Cross-platform installer (14 tools, format adapters, --all flag)
└── README.md         # Installation instructions
```

### 3. Install everywhere

```bash
# One-liner: auto-detects all tools, symlinks everywhere
./install.sh --all

# Or manual: clone to universal path
git clone https://github.com/your-org/sales-report-skill.git ~/.agents/skills/sales-report-skill
```

Key paths:
- `~/.claude/skills/` — Claude Code + VS Code Copilot (1.108+)
- `~/.agents/skills/` — Codex CLI, Gemini CLI, Kiro, Antigravity, and others
- `~/.codex/skills/` — OpenAI Codex
- `~/.cursor/skills/` — Cursor IDE

> Run `git pull` once to update everywhere.

## Platform Support (14 Tools)

| Tier | Platforms | Behavior |
|------|-----------|----------|
| **Tier 1 — Native** | Claude Code, Copilot, Codex CLI, Gemini CLI, Kiro, Antigravity, Goose, OpenCode | Reads `SKILL.md` directly |
| **Tier 2 — Auto-adapted** | Cursor (`.mdc`), Windsurf (`.md` rules), Cline, Roo Code, Trae | Installer auto-converts format |
| **Tier 3 — Manual** | Zed, Junie, Aider | Copy skill body into tool's config |

## Team Sharing

### Simple Sharing
Agent auto-creates repo, pushes skill, generates one-liner:
```bash
git clone https://github.com/your-org/sales-report-skill.git ~/.agents/skills/sales-report-skill
```

### Skill Registry (organizations with many skills)
Shared git repo (`{team}-skills-registry`) where all members publish and browse
skills. No servers, no databases — just git.

**Consultant model:** Teach, don't build. Install tool → create registry → teach
5-step workflow → team becomes self-sustaining.

## Quality Gates

| Gate | Checks |
|------|--------|
| **Spec Validation** | `SKILL.md` structure, frontmatter, naming, file references |
| **Security Scan** | No hardcoded API keys, no credentials, no injection patterns |
| **Staleness Check** | Review dates, dependency health, API schema drift |

Run independently: `scripts/validate.py`, `scripts/security_scan.py`

## Staleness Detection (3 Layers, Opt-in)

| Layer | What It Does | Flag |
|-------|-----------|------|
| **Review tracking** | Flags skills past their review date | automatic |
| **Dependency health** | HTTP-checks declared external URLs | `--check-deps` |
| **Schema drift** | Compares actual API response keys against expected | `--check-drift` |

**Frontmatter fields** (optional — existing skills work unchanged):
```yaml
reviewed: 2024-01-15
review_cycle: 90d
dependencies:
  - url: https://api.example.com/v1
    required_keys: [id, name, status]
```

Registry scan: `stale` (checks all published skills at once)

## Skill Structure Standards

### SKILL.md frontmatter (required)
```yaml
---
name: skill-name
description: >
  What this skill does and when to use it. Be specific about triggers.
metadata:
  short-description: One-line summary
---
```

### Body guidelines
- Keep under 500 lines; split into `references/` when larger
- Use imperative/infinitive form
- Include concrete examples, not just abstract instructions
- Reference bundled files clearly: "See [references/schema.md](references/schema.md)"

## Security Rules

- Never hardcode API keys, tokens, or credentials in skills
- Use environment variables or 1Password CLI (`op read`) for secrets
- Validate all user inputs before executing scripts
- Flag injection risks in generated code
- Block delivery if security scan fails

## Verification

After creating a skill, verify it works:

1. **Structure check:** `scripts/validate.py <skill-folder>`
2. **Security scan:** `scripts/security_scan.py <skill-folder>`
3. **Forward-test:** Use the skill on a realistic task in a fresh session
4. **Install test:** Run `./install.sh --all` and verify it appears in all tool paths

## Source

Based on <https://github.com/FrancyJGLisboa/agent-skill-creator> (v5.0.0, MIT).
