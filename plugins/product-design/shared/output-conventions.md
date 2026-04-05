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
    ├── decisions.md
    └── prds/
        ├── 0001-feature-name.md
        └── 0002-other-feature.md
```

## Core Rules

- **One responsibility per file.** Never merge concerns across files.
- **No monolithic PRD.** Information is distributed across focused files.
- **Incremental updates.** Append or refine; never rewrite from scratch unless explicitly requested.
- **product-context.md is the entry point.** Always reflects current state, open questions, and next steps. Update it whenever another product file changes.
- **Short working files.** If a section exceeds ~30 lines, it may need to be split or pruned.

## Naming Conventions

- Working files: lowercase, hyphen-separated (already defined above)
- PRD files: `NNNN-[hyphen-separated-title].md` — four-digit zero-padded number (e.g., `0001-user-authentication.md`)
- Decision log entries: ordered chronologically, newest last
- Feature list: ordered by priority (highest first)

## PRD Lifecycle

PRDs are per-feature crystallized artifacts. They follow a strict lifecycle:

`Draft` → `Proposed` → `Accepted` → `Deferred` or `Superseded by PRD-X`

- **Draft** — incomplete, exploration still needed
- **Proposed** — ready for review; requirements and scope are stable
- **Accepted** — approved; feeds into architecture handoff
- **Deferred** — deprioritized; retained for future reference
- **Superseded** — replaced by a later PRD (must reference it)

PRD file limit: **50 lines max.** A PRD over 50 lines is covering too much scope — split it into multiple focused PRDs.

## Prohibited Patterns

These are hard rules. Violating them produces output that is useless or harmful to downstream architecture agents.

- **No monolithic documents.** Never create a single PRD.md, USER-FLOWS.md, spec.md, requirements.md, or any document that combines multiple product concerns.
- **No working files over 30 lines of content.** Long files are a signal that a concern was not separated properly.
- **No PRD files over 50 lines of content.** A PRD that exceeds 50 lines is trying to cover too much scope.
- **Never write outside `product/`.** Not `docs/product/`, not `docs/`, not the project root. Only `product/` and `product/prds/`.
- **Only the 7 canonical working files + `prds/` subdirectory.** Do not invent new file names or directories.
- **Use templates as structure basis.** When creating a file for the first time, load the corresponding template from `templates/` to get the section headers.
- **PRDs are created only via `/prd` command.** The skill and agent may suggest creating one, but never write to `product/prds/` directly.

## Handoff Artifacts

Architecture handoff output is the one exception to the `product/` rule. It is written to:

```
your-project/
└── docs/
    └── product-handoff.md
```

This file is the input consumed by architecture plugins. It is generated only by `/handoff-architecture`, never by the skill or agent directly.
