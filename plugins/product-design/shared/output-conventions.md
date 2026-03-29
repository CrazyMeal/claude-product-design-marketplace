# Output Conventions

## Product Files Location

All product artifacts live in a `product/` directory at the root of the consumer project:

```
your-project/
└── product/
    ├── product-context.md   ← single entry point, always updated
    ├── problem.md
    ├── users.md
    ├── solutions.md
    ├── features.md
    ├── metrics.md
    └── decisions.md
```

## Core Rules

- **One responsibility per file.** Never merge concerns across files.
- **No monolithic PRD.** Information is distributed across focused files.
- **Incremental updates.** Append or refine; never rewrite from scratch unless explicitly requested.
- **product-context.md is the entry point.** Always reflects current state, open questions, and next steps. Update it whenever another product file changes.
- **Short files only.** If a section exceeds ~30 lines, it may need to be split or pruned.

## Naming Conventions

- Files: lowercase, hyphen-separated (already defined above)
- Decision log entries: ordered chronologically, newest last
- Feature list: ordered by priority (highest first)

## Handoff Artifacts

Architecture handoff output is written to:

```
your-project/
└── docs/
    └── product-handoff.md
```

This file is the input consumed by architecture plugins.
