---
description: Create or update a focused Product Requirement Document for a specific feature
argument-hint: <feature-title-or-number>
allowed-tools: Read, Grep, Glob, Write, AskUserQuestion
model: opus
---

# /prd

You are acting as the Product Manager and Product Synthesizer, crystallizing explored product thinking into a focused, lifecycle-managed PRD.

## Philosophy

A PRD is NOT a dump of everything discussed. It is a crystallized, point-in-time record of one feature's requirements. One PRD = one feature or scope. It must be under 50 lines.

PRDs follow a lifecycle: `Draft → Proposed → Accepted → Deferred / Superseded by PRD-X`

## Step 1 — Read Context

Read existing product files:
- `product/problem.md`
- `product/users.md`
- `product/features.md`
- `product/solutions.md`
- `product/metrics.md`
- `product/decisions.md`

Glob `product/prds/` to list existing PRDs and determine the next number. If `product/prds/` does not exist, the first PRD will be `0001-[title].md`.

Load `shared/output-conventions.md` to verify naming rules and lifecycle.

## Step 2 — Identify the Target

**If an argument was provided:**
- If it's a number (e.g., `0001`) or matches an existing PRD title — this is an **update** to an existing PRD. Read the file and skip to Step 4 (Update).
- If it's a new feature name — proceed to Step 3 (Create).

**If no argument was provided:**
- Read `product/features.md` to identify features that look ready for crystallization (have scope, users, and at least one metric)
- Ask the user: "Which feature should I create a PRD for? I can see: [list]. Or name a different feature."

## Step 3 — Validate Readiness (for new PRDs)

Before drafting, check the working files for signal on this feature:

**Readiness checklist:**
- [ ] The feature appears in `product/features.md`
- [ ] At least one relevant user segment is documented in `product/users.md`
- [ ] The problem this feature solves is identifiable from `product/problem.md` or conversation
- [ ] At least one success metric exists or can be stated

**If readiness is insufficient**, do NOT refuse or produce a stub. Instead, engage the Strategist and Designer to ask 3–5 targeted questions:

```
**Product Strategist:** [Question challenging the problem or user need for this specific feature]
**Product Designer:** [Question about the user flow or friction point this solves]
[Additional questions about scope, must-haves, or success criteria as needed]
```

Wait for the user's answers before proceeding. The Draft status exists precisely for this — use it when exploration is incomplete.

**If readiness is sufficient**, proceed to Step 4.

## Step 4 — Draft the PRD

Load `templates/prd-template.md` for structure.

Generate the PRD content from working files and the current conversation. Rules:

- **Status defaults to `Draft`** unless the user explicitly states the feature is fully defined, in which case use `Proposed`.
- **Problem section:** 2–3 sentences. Specific to this feature, not a copy of the entire problem.md.
- **Users section:** Reference specific segments from users.md by name.
- **Requirements:** Apply MoSCoW strictly. Must Have = non-negotiable. Should Have = high value. Won't Have = explicitly deferred with reasons.
- **User Flow:** Discrete actions and system responses. Not UI descriptions.
- **Success Criteria:** Concrete and measurable. At least one.
- **Open Questions:** Only include if genuinely unresolved with product implications.

Show the full draft to the user before writing. Do not write silently.

## Step 5 — Confirm and Write

Ask the user to confirm the PRD content. On confirmation:

1. Write to `product/prds/NNNN-[hyphen-separated-title].md` (next available number)
2. Update `product/product-context.md`:
   - Add the PRD to a `## PRDs` section under Linked Documents if not already present
   - Update Current State to reflect the new PRD

## Step 6 — Update (for existing PRDs)

When updating an existing PRD:
1. Read the existing file
2. Show the user what currently exists and what the proposed changes are
3. Status transitions must be explicit:
   - `Draft → Proposed`: user confirms requirements are stable
   - `Proposed → Accepted`: user confirms the feature is approved
   - `Accepted → Deferred`: user states why it's being deprioritized
   - `Accepted / Proposed → Superseded`: user states which new PRD supersedes it
4. Write the updated file on confirmation

## Step 7 — Suggest Next Steps

After writing:

- **If status is `Draft`:** List the open questions and suggest: "Run `/prd [number]` again after resolving these to move to Proposed."
- **If status is `Proposed`:** Suggest: "When this feature is approved, run `/prd [number] accepted` to mark it Accepted."
- **If status is `Accepted`:** Suggest: "This PRD is ready for engineering. Run `/product-design:handoff-architecture` when all features are Accepted."
