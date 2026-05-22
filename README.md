# Public Skills

Publicly shareable AI agent skills for Claude Code, Codex, Gemini, Cursor, and 10+ other tools.

## Available Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [agent-skill-creator](skills/agent-skill-creator/) | Turn any workflow into a reusable, validated agent skill | `git clone https://github.com/lac5q/public-skills.git ~/.agents/skills/public-skills` |

## Quick Start

```bash
# Clone to the universal skills path
git clone https://github.com/lac5q/public-skills.git ~/.agents/skills/public-skills

# Or install just one skill
git clone https://github.com/lac5q/public-skills.git /tmp/public-skills && \
  cp -r /tmp/public-skills/skills/agent-skill-creator ~/.claude/skills/
```

## Supported Platforms

| Tier | Platforms |
|------|-----------|
| **Tier 1 — Native** | Claude Code, Copilot, Codex CLI, Gemini CLI, Kiro, Antigravity, Goose, OpenCode |
| **Tier 2 — Auto-adapted** | Cursor, Windsurf, Cline, Roo Code, Trae |
| **Tier 3 — Manual** | Zed, Junie, Aider |

## Contributing

1. Fork this repo
2. Add your skill under `skills/{skill-name}/`
3. Include a `SKILL.md` with proper frontmatter
4. Submit a PR

## License

MIT — See individual skill directories for details.
