# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the official Anthropic Claude Code repository — a plugin and documentation hub (not the Claude Code application itself). It contains official plugins, example configurations, automation scripts, and a dev container setup. The main application is distributed as an npm package (`@anthropic-ai/claude-code`).

## Repository Structure

- **plugins/** — 13 official Claude Code plugins (the core of this repo)
- **examples/** — Settings configurations (lax, strict, bash-sandbox) and hook examples
- **scripts/** — TypeScript/bash automation for GitHub issue deduplication
- **Script/** — PowerShell dev container launcher for Windows
- **.devcontainer/** — Docker-based sandboxed development environment (Node 20, zsh, firewall)
- **.github/workflows/** — 11 GitHub Actions for issue triage, deduplication, and lifecycle management
- **.claude-plugin/marketplace.json** — Plugin marketplace registry metadata

## Plugin Architecture

Every plugin follows this structure:
```
plugin-name/
├── .claude-plugin/plugin.json   # Metadata (name, version, description, author)
├── commands/                    # Slash commands (.md files)
├── agents/                      # Specialized agents (.md files)
├── skills/                      # Skills with SKILL.md + references/examples dirs
├── hooks/                       # Event handlers (hooks.json config)
├── hooks-handlers/              # Hook implementation scripts (bash/python)
├── .mcp.json                    # MCP server configuration
└── README.md
```

All directories except `.claude-plugin/` are optional.

## Plugin Categories

- **Development workflows**: feature-dev (7-phase guided dev), plugin-dev (plugin creation toolkit), agent-sdk-dev (SDK scaffolding), frontend-design
- **Code review**: code-review (multi-agent with confidence scoring), pr-review-toolkit (6 specialized review agents)
- **Git automation**: commit-commands (/commit, /commit-push-pr, /clean_gone)
- **Hooks-based**: security-guidance (9 security pattern checks), hookify (markdown-based rule creation), explanatory-output-style, learning-output-style
- **Utilities**: ralph-wiggum (iterative dev loops), claude-opus-4-5-migration

## Key Conventions

- Plugin metadata lives in `.claude-plugin/plugin.json`; always update this when modifying a plugin
- Commands are markdown files in `commands/` that become slash commands (e.g., `commands/commit.md` → `/commit`)
- Agents are markdown files in `agents/` defining specialized sub-agents with model and tool constraints
- Skills use progressive disclosure: `SKILL.md` (core) → `references/` and `examples/` subdirs for detail
- Hooks use a `hooks.json` file mapping event types (PreToolUse, PostToolUse, SessionStart, Stop) to handlers
- New plugins must be registered in `.claude-plugin/marketplace.json` at the repo root

## Dev Container

The `.devcontainer/` setup provides a sandboxed Node 20 environment with firewall restrictions, zsh, git-delta, and Claude Code pre-installed. Run via VS Code Dev Containers or the PowerShell script in `Script/`.

## Contributing

When adding or modifying plugins:
1. Follow the standard plugin structure above
2. Include a comprehensive README.md with usage examples
3. Register new plugins in `.claude-plugin/marketplace.json`
4. Document all commands, agents, and hooks
