# CLAUDE.md — Product Design Plugin

## Overview

This is a single Claude Code plugin that enables structured product thinking upstream of architecture agents. It provides a team of 5 product personas that challenge ideas, explore alternatives, and progressively formalize insights into structured artifacts — then hand off cleanly to architecture plugins.

## Repository Structure

```
claude-product-design-marketplace/
├── CLAUDE.md                          ← you are here
├── README.md
├── .claude-plugin/
│   └── marketplace.json               ← marketplace component registry
└── plugins/
    └── product-design/
        ├── .claude-plugin/
        │   └── plugin.json            ← plugin manifest
        ├── agents/
        │   └── product-team.md        ← 5 product personas (single file)
        ├── skills/
        │   └── product-thinking/
        │       └── SKILL.md           ← auto-trigger skill
        ├── commands/
        │   ├── handoff-architecture.md ← /handoff-architecture
        │   ├── formalize.md           ← /formalize
        │   └── explore-alternatives.md ← /explore-alternatives
        ├── shared/
        │   ├── output-conventions.md  ← authoritative file locations and naming rules
        │   ├── product-knowledge.md   ← JTBD, RICE, experiment frameworks
        │   └── handoff-template.md    ← architecture handoff output format
        ├── templates/
        │   └── *.md                   ← blueprints for product/ files in consumer projects
        └── references/
            └── interaction-rules.md   ← detailed agent interaction protocol
```

## Plugin Conventions

### Frontmatter Formats

**Agents** (`agents/*.md`):
```yaml
---
name: agent-name
description: One-sentence persona description.
tools: Read, Grep, Glob, Write, AskUserQuestion
model: opus
---
```

**Skills** (`skills/<name>/SKILL.md`):
```yaml
---
name: skill-name
description: Trigger description — used by Claude to decide when to activate. Be specific.
allowed-tools: Read, Grep, Glob, Write
model: opus
---
```

**Commands** (`commands/<name>.md`):
```yaml
---
description: What the slash command does (shown in help)
argument-hint: <argument> [optional]
allowed-tools: Read, Grep, Glob, Write, AskUserQuestion
model: opus
---
```

### Shared Knowledge

Files in `shared/` are loaded **on-demand** by agents, skills, and commands — never auto-injected. Reference them explicitly in the body of the relevant files.

### Templates

Files in `templates/` are blueprints. They are copied into the consumer project's `product/` directory when a user initializes product work. They are not modified by the plugin itself.

## Versioning

- Version follows semver in `.claude-plugin/plugin.json`
- Bump version when adding or changing agents, skills, or commands

## Contributing

- Keep agent/skill/command files focused — one responsibility each
- No passive validation in agents — every contribution must add a distinct perspective
- Keep shared knowledge files reference-style (scannable, not narrative)
