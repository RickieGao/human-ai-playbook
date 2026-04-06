# Rules Fragment Assembly

## Purpose

When the output strategy is multi-file, these fragments become standalone `.claude/rules/*.md` files instead of being folded into CLAUDE.md.

## Fragment Format

Each rules fragment uses this structure:

```markdown
---
description: One-line purpose of this rule file
---

# [Rule Topic]

[Content — imperative instructions for AI]
```

## Path-Scoped Fragment Format

For monorepo scale, rules can target specific paths:

```markdown
---
description: One-line purpose of this rule file
paths:
  - "packages/api/**/*"
  - "packages/shared/**/*"
---

# [Rule Topic]

[Content — imperative instructions for AI]
```

## Which fragments to extract

| Fragment | Source template | When extracted |
|----------|---------------|----------------|
| `quality.md` | `base/quality-standards.md` (testing section) | small-team, monorepo |
| `commit.md` | `base/quality-standards.md` (commits section) | small-team, monorepo |
| `workflow.md` | `workflow/*.md` (selected workflow) | small-team, monorepo |
| Per-package rules | Custom from scan/interview | monorepo only |

## What stays in CLAUDE.md

When fragments are extracted, CLAUDE.md retains:
- Project Identity (always)
- Collaboration Mode (always — this is the "working contract")
- Context Management (always)
- Known Pitfalls and Safety Constraints (always — too critical to put in optional files)
- A brief note: "Additional rules are in `.claude/rules/` — these load automatically."
