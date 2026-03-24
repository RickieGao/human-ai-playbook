# Decision Tree

Maps interview answers to template fragment selections.

---

## Base Fragments (always included)

Every generated CLAUDE.md includes:
- `base/project-identity.md` - Project name, description, tech stack
- `base/collaboration-mode.md` - Workflow and communication preferences
- `base/quality-standards.md` - Testing and review standards
- `base/context-management.md` - Context window and memory guidelines

## Workflow Selection

```
Q: Which workflow?
├── TDD          -> include workflow/tdd-workflow.md
├── Plan-first   -> include workflow/plan-first-workflow.md
├── Spec-driven  -> include workflow/spec-driven-workflow.md
└── Incremental  -> include workflow/incremental-workflow.md
```

## Scale Selection

```
Q: Team size?
├── Solo         -> include scale/solo-developer.md
├── Small (2-5)  -> include scale/small-team.md
└── Large / OSS  -> include scale/monorepo.md
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

## Autonomy Level Adjustments

```
Q: AI autonomy?
├── Strict   -> Add: "Always wait for confirmation before applying changes"
├── Moderate -> Add: "Execute plan steps, pause at checkpoints for review"
└── High     -> Add: "Work independently, present results at PR level"
```

## Output Assembly Order

1. Project Identity (base)
2. Collaboration Mode (base + workflow)
3. Quality Standards (base)
4. Context Management (base)
5. Scale-specific guidelines
6. Domain-specific guidelines (if applicable)
7. Custom pitfalls and conventions (from Round 3)
