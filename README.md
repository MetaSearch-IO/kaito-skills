# kaito-skills

[![license](https://img.shields.io/github/license/MetaSearch-IO/kaito-skills)](./LICENSE)

Agent Skills powered by [Kaito](https://kaito.ai) MCP tools for crypto social intelligence. Install them into any compatible agent (Claude Code, Cursor, VS Code + Copilot, and 40+ more) so your agent can run Kaito-specific workflows like social listening and mindshare pulse analysis on demand.

## Prerequisites

These skills call Kaito MCP tools. You must have [kaito-mcp-server](https://github.com/MetaSearch-IO/kaito-mcp-server) configured in your agent first — see its [README](https://github.com/MetaSearch-IO/kaito-mcp-server#getting-started) for setup and a [Kaito API key](https://kaito.ai).

## Getting Started

Installation uses the open [Agent Skills CLI](https://github.com/vercel-labs/skills) — a single command that knows where each agent stores its skills.

### Quick install (auto-detect agents)

```bash
npx skills add MetaSearch-IO/kaito-skills
```

Installs into every coding agent detected on your machine. Use this if you don't know or don't care about the `--agent` flag.

### Client-specific install

#### Claude Code

```bash
# Project-scoped (committed with your repo, shared with your team)
npx skills add MetaSearch-IO/kaito-skills -a claude-code

# Or global (available across all projects)
npx skills add MetaSearch-IO/kaito-skills -a claude-code -g
```

Installs to `.claude/skills/` (project) or `~/.claude/skills/` (global). Restart your Claude Code session to pick up the new skills.

#### Cursor

```bash
npx skills add MetaSearch-IO/kaito-skills -a cursor
```

Installs to `.agents/skills/` (project) or `~/.cursor/skills/` (global). Requires **Cursor 2.4+** — earlier versions don't support Agent Skills.

#### VS Code (GitHub Copilot agent mode)

```bash
npx skills add MetaSearch-IO/kaito-skills -a github-copilot
```

Installs to `.agents/skills/` (project) or `~/.copilot/skills/` (global). Requires Copilot agent mode to be enabled.

#### Other supported agents

The [Agent Skills CLI supports 45+ agents](https://github.com/vercel-labs/skills#supported-agents) including Codex, OpenCode, Continue, Cline, Windsurf, Gemini CLI, Goose, Roo Code, Kiro, and more. Pick the right flag for yours:

```bash
npx skills add MetaSearch-IO/kaito-skills -a <agent>
```

#### Claude Desktop (Chat tab) / Claude.ai (web)

> **Using the Code tab in Claude Desktop?** The Code tab is Claude Code with a GUI — it runs the agent locally and supports skills. Follow the [Claude Code](#claude-code) instructions above instead. This section only applies to the **Chat tab** and Claude.ai web, where the agent runs in Anthropic's cloud.

The Chat tab and Claude.ai web **cannot read local skill directories**. You must upload each skill manually:

1. Clone this repo and zip each skill directory:
   ```bash
   git clone https://github.com/MetaSearch-IO/kaito-skills.git
   cd kaito-skills/skills/marketing-social-listening
   zip -r ../marketing-social-listening.zip .
   cd ../marketing-social-pulse
   zip -r ../marketing-social-pulse.zip .
   ```
2. Open **Settings → Capabilities → Skills** (Claude.ai web) or **Customize → Skills** (Claude Desktop).
3. Click **Upload skill** and select the `.zip` for each skill (repeat for each skill).

> **Note:** Claude Desktop's Chat tab does not read local skill directories — every skill must be zipped and uploaded to the cloud. The Code tab does not have this limitation (it runs Claude Code locally).

### Common flags

| Flag | Purpose |
|---|---|
| `-g, --global` | Install to your home directory instead of the current project |
| `-a <agent>` | Target a specific agent (e.g. `claude-code`, `cursor`, `github-copilot`) |
| `-s <skill>` | Install a specific skill only (e.g. `-s marketing-social-pulse`) |
| `--copy` | Copy files instead of symlinking (use when symlinks are unsupported) |
| `-y, --yes` | Skip confirmation prompts (CI-friendly) |

Full reference: [vercel-labs/skills README](https://github.com/vercel-labs/skills#readme).

## Skills

| Skill | Description |
|---|---|
| [marketing-social-listening](skills/marketing-social-listening/SKILL.md) | Cluster the top 100 highest-signal tweets for a crypto project into hot topics, with author enrichment, urgency scoring, and concrete response guidance. Use for past-window social listening reports. |
| [marketing-social-pulse](skills/marketing-social-pulse/SKILL.md) | Analyze mindshare, sentiment, and broader social metrics for an entity. Use when asking about the social pulse of a project, mindshare/sentiment trends, or anomaly-based explanations. |

## Verifying & Managing

```bash
# List everything installed (project + global)
npx skills list

# List for a specific agent
npx skills list -a cursor

# Update to the latest version
npx skills update

# Remove
npx skills remove -a <agent> marketing-social-pulse
```

## Development

Skills follow the [Agent Skills format](https://github.com/vercel-labs/skills#creating-skills) — a directory containing a `SKILL.md` with YAML frontmatter (`name`, `description`) followed by markdown instructions.

```
skills/
└── <skill-name>/
    └── SKILL.md
```

## License

[MIT](LICENSE)
