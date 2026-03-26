# Staged Review

Section-by-section review of the generated CLAUDE.md. Builds user understanding
and ownership by explaining each section's purpose before asking for confirmation.

## Entry

CLAUDE.md draft has been generated (Stage 3 complete).

## Mode Detection

Check whether a CLAUDE.md already exists in the project root:

- **No existing CLAUDE.md → First-time mode**: Full section-by-section review with explanations
- **Existing CLAUDE.md → Update mode**: Diff-focused review (see below)

## First-Time Mode Process

Present CLAUDE.md in 4-5 sections. For each section:
1. Show the content
2. Explain its purpose in one sentence
3. For Path B users: add a concrete example of how this affects collaboration
4. Wait for user to confirm, modify, or add content
5. Only proceed to next section after confirmation

## Update Mode Process

Compare generated CLAUDE.md against existing content. Then:
1. List unchanged sections in one line: "Sections 1, 2, 5 unchanged — skipping."
2. For each section with differences, show a diff and explain what changed and why
3. Wait for user to confirm, modify, or reject each change
4. Apply only confirmed changes; preserve existing content for rejected/unchanged sections

### Handling custom sections

Existing CLAUDE.md files may contain sections that don't match any template section (e.g., domain-specific rules, architecture diagrams, communication protocols). These are user-authored content with high value.

Rules:
- **Never remove or replace custom sections.** They represent domain knowledge that templates cannot generate.
- When listing changes, explicitly acknowledge custom sections: "The following sections are unique to your project and will be preserved as-is: [list]."
- If a custom section overlaps with a template section (e.g., project-specific testing rules vs. template Quality Standards), keep the custom version and skip the template default.
- Custom sections retain their original position in the document.

### Quality comparison principle

When existing content is more specific or detailed than the template default, preserve the existing content. Templates provide a starting point; they should not dilute a well-crafted CLAUDE.md.

Examples:
- Existing: "单笔最大亏损：账户余额的1%" → better than template default "Add safety constraints here"
- Existing: detailed architecture diagram → better than template's generic "Project description"
- Existing: domain-specific testing process → better than template's generic "Run `{{test_command}}`"

Only suggest template content when the existing CLAUDE.md is missing a section entirely.

## Sections

### Section 1: Project Identity

Show: Project name, description, tech stack, common commands.

> **What this does**: AI reads this first every session to understand what your project
> is and how to run it.

Path B extra: "For example, if you later add a database, you'd update the tech stack
and add migration commands here."

### Section 2: Collaboration Mode

Show: Workflow, scope handling, communication style, review process.

> **What this does**: This is your 'working contract' with AI. It will strictly follow
> these rules. For instance, it won't refactor code without your permission.

### Section 3: Quality Standards

Show: Testing requirements, commit conventions (including granularity and timing guidance), code style.

> **What this does**: Ensures AI produces consistent quality. Without this, AI might
> write tests sometimes and skip them other times.

**Review checkpoint**: Verify the Commits subsection includes:
- Atomic commit principle (one commit = one independent change)
- Proactive commit reminders (AI reminds user after completing a logical unit)
- No-mix rule (content, config, and cross-file fixes stay separate)

If missing, add from the `quality-standards.md` template before proceeding.

### Section 4: Guardrails and Pitfalls

Show: Known pitfalls, safety constraints, prohibited actions.

> **What this does**: This is the 'safety fence' — the most important section, because
> this contains knowledge AI cannot infer from your code.

Path B extra: "This section might be thin right now. As your project grows, you'll
discover more gotchas — come back and add them."

### Section 5: Context Management (if applicable)

Show: CLAUDE.md maintenance rules, session management, self-update mechanism.

> **What this does**: Keeps your CLAUDE.md alive and accurate as the project evolves.

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

Then offer optional scaffold:

> "Would you like me to initialize the project? (Create directory structure,
> install dependencies, set up toolchain)"

- If yes: proceed with scaffolding based on project type and tech summary
- If no: flow ends

## Scaffold Guidelines by Project Type

### All projects
- Initialize git repository
- Create `.gitignore` tailored to the tech stack
- Create directory structure as defined in CLAUDE.md

### Application projects
- Initialize package manager (`uv init`, `npm init`, etc.)
- Set up linter/formatter config
- Add a minimal test scaffold

### Documentation projects
- Create doc templates in target directories

### Research / Data projects
- `.gitignore` must explicitly block data files (`.csv`, `.xlsx`, `.pkl`, `.parquet`, etc.) to prevent accidental data leaks
- If a reference prompt/doc exists, offer to reorganize it into the project structure (e.g., `docs/research-context.md`)
- Create placeholder directories for outputs (`papers/`, `references/`, `logs/`, etc.)

### Docs + Automation projects
- Create workflow scaffolds with `workflow_dispatch` for manual testing
- Add placeholder scripts in automation directories
