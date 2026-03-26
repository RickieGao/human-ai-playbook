# Kickoff Agent: `.claude/rules/` Output Support

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Extend Kickoff Agent to generate `.claude/rules/` files alongside CLAUDE.md for medium-to-large projects, using path-scoped rules to save context and improve modularity.

**Architecture:** Add an "output strategy" decision layer between template assembly and file writing. Solo/simple projects continue producing a single CLAUDE.md. Small-team and monorepo projects additionally generate `.claude/rules/*.md` files, with monorepo rules using path-scoped frontmatter. The interview questions stay unchanged — output strategy is derived from existing scale selection.

**Tech Stack:** Markdown protocol files, no code changes needed.

---

### Task 1: Define output strategy in assembly rules

**Files:**
- Modify: `agents/kickoff/templates/_assembly-rules.md`

- [ ] **Step 1: Update the "## Assembly Process" section (lines 8-17) for multi-file awareness**

After step 8 ("Present to user for review before writing"), add:

```markdown
9. Determine output strategy based on scale selection (see Output Strategy section)
10. For single-file: write all content to CLAUDE.md
11. For multi-file: extract designated fragments into `.claude/rules/` files, keep remaining content in CLAUDE.md
```

- [ ] **Step 2: Update the "200 lines" rule in "## Rules" section (line 60)**

Replace:
```markdown
- Total assembled CLAUDE.md should be under 200 lines
```
With:
```markdown
- Single-file output: total CLAUDE.md should be under 200 lines
- Multi-file output: CLAUDE.md should be under 120 lines; each rules file under 50 lines
```

- [ ] **Step 3: Add output strategy section to `_assembly-rules.md`**

After the existing "## Rules" section (line 58), add:

```markdown
## Output Strategy

The Kickoff Agent produces different file structures based on project scale:

### Single-file (solo-developer scale)
- Output: `CLAUDE.md` only
- All content assembled into one file
- Target: under 200 lines

### Multi-file (small-team scale)
- Output: `CLAUDE.md` + `.claude/rules/` directory
- CLAUDE.md contains: Project Identity, Collaboration Mode, Context Management
- Rules files contain: quality standards, workflow specifics
- Each rules file should be self-contained and under 50 lines

### Multi-file with path scoping (monorepo scale)
- Output: `CLAUDE.md` + `.claude/rules/` directory with path-scoped rules
- CLAUDE.md contains: Project Identity, Collaboration Mode, Context Management
- Global rules (no path scope): quality standards, commit conventions
- Path-scoped rules: per-package/module conventions, testing requirements
- Path-scoped rules use YAML frontmatter:
  ```yaml
  ---
  paths:
    - "packages/api/**/*"
  ---
  ```

### Strategy Selection
- solo-developer → single-file
- small-team → multi-file
- monorepo → multi-file with path scoping
```

- [ ] **Step 4: Update the existing "## Rules" section**

Add one line to the existing rules list:

```markdown
- Output strategy is determined by scale selection (see Output Strategy section)
- For multi-file output, `base/quality-standards.md` content is distributed across `rules/quality.md` and `rules/commit.md` instead of being included in CLAUDE.md
```

- [ ] **Step 5: Commit**

```bash
git add agents/kickoff/templates/_assembly-rules.md
git commit -m "feat(kickoff): add output strategy for multi-file rules generation"
```

---

### Task 2: Add rules template fragments

**Files:**
- Create: `agents/kickoff/templates/rules/quality.md`
- Create: `agents/kickoff/templates/rules/commit.md`
- Create: `agents/kickoff/templates/rules/workflow.md`
- Create: `agents/kickoff/templates/rules/path-scoped-example.md`
- Create: `agents/kickoff/templates/rules/_rules-assembly.md`

- [ ] **Step 1: Create `_rules-assembly.md` — explains how rules fragments work**

```markdown
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
```

- [ ] **Step 2: Create `quality.md` rules fragment**

```markdown
---
description: Testing and code quality requirements
---

# Quality Standards

## Testing
- All new features must have tests
- Run `{{test_command}}` before committing
- Tests must pass before creating a PR

## Code Style
- {{coding_conventions}}
- Run `{{lint_command}}` to check formatting
```

- [ ] **Step 3: Create `commit.md` rules fragment**

```markdown
---
description: Commit conventions and discipline
---

# Commit Conventions

- Use conventional commits: feat:, fix:, docs:, chore:
- Keep commits atomic and focused — one commit = one describable, independent change
- After completing a logical unit of work, proactively remind the user to review and commit before moving on
- Do not mix content changes, config/structure changes, and cross-file fixes in one commit
- Never skip pre-commit hooks
```

- [ ] **Step 4: Create `workflow.md` rules fragment**

```markdown
---
description: Development workflow — selected during kickoff
---

# Workflow

{{workflow_description}}
```

Note: This is a structural placeholder. During assembly, the agent replaces `{{workflow_description}}` with the full content from the selected `workflow/*.md` template (e.g., plan-first, incremental, or TDD). The fragment exists so the multi-file assembly process knows to extract workflow content into a standalone rules file rather than embedding it in CLAUDE.md.

- [ ] **Step 5: Create `path-scoped-example.md` as a reference**

```markdown
---
description: Example of a path-scoped rule for monorepo packages
paths:
  - "packages/api/**/*"
---

# API Package Rules

- All endpoints must include input validation
- Use the shared error handler from `packages/shared/errors`
- API tests go in `packages/api/tests/`, not in a top-level test directory
```

This is a reference example, not a production template. It shows users and the agent how to write path-scoped rules.

- [ ] **Step 6: Commit**

```bash
git add agents/kickoff/templates/rules/
git commit -m "feat(kickoff): add rules template fragments for multi-file output"
```

---

### Task 3: Update decision tree with output strategy mapping

**Files:**
- Modify: `agents/kickoff/decision-tree.md`

- [ ] **Step 1: Add output strategy section at the end of file (after line 123, following "## Output Assembly Order")**

```markdown
## Output Strategy Selection

Output strategy is derived from scale selection:

```
Scale Selection Result
├── solo-developer  → Output: CLAUDE.md only
│                     All fragments assembled into single file
├── small-team      → Output: CLAUDE.md + .claude/rules/
│                     Extract: quality.md, commit.md, workflow.md
│                     CLAUDE.md keeps: identity, collaboration, context, guardrails
└── monorepo        → Output: CLAUDE.md + .claude/rules/ (with path scoping)
                      Extract: quality.md, commit.md, workflow.md
                      Generate: per-package rules from scan data (Path A) or tech recommendation (Path B)
                      CLAUDE.md keeps: identity, collaboration, context, guardrails
```

### Path A monorepo detection

When project scanner detects monorepo structure (multiple packages/modules with their own configs):
- Generate one path-scoped rule per detected package with distinct conventions
- Only create path-scoped rules when packages have meaningfully different conventions (e.g., different languages, different test frameworks)

### Path B monorepo setup

When user describes a monorepo in needs clarification:
- Generate skeleton path-scoped rules based on planned package structure
- Mark them with `TODO: refine after first sprint` comments
```

- [ ] **Step 2: Commit**

```bash
git add agents/kickoff/decision-tree.md
git commit -m "feat(kickoff): add output strategy mapping to decision tree"
```

---

### Task 4: Update staged review for multi-file output

**Files:**
- Modify: `agents/kickoff/staged-review.md`

- [ ] **Step 1: Add a new section after "### Section 5" and before "## After All Sections Confirmed" (between lines 82-83)**

```markdown
### Section 6: File Structure Preview (multi-file output only)

Skip this section if output strategy is single-file.

Show the planned file structure:

```
project-root/
├── CLAUDE.md                    ← Core: identity, collaboration, guardrails
└── .claude/
    └── rules/
        ├── quality.md           ← Testing and code style
        ├── commit.md            ← Commit conventions
        ├── workflow.md          ← Development workflow
        └── api.md (monorepo)   ← Path-scoped: packages/api/**/*
```

> **What this does**: Instead of one large CLAUDE.md, your rules are split into
> focused files. Path-scoped rules only load when AI reads matching files,
> which saves context window space in large projects.

Ask: "Does this file structure make sense? Would you like to merge any of these back into CLAUDE.md, or split differently?"
```

- [ ] **Step 2: Update "## After All Sections Confirmed" (line 83) to handle multi-file writing**

Replace the single write instruction with:

```markdown
## After All Sections Confirmed

### Single-file output
Write CLAUDE.md to project root directory.

### Multi-file output
1. Write CLAUDE.md to project root (with a note pointing to `.claude/rules/`)
2. Create `.claude/rules/` directory
3. Write each rules file

> "Your project configuration has been written:
> - `CLAUDE.md` — core project identity and collaboration rules
> - `.claude/rules/` — modular rules that load automatically
>
> These are living documents — update them as your project evolves."

Then offer optional scaffold (same as before).
```

- [ ] **Step 3: Commit**

```bash
git add agents/kickoff/staged-review.md
git commit -m "feat(kickoff): add multi-file review step to staged review"
```

---

### Task 5: Update examples

**Files:**
- Modify: `agents/kickoff/examples/team-monorepo.md`

- [ ] **Step 1: Rewrite `team-monorepo.md` to demonstrate multi-file output**

The example should show the complete set of output files. Replace the current content:

```markdown
# Example: Team Monorepo (Multi-File Output)

A sample output generated by the Kickoff Agent for a small team working in a monorepo.
Demonstrates the multi-file output strategy with path-scoped rules.

---

## Output Files

```
acme-platform/
├── CLAUDE.md
└── .claude/
    └── rules/
        ├── quality.md
        ├── commit.md
        ├── workflow.md
        ├── api.md          ← path-scoped: packages/api/**/*
        └── web.md          ← path-scoped: packages/web/**/*
```

---

## CLAUDE.md

```markdown
## Project Identity

- **Name**: acme-platform
- **Description**: Monorepo for Acme's platform services
- **Tech Stack**: Go (backend), React/TypeScript (frontend), PostgreSQL, Redis
- **Structure**: `packages/api/`, `packages/web/`, `packages/shared/`, `infra/`

## Commands

# Build all
make build

# Test specific package
make test PKG=api
make test PKG=web

# Lint
make lint

# Run locally
make dev

## Collaboration Mode

### Communication
- Always specify which package you are working in
- Reference team conventions when making choices
- Flag changes that affect multiple packages

### Autonomy
- Strict review: wait for confirmation before applying changes
- Always show the plan before executing

### Review Process
- Backend changes: reviewed by backend team
- Frontend changes: reviewed by frontend team
- Cross-cutting: needs both reviewers

## Context Management

- Focus on one package per session
- Use `/compact` proactively
- Additional rules are in `.claude/rules/` — these load automatically

## Known Pitfalls

- `packages/shared/` changes affect both api and web — run both test suites
- Redis connection pool has a 10-connection limit in dev
- Database migrations are in `infra/migrations/` not in package directories
- The CI pipeline runs in order: lint -> test -> build -> deploy
```

---

## .claude/rules/quality.md

```markdown
---
description: Testing and code quality requirements for acme-platform
---

# Quality Standards

## Testing
- All new features must have tests
- Run `make test PKG=<package>` before committing
- Tests must pass before creating a PR
- All PRs must pass CI before merge

## Code Style
- Go: follow `gofmt` and project `.golangci.yml`
- TypeScript: follow project ESLint + Prettier config
- Run `make lint` to check formatting
```

---

## .claude/rules/commit.md

```markdown
---
description: Commit conventions for acme-platform team
---

# Commit Conventions

- Use conventional commits with package scope: `feat(api): add user endpoint`
- Keep commits atomic and focused
- No direct commits to main — always use PRs
- Cross-package changes need architectural review
- After completing a logical unit of work, proactively remind the user to review and commit
```

---

## .claude/rules/workflow.md

```markdown
---
description: TDD workflow for acme-platform
---

# Workflow: TDD

1. Write test first in the relevant package
2. Run `make test PKG=<package>` to confirm failure
3. Implement the minimum code to pass
4. Run tests again to confirm
5. Refactor if needed
6. Commit with scope: `feat(api): add user endpoint`
```

---

## .claude/rules/api.md

```markdown
---
description: Backend API conventions — Go services
paths:
  - "packages/api/**/*"
---

# API Package Rules

- All endpoints must include input validation using the shared validator
- Use the error handler from `packages/shared/errors`
- API tests go in `packages/api/*_test.go`
- Database queries must use prepared statements
```

---

## .claude/rules/web.md

```markdown
---
description: Frontend conventions — React/TypeScript
paths:
  - "packages/web/**/*"
---

# Web Package Rules

- Components use functional style with hooks
- State management via React Context (no Redux)
- All components must have snapshot tests
- CSS modules only — no inline styles in production code
```
```

- [ ] **Step 2: Commit**

```bash
git add agents/kickoff/examples/team-monorepo.md
git commit -m "docs(kickoff): update monorepo example with multi-file output"
```

---

### Task 6: Update SKILL.md and TODO.md

**Files:**
- Modify: `agents/kickoff/SKILL.md`
- Modify: `agents/kickoff/TODO.md`

- [ ] **Step 1: Update SKILL.md flow diagram**

In the flow section (line 21-31), update to reflect the new output:

```
Detect Environment
  ├── Existing project → Scan & confirm → Collaboration questions → Output strategy
  └── New idea → Clarify needs → Research market → Tech recommendation
                                                          ↓
                                         Collaboration questions → Output strategy
                                                          ↓
                                              ├── Solo → CLAUDE.md
                                              └── Team/Monorepo → CLAUDE.md + .claude/rules/
                                                          ↓
                                              Staged review (section by section)
                                                          ↓
                                              Optional: scaffold project
```

- [ ] **Step 2: Add protocols table entry for rules assembly**

Add to the protocols table:

```markdown
| Rules Assembly | `templates/rules/_rules-assembly.md` | How rules fragments are structured |
```

- [ ] **Step 3: Update TODO.md — remove completed item, add new items if any**

Add to the top of TODO.md:

```markdown
### 4. Rules output 集成测试（中优先级）
- 多文件输出策略已定义但未在真实项目中验证
- 需要用 team-monorepo 场景做一次完整 dry-run
- **建议**: 在下次有人使用 monorepo 项目运行 kickoff 时记录反馈
```

- [ ] **Step 4: Commit**

```bash
git add agents/kickoff/SKILL.md agents/kickoff/TODO.md
git commit -m "docs(kickoff): update SKILL.md and TODO.md for rules output support"
```
