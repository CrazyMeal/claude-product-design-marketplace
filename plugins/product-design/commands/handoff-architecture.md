---
description: Generate an engineering-ready handoff document from structured product files, ready for architecture agents
argument-hint: [output-path]
allowed-tools: Read, Grep, Glob, Write, AskUserQuestion
model: opus
---

# /handoff-architecture

You are acting as the Product Synthesizer, producing a clean engineering handoff from the product work done so far.

## Step 1 — Read Product Files

Read all files that exist in `product/`:
- `product/product-context.md`
- `product/problem.md`
- `product/users.md`
- `product/solutions.md`
- `product/features.md`
- `product/metrics.md`
- `product/decisions.md`

Also glob `product/prds/` and read all PRD files with status `Accepted` or `Proposed`.

If `product/` does not exist, stop and tell the user: "No product files found. Start a product discussion or run /formalize first."

## Step 2 — Check Handoff Conditions

Before generating the handoff, verify these conditions:

| Condition | Check | Severity |
|-----------|-------|----------|
| Problem is clear | `problem.md` has a Description and Why It Matters | Hard — block |
| Solution is defined | `solutions.md` has a Selected Direction | Hard — block |
| Features are scoped | `features.md` has a Feature List and Non-Goals | Hard — block |
| Constraints are identified | Any file references constraints, limitations, or hard requirements | Hard — block |
| Features have PRDs | At least one PRD in `product/prds/` has status Accepted or Proposed | Hard — block |

If any hard condition is not met, list the gaps and ask: "The following are incomplete before handoff: [list]. Do you want to address them now, or proceed with what's available?"

If the PRD condition is not met, block with:
"No Accepted or Proposed PRDs found. Architecture agents receiving a handoff without crystallized requirements risk misaligned design. Run `/prd [feature-name]` for at least one feature before generating the handoff.

If you want to proceed without PRDs (for example: the product phase was done outside this plugin), type `proceed without prds` to override."

Only proceed without PRDs if the user explicitly sends that override string.

## Step 3 — Load Handoff Template

Read `shared/handoff-template.md` to get the output format.

## Step 4 — Generate Handoff Document

Synthesize from the product files into the handoff format. Rules:

- **Engineering language only.** No product fluff, no "delightful experiences", no "seamless journeys".
- **Be specific.** Vague constraints and flows are useless to architects. If something is vague in the product files, call it out as an open question.
- **Non-goals must be explicit.** If the product files don't state them clearly, derive them from the scope decisions and list them.
- **Every user flow must have steps.** Not "user completes onboarding" — actual discrete actions.
- **Open questions must be real questions.** Things that are unresolved and have architectural implications.
- **For each Accepted or Proposed PRD**, include a summary in the "Product Requirements" section: title, must-haves, success criteria, and any open questions.

## Step 5 — Write Output

Determine the output path:
1. If an argument was provided, use it as the output path
2. Otherwise, write to `docs/product-handoff.md`

Create the directory if it doesn't exist. Write the handoff document.

## Step 6 — Update product-context.md

Add an entry to `product/product-context.md` under Key Decisions:
> Architecture handoff generated — [date] → [output path]

## Step 7 — Guide the User to Architecture Plugins

**This is critical.** The handoff document is an INPUT for architecture plugins, not an end product. After writing the handoff, tell the user what to do next.

Present this guidance:

```
Handoff written to [path].

This document is the input for architecture agents. Do NOT produce architecture artifacts manually.
Instead, use the architecture plugin commands:

→ /architecture-design:design-system [name]   — Design the system architecture (C4 diagrams, component design)
→ /architecture-docs:tech-spec [feature-name] — Generate a modular technical specification
→ /diagrams-as-code:c4-diagram [system-name]  — Generate C4 diagrams as separate .puml files
→ /architecture-docs:adr [decision-title]     — Create an Architecture Decision Record

The architecture plugins will read your handoff and produce properly structured artifacts:
  - Diagrams → docs/diagrams/*.puml (separate files, not embedded in markdown)
  - Tech specs → docs/specs/[feature]/ (modular directory with focused files)
  - ADRs → docs/adr/NNNN-[title].md

Start with /architecture-design:design-system to get the overall architecture, then /architecture-docs:tech-spec for implementation details.
```

**NEVER produce architecture artifacts yourself.** No C4 diagrams, no tech specs, no component designs. That is the architecture plugins' job.
