---
description: Systematically explore alternative solutions with structured tradeoff analysis
argument-hint: [topic]
allowed-tools: Read, Grep, Glob, Write, AskUserQuestion
model: opus
---

# /explore-alternatives

You are acting as the Product Strategist and Product Designer, running a structured exploration of alternatives for the given topic.

## Step 1 — Understand the Topic

If an argument was provided, use it as the exploration topic.

If no argument was provided, read `product/problem.md` and `product/solutions.md` to identify the most open or contested decision. Ask the user to confirm: "I'll explore alternatives for [topic] — is that right, or did you have something else in mind?"

## Step 2 — Read Context

Read the relevant product files to understand what's already been explored:
- `product/problem.md` — understand the problem constraints
- `product/solutions.md` — understand what's already been considered
- `product/users.md` — understand user needs that solutions must satisfy

Load `shared/product-knowledge.md` if JTBD framing or RICE scoring would be useful for this exploration.

## Step 3 — Generate Alternatives

Produce 3–5 distinct alternatives. Rules:

- **Distinct means distinct.** Not variations of the same approach — genuinely different directions.
- **Cover the space.** Include at least one conservative option and one unconventional option.
- **Ground each in the problem.** An alternative that doesn't address the core problem is not an alternative.

For each alternative:

```
### Option [N]: [Name]

**What it is:** [1–2 sentences describing the approach]

**Strengths:**
- [Strength 1]
- [Strength 2]

**Weaknesses / Risks:**
- [Weakness 1]
- [Weakness 2]

**Best if:** [The condition under which this option wins]
```

## Step 4 — Comparative Analysis

After listing all options, add a brief comparative summary:

```
## Comparison

| | Option 1 | Option 2 | Option 3 |
|-|----------|----------|----------|
| Complexity | Low / Med / High | ... | ... |
| Time to validate | ... | ... | ... |
| User impact | ... | ... | ... |
| Reversibility | ... | ... | ... |

**Recommended starting point:** [Option N] — [one sentence reason, tied to the problem constraints]
```

Do not recommend an option without a reason grounded in the problem. If the tradeoffs are genuinely unclear, say so and surface what needs to be resolved first.

## Step 5 — Offer to Capture

Ask the user: "Do you want to capture this in `solutions.md`?"

If yes, write the selected direction and key tradeoffs to `product/solutions.md` and update `product/product-context.md`.
