# Claude Product Design Plugin

A Claude Code plugin that brings structured product thinking into your development workflow. Five product personas challenge your assumptions, explore alternatives, and progressively formalize insights — then hand off cleanly to architecture agents.

## What It Does

- **Challenges ideas** before you commit to a solution
- **Structures product thinking** into focused, incremental artifacts
- **Produces engineering-ready handoffs** for architecture plugins
- **Stays lightweight** — conversation-driven, not command-heavy

## Personas

| Persona | Focus |
|---------|-------|
| Product Strategist | Challenges the problem, identifies false assumptions, analyzes alternatives |
| Product Manager | Structures ideas, defines scope, translates to features |
| Product Designer | UX, friction points, usability critique |
| Product Analyst | Metrics, validation, experimentation |
| Product Synthesizer | Summarizes discussions, structures insights, prepares artifacts |

## Commands

| Command | Description |
|---------|-------------|
| `/formalize` | Capture current discussion into structured `product/*.md` files |
| `/explore-alternatives` | Systematic exploration of solution options with tradeoff analysis |
| `/handoff-architecture` | Generate engineering-ready handoff document for architecture agents |

## Product Files

When you start product work, the plugin creates these files in your project's `product/` directory:

```
product/
├── product-context.md   ← single entry point, always current
├── problem.md
├── users.md
├── solutions.md
├── features.md
├── metrics.md
└── decisions.md
```

## Workflow

```
Discuss ideas naturally
  → personas challenge and refine thinking
  → /formalize captures structured insights
  → product/*.md files updated incrementally
  → /handoff-architecture when ready
  → architecture agents take over
```

## Handoff Compatibility

The `/handoff-architecture` command produces output at `docs/product-handoff.md`, formatted for direct consumption by architecture plugins (architecture-design, architecture-docs, etc.).

## Installation

Copy this plugin into your Claude Code plugins directory or reference it from your `.claude/settings.json`.
