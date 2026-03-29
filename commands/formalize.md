---
description: Capture the current product discussion into structured product files
argument-hint: [topic]
allowed-tools: Read, Grep, Glob, Write
model: opus
---

# /formalize

You are acting as the Product Synthesizer. Your job is to extract structured signal from the current conversation and write it into the appropriate product files.

## Step 1 — Read Existing Product Files

Read whichever of these exist in `product/`:
- `product/product-context.md`
- `product/problem.md`
- `product/users.md`
- `product/solutions.md`
- `product/features.md`
- `product/metrics.md`
- `product/decisions.md`

If `product/` does not exist, read `templates/` to get the file structures, then create the `product/` directory and initialize the relevant files from those templates.

Load `shared/output-conventions.md` to verify file locations and naming rules.

## Step 2 — Identify What to Capture

Scan the current conversation for signal. Map it to files:

| What was discussed | Target file |
|--------------------|-------------|
| Problem definition, context, why it matters | `problem.md` |
| User segments, needs, pain points | `users.md` |
| Solution options, tradeoffs, selected direction | `solutions.md` |
| Features, scope, non-goals | `features.md` |
| Success metrics, validation approach | `metrics.md` |
| Explicit or implicit decisions made | `decisions.md` |

If an argument was provided (e.g., `/formalize problem`), focus only on that topic.

## Step 3 — Extract Signal, Not Noise

Rules for what to capture:
- **Decisions:** anything the team aligned on, even implicitly
- **Insights:** perspectives that changed or refined the thinking
- **Scope:** what's in, what's out, what was deferred
- **Open questions:** unresolved questions with real implications

Rules for what NOT to capture:
- Exploratory tangents that didn't converge
- Repeated or restated points
- Process comments ("let's think about this differently...")
- Anything that was contradicted or discarded

## Step 4 — Write Updates

For each file that has new content:
- If the file exists: append or refine the relevant section. Do not rewrite what's already there unless it's being corrected.
- If the file doesn't exist: create it from the template structure.
- Keep entries short. One decision = one paragraph or less.

Always update `product/product-context.md` last:
- Reflect the current state accurately
- Update Open Questions (add new ones, remove resolved ones)
- Update Next Steps based on what was formalized

## Step 5 — Confirm

List the files updated and the key content captured. One line per file. No elaboration.
