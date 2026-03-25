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

## After All Sections Confirmed

Write CLAUDE.md to project root directory.

> "CLAUDE.md has been written to your project root. This is a living document —
> update it anytime as your project evolves. AI will also suggest updates when
> it notices things have changed."

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
