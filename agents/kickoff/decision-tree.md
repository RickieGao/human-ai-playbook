# Decision Tree

Maps interview answers to template fragment selections.

---

## Base Fragments (always included)

Every generated CLAUDE.md includes:
- `base/project-identity.md` - Project name, description, tech stack
- `base/collaboration-mode.md` - Workflow and communication preferences
- `base/quality-standards.md` - Testing and review standards
- `base/context-management.md` - Context window and memory guidelines

## Workflow Selection (from Q1 — Work Rhythm)

```
Q1: "You ask AI to implement a user login feature. How should AI work?"
├── a) Plan first, wait for approval    → include workflow/plan-first-workflow.md
├── b) Code in small steps, show each   → include workflow/incremental-workflow.md
└── c) Complete whole feature, review end → include workflow/incremental-workflow.md

Note: If Q1-a AND Q4-a (full mode), consider TDD workflow instead:
├── Q1-a + Q4-a (strict testing)  → include workflow/tdd-workflow.md
└── Q1-a + Q4-b or Q4-c           → include workflow/plan-first-workflow.md
```

## Scale Selection

Scale is determined differently by path:

### Path A (existing project)
Inferred from project scan:
```
├── 1 contributor (last 30 days)     → include scale/solo-developer.md
├── 2-5 contributors                 → include scale/small-team.md
└── 5+ contributors or monorepo     → include scale/monorepo.md
```

### Path B (new project)
Inferred from user context during needs clarification:
```
├── Solo / personal project          → include scale/solo-developer.md
├── Small team (2-5)                 → include scale/small-team.md
└── Large team / open source         → include scale/monorepo.md
```

## Domain Selection (future)

```
Q: Project domain?
├── Web frontend  -> include domain/web-frontend.md (planned)
├── Backend API   -> include domain/backend-api.md (planned)
├── Mobile        -> include domain/mobile.md (planned)
├── Data/ML       -> include domain/data-ml.md (planned)
└── Other         -> no domain fragment
```

## Autonomy Level (from Q1 + Q2)

Autonomy is derived from the combination of Q1 (work rhythm) and Q2 (unexpected handling):

### Primary (from Q1)
```
├── Q1-a (plan first)      → Base: strict
├── Q1-b (small steps)     → Base: moderate
└── Q1-c (complete feature) → Base: high
```

### Modifier (from Q2)
```
├── Q2-a (only do asked)   → Confirm or tighten autonomy
├── Q2-b (ask about extras) → Confirm moderate
└── Q2-c (fix along the way) → Confirm or loosen autonomy
```

### Result
```
├── Strict   → Add: "Always wait for confirmation before applying changes. Do not modify files outside the explicit request."
├── Moderate → Add: "Execute plan steps, pause at checkpoints for review. Report discovered issues but don't fix without approval."
└── High     → Add: "Work independently, present results at PR level. Fix related issues proactively and report what changed."
```

## Communication Style (from Q3)

```
Q3: "After AI completes a task, how should it report?"
├── Q3-a (detailed explanation)  → communication: verbose
├── Q3-b (brief summary)        → communication: concise
└── Q3-c (just code diff)       → communication: minimal
```

No template fragment selection needed — the value is injected directly via `{{communication_style_description}}` placeholder.

## Additional Preferences (Full Mode Q4-Q7)

### Testing (from Q4)
```
├── Q4-a (every feature tested)     → Add strict testing requirements to quality-standards
├── Q4-b (core logic tested)        → Add moderate testing requirements
└── Q4-c (tests later)              → Add minimal testing requirements
```

### Review Process (from Q5)
```
├── Q5-a (every file change)        → review: every-change
├── Q5-b (per feature)              → review: per-feature
└── Q5-c (PR level)                 → review: per-pr
```

### Known Pitfalls (Q6) and Safety Red Lines (Q7)
Direct insertion into respective CLAUDE.md sections. No template mapping needed.

## Output Assembly Order

1. Project Identity (base)
2. Collaboration Mode (base + workflow)
3. Quality Standards (base)
4. Context Management (base)
5. Scale-specific guidelines
6. Domain-specific guidelines (if applicable)
7. Custom pitfalls, safety constraints, and conventions (from scenario questions)

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
