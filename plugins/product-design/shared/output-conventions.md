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

## Prohibited Patterns

These are hard rules. Violating them produces output that is useless or harmful to downstream architecture agents.

- **No monolithic documents.** Never create PRD.md, USER-FLOWS.md, spec.md, requirements.md, or any document that combines multiple product concerns.
- **No files over 30 lines of content.** Long files are a signal that a concern was not separated properly.
- **Never write outside `product/`.** Not `docs/product/`, not `docs/`, not the project root. Only `product/`.
- **Only the 7 canonical files.** Do not invent new file names. If something doesn't fit, reconsider the content, not the filename.
- **Use templates as structure basis.** When creating a file for the first time, load the corresponding template from `templates/` to get the section headers.

## Handoff Artifacts

Architecture handoff output is the one exception to the `product/` rule. It is written to:

```
your-project/
└── docs/
    └── product-handoff.md
```

This file is the input consumed by architecture plugins. It is generated only by `/handoff-architecture`, never by the skill or agent directly.
