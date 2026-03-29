# Product Knowledge

Reference frameworks loaded on demand by the product team. Do not preload — reference when explicitly needed.

---

## Jobs-to-be-Done (JTBD)

### When to use
When the problem definition feels vague, feature-driven, or solution-first. JTBD reframes around the outcome users are trying to achieve.

### Core formula
> When [situation], I want to [motivation], so I can [expected outcome].

### Application
1. Identify the situation that triggers the need
2. Identify the underlying motivation (functional, emotional, social)
3. Identify the outcome the user is trying to reach
4. Challenge: is the proposed solution the best way to achieve that outcome? Are there better alternatives?

### Common pitfall
Confusing the job with the feature. "I want a faster horse" is a solution. "I want to get from A to B faster" is the job.

---

## RICE Prioritization

### When to use
When there are multiple features or options and the team needs to prioritize objectively.

### Formula
**Score = (Reach × Impact × Confidence) / Effort**

| Factor | Description | Scale |
|--------|-------------|-------|
| Reach | How many users affected per time period | # of users |
| Impact | How much it moves the key metric | 0.25 / 0.5 / 1 / 2 / 3 |
| Confidence | How confident are we in the estimates | 50% / 80% / 100% |
| Effort | Person-months to build | months |

### Application
- Score each candidate feature
- Rank by score
- Flag any item where Confidence < 80% — validate before committing

### Common pitfall
Gaming Impact scores. If everything is Impact 3, the model breaks. Be conservative.

---

## Experiment Design

### When to use
When a key assumption hasn't been validated. Build the minimum needed to test it, not the full feature.

### Structure
1. **Assumption:** State the belief being tested explicitly
2. **Risk:** What happens if this assumption is wrong?
3. **Experiment:** What is the smallest test that could validate or invalidate it?
4. **Signal:** What metric or observation will tell you the result?
5. **Threshold:** What result would cause you to change direction?

### Experiment types (lightest to heaviest)
- **Fake door:** Measure demand before building (landing page, waitlist, button that 404s)
- **Wizard of Oz:** Simulate the system manually behind the scenes
- **Concierge:** Deliver value manually to a small set of users
- **Prototype:** Clickable mockup tested with real users
- **Shadow launch:** Build but don't expose — validate with synthetic traffic
- **Feature flag rollout:** Controlled exposure to a % of real users

### Common pitfall
Running an experiment that can't invalidate the assumption. If the result can only confirm, it's not an experiment — it's theater.
