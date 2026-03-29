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

If `product/` does not exist, stop and tell the user: "No product files found. Start a product discussion or run /formalize first."

## Step 2 — Check Handoff Conditions

Before generating the handoff, verify all four conditions are met:

| Condition | Check |
|-----------|-------|
| Problem is clear | `problem.md` has a Description and Why It Matters |
| Solution is defined | `solutions.md` has a Selected Direction |
| Features are scoped | `features.md` has a Feature List and Non-Goals |
| Constraints are identified | Any file references constraints, limitations, or hard requirements |

If any condition is not met, list the gaps and ask the user: "The following are incomplete before handoff: [list]. Do you want to address them now, or proceed with what's available?"

## Step 3 — Load Handoff Template

Read `shared/handoff-template.md` to get the output format.

## Step 4 — Generate Handoff Document

Synthesize from the product files into the handoff format. Rules:

- **Engineering language only.** No product fluff, no "delightful experiences", no "seamless journeys".
- **Be specific.** Vague constraints and flows are useless to architects. If something is vague in the product files, call it out as an open question.
- **Non-goals must be explicit.** If the product files don't state them clearly, derive them from the scope decisions and list them.
- **Every user flow must have steps.** Not "user completes onboarding" — actual discrete actions.
- **Open questions must be real questions.** Things that are unresolved and have architectural implications.

## Step 5 — Write Output

Determine the output path:
1. If an argument was provided, use it as the output path
2. Otherwise, write to `docs/product-handoff.md`

Create the directory if it doesn't exist. Write the handoff document.

Confirm to the user: "Handoff written to [path]. Architecture agents can now use this as input."

## Step 6 — Update product-context.md

Add an entry to `product/product-context.md` under Key Decisions:
> Architecture handoff generated — [date] → [output path]
